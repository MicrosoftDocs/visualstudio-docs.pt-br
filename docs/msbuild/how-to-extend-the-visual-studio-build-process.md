---
title: Estender o processo de build
description: Conheça várias maneiras de modificar o processo de compilação para que você possa controlar e personalizar como seus projetos são criados.
ms.custom: seodec18, SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, overriding predefined targets
- MSBuild, overriding DependsOn properties
- MSBuild, extending Visual Studio builds
- MSBuild, DependsOn properties
ms.assetid: cb077613-4a59-41b7-96ec-d8516689163c
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 94e5680f8e8635c969e25555463a21bba069284a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055811"
---
# <a name="how-to-extend-the-visual-studio-build-process"></a>Como estender o processo de build do Visual Studio

O processo de compilação do Visual Studio é definido por uma série de arquivos MSBuild *. targets* que são importados para o arquivo de projeto. Um desses arquivos importados, *Microsoft. Common. targets*, pode ser estendido para permitir que você execute tarefas personalizadas em vários pontos no processo de compilação. Este artigo explica dois métodos que você pode usar para estender o processo de compilação do Visual Studio:

- Substituir destinos predefinidos específicos definidos nos destinos comuns (*Microsoft. Common. targets* ou os arquivos que ele importa).

- Substituindo as propriedades "depends" definidas nos destinos comuns.

## <a name="override-predefined-targets"></a>Substituir destinos predefinidos

Os destinos comuns contêm um conjunto de destinos vazios predefinidos que é chamado antes e depois de alguns dos principais destinos no processo de compilação. Por exemplo, o MSBuild chama o `BeforeBuild` destino antes do `CoreBuild` destino principal e o `AfterBuild` destino após o `CoreBuild` destino. Por padrão, os destinos vazios nos destinos comuns não fazem nada, mas você pode substituir seu comportamento padrão definindo os destinos desejados em um arquivo de projeto que importe os destinos comuns. Ao substituir os destinos predefinidos, você pode usar tarefas do MSBuild para fornecer mais controle sobre o processo de compilação.

> [!NOTE]
> Projetos no estilo SDK têm uma importação implícita de destinos *após a última linha do arquivo de projeto*. Isso significa que não é possível substituir destinos padrão, a menos que você especifique suas importações manualmente, conforme descrito em [como: usar SDKs de projeto do MSBuild](how-to-use-project-sdk.md).

#### <a name="to-override-a-predefined-target"></a>Para substituir um destino predefinido

1. Identifique um destino predefinido nos destinos comuns que você deseja substituir. Consulte a tabela abaixo para obter uma lista completa de destinos que você pode substituir com segurança.

