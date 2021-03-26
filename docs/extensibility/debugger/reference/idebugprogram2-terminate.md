---
description: Encerra o programa.
title: 'IDebugProgram2:: Terminate | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Terminate
helpviewer_keywords:
- IDebugProgram2::Terminate
ms.assetid: 4d3127d3-b1e9-4b28-ac22-2f2eea255f86
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 404df2be6718ab691ec47081b6fd400a1ddc8891
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084461"
---
# <a name="idebugprogram2terminate"></a>IDebugProgram2::Terminate
Encerra o programa.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Terminate( 
   void 
);
```

```csharp
int Terminate();
```

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Se possível, o programa será encerrado e descarregado do processo; caso contrário, o mecanismo de depuração (DE) executará qualquer limpeza necessária.

 Esse método ou o método [Terminate](../../../extensibility/debugger/reference/idebugprocess2-terminate.md) é chamado pelo IDE, normalmente em resposta ao usuário que está interrompendo toda a depuração. A implementação desse método deve, de preferência, encerrar o programa dentro do processo. Se isso não for possível, o DE deve impedir que o programa execute mais nenhum nesse processo (e faça qualquer limpeza necessária). Se o `IDebugProcess2::Terminate` método foi chamado pelo IDE, todo o processo será encerrado em algum momento depois que o `IDebugProgram2::Terminate` método for chamado.

## <a name="see-also"></a>Confira também
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [Encerrar](../../../extensibility/debugger/reference/idebugprocess2-terminate.md)
