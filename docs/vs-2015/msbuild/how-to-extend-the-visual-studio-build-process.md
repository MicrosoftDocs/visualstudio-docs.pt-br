---
title: 'Como: Estender o processo de Build | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSBuild, overriding predefined targets
- MSBuild, overriding DependsOn properties
- MSBuild, extending Visual Studio builds
- MSBuild, DependsOn properties
ms.assetid: cb077613-4a59-41b7-96ec-d8516689163c
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e552b75ea5ba34004d0c53850f1af77a120b20cb
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53050251"
---
# <a name="how-to-extend-the-visual-studio-build-process"></a>Como: Estender o processo de build do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]


O processo de build [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é definido por uma série de arquivos .targets [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] que são importados para seu arquivo de projeto. Um desses arquivos importados, Microsoft.Common.targets, pode ser estendido para permitir a execução de tarefas personalizadas em vários pontos no processo de build. Este tópico explica os dois métodos que você pode usar para estender o processo de build do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]:

-   Substituindo destinos predefinidos específicos definidos no Microsoft.Common.targets.

-   Substituindo as propriedades “DependsOn” definidas no Microsoft.Common.targets.

## <a name="overriding-predefined-targets"></a>Substituindo destinos predefinidos
 O arquivo Microsoft.Common.targets contém um conjunto de destinos vazios predefinidos que são chamados antes e depois de alguns dos principais destinos no processo de build. Por exemplo, [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] chama o destino `BeforeBuild` antes do destino `CoreBuild` principal e o destino `AfterBuild` após o destino `CoreBuild`. Por padrão, os destinos vazios Microsoft.Common.targets não fazem nada, mas você pode substituir o comportamento padrão definindo os destinos que você desejar em um arquivo de projeto que importa o Microsoft.Common.targets. Fazendo isso, você pode usar as tarefas [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] para obter maior controle sobre o processo de build.

#### <a name="to-override-a-predefined-target"></a>Para substituir um destino predefinido

1. Identifique um destino predefinido em Microsoft.Common.targets que você deseja substituir. Consulte a tabela abaixo para obter uma lista completa de destinos que você pode substituir com segurança.

2. Defina o destino ou destinos no final do arquivo de projeto, imediatamente antes da marca `</Project>`. Por exemplo:

   ```
   <Project>
       ...
       <Target Name="BeforeBuild">
           <!-- Insert tasks to run before build here -->
       </Target>
       <Target Name="AfterBuild">
           <!-- Insert tasks to run after build here -->
       </Target>
   </Project>
   ```

3. Compile o arquivo de projeto.

   A tabela a seguir mostra todos os destinos no Microsoft.Common.targets que você pode substituir com segurança.

|Nome de Destino|Descrição|
|-----------------|-----------------|
|`BeforeCompile`, `AfterCompile`|Tarefas inseridas em um desses destinos são executadas antes ou após a conclusão da compilação principal. A maioria das personalizações é realizada em um desses dois destinos.|
|`BeforeBuild`, `AfterBuild`|Tarefas inseridas em um desses destinos serão executadas antes ou depois de todo o resto no build. **Observação:**  O `BeforeBuild` e `AfterBuild` destinos já estão definidos nos comentários no final da maioria dos arquivos de projeto. Isso permite que você adicione facilmente os eventos de pré e pós-build ao arquivo de projeto.|
|`BeforeRebuild`, `AfterRebuild`|Tarefas inseridas em um desses alvos são executadas antes ou depois que a funcionalidade de recompilação do núcleo é invocada. A ordem de execução de destino em Microsoft.Common.targets é: `BeforeRebuild`, `Clean`, `Build` e `AfterRebuild`.|
|`BeforeClean`, `AfterClean`|Tarefas inseridas em um desses destinos são executadas antes ou depois da funcionalidade de limpeza do núcleo ser invocada.|
|`BeforePublish`, `AfterPublish`|Tarefas inseridas em um desses destinos são executadas antes ou depois da funcionalidade de publicação do núcleo ser invocada.|
|`BeforeResolveReference`, `AfterResolveReferences`|Tarefas inseridas em um desses destinos são executadas antes ou após as referências de assembly serem resolvidas.|
|`BeforeResGen`, `AfterResGen`|Tarefas inseridas em um desses destinos são executadas antes ou após os recursos serem gerados.|

