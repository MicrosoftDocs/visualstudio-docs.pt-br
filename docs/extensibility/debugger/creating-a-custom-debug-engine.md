---
title: Criando um mecanismo de depuração personalizado | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, implementing
- debug engines, custom
- debugging [Debugging SDK], custom debug engines
ms.assetid: 52794238-6fae-451c-bf1c-99f344c6f173
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 241bc016d8a64905951bffef07ba425f1351a727
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903576"
---
# <a name="create-a-custom-debug-engine"></a>Criar um mecanismo de depuração personalizado
Um mecanismo DE depuração (DE) é um componente que permite a depuração de arquiteturas de tempo de execução específicas. Normalmente, há apenas uma DE implementação por ambiente DE tempo DE execução.

> [!NOTE]
> Embora haja implementações separadas para Transact-SQL e JScript, o VBScript e o JScript compartilham um único DE.

 Um DE funciona com o interpretador ou o sistema operacional para fornecer serviços de depuração como controle de execução, pontos de interrupção e avaliação de expressão. Esses serviços são implementados por meio de interfaces e podem fazer com que o depurador faça a transição entre diferentes modos operacionais. Para obter mais informações, consulte [modos operacionais](../../extensibility/debugger/operational-modes.md).

 A criação de um de consiste nas seguintes etapas:

1. Registrar um DE com o Visual Studio

2. Habilitar um programa a ser depurado

3. Implementar o controle de execução e a avaliação de estado

4. Enviar eventos

5. Configurar encerramento e desanexação

## <a name="in-this-section"></a>Nesta seção
 [Registrar um mecanismo de depuração personalizado](../../extensibility/debugger/registering-a-custom-debug-engine.md) Explica as etapas necessárias para registrar um mecanismo de depuração com o Visual Studio para que ele possa ser usado.

 [Habilitar um programa a ser depurado](../../extensibility/debugger/enabling-a-program-to-be-debugged.md) Explica que, antes que o DE possa depurar um programa, você deve primeiro iniciar o ou anexá-lo a um programa existente.

 [Implementar o controle de execução e a avaliação de estado](../../extensibility/debugger/execution-control-and-state-evaluation.md) Discute por que depurar um aplicativo requer a implementação de recursos de controle de execução.

 [Enviar eventos](../../extensibility/debugger/sending-events.md) Descreve a comunicação entre o depurador e o DE como um modelo DE evento baseado no DCOM.

 [Configurar encerramento e desanexação](../../extensibility/debugger/termination-and-detaching.md) Explica como obter um encerramento normal, o que significa que não há pontos de interrupção, exceções, erros de tempo de execução ou loops infinitos no aplicativo a ser depurado.

 [Chamar eventos do depurador](../../extensibility/debugger/calling-debugger-events.md) Documenta a ordem de chamada dos eventos que ocorrem em uma sessão de depuração.

 [Como depurar um mecanismo de depuração personalizado](../../extensibility/debugger/how-to-debug-a-custom-debug-engine.md) Explica como depurar um DE.

## <a name="see-also"></a>Confira também
- [Extensibilidade do depurador do Visual Studio](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
