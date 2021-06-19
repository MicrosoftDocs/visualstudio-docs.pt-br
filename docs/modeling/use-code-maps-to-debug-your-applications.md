---
title: Usar mapas de códigos para depurar aplicativos
description: Saiba como usar mapas de código para ajudá-lo a evitar se perder em grandes bases de código, código desconhecido ou código herddo.
ms.custom: SEO-VS-2020
ms.date: 09/28/2018
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Ultimate, visualizing code
- Visual Studio Ultimate, navigating code visually
- Visual Studio Ultimate, understanding code
- Visual Studio Ultimate, mapping code relationships
- Visual Studio Ultimate, code maps
- mapping code relationships
- code maps
- mapping relationships in code
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 23d05240208c6160968ae0013acfdb9f2a25c973
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388549"
---
# <a name="use-code-maps-to-debug-your-applications"></a>Usar mapas de códigos para depurar aplicativos

[Os mapas de Visual Studio](../modeling/map-dependencies-across-your-solutions.md) podem ajudá-lo a evitar se perder em grandes bases de código, código desconhecido ou código herddo. Por exemplo, ao depurar, talvez seja preciso ver o código em vários arquivos e projetos. Use mapas de código para navegar pelos trechos de código e entender as relações entre eles. Dessa forma, você não precisa manter o controle desse código na sua cabeça nem desenhar um diagrama separado. Portanto, quando seu trabalho é interrompido, os mapas de código ajudam a atualizar sua memória sobre o código no qual você está trabalhando.

