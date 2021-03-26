---
description: Continua executando esse processo a partir de um estado parado. Qualquer estado de execução anterior (como uma etapa) é preservado e o processo começa a ser executado novamente.
title: 'IDebugProcess3:: Continue | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Continue
helpviewer_keywords:
- IDebugProcess3::Continue
ms.assetid: 57506242-5763-4c08-adb9-8a78ce02cebb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 11f2d5b652b950976834b8ba18f71a1dc0d1b34c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081575"
---
# <a name="idebugprocess3continue"></a>IDebugProcess3::Continue
Continua executando esse processo a partir de um estado parado. Qualquer estado de execução anterior (como uma etapa) é preservado e o processo começa a ser executado novamente.

> [!NOTE]
> Esse método deve ser usado em vez de [continuar](../../../extensibility/debugger/reference/idebugprogram2-continue.md).

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
`pThread`\
no Um objeto [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) que representa o thread a ser continuado.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna o código de erro.

## <a name="remarks"></a>Comentários
 Esse método é chamado nesse processo, independentemente de quantos processos estão sendo depurados ou qual processo gerou o evento de interrupção. A implementação deve manter o estado de execução anterior (como uma etapa) e continuar a execução como se nunca tivesse sido interrompida antes de concluir sua execução anterior. Ou seja, se um thread nesse processo estivesse realizando uma operação de etapa em etapas e foi interrompido porque algum outro processo foi interrompido e, em seguida, `Continue` foi chamado, o thread especificado deve concluir a operação de depuração original.

 **Aviso** Não enviar um evento de interrupção ou um evento imediato (síncrono) para [evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) ao lidar com essa chamada; caso contrário, o depurador pode parar de responder.

## <a name="see-also"></a>Confira também
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [Evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
