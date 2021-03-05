---
description: Define o endereço de carregamento para o arquivo executável que corresponde aos símbolos neste repositório de símbolos.
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 05dc21a67a88270c4d3bce46387e46ed5a8e8497
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102156996"
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

## <a name="see-also"></a>Confira também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
