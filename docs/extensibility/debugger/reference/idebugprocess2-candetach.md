---
description: Determina se o SDM (Gerenciador de depuração de sessão) pode desanexar o processo.
title: 'IDebugProcess2:: desanexar | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::CanDetach
helpviewer_keywords:
- IDebugProcess2::CanDetach
ms.assetid: 2830f7c3-69fb-474a-97b8-5b869e38d546
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d0ffc6e8ee787960baf7ccb709ab76ab5d66be4d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071682"
---
# <a name="idebugprocess2candetach"></a>IDebugProcess2::CanDetach
Determina se o SDM (Gerenciador de depuração de sessão) pode desanexar o processo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CanDetach(
   void
);
```

```csharp
int CanDetach();
```

## <a name="return-value"></a>Valor retornado
 Se for bem-sucedido, `S_OK.` retornará `S_FALSE` um retorno se o depurador não puder ser desanexado do processo. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Confira também
- [CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
