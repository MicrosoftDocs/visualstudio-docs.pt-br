---
title: IDiaSectionContrib::get_virtualAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_virtualAddress method
ms.assetid: e5b44a81-0804-429b-97d8-467cbba3132a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9a85192d0ee5bc36241177a0e2e7c91933ec8e24
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99855343"
---
# <a name="idiasectioncontribget_virtualaddress"></a>IDiaSectionContrib::get_virtualAddress
Recupera o endereço virtual (VA) da contribuição.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_virtualAddress ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o VA da contribuição.

## <a name="return-value"></a>Valor retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Consulte também
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)