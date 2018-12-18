---
title: Estrutura DebugStackFrameDescriptor | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DebugStackFrameDescriptor
apilocation:
- scrobj.dll
helpviewer_keywords:
- DebugStackFrameDescriptor structure
ms.assetid: a86bcb99-41e4-4a26-a1dd-e1458fb73139
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 346f039ca96f2160d7ac28686e542b3d88a91dfb
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24641126"
---
# <a name="debugstackframedescriptor-structure"></a>Estrutura DebugStackFrameDescriptor
Enumera os registros de ativação e mescla saídas de vários enumeradores no mesmo thread.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef struct tagDebugStackFrameDescriptor {  
   IDebugStackFrame *pdsf;  
   DWORD_PTR        dwMin;  
   DWORD_PTR        dwLim;  
   BOOL             fFinal;  
   IUnknown         *punkFinal;  
} DebugStackFrameDescriptor;  
```  
  
## <a name="members"></a>Membros  
 `pdsf`  
 O objeto do quadro de pilha.  
  
 `dwMin`  
 Uma representação de dependente de máquina do intervalo inferior dos endereços físicos associados a este quadro de pilha.  
  
 `dwLim`  
 Uma representação de dependente de máquina do intervalo superior dos endereços físicos associados a este quadro de pilha.  
  
 `fFinal`  
 Sinalizador que indica que o quadro está sendo processado.  
  
 `punkFinal`  
 Se esse parâmetro não for `NULL`, o enumerador atual de mesclagem deve ser interrompida e uma nova deve ser iniciada. O objeto indica como iniciar nova enumeração.  
  
## <a name="remarks"></a>Comentários  
 O Gerenciador de depuração do processo usa essa estrutura para classificar os registros de ativação de vários mecanismos de script. Por convenção, as pilhas crescem para baixo. Consequentemente, em arquiteturas onde pilhas crescem, os endereços devem estar complementado pares.  
  
## <a name="see-also"></a>Consulte também  
 [Constantes, enumerações e estruturas de depurador do script ativo](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)