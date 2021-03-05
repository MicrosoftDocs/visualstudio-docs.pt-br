---
description: Recupera o nome do arquivo da biblioteca ou do arquivo de objeto do qual o objeto foi carregado.
title: IDiaSymbol::get_libraryName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_libraryName method
ms.assetid: d04ddd9a-812d-46e4-bd39-28bdf3edfb70
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e717e1794531114d7b68966ef19bdbb2158bfe60
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161987"
---
# <a name="idiasymbolget_libraryname"></a>IDiaSymbol::get_libraryName
Recupera o nome do arquivo da biblioteca ou do arquivo de objeto do qual o objeto foi carregado.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_libraryName ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o nome do arquivo da biblioteca ou do arquivo de objeto do qual o objeto foi carregado.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
