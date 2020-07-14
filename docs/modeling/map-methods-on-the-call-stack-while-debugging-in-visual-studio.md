---
title: Mapear métodos na pilha de chamadas ao depurar
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.progression.debugwithcodemaps
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- call stacks, code maps
- Call Stack window, mapping calls
- debugging [Visual Studio], diagramming the call stack
- call stacks, mapping
- Call Stack window, visualizing
- debugging code visually
- debugging [Visual Studio], mapping the call stack
- call stacks, visualizing
- debugging, code maps
- Call Stack window, tracing calls visually
- Call Stack window, show on code map
- debugging [Visual Studio], tracing the call stack visually
- debugging [Visual Studio], visualizing the call stack
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e1638b16eea9bfa20962359f0b63a7415915d0fc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85532698"
---
# <a name="map-methods-on-the-call-stack-while-debugging-in-visual-studio"></a>Mapear métodos na pilha de chamadas ao depurar no Visual Studio

Crie um mapa de códigos para rastrear visualmente a pilha de chamadas durante a depuração. Você pode fazer anotações no mapa para acompanhar o que o código está fazendo, de modo a se concentrar na localização de bugs.

 ![Depuração com pilhas de chamadas em mapas de código](../debugger/media/debuggermap_overview.png)

 Você precisará de:

 ::: moniker range="vs-2017"

