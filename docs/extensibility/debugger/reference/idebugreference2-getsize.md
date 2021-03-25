---
description: Obtém o tamanho, em bytes, do valor da referência.
title: 'IDebugReference2:: GetSize | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetSize
helpviewer_keywords:
- IDebugReference2::GetSize
ms.assetid: a404ddd9-d940-4513-97cd-f52b8ab6a560
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 061b4422efced1480a8f42cf39b7fdb648834b3b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075829"
---
# <a name="idebugreference2getsize"></a>IDebugReference2::GetSize
Obtém o tamanho, em bytes, do valor da referência. Reservado para uso futuro.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetSize ( 
   DWORD* pdwSize
);
```

```csharp
int GetSize ( 
   out uint pdwSize
);
```

## <a name="parameters"></a>Parâmetros
`pdwSize`\
fora Retorna o tamanho, em bytes, do valor da referência.

## <a name="return-value"></a>Valor Retornado
 Sempre retorna `E_NOTIMPL`.

## <a name="see-also"></a>Confira também
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
