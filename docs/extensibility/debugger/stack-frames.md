---
title: Registros de ativação | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- stack frames, debugging
- debugging [Debugging SDK], stack frames
- stack frames
ms.assetid: b5e439d4-1e9d-4e13-9cad-bb8b136d4ca8
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 21ef19e1eaf9e98da3e774f1d0038f03c131ec45
ms.sourcegitcommit: 8d38d5d2f2b75fc1563952c0d6de0fe43af12766
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/26/2018
ms.locfileid: "39276709"
---
# <a name="stack-frames"></a>Quadros de pilha
Na arquitetura do depurador, uma *quadro de pilha*:  
  
-   É uma abstração de uma pilha que fornece o contexto de execução de um thread. Um thread sempre é executado dentro de uma função. Um quadro de pilha contém as variáveis locais da função e os argumentos a ele. Para depurar com o Visual Studio, o idioma ou o ambiente que está sendo depurado deve dar suporte a quadros de pilha.  
  
-   Pode tanto identificar e descrever em si e pode retornar o thread associado. Um quadro de pilha também pode retornar o contexto de código que representa o ponteiro de instrução atual e a documentação associada e contextos de avaliação de expressão.  
  
-   Tem propriedades que descrevem o nome, tipo e valor de argumentos e variáveis locais, e que aparecem em várias janelas de depuração do IDE.  
  
-   É representado por um [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) interface, geralmente criado por um mecanismo de depuração (DES) ou a máquina virtual como consequência de execução de um thread.  
  
## <a name="see-also"></a>Consulte também  
 [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)   
 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)   
 [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)   
 [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)