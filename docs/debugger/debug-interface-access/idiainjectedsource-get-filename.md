---
description: Recupera o nome do arquivo para a origem.
title: IDiaInjectedSource::get_filename | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_filename method
ms.assetid: 20f4fc68-335a-4971-b3a6-76501f0e8b19
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e41b7d3b80f2e0f63a53fb9a0d6d63627af59d75
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102148424"
---
# <a name="idiainjectedsourceget_filename"></a>IDiaInjectedSource::get_filename
Recupera o nome do arquivo para a origem.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_filename ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 pRetVal

fora Retorna o nome do arquivo para a origem.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
