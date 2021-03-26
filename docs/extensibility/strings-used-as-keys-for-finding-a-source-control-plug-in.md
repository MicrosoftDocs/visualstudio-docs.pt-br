---
title: Cadeias de caracteres usadas como chaves para localizar um plug-in de controle do código-fonte
description: Saiba mais sobre as cadeias de caracteres que são as chaves para acessar o registro para encontrar informações sobre o plug-in de controle do código-fonte.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, strings used for finding
ms.assetid: c1e31f76-42a1-4c3d-afb2-664044ef12fd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b61c13973ac6668814fbc3ba076b373d6e0b1e44
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056292"
---
# <a name="strings-used-as-keys-for-finding-a-source-control-plug-in"></a>Cadeias de caracteres usadas como chaves para localizar um plug-in de controle do código-fonte
As cadeias de caracteres a seguir são as chaves para acessar o registro para encontrar informações sobre o plug-in de controle do código-fonte.

 `STR_SCC_PROVIDER_REG_LOCATION`, `STR_PROVIDERREGKEY` , `STR_SCCPROVIDERPATH` e `STR_SCCPROVIDERNAME` são chaves do registro ou valores usados para registrar uma dll como um plug-in de controle do código-fonte para o Visual Studio.

 `SCC_PROJECTNAME_KEY`, `SCC_PROJECTAUX_KEY` , `SCC_KEY, SCC_FILE_SIGNATURE` e `SCC_STATUS_FILE` são usados para descrever o formato do MSSCCPRJ. Arquivo SCC.

## <a name="string-keys-and-values"></a>Valores e chaves de cadeia de caracteres

|Chave|Valor|
|---------|-----------|
|`STR_SCC_PROVIDER_REG_LOCATION`|Software\SourceCodeControlProvider|
|`STR_PROVIDERREGKEY`|ProviderRegKey|
|`STR_SCCPROVIDERPATH`|SCCServerPath|
|`STR_SCCPROVIDERNAME`|SCCServerName|
|`STR_SCC_INI_SECTION`|Controle do Código-Fonte|
|`STR_SCC_INI_KEY`|SourceCodeControlProvider|
|`SCC_PROJECTNAME_KEY`|SCC_Project_Name|
|`SCC_PROJECTAUX_KEY`|SCC_Aux_Path|
|`SCC_STATUS_FILE`|MSSCCPRJ. SCC|
|`SCC_KEY`|SCC|
|`SCC_FILE_SIGNATURE`|Um arquivo de controle do código-fonte|
|`SCC_NSE`|Extensão do namespace|
|`SCC_NSE_PREFIX`|Prefixo protocolo|
|`SCC_NSE_DisableOpenSCC`|DisableOpenFromSourceControl|
|`STR_SCCHELPCOLLECTION`|HelpCollection|
|`STR_UI_LANGUAGE`|UILanguage|
|`STR_SRCSAFE_ROOT_KEY`|Software\Microsoft\SourceSafe|

## <a name="see-also"></a>Confira também
- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)
- [Como instalar um plug-in de controle do código-fonte](../extensibility/internals/how-to-install-a-source-control-plug-in.md)
- [Arquivo MSSCCPRJ.SCC](../extensibility/mssccprj-scc-file.md)
