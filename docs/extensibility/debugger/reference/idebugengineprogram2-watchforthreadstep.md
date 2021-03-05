---
description: Inspeciona a execução (ou pára de observar a execução) para ocorrer no thread determinado.
title: 'IDebugEngineProgram2:: WatchForThreadStep | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::WatchForThreadStep
helpviewer_keywords:
- IDebugEngineProgram2::WatchForThreadStep
ms.assetid: b70922a3-1313-409a-b3b7-50c7cd13e394
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: eaf02e07bebbbfd711d99ef7605befbdce1f9376
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153411"
---
# <a name="idebugengineprogram2watchforthreadstep"></a>IDebugEngineProgram2::WatchForThreadStep
Inspeciona a execução (ou pára de observar a execução) para ocorrer no thread determinado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT WatchForThreadStep( 
   IDebugProgram2* pOriginatingProgram,
   DWORD           dwTid,
   BOOL            fWatch,
   DWORD           dwFrame
);
```

```csharp
int WatchForThreadStep( 
   IDebugProgram2 pOriginatingProgram,
   uint           dwTid,
   int            fWatch,
   uint           dwFrame
);
```

## <a name="parameters"></a>Parâmetros
`pOriginatingProgram`\
no Um objeto [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) que representa o programa que está sendo percorrido.

`dwTid`\
no Especifica o identificador do thread a ser inspecionado.

`fWatch`\
no Diferente de zero ( `TRUE` ) significa começar a assistir para execução no thread identificado por `dwTid` ; caso contrário, zero ( `FALSE` ) significa parar de assistir para execução em `dwTid` .

`dwFrame`\
no Especifica um índice de quadro que controla o tipo de etapa. Quando esse valor for zero (0), o tipo de etapa será "Step Into" e o programa deverá ser interrompido sempre que o thread identificado pelo for `dwTid` executado. Quando `dwFrame` for diferente de zero, o tipo de etapa será "Step Over" e o programa deverá parar somente se o thread identificado pelo `dwTid` estiver em execução em um quadro cujo índice seja igual ou superior na pilha do que `dwFrame` .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Quando o SDM (Gerenciador de depuração de sessão) percorre um programa, identificado pelo `pOriginatingProgram` parâmetro, ele notifica todos os outros programas anexados chamando esse método.

 Esse método é aplicável somente à depuração do mesmo thread.

## <a name="see-also"></a>Confira também
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
