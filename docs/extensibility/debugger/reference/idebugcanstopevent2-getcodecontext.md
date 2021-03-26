---
description: Obtém o contexto de código que descreve o local desse evento.
title: 'IDebugCanStopEvent2:: GetCodeContext | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::GetCodeContext
helpviewer_keywords:
- IDebugCanStopEvent2::GetCodeContext
ms.assetid: eecf08b6-f9b7-4358-941b-3a448a92ac62
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b906241a189edf78f3917d7d80ba4e4e073d50c4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088582"
---
# <a name="idebugcanstopevent2getcodecontext"></a>IDebugCanStopEvent2::GetCodeContext
Obtém o contexto de código que descreve o local desse evento.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetCodeContext( 
   IDebugCodeContext2** ppCodeContext
);
```

```csharp
int GetCodeContext( 
   out IDebugCodeContext2 ppCodeContext
);
```

## <a name="parameters"></a>Parâmetros
`ppCodeContext`\
fora Retorna o objeto [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) que representa o local do código atual.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Para a maioria das arquiteturas de tempo de execução, um contexto de código pode ser considerado um endereço no fluxo de execução de um programa, apontando para uma instrução específica.

 Para obter o contexto do documento, que é orientado em direção às linhas do código-fonte, chame o método [GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md) .

## <a name="see-also"></a>Confira também
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)
