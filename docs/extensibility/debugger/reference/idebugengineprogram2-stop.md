---
title: IDebugEngineProgram2::Stop | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugEngineProgram2::Stop
helpviewer_keywords:
- IDebugEngineProgram2::Stop
ms.assetid: 6e1c3d56-fb67-4a5b-80f9-8ee5131972bf
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 17919b42f97d2255325c1ceae119014521325c7b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49860819"
---
# <a name="idebugengineprogram2stop"></a>IDebugEngineProgram2::Stop
Interrompe todos os threads em execução nesse programa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Stop(   
   void   
);  
```  
  
```csharp  
int Stop();  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Esse método é chamado quando este programa está sendo depurado em um ambiente de vários programa. Quando um evento de interrupção de algum outro programa for recebido, este método é chamado neste programa. A implementação deste método deve ser assíncrona; ou seja, nem todos os threads devem ser necessárias para ser interrompido antes desse método retorna. A implementação desse método pode ser tão simple quanto chamar o [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) método neste programa.  
  
 Nenhum evento de depuração é enviado em resposta a esse método.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)   
 [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)