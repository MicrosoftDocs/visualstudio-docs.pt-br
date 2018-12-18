---
title: IDebugExpression::Start | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugExpression.Start
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugExpression::Start
ms.assetid: a7af3470-62b5-40f0-987d-63b6b22538b3
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 14d293649e3a6a87c7f594e244378dc2a7e15ac6
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727596"
---
# <a name="idebugexpressionstart"></a>IDebugExpression::Start
Começa a avaliação da expressão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT Start(  
   IDebugExpressionCallBack*  pdecb  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pdecb`  
 [in] Retorno de chamada para indicar quando a avaliação da expressão é concluída. Se esse parâmetro for `NULL`, nenhum evento é acionado e o cliente deve sondar o estado de expressão usando `QueryIsComplete`.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Esse método inicia a avaliação da expressão.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugExpression::Abort](../../winscript/reference/idebugexpression-abort.md)   
 [Interface IDebugExpression](../../winscript/reference/idebugexpression-interface.md)