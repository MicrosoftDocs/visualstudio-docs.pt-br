---
title: Criar um personalizado de mecanismo de depuração | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, implementing
- debug engines, custom
- debugging [Debugging SDK], custom debug engines
ms.assetid: 52794238-6fae-451c-bf1c-99f344c6f173
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ece2b480890054526552ad3aeea4f3bd1a437f74
ms.sourcegitcommit: 36835f1b3ec004829d6aedf01938494465587436
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2018
ms.locfileid: "39203674"
---
# <a name="create-a-custom-debug-engine"></a>Criar um mecanismo de depuração personalizado
Um mecanismo de depuração (DES) é um componente que permite a depuração de arquiteturas de tempo de execução específicas. Normalmente, há apenas uma implementação DE cada ambiente de tempo de execução.  
  
> [!NOTE]
>  Embora existam implementações DE separadas para Transact-SQL e JScript, VBScript e JScript compartilham um único DE.  
  
 A DE funciona com o sistema de operação ou interpretador para fornecer esses serviços de depuração como avaliação de expressão, os pontos de interrupção e controle de execução. Esses serviços são implementados por meio DE interfaces e podem fazer com que o depurador para fazer a transição entre os modos operacionais diferentes. Para obter mais informações, consulte [modos operacionais](../../extensibility/debugger/operational-modes.md).  
  
 Criando a DE consiste as seguintes etapas:  
  
1.  Registrar a DE com o Visual Studio  
  
2.  Habilitar um programa a ser depurado  
  
3.  Implementar a avaliação de controle e o estado de execução  
  
4.  Enviar eventos  
  
5.  Configurar o encerramento e desanexação  
  
## <a name="in-this-section"></a>Nesta seção  
 [Registrar um mecanismo de depuração personalizado](../../extensibility/debugger/registering-a-custom-debug-engine.md)  
 Explica as etapas necessárias para registrar um mecanismo de depuração com o Visual Studio para que ele pode ser usado.  
  
 [Habilitar um programa a ser depurado](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)  
 Explica o que seu Alemanha pode depurar um programa, você deve primeiro iniciar o DE ou anexá-lo a um programa existente.  
  
 [Implementar a avaliação de controle e o estado de execução](../../extensibility/debugger/execution-control-and-state-evaluation.md)  
 Discute por que depurar um aplicativo requer a implementação de recursos de controle de execução.  
  
 [Enviar eventos](../../extensibility/debugger/sending-events.md)  
 Descreve a comunicação entre o depurador e DE como um modelo de evento com base no DCOM.  
  
 [Configurar o encerramento e desanexação](../../extensibility/debugger/termination-and-detaching.md)  
 Explica como realizar um encerramento normal, o que significa que não há nenhum pontos de interrupção, exceções, erros de tempo de execução ou loops infinitos no aplicativo a ser depurado.  
  
 [Chamar eventos do depurador](../../extensibility/debugger/calling-debugger-events.md)  
 Documenta a ordem de chamada dos eventos que ocorrem em uma sessão de depuração.  
  
 [Como Depurar um mecanismo de depuração personalizado](../../extensibility/debugger/how-to-debug-a-custom-debug-engine.md)  
 Explica como depurar a DE personalizado.  
  
## <a name="see-also"></a>Consulte também  
 [Extensibilidade do depurador do Visual Studio](../../extensibility/debugger/visual-studio-debugger-extensibility.md)