---
title: IDebugCanStopEvent2::CanStop | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDebugCanStopEvent2::CanStop
helpviewer_keywords:
- IDebugCanStopEvent2::CanStop
ms.assetid: 7d61adbe-6b3d-41f3-86a1-45d9cc01a7f8
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: c0b89f694d544cc622ee63f87c77e2ddaf8646d3
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51745425"
---
# <a name="idebugcanstopevent2canstop"></a>IDebugCanStopEvent2::CanStop
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Notifica o mecanismo de depuração (DES) ou não interromper no local atual do código ou simplesmente continuar a execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT CanStop (   
   BOOL fCanStop  
);  
```  
  
```csharp  
int CanStop (   
   int fCanStop  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `fCanStop`  
 [in] Diferente de zero (`TRUE`) se o DE deve parar no local atual do código; caso contrário, zero (`FALSE`).  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 O receptor desse evento normalmente chama o [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md) método para determinar o motivo pelo qual o DE que deseja interromper e, em seguida, chama o `IDebugCanStopEvent2::CanStop` método com a resposta apropriada.  
  
 Se o DE parar, ele envia um evento que descreve o motivo para interrupção. Normalmente, há dois eventos que são enviadas, uma quebra de usuário ou sinal representada pela [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) interface e um evento de ponto de interrupção representado pela [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) interface.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)   
 [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)   
 [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)   
 [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)

