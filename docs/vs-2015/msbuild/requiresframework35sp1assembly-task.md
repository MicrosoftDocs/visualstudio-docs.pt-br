---
title: Tarefa RequiresFramework35SP1Assembly | Microsoft Docs
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
- RequiresFramework35SP1Assembly task [MSBuild]
- MSBuild, RequiresFramework35SP1Assembly task
ms.assetid: 755c018a-8a8b-4c94-8aee-3f171fc419e5
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ba85c6a1502aa8ebb7a09c6212233feadde1d471
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49256913"
---
# <a name="requiresframework35sp1assembly-task"></a>Tarefa RequiresFramework35SP1Assembly
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Determina se o aplicativo requer o .NET Framework 3.5 SP1.  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `RequiresFramework35SP1Assembly`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`Assemblies`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Define os assemblies referenciados no aplicativo.|  
|`CreateDesktopShortcut`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, cria um ícone de atalho na área de trabalho durante a instalação.|  
|`DeploymentManifestEntryPoint`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> opcional.<br /><br /> Especifica o nome do arquivo de manifesto para o aplicativo.|  
|`EntryPoint`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> opcional.<br /><br /> Especifica o assembly que deve ser executado quando o aplicativo for executado.|  
|`ErrorReportUrl`|Parâmetro `String` opcional.<br /><br /> Especifica o site que é exibido nas caixas de diálogo que são encontradas durante as instalações do ClickOnce.|  
|`Files`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica a lista de arquivos que serão implantados quando o aplicativo for publicado.|  
|`ReferencedAssemblies`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Define os assemblies referenciados no projeto.|  
|`RequiresMinimumFramework35SP1`|Parâmetro de saída `Boolean` opcional.<br /><br /> Se `true`, o aplicativo requer o .NET Framework 3.5 SP1.|  
|`SigningManifests`|Parâmetro de saída `Boolean` opcional.<br /><br /> Se `true`, os manifestos do ClickOnce são assinados.|  
|`SuiteName`|Parâmetro `String` opcional.<br /><br /> Especifica o nome da pasta no menu **Iniciar** no qual o aplicativo será instalado.|  
|`TargetFrameworkVersion`|Parâmetro `String` opcional.<br /><br /> Especifica a versão do .NET Framework que o aplicativo direciona.|  
  
## <a name="remarks"></a>Comentários  
 Além de ter os parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



