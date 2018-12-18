---
title: Tarefa AL (Assembly Linker) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#AL
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- AL task [MSBuild]
- MSBuild, AL task
ms.assetid: 2ddefbf2-5662-4d55-99a6-ac383bf44560
caps.latest.revision: 25
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cf0f5995b9f0e2fca0d909b9d0da0dbe6b386978
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49280469"
---
# <a name="al-assembly-linker-task"></a>Tarefa AL (Assembly Linker)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
A tarefa AL encapsula AL.exe, uma ferramenta que é distribuída com o [!INCLUDE[winsdklong](../includes/winsdklong-md.md)]. Essa ferramenta, o Assembly Linker, é usada para criar um assembly com um manifesto com base em um ou mais arquivos que são arquivos de recurso ou módulos. Compiladores e ambientes de desenvolvimento talvez já forneçam essas funcionalidades, então muitas vezes não é necessário usar essa tarefa diretamente. O Assembly Linker é mais útil para os desenvolvedores que precisam criar um único assembly com base em vários arquivos de componente, como aqueles que podem ser produzidos via desenvolvimento de linguagens mistas. Essa tarefa não combina os módulos em um único arquivo do assembly; os módulos individuais ainda deverão ser distribuídos e estar disponíveis para que o assembly resultante carregue corretamente. Para obter mais informações sobre o AL.exe, consulte [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `AL`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`AlgorithmID`|Parâmetro `String` opcional.<br /><br /> Especifica um algoritmo hash para todos os arquivos em um assembly multiarquivo, exceto o arquivo que contém o manifesto de assembly. Para obter mais informações, consulte a documentação da opção `/algid` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`BaseAddress`|Parâmetro `String` opcional.<br /><br /> Especifica o endereço no qual uma DLL será carregada no computador do usuário no tempo de execução. Os aplicativos serão carregados mais rapidamente se você especificar o endereço básico das DLLs, em vez de deixar o sistema operacional realocar as DLLs no espaço de processo. Esse parâmetro corresponde à opção /base[endereço] [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`CompanyName`|Parâmetro `String` opcional.<br /><br /> Especifica uma cadeia de caracteres para o campo `Company` no assembly. Para obter mais informações, consulte a documentação da opção `/comp[any]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`Configuration`|Parâmetro `String` opcional.<br /><br /> Especifica uma cadeia de caracteres para o campo `Configuration` no assembly. Para obter mais informações, consulte a documentação da opção `/config[uration]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`Copyright`|Parâmetro `String` opcional.<br /><br /> Especifica uma cadeia de caracteres para o campo `Copyright` no assembly. Para obter mais informações, consulte a documentação da opção `/copy[right]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`Culture`|Parâmetro `String` opcional.<br /><br /> Especifica a cadeia de caracteres de cultura a ser associada ao assembly. Para obter mais informações, consulte a documentação da opção `/c[ulture]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`DelaySign`|Parâmetro `Boolean` opcional.<br /><br /> `true` para inserir apenas a chave pública no assembly. `false` para assinar totalmente o assembly. Para obter mais informações, consulte a documentação da opção `/delay[sign]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`Description`|Parâmetro `String` opcional.<br /><br /> Especifica uma cadeia de caracteres para o campo `Description` no assembly. Para obter mais informações, consulte a documentação da opção `/descr[iption]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`EmbedResources`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Incorpora os recursos especificados na imagem que contém o manifesto do assembly. Essa tarefa copia o conteúdo do arquivo de recurso para a imagem. Os itens passados para esse parâmetro podem ter metadados opcionais chamados `LogicalName` e `Access` anexados a eles. Os metadados `LogicalName` são usados para especificar o identificador interno do recurso.  Os metadados `Access` podem ser definidos como `private` para tornar o recurso não visível para outros assemblies. Para obter mais informações, consulte a documentação da opção `/embed[resource]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`EvidenceFile`|Parâmetro `String` opcional.<br /><br /> Insere o arquivo especificado no assembly com o nome do recurso de `Security.Evidence`.<br /><br /> Não é possível usar `Security.Evidence` para recursos comuns. Esse parâmetro corresponde à opção `/e[vidence]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`ExitCode`|Parâmetro somente leitura de saída `Int32` opcional.<br /><br /> Especifica o código de saída fornecido pelo comando executado.|  
|`FileVersion`|Parâmetro `String` opcional.<br /><br /> Especifica uma cadeia de caracteres para o campo `File Version` no assembly. Para obter mais informações, consulte a documentação da opção `/fileversion` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`Flags`|Parâmetro `String` opcional.<br /><br /> Especifica um valor para o campo `Flags` no assembly. Para obter mais informações, consulte a documentação da opção `/flags` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`GenerateFullPaths`|Parâmetro `Boolean` opcional.<br /><br /> Faz com que a tarefa use o caminho absoluto para todos os arquivos reportados em uma mensagem de erro. Esse parâmetro corresponde à opção `/fullpaths` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`KeyContainer`|Parâmetro `String` opcional.<br /><br /> Especifica um contêiner que mantém um par de chaves. Isso assinará o assembly (recebe um nome forte) inserindo uma chave pública no manifesto do assembly. A tarefa assinará então o assembly final com a chave privada. Para obter mais informações, consulte a documentação da opção `/keyn[ame]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`KeyFile`|Parâmetro `String` opcional.<br /><br /> Especifica um arquivo que contém um par de chaves ou apenas uma chave pública para assinar um assembly. O compilador insere a chave pública no manifesto do assembly e, em seguida, assina o assembly final com a chave privada. Para obter mais informações, consulte a documentação da opção `/keyf[ile]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`LinkResources`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Vincula os arquivos de recurso especificados a este assembly. O recurso torna-se parte do assembly, mas o arquivo não é copiado. Os itens passados para esse parâmetro podem ter metadados opcionais chamados `LogicalName`, `Target` e `Access` anexados a eles. Os metadados `LogicalName` são usados para especificar o identificador interno do recurso. Os metadados `Target` podem especificar o caminho e o nome do arquivo para o qual a tarefa copia o arquivo, antes de compilá-lo para dentro do assembly. Os metadados `Access` podem ser definidos como `private` para tornar o recurso não visível para outros assemblies. Para obter mais informações, consulte a documentação da opção `/link[resource]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`MainEntryPoint`|Parâmetro `String` opcional.<br /><br /> Especifica o nome totalmente qualificado (*class.method*) do método a ser usado como um ponto de entrada durante a conversão de um módulo em um arquivo executável. Esse parâmetro corresponde à opção `/main` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`OutputAssembly`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem> necessário.<br /><br /> Especifica o nome do arquivo gerado por essa tarefa. Esse parâmetro corresponde à opção `/out` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`Platform`|Parâmetro `String` opcional.<br /><br /> Limita as plataformas em que este código pode ser executado; deve ser uma entre `x86`, `Itanium`, `x64` e `anycpu`. O padrão é `anycpu`. Esse parâmetro corresponde à opção `/platform` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`ProductName`|Parâmetro `String` opcional.<br /><br /> Especifica uma cadeia de caracteres para o campo `Product` no assembly. Para obter mais informações, consulte a documentação da opção `/prod[uct]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`ProductVersion`|Parâmetro `String` opcional.<br /><br /> Especifica uma cadeia de caracteres para o campo `ProductVersion` no assembly. Para obter mais informações, consulte a documentação da opção `/productv[ersion]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`ResponseFiles`|Parâmetro `String[]` opcional.<br /><br /> Especifica os arquivos de resposta que contêm opções adicionais para passar para o vinculador de Assembly.|  
|`SdkToolsPath`|Parâmetro `String` opcional.<br /><br /> Especifica o caminho para as ferramentas do SDK, por exemplo, resgen.exe.|  
|`SourceModules`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Um ou mais módulos para serem compilados em um assembly. Os módulos serão listados no manifesto do assembly resultante e ainda precisarão ser distribuídos e estar disponíveis para que o assembly seja carregado. Os itens passados para esse parâmetro podem ter metadados adicionais chamados `Target`, que especificam o caminho e o nome do arquivo para o qual a tarefa copia o arquivo, antes de compilá-lo para dentro do assembly. Para obter mais informações, consulte a documentação de [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01). Esse parâmetro corresponde à lista de módulos passados em Al.exe sem uma opção específica.|  
|`TargetType`|Parâmetro `String` opcional.<br /><br /> Especifica o formato do arquivo de saída: `library` (biblioteca de códigos), `exe` (aplicativo de console) ou `win` (aplicativo com base no Windows). O padrão é `library`. Esse parâmetro corresponde à opção `/t[arget]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`TemplateFile`|Parâmetro `String` opcional.<br /><br /> Especifica o assembly do qual todos os metadados de assembly devem ser herdados, exceto o campo de cultura. O assembly especificado deve ter um nome forte.<br /><br /> Um assembly criado com o parâmetro `TemplateFile` será um assembly satélite. Esse parâmetro corresponde à opção `/template` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`Timeout`|Parâmetro `Int32` opcional.<br /><br /> Especifica a quantidade de tempo em milissegundos após o qual o executável da tarefa é encerrado. O valor padrão é `Int.MaxValue`, indicando que não há período de tempo limite.|  
|`Title`|Parâmetro `String` opcional.<br /><br /> Especifica uma cadeia de caracteres para o campo `Title` no assembly. Para obter mais informações, consulte a documentação da opção `/title` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`ToolPath`|Parâmetro `String` opcional.<br /><br /> Especifica o local do qual a tarefa carregará o arquivo executável subjacente (Al.exe). Se esse parâmetro não for especificado, a tarefa usará o caminho de instalação do SDK correspondente à versão da estrutura que está executando [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)].|  
|`Trademark`|Parâmetro `String` opcional.<br /><br /> Especifica uma cadeia de caracteres para o campo `Trademark` no assembly. Para obter mais informações, consulte a documentação da opção `/trade[mark]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`Version`|Parâmetro `String` opcional.<br /><br /> Especifica informações de versão desse assembly. O formato da cadeia de caracteres é *principal.secundária.build.revisão*. O valor padrão é 0. Para obter mais informações, consulte a documentação da opção `/v[ersion]` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`Win32Icon`|Parâmetro `String` opcional.<br /><br /> Insere um arquivo .ico no assembly. O arquivo .ico dá ao arquivo de saída a aparência desejada no Explorador de Arquivos. Esse parâmetro corresponde à opção `/win32icon` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
|`Win32Resource`|Parâmetro `String` opcional.<br /><br /> Insere um recurso Win32 (arquivo .res) no arquivo de saída. Para obter mais informações, consulte a documentação da opção `/win32res` em [Al.exe (Assembly Linker)](http://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01).|  
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.ToolTaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.ToolTask>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Classe base ToolTaskExtension](../msbuild/tooltaskextension-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir cria um assembly com as opções especificadas.  
  
```  
<AL  
    EmbedResources="@(EmbeddedResource)"  
    Culture="%(EmbeddedResource.Culture)"  
    TemplateFile="@(IntermediateAssembly)"  
    KeyContainer="$(KeyContainerName)"  
    KeyFile="$(KeyOriginatorFile)"  
    DelaySign="$(DelaySign)"  
  
    OutputAssembly=  
       "%(EmbeddedResource.Culture)\$(TargetName).resources.dll">  
  
    <Output TaskParameter="OutputAssembly"  
        ItemName="SatelliteAssemblies"/>  
</AL>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Tarefas](../msbuild/msbuild-tasks.md)



