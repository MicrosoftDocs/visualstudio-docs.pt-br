---
description: 'IDebugProgram2:: continuar continua executando este programa a partir de um estado parado. Qualquer estado de execução anterior (como uma etapa) é preservado e o programa começa a ser executado novamente.'
title: 'IDebugProgram2:: Continue | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Continue
helpviewer_keywords:
- IDebugProgram2::Continue
ms.assetid: e5a6e02a-d21b-4a03-a034-e8de1f71ce2e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 60f3cb4764a53d359e971020df8261d064c62e81
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076115"
---
# <a name="idebugprogram2continue"></a>IDebugProgram2::Continue
Continua executando este programa a partir de um estado parado. Qualquer estado de execução anterior (como uma etapa) é preservado e o programa começa a ser executado novamente.

> [!NOTE]
> Esse método é preterido. Em vez disso, use o método [continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md) .

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Continue( 
   IDebugThread2* pThread
);
```

```csharp
int Continue( 
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>Parâmetros
`pThread` no Um objeto [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) que representa o thread.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é chamado nesse programa independentemente de quantos programas estão sendo depurados ou qual programa gerou o evento de interrupção. A implementação deve manter o estado de execução anterior (como uma etapa) e continuar a execução como se nunca tivesse sido interrompida antes de concluir sua execução anterior. Ou seja, se um thread neste programa estivesse realizando uma operação de depuração completa e foi interrompido porque algum outro programa foi interrompido e, em seguida, esse método foi chamado, o programa deve concluir a operação de etapa em etapas original.

> [!WARNING]
> Não enviar um evento de interrupção ou um evento imediato (síncrono) para [evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) ao lidar com essa chamada; caso contrário, o depurador pode parar de responder.

## <a name="see-also"></a>Confira também
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [Evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
