---
title: IDiaSession::put_loadAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::put_loadAddress method
ms.assetid: b157b245-1ea0-4b80-8962-d8b278dbc742
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 807346ef5a34c0b175257fe2099dc25e8de692f6
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465380"
---
# <a name="idiasessionput_loadaddress"></a>IDiaSession::put_loadAddress
Define o endereço de carregamento para o arquivo executável que corresponde aos símbolos neste repositório de símbolos.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT put_loadAddress ( 
   ULONGLONG NewVal
);
```

#### <a name="parameters"></a>Parâmetros
 `NewVal`

no Carregue o endereço para o arquivo executável.

## <a name="remarks"></a>Comentários
 As propriedades de endereço virtual de símbolo (VA) são computadas usando o valor desse método. Os endereços virtuais não são calculados, a menos que essa propriedade seja definida como diferente de zero.

> [!NOTE]
> Você deve chamar esse método quando obter o objeto [IDiaSession](../../debugger/debug-interface-access/idiasession.md) e antes de começar a usar o objeto se precisar usar qualquer propriedade virtual em símbolos.

## <a name="see-also"></a>Veja também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)