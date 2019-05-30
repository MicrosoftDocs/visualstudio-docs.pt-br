---
title: Anexar diretamente a um programa | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: ad2b7db8-821c-440c-ba07-c55c6a395e0f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d4bf703544bbe1932608db17addba672bfd91a70
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350893"
---
# <a name="attach-directly-to-a-program"></a>Conectar diretamente a um programa
Os usuários que desejam depurar programas em um processo que já está em execução normalmente siga este processo:

1. No IDE, escolha o **depurar processos** comando da **ferramentas** menu.

    A caixa de diálogo **Processos** é exibida.

2. Escolher um processo e clique no **Attach** botão.

    O **anexar ao processo** caixa de diálogo for exibida, listando todos os mecanismos de depuração (DEs) instalados no computador.

3. Especifique o DEs usar para depurar o processo selecionado e, em seguida, clique em **Okey**.

   O pacote de depuração inicia uma sessão de depuração e passa a lista de DEs para ele. A sessão de depuração por sua vez, passa essa lista, juntamente com uma função de retorno de chamada, para o processo selecionado e, em seguida, solicita que o processo para enumerar os seus programas em execução.

   Programaticamente, em resposta à solicitação do usuário, o pacote de depuração instancia o Gerenciador de sessão de depuração (SDM) e passa a lista de DEs selecionado a ele. Junto com a lista, o pacote de depuração passa o SDM uma [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) interface. O pacote de depuração passa a lista de DEs para o processo selecionado chamando [IDebugProcess2::Attach](../../extensibility/debugger/reference/idebugprocess2-attach.md). Em seguida, chama o SDM [IDebugProcess2::EnumPrograms](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md) na porta para enumerar os programas em execução no processo.

   Desse ponto em diante, cada mecanismo de depuração é anexado a um programa exatamente conforme detalhado na [anexar após uma inicialização](../../extensibility/debugger/attaching-after-a-launch.md), com duas exceções.

   Para obter eficiência, DEs são implementados para compartilhar um espaço de endereço com o SDM são agrupados de forma que cada Alemanha tem um conjunto de programas, ele será anexado ao. Nesse caso, [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) chamadas [IDebugEngine2::Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) e passa uma matriz de programas para anexar a.

   A segunda exceção é que os eventos de inicialização enviados por um DE anexar a um programa que já está em execução normalmente não incluem o evento de ponto de entrada.

## <a name="see-also"></a>Consulte também
- [Enviar eventos de inicialização após uma inicialização](../../extensibility/debugger/sending-startup-events-after-a-launch.md)
- [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)