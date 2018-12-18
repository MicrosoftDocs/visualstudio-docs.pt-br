---
title: Tarefa GenerateTemporaryTargetAssembly | Microsoft Docs
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
- build process [WPF MSBuild], XAML page refers to a locally declared type
- GenerateTemporaryTargetAssembly task [WPF MSBuild]
- GenerateTemporaryTargetAssembly task [WPF MSBuild], parameters
- creating an assembly [WPF MSBuild], XAML page refers to a locally declared type
ms.assetid: 92b6539c-6897-45e0-8989-0c234bbfe782
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5d4b5ee29ed19f121c6da357fa20242f6762e51c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49892942"
---
# <a name="generatetemporarytargetassembly-task"></a>Tarefa GenerateTemporaryTargetAssembly
A tarefa [!INCLUDE[TLA#tla_xaml](../msbuild/includes/tlasharptla_xaml_md.md)] gera um assembly se pelo menos uma página <xref:Microsoft.Build.Tasks.Windows.GenerateTemporaryTargetAssembly> em um projeto referencia um tipo declarado localmente no projeto. O assembly gerado será removido após concluir o processo de build ou se o processo de build falhar.  
  
## <a name="task-parameters"></a>Parâmetros de tarefa  
  
| Parâmetro | Descrição |
|--------------------------| - |
| `AssemblyName` | Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o nome curto do assembly que é gerado para um projeto e também é o nome do assembly de destino que é gerado temporariamente. Por exemplo, se um projeto gera um executável [!INCLUDE[TLA#tla_mswin](../code-quality/includes/tlasharptla_mswin_md.md)] cujo nome é *WinExeAssembly.exe*, o parâmetro **AssemblyName** tem um valor de **WinExeAssembly**. |
| `CompileTargetName` | Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o nome do destino [!INCLUDE[TLA#tla_msbuild](../msbuild/includes/tlasharptla_msbuild_md.md)] que é usado para gerar assemblies de arquivos de código-fonte. O valor típico para **CompileTargetName** é **CoreCompile**. |
| `CompileTypeName` | Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o tipo de compilação é executada pelo destino que é especificado pelo parâmetro **CompileTargetName**. Para o destino **CoreCompile**, esse valor é **Compile**. |
| `CurrentProject` | Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o caminho completo do arquivo de projeto [!INCLUDE[TLA2#tla_msbuild](../msbuild/includes/tla2sharptla_msbuild_md.md)] para o projeto que exige um assembly de destino temporário. |
| `GeneratedCodeFiles` | Parâmetro opcional **ITaskItem[]**.<br /><br /> Especifica a lista de arquivos de código gerenciado específicos a um idioma que foram gerados pela tarefa [MarkupCompilePass1](../msbuild/markupcompilepass1-task.md). |
| `IntermediateOutputPath` | Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o diretório em que o assembly de destino temporário é gerado. |
| `MSBuildBinPath` | Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o local do *MSBuild.exe*, que é necessário para compilar o assembly de destino temporário. |
| `ReferencePath` | Parâmetro opcional **ITaskItem[]**.<br /><br /> Especifica uma lista de assemblies, pelo caminho e nome de arquivo, que são referenciados pelos tipos que são compilados no assembly de destino temporário. |
| `ReferencePathTypeName` | Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o parâmetro usado pelo parâmetro do destino de compilação (**CompileTargetName**) que especifica a lista de referências de assembly (**ReferencePath**). O valor apropriado é **ReferencePath**. |
  
## <a name="remarks"></a>Comentários  
 A primeira passagem de compilação de marcação, que é executada pelo [MarkupCompilePass1](../msbuild/markupcompilepass1-task.md), compila arquivos [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] em formato binário. Consequentemente, o compilador precisa de uma lista de assemblies referenciados que contêm os tipos que são usados pelos arquivos [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)]. No entanto, se um arquivo [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] usa um tipo que é definido no mesmo projeto, um assembly correspondente para esse projeto não é criado até o projeto ser compilado. Portanto, uma referência de assembly não pode ser fornecida durante a primeira passagem de compilação de marcação.  
  
 Em vez disso, **MarkupCompilePass1** adia a conversão de arquivos [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] que contêm referências a tipos no mesmo projeto para uma segunda passagem de compilação de marcação, que é executada por [MarkupCompilePass2](../msbuild/markupcompilepass2-task.md). Antes de **MarkupCompilePass2** ser executada, um assembly temporário é gerado. Esse assembly contém os tipos que são usados pelos arquivos [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)], cuja passagem de compilação de marcação foi adiada. Uma referência ao assembly gerado é fornecida para **MarkupCompilePass2** quando ela é executada para permitir que os arquivos [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] da compilação adiada sejam convertidos em formato binário.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir gera um assembly temporário porque *Page1.xaml* contém uma referência a um tipo que está no mesmo projeto.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <UsingTask  
    TaskName="Microsoft.Build.Tasks.Windows.GenerateTemporaryTargetAssembly"   
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />  
  <Target Name="GenerateTemporaryTargetAssemblyTask">  
    <GenerateTemporaryTargetAssembly  
      AssemblyName="WPFMSBuildSample"  
      CompileTargetName="CoreCompile"  
      CompileTypeName="Compile"  
      CurrentProject="FullBuild.proj"  
      GeneratedCodeFiles="obj\debug\app.g.cs;obj\debug\Page1.g.cs;obj\debug\Page2.g.cs"  
      ReferencePath="c:\windows\Microsoft.net\Framework\v2.0.50727\System.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationCore.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationFramework.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\WindowsBase.dll"  
      IntermediateOutputPath=".\obj\debug\"  
      MSBuildBinPath="$(MSBuildBinPath)"  
      ReferencePathTypeName="ReferencePath"/>  
  </Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência do WPF MSBuild](../msbuild/wpf-msbuild-reference.md)   
 [Referência de tarefas](../msbuild/wpf-msbuild-task-reference.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Compilar um aplicativo WPF](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)   
 [Visão geral dos aplicativos de navegador XAML do WPF](/dotnet/framework/wpf/app-development/wpf-xaml-browser-applications-overview)