---
title: Separação em lotes no MSBuild | Microsoft Docs
ms.date: 06/09/2020
ms.topic: conceptual
helpviewer_keywords:
- batching [MSBuild]
- MSBuild, batching
ms.assetid: d35c085b-27b8-49d7-b6f8-8f2f3a0eec38
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6d7c72d1da270220144cd5e6167ebecb66462ba9
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289268"
---
# <a name="msbuild-batching"></a>Envio em lote do MSBuild

O MSBuild divide as listas de itens em diferentes categorias ou lotes, com base nos metadados do item, e executa um destino ou uma tarefa uma vez com cada lote.

## <a name="task-batching"></a>Envio de tarefas em lote

O lote de tarefas permite que você simplifique os arquivos de projeto ao fornecer uma maneira de dividir as listas de itens em lotes diferentes e passar cada um desses lotes para uma tarefa separadamente. Isso significa que um arquivo de projeto só precisa ter a tarefa e seus atributos declarados uma vez, mesmo que seja executado várias vezes.

Você especifica que deseja que o MSBuild execute o envio em lote com uma tarefa usando a `%(ItemMetaDataName)` notação em um dos atributos da tarefa. O exemplo a seguir divide a lista de itens `Example` em lotes com base no valor do item de metadados `Color` e passa cada um dos lotes para a tarefa `MyTask` separadamente.

> [!NOTE]
> Se você não fizer referência à lista de itens em outro lugar nos atributos da tarefa, ou se o nome dos metadados puder ser ambíguo, você poderá usar a notação%(<ItemCollection.>) para qualificar totalmente o valor dos metadados do item a ser usado para o envio em lote.

```xml
<Project
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <Example Include="Item1">
            <Color>Blue</Color>
        </Example>
        <Example Include="Item2">
            <Color>Red</Color>
        </Example>
    </ItemGroup>

    <Target Name="RunMyTask">
        <MyTask
            Sources = "@(Example)"
            Output = "%(Color)\MyFile.txt"/>
    </Target>

</Project>
```

Para obter exemplos mais específicos do envio em lote, confira [Metadados de item no envio de tarefas em lote](../msbuild/item-metadata-in-task-batching.md).

## <a name="target-batching"></a>Envio em lote de destinos

O MSBuild verifica se as entradas e saídas de um destino estão atualizadas antes de executar o destino. Se as entradas e saídas estiverem atualizadas, o destino será ignorado. Se uma tarefa dentro de um destino usar o envio em lote, o MSBuild precisará determinar se as entradas e saídas de cada lote de itens estão atualizadas. Caso contrário, o destino será executado toda vez que for atingido.

O exemplo a seguir mostra um `Target` elemento que contém um `Outputs` atributo com a `%(ItemMetadataName)` notação. O MSBuild dividirá a `Example` lista de itens em lotes com base nos `Color` metadados do item e analisará os carimbos de data/hora dos arquivos de saída para cada lote. Se as saídas de um lote não estiverem atualizadas, o destino será executado. Caso contrário, o destino será ignorado.

```xml
<Project
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <Example Include="Item1">
            <Color>Blue</Color>
        </Example>
        <Example Include="Item2">
            <Color>Red</Color>
        </Example>
    </ItemGroup>

    <Target Name="RunMyTask"
        Inputs="@(Example)"
        Outputs="%(Color)\MyFile.txt">
        <MyTask
            Sources = "@(Example)"
            Output = "%(Color)\MyFile.txt"/>
    </Target>

</Project>
```

Para obter outro exemplo de envio de destinos em lote, confira [Metadados de item no envio de destinos em lote](../msbuild/item-metadata-in-target-batching.md).

## <a name="item-and-property-mutations"></a>Mutações de item e Propriedade

Esta seção descreve como entender os efeitos da alteração de propriedades e/ou metadados de item, ao usar o lote de destino ou o envio em lote de tarefas.

Como o lote de destino e o envio em lote de tarefas são duas operações diferentes do MSBuild, é importante entender exatamente qual forma de envio em lote do MSBuild usa em cada caso. Quando a sintaxe de envio em lote `%(ItemMetadataName)` é exibida em uma tarefa em um destino, mas não em um atributo no destino, o MSBuild usa o envio em lote de tarefas. A única maneira de especificar o envio em lote de destino é usando a sintaxe de envio em lote em um atributo de destino, geralmente o `Outputs` atributo.

Com o lote de destino e o envio em lote de tarefas, os lotes podem ser considerados para serem executados de forma independente. Todos os lotes começam com uma cópia do mesmo estado inicial dos valores de metadados de propriedade e item. Qualquer mutação de valores de propriedade durante a execução do lote não é visível para outros lotes. Considere o exemplo a seguir:

```xml
  <ItemGroup>
    <Thing Include="2" Color="blue" />
    <Thing Include="1" Color="red" />
  </ItemGroup>

  <Target Name="DemoIndependentBatches">
    <ItemGroup>
      <Thing Condition=" '%(Color)' == 'blue' ">
        <Color>red</Color>
        <NeededColorChange>true</NeededColorChange>
      </Thing>
    </ItemGroup>
    <Message Importance="high"
             Text="Things: @(Thing->'%(Identity) is %(Color); needed change=%(NeededColorChange)')"/>
  </Target>
```

A saída é:

```output
Target DemoIndependentBatches:
  Things: 2 is red; needed change=true;1 is red; needed change=
```

O `ItemGroup` no destino é implicitamente uma tarefa e, com o `%(Color)` no `Condition` atributo, o envio em lote de tarefas é executado. Há dois lotes: um para vermelho e o outro para azul. A propriedade `%(NeededColorChange)` só será definida se os `%(Color)` metadados forem azuis e a configuração afetar apenas o item individual que correspondeu à condição quando o lote azul foi executado. O `Message` atributo da tarefa `Text` não dispara o envio em lote, apesar da `%(ItemMetadataName)` sintaxe, porque é usado dentro de uma transformação de item.

