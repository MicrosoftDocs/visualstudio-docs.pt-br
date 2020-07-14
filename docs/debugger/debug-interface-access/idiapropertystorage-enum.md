---
title: 'IDiaPropertyStorage:: enum | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::Enum
ms.assetid: 00e462da-980a-40b3-a2d6-75a25ee809e5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 89c5b6418e832dd145837e579cfded3f47022e00
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466598"
---
# <a name="idiapropertystorageenum"></a>IDiaPropertyStorage::Enum
Obtém um enumerador para propriedades dentro deste conjunto.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Enum ( 
   IEnumSTATPROPSTG** ppenum
);
```

#### <a name="parameters"></a>Parâmetros
 `ppenum`

fora Retorna um `IEnumSTATPROPSTG` objeto (no namespace Microsoft. VisualStudio. OLE. Interop) que representa uma enumeração de propriedades.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)