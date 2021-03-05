---
description: Recupera o número de tabelas.
title: IDiaEnumTables::get_Count | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::get_Count method
ms.assetid: 30fa316b-a746-4028-acae-4efcd2066f38
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c69e1860e3a0b534e53d5431c77cdfa3753a6da1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102157857"
---
# <a name="idiaenumtablesget_count"></a>IDiaEnumTables::get_Count
Recupera o número de tabelas.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_Count (    LONG* pRetVal
);

```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o número de tabelas.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)
