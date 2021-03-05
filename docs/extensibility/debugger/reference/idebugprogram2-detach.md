---
description: Desanexa um mecanismo de depuração do programa.
title: IDebugProgram2::D Etach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Detach
helpviewer_keywords:
- IDebugProgram2::Detach
ms.assetid: 5e8d88b0-a8d4-4746-88c0-ad332ee73f33
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d303db7043865d770604d7feeec57ddf584fc346
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102146165"
---
# <a name="idebugprogram2detach"></a>IDebugProgram2::Detach
Desanexa um mecanismo de depuração do programa.

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
 Um programa desanexado continua em execução, mas não faz mais parte da sessão de depuração. Nenhum evento de depuração de programas mais é enviado quando o mecanismo de depuração é desanexado.

## <a name="see-also"></a>Confira também
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
