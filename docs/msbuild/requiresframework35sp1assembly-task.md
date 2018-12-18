---
title: Tarefa RequiresFramework35SP1Assembly | Microsoft Docs
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
- RequiresFramework35SP1Assembly task [MSBuild]
- MSBuild, RequiresFramework35SP1Assembly task
ms.assetid: 755c018a-8a8b-4c94-8aee-3f171fc419e5
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5297d1a573542fecc55fa90983befa43df8f3f3d
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39155354"
---
# <a name="requiresframework35sp1assembly-task"></a>Tarefa RequiresFramework35SP1Assembly
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
 Além de ter os parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)