---
title: Sinalizadores de recurso | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- source control plug-ins, capability flags
ms.assetid: a3f6071c-eac8-4bcd-8ffd-8d0a2d24a252
caps.latest.revision: 25
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6fd526abb5580b6eb3899df9ee76baacd91e56d7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51785281"
---
# <a name="capability-flags"></a>Sinalizadores de capacidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O SCC_CAP_*xxx* sinalizadores são sinalizadores de bit usados para indicar os recursos de um plug-in de controle de origem. O SCC_EXCAP_*xxx* sinalizadores são incrementais sinalizadores que indicam recursos estendidos e resolvem para valores inteiros.  
  
|Código de recurso|Valor|Descrição|  
|---------------------|-----------|-----------------|  
|`SCC_CAP_REMOVE`|0x00000001L|Dá suporte a [SccRemove](../extensibility/sccremove-function.md) e comando.|  
|`SCC_CAP_RENAME`|0x00000002L|Dá suporte a [SccRename](../extensibility/sccrename-function.md) e comando.|  
|`SCC_CAP_DIFF`|0x00000004L|Dá suporte a [SccDiff](../extensibility/sccdiff-function.md) e comando.|  
|`SCC_CAP_HISTORY`|0x00000008L|Dá suporte a [SccHistory](../extensibility/scchistory-function.md) e comando.|  
|`SCC_CAP_PROPERTIES`|0x00000010L|Dá suporte a [SccProperties](../extensibility/sccproperties-function.md) e comando.|  
|`SCC_CAP_RUNSCC`|0x00000020L|Dá suporte a [SccRunScc](../extensibility/sccrunscc-function.md) e comando.|  
|`SCC_CAP_GETCOMMANDOPTIONS`|0x00000040L|Dá suporte a [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) e comando.|  
|`SCC_CAP_QUERYINFO`|0x00000080L|Dá suporte a [SccQueryInfo](../extensibility/sccqueryinfo-function.md) e comando.|  
|`SCC_CAP_GETEVENTS`|0x00000100L|Dá suporte a [SccGetEvents](../extensibility/sccgetevents-function.md) e comando.|  
|`SCC_CAP_GETPROJPATH`|0x00000200L|Dá suporte a [SccGetProjPath](../extensibility/sccgetprojpath-function.md) e comando.|  
|`SCC_CAP_ADDFROMSCC`|0x00000400L|Dá suporte a [SccAddFromScc](../extensibility/sccaddfromscc-function.md) e comando.|  
|`SCC_CAP_COMMENTCHECKOUT`|0x00000800L|Dá suporte a um comentário no check-out.|  
|`SCC_CAP_COMMENTCHECKIN`|0x00001000L|Dá suporte a um comentário no check-in.|  
|`SCC_CAP_COMMENTADD`|0x00002000L|Dá suporte a um comentário em Adicionar.|  
|`SCC_CAP_COMMENTREMOVE`|0x00004000L|Dá suporte a um comentário em Remover.|  
|`SCC_CAP_TEXTOUT`|0x00008000L|Grava o texto em uma função de saída fornecido pelo IDE.|  
|`SCC_CAP_ADD_STORELATEST`|0x00200000L|Oferece suporte ao armazenamento de arquivos sem deltas.|  
|`SCC_CAP_HISTORY_MULTFILE`|0x00400000L|Dá suporte a vários histórico de arquivos.|  
|`SCC_CAP_IGNORECASE`|0x00800000L|Dá suporte à comparação de arquivo diferencia maiusculas de minúsculas.|  
|`SCC_CAP_IGNORESPACE`|0x01000000L|Dá suporte a arquivo de comparação que ignora o espaço em branco.|  
|`SCC_CAP_POPULATELIST`|0x02000000L|Oferece suporte à localização de arquivos extras.|  
|`SCC_CAP_COMMENTPROJECT`|0x04000000L|Dá suporte a comentários em criar o projeto.|  
|`SCC_CAP_DIFFALWAYS`|0x10000000L|Dá suporte à comparação em todos os estados se estiver sob controle.|  
|`SCC_CAP_GET_NOUI`|0x20000000L|Plug-in não suporta uma interface do usuário para Get, mas IDE ainda pode chamar [SccGet](../extensibility/sccget-function.md).|  
|`SCC_CAP_REENTRANT`|0x40000000L|Plug-in é reentrante e thread-safe. Na versão 1.0, nenhum plug-in deveriam para estar reentrante e thread-safe. Se um plug-in de 1.1 define esse bit, o host tem permissão para abrir vários projetos em paralelo.|  
  
