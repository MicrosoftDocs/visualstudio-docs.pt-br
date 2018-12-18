---
title: Conceitos do depurador | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK]
ms.assetid: 2d371d38-f1a0-4a9a-8ea3-100e8c0149b7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e38c743ce7170e0842a3430c7b2aa190df94782b
ms.sourcegitcommit: 36835f1b3ec004829d6aedf01938494465587436
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2018
ms.locfileid: "39203800"
---
# <a name="debugger-concepts"></a>Conceitos do depurador
Para compilar no pacote de depuração do Visual Studio, você precisa estar familiarizado com os conceitos de arquiteturas usados na criação do pacote.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Sessão de depuração](../../extensibility/debugger/debug-session.md)  
 Explica a função de uma sessão na arquitetura de depuração.  
  
 [Servidores](../../extensibility/debugger/servers-visual-studio-sdk.md)  
 Define o que um servidor está em termos de depuração de arquitetura, em termos de abstratos e físicos.  
  
 [Fornecedores de porta](../../extensibility/debugger/port-suppliers.md)  
 Define o que é de um fornecedor de porta em termos de arquitetura de depuração.  
  
 [Portas](../../extensibility/debugger/ports.md)  
 Define uma porta está em termos de arquitetura de depuração.  
  
 [Processos](../../extensibility/debugger/processes.md)  
 Define que um processo está em termos de arquitetura de depuração.  
  
 [Nós de programa](../../extensibility/debugger/program-nodes.md)  
 Define um nó de programa em termos de depuração de arquitetura, incluindo como ele pode identificar em si e o processo que está executando no.  
  
 [Programas](../../extensibility/debugger/programs.md)  
 Define um programa em termos de arquitetura de depuração.  
  
 [Threads](../../extensibility/debugger/threads.md)  
 Define as características de threads em termos de arquitetura de depuração.  
  
 [Quadros de pilha](../../extensibility/debugger/stack-frames.md)  
 Define um quadro de pilha em termos de arquitetura de depuração. Um quadro de pilha é uma abstração de uma pilha que fornece o contexto de execução de um thread.  
  
 [Módulos](../../extensibility/debugger/modules.md)  
 Define um módulo, em termos de arquitetura, como um contêiner físico de código, como um arquivo executável ou uma DLL de depuração.  
  
 [Pontos de interrupção](../../extensibility/debugger/breakpoints-visual-studio-sdk.md)  
 Define os três tipos de pontos de interrupção, pendente, associação e o erro — em termos de arquitetura de depuração.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)  
 Explica como o mecanismo de depuração (DES) simultaneamente opera dentro do código, documentação e contextos de avaliação de expressão. Descreve, para cada um dos três contextos, a localização, posição ou avaliação relevante a ele.  
  
 [Componentes do depurador](../../extensibility/debugger/debugger-components.md)  
 Fornece uma visão geral do que os componentes de depuração do Visual Studio, que inclui o mecanismo de depuração (DE), o avaliador de expressão (EE) e o manipulador de símbolo (SH).  
  
 [As tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)  
 Contém links para várias tarefas de depuração, como iniciar um programa e avaliar expressões.