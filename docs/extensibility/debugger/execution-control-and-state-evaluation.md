---
title: Controle de execução e avaliação de estado | Microsoft Docs
description: Saiba como a depuração do Visual Studio baseia seu controle de execução em eventos enviados entre componentes do depurador.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], execution control
- expression evaluation, control of execution
ms.assetid: 55adde38-1622-4b51-83cb-ce1b04c1ca7a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 598332ec1e9e1cb270360822ca32792b9a53f5c1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096948"
---
# <a name="execution-control-and-state-evaluation"></a>Controle de execução e avaliação de estado
A depuração de um aplicativo requer a implementação desses recursos de controle de execução como depuração em funções, parando em pontos de interrupção e continuando a execução. A depuração do Visual Studio baseia seu controle de execução em eventos enviados entre componentes do depurador.

## <a name="in-this-section"></a>Nesta seção
 [Controle de programa](../../extensibility/debugger/program-control.md) Lista as seguintes rotinas que ocorrem no nível do programa: definindo a próxima instrução, executando, percorrendo, continuando, suspendendo e retomando.

 [Métodos relacionados ao ponto de interrupção](../../extensibility/debugger/breakpoint-related-methods.md) Define os tipos associados e pendentes de pontos de interrupção aos quais o Visual Studio dá suporte.

 [Avaliação da pilha de chamadas](../../extensibility/debugger/call-stack-evaluation.md) Discute a implementação dos métodos que permitem a exibição dos quadros de pilha da pilha de chamadas durante o modo de interrupção.

 [Avaliação de expressão](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md) Explica como o mecanismo de depuração (DE), a avaliação de expressão (EE) e o Gerenciador de depuração de sessão estão envolvidos na análise e na avaliação de uma expressão inserida em uma das janelas do IDE.

 [Eventos de controle](../../extensibility/debugger/control-events.md) Discute a interface usada para enviar eventos durante a execução controlada do programa.
