---
title: Estrutura JS_NATIVE_FRAME | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- JS_NATIVE_FRAME
apilocation:
- jscript9diag.dll
ms.assetid: 5afa2ee1-b3e2-47cb-b304-84f96e6fbb14
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a0b624229a96cfc2a2d2044a926f45fa91a1c76c
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571770"
---
# <a name="js_native_frame-structure"></a>Estrutura JS_NATIVE_FRAME
Representa um registro de ativação.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
typedef struct {  
    UINT64 InstructionOffset;    UINT64 ReturnOffset;    UINT64 FrameOffset;    UINT64 StackOffset;  
} JS_NATIVE_FRAME;  
```  
  
## <a name="members"></a>Membros  
 `InstructionOffset`  
 O ponteiro de instrução.  
  
 `ReturnOffset`  
 O endereço de retorno.  
  
 `FrameOffset`  
 O ponteiro do quadro.  
  
 `StackOffset`  
 O ponteiro de pilha.  
  
## <a name="remarks"></a>Comentários  
 O `JS_NATIVE_FRAME` struct é usado pelo `IJsStackFrameEnumerator`.  
  
## <a name="see-also"></a>Consulte também  
 [Constantes, enumerações e estruturas de depurador do script ativo](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)