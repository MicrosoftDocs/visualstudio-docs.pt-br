---
description: Move o ponteiro de leitura no fluxo de desmontagem de um determinado número de instruções relativas a uma posição especificada.
title: 'IDebugDisassemblyStream2:: Seek | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::Seek
helpviewer_keywords:
- IDebugDisassemblyStream2::Seek
ms.assetid: afec3008-b1e0-4803-ad24-195dbfb6497e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 02277bf84bdc12e904b2651ef5ba9fc2356d9090
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066926"
---
# <a name="idebugdisassemblystream2seek"></a>IDebugDisassemblyStream2::Seek
Move o ponteiro de leitura no fluxo de desmontagem de um determinado número de instruções relativas a uma posição especificada.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Seek( 
   SEEK_START          dwSeekStart,
   IDebugCodeContext2* pCodeContext,
   UINT64              uCodeLocationId,
   INT64               iInstructions
);
```

```csharp
int Seek( 
   enum_SEEK_START    dwSeekStart,
   IDebugCodeContext2 pCodeContext,
   ulong              uCodeLocationId,
   long               iInstructions
);
```

## <a name="parameters"></a>Parâmetros
`dwSeekStart`\
no Um valor da enumeração [SEEK_START](../../../extensibility/debugger/reference/seek-start.md) que especifica a posição relativa para iniciar o processo de busca.

`pCodeContext`\
no O objeto [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) que representa o contexto de código ao qual a operação de busca é relativa. Esse parâmetro é usado somente se `dwSeekStart`  =  `SEEK_START_CODECONTEXT` ; caso contrário, esse parâmetro é ignorado e pode ser um valor nulo.

`uCodeLocationId`\
no O identificador de local do código ao qual a operação de busca é relativa. Esse parâmetro será usado se `dwSeekStart`  =  `SEEK_START_CODELOCID` ; caso contrário, esse parâmetro será ignorado e poderá ser definido como 0. Consulte a seção comentários do método [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md) para obter uma descrição de um identificador de local de código.

`iInstructions`\
no O número de instruções a serem movidas em relação à posição especificada em `dwSeekStart` . Esse valor pode ser negativo para mover para trás.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se a posição de busca era para um ponto além da lista de instruções disponíveis. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Se a busca foi até uma posição antes do início da lista, a posição de leitura é definida como a primeira instrução na lista. Se a visualização foi feita em uma posição após o final da lista, a posição de leitura é definida como a última instrução na lista.

## <a name="see-also"></a>Confira também
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [SEEK_START](../../../extensibility/debugger/reference/seek-start.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)
