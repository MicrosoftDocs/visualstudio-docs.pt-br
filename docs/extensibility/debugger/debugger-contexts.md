---
title: Contextos do depurador | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 79808036-b680-4e4c-9c61-4ed43aa11323
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 49af504b27afc6171a914d9559a5ff83f3d595eb
ms.sourcegitcommit: 36835f1b3ec004829d6aedf01938494465587436
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2018
ms.locfileid: "39204096"
---
# <a name="debugger-contexts"></a>Contextos do depurador
No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depuração, o mecanismo de depuração (DES) opera simultaneamente em vários contextos distintos, da seguinte maneira:  
  
-   O contexto de código, que descreve o local atual no fluxo de execução de um programa.  
  
-   O contexto de documentação ou posição, que descreve a posição atual dentro de um documento de origem.  
  
-   O contexto de avaliação de expressão, que descreve o contexto em que a expressão a avaliação será realizada.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Contexto de código](../../extensibility/debugger/code-context.md)  
 Discute o contexto de código como um endereço no fluxo de instruções de um programa em arquiteturas de tempo de execução de hoje versus idiomas não tradicionais, onde código não pode ser representado por instruções, mas outros meios.  
  
 [Posição do documento](../../extensibility/debugger/document-position.md)  
 Define a posição do documento na depuração por meio de uma abstração de uma posição em um arquivo de origem como o IDE conhecido do Visual Studio.  
  
 [Contexto de documento](../../extensibility/debugger/document-context.md)  
 Discute o contexto de documento representa em depuração do Visual Studio em relação a um arquivo de origem. Também discute como o manipulador de símbolo mapeia um contexto de código para o contexto da documentação.  
  
 [Contexto de avaliação de expressão](../../extensibility/debugger/expression-evaluation-context.md)  
 Fornece informações sobre um contexto de avaliação de expressão no Visual Studio. Por exemplo, um contexto de avaliação de expressão associado com um quadro de pilha fornece o contexto para avaliar as variáveis locais, parâmetros de método e membros de classe.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Conceitos de depuração](../../extensibility/debugger/debugger-concepts.md)  
 Descreve os principais conceitos de arquiteturas de depuração.  
  
 [Componentes de depuração](../../extensibility/debugger/debugger-components.md)  
 Fornece uma visão geral do que os componentes de depuração do Visual Studio, que incluem o mecanismo de depuração (DE), o avaliador de expressão (EE) e o manipulador de símbolo (SH).  
  
 [As tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)  
 Contém links para várias tarefas de depuração, como iniciar um programa e avaliar expressões.