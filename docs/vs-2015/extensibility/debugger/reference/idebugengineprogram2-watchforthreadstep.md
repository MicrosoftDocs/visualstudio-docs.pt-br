---
title: IDebugEngineProgram2::WatchForThreadStep | Microsoft Docs
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
- IDebugEngineProgram2::WatchForThreadStep
helpviewer_keywords:
- IDebugEngineProgram2::WatchForThreadStep
ms.assetid: b70922a3-1313-409a-b3b7-50c7cd13e394
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: baab97b35ee19b889ca4db2578e85f8f88f2ed47
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49907788"
---
# <a name="idebugengineprogram2watchforthreadstep"></a>IDebugEngineProgram2::WatchForThreadStep
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Aguarda a execução (ou interrompe a assistir a execução) para ocorrer em determinado thread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT WatchForThreadStep(   
   IDebugProgram2* pOriginatingProgram,  
   DWORD           dwTid,  
   BOOL            fWatch,  
   DWORD           dwFrame  
);  
```  
  
```csharp  
int WatchForThreadStep(   
   IDebugProgram2 pOriginatingProgram,  
   uint           dwTid,  
   int            fWatch,  
   uint           dwFrame  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pOriginatingProgram`  
 [in] Uma [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) objeto que representa o programa que está sendo passado.  
  
 `dwTid`  
 [in] Especifica o identificador do thread para assistir.  
  
 `fWatch`  
 [in] Diferente de zero (`TRUE`) significa começar a observar para execução no thread identificado por `dwTid`; caso contrário, zero (`FALSE`) significa parar de monitorar para execução em `dwTid`.  
  
 `dwFrame`  
 [in] Especifica um índice do quadro que controla o tipo de etapa. Quando se trata do que valor é zero (0), o tipo de etapa é "step into" e o programa deve ser interrompida sempre que o thread identificado por `dwTid` executa. Quando `dwFrame` é diferente de zero, o tipo de etapa é "step over" e o programa deve parar somente se o thread identificado por `dwTid` está em execução em um quadro cujo índice é igual ou superior na pilha que `dwFrame`.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Quando o Gerenciador de sessão de depuração (SDM) as etapas de um programa, identificado pelo `pOriginatingProgram` parâmetro, ele notifica todos os outros programas conectados ao chamar esse método.  
  
 Esse método é aplicável somente a revisão do mesmo thread.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)

