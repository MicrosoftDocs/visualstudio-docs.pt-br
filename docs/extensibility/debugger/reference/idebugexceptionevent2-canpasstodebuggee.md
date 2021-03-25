---
description: Determina se o mecanismo de depuração (DE) dá suporte à opção de passar essa exceção para o programa que está sendo depurado quando a execução é retomada.
title: 'IDebugExceptionEvent2:: CanPassToDebuggee | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::CanPassToDebuggee
helpviewer_keywords:
- IDebugExceptionEvent2::CanPassToDebuggee
ms.assetid: ae4bbe0a-fbe1-49be-a310-ea64279a434b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7fbc5cd55516f018a0a0877a114169a436b97fe1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084838"
---
# <a name="idebugexceptionevent2canpasstodebuggee"></a>IDebugExceptionEvent2::CanPassToDebuggee
Determina se o mecanismo de depuração (DE) dá suporte à opção de passar essa exceção para o programa que está sendo depurado quando a execução é retomada.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CanPassToDebuggee(
   void
);
```

```csharp
int CanPassToDebuggee();
```

## <a name="return-value"></a>Valor retornado
 Retorna `S_OK` (a exceção pode ser passada para o programa) ou `S_FALSE` (a exceção não pode ser passada).

## <a name="remarks"></a>Comentários
 O DE deve ter uma ação padrão para passar para o depurador. O IDE pode receber o evento [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) e chamar o método [continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md) sem chamar o `CanPassToDebuggee` método. Portanto, o DE deve ter um caso padrão para passar a exceção ou não.

## <a name="see-also"></a>Confira também
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [Continuar](../../../extensibility/debugger/reference/idebugprocess3-continue.md)
