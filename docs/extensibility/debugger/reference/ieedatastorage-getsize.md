---
description: Retorna o número de bytes contidos neste objeto.
title: 'IEEDataStorage:: GetSize | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage::GetSize
helpviewer_keywords:
- IEEDataStorage::GetSize
ms.assetid: 33d232c4-1239-4abc-922b-e1bc5b908169
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 46051ae73859213b3206e27fb83d40c0561d0c0b
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102222920"
---
# <a name="ieedatastoragegetsize"></a>IEEDataStorage::GetSize
Retorna o número de bytes contidos neste objeto.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetSize(
   ULONG* size
);
```

```csharp
int GetSize(
   out uint size
);
```

## <a name="parameters"></a>Parâmetros
`size`\
fora O número de bytes contidos neste objeto.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Use o método [GetData](../../../extensibility/debugger/reference/ieedatastorage-getdata.md) para recuperar os bytes de dados reais.

## <a name="see-also"></a>Confira também
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [GetData](../../../extensibility/debugger/reference/ieedatastorage-getdata.md)
