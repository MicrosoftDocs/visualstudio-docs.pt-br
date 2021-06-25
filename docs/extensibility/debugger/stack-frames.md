---
title: Stack Frames | Microsoft Docs
description: Este artigo descreve a definição e a função de um quadro de pilha na arquitetura do depurador Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- stack frames, debugging
- debugging [Debugging SDK], stack frames
- stack frames
ms.assetid: b5e439d4-1e9d-4e13-9cad-bb8b136d4ca8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 77b503afcc38ab9427e5268097655433007de5d9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898546"
---
# <a name="stack-frames"></a>Quadros de pilha
Na arquitetura do depurador, um *quadro de pilha*:

- É uma abstração de uma pilha que fornece o contexto de execução de um thread. Um thread sempre é executado dentro de uma função. Um quadro de pilha contém as variáveis locais da função e os argumentos para ela. Para depurar com Visual Studio, o idioma ou o ambiente que está sendo depurado deve dar suporte a quadros de pilha.

- Pode identificar e descrever a si mesmo e pode retornar o thread associado. Um quadro de pilha também pode retornar o contexto de código que representa o ponteiro de instrução atual e os contextos de avaliação de documentação e expressão associados.

- Tem propriedades que descrevem o nome, o tipo e o valor de variáveis e argumentos locais e que aparecem em várias janelas de depuração do IDE.

- É representado por uma interface [IDebugStackFrame2,](../../extensibility/debugger/reference/idebugstackframe2.md) normalmente criada por um DE (mecanismo de depuração) ou uma máquina virtual como consequência da execução de um thread.

## <a name="see-also"></a>Confira também
- [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)
- [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)
- [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)
- [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)
