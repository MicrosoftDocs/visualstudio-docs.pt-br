---
title: Tarefa UidManager | Microsoft Docs
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
- UidManager task [WPF MSBuild]
- UidManager task [WPF MSBuild], parameters
- managing UIDs when localizing XAML elements [WPF MSBuild]
- localizing XAML elements [WPF MSBuild], managing UIDs
- checking UIDs when localizing XAML elements [WPF MSBuild]
ms.assetid: 4fc7b5a5-11b0-46ca-9656-8c2a0b08d1fe
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fa51ddb8f2cf6e200b7313069fca3ee6db3ebcf3
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49208059"
---
# <a name="uidmanager-task"></a>Tarefa UidManager
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
A tarefa <xref:Microsoft.Build.Tasks.Windows.UidManager> verifica, atualiza ou remove UIDs (identificadores exclusivos), para localizar todos os elementos [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] que são incluídos nos arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] de origem.  
  
## <a name="task-parameters"></a>Parâmetros da tarefa  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`IntermediateDirectory`|Parâmetro **String** opcional.<br /><br /> Especifica o diretório usado para fazer backup dos arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] de origem especificados pelo parâmetro **MarkupFiles**.|  
|`MarkupFiles`|Parâmetro obrigatório **ITaskItem[]**.<br /><br /> Especifica os arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] de origem que serão incluídos na verificação, atualização ou remoção de UID.|  
|`Task`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica a tarefa de gerenciamento de UID que você deseja executar. As opções válidas são **Verificar**, **Atualizar** ou **Remover**.|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tarefa <xref:Microsoft.Build.Tasks.Windows.UidManager> para verificar se os arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] de origem contêm elementos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] que têm UIDs apropriados.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <UsingTask   
    TaskName="Microsoft.Build.Tasks.Windows.UidManager"   
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />  
  <Target Name="UidManagerTask">  
    <UidManager  
      Task="Check"  
      MarkupFiles="Page1.xaml;Page2.xaml"  
      IntermediateDirectory="c:\UidManagerIntermediateDirectory" />  
  </Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência MSBuild do WPF](../msbuild/wpf-msbuild-reference.md)   
 [Referência de tarefas](../msbuild/wpf-msbuild-task-reference.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Como compilar um aplicativo WPF (WPF)](http://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)   
 [Como: localizar um aplicativo](http://msdn.microsoft.com/library/5001227e-9326-48a4-9dcd-ba1b89ee6653)



