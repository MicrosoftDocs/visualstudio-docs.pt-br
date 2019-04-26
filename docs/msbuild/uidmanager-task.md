---
title: Tarefa UidManager | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9c4e8c5ccae37aba0f287e2c2f9e29ab36371846
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62938654"
---
# <a name="uidmanager-task"></a>Tarefa UidManager
A tarefa <xref:Microsoft.Build.Tasks.Windows.UidManager> verifica, atualiza ou remove UIDs (identificadores exclusivos), para localizar todos os elementos [!INCLUDE[TLA#tla_xaml](../msbuild/includes/tlasharptla_xaml_md.md)] que são incluídos nos arquivos [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] de origem.

## <a name="task-parameters"></a>Parâmetros de tarefa

| Parâmetro | Descrição |
|-------------------------| - |
| `IntermediateDirectory` | Parâmetro **String** opcional.<br /><br /> Especifica o diretório usado para fazer backup dos arquivos [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] de origem especificados pelo parâmetro **MarkupFiles**. |
| `MarkupFiles` | Parâmetro obrigatório **ITaskItem[]**.<br /><br /> Especifica os arquivos [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] de origem que serão incluídos na verificação, atualização ou remoção de UID. |
| `Task` | Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica a tarefa de gerenciamento de UID que você deseja executar. As opções válidas são **Verificar**, **Atualizar** ou **Remover**. |

## <a name="example"></a>Exemplo
 O exemplo a seguir usa a tarefa <xref:Microsoft.Build.Tasks.Windows.UidManager> para verificar se os arquivos [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] de origem contêm elementos [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] que têm UIDs apropriados.

```xml
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
- [Referência do WPF MSBuild](../msbuild/wpf-msbuild-reference.md)
- [Referência de tarefas](../msbuild/wpf-msbuild-task-reference.md)
- [Referência do MSBuild](../msbuild/msbuild-reference.md)
- [Referência de tarefas](../msbuild/msbuild-task-reference.md)
- [Compilar um aplicativo WPF](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)
- [Como: Localizar um aplicativo](/dotnet/framework/wpf/advanced/how-to-localize-an-application)