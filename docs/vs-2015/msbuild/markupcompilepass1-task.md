---
title: Tarefa MarkupCompilePass1 | Microsoft Docs
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
- converting XAML to binary format [WPF MSBuild]
- MarkupCompilePass1 task [WPF MSBuild], parameters
- converting XAML projects to compiled binary format [WPF MSBuild]
- MarkupCompilePass1 task [WPF MSBuild], converting XAML to binary format
ms.assetid: 693d6945-fd6f-4698-8f64-9dfcb71052d3
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7db6923b0a729d909e22136bd3994af45dfe1da9
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49189352"
---
# <a name="markupcompilepass1-task"></a>Tarefa MarkupCompilePass1
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
A tarefa <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass1> converte arquivos de projeto [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] não localizáveis para o formato binário compilado.  
  
## <a name="task-parameters"></a>Parâmetros da tarefa  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`AllGeneratedFiles`|Parâmetro de saída opcional **ITaskItem[]**.<br /><br /> Contém uma lista completa dos arquivos que são gerados pela tarefa <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass1>.|  
|`AlwaysCompileMarkupFilesInSeparateDomain`|Parâmetro **Boolean** opcional.<br /><br /> Especifica se a tarefa deve ser executada em um <xref:System.AppDomain> separado. Se esse parâmetro retorna **false**, a tarefa é executada no mesmo <xref:System.AppDomain> que [!INCLUDE[TLA#tla_msbuild](../includes/tlasharptla-msbuild-md.md)] e é executada mais rapidamente. Se o parâmetro retorna **true**, a tarefa é executada em um segundo <xref:System.AppDomain> que é isolado de [!INCLUDE[TLA2#tla_msbuild](../includes/tla2sharptla-msbuild-md.md)] e é executada de modo mais lento.|  
|`ApplicationMarkup`|Parâmetro opcional **ITaskItem[]**.<br /><br /> Especifica o nome do arquivo [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] de definição de aplicativo.|  
|`AssembliesGeneratedDuringBuild`|Parâmetro **String[]** opcional.<br /><br /> Especifica as referências aos assemblies alterados durante o processo de build. Por exemplo, uma solução [!INCLUDE[TLA#tla_visualstu2005](../includes/tlasharptla-visualstu2005-md.md)] pode conter um projeto que faz referência à saída compilada de outro projeto. Nesse caso, a saída compilada do segundo projeto pode ser adicionada ao parâmetro **AssembliesGeneratedDuringBuild**.<br /><br /> Observação: o parâmetro **AssembliesGeneratedDuringBuild** deve conter referências ao conjunto completo de assemblies que são gerados por uma solução de build.|  
|`AssemblyName`|Parâmetro obrigatório **string**.<br /><br /> Especifica o nome curto do assembly que é gerado para um projeto. Por exemplo, se um projeto está gerando um executável [!INCLUDE[TLA#tla_mswin](../includes/tlasharptla-mswin-md.md)] cujo nome é **WinExeAssembly.exe**, o parâmetro **AssemblyName** tem um valor de **WinExeAssembly**.|  
|`AssemblyPublicKeyToken`|Parâmetro **String** opcional.<br /><br /> Especifica o token da chave pública para o assembly.|  
|`AssemblyVersion`|Parâmetro **String** opcional.<br /><br /> Especifica o número de versão do assembly.|  
|`ContentFiles`|Parâmetro opcional **ITaskItem[]**.<br /><br /> Especifica a lista de arquivos de conteúdo flexível.|  
|`DefineConstants`|Parâmetro **String** opcional.<br /><br /> Especifica que o valor atual de **DefineConstants** é mantido. o que a afeta a geração do assembly de destino. se esse parâmetro é alterado, a API pública do assembly de destino pode ser alterada e a compilação de arquivos [!INCLUDE[TLA2#tla_titlexaml](../includes/tla2sharptla-titlexaml-md.md)] que fazem referência a tipos de locais pode ser afetada.|  
|`ExtraBuildControlFiles`|Parâmetro opcional **ITaskItem[]**.<br /><br /> Especifica uma lista de arquivos que controlam se uma recompilação é disparada quando a tarefa <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass1> é executada novamente, uma recompilação será acionada se um desses arquivos for alterado.|  
|`GeneratedBamlFiles`|Parâmetro de saída opcional **ITaskItem[]**.<br /><br /> Contém a lista de arquivos gerados no formato binário [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)].|  
|`GeneratedCodeFiles`|Parâmetro de saída opcional **ITaskItem[]**.<br /><br /> Contém a lista de arquivos de código gerenciado gerados.|  
|`GeneratedLocalizationFiles`|Parâmetro de saída opcional **ITaskItem[]**.<br /><br /> Contém a lista de arquivos de localização que foram gerados para cada arquivo [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] localizável.|  
|`HostInBrowser`|Parâmetro **String** opcional.<br /><br /> Especifica se o assembly gerado é um [!INCLUDE[TLA#tla_xbap](../includes/tlasharptla-xbap-md.md)]. As opções válidas são **true** e **false**. Se for **true**, código será gerado para dar suporte à hospedagem de navegador.|  
|`KnownReferencePaths`|Parâmetro **String[]** opcional.<br /><br /> Especifica as referências aos assemblies que não são alterados durante o processo de build. Inclui assemblies que estão localizados no [!INCLUDE[TLA#tla_gac](../includes/tlasharptla-gac-md.md)], em um diretório de instalação [!INCLUDE[TLA#tla_netframewk](../includes/tlasharptla-netframewk-md.md)] e assim por diante.|  
|`Language`|Parâmetro obrigatório **String**.<br /><br /> Especifica a linguagem gerenciada à qual o compilador dá suporte. As opções válidas são **C#**, **VB**, **JScript** e **C++**.|  
|`LanguageSourceExtension`|Parâmetro **String** opcional.<br /><br /> Especifica a extensão que é acrescentada à extensão do arquivo de código gerenciado gerado:<br /><br /> `<Filename>.g<LanguageSourceExtension>`<br /><br /> Se o parâmetro **LanguageSourceExtension** não está definido com um valor específico, a extensão de nome de arquivo de origem padrão para uma linguagem é usada: **.vb** para [!INCLUDE[TLA#tla_visualb](../includes/tlasharptla-visualb-md.md)], **.csharp** para [!INCLUDE[TLA#tla_cshrp](../includes/tlasharptla-cshrp-md.md)].|  
|`LocalizationDirectivesToLocFile`|Parâmetro **String** opcional.<br /><br /> Especifica como gerar informações de localização para cada arquivo [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] de origem. As opções válidas são **None**, **CommentsOnly** e **All**.|  
|`OutputPath`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o diretório no qual ocorre a geração dos arquivos de código gerenciado e arquivos de formato binário [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] gerados.|  
|`OutputType`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o tipo de assembly que é gerado por um projeto. As opções válidas são **winexe**, **exe**, **library** e **netmodule**.|  
|`PageMarkup`|Parâmetro opcional **ITaskItem[]**.<br /><br /> Especifica uma lista de arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] para processar.|  
|`References`|Parâmetro opcional **ITaskItem[]**.<br /><br /> Especifica a lista de referências de arquivos para assemblies que contêm os tipos que são usados nos arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)].|  
|`RequirePass2ForMainAssembly`|Parâmetro de saída opcional **Boolean**.<br /><br /> Indica se o projeto contém arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] não localizáveis que fazem referência a tipos de locais que são inseridos no assembly principal.|  
|`RequirePass2ForSatelliteAssembly`|Parâmetro de saída opcional **Boolean**.<br /><br /> Indica se o projeto contém arquivos [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] localizáveis que fazem referência a tipos de locais que são inseridos no assembly principal.|  
|`RootNamespace`|Parâmetro **String** opcional.<br /><br /> Especifica o namespace raiz para as classes que estão dentro do projeto. **RootNamespace** também é usado como o namespace padrão de um arquivo de código gerenciado gerado quando o arquivo [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] correspondente não inclui o atributo `x:Class`.|  
|`SourceCodeFiles`|Parâmetro opcional **ITaskItem[]**.<br /><br /> Especifica a lista de arquivos de código para o projeto atual. A lista não inclui arquivos de código gerenciado específicos a um idioma gerados.|  
|`UICulture`|Parâmetro **String** opcional.<br /><br /> Especifica o assembly satélite para a cultura de interface do usuário em que os arquivos de formato binário [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] gerados são inseridos. Se **UICulture** não estiver definido, arquivos de formato binário [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] gerados serão inseridos no assembly principal.|  
|`XAMLDebuggingInformation`|Parâmetro **Boolean** opcional.<br /><br /> Quando é **true**, informações de diagnóstico são geradas e incluídas no [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] compilado para auxiliar na depuração.|  
  
## <a name="remarks"></a>Comentários  
 A tarefa <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass1> normalmente compila [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] em um formato binário e gera arquivos de código. Se um arquivo [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] contém referências a tipos definidos no mesmo projeto, sua compilação para o formato binário é adiada por **MarkupCompilePass1** para uma segunda passagem de compilação de marcação (**MarkupCompilePass2**). Esses arquivos devem ter sua compilação adiada porque eles devem aguardar até que os tipos referenciados definidos localmente sejam compilados. No entanto, se um arquivo [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] tiver um atributo `x:Class`, <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass1> gerará o arquivo de código específico da linguagem para ele.  
  
 Um arquivo [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] é localizável se ele contém elementos que usam o atributo `x:Uid`:  
  
```  
<Page x:Class="WPFMSBuildSample.Page1"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    x:Uid="Page1Uid"  
    >  
  ...  
</Page>  
```  
  
 Um arquivo [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] faz referência a um tipo definido localmente quando ele declara um namespace [!INCLUDE[TLA#tla_xml](../includes/tlasharptla-xml-md.md)] que usa o valor `clr-namespace` para se referir a um namespace do projeto atual:  
  
```  
<Page x:Class="WPFMSBuildSample.Page1"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:localNamespace="clr-namespace:WPFMSBuildSample"  
    >  
    <Grid>  
      <Grid.Resources>  
        <localNameSpace:LocalType x:Key="localType" />  
      </Grid.Resources>  
      ...  
    </Grid>  
</Page>  
```  
  
 Se qualquer arquivo [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] for localizável ou fizer referência a um tipo definido localmente, uma segunda passagem de compilação de marcação será necessária, o que exigirá a execução de [GenerateTemporaryTargetAssembly](../msbuild/generatetemporarytargetassembly-task.md) e, em seguida, de [MarkupCompilePass2](../msbuild/markupcompilepass2-task.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como converter três arquivos `Page`[!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] em arquivos de formato binário. `Page1` contém uma referência a um tipo, `Class1`, que está no namespace raiz do projeto e, portanto, não é convertido em arquivos de formato binário nessa passagem de compilação de marcação. Em vez disso, o [GenerateTemporaryTargetAssembly](../msbuild/generatetemporarytargetassembly-task.md) é executado e é seguido de [MarkupCompilePass2](../msbuild/markupcompilepass2-task.md).  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <UsingTask   
    TaskName="Microsoft.Build.Tasks.Windows.MarkupCompilePass1"   
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />  
  <Target Name="MarkupCompilePass1Task">  
    <MarkupCompilePass1   
      AssemblyName="WPFMSBuildSample"  
      Language="C#"  
      OutputType="WinExe"  
      OutputPath="obj\Debug\"  
      ApplicationMarkup="App.xaml"  
      PageMarkup="Page1.xaml;Page2.xaml;Page3.xaml"  
      SourceCodeFiles="Class1.cs"  
      References="c:\windows\Microsoft.net\Framework\v2.0.50727\System.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationCore.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationFramework.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\WindowsBase.dll" />  
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



