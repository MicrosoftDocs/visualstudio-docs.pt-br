---
title: Programas | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], programs
- programs, debugging
ms.assetid: e1f955d8-95da-493b-837e-e97741a26d7e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: d8bd34f72f54fe068ff39b752ddbd6348e4970db
ms.sourcegitcommit: 71b307ce86c4079cc7ad686d8d5f96a6a123aadd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2018
ms.locfileid: "39252369"
---
# <a name="programs"></a>Programas
Na arquitetura do depurador, uma *programa*:  
  
-   É um contêiner para um conjunto de threads e um conjunto de módulos. Um programa não tem nenhum analogia única no sistema operacional Windows.  
  
     Um programa é um tipo de subprocesso. Por exemplo, quando você estiver depurando um site da Web, um script pode ser visto como um programa. Enquanto um script é executado no processo de mecanismo de script, independente dos outros scripts, ele também tem seu próprio conjunto de threads. Um mecanismo de depuração (DES) anexa a um programa e não a um processo ou um thread.  
  
-   Pode identificar em si e o processo que está executando no. Pode ser anexado a um programa para ser desanexado do e descrever o DE que o criou, se houver. Um programa pode também executar, interromper, continuar e ser encerrada.  
  
-   Pode enumerar todos os seus threads. Um programa também pode fornecer seu próprio fluxo de desmontagem e pode enumerar todos os contextos de código da posição de um determinado documento.  
  
-   É representado por um [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) interface, criada antes que o programa está anexado, ou como parte do processo de anexação, dependendo da implementação. Quando uma porta enumera os programas de um processo, cada programa é criado de acordo com um correspondente [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) interface é passada como um argumento para [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md). Embora os mecanismos de depuração também criar `IDebugProgram2` interfaces para representar os programas, esses programas não são criadas de acordo com um nó de programa. O `IDebugProgramNode2` interfaces criados por um DE são usados para depuração real, enquanto os criados por uma porta são usados apenas para descobrir quais programas estão em execução em um processo.  
  
## <a name="see-also"></a>Consulte também  
 [Processos](../../extensibility/debugger/processes.md)   
 [Nós de programa](../../extensibility/debugger/program-nodes.md)   
 [Módulos](../../extensibility/debugger/modules.md)   
 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)   
 [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)   
 [Posição do documento](../../extensibility/debugger/document-position.md)   
 [Contexto de código](../../extensibility/debugger/code-context.md)   
 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)