---
title: IDebugExpressionContext::ParseLanguageText | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugExpressionContext.ParseLanguageText
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugExpressionContext::ParseLanguageText
ms.assetid: 650cb016-7d80-4011-b264-780f871a3466
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e455768b7d38096c64ab61f2b36aeba871ddf0bc
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729236"
---
# <a name="idebugexpressioncontextparselanguagetext"></a>IDebugExpressionContext::ParseLanguageText
Cria uma expressão de depuração para o texto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT ParseLanguageText(  
   LPCOLESTR           pstrCode,  
   UINT                nRadix,  
   LPCOLESTR           pstrDelimiter,  
   DWORD               dwFlags,  
   IDebugExpression**  ppe  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pstrCode`  
 [in] Fornece o texto da expressão ou instrução (ões).  
  
 `nRadix`  
 [in] Base a ser usado.  
  
 `pstrDelimiter`  
 [in] O delimitador de final do bloco de script. Quando `pstrCode` é analisada a partir de um fluxo de texto, o host normalmente usa um delimitador, como duas aspas ("), para detectar o fim do bloco de script. Esse parâmetro especifica o delimitador que o host é usado, permitindo que o mecanismo de script fornecer algumas condicional pré-processamento primitivo (por exemplo, substituindo uma aspa simples ['] por duas aspas simples para uso como um delimitador). Exatamente como (e se) o mecanismo de script usa essas informações dependem do mecanismo de script. Definir esse parâmetro como `NULL` se o host não tiver usado um delimitador para marcar o fim do bloco de script.  
  
 `dwFlags`  
 [in] Combinação dos sinalizadores de texto de depuração a seguir:  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|DEBUG_TEXT_ISEXPRESSION|0x00000001|Indica que o texto é uma expressão em vez de uma instrução. Este sinalizador pode afetar a maneira na qual o texto é analisado por alguns idiomas.|  
|DEBUG_TEXT_RETURNVALUE|0x00000002|Se um valor de retorno estiver disponível, ele será usado pelo chamador.|  
|DEBUG_TEXT_NOSIDEEFFECTS|0x00000004|Não permite efeitos colaterais. Se esse sinalizador estiver definido, a avaliação da expressão não deve alterar nenhum estado de tempo de execução.|  
|DEBUG_TEXT_ALLOWBREAKPOINTS|0x00000008|Permite que os pontos de interrupção durante a avaliação do texto. Se este sinalizador não for definido, em seguida, os pontos de interrupção são ignorados durante a avaliação do texto.|  
|DEBUG_TEXT_ALLOWERRORREPORT|0x00000010|Permite que os relatórios de erro durante a avaliação do texto. Se este sinalizador não for definido, em seguida, erros não são relatados ao host durante a avaliação.|  
|DEBUG_TEXT_EVALUATETOCODECONTEXT|0x00000020|Indica a expressão será avaliada em um contexto de código em vez de executar a própria expressão|  
  
 `ppe`  
 [out] Retorna a expressão de depuração para o texto especificado.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Esse método cria uma expressão de depuração para o texto especificado.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDebugExpressionContext](../../winscript/reference/idebugexpressioncontext-interface.md)