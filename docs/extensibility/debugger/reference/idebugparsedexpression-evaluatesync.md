---
description: Esse método avalia a expressão analisada e, opcionalmente, converte o resultado em outro tipo de dados.
title: 'IDebugParsedExpression:: EvaluateSync | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugParsedExpression::EvaluateSync
helpviewer_keywords:
- IDebugParsedExpression::EvaluateSync method
ms.assetid: 0ea04cfa-de87-4b6c-897e-4572c1a28942
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 99760fb35975834186beddf2962ea8402543d088
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143097"
---
# <a name="idebugparsedexpressionevaluatesync"></a>IDebugParsedExpression::EvaluateSync
Esse método avalia a expressão analisada e, opcionalmente, converte o resultado em outro tipo de dados.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EvaluateSync( 
   DWORD                 dwEvalFlags,
   DWORD                 dwTimeout,
   IDebugSymbolProvider* pSymbolProvider,
   IDebugAddress*        pAddress,
   IDebugBinder*         pBinder,
   BSTR                  bstrResultType,
   IDebugProperty2**     ppResult
);
```

```csharp
int EvaluateSync(
   uint                 dwEvalFlags,
   uint                 dwTimeout,
   IDebugSymbolProvider pSymbolProvider,
   IDebugAddress        pAddress,
   IDebugBinder         pBinder,
   string               bstrResultType,
   out IDebugProperty2  ppResult
);
```

## <a name="parameters"></a>Parâmetros
`dwEvalFlags`\
no Uma combinação de constantes [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) que controlam como a expressão deve ser avaliada.

`dwTimeout`\
no Especifica o tempo máximo, em milissegundos, a aguardar antes de retornar desse método. Use `INFINITE` para aguardar indefinidamente.

`pSymbolProvider`\
no O provedor de símbolos, expresso como uma interface [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) .

`pAddress`\
no O local de execução atual dentro de um método, expresso como uma interface [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) .

`pBinder`\
no O associador, expresso como uma interface [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) .

`bstrResultType`\
no O tipo do qual o resultado deve ser convertido. Esse argumento pode ser um valor nulo.

`ppResult`\
fora Retorna a interface [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) que representa os resultados da avaliação.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 O contexto de avaliação de expressão é fornecido pelo `pAddress` , o que torna possível determinar o método que o contém e, em seguida, usar regras de escopo de linguagem para determinar o valor dos símbolos na expressão.

## <a name="see-also"></a>Confira também
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
