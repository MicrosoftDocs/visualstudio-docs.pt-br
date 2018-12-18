---
title: IActiveScriptParseProcedure32::ParseProcedureText | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ede37171-2f1e-4467-a358-17bd4a4f1869
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 2f36160ab9dca3ccc99aed1068b7e94fe1b7675d
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724786"
---
# <a name="iactivescriptparseprocedure32parseproceduretext"></a>IActiveScriptParseProcedure32::ParseProcedureText
Analisa o procedimento de código fornecido e adiciona o procedimento para o espaço de nome.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT ParseProcedureText(  
    LPCOLESTR pstrCode,              // address of procedure text  
    LPCOLESTR pstrFormalParams,      // address of formal parameter names  
    LPCOLESTR pstrProcedureName,     // address of procedure name  
    LPCOLESTR pstrItemName,          // address of item name  
    IUnknown *punkContext,           // address of debugging context  
    LPCOLESTR pstrDelimiter,         // address of end-of-procedure delimiter  
    DWORD_PTR dwSourceContextCookie, // application-defined value for debugging  
    ULONG ulStartingLineNumber,      // starting line of the script  
    DWORD dwFlags,                   // procedure flags  
    IDispatch **ppdisp               // receives IDispatch pointer  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pstrCode`  
 [in] Endereço de avaliar o texto do procedimento. A interpretação dessa cadeia de caracteres depende da linguagem de script.  
  
 `pstrFormalParams`  
 [in] Endereço de nomes de parâmetro formal para o procedimento. Os nomes de parâmetro devem ser separados com os delimitadores apropriados para o mecanismo de script. Os nomes não devem estar entre parênteses.  
  
 `pstrProcedureName`  
 [in] Endereço do nome do procedimento a ser analisada.  
  
 `pstrItemName`  
 [in] Endereço do nome do item que fornece o contexto no qual o procedimento será avaliada. Se esse parâmetro for `NULL`, o código é avaliado no contexto global do mecanismo de script.  
  
 `punkContext`  
 [in] Endereço do objeto de contexto. Esse objeto é reservado para uso em um ambiente de depuração, onde tal um contexto pode ser fornecido pelo depurador para representar um contexto de tempo de execução ativado. Se esse parâmetro for `NULL`, usa o mecanismo `pstrItemName` para identificar o contexto.  
  
 `pstrDelimiter`  
 [in] Endereço do delimitador final do procedimento. Quando `pstrCode` é analisada a partir de um fluxo de texto, o host normalmente usa um delimitador, como duas aspas ("), para detectar o fim do procedimento. Esse parâmetro especifica o delimitador que o host é usado, permitindo que o mecanismo de script fornecer algumas condicional pré-processamento primitivo (por exemplo, substituindo uma aspa simples ['] por duas aspas simples para uso como um delimitador). Exatamente como (e se) o script faz mecanismo use essas informações depende do mecanismo de script. Definir esse parâmetro como `NULL` se o host não tiver usado um delimitador para marcar o fim do procedimento.  
  
 `dwSourceContextCookie`  
 [in] Valor definido pelo aplicativo que é usado para fins de depuração.  
  
 `ulStartingLineNumber`  
 [in] Valor de base zero que especifica a linha a análise começará no.  
  
 `dwFlags`  
 [in] Sinalizadores associados com o procedimento. Pode ser uma combinação desses valores:  
  
|Valor|Significado|  
|-----------|-------------|  
|SCRIPTPROC_ISEXPRESSION|Indica que o código em `pstrCode` é uma expressão que representa o valor de retorno do procedimento. Por padrão, o código pode conter uma expressão, uma lista de instruções ou qualquer outro permitido em um procedimento de linguagem de script.|  
|SCRIPTPROC_IMPLICIT_THIS|Indica que o `this` ponteiro está incluído no escopo do procedimento.|  
|SCRIPTPROC_IMPLICIT_PARENTS|Indica que os pais do `this` ponteiro são incluídos no escopo do procedimento.|  
  
 `ppdisp`  
 [out] Endereço do ponteiro para o objeto que contém o script global métodos e propriedades. Se o mecanismo de script não dá suporte a tipo de objeto, `NULL` será retornado.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`E_INVALIDARG`|Um argumento era inválido.|  
|`E_POINTER`|Um ponteiro inválido foi especificado.|  
|`E_NOTIMPL`|Não há suporte para o método. O mecanismo de script não oferece suporte a adição de tempo de execução de procedimentos para o espaço para nome.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script está no estado não inicializado ou fechado).|  
|`OLESCRIPT_E_SYNTAX`|Ocorreu um erro de sintaxe não especificado no procedimento.|  
|`S_FALSE`|O mecanismo de script não dá suporte a um objeto de expedição; o `ppdisp` parâmetro está definido como `NULL`.|  
  
## <a name="remarks"></a>Comentários  
 Nenhum código de script é avaliado durante essa chamada; em vez disso, o procedimento é compilado para o estado de script em que ele pode ser chamado pelo script mais tarde.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptParseProcedure32](../../winscript/reference/iactivescriptparseprocedure32.md)