---
description: OBSOLETO. Recarrega os símbolos para este módulo.
title: 'IDebugModule2:: ReloadSymbols_Deprecated | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule2::ReloadSymbols
helpviewer_keywords:
- IDebugModule2::ReloadSymbols method
ms.assetid: 0f9f0133-7d58-4cd9-a6ca-1141e095749d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5dfcd1edd92048cde6da6cc195c3e0ba8f1cd392
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065704"
---
# <a name="idebugmodule2reloadsymbols_deprecated"></a>IDebugModule2::ReloadSymbols_Deprecated
OBSOLETO. NÃO USE. Recarrega os símbolos para este módulo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT ReloadSymbols( 
   LPCOLESTR pszUrlToSymbols,
   BSTR*     pbstrDebugMessage
);
```

```csharp
int ReloadSymbols( 
   string     pszUrlToSymbols,
   out string pbstrDebugMessage
);
```

## <a name="parameters"></a>Parâmetros
`pszUrlToSymbols`\
no O caminho para o repositório de símbolos.

`pbstrDebugMessage`\
fora Retorna uma mensagem informativa, como um status ou uma mensagem de erro, que é exibida à direita do nome do módulo na janela módulos.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Um mecanismo de depuração sempre deve retornar `E_FAIL` .

## <a name="remarks"></a>Comentários
 Não há mais suporte para este método. Em vez disso, implemente o método [LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md) .

## <a name="see-also"></a>Confira também
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)
