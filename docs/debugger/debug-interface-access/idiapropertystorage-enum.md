---
description: Obtém um enumerador para propriedades dentro deste conjunto.
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d113107621c3254b86356202e94eac6e3e3a8c66
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102148174"
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

## <a name="see-also"></a>Confira também
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
