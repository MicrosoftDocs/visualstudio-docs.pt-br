---
title: Registros de ativação | Microsoft Docs
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
- stack frames, debugging
- debugging [Debugging SDK], stack frames
- stack frames
ms.assetid: b5e439d4-1e9d-4e13-9cad-bb8b136d4ca8
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: ebd9f1881f0e0579a3b319f6608cdbf348ed027b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51789324"
---
# <a name="stack-frames"></a>Registros de ativação
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Em termos de arquitetura do depurador, uma **quadro de pilha**:  
  
-   É uma abstração de uma pilha que fornece o contexto de execução de um thread. Um thread sempre é executado dentro de uma função. Um quadro de pilha contém as variáveis locais da função e os argumentos a ele. Para depurar com o Visual Studio, o idioma ou o ambiente que está sendo depurado deve dar suporte a quadros de pilha.  
  
-   Pode tanto identificar e descrever em si e pode retornar o thread associado. Um quadro de pilha também pode retornar o contexto de código que representa o ponteiro de instrução atual, bem como a documentação associada e contextos de avaliação de expressão.  
  
-   Tem propriedades que descrevem o nome, tipo e valor de argumentos e variáveis locais, e que aparecem em várias janelas de depuração do IDE.  
  
-   É representado por um [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) interface, geralmente criado por um mecanismo de depuração (DES) ou a máquina virtual como consequência de execução de um thread.  
  
## <a name="see-also"></a>Consulte também  
 [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)   
 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)   
 [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)   
 [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)

