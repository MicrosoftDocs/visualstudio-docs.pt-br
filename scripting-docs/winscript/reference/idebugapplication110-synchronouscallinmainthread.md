---
title: IDebugApplication110::SynchronousCallInMainThread | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplication110::SynchronousCallInMainThread
ms.assetid: 57475ae5-1520-45ef-800d-ccfc6235a5d1
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ef52ebfe8bfccecc0eea2383787a5b2698a5ce5f
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725796"
---
# <a name="idebugapplication110synchronouscallinmainthread"></a>IDebugApplication110::SynchronousCallInMainThread
Faz uma chamada síncrona no thread principal.  
  
> [!IMPORTANT]
>  [Interface IDebugApplication110](../../winscript/reference/idebugapplication110-interface.md) é implementada por v PDM 11.0 e maior. Localizado em. activdbg100.h.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SynchronousCallInMainThread([in] IDebugThreadCall* pptc, [in] DWORD_PTR dwParam1, [in] DWORD_PTR dwParam2, [in] DWORD_PTR dwParam3);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pptc`  
 O [IDebugThreadCall Interface](../../winscript/reference/idebugthreadcall-interface.md) objeto chamar.  
  
 `dwParam1`  
 O primeiro parâmetro da chamada.  
  
 `dwParam1`  
 O primeiro parâmetro da chamada.  
  
 `dwParam2`  
 O segundo parâmetro da chamada.  
  
 `dwParam3`  
 O terceiro parâmetro da chamada.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugApplication110 Interface](../../winscript/reference/idebugapplication110-interface.md)