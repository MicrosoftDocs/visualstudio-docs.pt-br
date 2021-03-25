---
title: Conceitos do depurador | Microsoft Docs
description: Saiba mais sobre os conceitos de arquitetura usados na criação do pacote de depuração do Visual Studio para ajudá-lo a se basear nesse pacote.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK]
ms.assetid: 2d371d38-f1a0-4a9a-8ea3-100e8c0149b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 94249a6ff7c50fb054a3fc460708a8e36181bff8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094881"
---
# <a name="debugger-concepts"></a>Conceitos do depurador
Para criar o pacote de depuração do Visual Studio, você precisa estar familiarizado com os conceitos arquitetônicos usados na criação do pacote.

## <a name="in-this-section"></a>Nesta seção
 [Sessão de depuração](../../extensibility/debugger/debug-session.md) Explica a função de uma sessão na arquitetura de depuração.

 [Servidores](../../extensibility/debugger/servers-visual-studio-sdk.md) do Define o que um servidor está em termos de arquitetura de depuração, em termos abstratos e físicos.

 [Fornecedores de porta](../../extensibility/debugger/port-suppliers.md) Define o que um fornecedor de porta está em termos de arquitetura de depuração.

 [Portas](../../extensibility/debugger/ports.md) Define o que é uma porta em termos de arquitetura de depuração.

 [Processos](../../extensibility/debugger/processes.md) do Define o que é um processo em termos de arquitetura de depuração.

 [Nós de programa](../../extensibility/debugger/program-nodes.md) Define um nó de programa em termos de arquitetura de depuração, incluindo como ele pode se identificar e o processo em que ele está sendo executado.

 [Programas](../../extensibility/debugger/programs.md) do Define um programa em termos de arquitetura de depuração.

 [Threads](../../extensibility/debugger/threads.md) Define as características dos threads em termos de arquitetura de depuração.

 [Quadros de pilha](../../extensibility/debugger/stack-frames.md) Define um registro de ativação em termos de arquitetura de depuração. Um registro de ativação é uma abstração de uma pilha que fornece o contexto de execução de um thread.

 [Módulos](../../extensibility/debugger/modules.md) do Define um módulo, em termos de arquitetura de depuração, como um contêiner físico de código, como um arquivo executável ou uma DLL.

 [Pontos de interrupção](../../extensibility/debugger/breakpoints-visual-studio-sdk.md) Define os três tipos de pontos de interrupção — pendente, associado e erro — em termos de arquitetura de depuração.

## <a name="related-sections"></a>Seções relacionadas
 [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md) Explica como o mecanismo de depuração (DE) opera simultaneamente nos contextos de avaliação de código, documentação e expressão. Descreve, para cada um dos três contextos, o local, a posição ou a avaliação relevante para ele.

 [Componentes do depurador](../../extensibility/debugger/debugger-components.md) Fornece uma visão geral dos componentes de depuração do Visual Studio, que incluem o mecanismo DE depuração (DE), o avaliador de expressão (EE) e o manipulador de símbolo (SH).

 [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md) Contém links para várias tarefas de depuração, como iniciar um programa e avaliar expressões.
