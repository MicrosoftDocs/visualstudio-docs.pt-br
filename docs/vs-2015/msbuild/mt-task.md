---
title: Tarefa MT | Microsoft Docs
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
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c9b14de0b9e80379736dd7f6a02cb374d475fcda
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49214913"
---
# <a name="mt-task"></a>Tarefa MT
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Encapsula a Ferramenta de Manifesto da Microsoft, a mt.exe. Para obter mais informações, consulte “Mt.exe” no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa **MT**. A maioria dos parâmetros de tarefa e alguns conjuntos de parâmetros correspondem a uma opção de linha de comando.  
  
> [!NOTE]
>  A documentação da mt.exe usa um hífen (**-**) como prefixo para opções de linha de comando, mas este tópico usa uma barra (**/**). Qualquer um desses prefixos é aceitável.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|**AdditionalManifestFiles**|Parâmetro **String[]** opcional.<br /><br /> Especifica o nome de um ou mais arquivos de manifesto.<br /><br /> Para obter mais informações, consulte a opção **/manifest** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**AdditionalOptions**|Parâmetro **String** opcional.<br /><br /> Uma lista de opções de linha de comando. Por exemplo, "*/option1 /option2 /option#*". Use esse parâmetro para especificar opções de linha de comando não representadas por nenhum outro parâmetro da tarefa **MT**.<br /><br /> Para obter mais informações, consulte “Mt.exe” no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**AssemblyIdentity**|Parâmetro **String** opcional.<br /><br /> Especifica os valores de atributo do elemento **assemblyIdentity** do manifesto. Especifique uma lista delimitada por vírgulas, em que o primeiro componente é o valor do atributo `name` seguido por um ou mais pares nome-valor que tenham o formulário, por exemplo: *\<attribute name>=<attribute_value>*.<br /><br /> Para obter mais informações, consulte a opção **/identity** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**ComponentFileName**|Parâmetro **String** opcional.<br /><br /> Especifica o nome da biblioteca de vínculo dinâmico a ser criada com base nos arquivos .rgs ou .tlb. Esse parâmetro é necessário ao especificar os parâmetros de tarefa MT **RegistrarScriptFile** ou **TypeLibraryFile**.<br /><br /> Para obter mais informações, consulte a opção **/dll** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**DependencyInformationFile**|Parâmetro **String** opcional.<br /><br /> Especifica o arquivo das informações de dependência usado pelo Visual Studio para rastrear as informações de dependência de compilação para a ferramenta de manifesto.|  
|**EmbedManifest**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, incorpora o arquivo de manifesto no assembly. Se `false`, cria um arquivo de manifesto autônomo.|  
|**EnableDPIAwareness**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, adiciona as informações de manifesto que marcam o aplicativo como com reconhecimento de DPI. O registro de um aplicativo com reconhecimento de DPI melhora a aparência da interface do usuário de forma consistente em uma ampla variedade de configurações de exibição com alto DPI.<br /><br /> Para obter mais informações, consulte “Alto DPI” no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**GenerateCatalogFiles**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, gera arquivos de definição de catálogo (.cdf).<br /><br /> Para obter mais informações, consulte a opção **/makecdfs** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**GenerateCategoryTags**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, faz com que as marcas de categoria sejam geradas. Se esse parâmetro for `true`, o parâmetro de tarefa **ManifestFromManagedAssemblyMT** também deverá ser especificado.<br /><br /> Para obter mais informações, consulte a opção **/category** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**InputResourceManifests**|Parâmetro **String** opcional.<br /><br /> A entrada do manifesto por meio de um recurso do tipo RT_MANIFEST que tem o identificador especificado. Especifique um recurso do formulário, _\<file>[_**;**_[_**#**_]<resource_id>]_, em que o parâmetro `resource_id` opcional seja um número não negativo de 16 bits.<br /><br /> Se nenhum `resource_id` for especificado, o valor padrão (1) CREATEPROCESS_MANIFEST_RESOURCE será usado.<br /><br /> Para obter mais informações, consulte a opção **/inputresource** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**ManifestFromManagedAssembly**|Parâmetro **String** opcional.<br /><br /> Gera um manifesto do assembly gerenciado especificado.<br /><br /> Para obter mais informações, consulte a opção **/managedassemblyname** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**ManifestToIgnore**|Parâmetro **String** opcional.<br /><br /> (Não usado).|  
|**OutputManifestFile**|Parâmetro **String** opcional.<br /><br /> Especifica o nome do manifesto de saída. Se esse parâmetro for omitido e somente um manifesto for operado, esse manifesto será modificado.<br /><br /> Para obter mais informações, consulte a opção **/out** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**OutputResourceManifests**|Parâmetro **String** opcional.<br /><br /> A saída do manifesto por meio de um recurso do tipo RT_MANIFEST que tem o identificador especificado. O recurso é do formulário, _\<file>[_**;**_[_**#**_]<resource_id>]_, em que o parâmetro `resource_id` opcional é um número não negativo de 16 bits.<br /><br /> Se nenhum `resource_id` for especificado, o valor padrão (1) CREATEPROCESS_MANIFEST_RESOURCE será usado.<br /><br /> Para obter mais informações, consulte a opção **/outputresource** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**RegistrarScriptFile**|Parâmetro **String** opcional.<br /><br /> Especifica o nome do arquivo script de registrador (.rgs) a ser usado para suporte ao manifesto COM sem registro.<br /><br /> Para obter mais informações, consulte a opção **/rgs** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**ReplacementsFile**|Parâmetro **String** opcional.<br /><br /> Especifica o arquivo que contém valores para cadeias de caracteres substituíveis no arquivo registrador (.rgs).<br /><br /> Para obter mais informações, consulte a opção **/replacements** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**ResourceOutputFileName**|Parâmetro **String** opcional.<br /><br /> Especifica o arquivo de recurso de saída usado para inserir o manifesto na saída do projeto.|  
|**Sources**|Parâmetro `ITaskItem[]` opcional.<br /><br /> Especifica uma lista de arquivos de manifesto de origem separados por espaços.<br /><br /> Para obter mais informações, consulte a opção **/manifest** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**SuppressDependencyElement**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, gera um manifesto sem elementos de dependência. Se esse parâmetro for `true`, o parâmetro de tarefa **ManifestFromManagedAssemblyMT** também deverá ser especificado.<br /><br /> Para obter mais informações, consulte a opção **/nodependency** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**SuppressStartupBanner**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, impedirá a exibição da mensagem de direitos autorais e de número de versão quando a tarefa for iniciada.<br /><br /> Para obter mais informações, consulte a opção **/nologo** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**TrackerLogDirectory**|Parâmetro `String` opcional.<br /><br /> Especifica o diretório intermediário em que os logs de rastreamento para essa tarefa são armazenados.|  
|**TypeLibraryFile**|Parâmetro **String** opcional.<br /><br /> Especifica o nome do arquivo de biblioteca de tipos (.tlb). Ao especificar esse parâmetro, especifique também o parâmetro de tarefa **ComponentFileNameMT**.<br /><br /> Para obter mais informações, consulte a opção **/tlb** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
|**UpdateFileHashes**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, calcula o valor de hash dos arquivos no caminho especificado pelo parâmetro de tarefa **UpdateFileHashesSearchPathMT** e, em seguida, atualiza o valor do atributo **hash** do elemento de **arquivo** do manifesto usando o valor calculado.<br /><br /> Para obter mais informações, consulte a opção **/hashupdate** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737). Consulte também o parâmetro **UpdateFileHashesSearchPath** nesta tabela.|  
|**UpdateFileHashesSearchPath**|Parâmetro `String` opcional.<br /><br /> Especifica o caminho de pesquisa a ser usado quando os hashes de arquivo são atualizados. Use esse parâmetro com o parâmetro de tarefa **UpdateFileHashesMT**.<br /><br /> Para obter mais informações, consulte o parâmetro **UpdateFileHashes** nesta tabela.|  
|**VerboseOutput**|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, exibe informações de depuração detalhadas.<br /><br /> Para obter mais informações, consulte a opção **/verbose** em “Mt.exe”, no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



