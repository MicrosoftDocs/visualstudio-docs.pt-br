---
title: Tarefa WriteLinesToFile | Microsoft Docs
ms.date: 09/20/2018
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#WriteLinesToFile
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- WriteLinesToFile task [MSBuild]
- MSBuild, WriteLinesToFile task
ms.assetid: 9c8862ac-8da5-4437-9430-ecc30421f1c9
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 27673ba3691e53540bce2249700c4453cb56c166
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85286096"
---
# <a name="writelinestofile-task"></a>Tarefa WriteLinesToFile

Grava os caminhos dos itens especificados no arquivo de texto especificado.

## <a name="task-parameters"></a>Parâmetros de tarefa

 A tabela a seguir descreve os parâmetros da tarefa `WriteLinestoFile`.

|Parâmetro|Descrição|
|---------------|-----------------|
|`File`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> obrigatório.<br /><br /> Especifica o arquivo no qual os itens serão gravados.|
|`Lines`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica os itens a serem gravados no arquivo. O padrão é a lista vazia.|
|`Overwrite`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa substituirá todo o conteúdo existente no arquivo. O padrão é `false`.|
|`Encoding`|Parâmetro `String` opcional.<br /><br /> Seleciona a codificação de caracteres, por exemplo, "Unicode". Padrão é UTF-8.  Consulte também <xref:System.Text.Encoding>.|
|`WriteOnlyWhenDifferent`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, o arquivo de destino especificado, se ele existir, será lido primeiro para comparar o que a tarefa teria gravado. Se idêntico, o arquivo não será gravado no disco, e o carimbo de data e hora será preservado. O padrão é `false`.|

## <a name="remarks"></a>Comentários

 Se `Overwrite` for `true`, criará um novo arquivo, gravará os conteúdos nele e o fechará. Se o arquivo de destino já existir, ele será substituído. Se `Overwrite` for `false`, acrescentará os conteúdos ao arquivo, criando um arquivo de destino, caso ele ainda não exista.

 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base TaskExtension](../msbuild/taskextension-base-class.md).

## <a name="example"></a>Exemplo

 O exemplo a seguir usa a tarefa `WriteLinesToFile` para gravar os caminhos dos itens na coleção de itens `MyItems` no arquivo especificado pela coleção de itens `MyTextFile`.

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <MyTextFile Include="Items.txt"/>
        <MyItems Include="*.cs"/>
    </ItemGroup>

    <Target Name="WriteToFile">
        <WriteLinesToFile
            File="@(MyTextFile)"
            Lines="@(MyItems)"
            Overwrite="true"
            Encoding="Unicode"/>
    </Target>

</Project>
```

Neste exemplo, usamos uma propriedade com novas linhas inseridas para gravar um arquivo de texto com várias linhas. Se uma entrada em `Lines` tiver caracteres de nova linha inseridos, as novas linhas serão incluídas no arquivo de saída. Dessa forma, você pode fazer referência a propriedades multilinha.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.1</TargetFramework>
  </PropertyGroup>

  <Target Name="WriteLaunchers" AfterTargets="CopyFilesToOutputDirectory">
      <PropertyGroup>
        <LauncherCmd>
@ECHO OFF
dotnet %~dp0$(AssemblyName).dll %*
        </LauncherCmd>
      </PropertyGroup>

      <WriteLinesToFile
        File="$(OutputPath)$(AssemblyName).cmd"
        Overwrite="true"
        Lines="$(LauncherCmd)" />
  </Target>
</Project>
```

## <a name="see-also"></a>Veja também

- [Tarefas](../msbuild/msbuild-tasks.md)
- [Referência de tarefa](../msbuild/msbuild-task-reference.md)
