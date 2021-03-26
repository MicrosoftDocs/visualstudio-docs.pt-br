---
description: Esse método retorna o valor associado ao nome de uma constante de enumeração.
title: 'IDebugEnumField:: GetValueFromString | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetValueFromString
helpviewer_keywords:
- IDebugEnumField::GetValueFromString method
ms.assetid: 1ef8ac5e-a3e0-4078-b876-7f5615aedcbb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ec1070948685c69ce8615e2bef836c4d721e1cb0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092534"
---
# <a name="idebugenumfieldgetvaluefromstring"></a>IDebugEnumField::GetValueFromString
Esse método retorna o valor associado ao nome de uma constante de enumeração.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetValueFromString(
   LPCOLESTR  pszValue,
   ULONGLONG* pvalue
);
```

```csharp
int GetValueFromString(
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
 Esse método diferencia maiúsculas de minúsculas. Se uma pesquisa que não diferencia maiúsculas de minúsculas for necessária (por exemplo, em uma linguagem como Visual Basic onde os nomes não diferenciam maiúsculas de minúsculas), use [GetValueFromStringCaseInsensitive](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstringcaseinsensitive.md).

## <a name="see-also"></a>Confira também
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
- [GetValueFromStringCaseInsensitive](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstringcaseinsensitive.md)
