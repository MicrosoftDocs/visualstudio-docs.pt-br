---
title: IDebugEvent2::GetAttributes | Microsoft Docs
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
- IDebugEvent2::GetAttributes
helpviewer_keywords:
- IDebugEvent2::GetAttributes
ms.assetid: 2ac5b5fb-da17-43f7-811a-313f677e60d7
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: fde5fc207416782576252148a6abcf218ea0bc78
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49841709"
---
# <a name="idebugevent2getattributes"></a>IDebugEvent2::GetAttributes
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Obtém os atributos para este evento de depuração.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT GetAttribute(   
   DWORD* pdwAttrib  
);  
```  
  
```csharp  
int GetAttribute(   
   out uint pdwAttrib  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pdwAttrib`  
 [out] Uma combinação de sinalizadores do [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md) enumeração.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 O [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) interface é comum a todos os eventos. Esse método descreve o tipo de evento; Por exemplo, é o evento síncrono ou assíncrono e é um evento de interrupção ele.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)

