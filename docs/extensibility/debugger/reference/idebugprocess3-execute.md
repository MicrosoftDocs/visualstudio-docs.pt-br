---
title: IDebugProcess3::Execute | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Execute
helpviewer_keywords:
- IDebugProcess3::Execute
ms.assetid: d831cd81-d7bf-4172-8517-aa699867791f
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5f9afe4bb5087c7589415a6ae7fc143f5fd01b21
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63413213"
---
# <a name="idebugprocess3execute"></a>IDebugProcess3::Execute
Continua a execução desse processo de um estado parado. Qualquer estado de execução anterior (por exemplo, uma etapa) é limpo e o processo inicia a execução novamente.

> [!NOTE]
> Esse método deve ser usado em vez de [Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md).

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Execute(
   IDebugThread2* pThread
);
```

```csharp
int Execute(
   IDebugThread2 pThread
);
```

#### <a name="parameters"></a>Parâmetros
 `pThread`

 [in] Uma [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) objeto que representa a execução do thread.

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retornará o código de erro.

## <a name="remarks"></a>Comentários
 Quando o usuário inicia a execução de um estado parado em algum outro thread do processo, esse método é chamado sobre esse processo. Esse método também é chamado quando o usuário seleciona o **inicie** comando da **depurar** menu no IDE. A implementação desse método pode ser tão simple quanto chamar o [retomar](../../../extensibility/debugger/reference/idebugthread2-resume.md) método no thread no processo atual.

> [!WARNING]
> Não enviar um evento de interrupção ou um evento (síncrono) imediato [evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) ao manipular essa chamada; caso contrário, o depurador poderá parar de responder.

## <a name="see-also"></a>Consulte também
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)