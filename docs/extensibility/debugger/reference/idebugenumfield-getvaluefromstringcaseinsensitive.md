---
description: Esse método usa uma pesquisa que não diferencia maiúsculas de minúsculas para retornar o valor associado ao nome de uma constante de enumeração.
title: 'IDebugEnumField:: GetValueFromStringCaseInsensitive | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetValueFromStringCaseInsensitive
helpviewer_keywords:
- IDebugEnumField::GetValueFromStringCaseInsensitive method
ms.assetid: ef95b38e-d9b2-4fb5-a166-7c2e14641dc7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f853598c5d3c9b293c806e1db475c5053a1a208e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153216"
---
# <a name="idebugenumfieldgetvaluefromstringcaseinsensitive"></a>IDebugEnumField::GetValueFromStringCaseInsensitive
Esse método usa uma pesquisa que não diferencia maiúsculas de minúsculas para retornar o valor associado ao nome de uma constante de enumeração.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetValueFromStringCaseInsensitive(
   LPCOLESTR  pszValue,
   ULONGLONG* pvalue
);
```

```csharp
int GetValueFromStringCaseInsensitive(
   string    pszValue,
   out ulong pValue
);
```

## <a name="parameters"></a>Parâmetros
`pszValue`\
no Uma cadeia de caracteres que especifica o nome para o qual obter o valor. Observe que para C++, essa é uma cadeia de caracteres larga.

`pValue`\
fora Retorna o valor numérico associado.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK` ; caso contrário, retornará `S_FALSE` , se o nome não fizer parte da enumeração ou um código de erro.

## <a name="remarks"></a>Comentários
 Esse método não diferencia maiúsculas de minúsculas. Se uma pesquisa com diferenciação de maiúsculas e minúsculas for necessária (por exemplo, em uma linguagem como C++, em que os nomes diferenciam maiúsculas de minúsculas), use [GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md).

## <a name="see-also"></a>Confira também
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
- [GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)
