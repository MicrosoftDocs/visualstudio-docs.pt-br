---
title: Tarefas de depuração | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], tasks
ms.assetid: 5d60e9e8-305e-4a48-829f-b9440fc8af7b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8a1d2ae4b05398daa7c42be441cebecb304bf956
ms.sourcegitcommit: 36835f1b3ec004829d6aedf01938494465587436
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2018
ms.locfileid: "39204161"
---
# <a name="debug-tasks"></a>As tarefas de depuração
Para depurar um programa, ele deve ser iniciado e um mecanismo de depuração (DES) deve ser anexado a ele, caso contrário, o DE deve ser anexado a um programa iniciado anteriormente. Depois de anexada, o DE deve gerar determinados eventos de inicialização. Em resposta, o pacote de depuração tenta associar os pontos de interrupção definidos no IDE. Quando o programa atinge um ponto de interrupção associado, ele é interrompida e aguarda a entrada do usuário.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Problemas de segurança](../../extensibility/debugger/security-issues.md)  
 Discute as etapas de segurança que são necessários para depurar um programa.  
  
 [Iniciar um programa](../../extensibility/debugger/launching-a-program.md)  
 Fornece instruções passo a passo sobre como especificar a DE, que chama o sistema operacional para iniciar o programa.  
  
 [Conectar diretamente a um programa](../../extensibility/debugger/attaching-directly-to-a-program.md)  
 Descreve o processo usado para depurar um programa em um processo que já está em execução.  
  
 [Enviar eventos de inicialização após uma inicialização](../../extensibility/debugger/sending-startup-events-after-a-launch.md)  
 Lista os eventos que ocorrem depois que o DE que é anexado ao programa, até que o programa está em seu ponto de entrada principal e está pronto para depuração.  
  
 [Controle de execução](../../extensibility/debugger/control-of-execution.md)  
 Explica como o DE envia normalmente um evento de ponto de entrada, um evento de conclusão de carga ou um evento de interrupção, dependendo das circunstâncias.  
  
 [Associar os pontos de interrupção](../../extensibility/debugger/binding-breakpoints.md)  
 Descreve como fazer isso, se o usuário define um ponto de interrupção, o IDE Formula a solicitação e solicita que a sessão de depuração para criar o ponto de interrupção.  
  
 [Avaliar expressões](../../extensibility/debugger/evaluating-expressions.md)  
 Explica como as expressões são criadas e o que acontece quando uma expressão é avaliada.  
  
 [Visualizar e exibir dados](../../extensibility/debugger/visualizing-and-viewing-data.md)  
 Explica como os visualizadores de tipo e visualizadores personalizados são suportados pelo avaliador de expressão (EE).  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)  
 Descreve os principais conceitos de arquiteturas de depuração.  
  
 [Componentes do depurador](../../extensibility/debugger/debugger-components.md)  
 Fornece uma visão geral do que os componentes de depuração do Visual Studio, que incluem o DE, EE e o manipulador de símbolo (SH).  
  
 [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)  
 Explica como o DE simultaneamente opera dentro do código, documentação e contextos de avaliação de expressão. Descreve, para cada um dos três contextos, a localização, posição ou avaliação relevante a ele.  
  
## <a name="see-also"></a>Consulte também  
 [Introdução](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)