---
title: SymTagEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- SymTagEnum enumeration
ms.assetid: 528a50cf-e13d-46ec-a98c-323d5d047de9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 29bbb4eed485d3ff354757ab8c83a60b92f566aa
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461045"
---
# <a name="symtagenum"></a>SymTagEnum
Especifica o tipo de símbolo.

## <a name="syntax"></a>Syntax

```C++
enum SymTagEnum {
    SymTagNull,
    SymTagExe,
    SymTagCompiland,
    SymTagCompilandDetails,
    SymTagCompilandEnv,
    SymTagFunction,
    SymTagBlock,
    SymTagData,
    SymTagAnnotation,
    SymTagLabel,
    SymTagPublicSymbol,
    SymTagUDT,
    SymTagEnum,
    SymTagFunctionType,
    SymTagPointerType,
    SymTagArrayType,
    SymTagBaseType,
    SymTagTypedef,
    SymTagBaseClass,
    SymTagFriend,
    SymTagFunctionArgType,
    SymTagFuncDebugStart,
    SymTagFuncDebugEnd,
    SymTagUsingNamespace,
    SymTagVTableShape,
    SymTagVTable,
    SymTagCustom,
    SymTagThunk,
    SymTagCustomType,
    SymTagManagedType,
    SymTagDimension,
    SymTagCallSite,
    SymTagInlineSite,
    SymTagBaseInterface,
    SymTagVectorType,
    SymTagMatrixType,
    SymTagHLSLType
};
```

## <a name="elements"></a>Elementos
`SymTagNull`Indica que o símbolo não tem nenhum tipo.

`SymTagExe`Indica que o símbolo é um arquivo. exe. Há apenas um `SymTagExe` símbolo por repositório de símbolos. Ele serve como o escopo global e não tem um pai léxico.

`SymTagCompiland`Indica o símbolo de compiland para cada componente compiland do repositório de símbolos. Para aplicativos nativos, `SymTagCompiland` os símbolos correspondem aos arquivos de objeto vinculados à imagem. Para alguns tipos de imagens MSIL (Microsoft Intermediate Language), há um compiland por classe.

`SymTagCompilandDetails`Indica que o símbolo contém atributos estendidos do compiland. A recuperação dessas propriedades pode exigir o carregamento de símbolos compiland.

`SymTagCompilandEnv`Indica que o símbolo é uma cadeia de caracteres de ambiente definida para o compiland.

`SymTagFunction`Indica que o símbolo é uma função.

`SymTagBlock`Indica que o símbolo é um bloco aninhado.

`SymTagData`Indica que o símbolo é dado.

`SymTagAnnotation`Indica que o símbolo é para uma anotação de código. Os filhos deste símbolo são cadeias de caracteres de dados constantes ( `SymTagData` , `LocIsConstant` , `DataIsConstant` ). A maioria dos clientes ignora esse símbolo.

`SymTagLabel`Indica que o símbolo é um rótulo.

`SymTagPublicSymbol`Indica que o símbolo é um símbolo público. Para aplicativos nativos, esse símbolo é o símbolo externo COFF encontrado durante a vinculação da imagem.

`SymTagUDT`Indica que o símbolo é um tipo definido pelo usuário (estrutura, classe ou União).

`SymTagEnum`Indica que o símbolo é uma enumeração.

`SymTagFunctionType`Indica que o símbolo é um tipo de assinatura de função.

`SymTagPointerType`Indica que o símbolo é um tipo de ponteiro.

`SymTagArrayType`Indica que o símbolo é um tipo de matriz.

`SymTagBaseType`Indica que o símbolo é um tipo base.

`SymTagTypedef`Indica que o símbolo é um `typedef` , ou seja, um alias para outro tipo.

`SymTagBaseClass`Indica que o símbolo é uma classe base de um tipo definido pelo usuário.

`SymTagFriend`Indica que o símbolo é um amigo de um tipo definido pelo usuário.

`SymTagFunctionArgType`Indica que o símbolo é um argumento de função.

`SymTagFuncDebugStart`Indica que o símbolo é o local final do código de prólogo da função.

`SymTagFuncDebugEnd`Indica que o símbolo é o local inicial do código epílogo da função.

`SymTagUsingNamespace`Indica que o símbolo é um nome de namespace, ativo no escopo atual.

`SymTagVTableShape`Indica que o símbolo é uma descrição de tabela virtual.

`SymTagVTable`Indica que o símbolo é um ponteiro de tabela virtual.

`SymTagCustom`Indica que o símbolo é um símbolo personalizado e não é interpretado por DIA.

`SymTagThunk`Indica que o símbolo é uma conversão usada para compartilhar dados entre 16 e 32 bits de código.

`SymTagCustomType`Indica que o símbolo é um símbolo de compilador personalizado.

`SymTagManagedType`Indica que o símbolo está em metadados.

`SymTagDimension`Indica que o símbolo é uma matriz multidimensional FORTRAN.

`SymTagCallSite`Indica que o símbolo representa o local de chamada.

`SymTagInlineSite`Indica que o símbolo representa o site embutido.

`SymTagBaseInterface`Indica que o símbolo é uma interface base.

`SymTagVectorType`Indica que o símbolo é um tipo de vetor.

`SymTagMatrixType`Indica que o símbolo é um tipo de matriz.

`SymTagHLSLType`Indica que o símbolo é um tipo de linguagem sombreador de alto nível.

## <a name="remarks"></a>Comentários
Todos os símbolos em um arquivo de depuração têm uma marca de identificação que especifica o tipo do símbolo.

Os valores nessa enumeração são retornados por uma chamada para o método [IDiaSymbol:: get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md) .

Os valores nessa enumeração são passados para os seguintes métodos para limitar o escopo da pesquisa a um tipo de símbolo específico:

- [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)

- [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)

- [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)

- [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)

- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)

- [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)

- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)

- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)

## <a name="requirements"></a>Requisitos
Cabeçalho: cvconst. h

## <a name="see-also"></a>Veja também
- [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [Hierarquia lexical de tipos de símbolo](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)
- [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)
- [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)
- [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)
- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)
- [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
