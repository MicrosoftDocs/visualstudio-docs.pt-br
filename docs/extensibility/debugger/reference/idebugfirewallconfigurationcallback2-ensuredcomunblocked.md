---
title: IDebugFirewallConfigurationCallback2::EnsureDCOMUnblocked
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- EnsureDCOMUnblocked
- IDebugFirewallConfigurationCallback2::EnsureDCOMUnblocked
ms.assetid: acf54d27-32a6-47e7-aba6-3cc0004edc7f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 77ed081f47d08bc297050ed0cf92a88c8b167674
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89741373"
---
# <a name="idebugfirewallconfigurationcallback2ensuredcomunblocked"></a>IDebugFirewallConfigurationCallback2::EnsureDCOMUnblocked

Solicita que o firewall não bloqueie a depuração remota.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnsureDCOMUnblocked(
    Void
);
```

```csharp
public int EnsureDCOMUnblocked();
```

## <a name="return-value"></a>Valor retornado

 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Veja também

- [IDebugFirewallConfigurationCallback2](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2.md)
