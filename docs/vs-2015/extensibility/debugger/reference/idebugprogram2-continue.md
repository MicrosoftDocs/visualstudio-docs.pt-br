---
title: IDebugProgram2::Continue | Microsoft Docs
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
- IDebugProgram2::Continue
helpviewer_keywords:
- IDebugProgram2::Continue
ms.assetid: e5a6e02a-d21b-4a03-a034-e8de1f71ce2e
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: b90f9bd5fef44ab05cf835f41e274b4ec7695cab
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51744315"
---
# <a name="idebugprogram2continue"></a>IDebugProgram2::Continue
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Continua a execução deste programa de um estado parado. Qualquer estado de execução anterior (por exemplo, uma etapa) é preservado, e o programa inicia a execução novamente.  
  
> [!NOTE]
>  Esse método é preterido. Use o [continuar](../../../extensibility/debugger/reference/idebugprocess3-continue.md) método em vez disso.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT Continue(   
   IDebugThread2* pThread  
);  
```  
  
```csharp  
int Continue(   
   IDebugThread2 pThread  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pThread`  
 [in] Uma [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) objeto que representa o thread.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Este método é chamado neste programa, independentemente de quantos aplicativos estão sendo depurados, ou qual programa gerou o evento de interrupção. A implementação deve manter o estado de execução anterior (por exemplo, uma etapa) e continuar a execução como se ele nunca foi interrompido antes de concluir sua execução anterior. Ou seja, se um thread nesse programa estava fazendo uma operação de percorrer e foi interrompido porque algum outro programa é interrompido e, em seguida, esse método foi chamado, o programa deve concluir a operação percorrer original.  
  
> [!WARNING]
>  Não enviar um evento de interrupção ou um evento (síncrono) imediato [evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) ao manipular essa chamada; caso contrário, o depurador poderá parar de responder.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)   
 [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)

