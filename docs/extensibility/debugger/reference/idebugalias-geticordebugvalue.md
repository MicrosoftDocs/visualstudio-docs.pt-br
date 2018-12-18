---
title: IDebugAlias::GetICorDebugValue | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugAlias::GetICorDebugValue
helpviewer_keywords:
- IDebugAlias::GetICorDebugValue method
ms.assetid: b9eb39ee-84af-4ace-9cfe-236b3d48aff5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 393d5a7310a136ad83b7cbd74fca966633ffb62e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49833168"
---
# <a name="idebugaliasgeticordebugvalue"></a>IDebugAlias::GetICorDebugValue
Recupera uma interface de código gerenciado que representa o valor associado a este alias.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetICorDebugValue(  
   IUnknown** ppUnk  
);  
```  
  
```csharp  
int GetICorDebugValue(  
   out object ppUnk  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ppUnk`  
 [out] `IUnknown` interface que representa o valor associado a este alias. Essa interface pode ser consultada para o `ICorDebugValue` interface.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará S_OK; Caso contrário, retornará um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Esse método se aplica somente aos valores gerenciados (o `ICorDebugValue` é uma interface disponíveis na [!INCLUDE[dnprdnshort](../../../code-quality/includes/dnprdnshort_md.md)] e é definido no [!INCLUDE[dnprdnshort](../../../code-quality/includes/dnprdnshort_md.md)] SDK no arquivo cordebug. idl).  
  
## <a name="see-also"></a>Consulte também  
 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)