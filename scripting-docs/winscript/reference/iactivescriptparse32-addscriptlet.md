---
title: IActiveScriptParse32::AddScriptlet | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fcf11eb2-8e71-4cca-afda-a91791c243ff
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 7b4ea62bf8afa4247fc7c4fdbea40c6b7c772661
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724546"
---
# <a name="iactivescriptparse32addscriptlet"></a>IActiveScriptParse32::AddScriptlet
Adiciona um miniscript de código para o script. Esse método é usado em ambientes onde o estado persistente do script é entremeado com o documento de host e o host é responsável por restaurar o script, em vez da um `IPersist*` interface. Os exemplos primários são linguagens de scripts HTML que permitem miniscripts de código inserido no documento HTML a ser anexado à eventos intrínsecos (por exemplo, ONCLICK="button1.text='Exit'").  
  
## <a name="syntax"></a>Sintaxe  
  
```  
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
 [in] Endereço de um nome padrão para associar o miniscript. Se o miniscript não contém informações de nomenclatura (como no exemplo ONCLICK acima), esse nome será usado para identificar o miniscript. Se esse parâmetro for `NULL`, o mecanismo de script fabrica um nome exclusivo, se necessário.  
  
 `pstrCode`  
 [in] Endereço do texto miniscript a adicionar. A interpretação dessa cadeia de caracteres depende da linguagem de script.  
  
 `pstrItemName`  
 [in] Endereço de um buffer que contém o nome do item associado a este miniscript. Esse parâmetro, além de `pstrSubItemName`, identifica o objeto para o qual o miniscript é um manipulador de eventos.  
  
 `pstrSubItemName`  
 [in] Endereço de um buffer que contém o nome de um `subobject` do item nomeado com o qual este miniscript está associada; esse nome deve ser encontrado nas informações de tipo do item nomeado. Esse parâmetro é NULL se o miniscript deve ser associado ao item nomeado em vez de um `subitem`. Esse parâmetro, além de `pstrItemName`, identifica o objeto para o qual o miniscript é um manipulador de eventos.  
  
 `pstrEventName`  
 [in] Endereço de um buffer que contém o nome do evento para o qual o miniscript é um manipulador de eventos.  
  
 `pstrDelimiter`  
 [in] Endereço do delimitador final de miniscript. Quando o `pstrCode` parâmetro é analisado a partir de um fluxo de texto, o host normalmente usa um delimitador, como duas aspas ("), para detectar o fim do miniscript. Esse parâmetro especifica o delimitador que o host é usado, permitindo que o mecanismo de script fornecer algumas condicional pré-processamento primitivo (por exemplo, substituindo uma aspa simples ['] por duas aspas simples para uso como um delimitador). Exatamente como (e se) o script faz mecanismo use essas informações depende do mecanismo de script. Defina esse parâmetro como NULL se o host não tiver usado um delimitador para marcar o fim do miniscript.  
  
 `dwSourceContextCookie`  
 [in] Valor definido pelo aplicativo que é usado para fins de depuração.  
  
 `ulStartingLineNumber`  
 [in] Valor de base zero que especifica a linha a análise começará no.  
  
 `dwFlags`  
 [in] Sinalizadores associados com o miniscript. Pode ser uma combinação dos seguintes valores:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|SCRIPTTEXT_ISVISIBLE|Indica que o texto do script deve ser visível (e, portanto, pode ser chamado por nome) como um método global no espaço para nome do script.|  
|SCRIPTTEXT_ISPERSISTENT|Indica que o código adicionado durante essa chamada deve ser salva se o mecanismo de script é salvo (por exemplo, por meio de uma chamada para `IPersist*::Save`), ou se o mecanismo de script é redefinido por meio de uma transição para o estado inicializado. Para obter mais informações sobre esse estado, consulte estados de mecanismo de Script.|  
  
 `pbstrName` ,  
 [out] Nome real usado para identificar o miniscript. Deve ser em ordem de preferência: o nome especificado explicitamente no texto miniscript, o nome padrão fornecido no `pstrDefaultName`, ou um nome exclusivo sintetizadas pelo mecanismo de script.  
  
 `pexcepinfo` ,  
 [out] Endereço de uma estrutura que contém informações de exceção. Essa estrutura deve ser preenchida se DISP_E_EXCEPTION for retornado.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`DISP_E_EXCEPTION`|Ocorreu uma exceção na análise do miniscript. O `pexcepinfo` parâmetro contém informações sobre a exceção.|  
|`E_INVALIDARG`|Um argumento era inválido.|  
|`E_NOTIMPL`|Não há suporte para esse método; o mecanismo de script não oferece suporte à adição de miniscripts recebendo o evento.|  
|`E_POINTER`|Um ponteiro inválido foi especificado.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script ainda não foi carregado ou inicializado) e, portanto, a falha.|  
|`OLESCRIPT_E_INVALIDNAME`|O nome padrão fornecido é inválido nessa linguagem de script.|  
|`OLESCRIPT_E_SYNTAX`|Ocorreu um erro de sintaxe não especificado no miniscript.|  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptParse32](../../winscript/reference/iactivescriptparse32.md)