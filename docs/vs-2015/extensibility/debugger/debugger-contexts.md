---
title: Contextos do depurador | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 79808036-b680-4e4c-9c61-4ed43aa11323
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 771a3cd8ae25173f3033b3a3229e516570f5dedc
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60116232"
---
# <a name="debugger-contexts"></a>Contextos de depurador
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

No [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] depuração, o mecanismo de depuração (DES) opera simultaneamente em vários contextos distintos, da seguinte maneira:  
  
- O contexto de código, que descreve o local atual no fluxo de execução de um programa.  
  
- O contexto de documentação ou posição, que descreve a posição atual dentro de um documento de origem.  
  
- O contexto de avaliação de expressão, que descreve o contexto em que a expressão a avaliação será realizada.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Contexto do código](../../extensibility/debugger/code-context.md)  
 Discute o contexto de código como um endereço no fluxo de instruções de um programa em arquiteturas de tempo de execução de hoje versus idiomas não tradicionais, onde código não pode ser representado por instruções, mas outros meios.  
  
 [Posição do documento](../../extensibility/debugger/document-position.md)  
 Define a posição do documento na depuração por meio de uma abstração de uma posição em um arquivo de origem como o IDE conhecido do Visual Studio.  
  
 [Contexto do documento](../../extensibility/debugger/document-context.md)  
 Discute o contexto de documento representa em depuração do Visual Studio em relação a um arquivo de origem. Também discute como o manipulador de símbolo mapeia um contexto de código para o contexto da documentação.  
  
 [Contexto da avaliação de expressão](../../extensibility/debugger/expression-evaluation-context.md)  
 Fornece informações sobre um contexto de avaliação de expressão no Visual Studio. Por exemplo, um contexto de avaliação de expressão associado com um quadro de pilha fornece o contexto para avaliar as variáveis locais, parâmetros de método e membros de classe.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Conceitos de depuração](../../extensibility/debugger/debugger-concepts.md)  
 Descreve os principais conceitos de arquiteturas de depuração.  
  
 [Componentes de depuração](../../extensibility/debugger/debugger-components.md)  
 Fornece uma visão geral do que os componentes de depuração do Visual Studio, que incluem o mecanismo de depuração (DE), o avaliador de expressão (EE) e o manipulador de símbolo (SH).  
  
 [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)  
 Contém links para várias tarefas de depuração, como iniciar um programa e avaliar expressões.
