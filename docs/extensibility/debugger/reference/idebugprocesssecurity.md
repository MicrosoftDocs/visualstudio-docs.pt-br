---
description: O IDebugProcessSecurity é implementado por um fornecedor de porta para avisar o usuário que anexar ao processo não é seguro.
title: IDebugProcessSecurity | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity interface
ms.assetid: 8a52ddca-bd99-49c0-9778-469dce7abd44
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f7466d88be9460a2b4680fc7d14a741df9238ea0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076258"
---
# <a name="idebugprocesssecurity"></a>IDebugProcessSecurity
`IDebugProcessSecurity` é implementado por um fornecedor de porta para avisar o usuário que anexar ao processo não é seguro.

## <a name="syntax"></a>Sintaxe

```
IDebugProcessSecurity : IUnknown
```

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugProcessSecurity` .

|Método|Descrição|
|------------|-----------------|
|[GetUserName](../../../extensibility/debugger/reference/idebugprocesssecurity-getusername.md)|Obtém o nome de usuário do fornecedor da porta.|
|[QueryCanSafelyAttach](../../../extensibility/debugger/reference/idebugprocesssecurity-querycansafelyattach.md)|Avisa um usuário que anexar ao processo de depuração não é seguro.|

## <a name="remarks"></a>Comentários
 Implemente essa interface para mostrar um aviso e permitir que o usuário cancele se o processo ao qual você está anexando puder ser considerado não seguro.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Portas](../../../extensibility/debugger/ports.md)
- [Fornecedores de porta](../../../extensibility/debugger/port-suppliers.md)
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
