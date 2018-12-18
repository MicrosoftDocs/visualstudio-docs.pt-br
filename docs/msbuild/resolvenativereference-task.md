---
title: Tarefa ResolveNativeReference| Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ResolveNativeReference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, ResolveNativeReference task
- ResolveNativeReference task [MSBuild]
ms.assetid: 56acd101-de77-4eec-92c6-f5c6d2187579
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c6770452e26eae111624909078da3a880503a184
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39151288"
---
# <a name="resolvenativereference-task"></a>Tarefa ResolveNativeReference
Resolve referências nativas. Implementa a classe <xref:Microsoft.Build.Tasks.ResolveNativeReference>. Essa classe dá suporte à infraestrutura do .NET Framework, que não se destina a ser usada diretamente do seu código.  
  
## <a name="task-parameters"></a>Parâmetros de tarefa  
 A tabela a seguir descreve os parâmetros da tarefa `ResolveNativeReference`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`AdditionalSearchPaths`|Parâmetro <xref:System.String?displayProperty=fullName>`[]` obrigatório.<br /><br /> Obtém ou define os caminhos de pesquisa para resolver as identidades de assembly de referências nativas.|  
|`ContainedComComponents`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Obtém ou define os componentes COM do assembly nativo.|  
|`ContainedLooseEtcFiles`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Obtém ou define os arquivos *Etc* flexíveis listados no manifesto nativo.|  
|`ContainedLooseTlbFiles`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Obtém ou define os arquivos *.tlb* do assembly nativo.|  
|`ContainedPrerequisiteAssemblies`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Obtém ou define os assemblies que devem estar presentes antes que o manifesto possa ser usado.|  
|`ContainedTypeLibraries`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Obtém ou define as bibliotecas de tipo do assembly nativo.|  
|`ContainingReferenceFiles`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Obtém ou define os arquivos de referência.|  
|`NativeReferences`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem>`[]` obrigatório.<br /><br /> Obtém ou define as referências de assembly nativo do Win32.|  
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)