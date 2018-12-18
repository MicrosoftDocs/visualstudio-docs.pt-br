---
title: Interface IJsDebugFrame | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 5af46b18-9d25-4a23-b8d1-fa23bea3efcf
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f09a147375661fb52b88f531aff981897138adff
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729606"
---
# <a name="ijsdebugframe-interface"></a>Interface IJsDebugFrame
Representa um registro de ativação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IJsDebugFrame : public IUnknown;  
```  
  
## <a name="members"></a>Membros  
  
### <a name="public-methods"></a>Métodos Públicos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[Método IJsDebugFrame::Evaluate](../../winscript/reference/ijsdebugframe-evaluate-method.md)|Avalie uma expressão no contexto deste quadro de pilha.|  
|[Método IJsDebugFrame::GetDebugProperty](../../winscript/reference/ijsdebugframe-getdebugproperty-method.md)|Retorna um navegador de propriedade para este quadro de pilhas.|  
|[Método IJsDebugFrame::GetDocumentPositionWithId](../../winscript/reference/ijsdebugframe-getdocumentpositionwithid-method.md)|Retorna a posição atual deste quadro de pilha dentro do documento de nível de usuário.|  
|[Método IJsDebugFrame::GetDocumentPositionWithName](../../winscript/reference/ijsdebugframe-getdocumentpositionwithname-method.md)|Retorna a posição atual deste quadro de pilha dentro do documento de nível de usuário.|  
|[Método IJsDebugFrame::GetName](../../winscript/reference/ijsdebugframe-getname-method.md)|Obtém o nome amigável do quadro de pilhas.|  
|[Método IJsDebugFrame::GetReturnAddress](../../winscript/reference/ijsdebugframe-getreturnaddress-method.md)|Obtém o endereço de retorno enviado a 'start' (consulte GetStackRange) do quadro.|  
|[Método IJsDebugFrame::GetStackRange](../../winscript/reference/ijsdebugframe-getstackrange-method.md)|Retorna o intervalo de endereço absoluto do quadro de pilhas lógico do JavaScript.|  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Referência de interfaces de script do Windows](../../winscript/reference/windows-script-interfaces-reference.md)