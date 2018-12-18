---
title: IDebugApplication110::CallableWaitForHandles | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplication110::CallableWaitForHandles
ms.assetid: 02e79b60-0d67-47f9-bf78-b65a02c9c014
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b259f5296f8e0b32def793a81e4c2e1069643306
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725346"
---
# <a name="idebugapplication110callablewaitforhandles"></a>IDebugApplication110::CallableWaitForHandles
Esperas para qualquer uma das alças especificadas deve ser sinalizado permitindo chamadas entre threads para esse thread. Esse método deve ser chamado do thread do depurador.  
  
> [!IMPORTANT]
>  [Interface IDebugApplication110](../../winscript/reference/idebugapplication110-interface.md) é implementada por v PDM 11.0 e maior. Localizado em. activdbg100.h.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CallableWaitForHandles([in] DWORD handleCount, [in, size_is(handleCount)] const HANDLE* pHandles, [out] DWORD* pIndex);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `handleCount`  
 O número de identificadores de espera para.  
  
 `pHandles`  
 O conjunto de identificadores de espera para.  
  
 `pIndex`  
 Quando o valor HRESULT é S_OK, o índice `pHandles` para o identificador que foi sinalizado.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugApplication110 Interface](../../winscript/reference/idebugapplication110-interface.md)