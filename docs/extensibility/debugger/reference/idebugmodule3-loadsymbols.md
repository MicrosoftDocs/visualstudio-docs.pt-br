---
description: Carrega os símbolos para o módulo atual.
title: 'IDebugModule3:: LoadSymbols | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3::LoadSymbols
helpviewer_keywords:
- IDebugModule3::LoadSymbols
ms.assetid: 7548c8c1-cbc6-48aa-a845-19058d4a85bb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2e8a9c34c85263ab538bf07b10b87f12fddf12db
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065509"
---
# <a name="idebugmodule3loadsymbols"></a>IDebugModule3::LoadSymbols
Carrega os símbolos para o módulo atual.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT LoadSymbols(
   void
);
```

```csharp
int LoadSymbols();
```

## <a name="return-value"></a>Valor retornado
 Se o método for bem-sucedido, retornará `S_OK`. Se falhar, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Esse método carrega os símbolos do caminho de pesquisa atual (que pode ser alterado chamando o método [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md) ).

 Esse método é preferencial sobre o método [ReloadSymbols_Deprecated](../../../extensibility/debugger/reference/idebugmodule2-reloadsymbols-deprecated.md) .

## <a name="see-also"></a>Confira também
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
- [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)
