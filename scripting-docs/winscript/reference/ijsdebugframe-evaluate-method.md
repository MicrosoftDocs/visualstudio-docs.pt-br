---
title: 'Método Ijsdebugframe: | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugFrame.Evaluate
apilocation:
- jscript9diag.dll
ms.assetid: 0ee61340-37b8-4fbb-a028-748b5315e279
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 38e826048e85456ca63e069de67701b1fc3e9f04
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727446"
---
# <a name="ijsdebugframeevaluate-method"></a>Método IJsDebugFrame::Evaluate
Avalie uma expressão no contexto deste quadro de pilha.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT Evaluate(  
   LPCOLESTR pExpressionText,  
   IJsDebugProperty **ppDebugProperty,  
   BSTR *pError  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pExpressionText`  
 [in] A expressão a ser avaliada.  
  
 `ppDebugProperty`  
 [out] Objeto que representa o navegador de propriedade.  
  
 `pError`  
 [out] A mensagem de erro, se ocorrer um erro.  
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="remarks"></a>Comentários  
 Retorna o seguinte: S_OK: avaliação for bem-sucedida, * ppDebugProperty contém o resultado da avaliação. S_FALSE: Avaliação gera um erro (ou não há suporte para a operação de avaliação), \*pError contém a mensagem de erro.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Interface IJsDebugFrame](../../winscript/reference/ijsdebugframe-interface.md)