---
title: SymTagEnum | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- SymTagEnum enumeration
ms.assetid: 528a50cf-e13d-46ec-a98c-323d5d047de9
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 09462ee9d9223c79b4ee0dcf4e8a5efa37b4c796
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51783292"
---
# <a name="symtagenum"></a>SymTagEnum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Especifica o tipo do símbolo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
enum SymTagEnum {   
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
 `SymTagNull`  
 Indica que o símbolo não tem um tipo.  
  
 `SymTagExe`  
 Indica que o símbolo é um arquivo .exe. Há apenas um `SymTagExe` símbolo por repositório de símbolos. Ele serve como o escopo global e não tem um pai de léxico.  
  
 `SymTagCompiland`  
 Indica o símbolo compiland para cada componente de compiland do repositório de símbolos. Para aplicativos nativos, `SymTagCompiland` símbolos correspondem para os arquivos de objeto vinculados na imagem. Para alguns tipos de imagens do Microsoft Intermediate Language (MSIL), há um compiland por classe.  
  
 `SymTagCompilandDetails`  
 Indica que o símbolo contém atributos estendidos de compiland. Recuperar essas propriedades pode exigir o carregamento de símbolos de compiland.  
  
 `SymTagCompilandEnv`  
 Indica que o símbolo é uma cadeia de caracteres de ambiente definida para compiland.  
  
 `SymTagFunction`  
 Indica que o símbolo é uma função.  
  
 `SymTagBlock`  
 Indica que o símbolo é um bloco aninhado.  
  
 `SymTagData`  
 Indica que o símbolo de dados.  
  
 `SymTagAnnotation`  
 Indica que o símbolo é para uma anotação de código. Os filhos desse símbolo são cadeias de caracteres de constante de dados (`SymTagData`, `LocIsConstant`, `DataIsConstant`). A maioria dos clientes ignoram esse símbolo.  
  
 `SymTagLabel`  
 Indica que o símbolo é um rótulo.  
  
 `SymTagPublicSymbol`  
 Indica que o símbolo é um símbolo público. Para aplicativos nativos, esse símbolo é o símbolo externo de COFF encontrado durante a vinculação a imagem.  
  
 `SymTagUDT`  
 Indica que o símbolo é um tipo definido pelo usuário (estrutura, classe ou união).  
  
 `SymTagEnum`  
 Indica que o símbolo é uma enumeração.  
  
 `SymTagFunctionType`  
 Indica que o símbolo é um tipo de assinatura de função.  
  
 `SymTagPointerType`  
 Indica que o símbolo é um tipo de ponteiro.  
  
 `SymTagArrayType`  
 Indica que o símbolo é um tipo de matriz.  
  
 `SymTagBaseType`  
 Indica que o símbolo é um tipo base.  
  
 `SymTagTypedef`  
 Indica que o símbolo é um `typedef`, ou seja, um alias para outro tipo.  
  
 `SymTagBaseClass`  
 Indica que o símbolo é uma classe base de um tipo definido pelo usuário.  
  
 `SymTagFriend`  
 Indica que o símbolo é um amigo de um tipo definido pelo usuário.  
  
 `SymTagFunctionArgType`  
 Indica que o símbolo é um argumento de função.  
  
 `SymTagFuncDebugStart`  
 Indica que o símbolo é o local final do código de prólogo da função.  
  
 `SymTagFuncDebugEnd`  
 Indica que o símbolo é o local de início do código de epílogo da função.  
  
 `SymTagUsingNamespace`  
 Indica que o símbolo é um nome de namespace, o Active Directory no escopo atual.  
  
 `SymTagVTableShape`  
 Indica que o símbolo é uma descrição da tabela virtual.  
  
 `SymTagVTable`  
 Indica que o símbolo for um ponteiro da tabela virtual.  
  
 `SymTagCustom`  
 Indica que o símbolo é um símbolo personalizado e não é interpretado por DIA.  
  
 `SymTagThunk`  
 Indica que o símbolo é uma conversão usada para compartilhar dados entre 16 e o código de 32 bits.  
  
 `SymTagCustomType`  
 Indica que o símbolo é um símbolo de compilador personalizados.  
  
 `SymTagManagedType`  
 Indica que o símbolo é nos metadados.  
  
 `SymTagDimension`  
 Indica que o símbolo é uma matriz multidimensional do FORTRAN.  
  
 `SymTagCallSite`  
 Indica que o símbolo representa o site de chamada.  
  
 `SymTagInlineSite`  
 Indica que o símbolo representa o site embutido.  
  
 `SymTagBaseInterface`  
 Indica que o símbolo é uma interface de base.  
  
 `SymTagVectorType`  
 Indica que o símbolo é um tipo de vetor.  
  
 `SymTagMatrixType`  
 Indica que o símbolo é um tipo de matriz.  
  
 `SymTagHLSLType`  
 Indica que o símbolo é um tipo de linguagem de sombreador de nível alto.  
  
## <a name="remarks"></a>Comentários  
 Todos os símbolos em um arquivo de depuração têm uma marca de identifica que especifica o tipo do símbolo.  
  
 Os valores nesta enumeração são retornados por uma chamada para o [idiasymbol:: Get_symtag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md) método.  
  
 Os valores nesta enumeração são passados para os seguintes métodos para limitar o escopo da pesquisa para um tipo de símbolo específico:  
  
-   [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)  
  
-   [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)  
  
-   [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)  
  
-   [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)  
  
-   [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)  
  
-   [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)  
  
-   [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)  
  
-   [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: cvconst.h  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [Hierarquia lexical de tipos de símbolo](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)   
 [Idiasession:: Findsymbolbyaddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)   
 [Idiasession:: Findsymbolbyrva](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)   
 [Idiasession:: Findsymbolbyrvaex](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)   
 [Idiasession:: Findsymbolbytoken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)   
 [Idiasession:: Findsymbolbyva](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)   
 [Idiasession:: Findsymbolbyvaex](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)   
 [Idiasession:: Findchildren](../../debugger/debug-interface-access/idiasession-findchildren.md)   
 [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)



