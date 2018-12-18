---
title: Tarefa MarkupCompilePass2 | Microsoft Docs
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
- performing second-pass markup [WPF MSBuild], MarkupCompilePass2 task
- MarkupCompilePass2 task [WPF MSBuild]
- MarkupCompilePass2 task [WPF MSBuild], parameters
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 360a6c4d3e389583eece1adcc915f26091283653
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49942381"
---
# <a name="markupcompilepass2-task"></a>Tarefa MarkupCompilePass2

A tarefa <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> executa a compilação de marcação de segunda passagem em arquivos [!INCLUDE[TLA#tla_xaml](../msbuild/includes/tlasharptla_xaml_md.md)] que fazem referência a tipos no mesmo projeto.

## <a name="task-parameters"></a>Parâmetros de tarefa

| Parâmetro | Descrição |
| - | - |
| `AlwaysCompileMarkupFilesInSeparateDomain` | Parâmetro **Boolean** opcional.<br /><br /> Especifica se a tarefa deve ser executada em um <xref:System.AppDomain> separado. Se esse parâmetro retorna **false**, a tarefa é executada no mesmo <xref:System.AppDomain> que [!INCLUDE[TLA#tla_msbuild](../msbuild/includes/tlasharptla_msbuild_md.md)] e é executada mais rapidamente. Se o parâmetro retorna **true**, a tarefa é executada em um segundo <xref:System.AppDomain> que é isolado de [!INCLUDE[TLA2#tla_msbuild](../msbuild/includes/tla2sharptla_msbuild_md.md)] e é executada de modo mais lento. |
| `AssembliesGeneratedDuringBuild` | Parâmetro **String[]** opcional.<br /><br /> Especifica as referências aos assemblies alterados durante o processo de build. Por exemplo, uma solução do Visual Studio pode conter um projeto que faz referência à saída compilada de outro projeto. Nesse caso, a saída compilada do segundo projeto pode ser adicionada a **AssembliesGeneratedDuringBuild**.<br /><br /> Observação: **AssembliesGeneratedDuringBuild** deve conter referências ao conjunto completo de assemblies que são gerados por uma solução de build. |
| `AssemblyName` | Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o nome curto do assembly que é gerado para um projeto. Por exemplo, se um projeto está gerando um executável [!INCLUDE[TLA#tla_win](../msbuild/includes/tlasharptla_win_md.md)] cujo nome é *WinExeAssembly.exe*, o parâmetro **AssemblyName** tem um valor de **WinExeAssembly**. |
| `GeneratedBaml` | Parâmetro de saída opcional **ITaskItem[]**.<br /><br /> Contém a lista de arquivos gerados no formato binário [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)]. |
| `KnownReferencePaths` | Parâmetro **String[]** opcional.<br /><br /> Especifica as referências aos assemblies nunca alterados durante o processo de build. Inclui assemblies que estão localizados no [!INCLUDE[TLA#tla_gac](../msbuild/includes/tlasharptla_gac_md.md)], em um diretório de instalação [!INCLUDE[TLA#tla_netframewk](../misc/includes/tlasharptla_netframewk_md.md)] e assim por diante. |
| `Language` | Parâmetro obrigatório **String**.<br /><br /> Especifica a linguagem gerenciada à qual o compilador dá suporte. As opções válidas são **C#**, **VB**, **JScript** e **C++**. |
| `LocalizationDirectivesToLocFile` | Parâmetro **String** opcional.<br /><br /> Especifica como gerar informações de localização para cada arquivo [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] de origem. As opções válidas são **None**, **CommentsOnly** e **All**. |
| `OutputPath` | Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o diretório no qual ocorre a geração dos arquivos de formato binário [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] gerados. |
| `OutputType` | Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o tipo de assembly que é gerado por um projeto. As opções válidas são **winexe**, **exe**, **library** e **netmodule**. |
| `References` | Parâmetro opcional **ITaskItem[]**.<br /><br /> Especifica a lista de referências de arquivos para assemblies que contêm os tipos que são usados nos arquivos [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)]. Uma referência é ao assembly gerado pela tarefa <xref:Microsoft.Build.Tasks.Windows.GenerateTemporaryTargetAssembly>, que deve ser executada antes da tarefa <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2>. |
| `RootNamespace` | Parâmetro **String** opcional.<br /><br /> Especifica o namespace raiz para as classes que estão dentro do projeto. **RootNamespace** também é usado como o namespace padrão de um arquivo de código gerenciado gerado quando o arquivo [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] correspondente não inclui o atributo `x:Class`. |
| `XAMLDebuggingInformation` | Parâmetro **Boolean** opcional.<br /><br /> Quando é **true**, informações de diagnóstico são geradas e incluídas no [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] compilado para auxiliar na depuração. |

## <a name="remarks"></a>Comentários

Antes de executar **MarkupCompilePass2**, você deve gerar um assembly temporário que contém os tipos que são usados pelos arquivos [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)], cujas passagens de compilação de marcação foram adiadas. Gere o assembly temporário executando a tarefa **GenerateTemporaryTargetAssembly**.

Uma referência ao assembly temporário gerado é fornecida para <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> quando ele é executado, permitindo que os arquivos [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] cujo build foi adiado na primeira passagem de build de marcação sejam agora compilados em formato binário.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra como usar a tarefa <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> para executar uma compilação de segunda passagem.

```xml
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

[Referência do WPF MSBuild](../msbuild/wpf-msbuild-reference.md)  
[Referência de tarefas do WPF MSBuild](../msbuild/wpf-msbuild-task-reference.md)  
[Referência do MSBuild](../msbuild/msbuild-reference.md)  
[Referência de tarefas do MSBuild](../msbuild/msbuild-task-reference.md)  
[Compilar um aplicativo WPF](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)  
[Visão geral dos aplicativos de navegador XAML do WPF](/dotnet/framework/wpf/app-development/wpf-xaml-browser-applications-overview)