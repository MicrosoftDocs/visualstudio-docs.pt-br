---
title: Tarefa ZipDirectory | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.reviewer: ''
ms.suite: ''
ms.technology: msbuild
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ZipDirectory
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ZipDirectory task [MSBuild]
- MSBuild, ZipDirectory task
ms.assetid: 916bb2e3-3017-4828-ae27-c0b5c99bbb48
caps.latest.revision: 16
author: Mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3fffaa61a494c507aedf22238d22c861ba9f11bc
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671034"
---
# <a name="zipdirectory-task"></a>Tarefa ZipDirectory
Cria um arquivo *.zip* do conteúdo de um diretório.

>[!NOTE]
>A tarefa `ZipDirectory` está disponível apenas no MSBuild 15.8 e superiores.
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `ZipDirectory`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`DestinationFile`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> necessário<br /><br /> O caminho completo para o arquivo *.zip* a ser criado.|
|`Overwrite`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, o arquivo de destino será substituído, quando existir. Assume o padrão de `false`.|
|`SourceDirectory`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> obrigatório.<br /><br /> Especifica o diretório no qual será criado um arquivo morto *.zip*.|
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir cria um arquivo *.zip* do diretório de saída após a criação de um projeto.
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <Target Name="ZipOutputPath" AfterTargets="Build">
        <ZipDirectory
            SourceDirectory="$(OutputPath)"
            DestinationFile="$(MSBuildProjectDirectory)\output.zip" />
    </Target>

</Project>
```
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)
