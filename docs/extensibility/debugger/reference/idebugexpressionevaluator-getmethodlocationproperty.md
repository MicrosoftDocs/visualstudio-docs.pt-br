---
title: IDebugExpressionEvaluator::GetMethodLocationProperty | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty
helpviewer_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty method
ms.assetid: 52c42a2e-f144-476b-8bef-442464c8fe8e
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c15baa5475e912559b8cc0a23264b0c19ef8a464
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56686724"
---
# <a name="idebugexpressionevaluatorgetmethodlocationproperty"></a>IDebugExpressionEvaluator::GetMethodLocationProperty
Este método converte um local de método e o deslocamento em um endereço de memória.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetMethodLocationProperty( 
   LPCOLESTR             upstrFullyQualifiedMethodPlusOffset,
   IDebugSymbolProvider* pSymbolProvider,
   IDebugAddress*        pAddress,
   IDebugBinder*         pBinder,
   IDebugProperty2**     ppProperty
);
```

```csharp
int GetMethodLocationProperty(
   string               upstrFullyQualifiedMethodPlusOffset,
   IDebugSymbolProvider pSymbolProvider,
   IDebugAddress        pAddress,
   IDebugBinder         pBinder,
   out IDebugProperty2  ppProperty
);
```

#### <a name="parameters"></a>Parâmetros
 `upstrFullyQualifiedMethodPlusOffset`

 [in] O método local e o deslocamento, expresso como uma cadeia de caracteres.

 `pSymbolProvider`

 [in] O provedor de símbolo é expresso como uma [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) objeto.

 `pAddress`

 [in] Um endereço dentro do método, expressado como uma [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) objeto.

 `pBinder`

 [in] O associador expresso como uma [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) objeto.

 `ppProperty`

 [out] Retorna um [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) interface que representa o endereço de memória.

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 O endereço retornado pode ser usado para definir um ponto de interrupção, por exemplo.

 Apesar do nome `upstrFullyQualifiedMethodPlusOffset`, esse parâmetro pode ser passado como um nome de método parcialmente qualificado. Nesse caso, o método selecionado é aquele que circunscreve `pAddress`. Como esse parâmetro é interpretado é até a implementação do avaliador de expressão e o idioma que ele dá suporte.

## <a name="see-also"></a>Consulte também
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)