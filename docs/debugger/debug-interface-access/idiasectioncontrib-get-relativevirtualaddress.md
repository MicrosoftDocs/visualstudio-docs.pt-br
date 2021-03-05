---
description: Recupera o endereço virtual relativo da imagem (RVA) da contribuição.
title: IDiaSectionContrib::get_relativeVirtualAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_relativeVirtualAddress method
ms.assetid: 32f9674d-94f1-4590-99de-a2eb60da4af8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4bd7e1271ed163e9efe4971ca4af08858e79c7ff
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102147992"
---
# <a name="idiasectioncontribget_relativevirtualaddress"></a>IDiaSectionContrib::get_relativeVirtualAddress
Recupera o endereço virtual relativo da imagem (RVA) da contribuição.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_relativeVirtualAddress ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o RVA da imagem da contribuição.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