2. Defina o destino ou destinos no final do arquivo de projeto, imediatamente antes da marca `</Project>`. Por exemplo:

    ```xml
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

A tabela a seguir mostra todos os destinos nos destinos comuns que você pode substituir com segurança.

|Nome de destino|Descrição|
|-----------------|-----------------|
|`BeforeCompile`, `AfterCompile`|As tarefas inseridas em um desses destinos são executadas antes ou após a conclusão da compilação principal. A maioria das personalizações é realizada em um desses dois destinos.|
|`BeforeBuild`, `AfterBuild`|As tarefas inseridas em um desses destinos serão executadas antes ou depois de todo o resto no build. **Observação:** os destinos `BeforeBuild` e `AfterBuild` já estão definidos nos comentários ao final da maioria dos arquivos de projeto, permitindo que você adicione com facilidade eventos de pré e pós-build ao arquivo de projeto.|
|`BeforeRebuild`, `AfterRebuild`|As tarefas inseridas em um desses destinos são executadas antes ou após a invocação da funcionalidade de recompilação principal. A ordem de execução de destino em *Microsoft. Common. targets* é: `BeforeRebuild` , `Clean` , `Build` e, em seguida, `AfterRebuild` .|
|`BeforeClean`, `AfterClean`|As tarefas inseridas em um desses destinos são executadas antes ou após a invocação da funcionalidade de limpeza principal.|
|`BeforePublish`, `AfterPublish`|As tarefas inseridas em um desses destinos são executadas antes ou após a invocação da funcionalidade de publicação principal.|
|`BeforeResolveReferences`, `AfterResolveReferences`|As tarefas inseridas em um desses destinos são executadas antes ou após a resolução das referências de assembly.|
|`BeforeResGen`, `AfterResGen`|As tarefas inseridas em um desses destinos são executadas antes ou após a geração de recursos.|

## <a name="example-aftertargets-and-beforetargets"></a>Exemplo: AfterTargets e BeforeTargets

O exemplo a seguir mostra como usar o `AfterTargets` atributo para adicionar um destino personalizado que faz algo com os arquivos de saída. Nesse caso, ele copia os arquivos de saída para uma nova pasta *CustomOutput*.  O exemplo também mostra como limpar os arquivos criados pela operação de compilação personalizada com um `CustomClean` destino usando um `BeforeTargets` atributo e especificando que a operação de limpeza personalizada é executada antes do `CoreClean` destino.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
     <TargetFramework>netcoreapp3.1</TargetFramework>
     <_OutputCopyLocation>$(OutputPath)..\..\CustomOutput\</_OutputCopyLocation>
  </PropertyGroup>

  <Target Name="CustomAfterBuild" AfterTargets="Build">
    <ItemGroup>
      <_FilesToCopy Include="$(OutputPath)**\*"/>
    </ItemGroup>
    <Message Text="_FilesToCopy: @(_FilesToCopy)" Importance="high"/>

    <Message Text="DestFiles:
        @(_FilesToCopy->'$(_OutputCopyLocation)%(RecursiveDir)%(Filename)%(Extension)')"/>

    <Copy SourceFiles="@(_FilesToCopy)"
          DestinationFiles=
          "@(_FilesToCopy->'$(_OutputCopyLocation)%(RecursiveDir)%(Filename)%(Extension)')"/>
  </Target>

  <Target Name="CustomClean" BeforeTargets="CoreClean">
    <Message Text="Inside Custom Clean" Importance="high"/>
    <ItemGroup>
      <_CustomFilesToDelete Include="$(_OutputCopyLocation)**\*"/>
    </ItemGroup>
    <Delete Files='@(_CustomFilesToDelete)'/>
  </Target>
</Project>
```

> [!WARNING]
> Certifique-se de usar nomes diferentes dos destinos predefinidos listados na tabela na seção anterior (por exemplo, nomeamos o destino da compilação personalizada aqui `CustomAfterBuild` , não `AfterBuild` ), já que esses destinos predefinidos são substituídos pela importação do SDK que também os define. Você não vê a importação do arquivo de destino que substitui esses destinos, mas ele é adicionado implicitamente ao final do arquivo de projeto quando você usa o `Sdk` método de atributo de referência a um SDK.

## <a name="override-dependson-properties"></a>Substituir propriedades DependsOn

A substituição de destinos predefinidos é uma maneira fácil de estender o processo de compilação, mas, como o MSBuild avalia a definição de destinos sequencialmente, não há como impedir que outro projeto importe que o projeto substitua os destinos que você já tenha substituído. Dessa forma, por exemplo, o último destino `AfterBuild` no arquivo de projeto, depois que todos os outros projetos foram importados, será aquele usado durante o build.

Você pode se proteger contra substituições indesejadas de destinos substituindo as propriedades dependentes que são usadas em `DependsOnTargets` atributos em todos os destinos comuns. Por exemplo, o destino `Build` contém um valor de atributo `DependsOnTargets` de `"$(BuildDependsOn)"`. Considere:

```xml
<Target Name="Build" DependsOnTargets="$(BuildDependsOn)"/>
```

Este trecho de XML indica que, antes de poder executar o destino `Build`, todos os destinos especificados na propriedade `BuildDependsOn` devem ser executados primeiro. A propriedade `BuildDependsOn` está definida como:

```xml
<PropertyGroup>
    <BuildDependsOn>
        BeforeBuild;
        CoreBuild;
        AfterBuild
    </BuildDependsOn>
</PropertyGroup>
```

Você pode substituir esse valor da propriedade declarando outra propriedade denominada `BuildDependsOn` no final do seu arquivo de projeto. Incluindo a propriedade `BuildDependsOn` anterior na nova propriedade, você pode adicionar novos destinos no início e fim da lista de destinos. Por exemplo:

