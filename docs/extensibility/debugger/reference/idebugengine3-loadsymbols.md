---
description: Carrega (conforme necessário) símbolos para todos os módulos que estão sendo depurados por esse mecanismo de depuração.
title: 'IDebugEngine3:: LoadSymbols | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::LoadSymbols
helpviewer_keywords:
- IDebugEngine3::LoadSymbols
ms.assetid: c846a440-1d91-4d48-b8f1-82e902ae152b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 43651baac29b3904b9bc12d8d4b965ca1cd8e3ee
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066171"
---
# <a name="idebugengine3loadsymbols"></a>IDebugEngine3::LoadSymbols
Carrega (conforme necessário) símbolos para todos os módulos que estão sendo depurados por esse mecanismo de depuração.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT LoadSymbols();
```

```csharp
int LoadSymbols();
```

## <a name="parameters"></a>Parâmetros
 Nenhum.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna o código de erro.

## <a name="remarks"></a>Comentários
 Isso carrega os símbolos de depuração para todos os módulos referenciados por esse mecanismo de depuração. Os símbolos serão carregados somente se ainda não tiverem sido carregados. Os símbolos são pesquisados nos caminhos definidos por uma chamada para [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md).

## <a name="see-also"></a>Confira também
- [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
