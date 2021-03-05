---
description: Recupera um símbolo por seu identificador exclusivo.
title: IDiaSession::symbolById | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::symbolById method
ms.assetid: 062e4b5a-9c4d-4703-88da-ec13102c2b66
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 979825cd3e62c97334d55676b3bf32bf874f8445
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102147600"
---
# <a name="idiasessionsymbolbyid"></a>IDiaSession::symbolById
Recupera um símbolo por seu identificador exclusivo.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT symbolById (
    DWORD        id,
    IDiaSymbol** ppSymbol
);
```

#### <a name="parameters"></a>Parâmetros
`id`

no Identificador exclusivo.

`ppSymbol`

fora Retorna um objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representa o símbolo recuperado.

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
O identificador especificado é um valor exclusivo usado internamente pelo DIA SDK para tornar todos os símbolos exclusivos.

Esse método pode ser usado, por exemplo, para recuperar o símbolo que representa o tipo de outro símbolo (consulte o exemplo).

## <a name="example"></a>Exemplo
Este exemplo recupera um [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representa o tipo de outro símbolo. Este exemplo mostra como usar o `symbolById` método na sessão. Uma abordagem mais simples é chamar o método [IDiaSymbol:: get_Type](../../debugger/debug-interface-access/idiasymbol-get-type.md) para recuperar o símbolo de tipo diretamente.

```C++
IDiaSymbol *GetSymbolType(IDiaSymbol *pSymbol, IDiaSession *pSession)
{
    IDiaSymbol *pTypeSymbol = NULL;
    if (pSymbol != NULL && pSession != NULL)
    {
        DWORD symbolTypeId;
        pSymbol->get_typeId(&symbolTypeId);
        pSession->symbolById(symbolTypeId, &pTypeSymbol);
    }
    return(pTypeSymbol);
}
```

## <a name="see-also"></a>Confira também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)
