---
title: IDebugObject::SetReferenceValue | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugObject::SetReferenceValue
helpviewer_keywords:
- IDebugObject::SetReferenceValue method
ms.assetid: 08c78a4e-98eb-41cb-8b75-02a6a43d49f7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1b597d7a62880e00a570a1971a6fec2becaaddca
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49908620"
---
# <a name="idebugobjectsetreferencevalue"></a>IDebugObject::SetReferenceValue
Define o valor de referência do objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetReferenceValue(   
   IDebugObject* pObject  
);  
```  
  
```csharp  
int SetReferenceValue(  
   [In] IDebugObject pObject  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pObject`  
 [in] Uma [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) objeto que representa o novo valor de referência.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará S_OK; Caso contrário, retornará um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Esse método faz isso [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) objeto uma referência para o valor do objeto fornecido no `pObject` parâmetro, descartando qualquer referência anterior. Observe que este `IDebugObject` objeto já deve ser um tipo de referência.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)   
 [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)