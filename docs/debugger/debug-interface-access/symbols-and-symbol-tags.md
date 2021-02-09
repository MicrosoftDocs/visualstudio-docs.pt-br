---
title: Símbolos e marcas de símbolo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK]
ms.assetid: 2ee3a262-cda6-48bf-b799-a37edde6c8b8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 12f1927e4290ff9d008eff9f497c9d570d9d44f8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99862279"
---
# <a name="symbols-and-symbol-tags"></a>Símbolos e marcas de símbolos
As informações de depuração sobre um programa compilado são armazenadas no arquivo do banco de dados do programa (. pdb) como símbolos que são acessíveis usando as APIs do SDK de acesso à interface de depuração (DIA). Todos os símbolos têm uma propriedade [IDiaSymbol:: get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md) e [IDiaSymbol:: get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md) . A `symTag` propriedade indica o tipo de símbolo conforme definido pela enumeração de [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md) . A `symIndexId` propriedade é um `DWORD` valor que contém o identificador exclusivo para cada instância de um símbolo.

 Os símbolos também têm propriedades que podem especificar informações adicionais sobre o símbolo, bem como referências a outros símbolos, geralmente um [IDiaSymbol:: get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md) ou [IDiaSymbol:: get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md). Quando você consulta uma propriedade que contém uma referência, a referência é retornada como um objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) . Essas propriedades são sempre emparelhadas com outra propriedade com o mesmo nome, mas com sufixo "ID", por exemplo, [IDiaSymbol:: get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md) e [IDiaSymbol:: get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md). As tabelas em [locais de símbolo](../../debugger/debug-interface-access/symbol-locations.md), [hierarquia lexical de tipos de símbolo](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)e [hierarquia de classes de tipos de símbolo](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md) descrevem as propriedades de cada um dos diferentes tipos de símbolos. Essas propriedades podem ter informações relevantes sobre ou referências a outros símbolos. Como as `*Id` Propriedades são simplesmente identificadores ordinais numéricos de suas propriedades relacionadas, elas são omitidas de outras discussões. Eles são referidos apenas onde necessário para o esclarecimento do parâmetro.

 Ao tentar acessar a propriedade, se nenhum erro ocorrer e a propriedade Symbol tiver sido atribuído um valor, o método "Get" da propriedade retornará `S_OK` . Um valor de retorno `S_FALSE` indica que a propriedade não é válida para o símbolo atual.

## <a name="in-this-section"></a>Nesta seção

[Locais de símbolos](../../debugger/debug-interface-access/symbol-locations.md)

Descreve os diferentes tipos de locais que um símbolo pode ter.

[Hierarquia lexical de tipos de símbolo](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)

Descreve os tipos de símbolo que formam hierarquias léxicas, como arquivos, módulos e funções.

[Hierarquia de classes de tipos de símbolo](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)

Descreve os tipos de símbolo que correspondem a elementos de linguagem diferentes, como classes, matrizes e tipos de retorno de função.

## <a name="see-also"></a>Consulte também

- [SDK de Acesso à Interface de Depuração](../../debugger/debug-interface-access/debug-interface-access-sdk.md)