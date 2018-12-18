---
title: IActiveScriptParseProcedureOld::ParseProcedureText | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptParseProcedureOld.ParseProcedureText
apilocation:
- jscript.dll
helpviewer_keywords:
- IActiveScriptParseProcedureOld::ParseProcedureText
ms.assetid: 21a21313-35ce-432d-b9a6-7999065f19ac
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cab546deb390535fa8ff71e116a0ad42d33cc104
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724996"
---
# <a name="iactivescriptparseprocedureoldparseproceduretext"></a>IActiveScriptParseProcedureOld::ParseProcedureText
Analisa o procedimento de código fornecido e adiciona um procedimento de anônimo para o espaço de nome.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT ParseProcedureText(  
   LPCOLESTR    pstrCode,  
   LPCOLESTR    pstrFormalParams,  
   LPCOLESTR    pstrItemName,  
   IUnknown*    punkContext,  
   LPCOLESTR    pstrDelimiter,  
   DWORD_PTR    dwSourceContextCookie,  
   ULONG        ulStartingLineNumber,  
   DWORD        dwFlags,  
   IDispatch**  ppdisp  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pstrCode`  
 [in] O texto do procedimento para avaliar. A interpretação dessa cadeia de caracteres depende da linguagem de script.  
  
 `pstrFormalParams`  
 [in] Nomes de parâmetro formal para o procedimento. Os nomes de parâmetro devem ser separados com os delimitadores apropriados para o mecanismo de script. Os nomes não devem estar entre parênteses.  
  
 `pstrItemName`  
 [in] O nome do item nomeado que fornece o contexto no qual o procedimento será avaliada. Se esse parâmetro for `NULL`, o código é avaliado no contexto global do mecanismo de script.  
  
 `punkContext`  
 [in] O objeto de contexto. Esse objeto é reservado para uso em um ambiente de depuração, onde tal um contexto pode ser fornecido pelo depurador para representar um contexto de tempo de execução ativado. Se esse parâmetro for `NULL`, usa o mecanismo `pstrItemName` para identificar o contexto.  
  
 `pstrDelimiter`  
 [in] O delimitador de término do procedimento. Quando `pstrCode` é analisada a partir de um fluxo de texto, o host normalmente usa um delimitador, como duas aspas ("), para detectar o fim do procedimento. Esse parâmetro especifica o delimitador que o host é usado, permitindo que o mecanismo de script fornecer algumas condicional, primitivos de pré-processamento (por exemplo, substituindo uma aspa simples ['] por duas aspas simples para uso como um delimitador). Exatamente como (e se) o mecanismo de script usa essas informações dependem do mecanismo de script. Definir esse parâmetro como `NULL` se o host não tiver usado um delimitador para marcar o fim do procedimento.  
  
 `dwSourceContextCookie`  
 [in] Valor definido pelo aplicativo que é usado para fins de depuração.  
  
 `ulStartingLineNumber`  
 [in] Valor de base zero que especifica a linha na qual a análise será iniciado.  
  
 `dwFlags`  
 [in] Sinalizadores associados com o procedimento. Pode ser uma combinação desses valores.  
  
|Constante|Valor|Significado|  
|--------------|-----------|-------------|  
|SCRIPTPROC_ISEXPRESSION|0x00000020|Indica que o código em `pstrCode` é uma expressão que representa o valor de retorno do procedimento.|  
|SCRIPTPROC_IMPLICIT_THIS|0x00000100|Indica que o `this` ponteiro está incluído no escopo do procedimento.|  
|SCRIPTPROC_IMPLICIT_PARENTS|0x00000200|Indica que os pais do `this` ponteiro são incluídos no escopo do procedimento.|  
  
 `ppdisp`  
 [out] Retorna um wrapper de expedição onde o método padrão é o procedimento analisado por este método.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
|`E_INVALIDARG`|Um argumento era inválido.|  
|`E_POINTER`|Um ponteiro inválido foi especificado.|  
|`E_NOTIMPL`|Não há suporte para o método. O mecanismo de script não oferece suporte a adição de tempo de execução de procedimentos para o espaço para nome.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script está no estado não inicializado ou fechado).|  
|`OLESCRIPT_E_SYNTAX`|Ocorreu um erro de sintaxe não especificado no procedimento.|  
|`S_FALSE`|O mecanismo de script não dá suporte a um objeto de expedição; o `ppdisp`parâmetro está definido como `NULL`.|  
  
## <a name="remarks"></a>Comentários  
 Nenhum código de script é avaliado durante essa chamada; em vez disso, o procedimento é compilado em um método em `ppdisp` onde ele pode ser chamado pelo script mais tarde.  
  
 Essa interface é preterida em favor do `IActiveScriptParseProcedure` interface. O `IActiveScriptParseProcedure::ParseProcedureText` método é semelhante a este método, mas permite que o nome do procedimento seja especificado. Em todas as circunstâncias, `IActiveScriptParseProcedure::ParseProcedureText` deve ser usado.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IActiveScriptParseProcedureOld](../../winscript/reference/iactivescriptparseprocedureold-interface.md)   
 [IActiveScriptParseProcedure::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedure-parseproceduretext.md)