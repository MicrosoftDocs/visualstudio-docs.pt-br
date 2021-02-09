---
title: 'IDebugEngineProgram2:: Stop | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::Stop
helpviewer_keywords:
- IDebugEngineProgram2::Stop
ms.assetid: 6e1c3d56-fb67-4a5b-80f9-8ee5131972bf
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6013770e3a334e7924cafe4563d437d4f7730bfc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99892678"
---
# <a name="idebugengineprogram2stop"></a>IDebugEngineProgram2::Stop
Interrompe todos os threads em execução neste programa.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Stop( 
   void 
);
```

```csharp
int Stop();
```

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é chamado quando este programa está sendo depurado em um ambiente com vários programas. Quando um evento de parada de algum outro programa é recebido, esse método é chamado neste programa. A implementação desse método deve ser assíncrona; ou seja, nem todos os threads devem ser interrompidos antes que esse método seja retornado. A implementação desse método pode ser tão simples quanto chamar o método [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) neste programa.

 Os implementadores devem enviar um [IDebugStopCompleteEvent2](../../../extensibility/debugger/reference/idebugstopcompleteevent2.md) quando o programa parar.

## <a name="see-also"></a>Confira também
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
