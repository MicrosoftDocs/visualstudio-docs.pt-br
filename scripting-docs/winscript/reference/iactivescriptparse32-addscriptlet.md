---
title: 'IActiveScriptParse32:: AddScriptlet | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: fcf11eb2-8e71-4cca-afda-a91791c243ff
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 9ec8395f6c8f404a1d9010234da030c47594e087
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835739"
---
# <a name="iactivescriptparse32addscriptlet"></a>IActiveScriptParse32::AddScriptlet
Adiciona um Scriptlet de código ao script. Esse método é usado em ambientes em que o estado persistente do script é entrelaçado com o documento host e o host é responsável por restaurar o script, em vez de uma `IPersist*` interface. Os exemplos principais são linguagens de script HTML que permitem que scriptlets de código inserido no documento HTML seja anexado a eventos intrínsecos (por exemplo, OnClick = "Button1. Text = ' Exit '").  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT AddScriptlet(  
    LPCOLESTR pstrDefaultName,       // address of default name of scriptlet  
    LPCOLESTR pstrCode,              // address of scriptlet text  
    LPCOLESTR pstrItemName,          // address of item name  
    LPCOLESTR pstrSubItemName,       // address of subitem name  
    LPCOLESTR pstrEventName,         // address of event name  
    LPCOLESTR pstrDelimiter,         // address of end-of-scriptlet delimiter  
    DWORD_PTR dwSourceContextCookie, // application-defined value for debugging  
    ULONG ulStartingLineNumber,      // starting line of the script  
    DWORD dwFlags,                   // scriptlet flags  
    BSTR *pbstrName,                 // address of actual name of scriptlet  
    EXCEPINFO *pexcepinfo            // address of exception information  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pstrDefaultName`  
 no Endereço de um nome padrão a ser associado ao scriptlet. Se o scriptlet não contiver informações de nomenclatura (como no exemplo OnClick acima), esse nome será usado para identificar o scriptlet. Se esse parâmetro for `NULL` , o mecanismo de script fabricará um nome exclusivo, se necessário.  
  
 `pstrCode`  
 no Endereço do texto de scriptlet a ser adicionado. A interpretação dessa cadeia de caracteres depende da linguagem de script.  
  
 `pstrItemName`  
 no Endereço de um buffer que contém o nome do item associado a este scriptlet. Esse parâmetro, além de `pstrSubItemName` , identifica o objeto para o qual o scriptlet é um manipulador de eventos.  
  
 `pstrSubItemName`  
 no Endereço de um buffer que contém o nome de um `subobject` Item nomeado ao qual este scriptlet está associado; esse nome deve ser encontrado nas informações de tipo do item nomeado. Esse parâmetro será nulo se o scriptlet for associado ao item nomeado em vez de um `subitem` . Esse parâmetro, além de `pstrItemName` , identifica o objeto específico para o qual o scriptlet é um manipulador de eventos.  
  
 `pstrEventName`  
 no Endereço de um buffer que contém o nome do evento para o qual o scriptlet é um manipulador de eventos.  
  
 `pstrDelimiter`  
 no Endereço do delimitador de fim do scriptlet. Quando o `pstrCode` parâmetro é analisado a partir de um fluxo de texto, o host geralmente usa um delimitador, como duas aspas simples (' '), para detectar o final do scriptlet. Esse parâmetro especifica o delimitador usado pelo host, permitindo que o mecanismo de script forneça algum pré-processamento primitivo condicional (por exemplo, substituindo uma aspa simples ['] por duas aspas simples para uso como um delimitador). Exatamente como (e se) o mecanismo de script usa essas informações depende do mecanismo de script. Defina esse parâmetro como NULL se o host não tiver usado um delimitador para marcar o final do scriptlet.  
  
 `dwSourceContextCookie`  
 no Valor definido pelo aplicativo que é usado para fins de depuração.  
  
 `ulStartingLineNumber`  
 no Valor de base zero que especifica em qual linha a análise será iniciada.  
  
 `dwFlags`  
 no Sinalizadores associados ao scriptlet. Pode ser uma combinação dos seguintes valores:  
  
|Valor Retornado|Significado|  
|------------------|-------------|  
|SCRIPTTEXT_ISVISIBLE|Indica que o texto do script deve estar visível (e, portanto, pode ser chamado por nome) como um método global no espaço de nome do script.|  
|SCRIPTTEXT_ISPERSISTENT|Indica que o código adicionado durante essa chamada deve ser salvo se o mecanismo de script for salvo (por exemplo, por meio de uma chamada para `IPersist*::Save` ) ou se o mecanismo de script for redefinido por meio de uma transição de volta para o estado inicializado. Para obter mais informações sobre esse Estado, consulte script engine Statess.|  
  
 `pbstrName` ,  
 fora Nome real usado para identificar o scriptlet. Isso deve ser em ordem de preferência: um nome especificado explicitamente no texto do scriptlet, o nome padrão fornecido em `pstrDefaultName` ou um nome exclusivo sintetizado pelo mecanismo de script.  
  
 `pexcepinfo` ,  
 fora Endereço de uma estrutura que contém informações de exceção. Essa estrutura deve ser preenchida se DISP_E_EXCEPTION for retornada.  
  
## <a name="return-value"></a>Valor Retornado  
 Retorna um dos seguintes valores:  
  
|Valor Retornado|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`DISP_E_EXCEPTION`|Ocorreu uma exceção na análise do scriptlet. O `pexcepinfo` parâmetro contém informações sobre a exceção.|  
|`E_INVALIDARG`|Um argumento era inválido.|  
|`E_NOTIMPL`|Não há suporte para esse método; o mecanismo de script não dá suporte à adição de scriptlets de coletor de eventos.|  
|`E_POINTER`|Um ponteiro inválido foi especificado.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script ainda não foi carregado ou inicializado) e, portanto, falhou.|  
|`OLESCRIPT_E_INVALIDNAME`|O nome padrão fornecido é inválido nesta linguagem de script.|  
|`OLESCRIPT_E_SYNTAX`|Ocorreu um erro de sintaxe não especificado no scriptlet.|  
  
## <a name="see-also"></a>Confira também  
 [IActiveScriptParse32](../../winscript/reference/iactivescriptparse32.md)