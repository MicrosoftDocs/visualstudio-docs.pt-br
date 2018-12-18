---
title: Introdução ao Spy + + | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Spy++
ms.assetid: 733b514b-63a9-402d-89aa-4f0416766655
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b5e6aecff83d745c724fa0009b33a798ae94118d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792418"
---
# <a name="introducing-spy"></a>Introdução a Spy++
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Spy + + permite que você execute as seguintes tarefas:  
  
- Exiba um gráfico de árvore de relações entre os objetos do sistema. Eles incluem [processos](../debugger/processes-view.md), [threads](../debugger/threads-view.md), e [windows](../debugger/windows-view.md).  
  
- Pesquisar para especificado [windows](../debugger/how-to-search-for-a-window-in-windows-view.md), [threads](../debugger/how-to-search-for-a-thread-in-threads-view.md), [processos](../debugger/how-to-search-for-a-process-in-processes-view.md), ou [mensagens](../debugger/how-to-search-for-a-message-in-messages-view.md).  
  
- Exibir as propriedades de selecionado [windows](../debugger/how-to-display-window-properties.md), [threads](../debugger/how-to-display-thread-properties.md), [processos](../debugger/how-to-display-process-properties.md), ou [mensagens](../debugger/how-to-display-message-properties.md).  
  
- Selecione uma janela, o thread, o processo ou a mensagem diretamente no modo de exibição.  
  
- Use o [ferramenta Descobridora](../debugger/how-to-use-the-finder-tool.md) para selecionar uma janela, o posicionamento do ponteiro do mouse.  
  
- Definir **opções de mensagem** usando parâmetros de seleção de log de mensagens complexos.  
  
  Spy + + tem uma barra de ferramentas e hiperlinks para ajudar você a trabalhar com mais rapidez. Também fornece um **Refresh** comando para atualizar a exibição ativa, um **ferramenta Descobridora de janelas** para tornar a espionagem e um **fonte** caixa de diálogo para personalizar o windows de modo de exibição. Além disso, Spy + + permite salvar e restaurar as preferências do usuário.  
  
  Em várias janelas Spy + +, você pode clique com botão direito para exibir um menu de atalho de comandos usados com frequência. Quais comandos são exibidos depende de onde é o ponteiro. Por exemplo, se o botão direito do mouse uma entrada na exibição da janela e a janela selecionada estiver visível, clique em **realçar** no atalho do menu faz com que a borda da janela selecionada para flash para que possa ser localizado com mais facilidade.  
  
> [!NOTE]
>  Há dois outros utilitários que se assemelhem a Spy + +: PView, que mostra detalhes sobre processos e threads e DDESPY. EXE, que permite que você monitore as mensagens de troca dinâmica de dados (DDE).  
  
## <a name="64-bit-operating-systems"></a>Sistemas operacionais de 64 bits  
 Há duas versões do Spy + +. A primeira versão, chamada Spy + + (spyxx.exe) é projetada para exibir as mensagens enviadas para uma janela que está em execução em um processo de 32 bits. Por exemplo, o Visual Studio é executado em um processo de 32 bits. Portanto, você pode usar Spy + + para exibir as mensagens enviadas ao **Gerenciador de soluções**. Como a configuração padrão para a maioria das compilações no Visual Studio é executado em um processo de 32 bits, essa primeira versão do Spy + + é aquele que está disponível na **ferramentas** menu do Visual Studio.  
  
 A segunda versão, chamada Spy + + (64-bit) (spyxx_amd64.exe) é projetada para exibir as mensagens enviadas para uma janela que está em execução em um processo de 64 bits. Por exemplo, em um sistema operacional de 64 bits, o bloco de notas é executado em um processo de 64 bits. Portanto, você pode usar Spy + + (64 bits) para exibir as mensagens enviadas para o bloco de notas. Spy + + (64 bits) geralmente está localizado em  
  
 .. \\ *Pasta de instalação do visual Studio*\Common7\Tools\spyxx_amd64.exe.  
  
 Você pode executar qualquer versão do Spy + + diretamente da linha de comando.  
  
> [!NOTE]
>  Embora o nome de arquivo (64 bits) do Spy + + contiver "amd", ele é executado em qualquer x64 sistema de operacional Windows.  
  
## <a name="see-also"></a>Consulte também  
 [Usando Spy + +](../debugger/using-spy-increment.md)   
 [Exibições do Spy + +](../debugger/spy-increment-views.md)   
 [Referência a Spy++](../debugger/spy-increment-reference.md)




