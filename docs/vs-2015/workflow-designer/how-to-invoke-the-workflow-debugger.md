---
title: 'Como: chamar o depurador de fluxo de trabalho | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 34c592af-f4f6-4d02-99f6-63a94698e48b
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: acfbe34bc4a3d3c1139f8b1e821d9996fb8c712b
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49295731"
---
# <a name="how-to-invoke-the-workflow-debugger"></a>Como: Chamar o depurador de fluxo de trabalho
Geralmente, você depura fluxos de trabalho assim como você os programas de depuração escritos em outras linguagens de programação do Visual Studio. Você pode iniciar o depurador de fluxo de trabalho das seguintes maneiras:  
  
-   Selecione **anexar ao processo** sobre o **depurar** menu para selecionar o processo de host em execução para a instância de fluxo de trabalho. Este procedimento é o mesmo que anexar a um processo host no código gerenciado.  
  
-   Pressione **F5** para iniciar a execução de uma instância do fluxo de trabalho, ou para continuar a executar após um ponto de interrupção foi atingido.  
  
-   Use a depuração remota. Para obter informações sobre como usar a depuração remota, consulte [como: Ativar depuração remota](http://go.microsoft.com/fwlink/?LinkId=196257).  
  
    > [!NOTE]
    >  Se o aplicativo de fluxo de trabalho se destina a x86 arquitetura e é hospedado em um computador executando um sistema operacional de 64 bits, então a depuração remota não funcionará a menos que [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] está instalado no computador remoto ou o destino para o aplicativo de fluxo de trabalho é alterado para **Qualquer CPU**.  
  
### <a name="stepping-through-code"></a>Percorrendo o código  
  
-   **Etapa nas**: você pode entrar em uma atividade usando **F11**. O depurador avança em qualquer manipulador que é definido. Se nenhum manipulador é definido, você vai sobre a atividade, ou com atividades compostas, que contém outras atividades, você vai na primeira atividade executando.  
  
-   **Saída de etapa:** você pode entrar fora de uma atividade usando **Shift-F11**. Depuração fora de uma atividade executa a atividade atual e todas as suas atividades irmãos para a conclusão. O depurador interrompe no pai de atividade atual. Para passar para fora de um manipulador de código, o depurador interrompe a atividade com que o manipulador está associado.  
  
-   **Step Over**: você pode entrar em uma atividade usando **F10**. Para entrar em uma atividade de composição, o depurador interrompe no primeiro filho executável de atividade composta. Para entrar em uma não composição, como uma atividade de <xref:System.Activities.Statements.Assign> , o depurador executa a atividade e seus manipuladores associados e interromper-los na atividade seguir. Se a atividade que é executada é a atividade filho a última em uma atividade de composição, então, após a execução, o depurador interrompe a atividade pai.  
  
### <a name="debugging-with-f5"></a>Depuração com F5  
  
-   Se você estiver criando um projeto de aplicativo de Console do fluxo de trabalho, basta pressionar **F5** para iniciar a depuração em seu aplicativo e o fluxo de trabalho. Se você estiver criando uma biblioteca de atividade em seus próprios, você deve ter um executável do aplicativo host como um projeto de inicialização. Para definir um projeto de inicialização no **Gerenciador de soluções**, clique com botão direito no nome do host do projeto e selecione **definir como projeto de inicialização**.  
  
## <a name="see-also"></a>Consulte também  
 [Como: definir pontos de interrupção em fluxos de trabalho](../workflow-designer/how-to-set-breakpoints-in-workflows.md)   
 [Fluxos de trabalho de depuração com o Designer de Fluxo de Trabalho](../workflow-designer/debugging-workflows-with-the-workflow-designer.md)