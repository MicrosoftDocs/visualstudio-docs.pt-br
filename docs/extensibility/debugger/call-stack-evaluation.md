---
title: Chamar a avaliação da pilha | Microsoft Docs
description: Saiba mais sobre o método EnumFrameInfo e como implementá-lo para exibir os quadros de pilha da pilha de chamada durante o modo de quebra.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], call stack evaluation
- call stacks, evaluation
ms.assetid: 373d6b49-0459-4cce-816e-05745a44fe49
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 059c42349c7f8e681709d69104cf65a6fc245206
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898533"
---
# <a name="call-stack-evaluation"></a>Avaliação da pilha de chamada
Para exibir os quadros de pilha da pilha de chamada durante o modo de quebra, você deve implementar o [método EnumFrameInfo.](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)

## <a name="methods-for-evaluation"></a>Métodos para avaliação
 Para um DE (mecanismo de depuração) simples, pode haver apenas um quadro de pilha. Para examinar o quadro de pilha durante o modo de quebra, você deve implementar os seguintes métodos de [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md).

|Método|Descrição|
|------------|-----------------|
|[GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|Obtém o contexto de código para um quadro de pilha. O contexto de código representa o ponteiro de instrução atual em um quadro de pilha.|
|[GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|Obtém o contexto do documento para um quadro de pilha. O contexto do documento representa o local atual no código-fonte de um quadro de pilha. Necessário para exibir o código-fonte quando você é interrompido em um programa.|

 Esses métodos exigem a implementação de várias interfaces e métodos relacionados ao contexto. Portanto, você deve implementar o [método GetDocumentContext](../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md) e os seguintes métodos de [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md).

|Método|Descrição|
|------------|-----------------|
|[GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|Obtém o intervalo de instrução de arquivo de um contexto de documento.|

 Para enumerar contextos de código, você deve implementar todos os métodos de [IEnumDebugCodeContexts2](../../extensibility/debugger/reference/ienumdebugcodecontexts2.md).

## <a name="see-also"></a>Confira também
- [Controle de execução e avaliação de estado](../../extensibility/debugger/execution-control-and-state-evaluation.md)
