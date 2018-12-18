---
title: IDebugObject::IsEqual | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugObject::IsEqual
helpviewer_keywords:
- IDebugObject::IsEqual method
ms.assetid: 4b76e663-ef2e-41ff-9be1-bf26d666a34a
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 91e84d47f7fc60e60c3c7fb58ba66bc0a00daf30
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49839993"
---
# <a name="idebugobjectisequal"></a>IDebugObject::IsEqual
Compara um objeto com esse objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT IsEqual(   
   IDebugObject* pObject,  
   BOOL*         pfIsEqual  
);  
```  
  
```csharp  
int IsEqual(  
   IDebugObject pObject,  
   out int      pfIsEqual  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pObject`  
 [in] Uma [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) objeto que representa o objeto a ser comparado.  
  
 `pfIsEqual`  
 [out] Retorna não zero (`TRUE`) se os valores dos objetos forem iguais; caso contrário, retornará zero (`FALSE`).  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará S_OK; Caso contrário, retornará um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Normalmente, esse método pode comparar os endereços dos valores representados pelo `pObject` parâmetro e isso [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) objeto; se os endereços são iguais e, em seguida, os objetos podem ser considerados iguais.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)