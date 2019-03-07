---
title: 'Método ijsdebugframe:: Getdocumentpositionwithname | Microsoft Docs'
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
ms.openlocfilehash: d6333f9c52c3ab4e0cd01c34f5e5228721aa55b4
ms.sourcegitcommit: 116e9614867e0b3c627ce9001012a4c39435a42b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54093828"
---
# <a name="ijsdebugframegetdocumentpositionwithname-method"></a>Método IJsDebugFrame::GetDocumentPositionWithName
Retorna a posição atual deste quadro de pilha dentro do documento de nível de usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetDocumentPositionWithName(  
   BSTR *pDocumentName,  
   DWORD *pLine,  
   DWORD *pColumn  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pDocumentName`  
 [out] Para scripts estáticos, uma URL para o documento. Para scripts dinâmicos, um nome contendo o tipo de script (por exemplo, o código de avaliação, o código de função etc.) será retornado.  
  
 `pLine`  
 [out] posição de linha de base 1 dentro do documento.  
  
 `pColumn`  
 [out] posição de linha de base 1 dentro do documento.  
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Interface IJsDebugFrame](../../winscript/reference/ijsdebugframe-interface.md)