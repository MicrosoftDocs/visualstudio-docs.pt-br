---
description: Desanexa o depurador desse processo desanexando todos os programas no processo.
title: IDebugProcess2::D Etach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::Detach
helpviewer_keywords:
- IDebugProcess2::Detach
ms.assetid: ee2b9084-2db1-4e49-a1d9-387284b7c3f8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b4d75f9dd58e2a26f6d465fc93988fa3d3785a0d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071656"
---
# <a name="idebugprocess2detach"></a>IDebugProcess2::Detach
Desanexa o depurador desse processo desanexando todos os programas no processo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Detach( 
   void 
);
```

```csharp
int Detach();
```

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Todos os programas e o processo continuam em execução, mas não fazem mais parte da sessão de depuração. Depois que a operação de desanexação for concluída, não serão enviados mais eventos de depuração para esse processo (e seus programas).

## <a name="see-also"></a>Confira também
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
