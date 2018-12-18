---
title: Tarefa GenerateTemporaryTargetAssembly | Microsoft Docs
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
- build process [WPF MSBuild], XAML page refers to a locally declared type
- GenerateTemporaryTargetAssembly task [WPF MSBuild]
- GenerateTemporaryTargetAssembly task [WPF MSBuild], parameters
- creating an assembly [WPF MSBuild], XAML page refers to a locally declared type
ms.assetid: 92b6539c-6897-45e0-8989-0c234bbfe782
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1dd1df7ce9d7672917296207e38a846ff69aba5a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49205153"
---
# <a name="generatetemporarytargetassembly-task"></a>Tarefa GenerateTemporaryTargetAssembly
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
A tarefa [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] gera um assembly se pelo menos uma página <xref:Microsoft.Build.Tasks.Windows.GenerateTemporaryTargetAssembly> em um projeto referencia um tipo declarado localmente no projeto. O assembly gerado será removido após concluir o processo de build ou se o processo de build falhar.  
  
## <a name="task-parameters"></a>Parâmetros da tarefa  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`AssemblyName`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o nome curto do assembly que é gerado para um projeto e também é o nome do assembly de destino que é gerado temporariamente. Por exemplo, se um projeto gera um executável [!INCLUDE[TLA#tla_mswin](../includes/tlasharptla-mswin-md.md)] cujo nome é **WinExeAssembly.exe**, o parâmetro **AssemblyName** tem um valor de **WinExeAssembly**.|  
|`CompileTargetName`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o nome do destino [!INCLUDE[TLA#tla_msbuild](../includes/tlasharptla-msbuild-md.md)] que é usado para gerar assemblies de arquivos de código-fonte. O valor típico para **CompileTargetName** é **CoreCompile**.|  
|`CompileTypeName`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o tipo de compilação é executada pelo destino que é especificado pelo parâmetro **CompileTargetName**. Para o destino **CoreCompile**, esse valor é **Compile**.|  
|`CurrentProject`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o caminho completo do arquivo de projeto [!INCLUDE[TLA2#tla_msbuild](../includes/tla2sharptla-msbuild-md.md)] para o projeto que exige um assembly de destino temporário.|  
|`GeneratedCodeFiles`|Parâmetro opcional **ITaskItem[]**.<br /><br /> Especifica a lista de arquivos de código gerenciado específicos a um idioma que foram gerados pela tarefa [MarkupCompilePass1](../msbuild/markupcompilepass1-task.md).|  
|`IntermediateOutputPath`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o diretório em que o assembly de destino temporário é gerado.|  
|`MSBuildBinPath`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o local do **MSBuild.exe**, que é necessário para compilar o assembly de destino temporário.|  
|`ReferencePath`|Parâmetro opcional **ITaskItem[]**.<br /><br /> Especifica uma lista de assemblies, pelo caminho e nome de arquivo, que são referenciados pelos tipos que são compilados no assembly de destino temporário.|  
|`ReferencePathTypeName`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o parâmetro usado pelo parâmetro do destino de compilação (**CompileTargetName**) que especifica a lista de referências de assembly (**ReferencePath**). O valor apropriado é **ReferencePath**.|  
  
## <a name="remarks"></a>Comentários  
 A primeira passagem de compilação de marcação, que é executada pelo [MarkupCompilePass1](../msbuild/markupcompilepass1-task.md), compila arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] em formato binário. Consequentemente, o compilador precisa de uma lista de assemblies referenciados que contêm os tipos que são usados pelos arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)]. No entanto, se um arquivo [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] usa um tipo que é definido no mesmo projeto, um assembly correspondente para esse projeto não é criado até o projeto ser compilado. Portanto, uma referência de assembly não pode ser fornecida durante a primeira passagem de compilação de marcação.  
  
 Em vez disso, **MarkupCompilePass1** adia a conversão de arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] que contêm referências a tipos no mesmo projeto para uma segunda passagem de compilação de marcação, que é executada por [MarkupCompilePass2](../msbuild/markupcompilepass2-task.md). Antes de **MarkupCompilePass2** ser executada, um assembly temporário é gerado. Esse assembly contém os tipos que são usados pelos arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)], cuja passagem de compilação de marcação foi adiada. Uma referência ao assembly gerado é fornecida para **MarkupCompilePass2** quando ela é executada para permitir que os arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] da compilação adiada sejam convertidos em formato binário.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir gera um assembly temporário porque `Page1.xaml` contém uma referência a um tipo que está no mesmo projeto.  
  
```  
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
 [Referência MSBuild do WPF](../msbuild/wpf-msbuild-reference.md)   
 [Referência de tarefas](../msbuild/wpf-msbuild-task-reference.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Compilando um aplicativo WPF (WPF)](http://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)   
 [Visão geral dos aplicativos de navegador XAML do WPF](http://msdn.microsoft.com/library/3a7a86a8-75d5-4898-96b9-73da151e5e16)



