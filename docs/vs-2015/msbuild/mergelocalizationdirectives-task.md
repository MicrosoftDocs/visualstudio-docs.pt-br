---
title: Tarefa MergeLocalizationDirectives | Microsoft Docs
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
- localizing XAML [WPF MSBuild], moving comments and attributes to a separate file
- MergeLocalizationDirectives task [WPF MSBuild], parameters
- MergeLocalizationDirectives task [WPF MSBuild]
- moving localization comments and attributes to a separate file [WPF MSBuild]
ms.assetid: 9095b4f1-88da-4194-914b-ee1456826830
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 842e36d549dab7d6e7c2f7d1da2f3e9b4db4e9d3
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49268197"
---
# <a name="mergelocalizationdirectives-task"></a>Tarefa MergeLocalizationDirectives
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
A tarefa <xref:Microsoft.Build.Tasks.Windows.MergeLocalizationDirectives> mescla os atributos de localização e comentários de um ou mais [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] arquivos de formato binário em um único arquivo para todo o assembly.  
  
## <a name="task-parameters"></a>Parâmetros da tarefa  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`GeneratedLocalizationFiles`|Parâmetro obrigatório **ITaskItem[]**.<br /><br /> Especifica a lista de arquivos de diretivas de localização de arquivos individuais no formato binário [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)].|  
|`OutputFile`|Parâmetro de saída da **cadeia de caracteres** necessário.<br /><br /> Especifica o caminho de saída do assembly de diretivas de localização compilado.|  
  
## <a name="remarks"></a>Comentários  
 Você pode adicionar atributos de localização e comentários no conteúdo [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)]. Com suporte à localização da [!INCLUDE[TLA#tla_wpf](../includes/tlasharptla-wpf-md.md)], você pode retirar os comentários e atributos de localização e colocá-los em um arquivo .loc separado do assembly gerado. Você pode fazer isso usando o atributo **LocalizationPropertyStorage**. Para obter mais informações sobre os atributos de localização e comentários e **LocalizationPropertyStorage**, confira [Atributos de localização e comentários](http://msdn.microsoft.com/library/ead2d9ac-b709-4ec1-a924-39927a29d02f).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mescla os comentários de localização de vários arquivos de formato binário [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] em um único arquivo .loc.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <UsingTask   
    TaskName="Microsoft.Build.Tasks.Windows.MergeLocalizationDirectives"   
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />  
  <Target Name="MergeLocalizationDirectivesTask">  
    <MergeLocalizationDirectives   
      GeneratedLocalizationFiles="obj\debug\page1.loc;obj\debug\page2.loc;obj\debug\page3.loc"  
      OutputFile="obj\debug\WPFMSBuildSample.loc" />  
  </Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência MSBuild do WPF](../msbuild/wpf-msbuild-reference.md)   
 [Referência de tarefas](../msbuild/wpf-msbuild-task-reference.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Como compilar um aplicativo WPF (WPF)](http://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)



