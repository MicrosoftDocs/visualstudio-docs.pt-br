---
title: Tarefa MergeLocalizationDirectives | Microsoft Docs
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
- localizing XAML [WPF MSBuild], moving comments and attributes to a separate file
- MergeLocalizationDirectives task [WPF MSBuild], parameters
- MergeLocalizationDirectives task [WPF MSBuild]
- moving localization comments and attributes to a separate file [WPF MSBuild]
ms.assetid: 9095b4f1-88da-4194-914b-ee1456826830
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2d0245765c1b6aa01d6762848463997ad2f13ba3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49936661"
---
# <a name="mergelocalizationdirectives-task"></a>Tarefa MergeLocalizationDirectives
A tarefa <xref:Microsoft.Build.Tasks.Windows.MergeLocalizationDirectives> mescla os atributos de localização e comentários de um ou mais [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] arquivos de formato binário em um único arquivo para todo o assembly.  
  
## <a name="task-parameters"></a>Parâmetros de tarefa  
  
| Parâmetro | Descrição |
|------------------------------| - |
| `GeneratedLocalizationFiles` | Parâmetro obrigatório **ITaskItem[]**.<br /><br /> Especifica a lista de arquivos de diretivas de localização de arquivos individuais no formato binário [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)]. |
| `OutputFile` | Parâmetro de saída da **cadeia de caracteres** necessário.<br /><br /> Especifica o caminho de saída do assembly de diretivas de localização compilado. |
  
## <a name="remarks"></a>Comentários  
 Você pode adicionar atributos de localização e comentários no conteúdo [!INCLUDE[TLA#tla_xaml](../msbuild/includes/tlasharptla_xaml_md.md)]. Com o suporte à localização do [!INCLUDE[TLA#tla_wpf](../msbuild/includes/tlasharptla_wpf_md.md)], você pode retirar os atributos de localização e os comentários colocá-los em um arquivo *.loc* separado do assembly gerado. Você pode fazer isso usando o atributo **LocalizationPropertyStorage**. Para obter mais informações sobre atributos de localização e comentários, bem como sobre **LocalizationPropertyStorage**, confira [Atributos de localização e comentários](/dotnet/framework/wpf/advanced/localization-attributes-and-comments).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mescla os comentários de localização de vários arquivos de formato binário [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] em um único arquivo *.loc*.  
  
```xml  
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
[Referência do WPF MSBuild](../msbuild/wpf-msbuild-reference.md)  
[Referência de tarefas do WPF MSBuild](../msbuild/wpf-msbuild-task-reference.md)  
[Referência do MSBuild](../msbuild/msbuild-reference.md)  
[Referência de tarefas do MSBuild](../msbuild/msbuild-task-reference.md)  
[Compilar um aplicativo WPF](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)  
