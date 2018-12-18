---
title: Fluxos de trabalho de depuração com designers de Fluxo de Trabalho
ms.date: 11/04/2016
ms.topic: conceptual
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
helpviewer_keywords:
- Visual Studio Workflow Designer [WFD], debugging workflows
- Workflow Designer [WFD], debugging workflows
ms.assetid: d71308cf-d464-4536-8711-0d0a8eadb255
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 482e13a91513151d7c4595e0a622f223751ae553
ms.sourcegitcommit: 30f653d9625ba763f6b58f02fb74a24204d064ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36755308"
---
# <a name="debug-workflows-with-the-workflow-designer"></a>Depurar fluxos de trabalho com o Designer de fluxo de trabalho

O **Designer de fluxo de trabalho** fornece a capacidade de depurar fluxos de trabalho e atividades personalizadas. O processo e o comportamento são semelhantes do depurador do Visual Studio padrão.

## <a name="invoke-the-workflow-debugger"></a>Chamar o depurador de fluxo de trabalho

Geralmente, você depura fluxos de trabalho assim como você os programas de depuração escritos em outras linguagens de programação do Visual Studio. Você pode iniciar o depurador de fluxo de trabalho das seguintes maneiras:

- Selecione **anexar ao processo** sobre o **depurar** menu para selecionar o processo de host em execução para a instância de fluxo de trabalho. Este procedimento é o mesmo que anexar a um processo host no código gerenciado.

- Pressione **F5** para iniciar a execução de uma instância do fluxo de trabalho, ou para continuar a executar após um ponto de interrupção foi atingido.

- Use a depuração remota. Para obter informações sobre como usar a depuração remota, consulte [como: habilitar a depuração remota](/previous-versions/visualstudio/visual-studio-2010/febz73k0(v=vs.100)).

   > [!NOTE]
   > Se o aplicativo de fluxo de trabalho se destina a x86 arquitetura e é hospedado em um computador executando um sistema operacional de 64 bits, então a depuração remota não funcionará a menos que o Visual Studio está instalado no computador remoto ou o destino para o aplicativo de fluxo de trabalho é alterado para  **Qualquer CPU**.

## <a name="step-through-code"></a>Percorrer o código

- **Etapa nas**: etapa em uma atividade pressionando **F11**. O depurador avança em qualquer manipulador que é definido. Se nenhum manipulador é definido, você vai sobre a atividade, ou com atividades compostas, que contém outras atividades, você vai na primeira atividade executando.

- **Saída de etapa:** sair de uma atividade pressionando **Shift**+**F11**. Depuração fora de uma atividade executa a atividade atual e todas as suas atividades irmãos para a conclusão. O depurador interrompe no pai de atividade atual. Para passar para fora de um manipulador de código, o depurador interrompe a atividade com que o manipulador está associado.

- **Step Over**: passar sobre uma atividade pressionando **F10**. Para entrar em uma atividade de composição, o depurador interrompe no primeiro filho executável de atividade composta. Para entrar em uma não composição, como uma atividade de <xref:System.Activities.Statements.Assign> , o depurador executa a atividade e seus manipuladores associados e interromper-los na atividade seguir. Se a atividade que é executada é a atividade filho a última em uma atividade de composição, então, após a execução, o depurador interrompe a atividade pai.

## <a name="debug-with-f5"></a>Depuração com F5

Se você estiver criando um aplicativo de console do fluxo de trabalho, basta pressionar **F5** para iniciar a depuração em seu aplicativo e o fluxo de trabalho. Se você estiver criando uma biblioteca de atividades por conta própria, você deve especificar um executável do aplicativo host como o projeto de inicialização. Para definir um projeto de inicialização no **Gerenciador de soluções**, clique com botão direito no nome do host do projeto e selecione **definir como projeto de inicialização**.