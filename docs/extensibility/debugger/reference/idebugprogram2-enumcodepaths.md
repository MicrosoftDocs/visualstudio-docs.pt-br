---
description: Recupera uma lista de caminhos de código para uma determinada posição em um arquivo de origem.
title: 'IDebugProgram2:: EnumCodePaths | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumCodePaths
helpviewer_keywords:
- IDebugProgram2::EnumCodePaths
ms.assetid: fb100c3c-9c29-4d63-bd1f-a3e531cb395f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c647379d0b72832a4068d720846f8a9331f9b939
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102159959"
---
# <a name="idebugprogram2enumcodepaths"></a>IDebugProgram2::EnumCodePaths
Recupera uma lista de caminhos de código para uma determinada posição em um arquivo de origem.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumCodePaths( 
   LPCOLESTR            pszHint,
   IDebugCodeContext2*  pStart,
   IDebugStackFrame2*   pFrame,
   BOOL                 fSource,
   IEnumCodePaths2**    ppEnum,
   IDebugCodeContext2** ppSafety
);
```

```csharp
int EnumCodePaths( 
   string                 pszHint,
   IDebugCodeContext2     pStart,
   IDebugStackFrame2      pFrame,
   Int                    fSource,
   out IEnumCodePaths2    ppEnum,
   out IDebugCodeContext2 ppSafety
);
```

## <a name="parameters"></a>Parâmetros
`pszHint`\
no A palavra sob o cursor na exibição de **origem** ou de **desmontagem** no IDE.

`pStart`\
no Um objeto [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) que representa o contexto de código atual.

`pFrame`\
no Um objeto [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) que representa o quadro de pilhas associado ao ponto de interrupção atual.

`fSource`\
no Diferente de zero ( `TRUE` ) se estiver na exibição de **origem** ou zero ( `FALSE` ) se estiver na exibição de **desmontagem** .

`ppEnum`\
fora Retorna um objeto [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md) que contém uma lista de caminhos de código.

`ppSafety`\
fora Retorna um objeto [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) que representa um contexto de código adicional a ser definido como um ponto de interrupção, caso o caminho de código escolhido seja ignorado. Isso pode acontecer no caso de uma expressão booliana de curto-circuito, por exemplo.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Um caminho de código descreve o nome de um método ou função que foi chamado para chegar ao ponto atual na execução do programa. Uma lista de caminhos de código representa a pilha de chamadas.

## <a name="see-also"></a>Confira também
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
