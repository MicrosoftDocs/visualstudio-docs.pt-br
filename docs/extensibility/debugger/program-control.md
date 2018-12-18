---
title: Controle do programa | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], control of execution
ms.assetid: 6be80904-e66c-4cae-8891-1113b799fb01
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a60b766763ca5f68f8c379fbab9372e41c319671
ms.sourcegitcommit: 71b307ce86c4079cc7ad686d8d5f96a6a123aadd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2018
ms.locfileid: "39251092"
---
# <a name="program-control"></a>Controle do programa
No Visual Studio de depuração, todos os procedimentos passo a passo e continuando rotinas ocorrerem no nível do programa:  
  
-   Ou seja, definir a próxima instrução, a configuração de seu computador para a próxima instrução a ser executada no ambiente de um determinado quadro  
  
-   Ou seja, executar, continuando sair do modo de depuração  
  
-   Passo a passo para a próxima instrução  
  
-   Continuando com o modo de depuração atual  
  
-   Suspender os threads contidos pelo programa  
  
-   Retomar os threads contidos pelo programa  
  
> [!NOTE]
>  Exibindo a pilha de chamadas é implementada no nível do thread. Para enumerar as informações do quadro ao exibir a pilha de chamadas para um thread, você deve implementar todos os métodos do [IEnumDebugFrameInfo2](../../extensibility/debugger/reference/ienumdebugframeinfo2.md) interface.  
  
## <a name="methods-of-program-control"></a>Métodos de controle do programa  
 A tabela a seguir mostra os métodos de [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) que deve ser implementada para um mecanismo de depuração minimamente funcional (DES) e o controle de execução.  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugProgram2::Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md)|Continuar em execução por todos os threads contidos por um programa de um estado parado. Necessário para o controle de execução.|  
|[IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)|Continuar em execução por todos os threads contidos por um programa de um estado parado. Necessário para o controle de execução.|  
|[IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md)|Executa uma etapa em determinado thread. Continua em execução a todos os outros threads contidos pelo programa. Necessário para o controle de execução.|  
  
 Para os programas multithread, você também deve implementar o [IDebugProgram2::EnumThreads](../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) método e todos os métodos do [IEnumDebugThreads2](../../extensibility/debugger/reference/ienumdebugthreads2.md) interface.  
  
## <a name="see-also"></a>Consulte também  
 [Avaliação de controle e o estado de execução](../../extensibility/debugger/execution-control-and-state-evaluation.md)