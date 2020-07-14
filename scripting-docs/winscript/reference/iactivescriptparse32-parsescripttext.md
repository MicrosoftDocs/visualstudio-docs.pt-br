---
title: IActiveScriptParse32::P arseScriptText | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: f33e454c-69d8-4cab-9150-d1e7fd04786d
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: e26b5cb1790cab38a6544a04307b7e336a952519
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835362"
---
# <a name="iactivescriptparse32parsescripttext"></a>IActiveScriptParse32::ParseScriptText
Analisa o scriptlet de código fornecido, adicionando declarações ao namespace e avaliando o código conforme apropriado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT ParseScriptText(  
    LPCOLESTR pstrCode,              // address of scriptlet text  
    LPCOLESTR pstrItemName,          // address of item name  
    IUnknown *punkContext,           // address of debugging context  
    LPCOLESTR pstrDelimiter,         // address of end-of-scriptlet delimiter  
    DWORD_PTR dwSourceContextCookie, // cookie for debugging  
    ULONG ulStartingLineNumber,      // starting line of the script  
    DWORD dwFlags,                   // scriptlet flags  
    VARIANT *pvarResult,             // address of buffer for results  
    EXCEPINFO *pexcepinfo            // address of buffer for error data  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
  
|||  
|-|-|  
|`pstrCode`|no Endereço do texto de scriptlet a ser avaliado. A interpretação dessa cadeia de caracteres depende da linguagem de script.|  
|`pstrItemName`|no Endereço do nome do item que fornece o contexto no qual o scriptlet deve ser avaliado. Se esse parâmetro for nulo, o código será avaliado no contexto global do mecanismo de script.|  
|`punkContext`|no Endereço do objeto de contexto. Esse objeto é reservado para uso em um ambiente de depuração, onde tal contexto pode ser fornecido pelo depurador para representar um contexto de tempo de execução ativo. Se esse parâmetro for nulo, o mecanismo usará `pstrItemName` para identificar o contexto.|  
|`pstrDelimiter`|no Endereço do delimitador de fim do scriptlet. Quando `pstrCode` é analisado a partir de um fluxo de texto, o host geralmente usa um delimitador, como duas aspas simples (' '), para detectar o final do scriptlet. Esse parâmetro especifica o delimitador usado pelo host, permitindo que o mecanismo de script forneça algum pré-processamento primitivo condicional (por exemplo, substituindo uma aspa simples ['] por duas aspas simples para uso como um delimitador). Exatamente como (e se) o mecanismo de script usa essas informações depende do mecanismo de script. Defina esse parâmetro como `NULL` se o host não tivesse usado um delimitador para marcar o final do scriptlet.|  
|`dwSourceContextCookie`|no Cookie usado para fins de depuração.|  
|`ulStartingLineNumber`|no Valor de base zero que especifica em qual linha a análise será iniciada.|  
|`dwFlags`|no Sinalizadores associados ao scriptlet. Pode ser uma combinação desses valores:|  
  
|Valor|Significado|  
|-----------|-------------|  
|SCRIPTTEXT_ISEXPRESSION|Se a distinção entre uma expressão computacional e uma instrução for importante, mas sintaticamente ambígua na linguagem de script, esse sinalizador especificará que o scriptlet deve ser interpretado como uma expressão, em vez de uma instrução ou uma lista de instruções. Por padrão, são presumidas instruções a menos que a escolha correta possa ser determinada a partir da sintaxe do texto do scriptlet.|  
|SCRIPTTEXT_ISPERSISTENT|Indica que o código adicionado durante essa chamada deve ser salvo se o mecanismo de script for salvo (por exemplo, por meio de uma chamada para `IPersist*::Save` ) ou se o mecanismo de script for redefinido por meio de uma transição de volta para o estado inicializado.|  
|SCRIPTTEXT_ISVISIBLE|Indica que o texto do script deve estar visível (e, portanto, pode ser chamado por nome) como um método global no espaço de nome do script.|  
  
|||  
|-|-|  
|`pvarResult`|fora Endereço de um buffer que recebe os resultados do processamento de scriptlet, ou `NULL` se o chamador não espera nenhum resultado (ou seja, o valor de SCRIPTTEXT_ISEXPRESSION não está definido).|  
|`pexcepinfo`|fora Endereço de uma estrutura que recebe informações de exceção. Essa estrutura será preenchida se o `IActiveScriptParse::ParseScriptText` retornar DISP_E_EXCEPTION.|  
  
## <a name="return-value"></a>Valor Retornado  
 Retorna um dos seguintes valores:  
  
|Valor Retornado|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`DISP_E_EXCEPTION`|Ocorreu uma exceção no processamento do scriptlet. O `pexcepinfo` parâmetro contém informações sobre a exceção.|  
|`E_INVALIDARG`|Um argumento era inválido.|  
|`E_POINTER`|Um ponteiro inválido foi especificado.|  
|`E_NOTIMPL`|Não há suporte para esse método. O mecanismo de script não dá suporte à avaliação em tempo de execução de expressões ou instruções.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script está no estado não inicializado ou fechado, ou o sinalizador de SCRIPTTEXT_ISEXPRESSION foi definido e o mecanismo de script está no estado inicializado).|  
|`OLESCRIPT_E_SYNTAX`|Ocorreu um erro de sintaxe não especificado no scriptlet.|  
  
## <a name="remarks"></a>Comentários  
 Se o mecanismo de script estiver no estado inicializado, nenhum código será realmente avaliado durante essa chamada; em vez disso, esse código é colocado em fila e executado quando o mecanismo de script é transferido para (ou até) o estado iniciado. Como a execução não é permitida no estado inicializado, é um erro chamar esse método com o sinalizador SCRIPTTEXT_ISEXPRESSION quando estiver no estado inicializado.  
  
 O scriptlet pode ser uma expressão, uma lista de instruções ou qualquer coisa permitida pela linguagem de script. Por exemplo, esse método é usado na avaliação da \<SCRIPT> marca HTML, que permite que as instruções sejam executadas à medida que a página HTML está sendo construída, em vez de apenas compilá-las no estado do script.  
  
 O código passado para esse método deve ser uma parte válida e completa do código. Por exemplo, no VBScript, é ilegal chamar esse método uma vez com sub function (x) e, em seguida, uma segunda vez com `End Sub` . O analisador não deve aguardar a segunda chamada para concluir a sub-rotina, mas, em vez disso, deve gerar um erro de análise porque uma declaração de sub-rotina foi iniciada, mas não foi concluída.  
  
 Para obter mais informações sobre os Estados de script, consulte a seção Estados de mecanismo de script dos [mecanismos de script do Windows](../../winscript/windows-script-engines.md).  
  
## <a name="see-also"></a>Confira também  
 [IActiveScriptParse32](../../winscript/reference/iactivescriptparse32.md)