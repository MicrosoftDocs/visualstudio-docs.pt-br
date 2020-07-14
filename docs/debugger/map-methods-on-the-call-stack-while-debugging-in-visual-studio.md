---
title: Criar um mapa Visual da pilha de chamadas | Microsoft Docs
ms.date: 11/26/2018
ms.topic: how-to
f1_keywords:
- vs.progression.debugwithcodemaps
dev_langs:
- CSharp
- VB
- FSharp
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
ms.assetid: d6a72e5e-f88d-46fc-94a3-1789d34805ef
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2cf0cda942241ca77aa750624b6de25b5ae39391
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348529"
---
# <a name="create-a-visual-map-of-the-call-stack-while-debugging-c-visual-basic-c-javascript"></a>Criar um mapa Visual da pilha de chamadas durante a depuração (C#, Visual Basic, C++, JavaScript)

Crie um mapa de códigos para rastrear visualmente a pilha de chamadas durante a depuração. Você pode fazer anotações no mapa para acompanhar o que o código está fazendo, de modo a se concentrar na localização de bugs.

Para obter instruções, assista a este vídeo: [Vídeo: Depurar visualmente com a integração do depurador mapa de códigos (Channel 9)](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012Debug-visually-with-Code-Map-debugger-integration)

Para obter detalhes de comandos e ações que você pode usar com mapas de código, consulte [procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md).

