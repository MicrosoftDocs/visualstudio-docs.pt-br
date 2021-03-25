---
title: Sinalizadores de capacidade | Microsoft Docs
description: Saiba mais sobre os sinalizadores de SCC_CAP_xxx que indicam os recursos de um plug-in de controle do código-fonte e os sinalizadores de SCC_EXCAP_xxx que indicam recursos estendidos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, capability flags
ms.assetid: a3f6071c-eac8-4bcd-8ffd-8d0a2d24a252
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 12acefb99de787d55bc0f932757dde5ea928c6cb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094920"
---
# <a name="capability-flags"></a>Sinalizadores de capacidade
Os sinalizadores de SCC_CAP_ *xxx* são sinalizadores de bits usados para indicar os recursos de um plug-in de controle do código-fonte. Os sinalizadores de SCC_EXCAP_ *xxx* são sinalizadores incrementais que indicam recursos estendidos e resolvem para valores inteiros.

|Código de funcionalidade|Valor|Descrição|
|---------------------|-----------|-----------------|
|`SCC_CAP_REMOVE`|0x00000001L|Dá suporte ao [SccRemove](../extensibility/sccremove-function.md) e ao comando.|
|`SCC_CAP_RENAME`|0x00000002L|Dá suporte ao [SccRename](../extensibility/sccrename-function.md) e ao comando.|
|`SCC_CAP_DIFF`|0x00000004L|Dá suporte ao [SccDiff](../extensibility/sccdiff-function.md) e ao comando.|
|`SCC_CAP_HISTORY`|0x00000008L|Dá suporte ao [SccHistory](../extensibility/scchistory-function.md) e ao comando.|
|`SCC_CAP_PROPERTIES`|0x00000010L|Dá suporte ao [SccProperties](../extensibility/sccproperties-function.md) e ao comando.|
|`SCC_CAP_RUNSCC`|0x00000020L|Dá suporte ao [SccRunScc](../extensibility/sccrunscc-function.md) e ao comando.|
|`SCC_CAP_GETCOMMANDOPTIONS`|0x00000040L|Dá suporte ao [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) e ao comando.|
|`SCC_CAP_QUERYINFO`|0x00000080L|Dá suporte ao [SccQueryInfo](../extensibility/sccqueryinfo-function.md) e ao comando.|
|`SCC_CAP_GETEVENTS`|0x00000100L|Dá suporte ao [SccGetEvents](../extensibility/sccgetevents-function.md) e ao comando.|
|`SCC_CAP_GETPROJPATH`|0x00000200L|Dá suporte ao [SccGetProjPath](../extensibility/sccgetprojpath-function.md) e ao comando.|
|`SCC_CAP_ADDFROMSCC`|0x00000400L|Dá suporte ao [SccAddFromScc](../extensibility/sccaddfromscc-function.md) e ao comando.|
|`SCC_CAP_COMMENTCHECKOUT`|0x00000800L|Dá suporte a um comentário sobre o check-out.|
|`SCC_CAP_COMMENTCHECKIN`|0x00001000L|Dá suporte a um comentário no check-in.|
|`SCC_CAP_COMMENTADD`|0x00002000L|Dá suporte a um comentário sobre adicionar.|
|`SCC_CAP_COMMENTREMOVE`|0x00004000L|Dá suporte a um comentário sobre remove.|
|`SCC_CAP_TEXTOUT`|0x00008000L|Grava o texto em uma função de saída fornecida pelo IDE.|
|`SCC_CAP_ADD_STORELATEST`|0x00200000L|Oferece suporte ao armazenamento de arquivos sem deltas.|
|`SCC_CAP_HISTORY_MULTFILE`|0x00400000L|Dá suporte a vários históricos de arquivo.|
|`SCC_CAP_IGNORECASE`|0x00800000L|Dá suporte à comparação de arquivo que não diferencia maiúsculas de minúsculas.|
|`SCC_CAP_IGNORESPACE`|0x01000000L|Dá suporte à comparação de arquivos que ignora o espaço em branco.|
|`SCC_CAP_POPULATELIST`|0x02000000L|Oferece suporte à localização de arquivos extras.|
|`SCC_CAP_COMMENTPROJECT`|0x04000000L|Dá suporte a comentários em criar projeto.|
|`SCC_CAP_DIFFALWAYS`|0x10000000L|Dá suporte à comparação em todos os Estados, se estiver sob controle.|
|`SCC_CAP_GET_NOUI`|0x20000000L|O plug-in não dá suporte a uma interface do usuário para Get, mas o IDE ainda pode chamar [SccGet](../extensibility/sccget-function.md).|
|`SCC_CAP_REENTRANT`|0x40000000L|O plug-in é reentrante e thread-safe. Na versão 1,0, nenhum plug-in foi considerado reentrante e seguro para thread. Se um plug-in 1,1 definir esse bit, o host poderá abrir vários projetos em paralelo.|

