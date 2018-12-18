---
title: IDebugApplicationThread110::IsThreadCallable | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationThread110::IsThreadCallable
ms.assetid: 2a75a366-801d-47e0-bba3-51aa669e03a7
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b34e2c45d7e94c72ade62780f46f4b5c7c22405e
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725566"
---
# <a name="idebugapplicationthread110isthreadcallable"></a>IDebugApplicationThread110::IsThreadCallable
Determina se esse thread está em um estado que processará as chamadas feitas usando o thread do PDM alternância de mecanismos, como SynchronousCallInThread.  
  
> [!IMPORTANT]
>  [Interface IDebugApplicationThread110](../../winscript/reference/idebugapplicationthread110-interface.md) é implementada por v PDM 11.0 e maior. Localizado em. activdbg100.h.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT IsThreadCallable([out, annotation("_Out_")] BOOL * pfIsCallable);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pfIsCallable`  
 [out] `true` se o thread é chamado, caso contrário, `false`.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDebugApplicationThread110](../../winscript/reference/idebugapplicationthread110-interface.md)