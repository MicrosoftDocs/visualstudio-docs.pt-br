---
title: MSBuild | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, about MSBuild
- MSBuild, overview
ms.assetid: e39f13f7-1e1d-4435-95ca-0c222bca071c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c1bd4c4ab15364e9e2ac8e189fcde01f65244b7a
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289190"
---
# <a name="msbuild"></a>MSBuild

A Microsoft Build Engine é uma plataforma para a criação de aplicativos. Esse mecanismo, que é também conhecido como MSBuild, fornece um esquema XML para um arquivo de projeto que controla como a plataforma de build processa e compila software. O Visual Studio usa o MSBuild, mas o MSBuild não depende do Visual Studio. Ao invocar o *msbuild.exe* no seu arquivo de projeto ou solução, você pode organizar e criar produtos em ambientes em que o Visual Studio não está instalado.

 O Visual Studio usa o MSBuild para carregar e compilar projetos gerenciados. Os arquivos de projeto no Visual Studio (*.csproj*, *.vbproj*, *.vcxproj* e outros) contêm o código XML do MSBuild que é executado ao compilar um projeto usando o IDE. Os projetos do Visual Studio importam toas as configurações e processos de build necessários para realizar o trabalho de desenvolvimento típico, mas você pode estendê-las ou modificá-las de dentro do Visual Studio ou usando um editor de XML.

 Para obter informações sobre o MSBuild para C++, consulte [MSBuild (C++)](/cpp/build/msbuild-visual-cpp).

 Os exemplos a seguir ilustram quando você pode executar compilações invocando o MSBuild da linha de comando em vez do IDE do Visual Studio.

