---
title: Avaliação da pilha de chamadas | Microsoft Docs
description: Saiba mais sobre o método EnumFrameInfo e como implementá-lo para exibir os quadros de pilha da pilha de chamadas durante o modo de interrupção.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], call stack evaluation
- call stacks, evaluation
ms.assetid: 373d6b49-0459-4cce-816e-05745a44fe49
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c7e7180301965e43e6757340019c3506fe1a5e1f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055083"
---
# <a name="call-stack-evaluation"></a>Avaliação da pilha de chamadas
Para exibir os quadros de pilha da pilha de chamadas durante o modo de interrupção, você deve implementar o método [EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) .

## <a name="methods-for-evaluation"></a>Métodos para avaliação
 Para um mecanismo DE depuração simples (DE), pode haver apenas um quadro de pilha. Para examinar o quadro de pilhas durante o modo de interrupção, você deve implementar os seguintes métodos de [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md).

|Método|Descrição|
|------------|-----------------|
|[GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|Obtém o contexto do código para um registro de ativação. O contexto de código representa o ponteiro de instrução atual em um registro de ativação.|
|[GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|Obtém o contexto do documento para um quadro de pilha. O contexto do documento representa o local atual no código-fonte de um registro de ativação. Necessário para exibir o código-fonte quando você está parado em um programa.|

 Esses métodos exigem a implementação de várias interfaces e métodos relacionados ao contexto. Portanto, você deve implementar o método [GetDocumentContext](../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md) e os seguintes métodos de [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md).

|Método|Descrição|
|------------|-----------------|
|[GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|Obtém o intervalo de instruções de arquivo de um contexto de documento.|

 Para enumerar contextos de código, você deve implementar todos os métodos de [IEnumDebugCodeContexts2](../../extensibility/debugger/reference/ienumdebugcodecontexts2.md).

## <a name="see-also"></a>Confira também
- [Controle de execução e avaliação de estado](../../extensibility/debugger/execution-control-and-state-evaluation.md)
