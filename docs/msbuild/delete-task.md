---
title: Tarefa Delete | Microsoft Docs
ms.date: 06/11/2020
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Delete
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Delete task [MSBuild]
- MSBuild, Delete task
ms.assetid: 916bb2e3-3017-4828-ae27-c0b5c99bbb48
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: eddb9804378a4c32de9d1b68f952bc715f32ffd6
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288904"
---
# <a name="delete-task"></a>tarefa Delete

Exclui os arquivos especificados.

## <a name="parameters"></a>Parâmetros

A tabela a seguir descreve os parâmetros da tarefa `Delete`.

|Parâmetro|Descrição|
|---------------|-----------------|
|`DeletedFiles`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Especifica os arquivos que foram excluídos com êxito.|
|`Files`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem>`[]` obrigatório.<br /><br /> Especifica os arquivos a serem excluídos.|
|`TreatErrorsAsWarnings`|Parâmetro opcional `Boolean`<br /><br /> Se `true`, os erros são registrados como avisos. O valor padrão é `false`.|

## <a name="remarks"></a>Comentários

Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base TaskExtension](../msbuild/taskextension-base-class.md).

> [!WARNING]
> Tenha cuidado ao usar curingas com a `Delete` tarefa. Você pode excluir facilmente os arquivos errados com expressões como `$(SomeProperty)\**\*.*` ou `$(SomeProperty)/**/*.*` , especialmente se a propriedade for avaliada como uma cadeia de caracteres vazia; nesse caso, o `Files` parâmetro pode ser avaliado como a raiz da unidade e excluído muito mais do que você queria excluir.

## <a name="example"></a>Exemplo

O exemplo a seguir exclui o arquivo *MyApp. pdb* quando você cria o `DeleteDebugSymbolFile` destino.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
  </PropertyGroup>

    <PropertyGroup>
        <AppName>ConsoleApp1</AppName>
    </PropertyGroup>

    <Target Name="DeleteDebugSymbolFile">
        <Message Text="Deleting $(OutDir)$(AppName).pdb"/>
        <Delete Files="$(OutDir)$(AppName).pdb" />
    </Target>
  
</Project>

```

Se você precisar acompanhar os arquivos excluídos, defina `TaskParameter` como `DeletedFiles` com o nome do item, da seguinte maneira:

```xml
      <Target Name="DeleteDebugSymbolFile">
        <Delete Files="$(OutDir)$(AppName).pdb" >
              <Output TaskParameter="DeletedFiles" ItemName="DeletedList"/>
        </Delete>
        <Message Text="Deleted files: '@(DeletedList)'"/>
    </Target>
```

Em vez de usar curingas diretamente na `Delete` tarefa, crie um `ItemGroup` dos arquivos para excluir e executar a `Delete` tarefa nele. Mas não deixe de fazer isso com `ItemGroup` cuidado. Se você colocar um `ItemGroup` no nível superior em um arquivo de projeto, ele será avaliado no início, antes do início da compilação, de modo que não incluirá nenhum arquivo criado como parte do processo de compilação. Portanto, coloque o `ItemGroup` que cria a lista de itens a serem excluídos em um destino próximo à `Delete` tarefa. Você também pode especificar uma condição para verificar se a propriedade não está vazia, para que você não crie uma lista de itens com um caminho que comece na raiz da unidade.

A `Delete` tarefa destina-se à exclusão de arquivos. Se você quiser excluir um diretório, use [RemoveDir](removedir-task.md).

A `Delete` tarefa não fornece uma opção para excluir arquivos somente leitura. Para excluir arquivos somente leitura, você pode usar a `Exec` tarefa para executar o `del` comando ou equivalente, com a opção apropriada para habilitar a exclusão de arquivos somente leitura. Você precisa prestar atenção no comprimento da lista de itens de entrada, já que há uma limitação de comprimento na linha de comando, bem como certificar-se de tratar nomes de filespaces com espaços, como neste exemplo:

```xml
<Target Name="DeleteReadOnly">
  <ItemGroup>
    <FileToDelete Include="read only file.txt"/>
  </ItemGroup>
  <Exec Command="del /F /Q &quot;@(FileToDelete)&quot;"/>
</Target>
```

Em geral, ao escrever scripts de Build, considere se a sua exclusão é logicamente parte de uma `Clean` operação. Se você precisar definir alguns arquivos a serem limpos como parte de uma operação normal `Clean` , poderá adicioná-los à `@(FileWrites)` lista e eles serão excluídos no próximo `Clean` . Se for necessário mais processamento personalizado, defina um destino e especifique para que ele seja executado definindo o atributo `BeforeTargets="Clean"` ou `AfterTargets="Clean"` , ou defina a versão personalizada dos `BeforeClean` destinos ou `AfterClean` . Consulte [personalizar sua compilação](customize-your-build.md).

## <a name="see-also"></a>Veja também

- [Tarefa RemoveDir](removedir-task.md)
- [Tarefas](../msbuild/msbuild-tasks.md)
- [Referência de tarefa](../msbuild/msbuild-task-reference.md)
