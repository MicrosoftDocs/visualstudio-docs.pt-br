---
title: Tarefa CreateCSharpManifestResourceName | Microsoft Docs
description: Use a tarefa MSBuild CreateCSharpManifestResourceName para criar um nome de manifesto em estilo C# de um determinado nome de arquivo. resx ou outro recurso.
ms.custom: SEO-VS-2020
ms.date: 11/15/2020
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, CreateCSharpManifestResourceName task
- CreateCSharpManifestResourceName task [MSBuild]
ms.assetid: 2ace88c1-d757-40a7-8158-c1d3f5ff0511
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3e1bd096c2a9c7763a3be0611f3716f61df22856
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055863"
---
# <a name="createcsharpmanifestresourcename-task"></a>Tarefa CreateCSharpManifestResourceName

Cria um nome de manifesto em estilo C# a partir de um determinado nome de arquivo *. resx* ou outro recurso.

## <a name="parameters"></a>Parâmetros

 A tabela a seguir descreve os parâmetros da [tarefa CreateCSharpManifestResourceName](../msbuild/createcsharpmanifestresourcename-task.md).

| Parâmetro | Descrição |
| - | - |
| `ManifestResourceNames` | <xref:Microsoft.Build.Framework.ITaskItem>`[]`parâmetro somente leitura de saída.<br /><br /> Os nomes de manifesto resultantes. |
| `ResourceFiles` | Parâmetro `String` obrigatório.<br /><br /> O nome do arquivo de recurso do qual criar o nome do manifesto C#. |
| `RootNamespace` | Parâmetro `String` opcional.<br /><br /> O namespace raiz do arquivo de recurso, geralmente obtido do arquivo de projeto. Pode ser `null`. |
| `PrependCultureAsDirectory` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, o nome da cultura é adicionado como um nome de diretório antes do nome do recurso de manifesto. O valor padrão é `true`. |
| `ResourceFilesWithManifestResourceNames` | Parâmetro de saída opcional somente leitura `String`.<br /><br /> Retorna o nome do arquivo de recurso que agora inclui o nome do recurso de manifesto. |

## <a name="remarks"></a>Comentários

 A [tarefa CreateCSharpManifestResourceName](../msbuild/createcsharpmanifestresourcename-task.md) determina o nome do recurso de manifesto apropriado a ser atribuído a um determinado arquivo *. resx* ou outro recurso. A tarefa fornece um nome lógico para um arquivo de recurso e, em seguida, anexa-o a um parâmetro de saída como metadados.

 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base TaskExtension](../msbuild/taskextension-base-class.md).

## <a name="see-also"></a>Confira também

- [Tarefas](../msbuild/msbuild-tasks.md)
- [Referência de tarefas](../msbuild/msbuild-task-reference.md)
