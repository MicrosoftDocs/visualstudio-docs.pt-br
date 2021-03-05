---
description: Recupera os nomes de cadeia de caracteres correspondentes para determinados identificadores de propriedade.
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cbb6d511a6be9ed408b076162a3d00d22705075a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102148139"
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

## <a name="see-also"></a>Confira também
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
