---
title: IDiaEnumTables::get__NewEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::get__NewEnum method
ms.assetid: 7b1159c7-a5f0-4baa-861a-dc11437d8b93
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3ebe751e43a41f2d8f77c0aea67435b9a2908317
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467536"
---
# <a name="idiaenumtablesget__newenum"></a>IDiaEnumTables::get__NewEnum
Recupera a <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> versão deste enumerador.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get__NewEnum ( 
   IUnknown** pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna a `IUnknown` interface que representa a <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> versão deste enumerador.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)