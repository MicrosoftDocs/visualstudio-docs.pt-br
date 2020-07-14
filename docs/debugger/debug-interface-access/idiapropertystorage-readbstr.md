---
title: IDiaPropertyStorage::ReadBSTR | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadBSTR
ms.assetid: 7214643b-3286-48ed-90aa-0fe95b4cae5b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c6e87c2ed168a262fc1a12f06fc6a18bcf73e7bc
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466591"
---
# <a name="idiapropertystoragereadbstr"></a>IDiaPropertyStorage::ReadBSTR
Lê `BSTR` valores em um conjunto de propriedades.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT ReadBSTR ( 
   PROPID id,
   BSTR*  pValue
);
```

#### <a name="parameters"></a>Parâmetros
 `id`

no Identificador da propriedade a ser lida ( `PROPID` definida em WTypes. h como um `ULONG` ).

 `pValue`

fora Retorna o valor da propriedade.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Retorna `E_INVALIDARG` se a propriedade não é do tipo `BSTR` .

## <a name="remarks"></a>Comentários
 Um `BSTR` é definido pelo Windows como uma cadeia de caracteres largo terminada em zero.

## <a name="see-also"></a>Veja também
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)