---
title: IDebugPort2::GetPortSupplier | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPort2::GetPortSupplier
helpviewer_keywords:
- IDebugPort2::GetPortSupplier
ms.assetid: 7a7b0615-df6b-4726-ab35-39dfa1ebed8f
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e897259dbbd8c5045a72853bccd0b9c8b7423318
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58927185"
---
# <a name="idebugport2getportsupplier"></a>IDebugPort2::GetPortSupplier
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Obtém o fornecedor de porta para essa porta.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT GetPortSupplier(   
   IDebugPortSupplier2** ppSupplier  
);  
```  
  
```csharp  
int GetPortSupplier(   
   out IDebugPortSupplier2 ppSupplier  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ppSupplier`  
 [out] Retorna um [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) objeto representa o fornecedor de porta para uma porta.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
