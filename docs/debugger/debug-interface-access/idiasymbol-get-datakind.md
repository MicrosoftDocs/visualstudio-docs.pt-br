---
title: IDiaSymbol::get_dataKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_dataKind method
ms.assetid: 45005ad0-8b29-4cde-9d33-6bef72f6e463
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6448b30f94924d24358409715af0dec673e31d87
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99863434"
---
# <a name="idiasymbolget_datakind"></a>IDiaSymbol::get_dataKind
Recupera a classificação de variável de um símbolo de dados.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_dataKind ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna um valor da enumeração de [Enumeração datakind](../../debugger/debug-interface-access/datakind.md) especificando o tipo de dados como global, estático ou constante, por exemplo.

## <a name="return-value"></a>Valor retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 7.0|

## <a name="see-also"></a>Consulte também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração DataKind](../../debugger/debug-interface-access/datakind.md)