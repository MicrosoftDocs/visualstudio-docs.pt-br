---
title: Tarefa MT | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- VC.Project.VCManifestTool.ResourceOutputFileName
- VC.Project.VCManifestTool.SuppressDependencyElement
- VC.Project.VCManifestTool.ManifestFromManagedAssembly
- VC.Project.VCManifestTool.GenerateCategoryTags
- VC.Project.VCManifestTool.EnableDPIAwareness
- vc.task.mt
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBUILD (Visual C++), MT task
- MT task (MSBuild (Visual C++))
ms.assetid: bb94913c-1042-4968-9f08-b394518e899f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c6e4298fa9482674232dea2cae98bb25ba51be30
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219868"
---
# <a name="mt-task"></a>tarefa MT
Encapsula a Ferramenta de Manifesto da Microsoft, *mt.exe*. Para saber mais, confira [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa **MT**. A maioria dos parâmetros de tarefa e alguns conjuntos de parâmetros correspondem a uma opção de linha de comando.  
  
> [!NOTE]
>  A documentação da *mt.exe* usa um hífen (**-**) como prefixo para opções de linha de comando, mas este tópico usa uma barra (**/**). Qualquer um desses prefixos é aceitável.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|**AdditionalManifestFiles**|Parâmetro **String[]** opcional.<br /><br /> Especifica o nome de um ou mais arquivos de manifesto.<br /><br /> Para saber mais, confira a opção **/manifest** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**AdditionalOptions**|Parâmetro **String** opcional.<br /><br /> Uma lista de opções de linha de comando. Por exemplo, /\<option1> /\<option2> /\<option#>. Use esse parâmetro para especificar opções de linha de comando não representadas por nenhum outro parâmetro da tarefa **MT**.<br /><br /> Para saber mais, confira [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**AssemblyIdentity**|Parâmetro **String** opcional.<br /><br /> Especifica os valores de atributo do elemento **assemblyIdentity** do manifesto. Especifique uma lista delimitada por vírgulas, em que o primeiro componente é o valor do atributo `name` seguido por um ou mais pares nome-valor que tenham o formulário, por exemplo: *\<attribute name>=<attribute_value>*.<br /><br /> Para saber mais, confira a opção **/identity** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**ComponentFileName**|Parâmetro **String** opcional.<br /><br /> Especifica o nome da biblioteca de vínculo dinâmico a ser criada com base nos arquivos *.rgs* ou *.tlb*. Esse parâmetro é necessário ao especificar os parâmetros de tarefa MT **RegistrarScriptFile** ou **TypeLibraryFile**.<br /><br /> Para saber mais, confira a opção **/dll** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**DependencyInformationFile**|Parâmetro **String** opcional.<br /><br /> Especifica o arquivo das informações de dependência usado pelo Visual Studio para rastrear as informações de dependência de compilação para a ferramenta de manifesto.|  
|**EmbedManifest**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, incorpora o arquivo de manifesto no assembly. Se `false`, cria um arquivo de manifesto autônomo.|  
|**EnableDPIAwareness**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, adiciona as informações de manifesto que marcam o aplicativo como com reconhecimento de DPI. O registro de um aplicativo com reconhecimento de DPI melhora a aparência da interface do usuário de forma consistente em uma ampla variedade de configurações de exibição com alto DPI.<br /><br /> Para saber mais, confira [Alto DPI](https://docs.microsoft.com/windows/desktop/win7devguide/high-dpi).|  
|**GenerateCatalogFiles**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, gera arquivos de definição de catálogo (*.cdf*).<br /><br /> Para saber mais, confira a opção **/makecdfs** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**GenerateCategoryTags**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, faz com que as marcas de categoria sejam geradas. Se esse parâmetro for `true`, o parâmetro de tarefa **ManifestFromManagedAssemblyMT** também deverá ser especificado.<br /><br /> Para saber mais, confira a opção **/category** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**InputResourceManifests**|Parâmetro **String** opcional.<br /><br /> A entrada do manifesto por meio de um recurso do tipo RT_MANIFEST que tem o identificador especificado. Especifique um recurso do formulário, \<file>[;[#]\<resource_id>], em que o parâmetro \<resource_id> opcional seja um número não negativo de 16 bits.<br /><br /> Se nenhum `resource_id` for especificado, o valor padrão (1) CREATEPROCESS_MANIFEST_RESOURCE será usado.<br /><br /> Para saber mais, confira a opção **/inputresource** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**ManifestFromManagedAssembly**|Parâmetro **String** opcional.<br /><br /> Gera um manifesto do assembly gerenciado especificado.<br /><br /> Para saber mais, confira a opção **/managedassemblyname** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**ManifestToIgnore**|Parâmetro **String** opcional.<br /><br /> (Não usado).|  
|**OutputManifestFile**|Parâmetro **String** opcional.<br /><br /> Especifica o nome do manifesto de saída. Se esse parâmetro for omitido e somente um manifesto for operado, esse manifesto será modificado.<br /><br /> Para saber mais, confira a opção **/out** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**OutputResourceManifests**|Parâmetro **String** opcional.<br /><br /> A saída do manifesto por meio de um recurso do tipo RT_MANIFEST que tem o identificador especificado. O formato do recurso é \<file>[;[#]\<resource_id>], em que o parâmetro \<resource_id> opcional é um número não negativo de 16 bits.<br /><br /> Se nenhum `resource_id` for especificado, o valor padrão (1) CREATEPROCESS_MANIFEST_RESOURCE será usado.<br /><br /> Para saber mais, confira a opção **/outputresource** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**RegistrarScriptFile**|Parâmetro **String** opcional.<br /><br /> Especifica o nome do arquivo de script de registrador (*.rgs*) a ser usado para suporte ao manifesto COM sem registro.<br /><br /> Para saber mais, confira a opção **/rgs** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**ReplacementsFile**|Parâmetro **String** opcional.<br /><br /> Especifica o arquivo que contém valores para cadeias de caracteres substituíveis no arquivo registrador (*.rgs*).<br /><br /> Para saber mais, confira a opção **/replacements** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**ResourceOutputFileName**|Parâmetro **String** opcional.<br /><br /> Especifica o arquivo de recurso de saída usado para inserir o manifesto na saída do projeto.|  
|**Sources**|Parâmetro `ITaskItem[]` opcional.<br /><br /> Especifica uma lista de arquivos de manifesto de origem separados por espaços.<br /><br /> Para saber mais, confira a opção **/manifest** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**SuppressDependencyElement**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, gera um manifesto sem elementos de dependência. Se esse parâmetro for `true`, o parâmetro de tarefa **ManifestFromManagedAssemblyMT** também deverá ser especificado.<br /><br /> Para saber mais, confira a opção **/nodependency** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**SuppressStartupBanner**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, impedirá a exibição da mensagem de direitos autorais e de número de versão quando a tarefa for iniciada.<br /><br /> Para saber mais, confira a opção **/nologo** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**TrackerLogDirectory**|Parâmetro `String` opcional.<br /><br /> Especifica o diretório intermediário em que os logs de rastreamento para essa tarefa são armazenados.|  
|**TypeLibraryFile**|Parâmetro **String** opcional.<br /><br /> Especifica o nome do arquivo de biblioteca de tipos (*.tlb*). Ao especificar esse parâmetro, especifique também o parâmetro de tarefa **ComponentFileNameMT**.<br /><br /> Para saber mais, confira a opção **/tlb** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
|**UpdateFileHashes**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, calcula o valor de hash dos arquivos no caminho especificado pelo parâmetro de tarefa **UpdateFileHashesSearchPathMT** e, em seguida, atualiza o valor do atributo **hash** do elemento de **arquivo** do manifesto usando o valor calculado.<br /><br /> Para saber mais, confira a opção **/hashupdate** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe). Consulte também o parâmetro **UpdateFileHashesSearchPath** nesta tabela.|  
|**UpdateFileHashesSearchPath**|Parâmetro `String` opcional.<br /><br /> Especifica o caminho de pesquisa a ser usado quando os hashes de arquivo são atualizados. Use esse parâmetro com o parâmetro de tarefa **UpdateFileHashesMT**.<br /><br /> Para obter mais informações, consulte o parâmetro **UpdateFileHashes** nesta tabela.|  
|**VerboseOutput**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, exibe informações de depuração detalhadas.<br /><br /> Para saber mais, confira a opção **/verbose** em [Mt.exe](https://docs.microsoft.com/windows/desktop/SbsCs/mt-exe).|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)