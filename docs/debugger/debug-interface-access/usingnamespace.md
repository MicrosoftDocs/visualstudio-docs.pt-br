---
description: Alguns símbolos podem ser referenciados pelo namespace e, subsequentemente, ser identificados por uma marca SymTagUsingNameSpace.
title: UsingNameSpace | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- UsingNamespace symbol tag
ms.assetid: e8e1beb5-7cb9-43b4-9ff4-760d5f91ea2d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1fde0be17059342c3b00ba43cab93f4464e31f1e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161539"
---
# <a name="usingnamespace"></a>UsingNameSpace
Alguns símbolos podem ser referenciados pelo namespace e, subsequentemente, ser identificados por uma `SymTagUsingNameSpace` marca.

> [!NOTE]
> A marca de símbolo UsingNamespace aparece apenas no código gerenciado.

## <a name="properties"></a>Propriedades
 A tabela a seguir mostra as propriedades que são válidas para esse tipo de símbolo.

|Propriedade|Tipo de dados|Descrição|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|Símbolo para o compiland, o bloco ou a função delimitador.|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|ID do símbolo pai léxico.|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|Nome do namespace.|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|ID do índice do símbolo.|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|Retorna `SymTagNameSpace` (um dos valores de [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md) ).|

## <a name="see-also"></a>Confira também
- [Hierarquia lexical de tipos de símbolo](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
