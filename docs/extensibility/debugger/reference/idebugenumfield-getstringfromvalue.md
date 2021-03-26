---
description: Esse método obtém o nome da constante de enumeração de acordo com seu valor.
title: 'IDebugEnumField:: GetStringFromValue | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetStringFromValue
helpviewer_keywords:
- IDebugEnumField::GetStringFromValue method
ms.assetid: 5f95fd0c-fdce-497f-9f54-2ad8749494e9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 41d004a9b226646dd1196f1debc244cdf11efe32
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092573"
---
# <a name="idebugenumfieldgetstringfromvalue"></a>IDebugEnumField::GetStringFromValue
Esse método obtém o nome da constante de enumeração de acordo com seu valor.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetStringFromValue(
   ULONGLONG value,
   BSTR*     pbstrValue
);
```

```csharp
int GetStringFromValue(
   ulong      value,
   out string pbstrValue
);
```

## <a name="parameters"></a>Parâmetros
`value`\
no O valor para o qual obter o nome da constante de enumeração.

`pbstrValue`\
fora Retorna o nome da constante de enumeração.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` se o valor não tem nenhum nome associado ou retorna um código de erro.

## <a name="remarks"></a>Comentários
 Se houver mais de um nome associado ao mesmo valor, o primeiro nome definido na enumeração será retornado.

## <a name="see-also"></a>Confira também
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