- [Visual Studio Enterprise](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

::: moniker-end

::: moniker range="vs-2019"

- [Visual Studio Enterprise](https://visualstudio.microsoft.com/downloads)

::: moniker-end

- Código que você pode depurar, como Visual C#, Visual Basic, C++, JavaScript ou X + +

  Consulte:

- [Vídeo: Depurar visualmente com a integração do depurador do mapa de código (canal 9)](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012Debug-visually-with-Code-Map-debugger-integration)

- [Mapear a pilha de chamadas](#MapStack)

- [Faça observações sobre o código](#MakeNotes)

- [Atualizar o mapa com a próxima pilha de chamadas](#UpdateMap)

- [Adicionar código relacionado ao mapa](#AddRelatedCode)

- [Localizar bugs usando o mapa](#FindBugs)

- [P & A](#QA)

  Para obter detalhes dos comandos e ações que você pode usar ao trabalhar com mapas de código, consulte [procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md).

## <a name="map-the-call-stack"></a><a name="MapStack"></a> Mapear a pilha de chamadas

1. Inicie a depuração. (Teclado: **F5**)

2. Depois que o aplicativo entrar no modo de interrupção ou você entrar em uma função, escolha **mapa de código**. (Teclado: **Ctrl**  +  **Shift**  +  **`** )

     ![Escolha o mapa de código para iniciar o mapeamento da pilha de chamadas](../debugger/media/debuggermap_choosecodemap.png)

     A pilha de chamadas atual aparece em laranja em um novo mapeamento de código:

     ![Consulte pilha de chamadas no mapa de códigos](../debugger/media/debuggermap_seeundocallstack.png)

     O mapa será atualizado automaticamente enquanto você continua a depuração. Consulte [atualizar o mapa com a próxima pilha de chamadas](#UpdateMap).

## <a name="make-notes-about-the-code"></a><a name="MakeNotes"></a> Fazer anotações sobre o código

 Adicione comentários para acompanhar o que está acontecendo no código. Para adicionar uma nova linha em um comentário, pressione **Shift + Return**.

 ![Adicionar comentário à pilha de chamadas no mapa de códigos](../debugger/media/debuggermap_addcomment.png)

## <a name="update-the-map-with-the-next-call-stack"></a><a name="UpdateMap"></a> Atualizar o mapa com a próxima pilha de chamadas

 Execute o aplicativo até o próximo ponto de interrupção ou siga uma função. O mapa adiciona uma nova pilha de chamadas.

 ![Atualizar mapa de códigos com a próxima pilha de chamadas](../debugger/media/debuggermap_addclearcallstack.png)

## <a name="add-related-code-to-the-map"></a><a name="AddRelatedCode"></a> Adicionar código relacionado ao mapa

 Agora você tem um mapa, o que vem a seguir? Se você estiver trabalhando com C# ou Visual Basic, adicione itens, como campos, propriedades e outros métodos, para controlar o que está acontecendo no código.

 Clique duas vezes em um método para ver sua definição de código ou use o menu de atalho para o método. (Teclado: selecione o método no mapa e pressione **F12**)

 ![Ir para a definição de código de um método no mapa de códigos](../debugger/media/debuggermap_gotocodedefinition.png)

 Adicione os itens que você deseja rastrear no mapa.

 ![Mostrar campos em um método no mapa de códigos de pilha de chamadas](../debugger/media/debuggermap_showfields.png)

> [!NOTE]
> Por padrão, a adição de itens ao mapa também adiciona os nós do grupo pai, como a classe, o namespace e o assembly. Embora isso seja útil, você pode manter o mapa simples desativando esse recurso usando o botão **incluir pais** na barra de ferramentas do mapa ou pressionando **Ctrl** ao adicionar itens.

 ![Campos relacionados a um método no mapa de códigos de pilha de chamadas](../debugger/media/debuggermap_showedfields.png)

 Aqui, você pode visualizar facilmente quais métodos usam os mesmos campos. Os itens mais recentemente adicionados aparecem em verde.

 Continue criando o mapa para ver mais código.

 ![Consulte métodos que usam um campo: mapa de códigos de pilha de chamadas](../debugger/media/debuggermap_findallreferences.png)

 ![Métodos que usam um campo no mapa de códigos de pilha de chamadas](../debugger/media/debuggermap_foundallreferences.png)

## <a name="find-bugs-using-the-map"></a><a name="FindBugs"></a> Localizar bugs usando o mapa

 Visualizar seu código pode ajudar a localizar bugs com mais rapidez. Por exemplo, suponha que você esteja investigando um bug em um programa de desenho. Quando você desenha uma linha e tenta desfazê-la, nada acontece até que você desenhe outra linha.

 Portanto, você define pontos de interrupção `clear` nos `undo` métodos, e `Repaint` , inicia a depuração e cria um mapa como este:

 ![Adicionar outra pilha de chamadas ao mapa de códigos](../debugger/media/debuggermap_addpaintobjectcallstack.png)

 Você observará que todos os gestos do usuário no mapa chamam `Repaint`, exceto para `undo`. Isso pode explicar o motivo de `undo` não funcionar imediatamente.

 Após corrigir o bug e continuar executando o programa, o mapa adicionará a nova chamada de `undo` para `Repaint`:

 ![Adicionar nova chamada de método para pilha de chamadas no mapa de códigos](../debugger/media/debuggermap_addnewcallforrepaint.png)

## <a name="q--a"></a><a name="QA"></a>P & A

- **Nem todas as chamadas aparecem no mapa. Por?**

   Por padrão, apenas seu próprio código aparece no mapa. Para ver o código externo, ative-o na janela **pilha de chamadas** :

   ![Exibir código externo usando a janela pilha de chamadas](../debugger/media/debuggermap_callstackmenu.png)

   ou desative a opção **habilitar apenas meu código** nas opções de depuração do Visual Studio:

   ![Mostrar código externo usando a caixa de diálogo opções](../debugger/media/debuggermap_debugoptions.png)

- **Alterar o mapa afeta o código?**

   A alteração do mapa não afeta o código de forma alguma. Sinta-se à vontade para renomear, mover ou remover qualquer item no mapa.

- **O que significa essa mensagem: "o diagrama pode ser baseado em uma versão mais antiga do código"?**

   O código pode ter sido alterado depois que você alterou o mapa pela última vez. Por exemplo, uma chamada no mapa pode não existir mais no código. Feche a mensagem e tente recriar a solução antes de atualizar o mapa outra vez.

- **Como fazer controlar o layout do mapa?**

   Abra o menu **layout** na barra de ferramentas do mapa:

  - Altere o layout padrão.

  - Para parar de reorganizar o mapa automaticamente, desative o **layout automaticamente durante a depuração**.

  - Para reorganizar o mapa o mínimo possível ao adicionar itens, desative o **layout incremental**.

- **Posso compartilhar o mapa com outras pessoas?**

   Você pode exportar o mapa, enviá-lo para outras pessoas se tiver o Microsoft Outlook ou salvá-lo em sua solução para que você possa verificá-lo no controle do código-fonte.

   ![Compartilhar mapa de código de pilha de chamadas com outras pessoas](../debugger/media/debuggermap_sharewithothers.png)

- **Como fazer com que o mapa pare de adicionar novas pilhas de chamadas automaticamente?**

   Escolha ![ o botão &#45; mostrar pilha de chamadas no mapa de códigos automaticamente ](../debugger/media/debuggermap_automaticupdateicon.gif) na barra de ferramentas do mapa. Para adicionar manualmente a pilha de chamadas atual ao mapa, pressione **Ctrl**  +  **Shift**  +  **`** .

   O mapa continuará realçando as pilhas de chamadas existentes no mapa enquanto você estiver depurando.

- **Qual é o significado das setas e dos ícones de item?**

   Para obter mais informações sobre um item, mova o ponteiro do mouse sobre ele e examine a dica de ferramenta do item. Você também pode examinar a **legenda** para saber o que significa cada ícone.

   ![O que os ícones no mapa de códigos da pilha de chamadas significam?](../debugger/media/debuggermap_showlegend.png)

  Consulte:

- [Mapear a pilha de chamadas](#MapStack)

- [Faça observações sobre o código](#MakeNotes)

- [Atualizar o mapa com a próxima pilha de chamadas](#UpdateMap)

- [Adicionar código relacionado ao mapa](#AddRelatedCode)

- [Localizar bugs usando o mapa](#FindBugs)

## <a name="see-also"></a>Confira também

- [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)
- [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)
- [Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)
- [Procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md)
