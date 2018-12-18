---
title: Tarefa CreateCSharpManifestResourceName | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, CreateCSharpManifestResourceName task
- CreateCSharpManifestResourceName task [MSBuild]
ms.assetid: 2ace88c1-d757-40a7-8158-c1d3f5ff0511
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 32aa7fdb5779d7ae042e8efa9652f25df70a2754
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49247839"
---
# <a name="createcsharpmanifestresourcename-task"></a>Tarefa CreateCSharpManifestResourceName
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Cria um nome de manifesto de estilo [!INCLUDE[csprcs](../includes/csprcs-md.md)] de um nome de arquivo .resx fornecido ou de outro recurso.  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da [tarefa CreateCSharpManifestResourceName](../msbuild/createcsharpmanifestresourcename-task.md).  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`ManifestResourceNames`|Parâmetro de saída somente leitura <xref:Microsoft.Build.Framework.ITaskItem> `[]`.<br /><br /> Os nomes de manifesto resultantes.|  
|`ResourceFiles`|Parâmetro `String` obrigatório.<br /><br /> O nome do arquivo de recurso do qual criar o nome do manifesto [!INCLUDE[csprcs](../includes/csprcs-md.md)].|  
|`RootNamespace`|Parâmetro `String` opcional.<br /><br /> O namespace raiz do arquivo de recurso, geralmente obtido do arquivo de projeto. Pode ser `null`.|  
|`PrependCultureAsDirectory`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, o nome da cultura é adicionado como um nome de diretório antes do nome do recurso de manifesto. O valor padrão é `true`.|  
|`ResourceFilesWithManifestResourceNames`|Parâmetro de saída opcional somente leitura `String`.<br /><br /> Retorna o nome do arquivo de recurso que agora inclui o nome do recurso de manifesto.|  
  
## <a name="remarks"></a>Comentários  
 A [tarefa CreateVisualBasicManifestResourceName](../msbuild/createvisualbasicmanifestresourcename-task.md) determina o nome do recurso de manifesto apropriado para atribuir a um determinado arquivo .resx ou outro arquivo de recurso. A tarefa fornece um nome lógico para um arquivo de recurso e, em seguida, anexa-o a um parâmetro de saída como metadados.  
  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



