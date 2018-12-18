---
title: IDebugEngine2::RemoveSetException | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugEngine2::RemoveSetException
helpviewer_keywords:
- IDebugEngine2::RemoveSetException
ms.assetid: bdd25097-0e9d-4218-b417-0497ea48d2e8
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4880bfc80f27c362deb056b176492eb62ec6f975
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49941536"
---
# <a name="idebugengine2removesetexception"></a>IDebugEngine2::RemoveSetException
Remove a exceção especificada, para que ele não é tratado pelo mecanismo de depuração.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT RemoveSetException(   
   EXCEPTION_INFO* pException  
);  
```  
  
```csharp  
int RemoveSetException(   
   EXCEPTION_INFO[] pException  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pException`  
 [in] Uma [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) estrutura que descreve a exceção a ser removido.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 A exceção que está sendo removida deve ter sido anteriormente definida por uma chamada anterior para o [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md) método.  
  
 Para remover todas as exceções do conjunto ao mesmo tempo, chame o [RemoveAllSetExceptions](../../../extensibility/debugger/reference/idebugengine2-removeallsetexceptions.md) método.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)   
 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)