---
description: Essa interface representa um tipo de variável.
title: IDebugDynamicField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDynamicField
helpviewer_keywords:
- IDebugDynamicField interface
ms.assetid: caffbd95-7596-4714-84b1-b964e89a78bb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dcf148294a7c18c2b717bb4de63dac7e656e25d6
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167224"
---
# <a name="idebugdynamicfield"></a>IDebugDynamicField
Essa interface representa um tipo de variável.

## <a name="syntax"></a>Sintaxe

```
IDebugDynamicField : IDebugField
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Essa interface é implementada por provedores de símbolos como uma classe base para qualquer tipo que possa ser determinado em tempo de execução. Isso é apenas para código gerenciado.

## <a name="notes-for-callers"></a>Observações para chamadores
 Essa interface representa uma classe base da qual interfaces mais especializadas podem ser derivadas.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Esta interface não fornece nenhum método diferente daqueles herdados de `IDebugField` .

## <a name="requirements"></a>Requisitos
 Cabeçalho: sh. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces de provedor de símbolos](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
