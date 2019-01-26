---
title: IDebugProperty2::SetValueAsReference | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- IDebugProperty2::SetValueAsReference
helpviewer_keywords:
- IDebugProperty2::SetValueAsReference method
ms.assetid: 341b1b89-4ab8-4e1c-abe2-fb955df5c6b0
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7b185d284c7b5d5970737fa28aa006c636a6e6f1
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54951476"
---
# <a name="idebugproperty2setvalueasreference"></a>IDebugProperty2::SetValueAsReference
Define o valor dessa propriedade como o valor da referência fornecida.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetValueAsReference(  
   IDebugReference2** rgpArgs,  
   DWORD              dwArgCount,  
   IDebugReference2*  pValue,  
   DWORD              dwTimeout  
);  
```  
  
```csharp  
int SetValueAsReference(  
   IDebugReference2[] rgpArgs,  
   uint               dwArgCount,  
   IDebugReference2   pValue,  
   uint               dwTimeout  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `rgpArgs`  
 [in] Uma matriz de argumentos a serem passados para o setter de propriedade de código gerenciado. Se a propriedade setter não recebe argumentos ou se esse [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) objeto não faz referência a tal um setter de propriedade `rgpArgs` deve ser um valor nulo. Normalmente, esse parâmetro é um valor nulo.  
  
 `dwArgCount`  
 [in] O número de argumentos no `rgpArgs` matriz.  
  
 `pValue`  
 [in] Uma referência, na forma de um [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) objeto para o valor a ser usado para definir essa propriedade.  
  
 `dwTimeout`  
 [in] Quanto tempo para ser o valor, em milissegundos. Um valor típico é `INFINITE`. Isso afeta o período de tempo que qualquer avaliação possível.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retornará um erro de código, geralmente um dos seguintes:  
  
|Erro|Descrição|  
|-----------|-----------------|  
|`E_SETVALUEASREFERENCE_NOTSUPPORTED`|Não há suporte para a definição do valor de uma referência.|  
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|O valor não pode ser definido como essa propriedade se refere a um método.|  
|`E_SETVALUE_VALUE_IS_READONLY`|O valor é somente leitura e não pode ser definido.|  
|`E_NOTIMPL`|O método não está implementado.|  
  
## <a name="see-also"></a>Consulte também  
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)