## <a name="capability-bits-added-in-version-12"></a>Bits de funcionalidade adicionadas na versão 1.2  
  
|Código de recurso|Valor|Descrição|  
|---------------------|-----------|-----------------|  
|`SCC_CAP_CREATESUBPROJECT`|0x00010000L|Dá suporte a [SccCreateSubProject](../extensibility/scccreatesubproject-function.md).|  
|`SCC_CAP_GETPARENTPROJECT`|0x00020000L|Dá suporte a [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md).|  
|`SCC_CAP_BATCH`|0x00040000L|Dá suporte a [SccBeginBatch](../extensibility/sccbeginbatch-function.md) e [SccEndBatch](../extensibility/sccendbatch-function.md).|  
|`SCC_CAP_DIRECTORYSTATUS`|0x00080000L|Dá suporte a [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md).|  
|`SCC_CAP_DIRECTORYDIFF`|0x00100000L|Dá suporte a [SccDirDiff](../extensibility/sccdirdiff-function.md).|  
|`SCC_CAP_MULTICHECKOUT`|0x08000000L|Dá suporte a vários check-outs em um arquivo e o [SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md).|  
|`SCC_CAP_SCCFILE`|0x80000000L|Oferece suporte a MSSCCPRJ. Arquivos SCC (sujeito a substituição do administrador do usuário) e o [SccWillCreateSccFile](../extensibility/sccwillcreatesccfile-function.md).|  
  
## <a name="capability-bits-added-in-version-13"></a>Bits de funcionalidade adicionadas na versão 1.3  
 Esses sinalizadores são passados a um de cada vez para o [SccGetExtendedCapabilities](../extensibility/sccgetextendedcapabilities-function.md) função para determinar se o recurso tem suporte.  
  
|Código de capacidade estendida|Valor|Descrição|  
|------------------------------|-----------|-----------------|  
|`SCC_EXCAP_CHECKOUT_LOCALVER`|1|Dá suporte a `SCC_CHECKOUT_LOCALVER` opção para check-outs.|  
|`SCC_EXCAP_BACKGROUND_GET`|2|Dá suporte a [SccBackgroundGet](../extensibility/sccbackgroundget-function.md).|  
|`SCC_EXCAP_ENUM_CHANGED_FILES`|3|Dá suporte a [SccEnumChangedFiles](../extensibility/sccenumchangedfiles-function.md).|  
|`SCC_EXCAP_POPULATELIST_DIR`|4|Oferece suporte à localização diretórios extras.|  
|`SCC_EXCAP_QUERYCHANGES`|5|Dá suporte ao enumerar as alterações de arquivo.|  
|`SCC_EXCAP_ADD_FILES_FROM_SCC`|6|Dá suporte a [SccAddFilesFromSCC](../extensibility/sccaddfilesfromscc-function.md).|  
|`SCC_EXCAP_GET_USER_OPTIONS`|7|Dá suporte a [SccGetUserOption](../extensibility/sccgetuseroption-function.md).|  
|`SCC_EXCAP_THREADSAFE_QUERY_INFO`|8|Dá suporte a chamar SccQueryInfo em vários threads.|  
|`SCC_EXCAP_REMOVE_DIR`|9|Suporta a função de SccRemoveDir.|  
|`SCC_EXCAP_DELETE_CHECKEDOUT`|10|Pode excluir arquivos com check-out.|  
|`SCC_EXCAP_RENAME_CHECKEDOUT`|11|Pode renomear os arquivos com check-out.|  
  
## <a name="see-also"></a>Consulte também  
 [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)