## <a name="capability-bits-added-in-version-12"></a>Bits de funcionalidade adicionados na versão 1,2

|Código de funcionalidade|Valor|Descrição|
|---------------------|-----------|-----------------|
|`SCC_CAP_CREATESUBPROJECT`|0x00010000L|Dá suporte ao [SccCreateSubProject](../extensibility/scccreatesubproject-function.md).|
|`SCC_CAP_GETPARENTPROJECT`|0x00020000L|Dá suporte ao [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md).|
|`SCC_CAP_BATCH`|0x00040000L|Dá suporte a [SccBeginBatch](../extensibility/sccbeginbatch-function.md) e [SccEndBatch](../extensibility/sccendbatch-function.md).|
|`SCC_CAP_DIRECTORYSTATUS`|0x00080000L|Dá suporte ao [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md).|
|`SCC_CAP_DIRECTORYDIFF`|0x00100000L|Dá suporte ao [SccDirDiff](../extensibility/sccdirdiff-function.md).|
|`SCC_CAP_MULTICHECKOUT`|0x08000000L|Dá suporte a vários check-outs em um arquivo e [SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md).|
|`SCC_CAP_SCCFILE`|0x80000000L|Dá suporte ao arquivo *MSSCCPRJ. SCC* (sujeito à substituição de usuário/administrador) e [SccWillCreateSccFile](../extensibility/sccwillcreatesccfile-function.md).|

## <a name="capability-bits-added-in-version-13"></a>Bits de funcionalidade adicionados na versão 1,3
 Esses sinalizadores são passados um de cada vez para a função [SccGetExtendedCapabilities](../extensibility/sccgetextendedcapabilities-function.md) para determinar se há suporte para a funcionalidade.

|Código de funcionalidade estendida|Valor|Descrição|
|------------------------------|-----------|-----------------|
|`SCC_EXCAP_CHECKOUT_LOCALVER`|1|Dá suporte à `SCC_CHECKOUT_LOCALVER` opção para check-outs.|
|`SCC_EXCAP_BACKGROUND_GET`|2|Dá suporte ao [SccBackgroundGet](../extensibility/sccbackgroundget-function.md).|
|`SCC_EXCAP_ENUM_CHANGED_FILES`|3|Dá suporte ao [SccEnumChangedFiles](../extensibility/sccenumchangedfiles-function.md).|
|`SCC_EXCAP_POPULATELIST_DIR`|4|Oferece suporte à localização de diretórios extras.|
|`SCC_EXCAP_QUERYCHANGES`|5|Dá suporte à enumeração de alterações de arquivo.|
|`SCC_EXCAP_ADD_FILES_FROM_SCC`|6|Dá suporte ao [SccAddFilesFromSCC](../extensibility/sccaddfilesfromscc-function.md).|
|`SCC_EXCAP_GET_USER_OPTIONS`|7|Dá suporte ao [SccGetUserOption](../extensibility/sccgetuseroption-function.md).|
|`SCC_EXCAP_THREADSAFE_QUERY_INFO`|8|Dá suporte à chamada de SccQueryInfo em vários threads.|
|`SCC_EXCAP_REMOVE_DIR`|9|Dá suporte à função SccRemoveDir.|
|`SCC_EXCAP_DELETE_CHECKEDOUT`|10|Pode excluir arquivos com check-out.|
|`SCC_EXCAP_RENAME_CHECKEDOUT`|11|Pode renomear arquivos com check-out.|

## <a name="see-also"></a>Confira também
- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)
