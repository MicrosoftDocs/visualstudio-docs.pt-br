---
title: IDiaSymbol::get_token | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_token method
ms.assetid: 7ee7a9be-a0d8-48e4-9fef-d37b3d6ae4ef
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 717c7efe5792a7df53139571273b4796e2e7f030
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461749"
---
# <a name="idiasymbolget_token"></a>IDiaSymbol::get_token
Recupera o token de metadados de uma função ou variável gerenciada.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_token ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o token de metadados de uma função ou variável gerenciada.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)