- O Visual Studio não está instalado. ([Baixe o MSBuild sem o Visual Studio](https://visualstudio.microsoft.com/downloads/?q=build+tools).)

- Você deseja usar a versão de 64 bits do MSBuild. Esta versão do MSBuild normalmente não é necessária, mas permite que o MSBuild acesse mais memória.

- Você deseja executar um build em vários processos. No entanto, você pode usar o IDE para alcançar o mesmo resultado em projetos em C++ e C#.

- Você deseja modificar o sistema de build. Por exemplo, você talvez queira habilitar as seguintes ações:

  - Pré-processar arquivos antes de eles chegarem ao compilador.

  - Copiar as saídas de build para um local diferente.

  - Criar arquivos compactados de saídas de build.

  - Realizar uma etapa de pós-processamento. Por exemplo, convém marcar um assembly com uma versão diferente.

Você pode escrever código no IDE do Visual Studio, mas executar os builds usando o MSBuild. Como outra alternativa, você pode criar código no IDE em um computador de desenvolvimento, mas executar o MSBuild na linha de comando para compilar o código que é integrado a vários desenvolvedores. Você também pode usar a [CLI (interface de linha de comando) do .NET Core](/dotnet/core/tools/), que usa o MSBuild, para compilar projetos do .NET Core.

> [!NOTE]
> Você pode usar Azure Pipelines para compilar, testar e implantar automaticamente seu aplicativo. O sistema de build pode executar builds automaticamente quando os desenvolvedores fazem o check-in de código (por exemplo, como parte de uma estratégia de Integração Contínua) ou de acordo com um cronograma (por exemplo, um build de teste de aceitação pós-build noturno). Azure Pipelines compila seu código usando o MSBuild. Para obter mais informações, confira [Azure Pipelines](/azure/devops/pipelines/index?view=vsts).

Este artigo fornece uma visão geral do MSBuild. Para um tutorial de introdução, consulte [Instruções passo a passo: usando o MSBuild](../msbuild/walkthrough-using-msbuild.md).

## <a name="use-msbuild-at-a-command-prompt"></a>Usar MSBuild em um prompt de comando

 Para executar o MSBuild em um prompt de comando, passe um arquivo de projeto para *MSBuild.exe*, junto com as opções de linha de comando apropriadas. As opções de linha de comando permitem que você defina propriedades, execute destinos específicos e defina outras opções que controlam o processo de build. Por exemplo, você usaria a seguinte sintaxe de linha de comando para criar o arquivo *MyProj.proj* com a propriedade `Configuration` definida como `Debug`.

```cmd
MSBuild.exe MyProj.proj -property:Configuration=Debug
```

 Para obter mais informações sobre opções de linha de comando do MSBuild, consulte [referência de linha de comando](../msbuild/msbuild-command-line-reference.md).

> [!IMPORTANT]
> Antes de baixar um projeto, determine a confiabilidade do código.

## <a name="project-file"></a>Arquivo de projeto

 O MSBuild usa um formato de arquivo de projeto baseado em XML que é simples e extensível. O formato de arquivo de projeto do MSBuild permite que os desenvolvedores descrevam os itens que devem ser criados e também como eles devem ser criados para diferentes sistemas operacionais e configurações. Além disso, o formato de arquivo de projeto permite aos desenvolvedores criar regras de build reutilizáveis que podem ser fatoradas em arquivos separados para que os builds possam ser realizados de forma consistente entre os diferentes projetos no produto.

 As seções a seguir descrevem alguns dos elementos básicos do formato de arquivo de projeto do MSBuild. Para obter um tutorial sobre como criar um arquivo de projeto básico, consulte [Passo a passo: criar um arquivo de projeto do MSBuild do zero](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md).

### <a name="properties"></a><a name="BKMK_Properties"></a> Propriedades

 As propriedades representam pares chave-valor que podem ser usados para configurar builds. As propriedades são declaradas com a criação de um elemento que tem o nome da propriedade como um filho de um elemento [PropertyGroup](../msbuild/propertygroup-element-msbuild.md). Por exemplo, o código a seguir cria uma propriedade chamada `BuildDir` que tem um valor de `Build`.

```xml
<PropertyGroup>
    <BuildDir>Build</BuildDir>
</PropertyGroup>
```

 Você pode definir uma propriedade condicionalmente colocando um atributo `Condition` no elemento. O conteúdo dos elementos condicionais é ignorado a menos que a condição seja avaliada como `true`. No exemplo a seguir, o elemento `Configuration` será definido se ainda não tiver sido definido.

```xml
<Configuration  Condition=" '$(Configuration)' == '' ">Debug</Configuration>
```

 As propriedades podem ser referenciadas em todo o arquivo de projeto usando a sintaxe $ ( \<PropertyName> ). Por exemplo, você pode fazer referência às propriedades nos exemplos anteriores usando `$(BuildDir)` e `$(Configuration)`.

 Para obter mais informações sobre propriedades, confira [Propriedades do MSBuild](../msbuild/msbuild-properties.md).

### <a name="items"></a><a name="BKMK_Items"></a>Los

 Os itens são entradas no sistema de build e normalmente representam arquivos. Os itens são agrupados em tipos de item com base em nomes de itens definidos pelo usuário. Esses tipos de item podem ser usados como parâmetros para tarefas, que usam os itens individuais para executar as etapas do processo de build.

 Os itens são declarados no arquivo de projeto, criando um elemento que tem o nome do tipo de item como um filho de um elemento [ItemGroup](../msbuild/itemgroup-element-msbuild.md). Por exemplo, o código a seguir cria um tipo de item chamado `Compile`, que inclui dois arquivos.

```xml
<ItemGroup>
    <Compile Include = "file1.cs"/>
    <Compile Include = "file2.cs"/>
</ItemGroup>
```

 Os tipos de item podem ser referenciados em todo o arquivo de projeto usando a sintaxe @ ( \<ItemType> ). Por exemplo, o tipo de item no exemplo seria referenciado usando `@(Compile)`.

 No MSBuild, os nomes de elementos e atributos diferenciam maiúsculas de minúsculas. No entanto, os nomes de propriedade, item e metadados não. O exemplo a seguir cria o tipo de item `Compile`, `comPile` ou qualquer outra variação de maiúsculas e minúsculas e fornece ao tipo de item o valor "one.cs;two.cs".

```xml
<ItemGroup>
  <Compile Include="one.cs" />
  <comPile Include="two.cs" />
</ItemGroup>
```

 Os itens podem ser declarados usando caracteres curinga e podem conter metadados adicionais para cenários de build mais avançados. Para obter mais informações sobre os itens, consulte [Itens](../msbuild/msbuild-items.md).

### <a name="tasks"></a><a name="BKMK_Tasks"></a>Tarefa

 Tarefas são unidades de código executável que os projetos do MSBuild usam para executar operações de compilação. Por exemplo, uma tarefa pode compilar os arquivos de entrada ou executar uma ferramenta externa. As tarefas podem ser reutilizadas e podem ser compartilhadas por diferentes desenvolvedores em projetos diferentes.

 A lógica de execução de uma tarefa é escrita em código gerenciado e mapeada para o MSBuild usando o elemento [UsingTask](../msbuild/usingtask-element-msbuild.md) . Você pode escrever sua própria tarefa por meio da criação de um tipo gerenciado que implementa a interface <xref:Microsoft.Build.Framework.ITask>. Para obter mais informações sobre como escrever tarefas, consulte [gravação de tarefas](../msbuild/task-writing.md).

 O MSBuild inclui tarefas comuns que você pode modificar para atender às suas necessidades. Os exemplos são [Copy](../msbuild/copy-task.md), que copia arquivos, [MakeDir](../msbuild/makedir-task.md), que cria diretórios e [Csc](../msbuild/csc-task.md), que compila os arquivos de código-fonte do Visual C#. Para obter uma lista das tarefas disponíveis juntamente com as informações de uso, consulte [Referência das tarefas](../msbuild/msbuild-task-reference.md).

 Uma tarefa é executada em um arquivo de projeto do MSBuild criando um elemento que tem o nome da tarefa como um filho de um elemento de [destino](../msbuild/target-element-msbuild.md) . As tarefas normalmente aceitam parâmetros, que são passados como atributos do elemento. As propriedades e os itens do MSBuild podem ser usados como parâmetros. Por exemplo, o código a seguir chama a tarefa [MakeDir](../msbuild/makedir-task.md) e passa para ela o valor da propriedade `BuildDir` que foi declarada em um exemplo anterior.

```xml
<Target Name="MakeBuildDirectory">
    <MakeDir  Directories="$(BuildDir)" />
</Target>
```

 Para obter mais informações sobre as tarefas, consulte [Tarefas](../msbuild/msbuild-tasks.md).

### <a name="targets"></a><a name="BKMK_Targets"></a>Aos

 Os destinos agrupam tarefas em uma ordem específica e expõe seções do arquivo de projeto como pontos de entrada para o processo de build. Os destinos geralmente são agrupados em seções lógicas para aumentar a legibilidade e para permitir a expansão. Dividir as etapas de build em destinos permite que você chame uma parte do processo de build de outros destinos sem copiar essa seção do código em cada destino. Por exemplo, se vários pontos de entrada no processo de build precisam de referências para serem compilados, você pode criar um destino que compila as referências e, em seguida, executar esse destino de todos os pontos de entrada em que ele é necessário.

 Os destinos são declarados no arquivo de projeto usando o elemento [Target](../msbuild/target-element-msbuild.md). Por exemplo, o código a seguir cria um destino chamado `Compile`, que, em seguida, chama a tarefa [Csc](../msbuild/csc-task.md) que tem a lista de itens declarada no exemplo anterior.

```xml
<Target Name="Compile">
    <Csc Sources="@(Compile)" />
</Target>
```

 Em cenários mais avançados, os destinos podem ser usados para descrever relações entre si e executar a análise de dependência para que seções inteiras do processo de build possam ser ignoradas se o destino estiver atualizado. Para obter mais informações sobre destinos, consulte [Destinos](../msbuild/msbuild-targets.md).

## <a name="build-logs"></a>Logs de build

 Você pode registrar erros de build, avisos e mensagens para o console ou outro dispositivo de saída. Para saber mais, confira [Obter logs de build](../msbuild/obtaining-build-logs-with-msbuild.md) e [Registrar em logs no MSBuild](../msbuild/logging-in-msbuild.md).

## <a name="use-msbuild-in-visual-studio"></a>Usar MSBuild no Visual Studio

 O Visual Studio usa o formato de arquivo de projeto do MSBuild para armazenar informações de compilação sobre projetos gerenciados. As configurações do projeto que são adicionadas ou alteradas usando a interface do Visual Studio são refletidas no *. \* arquivo proj* que é gerado para cada projeto. O Visual Studio usa uma instância hospedada do MSBuild para criar projetos gerenciados. Isso significa que um projeto gerenciado pode ser criado no Visual Studio ou em um prompt de comando (mesmo que o Visual Studio não esteja instalado) e os resultados serão idênticos.

 Para obter um tutorial sobre como usar o MSBuild no Visual Studio, consulte [Instruções passo a passo: usando o MSBuild](../msbuild/walkthrough-using-msbuild.md).

## <a name="multitargeting"></a><a name="BKMK_Multitargeting"></a>Multidirecionamento

 Usando o Visual Studio, você pode compilar um aplicativo para ser executado em qualquer uma das várias versões do .NET Framework. Por exemplo, você pode compilar um aplicativo para ser executado no .NET Framework 2,0 em uma plataforma de 32 bits e pode compilar o mesmo aplicativo para ser executado em .NET Framework 4,5 em uma plataforma de 64 bits. A capacidade de compilar para mais de uma estrutura é chamada de multiplataforma.

 Estes são alguns dos benefícios de multiplataforma:

- Você pode desenvolver aplicativos destinados a versões anteriores do .NET Framework, por exemplo, versões 2,0, 3,0 e 3,5.

- Você pode direcionar estruturas diferentes de .NET Framework, por exemplo, Silverlight.

- Você pode direcionar um *perfil de estrutura*, que é um subconjunto predefinido de uma estrutura de destino.

- Se uma service pack para a versão atual do .NET Framework for lançada, você poderá direcioná-la.

- A multiplataforma garante que um aplicativo use apenas a funcionalidade que está disponível na estrutura de destino e na plataforma.

Para obter mais informações, consulte [multidirecionamento](../msbuild/msbuild-multitargeting-overview.md).

## <a name="see-also"></a>Veja também

| Title | Descrição |
| - | - |
| [Walkthrough: Criando um arquivo de projeto do MSBuild do zero](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md) | Mostra como criar um arquivo de projeto básico de forma incremental, usando somente um editor de texto. |
| [Instruções passo a passo: usando o MSBuild](../msbuild/walkthrough-using-msbuild.md) | Apresenta os blocos de construção do MSBuild e mostra como escrever, manipular e depurar projetos do MSBuild sem fechar o IDE do Visual Studio. |
| [Conceitos do MSBuild](../msbuild/msbuild-concepts.md) | Apresenta os quatro blocos de construção do MSBuild: propriedades, itens, destinos e tarefas. |
| [Itens](../msbuild/msbuild-items.md) | Descreve os conceitos gerais por trás do formato de arquivo do MSBuild e como as peças se encaixam. |
| [Propriedades do MSBuild](../msbuild/msbuild-properties.md) | Introduz propriedades e coleções de propriedades. Propriedades são pares chave-valor que podem ser usados para configurar builds. |
| [Destinos](../msbuild/msbuild-targets.md) | Explica como agrupar tarefas em uma ordem específica e habilitar seções do processo de build a ser chamado na linha de comando. |
| [Tarefas](../msbuild/msbuild-tasks.md) | Mostra como criar uma unidade de código executável que pode ser usada pelo MSBuild para executar operações de compilação atômicas. |
| [Condições](../msbuild/msbuild-conditions.md) | Discute como usar o atributo `Condition` em um elemento do MSBuild. |
| [Conceitos avançados](../msbuild/msbuild-advanced-concepts.md) | Apresenta o envio em lote, a execução de transformações, a multiplataforma e outras técnicas avançadas. |
| [Registrando em log no MSBuild](../msbuild/logging-in-msbuild.md) | Descreve como registrar eventos de build, mensagens e erros. |
| [Como o MSBuild compila projetos](build-process-overview.md) | Descreve o processo de compilação interno usado no MSBuild |
| [Recursos adicionais](https://social.msdn.microsoft.com/forums/vstudio/home?forum=msbuild) | Lista os recursos de comunidade e suporte para obter mais informações sobre o MSBuild. |

## <a name="reference"></a>Referência

- [Referência do MSBuild](../msbuild/msbuild-reference.md)\
 Links para tópicos que contêm informações de referência.

- [Glossário](msbuild-glossary.md)\
 Define termos comuns do MSBuild.
