---
title: Mapear métodos na pilha de chamadas ao depurar
description: Saiba como criar um mapa de código para rastrear visualmente a pilha de chamada durante a depuração. Além disso, saiba que você pode fazer anotações no mapa para acompanhar o que o código está fazendo.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: faeee42f179351649ba73e06d25e5e948538392e
ms.sourcegitcommit: 398b4d4e5ce0f978720f11990db05b209766aedc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2021
ms.locfileid: "112016314"
---
# <a name="map-methods-on-the-call-stack-while-debugging-in-visual-studio"></a>Mapear métodos na pilha de chamadas ao depurar no Visual Studio

Crie um mapa de códigos para rastrear visualmente a pilha de chamadas durante a depuração. Você pode fazer anotações no mapa para acompanhar o que o código está fazendo, de modo a se concentrar na localização de bugs.

 ![Depuração com pilhas de chamada em mapas de código](../debugger/media/debuggermap_overview.png)

 Você precisará de:

 ::: moniker range="vs-2017"

- [Visual Studio Enterprise](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

::: moniker-end

::: moniker range=">=vs-2019"

- [Visual Studio Enterprise](https://visualstudio.microsoft.com/downloads)

::: moniker-end

- Código que você pode depurar, como Visual C#, Visual Basic, C++, JavaScript ou X++

  Consulte:

- [Vídeo: Depurar visualmente com a integração do depurador do Mapa de Código (Channel 9)](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012Debug-visually-with-Code-Map-debugger-integration)

- [Mapear a pilha de chamada](#MapStack)

- [Fazer anotações sobre o código](#MakeNotes)

- [Atualizar o mapa com a próxima pilha de chamada](#UpdateMap)

- [Adicionar código relacionado ao mapa](#AddRelatedCode)

- [Encontrar bugs usando o mapa](#FindBugs)

- [P & R](#QA)

  Para obter detalhes dos comandos e ações que você pode usar ao trabalhar com mapas de código, consulte Procurar [e reorganizar mapas de código.](../modeling/browse-and-rearrange-code-maps.md)

## <a name="map-the-call-stack"></a><a name="MapStack"></a> Mapear a pilha de chamadas

1. Inicie a depuração. (Teclado: **F5**)

2. Depois que o aplicativo entrar no modo de quebra ou você entrar em uma função, escolha **Mapa de Código**. (Teclado: **Ctrl**  +  **Shift**  +  **`** )

     ![Escolha Mapa de Código para iniciar a pilha de chamada de mapeamento](../debugger/media/debuggermap_choosecodemap.png)

     A pilha de chamadas atual aparece em laranja em um novo mapeamento de código:

     ![Consulte pilha de chamada no mapa de código](../debugger/media/debuggermap_seeundocallstack.png)

     O mapa será atualizado automaticamente enquanto você continua a depuração. Consulte [Atualizar o mapa com a próxima pilha de chamada](#UpdateMap).

## <a name="make-notes-about-the-code"></a><a name="MakeNotes"></a> Fazer anotações sobre o código

 Adicione comentários para acompanhar o que está acontecendo no código. Para adicionar uma nova linha em um comentário, pressione **Shift + Return**.

 ![Adicionar comentário à pilha de chamada no mapa de código](../debugger/media/debuggermap_addcomment.png)

## <a name="update-the-map-with-the-next-call-stack"></a><a name="UpdateMap"></a> Atualizar o mapa com a próxima pilha de chamadas

 Execute o aplicativo até o próximo ponto de interrupção ou siga uma função. O mapa adiciona uma nova pilha de chamadas.

 ![Atualizar o mapa de código com a próxima pilha de chamada](../debugger/media/debuggermap_addclearcallstack.png)

## <a name="add-related-code-to-the-map"></a><a name="AddRelatedCode"></a> Adicionar código relacionado ao mapa

 Agora você tem um mapa – o que vem a seguir? Se você estiver trabalhando com C# ou Visual Basic, adicione itens, como campos, propriedades e outros métodos, para acompanhar o que está acontecendo no código.

 Clique duas vezes em um método para ver sua definição de código ou use o menu de atalho para o método . (Teclado: selecione o método no mapa e pressione **F12**)

 ![Ir para a definição de código para um método no mapa de código](../debugger/media/debuggermap_gotocodedefinition.png)

 Adicione os itens que você deseja rastrear no mapa.

 ![Mostrar campos em um método no mapa de código da pilha de chamada](../debugger/media/debuggermap_showfields.png)

> [!NOTE]
> Por padrão, adicionar itens ao mapa também adiciona os nós de grupo pai, como a classe, o namespace e o assembly. Embora isso seja útil, você pode manter o mapa  simples, desligando esse recurso usando o botão Incluir Pais na barra de ferramentas do mapa ou pressionando **CTRL** ao adicionar itens.

 ![Campos relacionados a um método no mapa de código da pilha de chamada](../debugger/media/debuggermap_showedfields.png)

 Aqui, você pode visualizar facilmente quais métodos usam os mesmos campos. Os itens mais recentemente adicionados aparecem em verde.

 Continue criando o mapa para ver mais código.

 ![Consulte métodos que usam um campo: mapa de código da pilha de chamada](../debugger/media/debuggermap_findallreferences.png)

 ![Métodos que usam um campo no mapa de código da pilha de chamada](../debugger/media/debuggermap_foundallreferences.png)

## <a name="find-bugs-using-the-map"></a><a name="FindBugs"></a> Localizar bugs usando o mapa

 Visualizar seu código pode ajudar a localizar bugs com mais rapidez. Por exemplo, suponha que você esteja investigando um bug em um programa de desenho. Quando você desenha uma linha e tenta desfazê-la, nada acontece até que você desenhe outra linha.

 Portanto, você definirá pontos de interrupção nos métodos `clear` `undo` , e , iniciará a depuração e criará `Repaint` um mapa como este:

 ![Adicionar outra pilha de chamada ao mapa de código](../debugger/media/debuggermap_addpaintobjectcallstack.png)

 Você observará que todos os gestos do usuário no mapa chamam `Repaint`, exceto para `undo`. Isso pode explicar o motivo de `undo` não funcionar imediatamente.

 Após corrigir o bug e continuar executando o programa, o mapa adicionará a nova chamada de `undo` para `Repaint`:

 ![Adicionar nova chamada de método para pilha de chamada no mapa de código](../debugger/media/debuggermap_addnewcallforrepaint.png)

## <a name="q--a"></a><a name="QA"></a> P & A

- **Nem todas as chamadas aparecem no mapa. Porque?**

   Por padrão, somente seu próprio código aparece no mapa. Para ver o código externo, a ligue na janela **Pilha de** Chamada:

   ![Exibir código externo usando a janela Pilha de Chamada](../debugger/media/debuggermap_callstackmenu.png)

   ou desligue **Habilitar Apenas Meu Código** nas opções Visual Studio depuração:

   ![Mostrar código externo usando a caixa de diálogo Opções](../debugger/media/debuggermap_debugoptions.png)

- **Alterar o mapa afeta o código?**

   Alterar o mapa não afeta o código de forma alguma. Sinta-se à vontade para renomear, mover ou remover qualquer item no mapa.

- **O que essa mensagem significa: "O diagrama pode ser baseado em uma versão mais antiga do código"?**

   O código pode ter sido alterado depois que você alterou o mapa pela última vez. Por exemplo, uma chamada no mapa pode não existir mais no código. Feche a mensagem e tente recriar a solução antes de atualizar o mapa outra vez.

- **Como fazer controlar o layout do mapa?**

   Abra o menu **Layout** na barra de ferramentas do mapa:

  - Altere o layout padrão.

  - Para parar de reorganizar o mapa automaticamente, desligue o **Layout Automático ao Depurar**.

  - Para reorganizar o mapa o menos possível ao adicionar itens, desligue o **Layout Incremental**.

- **Posso compartilhar o mapa com outras pessoas?**

   Você pode exportar o mapa, enviá-lo para outras pessoas se você tiver o Microsoft Outlook ou salvá-lo em sua solução para poder fazer check-in no controle do código-fonte.

   ![Compartilhar mapa de código da pilha de chamada com outras pessoas](../debugger/media/debuggermap_sharewithothers.png)

- **Como fazer com que o mapa pare de adicionar novas pilhas de chamadas automaticamente?**

   Escolha ![ Botão &#45; Mostrar pilha de chamada no mapa de código ](../debugger/media/debuggermap_automaticupdateicon.gif) automaticamente na barra de ferramentas do mapa. Para adicionar manualmente a pilha de chamada atual ao mapa, pressione **Ctrl**  +  **Shift**  +  **`** .

   O mapa continuará realçando as pilhas de chamada existentes no mapa enquanto você estiver depurando.

- **Qual é o significado das setas e dos ícones de item?**

   Para obter mais informações sobre um item, mova o ponteiro do mouse sobre ele e veja a dica de ferramenta do item. Você também pode ver a Legenda **para** saber o que cada ícone significa.

   ![O que significam os ícones no mapa de código da pilha de chamada?](../debugger/media/debuggermap_showlegend.png)

  Consulte:

- [Mapear a pilha de chamada](#MapStack)

- [Fazer anotações sobre o código](#MakeNotes)

- [Atualizar o mapa com a próxima pilha de chamada](#UpdateMap)

- [Adicionar código relacionado ao mapa](#AddRelatedCode)

- [Encontrar bugs usando o mapa](#FindBugs)

## <a name="see-also"></a>Confira também

- [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)
- [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)
- [Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)
- [Procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md)
