---
description: Esse método define o idioma a ser usado para criar resultados imprimíveis.
title: 'IDebugExpressionEvaluator:: setlocale | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::SetLocale
helpviewer_keywords:
- IDebugExpressionEvaluator::SetLocale method
ms.assetid: d3d2027d-74e2-4ae6-bcc7-59d12f873b7c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5f833311fe9029931c0d56cbe828bd027c45c26a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092053"
---
# <a name="idebugexpressionevaluatorsetlocale"></a>IDebugExpressionEvaluator::SetLocale
Esse método define o idioma a ser usado para criar resultados imprimíveis.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT SetLocale( 
   WORD wLangID
);
```

```csharp
int SetLocale(
   ushort wLangID
);
```

## <a name="parameters"></a>Parâmetros
`wLangID`\
no O identificador de idioma.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método pode ser chamado muitas vezes enquanto o avaliador de expressão (EE) é carregado, portanto, o EE deve ser capaz de alternar os idiomas de forma dinâmica. O EE usa essa localidade para retornar mensagens de erro e cadeias de caracteres no idioma apropriado.

## <a name="see-also"></a>Confira também
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
