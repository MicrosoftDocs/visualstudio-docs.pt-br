---
title: IDebugEngine3::SetAllExceptions | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetAllExceptions
helpviewer_keywords:
- IDebugEngine3::SetAllExceptions
ms.assetid: 8f03a6ac-a854-42f7-933c-a2df1b351975
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 48abbfb47e346ad9acbfac7b92642e6638f67df3
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58925126"
---
# <a name="idebugengine3setallexceptions"></a>IDebugEngine3::SetAllExceptions
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Esse método define o estado de todas as exceções pendentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetAllExceptions(  
   EXCEPTION_STATE dwState  
);  
```  
  
```csharp  
int SetAllExceptions(  
   enum_EXCEPTION_STATE dwState  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `dwState`  
 [in] Um dos [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md) valores.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retornará o código de erro.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)   
 [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md)
