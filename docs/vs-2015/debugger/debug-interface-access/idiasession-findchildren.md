---
title: 'Idiasession:: Findchildren | Microsoft Docs'
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
- IDiaSession::findChildren method
ms.assetid: 5d19046f-f668-4aa9-8788-95cda9a98997
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a4bb723009181d0a1b69fd0a69a96263e8c82506
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49903862"
---
# <a name="idiasessionfindchildren"></a>IDiaSession::findChildren
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Recupera todos os filhos de um identificador do pai especificado que corresponde ao tipo de nome e o símbolo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
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
 [in] Uma [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representa o pai do objeto. Se esse símbolo pai for uma função, módulo ou bloco, seus filhos léxicos são retornados em `ppResult`. Se o símbolo de pai for um tipo, seus filhos de classe são retornados. Se esse parâmetro for `NULL`, em seguida, `symtag` deve ser definida como `SymTagExe` ou `SymTagNull`, que retorna o escopo global (.exe arquivo).  
  
 `symtag`  
 [in] Especifica a marca de símbolo dos filhos a serem recuperados. Valores são tirados de [enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md) enumeração. Definido como `SymTagNull` para recuperar todos os filhos.  
  
 `name`  
 [in] Especifica o nome dos filhos a serem recuperados. Definido como `NULL` para todos os filhos a serem recuperados.  
  
 `compareFlags`  
 [in] Especifica as opções de comparação aplicadas a correspondência de nomes. Os valores do [enumeração NameSearchOptions](../../debugger/debug-interface-access/namesearchoptions.md) enumeração pode ser usada sozinho ou em combinação.  
  
 `ppResult`  
 [out] Retorna um [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) recuperado do objeto que contém a lista de símbolos de filho.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como localizar as variáveis locais da função `pFunc` que corresponder ao nome `szVarName`.  
  
```cpp#  
IDiaEnumSymbols* pEnum;  
pSession->findChildren( pFunc, SymTagData, szVarName, nsCaseSensitive, &pEnum );  
```  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)   
 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)   
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [Enumeração NameSearchOptions](../../debugger/debug-interface-access/namesearchoptions.md)   
 [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)



