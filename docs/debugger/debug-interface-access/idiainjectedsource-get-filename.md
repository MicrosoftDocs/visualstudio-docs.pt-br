---
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cc7a1ced59f2a1126df1cf2db3348d9d26fb1461
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467067"
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

## <a name="see-also"></a>Veja também
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)