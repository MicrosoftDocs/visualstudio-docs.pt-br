---
title: Hierarquia lexical de tipos de símbolo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK], type hierarchies
ms.assetid: 912da653-ddfe-45a4-84aa-64281283739a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b003fcbd1b38eb5dc919b7f4f361e0b56b585f08
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461220"
---
# <a name="lexical-hierarchy-of-symbol-types"></a>Hierarquia lexical de tipos de símbolos
A tabela a seguir mostra os tipos de símbolo na hierarquia lexical.

## <a name="symbol-types"></a>Tipos de símbolo

|Tipo de símbolo|Descrição|
|-----------------|-----------------|
|[Anotação](../../debugger/debug-interface-access/annotation.md)|Especifica um local anotado no código do programa.|
|[Bloquear](../../debugger/debug-interface-access/block.md)|Especifica escopos aninhados em funções.|
|`Compiland`|Especifica um `compiland` link para o arquivo. exe.|
|[CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)|Especifica dados de compiland que podem exigir o carregamento de detalhes de compiland adicionais e, portanto, incorrem na sobrecarga de tempo de execução para recuperar.|
|[CompilandEnv](../../debugger/debug-interface-access/compilandenv.md)|Especifica quaisquer variáveis de ambiente adicionais significativas para a compilação do compiland.|
|[Custom (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/custom-debug-interface-access-sdk.md)|Especifica um símbolo definido pelo usuário.|
|[Dados (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/data-debug-interface-access-sdk.md)|Especifica essas variáveis como parâmetros, variáveis locais, variáveis globais e membros de classe.|
|[Exe](../../debugger/debug-interface-access/exe.md)|Especifica o escopo global dos dados; corresponde a um arquivo. exe ou. dll inteiro.|
|[FuncDebugEnd](../../debugger/debug-interface-access/funcdebugend.md)|Especifica uma função que tem um ponto definido no qual a depuração deve terminar.|
|[FuncDebugStart](../../debugger/debug-interface-access/funcdebugstart.md)|Especifica uma função que tem um ponto definido no qual a depuração deve começar.|
|[Função (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/function-debug-interface-access-sdk.md)|Especifica uma função.|
|[Rótulo (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/label-debug-interface-access-sdk.md)|Especifica um local no código do programa.|
|[PublicSymbol](../../debugger/debug-interface-access/publicsymbol.md)|Especifica um símbolo externo que aparece ao criar o programa executável.|
|[Conversão](../../debugger/debug-interface-access/thunk.md)|Especifica um `thunk` .|
|[UsingNameSpace](../../debugger/debug-interface-access/usingnamespace.md)|Especifica um `namespace` identificador.|

> [!NOTE]
> As propriedades de símbolo adicionais podem estar disponíveis dependendo do tipo de símbolo. Essas propriedades são listadas nos tópicos de símbolos individuais.

## <a name="see-also"></a>Veja também
- [Hierarquia de classes de tipos de símbolo](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)
- [IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)
- [Símbolos e marcas de símbolos](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)
- [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)