```xml
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

#### <a name="to-override-a-dependson-property"></a>Para substituir uma propriedade DependsOn

1. Identifique uma propriedade dependente predefinida nos destinos comuns que você deseja substituir. Confira a tabela abaixo para obter uma lista das propriedades DependsOn geralmente substituídas.

2. Defina outra instância da propriedade ou propriedades no final do seu arquivo de projeto. Inclua a propriedade original, por exemplo `$(BuildDependsOn)`, na nova propriedade.

3. Defina seus destinos personalizados antes ou após a definição da propriedade.

4. Compile o arquivo de projeto.

### <a name="commonly-overridden-dependson-properties"></a>Propriedades DependsOn geralmente substituídas

|Nome da propriedade|Descrição|
|-------------------|-----------------|
|`BuildDependsOn`|A propriedade a ser substituída se você quiser inserir destinos personalizados antes ou após o processo inteiro de build.|
|`CleanDependsOn`|A propriedade a ser substituída você quiser limpar a saída do seu processo de build personalizado.|
|`CompileDependsOn`|A propriedade a ser substituída se você quiser inserir processos personalizados antes ou após a etapa de compilação.|

## <a name="example-builddependson-and-cleandependson"></a>Exemplo: BuildDependsOn e CleanDependsOn

O exemplo a seguir é semelhante ao `BeforeTargets` `AfterTargets` exemplo e, mas mostra como obter uma funcionalidade semelhante. Ele estende a compilação usando `BuildDependsOn` para adicionar sua própria tarefa `CustomAfterBuild` que copia os arquivos de saída após a compilação e também adiciona a tarefa correspondente `CustomClean` usando `CleanDependsOn` .  

Neste exemplo, este é um projeto no estilo SDK. Conforme mencionado na observação sobre os projetos no estilo do SDK anteriormente neste artigo, você deve usar o método de importação manual em vez do `Sdk` atributo que o Visual Studio usa quando gera arquivos de projeto.

```xml
<Project>
  <Import Project="Sdk.props" Sdk="Microsoft.NET.Sdk"/>

  <PropertyGroup>
    <TargetFramework>netcoreapp3.1</TargetFramework>
  </PropertyGroup>

  <Import Project="Sdk.targets" Sdk="Microsoft.NET.Sdk"/>

  <PropertyGroup>
    <BuildDependsOn>
      $(BuildDependsOn);CustomAfterBuild
    </BuildDependsOn>

    <CleanDependsOn>
      $(CleanDependsOn);CustomClean
    </CleanDependsOn>

    <_OutputCopyLocation>$(OutputPath)..\..\CustomOutput\</_OutputCopyLocation>
  </PropertyGroup>

  <Target Name="CustomAfterBuild">
    <ItemGroup>
      <_FilesToCopy Include="$(OutputPath)**\*"/>
    </ItemGroup>
    <Message Importance="high" Text="_FilesToCopy: @(_FilesToCopy)"/>

    <Message Text="DestFiles:
      @(_FilesToCopy-&gt;'$(_OutputCopyLocation)%(RecursiveDir)%(Filename)%(Extension)')"/>

    <Copy SourceFiles="@(_FilesToCopy)"
          DestinationFiles="@(_FilesToCopy-&gt;'$(_OutputCopyLocation)%(RecursiveDir)%(Filename)%(Extension)')"/>
  </Target>

  <Target Name="CustomClean">
    <Message Importance="high" Text="Inside Custom Clean"/>
    <ItemGroup>
      <_CustomFilesToDelete Include="$(_OutputCopyLocation)**\*"/>
    </ItemGroup>
    <Delete Files="@(_CustomFilesToDelete)"/>
  </Target>
</Project>
```

A ordem dos elementos é importante. Os `BuildDependsOn` `CleanDependsOn` elementos e devem aparecer depois de importar o arquivo de destino padrão do SDK.

## <a name="see-also"></a>Confira também

- [integração com o Visual Studio](../msbuild/visual-studio-integration-msbuild.md)
- [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)
- [arquivos. targets](../msbuild/msbuild-dot-targets-files.md)