>[!IMPORTANT]
>Você pode criar mapas de código somente no [Visual Studio Enterprise Edition](https://visualstudio.microsoft.com/downloads).

Aqui está uma visão rápida de um mapa de código:

 ![Depuração com pilhas de chamadas em mapas de código](../debugger/media/debuggermap_overview.png "DebuggerMap_Overview")

## <a name="map-the-call-stack"></a><a name="MapStack"></a> Mapear a pilha de chamadas

1. Em um projeto Visual Studio Enterprise C#, Visual Basic, C++ ou JavaScript, inicie a depuração selecionando **depurar**  >  **Iniciar Depuração** ou pressionando **F5**.

1. Depois que o aplicativo entrar no modo de interrupção ou você entrar em uma função, selecione **depurar**  >  **mapa de código**ou pressione **Ctrl** + **Shift** + **`** .

   A pilha de chamadas atual aparece em laranja em um novo mapeamento de código:

   ![Consulte pilha de chamadas no mapa de códigos](../debugger/media/debuggermap_seeundocallstack.png "DebuggerMap_SeeUndoCallStack")

O mapa de código é atualizado automaticamente conforme você continua a depuração. A alteração de itens ou layout de mapa não afeta o código de forma alguma. Sinta-se à vontade para renomear, mover ou remover qualquer item no mapa.

Para obter mais informações sobre um item, passe o mouse sobre ele e examine a dica de ferramenta do item. Você também pode selecionar **legenda** na barra de ferramentas para saber o que significa cada ícone.

![Legenda do mapa de código](../debugger/media/debuggermap_showlegend.png "Legenda do mapa de código")

>[!NOTE]
>A mensagem **o diagrama pode ser baseado em uma versão mais antiga do código** na parte superior do mapa de código significa que o código pode ter mudado após a última atualização do mapa. Por exemplo, uma chamada no mapa pode não existir mais no código. Feche a mensagem e tente recriar a solução antes de atualizar o mapa outra vez.

## <a name="map-external-code"></a>Mapear código externo

Por padrão, apenas seu próprio código aparece no mapa. Para ver o código externo no mapa:

- Clique com o botão direito do mouse na janela **pilha de chamadas** e selecione **Mostrar código externo**:

  ![Exibir código externo usando a janela pilha de chamadas](../debugger/media/debuggermap_callstackmenu.png "DebuggerMap_CallStackMenu")
- Ou, desmarque **habilitar apenas meu código** na depuração de **Opções**de **ferramentas** do Visual Studio (ou **depurar**) >  >  **Debugging**:

  ![Mostrar código externo usando a caixa de diálogo opções](../debugger/media/debuggermap_debugoptions.png "DebuggerMap_DebugOptions")

## <a name="control-the-maps-layout"></a>Controlar o layout do mapa

A alteração do layout do mapa não afeta o código de forma alguma.

Para controlar o layout do mapa, selecione o menu **layout** na barra de ferramentas do mapa.

No menu **layout** , você pode:

- Altere o layout padrão.
- Parar de reorganizar o mapa automaticamente, desmarcando o **layout automaticamente durante a depuração**.
- Reorganize o mapa o mínimo possível ao adicionar itens, desmarcando **layout incremental**.

## <a name="make-notes-about-the-code"></a><a name="MakeNotes"></a> Fazer anotações sobre o código

Você pode adicionar comentários para controlar o que está acontecendo no código.

Para adicionar um comentário, clique com o botão direito do mouse no mapa do código e selecione **Editar**  >  **novo comentário**e digite o comentário.

Para adicionar uma nova linha em um comentário, pressione **Shift** + **Enter**.

 ![Adicionar comentário à pilha de chamadas no mapa de códigos](../debugger/media/debuggermap_addcomment.png "DebuggerMap_AddComment")

## <a name="update-the-map-with-the-next-call-stack"></a><a name="UpdateMap"></a> Atualizar o mapa com a próxima pilha de chamadas

À medida que você executa o aplicativo no próximo ponto de interrupção ou entrar em uma função, o mapa adiciona novas pilhas de chamadas automaticamente.

![Atualizar mapa de códigos com a próxima pilha de chamadas](../debugger/media/debuggermap_addclearcallstack.png "DebuggerMap_AddClearCallStack")

Para impedir que o mapa adicione novas pilhas de chamadas automaticamente, selecione ![Mostrar pilha de chamadas no mapa de códigos automaticamente](../debugger/media/debuggermap_automaticupdateicon.gif "Mostrar pilha de chamadas no mapa de códigos automaticamente") na barra de ferramentas do mapa de códigos. O mapa continua realçando as pilhas de chamadas existentes. Para adicionar manualmente a pilha de chamadas atual ao mapa, pressione **Ctrl** + **Shift** + **`** .

## <a name="add-related-code-to-the-map"></a><a name="AddRelatedCode"></a> Adicionar código relacionado ao mapa

Agora que você tem um mapa, em C# ou Visual Basic, pode adicionar itens como campos, propriedades e outros métodos para controlar o que está acontecendo no código.

Para ir para a definição de um método no código, clique duas vezes no método no mapa ou selecione-o e pressione **F12**, ou clique com o botão direito do mouse e selecione **ir para definição**.

![Ir para a definição de código de um método no mapa de códigos](../debugger/media/debuggermap_gotocodedefinition.png "DebuggerMap_GoToCodeDefinition")

Para adicionar itens que você deseja controlar ao mapa, clique com o botão direito do mouse em um método e selecione os itens que deseja rastrear. Os itens adicionados mais recentemente aparecem em verde.

![Campos relacionados a um método no mapa de códigos de pilha de chamadas](../debugger/media/debuggermap_showedfields.png "DebuggerMap_ShowedFields")

>[!NOTE]
>Por padrão, a adição de itens ao mapa também adiciona os nós do grupo pai, como a classe, o namespace e o assembly. Você pode desativar e desativar esse recurso selecionando o botão **incluir pais** na barra de ferramentas do mapa de códigos ou pressionando **Ctrl** enquanto adiciona itens.

![Mostrar campos em um método no mapa de códigos de pilha de chamadas](../debugger/media/debuggermap_showfields.png "DebuggerMap_ShowFields")

Continue criando o mapa para ver mais código.

 ![Consulte métodos que usam um campo: mapa de códigos de pilha de chamadas](../debugger/media/debuggermap_findallreferences.png "DebuggerMap_FindAllReferences")

 ![Métodos que usam um campo no mapa de códigos de pilha de chamadas](../debugger/media/debuggermap_foundallreferences.png "DebuggerMap_FoundAllReferences")

## <a name="find-bugs-using-the-map"></a><a name="FindBugs"></a> Localizar bugs usando o mapa
 Visualizar seu código pode ajudar a localizar bugs com mais rapidez. Por exemplo, suponha que você esteja investigando um bug em um aplicativo de desenho. Quando você desenha uma linha e tenta desfazê-la, nada acontece até que você desenhe outra linha.

 Portanto, você define pontos de interrupção `clear` nos `undo` métodos, e `Repaint` , inicia a depuração e cria um mapa como este:

 ![Adicionar outra pilha de chamadas ao mapa de códigos](../debugger/media/debuggermap_addpaintobjectcallstack.png "DebuggerMap_AddPaintObjectCallStack")

 Você observará que todos os gestos do usuário no mapa chamam `Repaint`, exceto para `undo`. Isso pode explicar o motivo de `undo` não funcionar imediatamente.

 Depois de corrigir o bug e continuar executando o aplicativo, o mapa adiciona a nova chamada de `undo` para `Repaint` :

 ![Adicionar nova chamada de método para pilha de chamadas no mapa de códigos](../debugger/media/debuggermap_addnewcallforrepaint.png "DebuggerMap_AddNewCallForRepaint")

## <a name="share-the-map-with-others"></a>Compartilhar o mapa com outras pessoas

Você pode exportar um mapa, enviá-lo para outras pessoas com o Microsoft Outlook, salvá-lo em sua solução e verificá-lo no controle de versão.

Para compartilhar ou salvar o mapa, use **compartilhar** na barra de ferramentas do mapa de código.

![Compartilhar mapa de código de pilha de chamadas com outras pessoas](../debugger/media/debuggermap_sharewithothers.png "Compartilhar mapa de código de pilha de chamadas com outras pessoas")

## <a name="see-also"></a>Veja também
[Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)

[Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)

[Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)

[Procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md)
