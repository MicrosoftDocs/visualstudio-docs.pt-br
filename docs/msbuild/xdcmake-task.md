---
title: Tarefa XDCMake | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- vc.task.xdcmake
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- XDCMake task (MSBuild (Visual C++))
- MSBuild (Visual C++), XDCMake task
ms.assetid: a7de9c64-903a-4a02-85f3-f37672270f25
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 460d5f68242f232048fec294156f90f49331a21d
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39231172"
---
# <a name="xdcmake-task"></a>tarefa XDCMake
Encapsula a ferramenta de Documentação XML (*xdcmake.exe*), que mescla arquivos de comentário (*.xdc*) do documento XML com um arquivo *.xml*.  
  
 Um arquivo *.xdc* será criado quando comentários de documentação forem fornecidos no código-fonte do Visual C++ e compilados por meio da opção do compilador [/doc](/cpp/build/reference/doc-process-documentation-comments-c-cpp). Para saber mais, consulte [Referência XDCMake](/cpp/ide/xdcmake-reference), [Páginas de Propriedade da Ferramenta Geradora de Documento XML](/cpp/ide/xml-document-generator-tool-property-pages) e a opção de ajuda de linha de comando (**/?**) para *xdcmake.exe*.  
  
## <a name="remarks"></a>Comentários  
 Por padrão, a ferramenta *xdcmake.exe* dá suporte a algumas opções de linha de comando. Opções adicionais terão suporte quando a opção de linha de comando **/old** for especificada.  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa **XDCMake**.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|**AdditionalDocumentFile**|Parâmetro **String[]** opcional.<br /><br /> Especifica um ou mais arquivos *.xdc* adicionais para mesclagem.<br /><br /> Para saber mais, consulte a descrição **Arquivos Adicionais de Documento** nas [Páginas de propriedade da Ferramenta Geradora de Documento XML](/cpp/ide/xml-document-generator-tool-property-pages). Consulte também as opções de linha de comando **/old** e **/Fs** para o *xdcmake.exe*.|  
|**AdditionalOptions**|Parâmetro **String** opcional.<br /><br /> Uma lista de opções, conforme especificado na linha de comando. Por exemplo, /\<option1> /\<option2> /\<option#>. Use esse parâmetro para especificar opções não representadas por nenhum outro parâmetro da tarefa **XDCMake**.<br /><br /> Para saber mais, consulte [Referência XDCMake](/cpp/ide/xdcmake-reference), [Páginas de Propriedade da Ferramenta Geradora de Documento XML](/cpp/ide/xml-document-generator-tool-property-pages) e a ajuda da linha de comando (**/?**) para o *xdcmake.exe*.|  
|**DocumentLibraryDependencies**|Parâmetro **Boolean** opcional.<br /><br /> Se `true` e o projeto atual tiverem uma dependência em um projeto de biblioteca estática (*.lib*) na solução, os arquivos *.xdc* desse projeto de biblioteca serão incluídos no arquivo *.xml* de saída do projeto atual.<br /><br /> Para saber mais, confira a descrição **Dependências de Biblioteca de Documentos** nas [Páginas de propriedade da Ferramenta Geradora de Documento XML](/cpp/ide/xml-document-generator-tool-property-pages).|  
|**OutputFile**|Parâmetro **String** opcional.<br /><br /> Substitui o nome de arquivo de saída padrão. O nome padrão é derivado do nome do primeiro arquivo *.xdc* processado.<br /><br /> Para saber mais, confira a opção **/out:\<nomedoarquivo>** em [Referência XDCMake](/cpp/ide/xdcmake-reference). Consulte também as opções de linha de comando **/old** e **/Fo** para o *xdcmake.exe*.|  
|**ProjectName**|Parâmetro **String** opcional.<br /><br /> O nome do projeto atual.|  
|**SlashOld**|Parâmetro **Boolean** opcional.<br /><br /> Se `true`, habilitará as opções adicionais do *xdcmake.exe*.<br /><br /> Para saber mais, consulte a opção de linha de comando **/old** para o *xdcmake.exe*.|  
|**Sources**|Parâmetro `ITaskItem[]` obrigatório.<br /><br /> Define uma matriz de itens de arquivo de origem do MSBuild que pode ser consumida e emitida por tarefas.|  
|**SuppressStartupBanner**|Parâmetro **Boolean** opcional.<br /><br /> Se `true`, impedirá a exibição da mensagem de direitos autorais e de número de versão quando a tarefa for iniciada.<br /><br /> Para saber mais, consulte a opção **/nologo** em [Referência XDCMake](/cpp/ide/xdcmake-reference).|  
|**TrackerLogDirectory**|Parâmetro **String** opcional.<br /><br /> Especifica o diretório do log de rastreamento.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)