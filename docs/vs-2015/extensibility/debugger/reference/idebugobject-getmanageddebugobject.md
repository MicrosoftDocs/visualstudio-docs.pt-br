---
title: IDebugObject::GetManagedDebugObject | Microsoft Docs
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
- IDebugObject::GetManagedDebugObject
helpviewer_keywords:
- IDebugObject::GetManagedDebugObject method
ms.assetid: cb89692e-7657-47ff-846d-311943521951
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 5530865b9d6c7cfb74c91f00b6a65e41702135cb
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51807264"
---
# <a name="idebugobjectgetmanageddebugobject"></a>IDebugObject::GetManagedDebugObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Cria uma cópia do objeto gerenciado no espaço de endereço do mecanismo de depuração.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT GetManagedDebugObject(   
   IDebugManagedObject** ppObject  
);  
```  
  
```csharp  
int GetManagedDebugObject(  
   out IDebugManagedObject ppObject  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ppObject`  
 [out] Retorna um [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md) objeto que representa o objeto gerenciado recém-criado.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará S_OK; Caso contrário, retornará um código de erro. Retornará E_FAIL se este [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) não representa uma instância da classe de valor gerenciado.  
  
## <a name="remarks"></a>Comentários  
 Isso [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) objeto deve representar uma instância da classe de valor gerenciado, como um `System.Decimal` instância. Fazendo uma cópia local, a sobrecarga da chamada [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) é eliminado.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)   
 [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)

