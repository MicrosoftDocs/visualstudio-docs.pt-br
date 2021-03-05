---
description: Habilita um mecanismo de depuração que usa DCOM para solicitar que a interface do usuário do Visual Studio Verifique se o firewall não bloqueará a depuração remota.
title: IDebugFirewallConfigurationCallback2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFirewallConfigurationCallback2 interface
ms.assetid: 0827361c-b97c-4851-9898-ab6d88c81811
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bf8659a1bc4af55a9809a3c85548b971a7193b26
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166522"
---
# <a name="idebugfirewallconfigurationcallback2"></a>IDebugFirewallConfigurationCallback2
Habilita um mecanismo de depuração que usa DCOM para solicitar [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] que a interface do usuário Verifique se o firewall não bloqueará a depuração remota.

## <a name="syntax"></a>Sintaxe

```
IDebugFirewallConfigurationCallback2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Implementado pelo objeto Port do Gerenciador de depuração de sessão.

## <a name="methods"></a>Métodos
 A tabela a seguir mostra os métodos de `IDebugFirewallConfigurationCallback2` .

|Método|Descrição|
|------------|-----------------|
|[EnsureDCOMUnblocked](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2-ensuredcomunblocked.md)|Solicita que o firewall não bloqueie a depuração remota.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: Msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
