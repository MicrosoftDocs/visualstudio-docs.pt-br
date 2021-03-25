---
title: IDebugProgramNode2::D etachDebugger_V7 | Microsoft Docs
description: Esse método é uma forma antiga e preterida do método Detach usado antes do Visual Studio 2005.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::DetachDebugger
helpviewer_keywords:
- IDebugProgramNode2::DetachDebugger
- IDebugProgramNode2::DetachDebugger_V7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 16630be49dd884f8bcc82da2fead158eb3a25e5e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053549"
---
# <a name="idebugprogramnode2detachdebugger_v7"></a>IDebugProgramNode2::DetachDebugger_V7

> [!Note]
> Preterido. NÃO USE.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT DetachDebugger_V7 (
   void 
);
```

```csharp
int DetachDebugger_V7 ();
```

## <a name="return-value"></a>Valor retornado

Uma implementação sempre deve retornar `E_NOTIMPL` .

## <a name="remarks"></a>Comentários

> [!WARNING]
> A partir do Visual Studio 2005, esse método não é mais usado e sempre deve retornar `E_NOTIMPL` .

Esse método é chamado quando o depurador é encerrado inesperadamente. Quando esse método é chamado, o DE deve retomar o programa como se o usuário fosse desanexado dele. Não devem ser enviados mais eventos de depuração. O programa deve estar em um estado no qual é possível anexá-lo de outra instância do depurador.

## <a name="see-also"></a>Confira também

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
