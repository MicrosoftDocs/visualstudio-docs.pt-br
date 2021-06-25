---
title: Controle de programa | Microsoft Docs
description: Saiba mais sobre as rotinas na depuração do Visual Studio que ocorrem no nível do programa, como execução, depuração, continuação e suspensão/retomada de threads.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], control of execution
ms.assetid: 6be80904-e66c-4cae-8891-1113b799fb01
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7b2946309c72fbdddf2794c1da1e773e9a529368
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900701"
---
# <a name="program-control"></a>Controle de programa
Na depuração do Visual Studio, todas as seguintes rotinas de revisão e continuação ocorrem no nível do programa:

- Configurando a próxima instrução, ou seja, definindo seu computador para a próxima instrução a ser executada em um ambiente de quadro específico

- Executando, ou seja, continuando a sair do modo de depuração

- Avançando para a próxima instrução

- Continuando com o modo de revisão atual

- Suspendendo os threads contidos no programa

- Retomando os threads contidos no programa

> [!NOTE]
> A exibição da pilha de chamadas é implementada no nível do thread. Para enumerar as informações do quadro ao exibir a pilha de chamadas para um thread, você deve implementar todos os métodos da interface [IEnumDebugFrameInfo2](../../extensibility/debugger/reference/ienumdebugframeinfo2.md) .

## <a name="methods-of-program-control"></a>Métodos de controle de programa
 A tabela a seguir mostra os métodos de [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) que devem ser implementados para um mecanismo de depuração (de) e controle de execução minimamente funcional.

|Método|Descrição|
|------------|-----------------|
|[IDebugProgram2::Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md)|Continua executando todos os threads contidos por um programa a partir de um estado parado. Necessário para o controle de execução.|
|[IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)|Continua executando todos os threads contidos por um programa a partir de um estado parado. Necessário para o controle de execução.|
|[IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md)|Executa uma etapa no thread determinado. Continua executando todos os outros threads contidos no programa. Necessário para o controle de execução.|

 Para programas multissegmentados, você também deve implementar o método [IDebugProgram2:: EnumThreads](../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) e todos os métodos da interface [IEnumDebugThreads2](../../extensibility/debugger/reference/ienumdebugthreads2.md) .

## <a name="see-also"></a>Confira também
- [Controle de execução e avaliação de estado](../../extensibility/debugger/execution-control-and-state-evaluation.md)
