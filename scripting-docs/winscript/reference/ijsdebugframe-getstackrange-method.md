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
- IJsDebugFrame.GetStackRange
apilocation:
- jscript9diag.dll
ms.assetid: a6d1d8be-efc0-442d-9756-1959c8f102bd
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cce4d4542f4f76657475636ad6d8e430e1909181
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727866"
---
# <a name="ijsdebugframegetstackrange-method"></a>Método IJsDebugFrame::GetStackRange
Retorna o intervalo de endereço absoluto do quadro de pilhas lógico do JavaScript.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetStackRange(  
   UINT64 *pStart,  
   UINT64 *pEnd  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pStart`  
 [out] Inferior a maioria dos ponteiro de pilha do quadro.  
  
 `pEnd`  
 [out] Ponteiro de pilha mais superior do quadro.  
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="remarks"></a>Comentários  
 Esse método é útil para juntando rastreamentos de pilha intercalada coletados a partir de vários tempos de execução. O início, fim ponteiros de pilha podem abranger vários registros de ativação de máquina física (para os quadros de tempo de execução de JavaScript interpretados). Iniciar > terminar como a pilha cresce de alto para baixo endereço.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Interface IJsDebugFrame](../../winscript/reference/ijsdebugframe-interface.md)