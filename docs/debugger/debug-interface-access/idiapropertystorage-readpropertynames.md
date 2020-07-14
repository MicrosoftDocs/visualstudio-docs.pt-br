---
title: IDiaPropertyStorage::ReadPropertyNames | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadPropertyNames
ms.assetid: f8bcab77-afca-4a8f-8710-697842f8a518
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 257546e54cb04713f2f13892ec782aca1712cfba
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466514"
---
# <a name="idiapropertystoragereadpropertynames"></a>IDiaPropertyStorage::ReadPropertyNames
Recupera os nomes de cadeia de caracteres correspondentes para determinados identificadores de propriedade.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT ReadPropertyNames (
   ULONG         cpropid,
   PROPID const* rgpropid,
   BSTR*         rglpwstrName
);
```

#### <a name="parameters"></a>Parâmetros
 `cpropid`

no Número de IDs de propriedade no `rgpropid` .

 `rgpropid`

no Matriz de IDs de propriedade para as quais obter os nomes ( `PROPID` é definido em WTypes. h como um `ULONG` ).

 `rglpwstrName`

[entrada, saída] Matriz de nomes de propriedade para as IDs de propriedade especificadas. A matriz deve ser pré-configurada para conter o número solicitado de nomes de propriedade e deve ser capaz de armazenar pelo menos `cpropid``BSTR` cadeias de caracteres.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Os nomes de propriedade retornados devem ser liberados (chamando a `SysFreeString` função) quando não forem mais necessários.

## <a name="see-also"></a>Veja também
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)