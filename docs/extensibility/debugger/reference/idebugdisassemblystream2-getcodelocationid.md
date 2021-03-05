---
description: Retorna um identificador de local de código para um contexto de código específico.
title: 'IDebugDisassemblyStream2:: GetCodeLocationId | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
helpviewer_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
ms.assetid: 567adfb8-2f54-499a-a027-e4ecb82277ef
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8c1c3a6f7a9f2e2a0617f1322d17073a9dcc7c32
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162921"
---
# <a name="idebugdisassemblystream2getcodelocationid"></a>IDebugDisassemblyStream2::GetCodeLocationId
Retorna um identificador de local de código para um contexto de código específico.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetCodeLocationId( 
   IDebugCodeContext2* pCodeContext,
   UINT64*             puCodeLocationId
);
```

```csharp
int GetCodeLocationId( 
   IDebugCodeContext2 pCodeContext,
   out ulong          puCodeLocationId
);
```

## <a name="parameters"></a>Parâmetros
`pCodeContext`\
no Um objeto [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) a ser convertido em um identificador.

`puCodeLocationId` fora Retorna o identificador de local do código. Consulte Observações.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Retorna `E_CODE_CONTEXT_OUT_OF_SCOPE` se o contexto de código é válido, mas fora do escopo.

## <a name="remarks"></a>Comentários
 O identificador de local de código é específico para o mecanismo de depuração (DE) que dá suporte à desmontagem. Esse identificador de local é usado internamente pelo DE para rastrear posições no código e normalmente é um endereço ou deslocamento de algum tipo. O único requisito é que, se o contexto de código de um local for menor que o contexto de código de outro local, o identificador de local de código correspondente do primeiro contexto de código também deverá ser menor que o identificador de local de código do segundo contexto de código.

 Para recuperar o contexto de código de um identificador de local de código, chame o método [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md) .

## <a name="see-also"></a>Confira também
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)
