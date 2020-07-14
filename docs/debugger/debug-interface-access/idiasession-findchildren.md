---
title: IDiaSession::findChildren | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findChildren method
ms.assetid: 5d19046f-f668-4aa9-8788-95cda9a98997
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dcc62ed0b4a1f0a9ddd43ef692f748db4d9b6f10
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465835"
---
# <a name="idiasessionfindchildren"></a>IDiaSession::findChildren
Recupera todos os filhos de um identificador pai especificado que correspondem ao nome e ao tipo de símbolo.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findChildren ( 
   IDiaSymbol*       parent,
   SymTagEnum        symtag,
   LPCOLESTR         name,
   DWORD             compareFlags,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>Parâmetros
 `parent`

no Um objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representa o pai. Se esse símbolo pai for uma função, módulo ou bloco, seus filhos léxicos serão retornados em `ppResult` . Se o símbolo pai for um tipo, sua classe filho será retornada. Se esse parâmetro for `NULL` , `symtag` deve ser definido como `SymTagExe` ou `SymTagNull` , que retorna o escopo global (arquivo. exe).

 `symtag`

no Especifica a marca de símbolo dos filhos a serem recuperados. Os valores são obtidos da enumeração de [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md) . Defina como `SymTagNull` para recuperar todos os filhos.

 `name`

no Especifica o nome dos filhos a serem recuperados. Defina como `NULL` para todos os filhos a serem recuperados.

 `compareFlags`

no Especifica as opções de comparação aplicadas à correspondência de nomes. Os valores da enumeração de [Enumeração NameSearchOptions](../../debugger/debug-interface-access/namesearchoptions.md) podem ser usados sozinhos ou em combinação.

 `ppResult`

fora Retorna um objeto [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) que contém a lista de símbolos filho recuperados.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra como localizar variáveis locais da função `pFunc` que correspondem ao nome `szVarName` .

```C++
IDiaEnumSymbols* pEnum;
pSession->findChildren( pFunc, SymTagData, szVarName, nsCaseSensitive, &pEnum );
```

## <a name="see-also"></a>Veja também
- [Visão geral](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração NameSearchOptions](../../debugger/debug-interface-access/namesearchoptions.md)
- [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)