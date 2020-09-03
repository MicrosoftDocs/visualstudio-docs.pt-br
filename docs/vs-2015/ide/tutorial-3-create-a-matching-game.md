---
title: 'Tutorial 3: criar um jogo da memória | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 525815c8-2845-45e8-be96-100d1f144725
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 30ee029fe231202c821c8448d3594192b5ebfdf8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "74299855"
---
# <a name="tutorial-3-create-a-matching-game"></a>Tutorial 3: criar um jogo da memória
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Neste tutorial, você cria um jogo da memória, onde o jogador deve combinar pares de ícones ocultos. Você aprenderá como:

- Armazenar objetos, como ícones, em um objeto `List`.

- Usar um loop `foreach` no Visual C# ou um loop `For Each` no Visual Basic para iterar pelos itens em uma lista.

- Acompanhar o estado de um formulário usando variáveis de referência.

- Criar um manipulador de eventos para responder a eventos que você pode usar com vários objetos.

- Criar um temporizador que faça a contagem regressiva e dispare um evento logo depois que ele for iniciado.

  Quando terminar este tutorial, seu programa se parecerá com a imagem a seguir.

  ![Jogo que você cria neste tutorial](../ide/media/express-finishedgame.png "Express_FinishedGame") Jogo que você cria neste tutorial

> [!NOTE]
> Neste tutorial, o Visual C# e o Visual Basic são abordados, portanto concentre-se nas informações específicas da linguagem de programação que você está usando.

 Se você estiver com dificuldades ou tiver dúvidas quanto à programação, tente publicar sua dúvida em um dos fóruns do MSDN. Consulte [Fórum do Visual Basic](https://social.msdn.microsoft.com/Forums/en-US/home) e [Fórum do Visual C#](https://social.msdn.microsoft.com/Forums/en-US/home). Além disso, há recursos de aprendizagem por vídeo excelentes e gratuitos disponíveis para você. Para saber mais sobre programação em Visual Basic, consulte [conceitos básicos de Visual Basic: desenvolvimento para iniciantes absolutos](https://channel9.msdn.com/Series/Visual-Basic-Development-for-Absolute-Beginners). Para saber mais sobre programação no Visual C#, consulte [C# Fundamentals: Development for Absolute Beginners (Conceitos básicos do C#: desenvolvimento para iniciantes absolutos)](https://channel9.msdn.com/Series/C-Sharp-Fundamentals-Development-for-Absolute-Beginners).

## <a name="related-topics"></a>Tópicos relacionados

|Título|Descrição|
|-----------|-----------------|
|[Etapa 1: criar um projeto e adicionar uma tabela ao formulário](../ide/step-1-create-a-project-and-add-a-table-to-your-form.md)|Comece criando o projeto e adicionando um controle `TableLayoutPanel` para manter os controles devidamente alinhados.|
|[Etapa 2: adicionar um objeto aleatório e uma lista de ícones](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)|Adicione um objeto `Random` e um objeto `List` para criar uma lista de ícones.|
|[Etapa 3: atribuir um ícone aleatório a cada rótulo](../ide/step-3-assign-a-random-icon-to-each-label.md)|Atribua os ícones aleatoriamente aos controles `Label` para que cada jogo seja diferente.|
|[Etapa 4: adicionar um manipulador de eventos de clique a cada rótulo](../ide/step-4-add-a-click-event-handler-to-each-label.md)|Adicione um manipulador de eventos Click que altere a cor do rótulo que é clicado.|
|[Etapa 5: adicionar referências de rótulo](../ide/step-5-add-label-references.md)|Adicione variáveis de referência para acompanhar quais rótulos são clicados.|
|[Etapa 6: adicionar um temporizador](../ide/step-6-add-a-timer.md)|Adicione um temporizador ao formulário para controlar o tempo que passou no jogo.|
|[Etapa 7: manter os pares visíveis](../ide/step-7-keep-pairs-visible.md)|Mantenha pares de ícones visíveis, se um par correspondente for selecionado.|
|[Etapa 8: adicionar um método para verificar se o jogador venceu](../ide/step-8-add-a-method-to-verify-whether-the-player-won.md)|Adicione um método `CheckForWinner()` para verificar se o jogador venceu.|
|[Etapa 9: Experimente outros recursos](../ide/step-9-try-other-features.md)|Teste outros recursos, como alterar ícones e cores, adicionar uma grade e adicionar sons. Tente aumentar o tamanho do tabuleiro e ajustar o temporizador.|
