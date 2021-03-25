---
title: Threads | Microsoft Docs
description: Este artigo descreve a definição e a função de um thread na arquitetura do depurador no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], threads
- threading [Debugging SDK]
ms.assetid: 2243d24a-c3d2-41d1-abbb-6db21a2db9ee
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 168d29b8306ec58233f426b48c3ab0adfacb2bd5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057839"
---
# <a name="threads"></a>Threads
Na arquitetura do depurador, um *thread*:

- É a unidade fundamental de computação. Um thread executa sequencialmente suas instruções no contexto de uma única pilha de chamadas, movendo de um contexto de código para o outro.

- Pode identificar a si mesmo e o programa em que ele está sendo executado. Os threads podem ser nomeados, suspensos e retomados. Um thread também pode enumerar seus quadros de pilhas associados e, em algumas condições, pode ser movido para outro quadro de pilha. Dado o contexto de um quadro de pilha, um thread pode retornar seu thread lógico associado, se houver. Um thread tem propriedades, como uma contagem de suspensão, que pode ser exibida na janela **threads** do IDE.

- É representado por uma interface [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) , normalmente criada por um mecanismo de depuração (de) ou máquina virtual como consequência da execução de um programa.

## <a name="see-also"></a>Confira também
- [Programas](../../extensibility/debugger/programs.md)
- [Quadros de pilha](../../extensibility/debugger/stack-frames.md)
- [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)
- [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)
- [Gerenciador de depuração de sessão](../../extensibility/debugger/session-debug-manager.md)
