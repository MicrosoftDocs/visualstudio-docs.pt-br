---
title: Tarefa GenerateTrustInfo | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GenerateTrustInfo task
- GenerateTrustInfo task [MSBuild]
ms.assetid: 3ca60816-4bb0-4fef-ae43-ca0bfb63def3
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1f5e5e73f7e4e9f32c4fc929b86da3e629a1eb62
ms.sourcegitcommit: c57ae28181ffe14a30731736661bf59c3eff1211
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37946674"
---
# <a name="generatetrustinfo-task"></a>Tarefa GenerateTrustInfo
Gera a confiança do aplicativo do manifesto base e dos parâmetros `TargetZone` e `ExcludedPermissions`.  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `GenerateTrustInfo`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`ApplicationDependencies`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica os assemblies dependentes.|  
|`BaseManifest`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> opcional.<br /><br /> Especifica o manifesto base do qual gerar a confiança do aplicativo.|  
|`ExcludedPermissions`|Parâmetro `String` opcional.<br /><br /> Especifica um ou mais valores de identidade de permissão separados por ponto e vírgula a serem excluídos do conjunto de permissões da zona padrão.|  
|`TargetZone`|Parâmetro `String` opcional.<br /><br /> Especifica um conjunto de permissões padrão de zona, que é obtido da política do computador.|  
|`TrustInfoFile`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem> necessário.<br /><br /> Especifica o arquivo que contém as informações de confiança de segurança do aplicativo.|  
  
## <a name="remarks"></a>Comentários  
 Além de ter os parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)