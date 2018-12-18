---
title: IActiveScriptParse::ParseScriptText | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptParse.ParseScriptText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptParse_ParseScriptText
ms.assetid: 2d237d6c-cc65-415b-8808-72791304a136
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 70d17807b47468f2238c0254cc39b339df616411
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724526"
---
# <a name="iactivescriptparseparsescripttext"></a>IActiveScriptParse::ParseScriptText
Analisa o miniscript de código fornecido, adicionar declarações no namespace e avaliar o código conforme apropriado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
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
|`pstrCode`|[in] Endereço do texto miniscript para avaliar. A interpretação dessa cadeia de caracteres depende da linguagem de script.|  
|`pstrItemName`|[in] Endereço do nome do item que fornece o contexto no qual o miniscript será avaliada. Se esse parâmetro for NULL, o código é avaliado no contexto global do mecanismo de script.|  
|`punkContext`|[in] Endereço do objeto de contexto. Esse objeto é reservado para uso em um ambiente de depuração, onde tal um contexto pode ser fornecido pelo depurador para representar um contexto de tempo de execução ativado. Se esse parâmetro for NULL, o mecanismo usa `pstrItemName` para identificar o contexto.|  
|`pstrDelimiter`|[in] Endereço do delimitador final de miniscript. Quando `pstrCode` é analisada a partir de um fluxo de texto, o host normalmente usa um delimitador, como duas aspas ("), para detectar o fim do miniscript. Esse parâmetro especifica o delimitador que o host é usado, permitindo que o mecanismo de script fornecer algumas condicional pré-processamento primitivo (por exemplo, substituindo uma aspa simples ['] por duas aspas simples para uso como um delimitador). Exatamente como (e se) o script faz mecanismo use essas informações depende do mecanismo de script. Definir esse parâmetro como `NULL` se o host não tiver usado um delimitador para marcar o fim do miniscript.|  
|`dwSourceContextCookie`|[in] Cookie usado para fins de depuração.|  
|`ulStartingLineNumber`|[in] Valor de base zero que especifica a linha a análise começará no.|  
|`dwFlags`|[in] Sinalizadores associados com o miniscript. Pode ser uma combinação desses valores:|  
  
|Valor|Significado|  
|-----------|-------------|  
|SCRIPTTEXT_ISEXPRESSION|Se a diferença entre uma expressão computacional e uma instrução é importante, mas sintaticamente ambígua a linguagem de script, este sinalizador Especifica que o miniscript deve ser interpretado como uma expressão, em vez de uma instrução ou uma lista de instruções. Por padrão, as instruções são assumidas, a menos que a opção correta pode ser determinada da sintaxe do texto miniscript.|  
|SCRIPTTEXT_ISPERSISTENT|Indica que o código adicionado durante essa chamada deve ser salva se o mecanismo de script é salvo (por exemplo, por meio de uma chamada para `IPersist*::Save`), ou se o mecanismo de script é redefinido por meio de uma transição para o estado inicializado.|  
|SCRIPTTEXT_ISVISIBLE|Indica que o texto do script deve ser visível (e, portanto, pode ser chamado por nome) como um método global no espaço para nome do script.|  
  
|||  
|-|-|  
|`pvarResult`|[out] Endereço de um buffer que recebe os resultados do processamento de miniscript ou `NULL` se o chamador não espera que nenhum resultado (ou seja, o valor SCRIPTTEXT_ISEXPRESSION não está definido).|  
|`pexcepinfo`|[out] Endereço de uma estrutura que recebe informações de exceção. Essa estrutura é preenchida se `IActiveScriptParse::ParseScriptText` retorna DISP_E_EXCEPTION.|  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`DISP_E_EXCEPTION`|Ocorreu uma exceção no processamento do miniscript. O `pexcepinfo` parâmetro contém informações sobre a exceção.|  
|`E_INVALIDARG`|Um argumento era inválido.|  
|`E_POINTER`|Um ponteiro inválido foi especificado.|  
|`E_NOTIMPL`|Não há suporte para o método. O mecanismo de script não dá suporte a avaliação do tempo de execução de instruções ou expressões.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script está em estado não inicializado ou fechado, ou o sinalizador SCRIPTTEXT_ISEXPRESSION foi definido e o mecanismo de script está no estado inicializado).|  
|`OLESCRIPT_E_SYNTAX`|Ocorreu um erro de sintaxe não especificado no miniscript.|  
  
## <a name="remarks"></a>Comentários  
 Se o mecanismo de script está no estado inicializado, nenhum código realmente será avaliado durante essa chamada; em vez disso, esse código será enfileirado e executado quando o mecanismo de script é transferido para (ou por meio de) o estado iniciado. Execução não é permitida no estado inicializado, é um erro ao chamar esse método com o sinalizador SCRIPTTEXT_ISEXPRESSION no estado inicializado.  
  
 O miniscript pode ser uma expressão, uma lista de instruções ou nada permitido pela linguagem de script. Por exemplo, esse método é usado na avaliação de HTML \<SCRIPT > marca, que permite que instruções a serem executadas como a página HTML que está sendo construída, em vez de apenas compilá-los para o estado de script.  
  
 O código passado para este método deve ser uma parte válida e completa do código. Por exemplo, no VBScript é inválido chamar esse método uma vez com a Sub Function(x) e, em seguida, uma segunda vez com `End Sub`. O analisador não deve aguardar para a segunda chamada concluir a sub-rotina, mas em vez disso, deve gerar um erro de análise porque uma declaração sub-rotina foi iniciada mas não foram concluída.  
  
 Para obter mais informações sobre os estados de script, consulte a seção de estados do mecanismo de Script de [mecanismos de Script do Windows](../../winscript/windows-script-engines.md).  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptParse](../../winscript/reference/iactivescriptparse.md)