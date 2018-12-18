---
title: IDebugBinder::Bind | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugBinder::Bind
helpviewer_keywords:
- IDebugBinder::Bind method
ms.assetid: 15a11ad7-0fcc-4e80-ae34-8a7dd7bae3c3
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a1210b84a52aa15d3c8e1bb73bc58d1fbe48a19d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49920346"
---
# <a name="idebugbinderbind"></a>IDebugBinder::Bind
Esse método obtém o contexto de memória ou um objeto que contém o valor atual do símbolo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Bind(   
   IDebugObject*  pContainer,  
   IDebugField*   pField,  
   IDebugObject** ppObject  
);  
```  
  
```csharp  
int Bind(  
   IDebugObject     pContainer,  
   IDebugField      pField,  
   out IDebugObject ppObject  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pContainer`  
 [in] O [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) que contém o filho referenciado por `pField`.  
  
 `pField`  
 [in] O [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) que representa o símbolo.  
  
 `ppObject`  
 [out] Retorna o `IDebugObject` que representa a instância do símbolo.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)   
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)