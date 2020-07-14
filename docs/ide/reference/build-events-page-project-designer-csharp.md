---
title: Página Eventos de Build, Designer de Projeto (C#)
ms.date: 10/17/2019
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesBuildEvents
helpviewer_keywords:
- build events
- Project Designer, Build Events page
- pre-build events
- post-build events
ms.assetid: 3fff9ae5-213c-46ea-a660-1d70acb6c922
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: a56093ab14b9be72f99e36b03eefe7abb895183f
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85419049"
---
# <a name="build-events-page-project-designer-c"></a>Página Eventos de Build, Designer de Projeto (C#)

Use a página **Eventos de Build** do **Designer de Projeto** para especificar as instruções de configuração de build. Você também pode especificar as condições sob as quais eventos pós-build são executados. Para obter mais informações, consulte [como: especificar eventos de compilação (C#)](../../ide/how-to-specify-build-events-csharp.md) e [como especificar eventos de compilação (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md).

## <a name="uielement-list"></a>Lista de elementos de interface do usuário

**Configuration**

Esse controle não é editável nesta página. Para obter uma descrição desse controle, consulte [Página de Build, Designer de Projeto (C#)](../../ide/reference/build-page-project-designer-csharp.md).

**Plataforma**

Esse controle não é editável nesta página. Para obter uma descrição desse controle, consulte [Página de Build, Designer de Projeto (C#)](../../ide/reference/build-page-project-designer-csharp.md).

**Linha de comando de evento de pré-compilação**

Especifica comandos serem executados antes do início do build. Para digitar comandos longos, clique em **Editar Pré-Build** para exibir a [Caixa de Diálogo Linha de Comando de Evento de Pré-Build/Evento de Pós-Build](../../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md).

> [!NOTE]
> Eventos de pré-build não serão executados se o projeto estiver atualizado e nenhum build será disparado.

**Linha de comando de eventos pós-compilação**

Especifica comandos a serem executados após o fim do build. Para digitar comandos longos, clique em **Editar pós-compilação** para exibir a caixa de diálogo linha de comando do evento de **pré-compilação evento/pós-** compilação.

> [!NOTE]
> Adicione uma instrução `call` antes de todos os comandos pós-build que executam arquivos .bat. Por exemplo, `call C:\MyFile.bat` ou `call C:\MyFile.bat call C:\MyFile2.bat`.

**Executar o evento pós-compilação**

Especifica as condições a seguir para o evento de pós-build ser executado, conforme mostrado na tabela a seguir.

|Opção|Result|
|------------|------------|
|**Constante**|O evento de pós-build será executado independentemente de o build ser bem-sucedido.|
|**Na compilação bem-sucedida**|O evento de pós-build será executado se o build for bem-sucedido. Assim, o evento será executado mesmo para um projeto atualizado, desde que o build seja bem-sucedido.|
|**Quando o build atualizar a saída do projeto**|O evento de pós-build só será executado quando o arquivo de saída do compilador (.exe ou .dll) for diferente do arquivo de saída anterior do compilador. Portanto, um evento de pós-build não será executado se um projeto for atualizado.|

## <a name="in-the-project-file"></a>No arquivo de projeto

Em versões anteriores do Visual Studio, quando você altera a configuração **PreBuildEvent** ou **PostBuildEvent** no IDE, o Visual Studio adiciona uma `PreBuildEvent` `PostBuildEvent` propriedade ou ao arquivo de projeto. Por exemplo, se a configuração de linha de comando **PreBuildEvent** no IDE for a seguinte:

```input
"$(ProjectDir)PreBuildEvent.bat" "$(ProjectDir)..\" "$(ProjectDir)" "$(TargetDir)"
```

em seguida, a configuração do arquivo de projeto é:

```xml
<PropertyGroup>
    <PreBuildEvent>"$(ProjectDir)PreBuildEvent.bat" "$(ProjectDir)..\" "$(ProjectDir)" "$(TargetDir)" />
</PropertyGroup>
```

Para projetos do .NET Core, o Visual Studio 2019 (e o Visual Studio 2017 em atualizações mais recentes) adiciona um destino do MSBuild denominado `PreBuild` ou `PostBuild` para configurações de **PreBuildEvent** e **PostBuildEvent** . Esses destinos usam os atributos **BeforeTargets** e **AfterTargets** , que o MSBuild reconhece. Por exemplo, para o exemplo anterior, o Visual Studio agora gera o seguinte código:

```xml
<Target Name="PreBuild" BeforeTargets="PreBuildEvent">
    <Exec Command="&quot;$(ProjectDir)PreBuildEvent.bat&quot; &quot;$(ProjectDir)..\&quot; &quot;$(ProjectDir)&quot; &quot;$(TargetDir)&quot;" />
</Target>
```

Para um evento de pós-compilação, use o nome `PostBuild` e defina o atributo `AfterTargets` como `PostBuildEvent` .

```xml
<Target Name="PostBuild" AfterTargets="PostBuildEvent">
   <Exec Command="echo Output written to $(TargetDir)" />
</Target>
```

> [!NOTE]
> Essas alterações de arquivo de projeto foram feitas para dar suporte a projetos no estilo SDK. Se você estiver migrando um arquivo de projeto do formato antigo para o formato de estilo SDK manualmente, deverá excluir as `PreBuildEvent` `PostBuildEvent` Propriedades e e substituí-las `PreBuild` pelos `PostBuild` destinos e conforme mostrado no código anterior. Para saber como saber se seu projeto é um projeto no estilo SDK, consulte verificar o [formato do projeto](/nuget/resources/check-project-format).

## <a name="see-also"></a>Veja também

- [Como especificar eventos de build (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)
- [Como especificar eventos de build (C#)](../../ide/how-to-specify-build-events-csharp.md)
- [Referência de propriedades do projeto](../../ide/reference/project-properties-reference.md)
- [Compilando e criando](../../ide/compiling-and-building-in-visual-studio.md)
