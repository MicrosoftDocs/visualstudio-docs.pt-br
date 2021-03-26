---
title: Quais &apos; s novidades na API de plug-in de controle do código-fonte 1,3
description: Saiba mais sobre as novidades na API de plug-in de controle do código-fonte versão 1,3, que introduz as novas funções para fornecer controle mais avançado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, what's new in API v1.3
- what's new [Visual Studio SDK], source control plug-ins
ms.assetid: 7dfb2227-6e1d-4028-bce9-f8967456a993
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7ab9079248931758efbcfcd792ce3c79ccffb270
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074256"
---
# <a name="what39s-new-in-the-source-control-plug-in-api-version-13"></a>O que&#39;s New na API de plug-in de controle do código-fonte versão 1,3
A API de plug-in de controle do código-fonte versão 1,3 apresenta as novas funções a seguir para fornecer controle mais avançado.

## <a name="changes"></a>Alterações
 As seguintes funções são novas na API de plug-in de controle do código-fonte versão 1,3:

|Função|Visão geral|
|--------------|--------------|
|[SccGetExtendedCapabilities](../../extensibility/sccgetextendedcapabilities-function.md)|Permite que bits de funcionalidade adicionais sejam relatados|
|[SccEnumChangedFiles](../../extensibility/sccenumchangedfiles-function.md)|Permite o exame de arquivos que têm versões mais recentes no banco de dados de controle de versão do que no disco local|
|[SccQueryChanges](../../extensibility/sccquerychanges-function.md)|Permite o exame do estado de alterações de nome (renomeações, adições e exclusões) para arquivos especificados|
|[SccPopulateDirList](../../extensibility/sccpopulatedirlist-function.md)|Permite o exame de diretórios e arquivos no banco de dados do controle de versão|
|[SccAddFilesFromSCC](../../extensibility/sccaddfilesfromscc-function.md)|Adiciona uma lista especificada de arquivos do banco de dados de controle de versão ao projeto atual|
|[SccBackgroundGet](../../extensibility/sccbackgroundget-function.md)|Executa um "Get" silencioso dos arquivos especificados (nenhuma interface do usuário é mostrada)|
|[SccGetUserOption](../../extensibility/sccgetuseroption-function.md)|Permite o acesso a opções específicas do usuário|

## <a name="see-also"></a>Confira também
- [Introdução](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)
- [Novidades na API do plug-in de controle do código-fonte versão 1.2](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
