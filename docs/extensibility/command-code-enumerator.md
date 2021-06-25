---
title: Enumerador de código de comando | Microsoft Docs
description: O enumerador de código de comando é usado em opções para SccGetCommandOptions e SccPopulateListto para indicar o comando para o qual as opções são especificadas.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- command code enumerator
- source control plug-ins, command code enumeration
ms.assetid: 5d2c360c-59e4-4da8-bcb4-dd07c7441e40
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b97d5083c4f262ae2d86aeef5ee2627fdc854bcb
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901377"
---
# <a name="command-code-enumerator"></a>Enumerador de código de comando
Esse enumerador é usado nas opções de [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) e [SccPopulateList](../extensibility/sccpopulatelist-function.md)para indicar o comando para o qual as opções são especificadas.

## <a name="syntax"></a>Sintaxe

```
enum SCCCOMMAND {
   SCC_COMMAND_GET,
   SCC_COMMAND_CHECKOUT,
   SCC_COMMAND_CHECKIN,
   SCC_COMMAND_UNCHECKOUT,
   SCC_COMMAND_ADD,
   SCC_COMMAND_REMOVE,
   SCC_COMMAND_DIFF,
   SCC_COMMAND_HISTORY,
   SCC_COMMAND_RENAME,
   SCC_COMMAND_PROPERTIES,
   SCC_COMMAND_OPTIONS
};
```

## <a name="members"></a>Membros
SCC_COMMAND_GET corresponde ao [SccGet](../extensibility/sccget-function.md).

SCC_COMMAND_CHECKOUT corresponde ao [SccCheckout](../extensibility/scccheckout-function.md).

SCC_COMMAND_CHECKIN corresponde ao [SccCheckin](../extensibility/scccheckin-function.md).

SCC_COMMAND_UNCHECKOUT corresponde ao [SccUncheckout](../extensibility/sccuncheckout-function.md).

SCC_COMMAND_ADD corresponde ao [SccAdd](../extensibility/sccadd-function.md).

SCC_COMMAND_REMOVE corresponde ao [SccRemove](../extensibility/sccremove-function.md).

SCC_COMMAND_DIFF corresponde ao [SccDiff](../extensibility/sccdiff-function.md).

SCC_COMMAND_HISTORY corresponde ao [SccHistory](../extensibility/scchistory-function.md).

SCC_COMMAND_RENAME corresponde ao [SccRename](../extensibility/sccrename-function.md).

SCC_COMMAND_PROPERTIES corresponde ao [SccProperties](../extensibility/sccproperties-function.md).

SCC_COMMAND_OPTIONS corresponde ao [SccSetOption](../extensibility/sccsetoption-function.md).

## <a name="see-also"></a>Confira também
- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)
- [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)
- [SccPopulateList](../extensibility/sccpopulatelist-function.md)
