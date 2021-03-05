---
description: Esse método converte um local do método e desloca em um endereço de memória.
title: 'IDebugExpressionEvaluator:: GetMethodLocationProperty | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty
helpviewer_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty method
ms.assetid: 52c42a2e-f144-476b-8bef-442464c8fe8e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f841f602064b21035ea409457c708f99ec25bf12
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102152514"
---
# <a name="idebugexpressionevaluatorgetmethodlocationproperty"></a>IDebugExpressionEvaluator::GetMethodLocationProperty
Esse método converte um local do método e desloca em um endereço de memória.

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

## <a name="parameters"></a>Parâmetros
`upstrFullyQualifiedMethodPlusOffset`\
no O local e o deslocamento do método, expressos como uma cadeia de caracteres.

`pSymbolProvider`\
no O provedor de símbolos expresso como um objeto [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) .

`pAddress`\
no Um endereço dentro do método, expresso como um objeto [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) .

`pBinder`\
no O associador expresso como um objeto [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) .

`ppProperty`\
fora Retorna uma interface [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) que representa o endereço de memória.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 O endereço retornado pode ser usado para definir um ponto de interrupção, por exemplo.

 Apesar do nome `upstrFullyQualifiedMethodPlusOffset` , esse parâmetro pode ser passado para um nome de método parcialmente qualificado. Nesse caso, o método selecionado é aquele que se fecha `pAddress` . Como esse parâmetro é interpretado é até a implementação do avaliador de expressão e o idioma para o qual ele dá suporte.

## <a name="see-also"></a>Confira também
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
