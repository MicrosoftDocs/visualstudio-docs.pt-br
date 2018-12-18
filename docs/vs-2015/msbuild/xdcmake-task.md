---
title: Tarefa XDCMake | Microsoft Docs
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
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: caf3803edff01e6ffe650f18aaccef99fc50728f
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49204874"
---
# <a name="xdcmake-task"></a>Tarefa XDCMake
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Encapsula a ferramenta de Documentação XML (xdcmake.exe), que mescla arquivos de comentário (.xdc) do documento XML com um arquivo .xml.  
  
 Um arquivo .xdc será criado quando comentários de documentação forem fornecidos no código-fonte do Visual C++ e compilados por meio da opção do compilador [/doc](http://msdn.microsoft.com/library/b54f7e2c-f28f-4f46-9ed6-0db09be2cc63). Para obter mais informações, consulte [Referência XDCMake](http://msdn.microsoft.com/library/14e65747-d000-4343-854b-8393bf01cbac), [Páginas de Propriedade da Ferramenta Geradora de Documento XML](http://msdn.microsoft.com/library/645912b5-197a-4c36-ba58-64df09444ca0) e a opção de ajuda de linha de comando (**/?**) para xdcmake.exe.  
  
## <a name="remarks"></a>Comentários  
 Por padrão, a ferramenta xdcmake.exe dá suporte a algumas opções de linha de comando. Opções adicionais terão suporte quando a opção de linha de comando **/old** for especificada.  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa **XDCMake**.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|**AdditionalDocumentFile**|Parâmetro **String[]** opcional.<br /><br /> Especifica um ou mais arquivos .xdc adicionais para mesclagem.<br /><br /> Para obter mais informações, consulte a descrição **Arquivos Adicionais de Documento** nas [Páginas de Propriedade da Ferramenta Geradora de Documento XML](http://msdn.microsoft.com/library/645912b5-197a-4c36-ba58-64df09444ca0). Consulte também as opções de linha de comando **/old** e **/Fs** para o xdcmake.exe.|  
|**AdditionalOptions**|Parâmetro **String** opcional.<br /><br /> Uma lista de opções, conforme especificado na linha de comando. Por exemplo, "*/option1 /option2 /option#*". Use esse parâmetro para especificar opções não representadas por nenhum outro parâmetro da tarefa **XDCMake**.<br /><br /> Para obter mais informações, consulte [Referência XDCMake](http://msdn.microsoft.com/library/14e65747-d000-4343-854b-8393bf01cbac), [Páginas de Propriedade da Ferramenta Geradora de Documento XML](http://msdn.microsoft.com/library/645912b5-197a-4c36-ba58-64df09444ca0) e a ajuda da linha de comando (**/?**) para o xdcmake.exe.|  
|**DocumentLibraryDependencies**|Parâmetro **Boolean** opcional.<br /><br /> Se `true` e o projeto atual tiverem uma dependência em um projeto de biblioteca estática (.lib) na solução, os arquivos .xdc desse projeto de biblioteca serão incluídos no arquivo .xml de saída do projeto atual.<br /><br /> Para obter mais informações, consulte a descrição **Dependências de Biblioteca de Documentos** nas [Páginas de Propriedade da Ferramenta Geradora de Documento XML](http://msdn.microsoft.com/library/645912b5-197a-4c36-ba58-64df09444ca0).|  
|**OutputFile**|Parâmetro **String** opcional.<br /><br /> Substitui o nome de arquivo de saída padrão. O nome padrão é derivado do nome do primeiro arquivo .xdc processado.<br /><br /> Para obter mais informações, consulte a opção **/out:**`filename` em [Referência XDCMake](http://msdn.microsoft.com/library/14e65747-d000-4343-854b-8393bf01cbac). Consulte também as opções de linha de comando **/old** e **/Fo** para o xdcmake.exe.|  
|**ProjectName**|Parâmetro **String** opcional.<br /><br /> O nome do projeto atual.|  
|**SlashOld**|Parâmetro **Boolean** opcional.<br /><br /> Se `true`, habilitará as opções adicionais do xdcmake.exe.<br /><br /> Para obter mais informações, consulte a opção de linha de comando **/old** para o xdcmake.exe.|  
|**Sources**|Parâmetro `ITaskItem[]` obrigatório.<br /><br /> Define uma matriz de itens de arquivo de origem do MSBuild que pode ser consumida e emitida por tarefas.|  
|**SuppressStartupBanner**|Parâmetro **Boolean** opcional.<br /><br /> Se `true`, impedirá a exibição da mensagem de direitos autorais e de número de versão quando a tarefa for iniciada.<br /><br /> Para obter mais informações, consulte a opção **/nologo** em [Referência XDCMake](http://msdn.microsoft.com/library/14e65747-d000-4343-854b-8393bf01cbac).|  
|**TrackerLogDirectory**|Parâmetro **String** opcional.<br /><br /> Especifica o diretório do log de rastreamento.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



