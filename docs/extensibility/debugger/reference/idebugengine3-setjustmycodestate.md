---
title: IDebugEngine3::SetJustMyCodeState | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugEngine3::SetJustMyCodeState
helpviewer_keywords:
- IDebugEngine3::SetJustMyCodeState
ms.assetid: 8ec17fbf-df93-424a-b2ed-fd1e5ee51256
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ffad3e6be4d81e19bd6f707bd30c744904217ba5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49928965"
---
# <a name="idebugengine3setjustmycodestate"></a>IDebugEngine3::SetJustMyCodeState
Esse método informa o mecanismo de depuração sobre as informações de estado de JustMyCode.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetJustMyCodeState(  
   BOOL           fUpdate,  
   DWORD          dwModules,  
   JMC_CODE_SPEC* rgJMCSpec  
);  
```  
  
```csharp  
int SetJustMyCodeState(  
   int             fUpdate,   
   uint            dwModules,   
   JMC_CODE_SPEC[] rgJMCSpec  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `fUpdate`  
 [in] Diferente de zero (`TRUE`) para atualizar as informações atuais, zero (`FALSE`) para redefinir todas as informações (ignorando tudo definido anteriormente).  
  
 `dwModules`  
 [in] Número de estruturas de informações em `rgJMCSpec.`  
  
 `rgJMCSpec`  
 [in] Matriz de [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md) estruturas para usar.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retornará o código de erro.  
  
## <a name="remarks"></a>Comentários  
 JustMyCode é o conceito de depuração somente o código que pertence a um usuário e ignorando todo o código intermediário, como o código do sistema — mesmo se o código-fonte está disponível para esse código do sistema.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)   
 [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md)