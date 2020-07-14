---
title: 'IDiaPropertyStorage:: ReadLONG | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadLONG
ms.assetid: 32054cbc-db55-4513-a1b4-de80e77aac8a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 697d93af1256d76e5448de5cbc34e04ffc26927f
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466577"
---
# <a name="idiapropertystoragereadlong"></a>IDiaPropertyStorage::ReadLONG
Lê `LONG` valores em um conjunto de propriedades.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT ReadDLONG ( 
   PROPID id,
   LONG*  pValue
);
```

#### <a name="parameters"></a>Parâmetros
 `id`

no Identificador da propriedade a ser lida ( `PROPID` definida em WTypes. h como um `ULONG` ).

 `pValue`

fora Retorna o valor da propriedade.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Retorna `E_INVALIDARG` se a propriedade não é do tipo `LONG` .

## <a name="remarks"></a>Comentários
 Um `LONG` é definido pelo Windows como um inteiro com sinal de 32 bits.

## <a name="see-also"></a>Veja também
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)