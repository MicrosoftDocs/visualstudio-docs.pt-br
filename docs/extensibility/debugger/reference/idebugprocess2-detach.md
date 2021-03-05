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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5775ee9ffc3fa3c4151df999b64ba1160da6f7c3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166275"
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
