---
title: IEnumDebugPorts2::Reset | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- IEnumDebugPorts2::Reset
helpviewer_keywords:
- IEnumDebugPorts2::Reset
ms.assetid: 67da406c-eadb-421e-ae12-e26e9866f262
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a5f2f7c852e3643c89522eb95b72ab573dd65808
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54980759"
---
# <a name="ienumdebugports2reset"></a>IEnumDebugPorts2::Reset
Redefine a enumeração para o primeiro elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Reset(  
   void  
);  
```  
  
```csharp  
int Reset();  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Depois que esse método é chamado, a próxima chamada para o [próxima](../../../extensibility/debugger/reference/ienumdebugports2-next.md) método retorna o primeiro elemento da enumeração.  
  
## <a name="see-also"></a>Consulte também  
 [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)