## <a name="overriding-dependson-properties"></a>Substituindo propriedades “DependsOn”
 Substituir destinos predefinidos é uma maneira fácil de estender o processo de build, mas, como [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] avalia a definição de destinos sequencialmente, não há nenhuma maneira de impedir que outro projeto que importa seu projeto substitua os destinos que você já substituiu. Dessa forma, por exemplo, o último destino `AfterBuild` no arquivo de projeto, depois que todos os outros projetos foram importados, será aquele usado durante o build.

 Você pode se proteger contra substituições indesejadas de destinos substituindo as propriedades “DependsOn” que são usadas em atributos `DependsOnTargets` por todo o arquivo Microsoft.Common.targets. Por exemplo, o destino `Build` contém um valor de atributo `DependsOnTargets` de `"$(BuildDependsOn)"`. Considere:

```
<Target Name="Build" DependsOnTargets="$(BuildDependsOn)"/>
```

 Este trecho de XML indica que, antes de poder executar o destino `Build`, todos os destinos especificados na propriedade `BuildDependsOn` devem ser executados primeiro. A propriedade `BuildDependsOn` está definida como:

```
<PropertyGroup>
    <BuildDependsOn>
        BeforeBuild;
        CoreBuild;
        AfterBuild
    </BuildDependsOn>
</PropertyGroup>
```

 Você pode substituir esse valor da propriedade declarando outra propriedade denominada `BuildDependsOn` no final do seu arquivo de projeto. Incluindo a propriedade `BuildDependsOn` anterior na nova propriedade, você pode adicionar novos destinos no início e fim da lista de destinos. Por exemplo:

```
<PropertyGroup>
    <BuildDependsOn>
        MyCustomTarget1;
        $(BuildDependsOn);
        MyCustomTarget2
    </BuildDependsOn>
</PropertyGroup>

<Target Name="MyCustomTarget1">
    <Message Text="Running MyCustomTarget1..."/>
</Target>
<Target Name="MyCustomTarget2">
    <Message Text="Running MyCustomTarget2..."/>
</Target>
```

 Projetos que importam seus arquivos de projeto podem substituir essas propriedades sem substituir as personalizações que você fez.

#### <a name="to-override-a-dependson-property"></a>Para substituir uma propriedade “DependsOn”

1.  Identifique uma propriedade “DependsOn” predefinida no Microsoft.Common.targets que você deseja substituir. Consulte a tabela abaixo para obter uma lista das propriedades “DependsOn” comumente substituídas.

2.  Defina outra instância da propriedade ou propriedades no final do seu arquivo de projeto. Inclua a propriedade original, por exemplo `$(BuildDependsOn)`, na nova propriedade.

3.  Defina seus destinos personalizados antes ou após a definição da propriedade.

4.  Compile o arquivo de projeto.

### <a name="commonly-overridden-dependson-properties"></a>Propriedades “DependsOn” geralmente substituídas

|Nome da Propriedade|Descrição|
|-------------------|-----------------|
|`BuildDependsOn`|A propriedade a ser substituída se você quiser inserir destinos personalizados antes ou após o processo inteiro de build.|
|`CleanDependsOn`|A propriedade a ser substituída você quiser limpar a saída do seu processo de build personalizado.|
|`CompileDependsOn`|A propriedade a ser substituída se você quiser inserir processos personalizados antes ou após a etapa de compilação.|

## <a name="see-also"></a>Consulte também
 [Integração do Visual Studio](../msbuild/visual-studio-integration-msbuild.md) [conceitos do MSBuild](../msbuild/msbuild-concepts.md) [. Arquivos de destino](../msbuild/msbuild-dot-targets-files.md)
