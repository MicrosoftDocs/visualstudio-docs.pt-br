---
title: Chame a pilha de avaliação | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- debugging [Debugging SDK], call stack evaluation
- call stacks, evaluation
ms.assetid: 373d6b49-0459-4cce-816e-05745a44fe49
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e3ab4877a1d6f772572f430c12c436ff5a4b8537
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51772073"
---
# <a name="call-stack-evaluation"></a>Avaliação de pilha de chamadas
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Para exibir os registros de ativação da pilha de chamadas durante o modo de interrupção, você deve implementar o [EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) método.  
  
## <a name="methods-for-evaluation"></a>Métodos de avaliação  
 Para um mecanismo de depuração simples (DE), pode haver apenas um quadro de pilha. Para examinar o quadro de pilha durante o modo de interrupção, você deve implementar os seguintes métodos de [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md).  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|Obtém o contexto de código para um quadro de pilha. O contexto do código representa o ponteiro de instrução atual em um quadro de pilha.|  
|[GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|Obtém o contexto do documento para um quadro de pilha. O contexto do documento representa o local atual no código-fonte para um quadro de pilha. Necessário para exibir o código-fonte, quando você for interrompido em um programa.|  
  
 Esses métodos exigem a implementação de vários métodos e interfaces relacionadas ao contexto. Portanto, você deve implementar o [GetDocumentContext](../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md) método e os seguintes métodos da [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md).  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|Obtém o intervalo de instrução de arquivo de um contexto de documento.|  
  
 Para enumerar os contextos de código, você deve implementar todos os métodos de [IEnumDebugCodeContexts2](../../extensibility/debugger/reference/ienumdebugcodecontexts2.md).  
  
## <a name="see-also"></a>Consulte também  
 [Controle de execução e avaliação de estado](../../extensibility/debugger/execution-control-and-state-evaluation.md)

