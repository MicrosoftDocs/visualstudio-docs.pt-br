---
title: IDiaPropertyStorage::ReadBOOL | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadBOOL
ms.assetid: ad1822db-4572-48f7-9919-f8137f6701f2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 60d985851b1d547eed4306762c453bdd480bb1a9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99855588"
---
# <a name="idiapropertystoragereadbool"></a>IDiaPropertyStorage::ReadBOOL
Lê `BOOL` valores em um conjunto de propriedades.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT ReadBOOL ( 
   PROPID id,
   BOOL*  pValue
);
```

#### <a name="parameters"></a>Parâmetros
 `id`

no Identificador da propriedade a ser lida ( `PROPID` definida em WTypes. h como um `ULONG` ).

 `pValue`

fora Retorna o valor da propriedade.

## <a name="return-value"></a>Valor retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Retorna `E_INVALIDARG` se a propriedade não é do tipo `BOOL` .

## <a name="remarks"></a>Comentários
 Para obter resultados consistentes, interprete o `BOOL` valor de forma que os valores diferentes de `TRUE` zero sejam `FALSE` .

## <a name="see-also"></a>Consulte também
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)