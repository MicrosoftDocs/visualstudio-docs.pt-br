---
title: Contextos do depurador | Microsoft Docs
description: 'Saiba como o mecanismo de depuração do Visual Studio opera em contextos distintos: contexto de código, contexto ou posição de documentação e contexto de avaliação de expressão.'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 79808036-b680-4e4c-9c61-4ed43aa11323
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5103561a420c3836f60a22790335522a83798966
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903665"
---
# <a name="debugger-contexts"></a>Contextos do depurador
Na [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depuração, o mecanismo de depuração (de) opera simultaneamente em vários contextos distintos, da seguinte maneira:

- O contexto do código, que descreve o local atual no fluxo de execução de um programa.

- O contexto ou a posição da documentação, que descreve a posição atual em um documento de origem.

- O contexto de avaliação da expressão, que descreve o contexto no qual ocorre a avaliação da expressão.

## <a name="in-this-section"></a>Nesta seção
 [Contexto de código](../../extensibility/debugger/code-context.md) Discute o contexto de código como um endereço no fluxo de instruções de um programa nas arquiteturas de tempo de execução de hoje versus linguagens não tradicionais, em que o código não pode ser representado por instruções, mas outros meios.

 [Posição do documento](../../extensibility/debugger/document-position.md) Define a posição do documento na depuração do Visual Studio por meio de uma abstração de uma posição em um arquivo de origem, como conhecido pelo IDE.

 [Contexto do documento](../../extensibility/debugger/document-context.md) Discute o que o contexto de documento representa na depuração do Visual Studio em relação a um arquivo de origem. Também discute como o manipulador de símbolo mapeia um contexto de código para o contexto de documentação.

 [Contexto de avaliação da expressão](../../extensibility/debugger/expression-evaluation-context.md) Fornece informações sobre um contexto de avaliação de expressão no Visual Studio. Por exemplo, um contexto de avaliação de expressão associado a um quadro de pilha fornece o contexto para avaliar variáveis locais, parâmetros de método e membros de classe.

## <a name="related-sections"></a>Seções relacionadas
 [Conceitos de depuração](../../extensibility/debugger/debugger-concepts.md) Descreve os principais conceitos de arquitetura da depuração.

 [Componentes de depuração](../../extensibility/debugger/debugger-components.md) Fornece uma visão geral dos componentes de depuração do Visual Studio, que incluem o mecanismo DE depuração (DE), o avaliador de expressão (EE) e o manipulador de símbolo (SH).

 [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md) Contém links para várias tarefas de depuração, como iniciar um programa e avaliar expressões.
