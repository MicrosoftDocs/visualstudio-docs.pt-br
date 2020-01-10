---
title: Como usar caracteres XML reservados em arquivos de projeto | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, using reserved XML characters
- MSBuild, reserved XML characters
ms.assetid: 1ae37275-96bf-4e6e-897b-6b048e5bbe93
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2f60b7d2c0de74743c021feee56a3d9f3c8f3eb5
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2020
ms.locfileid: "75574321"
---
# <a name="how-to-use-reserved-xml-characters-in-project-files"></a>Como usar caracteres XML reservados em arquivos de projeto
Quando você cria arquivos de projeto, talvez seja necessário usar caracteres XML reservados, por exemplo, nos valores de propriedade ou em valores de parâmetro de tarefa. No entanto, alguns caracteres reservados devem ser substituídos por uma entidade nomeada para que o arquivo de projeto possa ser analisado.

## <a name="use-reserved-characters"></a>Usar caracteres reservados
 A tabela a seguir descreve os caracteres XML reservados que devem ser substituídos pela entidade nomeada correspondente para que o arquivo de projeto possa ser analisado.

|Caractere reservado|Entidade nomeada|
|------------------------|------------------|
|\<|&amp;lt;|
|>|&amp;gt;|
|&|&amp;amp;|
|"|&amp;quot;|
|'|&amp;apos;|

#### <a name="to-use-double-quotes-in-a-project-file"></a>Para usar aspas duplas em um arquivo de projeto

- Substitua as aspas duplas pela entidade nomeada correspondente, &amp;quot;. Por exemplo, para colocar aspas duplas em torno da lista de itens `EXEFile`, digite:

    ```xml
    <Message Text="The output file is &quot;@(EXEFile)&quot;."/>
    ```

## <a name="example"></a>Exemplo
 No exemplo de código a seguir, as aspas duplas são usadas para realçar o nome de arquivo na mensagem gerada pelo arquivo de projeto.

```xml
<Project DefaultTargets="Compile"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >
    <!-- Set the application name as a property -->
    <PropertyGroup>
        <appname>"HelloWorldCS"</appname>
    </PropertyGroup>
    <!-- Specify the inputs -->
    <ItemGroup>
        <CSFile Include = "consolehwcs1.cs" />
    </ItemGroup>
    <Target Name = "Compile">
        <!-- Run the Visual C# compilation using input
        files of type CSFile -->
        <Csc Sources = "@(CSFile)">
            <!-- Set the OutputAssembly attribute of the CSC task
            to the name of the executable file that is created -->
            <Output
                TaskParameter = "OutputAssembly"
                ItemName = "EXEFile"/>
        </Csc>
        <!-- Log the file name of the output file -->
        <Message Text="The output file is &quot;@(EXEFile)&quot;."/>
    </Target>
</Project>
```

## <a name="see-also"></a>Veja também
- [Referência do MSBuild](../msbuild/msbuild-reference.md)
- [MSBuild](../msbuild/msbuild.md)
