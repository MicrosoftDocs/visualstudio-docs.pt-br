---
title: 'Método: Getdocumentpositionwithname | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugFrame.GetDocumentPositionWithName
apilocation:
- jscript9diag.dll
ms.assetid: 1d994714-2c87-4a9e-ae14-a15eec9520c7
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 49afb5903e190280d226a24b22dc389041861c52
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24728046"
---
# <a name="ijsdebugframegetdocumentpositionwithname-method"></a>Método IJsDebugFrame::GetDocumentPositionWithName
Retorna a posição atual deste quadro de pilha dentro do documento de nível de usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetDocumentPositionWithName(  
   BSTR *pDocumentName,  
   DWORD *pLine,  
   DWORD *pColumn  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pDocumentName`  
 [out] Para scripts estáticos, uma URL para o documento. Para scripts dinâmicos, um nome que contém o tipo de script (por exemplo, código de avaliação, o código de função etc.) é retornado.  
  
 `pLine`  
 [out] posição de linha de base 1 no documento.  
  
 `pColumn`  
 [out] posição de linha de base 1 no documento.  
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Interface IJsDebugFrame](../../winscript/reference/ijsdebugframe-interface.md)