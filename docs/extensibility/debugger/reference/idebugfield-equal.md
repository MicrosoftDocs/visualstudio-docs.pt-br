---
description: Esse método compara esse campo com o campo especificado para igualdade.
title: 'IDebugField:: equal | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::Equal
helpviewer_keywords:
- IDebugField::Equal method
ms.assetid: 75369fe6-ddd3-497d-80d1-2488e6100e9f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 58673703fa0e585095c9a82fe2c7a4bc3e14827c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077103"
---
# <a name="idebugfieldequal"></a>IDebugField::Equal
Esse método compara esse campo com o campo especificado para igualdade.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Equal( 
   IDebugField* pField
);
```

```csharp
int Equal(
   IDebugField pField
);
```

## <a name="parameters"></a>Parâmetros
`pField`\
no O campo a ser comparado a este.

## <a name="return-value"></a>Valor Retornado
 Se os campos forem iguais, retorna `S_OK` . Se os campos forem diferentes, retorna de `S_FALSE.` outra forma, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
