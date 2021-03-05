---
description: Este método determina se o status editar e continuar deste objeto ou do contêiner pai está desatualizado.
title: 'IDebugObject2:: IsEncOutdated | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::IsEncOutdated
helpviewer_keywords:
- IDebugObject2::IsEncOutdated method
ms.assetid: d3a8c02d-895b-478c-9957-d663130f308e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 583b77ed4f3fbfc81bb595ddde025b8c08f169dd
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170010"
---
# <a name="idebugobject2isencoutdated"></a>IDebugObject2::IsEncOutdated
Este método determina se o status editar e continuar deste objeto ou do contêiner pai está desatualizado. Um avaliador de expressão personalizado não implementa esse método e sempre retorna `E_NOTIMPL` .

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT IsEncOutdated(
   BOOL* pfEncOutdated
);
```

```csharp
int IsEncOutdated(
   out int pfEncOutdated
);
```

## <a name="parameters"></a>Parâmetros
`pfEncOutdated`\
fora Diferente de zero ( `TRUE` ) se o estado editar e continuar estiver desatualizado, zero ( `FALSE` ) se não for.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

> [!NOTE]
> Um avaliador de expressão personalizado sempre deve retornar `E_NOTIMPL` .

## <a name="see-also"></a>Confira também
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
