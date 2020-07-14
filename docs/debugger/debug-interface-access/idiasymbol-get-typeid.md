---
title: IDiaSymbol::get_typeId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_typeId method
ms.assetid: b40be36e-10e1-463c-9c6d-21862679d29f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1d9c8f559e86e0acfb4137df61b82e28d21d3dfc
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461708"
---
# <a name="idiasymbolget_typeid"></a>IDiaSymbol::get_typeId
Recupera o identificador de tipo do símbolo.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_typeId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna a ID do tipo do símbolo.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 O identificador é um valor exclusivo criado pelo DIA SDK para marcar todos os símbolos como exclusivos.

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)