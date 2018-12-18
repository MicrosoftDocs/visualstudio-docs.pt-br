---
title: Usar mapas de códigos para depurar aplicativos
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
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 838bf3cab092106140f3aeeaf33c74a13cd23b35
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47859660"
---
# <a name="use-code-maps-to-debug-your-applications"></a>Usar mapas de códigos para depurar aplicativos

Mapas de código podem ajudar você a evitar se perca em grandes bases de código, código não familiar ou código herdado. Por exemplo, quando você estiver depurando, você talvez precise examinar o código em vários arquivos e projetos. Usar mapas de códigos para navegar em torno de trechos de código e entender as relações entre eles. Dessa forma, você não precisa manter o controle desse código na sua cabeça ou desenhar um diagrama separado. Dessa forma, quando o trabalho for interrompido, os mapas de código ajudarão a atualizar sua memória sobre o código que você está trabalhando.

![Mapa de código &#45; mapear relacionamentos no código](../modeling/media/codemapstoryboardpaint.png)

**Uma seta verde mostra onde o cursor é exibido no editor**

Para obter detalhes sobre os comandos e ações que você pode usar ao trabalhar com mapas de código, consulte [procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md).

> [!NOTE]
> Para criar e editar os mapas de código, é necessário o Visual Studio Enterprise edition. No Visual Studio Community e Professional Edition, você pode abrir diagramas gerados no Enterprise edition, mas você não pode editá-los.

## <a name="understand-the-problem"></a>Compreender o problema
 Suponhamos que haja um bug em um programa de desenho no qual você está trabalhando. Para reproduzir o bug, você deve abrir a solução no Visual Studio e pressione **F5** para iniciar a depuração.

 Quando você desenhar uma linha e escolha **desfazer meu último traço**, nada acontecerá até você desenha a próxima linha.

 ![Mapa de código &#45; bug de reprodução](../modeling/media/codemapstoryboardpaint0.png)

 Assim, você começa a investigação procurando o método `Undo`. Você o encontra na classe `PaintCanvas`.

 ![Mapa de código &#45; localizar código](../modeling/media/codemapstoryboardpaint1.png)

## <a name="start-mapping-the-code"></a>Começar a mapear o código
 Agora começar a mapear o `undo` método e suas relações. No editor de códigos, você adiciona o método `undo` e os campos aos quais faz referência a um novo mapa de códigos. Quando você cria um novo mapa, ele pode demorar algum tempo para indexar o código. Isso ajuda a executar mais rapidamente as operações posteriores.

 ![Mapa de código &#45; Mostrar campos relacionados e método](../modeling/media/codemapstoryboardpaint3.png)

> [!TIP]
> O realce verde mostra os últimos itens que foram adicionados ao mapa. A seta verde mostra a posição do cursor no código. As setas entre os itens representam relações diferentes. Você pode obter mais informações sobre itens no mapa movendo o mouse sobre eles e examinando suas dicas de ferramenta.

 ![Mapa de código &#45; Mostrar dicas de ferramenta](../modeling/media/codemapstoryboardpaint4.png)

## <a name="navigate-and-examine-code-from-the-map"></a>Navegar e examinar o código no mapa
 Para ver a definição de código para cada campo, clique duas vezes no campo no mapa ou selecione o campo e pressione **F12**. A seta verde alterna itens no mapa. O cursor no editor de códigos também se move automaticamente.

 ![Mapa de código &#45; examinar a definição de campo](../modeling/media/codemapstoryboardpaint5.png)

 ![Mapa de código &#45; examinar a definição de campo](../modeling/media/codemapstoryboardpaint5a.png)

> [!TIP]
> Também é possível mover a seta verde no mapa movendo-se o cursor no editor de códigos.

## <a name="understand-relationships-between-pieces-of-code"></a>Compreender as relações entre as partes do código
 Agora você deseja saber qual o outro código interage com os campos `history` e `paintObjects`. É possível adicionar todos os métodos que referenciam esses campos no mapa. Você pode fazer isso do mapa ou do editor de códigos.

 ![Mapa de código &#45; localizar todas as referências](../modeling/media/codemapstoryboardpaint6.png)

 ![Abra um mapa de código do editor de códigos](../modeling/media/codemapstoryboardpaint6a.png)

> [!NOTE]
> Se você adicionar itens de um projeto que é compartilhado entre vários aplicativos, como Windows Phone ou Windows Store, em seguida, esses itens são sempre exibidos com o projeto de aplicativo atualmente ativo no mapa. Portanto, se você alterar o contexto para outro projeto de aplicativo, também altera o contexto no mapa para alguns recentemente adicionados itens do projeto compartilhado. Operações realizadas com um item no mapa se aplicam apenas aos itens que compartilham o mesmo contexto.

 Altere o layout para reorganizar o fluxo de relações e para facilitar a leitura do mapa. Também é possível mover itens pelo mapa arrastando-os.

 ![Mapa de código &#45; alterar o layout](../modeling/media/codemapstoryboardpaint7a.png)

> [!TIP]
> Por padrão, **Layout Incremental** está ativado. Isso reorganiza o mapa o menos possível quando você adiciona novos itens. Para reorganizar o mapa inteiro sempre que você adicionar novos itens, desative **Layout Incremental**.

 ![Mapa de código &#45; alterar o layout](../modeling/media/codemapstoryboardpaint7.png)

 Vamos examinar esses métodos. No mapa, clique duas vezes o **PaintCanvas** método, ou selecione esse método e pressione **F12**. Você aprende que esse método cria `history` e `paintObjects` como listas vazias.

 ![Mapa de código &#45; examinar a definição de método](../modeling/media/codemapstoryboardpaint8.png)

 Agora repita as mesmas etapas para examinar a definição do método `clear`. Você aprende que `clear` realiza algumas tarefas com `paintObjects` e `history`. Em seguida, ele chama o método `Repaint`.

 ![Mapa de código &#45; examinar a definição de método](../modeling/media/codemapstoryboardpaint9.png)

 Agora examine a definição do método `addPaintObject`. Ele também realiza algumas tarefas com `history` e `paintObjects`. Ele também chama `Repaint`.

 ![Mapa de código &#45; examinar a definição de método](../modeling/media/codemapstoryboardpaint10.png)

## <a name="find-the-problem-by-examining-the-map"></a>Encontre o problema examinando o mapa
 Aparentemente, todos os métodos que modificam `history` e `paintObjects` chamam `Repaint`. Ainda assim, o método `undo` não chama `Repaint`, mesmo que `undo` modifique os mesmos campos. Então você acha que é possível corrigir esse problema chamando `Repaint` em `undo`.

 ![Mapa de código &#45; localizar ausente chamada de método](../modeling/media/codemapstoryboardpaint11.png)

 Se você não tivesse um mapa para mostrar essa chamada perdida, poderia ser bem mais difícil encontrar esse problema, especialmente com um código mais complexo.

## <a name="share-your-discovery-and-next-steps"></a>Compartilhar a descoberta e as próximas etapas
 Antes de você ou alguma outra pessoa corrigir esse bug, é possível fazer anotações no mapa sobre o problema e como corrigi-lo.

 ![Mapa de código &#45; itens de comentário e o sinalizador para acompanhamento](../modeling/media/codemapstoryboardpaint12.png)

 Por exemplo, é possível adicionar comentários ao mapa e sinalizar itens usando cores.

 ![Mapa de código &#45; comentada e itens sinalizados](../modeling/media/codemapstoryboardpaint12a.png)

 Se tiver o Microsoft Outlook instalado, você poderá enviar por email o mapa para outras pessoas. Também é possível exportar o mapa como uma imagem ou em outro formato.

 ![Mapa de código &#45; compartilhamento de exportação, o email](../modeling/media/codemapstoryboardpaint13.png)

## <a name="fix-the-problem-and-show-what-you-did"></a>Corrigir o problema e mostrar o que você fez
 Para corrigir esse bug, adicione a chamada de `Repaint` ao `undo`.

 ![Mapa de código &#45; adicionar a chamada de método ausente](../modeling/media/codemapstoryboardpaint14.png)

 Para confirmar a correção, reinicie a sessão de depuração e tente reproduzir o erro. Agora escolher **desfazer meu último traço** funciona conforme o esperado e confirma que você fez a correção certa.

 ![Mapa de código &#45; confirmar correção de código](../modeling/media/codemapstoryboardpaint15.png)

 É possível atualizar o mapa para mostrar a correção feita.

 ![Mapa de código &#45; mapa de atualização com a ausência de chamada de método](../modeling/media/codemapstoryboardpaint16.png)

 O mapa agora mostra um link entre **desfazer** e **redesenhar**.

 ![Mapa de código &#45; mapa atualizado com a chamada de método](../modeling/media/codemapstoryboardpaint17.png)

> [!NOTE]
> Ao atualizar o mapa, você talvez veja uma mensagem afirmando que o índice de código usado para criar o mapa foi atualizado. Isso significa que alguém alterou o código, o que faz o mapa não corresponder ao código atual. Isso não impede você de atualizar o mapa, mas talvez precise recriar o mapa para confirmar se ele corresponde ao código.

 Agora você concluiu sua investigação. Você encontrou e corrigiu o problema com êxito mapeando o código. Você também tem um mapa que ajuda a navegar no código, lembrar o que aprendeu e mostra as etapas que você seguiu para corrigir o problema.

## <a name="see-also"></a>Consulte também

- [Mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)
- [Visualizar código](../modeling/visualize-code.md)
