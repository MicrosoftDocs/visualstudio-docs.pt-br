---
title: Enumerador de código de status do diretório | Microsoft Docs
description: O enumerador SccDirStatus contém valores constantes nomeados que especificam o estado de um diretório no sistema de controle do código-fonte e é usado por SccDirQueryInfo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- directory status code enumerator
- source control plug-ins, directory status enumeration
ms.assetid: 616026b5-f529-40ef-90c1-1836e116d797
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a504c6c080c34b4506cf4078b64465a3bd6c7d97
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904224"
---
# <a name="directory-status-code-enumerator"></a>Enumerador de código de status do diretório
O `SccDirStatus` enumerador contém valores constantes nomeados que especificam o estado de um diretório no sistema de controle do código-fonte. Essa enumeração é usada pelo [SccDirQueryInfo.](../extensibility/sccdirqueryinfo-function.md) Isso foi introduzido na versão 1.2 da API de Plug-in de Controle do Código-Fonte.

## <a name="syntax"></a>Sintaxe

```
enum SccDirStatus {
   SCC_DIRSTATUS_INVALID       = -1L,
   SCC_DIRSTATUS_NOTCONTROLLED = 0x0000L,
   SCC_DIRSTATUS_CONTROLLED    = 0x0001L,
   SCC_DIRSTATUS_EMPTYPROJ     = 0x0002L
};
```

## <a name="members"></a>Membros
 SCC_DIRSTATUS_INVALID status não pôde ser obtido; não dependem dele.

 SCC_DIRSTATUS_NOTCONTROLLED Directory não está sob controle do código-fonte.

 SCC_DIRSTATUS_CONTROLLED Directory está sob controle do código-fonte.

 SCC_DIRSTATUS_EMPTYPROJ Projeto correspondente a esse diretório está vazio.

## <a name="see-also"></a>Confira também
- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)
- [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)
