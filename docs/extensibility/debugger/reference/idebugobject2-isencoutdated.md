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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e9b78eb0295d039d4f5d8ca3169cb77d04321aaf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053731"
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
