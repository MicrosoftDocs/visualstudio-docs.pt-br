---
title: IDiaSymbol::get_upperBoundId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_upperBoundId method
ms.assetid: ddfa1617-bd0f-4187-ba77-a225bab93a95
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6d573f54a6264562c02960448768a8409fcc5e5a
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461542"
---
# <a name="idiasymbolget_upperboundid"></a>IDiaSymbol::get_upperBoundId
Recupera o identificador de símbolo do limite superior de uma dimensão de matriz FORTRAN.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_upperBoundId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`
- [fora,] Retorna a ID do símbolo que representa o limite superior de uma dimensão de matriz FORTRAN.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 O identificador é um valor exclusivo criado pelo DIA SDK para marcar todos os símbolos como exclusivos.

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)