![Mapa de código &#45; mapear relações no código](../modeling/media/codemapstoryboardpaint.png)

**Uma seta verde mostra onde o cursor aparece no editor**

Para obter detalhes dos comandos e ações que você pode usar ao trabalhar com mapas de código, consulte Procurar [e reorganizar mapas de código.](../modeling/browse-and-rearrange-code-maps.md)

Saiba mais sobre [a depuração no Visual Studio com a ferramenta de depurador](../debugger/debugger-feature-tour.md).

> [!NOTE]
> Para criar e editar mapas de código, você precisa Visual Studio Enterprise edição. Nas Visual Studio Community e Professional, você pode abrir diagramas que foram gerados na Edição Enterprise, mas não pode editá-los.

## <a name="understand-the-problem"></a>Compreender o problema
 Suponhamos que haja um bug em um programa de desenho no qual você está trabalhando. Para reproduzir o bug, abra a solução no Visual Studio pressione **F5** para iniciar a depuração.

 Quando você desenha uma linha e escolhe **Desfazer meu último traço,** nada acontece até que você desenhe a próxima linha.

 ![Mapa de código &#45; Bug de reprodução](../modeling/media/codemapstoryboardpaint0.png)

 Assim, você começa a investigação procurando o método `Undo`. Você o encontra na classe `PaintCanvas`.

 ![Mapa de código &#45; Encontrar código](../modeling/media/codemapstoryboardpaint1.png)

## <a name="start-mapping-the-code"></a>Começar a mapear o código
 Agora, comece a mapear `undo` o método e suas relações. No editor de códigos, você adiciona o método `undo` e os campos aos quais faz referência a um novo mapa de códigos. Quando você cria um novo mapa, ele pode demorar algum tempo para indexar o código. Isso ajuda a executar mais rapidamente as operações posteriores.

 ![Mapa de código &#45; Mostrar método e campos relacionados](../modeling/media/codemapstoryboardpaint3.png)

> [!TIP]
> O realce verde mostra os últimos itens que foram adicionados ao mapa. A seta verde mostra a posição do cursor no código. As setas entre os itens representam relações diferentes. Você pode obter mais informações sobre itens no mapa movendo o mouse sobre eles e examinando suas dicas de ferramenta.

 ![Mapa de código &#45; Mostrar dicas de ferramenta](../modeling/media/codemapstoryboardpaint4.png)

## <a name="navigate-and-examine-code-from-the-map"></a>Navegar e examinar o código no mapa
 Para ver a definição de código para cada campo, clique duas vezes no campo no mapa ou selecione o campo e pressione **F12**. A seta verde alterna itens no mapa. O cursor no editor de códigos também se move automaticamente.

 ![Captura de tela de uma janela de mapa de código com o campo histórico selecionado e uma janela do editor de códigos em que todas as instâncias do histórico são realçadas.](../modeling/media/codemapstoryboardpaint5.png)

 ![Captura de tela de uma janela de mapa de código com o campo paintObjects selecionado e uma janela do editor de códigos em que todas as instâncias de paintObjects estão realçadas.](../modeling/media/codemapstoryboardpaint5a.png)

> [!TIP]
> Também é possível mover a seta verde no mapa movendo-se o cursor no editor de códigos.

## <a name="understand-relationships-between-pieces-of-code"></a>Compreender as relações entre as partes do código
 Agora você deseja saber qual o outro código interage com os campos `history` e `paintObjects`. É possível adicionar todos os métodos que referenciam esses campos no mapa. Você pode fazer isso no mapa ou no editor de códigos.

 ![Mapa de código &#45; Encontrar todas as referências](../modeling/media/codemapstoryboardpaint6.png)

 ![Abrir um mapa de código no editor de códigos](../modeling/media/codemapstoryboardpaint6a.png)

> [!NOTE]
> Se você adicionar itens de um projeto compartilhado entre vários aplicativos, como Windows Phone ou Windows Store, esses itens sempre aparecerão com o projeto de aplicativo ativo no mapa no momento. Portanto, se você alterar o contexto para outro projeto de aplicativo, o contexto no mapa também mudará para os itens recém-adicionados do projeto compartilhado. Operações realizadas com um item no mapa se aplicam apenas aos itens que compartilham o mesmo contexto.

 Altere o layout para reorganizar o fluxo de relações e para facilitar a leitura do mapa. Também é possível mover itens pelo mapa arrastando-os.

 ![Captura de tela de uma janela de mapa de código com o menu Layout aberto e o comando Left to Rgiht selecionado.](../modeling/media/codemapstoryboardpaint7a.png)

> [!TIP]
> Por padrão, **o Layout Incremental** é ligado. Isso reorganiza o mapa o menos possível quando você adiciona novos itens. Para reorganizar todo o mapa sempre que você adicionar novos itens, desligue o **Layout Incremental.**

 ![Captura de tela de uma janela de mapa de código com as setas de relaçõeshiop entre os campos apontando da esquerda para a direita.](../modeling/media/codemapstoryboardpaint7.png)

 Vamos examinar esses métodos. No mapa, clique duas vezes no **método PaintCanvas** ou selecione esse método e pressione **F12**. Você aprende que esse método cria `history` e `paintObjects` como listas vazias.

 ![Captura de tela de uma janela de mapa de código com o método PaintCanvas selecionado e uma imagem de snippet de código mostrando o nome do método PainCanvas realçada.](../modeling/media/codemapstoryboardpaint8.png)

 Agora repita as mesmas etapas para examinar a definição do método `clear`. Você aprende que `clear` realiza algumas tarefas com `paintObjects` e `history`. Em seguida, ele chama o método `Repaint`.

 ![Captura de tela de uma janela de mapa de código com o método Clear selecionado e uma imagem de snippet de código mostrando o código para o método Clear.](../modeling/media/codemapstoryboardpaint9.png)

 Agora examine a definição do método `addPaintObject`. Ele também realiza algumas tarefas com `history` e `paintObjects`. Ele também chama `Repaint`.

 ![Captura de tela de uma janela de mapa de código com o método addPaintObject selecionado e uma imagem de snippet de código mostrando o código para o método addPaintObject.](../modeling/media/codemapstoryboardpaint10.png)

## <a name="find-the-problem-by-examining-the-map"></a>Encontre o problema examinando o mapa
 Aparentemente, todos os métodos que modificam `history` e `paintObjects` chamam `Repaint`. Ainda assim, o método `undo` não chama `Repaint`, mesmo que `undo` modifique os mesmos campos. Então você acha que é possível corrigir esse problema chamando `Repaint` em `undo`.

 ![Mapa de código &#45; encontrar chamada de método ausente](../modeling/media/codemapstoryboardpaint11.png)

 Se você não tivesse um mapa para mostrar essa chamada perdida, poderia ser bem mais difícil encontrar esse problema, especialmente com um código mais complexo.

## <a name="share-your-discovery-and-next-steps"></a>Compartilhar a descoberta e as próximas etapas
 Antes de você ou alguma outra pessoa corrigir esse bug, é possível fazer anotações no mapa sobre o problema e como corrigi-lo.

 ![Mapa de código &#45; itens de comentário e sinalizador para acompanhamento](../modeling/media/codemapstoryboardpaint12.png)

 Por exemplo, é possível adicionar comentários ao mapa e sinalizar itens usando cores.

 ![Mapa de código &#45; itens comentados e sinalizados](../modeling/media/codemapstoryboardpaint12a.png)

 Se tiver o Microsoft Outlook instalado, você poderá enviar por email o mapa para outras pessoas. Também é possível exportar o mapa como uma imagem ou em outro formato.

 ![Mapa de código &#45; Compartilhamento, exportação, email](../modeling/media/codemapstoryboardpaint13.png)

## <a name="fix-the-problem-and-show-what-you-did"></a>Corrigir o problema e mostrar o que você fez
 Para corrigir esse bug, adicione a chamada de `Repaint` ao `undo`.

 ![Mapa de código &#45; adicionar chamada de método ausente](../modeling/media/codemapstoryboardpaint14.png)

 Para confirmar a correção, reinicie a sessão de depuração e tente reproduzir o erro. Agora, **escolher Desfazer meu último traço** funciona conforme o esperado e confirma que você fez a correção correta.

 ![Mapa de código &#45; Confirmar correção de código](../modeling/media/codemapstoryboardpaint15.png)

 É possível atualizar o mapa para mostrar a correção feita.

 ![Mapa de código &#45; mapa de atualização com chamada de método ausente](../modeling/media/codemapstoryboardpaint16.png)

 Agora, seu mapa mostra um link entre **desfazer** **e Repaint.**

 ![Mapa de código &#45; mapa atualizado com chamada de método](../modeling/media/codemapstoryboardpaint17.png)

> [!NOTE]
> Ao atualizar o mapa, você talvez veja uma mensagem afirmando que o índice de código usado para criar o mapa foi atualizado. Isso significa que alguém alterou o código, o que faz o mapa não corresponder ao código atual. Isso não impede você de atualizar o mapa, mas talvez precise recriar o mapa para confirmar se ele corresponde ao código.

 Agora você terminou sua investigação. Você encontrou e corrigiu o problema com êxito mapeando o código. Você também tem um mapa que ajuda a navegar no código, lembrar o que aprendeu e mostra as etapas que você seguiu para corrigir o problema.

## <a name="see-also"></a>Confira também

- [Mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)
- [Visualizar código](../modeling/visualize-code.md)