Os lotes são executados de forma independente, mas não em paralelo. Isso faz diferença quando você acessa os valores de metadados que são alterados na execução em lote. No caso em que você definir uma propriedade com base em alguns metadados na execução em lote, a propriedade usará o *último* valor definido:

```xml
   <PropertyGroup>
       <SomeProperty>%(SomeItem.MetadataValue)</SomeProperty>
   </PropertyGroup>
```

Após a execução em lote, a propriedade retém o valor final de `%(MetadataValue)` .

Embora os lotes sejam executados de forma independente, é importante considerar a diferença entre o lote de destino e o envio em lote de tarefas e saber qual tipo se aplica à sua situação. Considere o exemplo a seguir para entender melhor a importância dessa distinção.

As tarefas podem ser implícitas, em vez de explícitas, que podem ser confusas quando ocorre o envio em lote de tarefas com tarefas implícitas. Quando um `PropertyGroup` `ItemGroup` elemento ou aparece em um `Target` , cada declaração de propriedade no grupo é implicitamente tratada como uma tarefa [CreateProperty](createproperty-task.md) ou [CreateItem](createitem-task.md) separada. Isso significa que o comportamento é diferente quando o destino é agrupado, em vez de quando o destino não é em lotes (ou seja, quando falta a `%(ItemMetadataName)` sintaxe no `Outputs` atributo). Quando o destino é agrupado, o `ItemGroup` é executado uma vez por destino, mas quando o destino não é executado em lote, os equivalentes implícitos das `CreateItem` `CreateProperty` tarefas ou são executados em lote usando o envio em lote de tarefas, de modo que o destino execute apenas uma vez, e cada item ou propriedade no grupo é agrupada separadamente usando o envio em lote de tarefas.

O exemplo a seguir ilustra o envio em lote de destino versus envio em lote de tarefas no caso em que os metadados são modificados. Considere uma situação em que você tem as pastas A e B com alguns arquivos:

```
A\1.stub
B\2.stub
B\3.stub
```

Agora, examine a saída desses dois projetos semelhantes.

```xml
    <ItemGroup>
      <StubFiles Include="$(MSBuildThisFileDirectory)**\*.stub"/>

      <StubDirs Include="@(StubFiles->'%(RecursiveDir)')"/>
    </ItemGroup>

    <Target Name="Test1" AfterTargets="Build" Outputs="%(StubDirs.Identity)">
      <PropertyGroup>
        <ComponentDir>%(StubDirs.Identity)</ComponentDir>
        <ComponentName>$(ComponentDir.TrimEnd('\'))</ComponentName>
      </PropertyGroup>

      <Message Text=">> %(StubDirs.Identity) '$(ComponentDir)' '$(ComponentName)'"/>
    </Target>
```

A saída é:

```output
Test1:
  >> A\ 'A\' 'A'
Test1:
  >> B\ 'B\' 'B'
```

Agora, remova o `Outputs` atributo que especificou o envio em lote de destino.

```xml
    <ItemGroup>
      <StubFiles Include="$(MSBuildThisFileDirectory)**\*.stub"/>

      <StubDirs Include="@(StubFiles->'%(RecursiveDir)')"/>
    </ItemGroup>

    <Target Name="Test1" AfterTargets="Build">
      <PropertyGroup>
        <ComponentDir>%(StubDirs.Identity)</ComponentDir>
        <ComponentName>$(ComponentDir.TrimEnd('\'))</ComponentName>
      </PropertyGroup>

      <Message Text=">> %(StubDirs.Identity) '$(ComponentDir)' '$(ComponentName)'"/>
    </Target>
```

A saída é:

```output
Test1:
  >> A\ 'B\' 'B'
  >> B\ 'B\' 'B'
```

Observe que o título `Test1` é impresso apenas uma vez, mas no exemplo anterior, ele foi impresso duas vezes. Isso significa que o destino não está em lote.  E, como resultado, a saída é confusamente diferente.

O motivo é que, ao usar o envio em lote de destino, cada lote de destino executa tudo no destino com sua própria cópia independente de todas as propriedades e itens, mas quando você omite o `Outputs` atributo, as linhas individuais no grupo de propriedades são tratadas como tarefas distintas e potencialmente em lote. Nesse caso, a `ComponentDir` tarefa é processada em lote (ela usa a `%(ItemMetadataName)` sintaxe), de modo que, no momento em `ComponentName` que a linha é executada, ambos os lotes da `ComponentDir` linha foram concluídos e o segundo que executou determinado o valor, como visto na segunda linha.

## <a name="property-functions-using-metadata"></a>Funções de propriedade usando metadados

O envio em lote pode ser controlado por funções de propriedade que incluem metadados. Por exemplo,

`$([System.IO.Path]::Combine($(RootPath),%(Compile.Identity)))`

usa <xref:System.IO.Path.Combine%2A> para combinar um caminho de pasta raiz com um caminho do item de compilação.

Funções de propriedade podem não aparecer em valores de metadados. Por exemplo,

`%(Compile.FullPath.Substring(0,3))`

não é permitido.

Para obter mais informações sobre funções de propriedade, confira [Funções de propriedade](../msbuild/property-functions.md).

## <a name="see-also"></a>Veja também

- [Elemento ItemMetadata (MSBuild)](../msbuild/itemmetadata-element-msbuild.md)
- [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)
- [Referência do MSBuild](../msbuild/msbuild-reference.md)
- [Conceitos avançados](../msbuild/msbuild-advanced-concepts.md)
