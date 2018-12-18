---
title: IDebugPointerField::GetDereferencedField | Microsoft Docs
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
- IDebugPointerField::GetDereferencedField
helpviewer_keywords:
- IDebugPointerField::GetDereferencedField method
ms.assetid: 8de988ab-cd79-4287-be72-3c900f2fe407
caps.latest.revision: 8
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 24989a5f509cd42b21ee0ed8b88f8eaac272968d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51787504"
---
# <a name="idebugpointerfieldgetdereferencedfield"></a>IDebugPointerField::GetDereferencedField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Esse método retorna o tipo de objeto para o qual este objeto de ponteiro aponta.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT GetDereferencedField(  
   IDebugField** ppField  
);  
```  
  
```csharp  
int GetDereferencedField(  
   out IDebugField ppField  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ppField`  
 [out] Retorna um [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) que descreve o tipo de objeto de destino.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Se, por exemplo, o [IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md) objeto aponta para um número inteiro, o [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) tipo retornado por esse método descreve que tipo de inteiro.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)

