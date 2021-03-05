---
description: Especifica se a exceção deve ser passada para o programa que está sendo depurado quando a execução é retomada ou se a exceção deve ser descartada.
title: IDebugExceptionEvent2::P assToDebuggee | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::PassToDebuggee
helpviewer_keywords:
- IDebugExceptionEvent2::PassToDebuggee
ms.assetid: a20d0f0b-2ca0-4437-bd22-9213c81d2738
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7fca977aba3657592088879cdad884f6e6325ffd
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102152852"
---
# <a name="idebugexceptionevent2passtodebuggee"></a>IDebugExceptionEvent2::PassToDebuggee
Especifica se a exceção deve ser passada para o programa que está sendo depurado quando a execução é retomada ou se a exceção deve ser descartada.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT PassToDebuggee(
   BOOL fPass
);
```

```csharp
int PassToDebuggee(
   int fPass
);
```

## <a name="parameters"></a>Parâmetros
`fPass`\
no Zero ( `TRUE` ) se a exceção deve ser passada para o programa que está sendo depurado quando a execução é retomada, ou zero ( `FALSE` ) se a exceção deve ser descartada.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Chamar esse método, na verdade, não faz com que qualquer código seja executado no programa que está sendo depurado. A chamada é simplesmente definir o estado para a próxima execução de código. Por exemplo, as chamadas para o método [CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) podem retornar `S_OK` com o [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md).`dwState` conjunto de campos como `EXCEPTION_STOP_SECOND_CHANCE` .

 O IDE pode receber o evento [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) e chamar o método [continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md) . O mecanismo de depuração (DE) deve ter um comportamento padrão para manipular o caso se o `PassToDebuggee` método não for chamado.

## <a name="see-also"></a>Confira também
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)
- [Continuar](../../../extensibility/debugger/reference/idebugprogram2-continue.md)
