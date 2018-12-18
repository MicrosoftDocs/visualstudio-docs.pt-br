---
title: Tarefa MarkupCompilePass2 | Microsoft Docs
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
- performing second-pass markup [WPF MSBuild], MarkupCompilePass2 task
- MarkupCompilePass2 task [WPF MSBuild]
- MarkupCompilePass2 task [WPF MSBuild], parameters
ms.assetid: 1d25689a-d21f-4b05-be26-95aa0ed4fd03
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ea61e827bfae47c3bea961cb15c208f585aa6ed9
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49179206"
---
# <a name="markupcompilepass2-task"></a>Tarefa MarkupCompilePass2
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
A tarefa <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> executa a compilação de marcação de segunda passagem em arquivos [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] que fazem referência a tipos no mesmo projeto.  
  
## <a name="task-parameters"></a>Parâmetros da tarefa  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`AlwaysCompileMarkupFilesInSeparateDomain`|Parâmetro **Boolean** opcional.<br /><br /> Especifica se a tarefa deve ser executada em um <xref:System.AppDomain> separado. Se esse parâmetro retorna **false**, a tarefa é executada no mesmo <xref:System.AppDomain> que [!INCLUDE[TLA#tla_msbuild](../includes/tlasharptla-msbuild-md.md)] e é executada mais rapidamente. Se o parâmetro retorna **true**, a tarefa é executada em um segundo <xref:System.AppDomain> que é isolado de [!INCLUDE[TLA2#tla_msbuild](../includes/tla2sharptla-msbuild-md.md)] e é executada de modo mais lento.|  
|`AssembliesGeneratedDuringBuild`|Parâmetro **String[]** opcional.<br /><br /> Especifica as referências aos assemblies alterados durante o processo de build. Por exemplo, uma solução [!INCLUDE[TLA#tla_visualstu2005](../includes/tlasharptla-visualstu2005-md.md)] pode conter um projeto que faz referência à saída compilada de outro projeto. Nesse caso, a saída compilada do segundo projeto pode ser adicionada a **AssembliesGeneratedDuringBuild**.<br /><br /> Observação: **AssembliesGeneratedDuringBuild** deve conter referências ao conjunto completo de assemblies que são gerados por uma solução de build.|  
|`AssemblyName`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o nome curto do assembly que é gerado para um projeto. Por exemplo, se um projeto está gerando um executável [!INCLUDE[TLA#tla_win](../includes/tlasharptla-win-md.md)] cujo nome é **WinExeAssembly.exe**, o parâmetro **AssemblyName** tem um valor de **WinExeAssembly**.|  
|`GeneratedBaml`|Parâmetro de saída opcional **ITaskItem[]**.<br /><br /> Contém a lista de arquivos gerados no formato binário [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)].|  
|`KnownReferencePaths`|Parâmetro **String[]** opcional.<br /><br /> Especifica as referências aos assemblies nunca alterados durante o processo de build. Inclui assemblies que estão localizados no [!INCLUDE[TLA#tla_gac](../includes/tlasharptla-gac-md.md)], em um diretório de instalação [!INCLUDE[TLA#tla_netframewk](../includes/tlasharptla-netframewk-md.md)] e assim por diante.|  
|`Language`|Parâmetro obrigatório **String**.<br /><br /> Especifica a linguagem gerenciada à qual o compilador dá suporte. As opções válidas são **C#**, **VB**, **JScript** e **C++**.|  
|`LocalizationDirectivesToLocFile`|Parâmetro **String** opcional.<br /><br /> Especifica como gerar informações de localização para cada arquivo [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] de origem. As opções válidas são **None**, **CommentsOnly** e **All**.|  
|`OutputPath`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o diretório no qual ocorre a geração dos arquivos de formato binário [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] gerados.|  
|`OutputType`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o tipo de assembly que é gerado por um projeto. As opções válidas são **winexe**, **exe**, **library** e **netmodule**.|  
|`References`|Parâmetro opcional **ITaskItem[]**.<br /><br /> Especifica a lista de referências de arquivos para assemblies que contêm os tipos que são usados nos arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)]. Uma referência é ao assembly gerado pela tarefa <xref:Microsoft.Build.Tasks.Windows.GenerateTemporaryTargetAssembly>, que deve ser executada antes da tarefa <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2>.|  
|`RootNamespace`|Parâmetro **String** opcional.<br /><br /> Especifica o namespace raiz para as classes que estão dentro do projeto. **RootNamespace** também é usado como o namespace padrão de um arquivo de código gerenciado gerado quando o arquivo [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] correspondente não inclui o atributo `x:Class`.|  
|`XAMLDebuggingInformation`|Parâmetro **Boolean** opcional.<br /><br /> Quando é **true**, informações de diagnóstico são geradas e incluídas no [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] compilado para auxiliar na depuração.|  
  
## <a name="remarks"></a>Comentários  
 Antes de executar **MarkupCompilePass2**, você deve gerar um assembly temporário que contém os tipos que são usados pelos arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)], cujas passagens de compilação de marcação foram adiadas. Gere o assembly temporário executando a tarefa **GenerateTemporaryTargetAssembly**.  
  
 Uma referência ao assembly temporário gerado é fornecida para <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> quando ele é executado, permitindo que os arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] cujo build foi adiado na primeira passagem de build de marcação sejam agora compilados em formato binário.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar a tarefa <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> para executar uma compilação de segunda passagem.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <UsingTask   
    TaskName="Microsoft.Build.Tasks.Windows.MarkupCompilePass2"   
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />  
  <Target Name="MarkupCompilePass2Task">  
    <MarkupCompilePass2   
      AssemblyName="WPFMSBuildSample"  
      Language="C#"  
      OutputType="WinExe"  
      OutputPath="obj\Debug\"  
      References=".\obj\debug\WPFMSBuildSample.exe;c:\windows\Microsoft.net\Framework\v2.0.50727\System.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationCore.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationFramework.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\WindowsBase.dll" />  
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



