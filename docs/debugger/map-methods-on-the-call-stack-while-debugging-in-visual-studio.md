---
title: Criar um mapa visual da pilha de chamadas | Microsoft Docs
ms.custom: ''
ms.date: 11/26/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ede973d96ffe21fb9406bb471400ffa8e2b69251
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389572"
---
# <a name="create-a-visual-map-of-the-call-stack-while-debugging"></a>Criar um mapa visual da pilha de chamadas durante a depuração 

Crie um mapa de códigos para rastrear visualmente a pilha de chamadas durante a depuração. Você pode fazer anotações no mapa para acompanhar o que o código está fazendo, de modo a se concentrar na localização de bugs.

Para obter instruções, assista a este vídeo: [vídeo: depurar visualmente com a integração do depurador mapa de códigos (Channel 9)](http://go.microsoft.com/fwlink/?LinkId=293418)

Para obter detalhes de comandos e ações que você pode usar com mapas de código, consulte [procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md).

>[!IMPORTANT]
>Você pode criar mapas de código somente no [Visual Studio Enterprise edition](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).

Aqui está uma rápida olhada um mapa de código:

 ![Depuração com pilhas de chamadas em mapas de códigos](../debugger/media/debuggermap_overview.png "DebuggerMap_Overview")

##  <a name="MapStack"></a> Mapear a pilha de chamadas

1. Em um Visual Studio Enterprise C#, Visual Basic, C++, JavaScript ou X + exe + de projeto, iniciar a depuração, selecionando **depurar** > **iniciar depuração** ou pressionando **F5**.
   
1. Depois que seu aplicativo entra em modo de interrupção ou entrar em uma função, selecione **Debug** > **mapa de códigos**, ou pressione **Ctrl**+**Shift** +**`**.

   A pilha de chamadas atual aparece em laranja em um novo mapeamento de código:

   ![Ver a pilha de chamadas no mapa de códigos](../debugger/media/debuggermap_seeundocallstack.png "DebuggerMap_SeeUndoCallStack")

O código mapeado atualizações automaticamente conforme você continua a depuração. Alteração de itens de mapa ou layout não afeta o código de forma alguma. Sinta-se à vontade para renomear, mover ou remover qualquer item no mapa.

Para obter mais informações sobre um item, passe o mouse sobre ele e examine a dica de ferramenta do item. Você também pode selecionar **legenda** na barra de ferramentas para saber o que significa cada ícone.

![Legenda do mapa de código](../debugger/media/debuggermap_showlegend.png "legenda do mapa de código")

>[!NOTE]
>A mensagem **o diagrama pode ser baseado em uma versão mais antiga do código** na parte superior do código de mapa significa que o código pode ter alterado depois que você atualizou pela última vez o mapa. Por exemplo, uma chamada no mapa pode não existir mais no código. Feche a mensagem e tente recriar a solução antes de atualizar o mapa outra vez.

## <a name="map-external-code"></a>Mapa de código externo

Por padrão, somente seu próprio código aparece no mapa. Para ver o código externo no mapa:
  
- Clique com botão direito no **pilha de chamadas** janela e selecione **Mostrar código externo**:
  
  ![Exibir código externo usando a janela pilha de chamadas](../debugger/media/debuggermap_callstackmenu.png "DebuggerMap_CallStackMenu")
- Ou, desmarque **habilitar apenas meu código** no Visual Studio **ferramentas** (ou **depurar**) > **opções**  >   **Depuração**:
  
  ![Mostrar código externo usando a caixa de diálogo Opções](../debugger/media/debuggermap_debugoptions.png "DebuggerMap_DebugOptions")

## <a name="control-the-maps-layout"></a>Controlar o layout do mapa

Alterar o layout do mapa não afeta o código de alguma forma. 

Para controlar o layout do mapa, selecione o **Layout** menu na barra de ferramentas do mapa. 

No **Layout** menu, você pode:

-   Altere o layout padrão.
-   Parar de reorganizar o mapa automaticamente, desmarcando **Layout automaticamente ao depurar**.
-   Reorganizar o mapa o mínimo possível quando você adicionar itens, desmarcando **Layout Incremental**.

##  <a name="MakeNotes"></a> Fazer anotações sobre o código

Você pode adicionar comentários para acompanhar o que está acontecendo no código. 

Para adicionar um comentário, clique com botão direito no mapa de código e selecione **edite** > **novo comentário**, em seguida, digite o comentário. 

Para adicionar uma nova linha em um comentário, pressione **Shift**+**Enter**.

 ![Adicionar comentário para a pilha de chamadas no mapa de códigos](../debugger/media/debuggermap_addcomment.png "DebuggerMap_AddComment")

##  <a name="UpdateMap"></a> Atualizar o mapa com a próxima pilha de chamadas

À medida que você executa seu aplicativo para o próximo ponto de interrupção ou a etapa em uma função, o mapa adiciona novas pilhas de chamadas automaticamente.

![Mapa de código de atualização com a próxima pilha de chamadas](../debugger/media/debuggermap_addclearcallstack.png "DebuggerMap_AddClearCallStack")

Para interromper o mapa de adicionar novas pilhas de chamadas automaticamente, selecione ![pilha de chamadas de mostrar no mapa de códigos automaticamente](../debugger/media/debuggermap_automaticupdateicon.gif "pilha de chamadas de mostrar no mapa de códigos automaticamente") na barra de ferramentas de mapa de código. O mapa continuará realçar as pilhas de chamadas existentes. Para adicionar manualmente a pilha de chamadas atual ao mapa, pressione **Ctrl**+**Shift**+**`**. 

##  <a name="AddRelatedCode"></a> Adicionar código relacionado ao mapa

Agora que você tem um mapa, em C# ou Visual Basic, você pode adicionar itens, como campos, propriedades e outros métodos, para acompanhar o que está acontecendo no código. 

Para ir para a definição de um método no código, clique duas vezes o método no mapa, ou selecione-o e pressione **F12**, ou clique duas vezes e selecione **ir para definição**.

![Ir para definição de código para um método no mapa de códigos](../debugger/media/debuggermap_gotocodedefinition.png "DebuggerMap_GoToCodeDefinition")

Para adicionar os itens que você deseja rastrear no mapa, um método com o botão direito e selecione os itens que você deseja rastrear. Os itens mais recentemente adicionados aparecem em verde.

![Campos relacionados a um método no mapa de códigos de pilha de chamadas](../debugger/media/debuggermap_showedfields.png "DebuggerMap_ShowedFields")

>[!NOTE]
>Por padrão, a adição de itens no mapa também adiciona os nós do grupo pai, como a classe, namespace e assembly. Você pode ativar esse recurso e desativar, selecionando o **incluem pais** botão na barra de ferramentas de mapa de código ou pressionando **Ctrl** enquanto você adicionar itens.

![Mostrar campos em um método no mapa de códigos de pilha de chamadas](../debugger/media/debuggermap_showfields.png "DebuggerMap_ShowFields")

Continue criando o mapa para ver mais código.

 ![Consulte os métodos que usam um campo: mapa de códigos de pilha de chamadas](../debugger/media/debuggermap_findallreferences.png "DebuggerMap_FindAllReferences")

 ![Métodos que usam um campo no mapa de códigos de pilha de chamadas](../debugger/media/debuggermap_foundallreferences.png "DebuggerMap_FoundAllReferences")

##  <a name="FindBugs"></a> Localizar bugs usando o mapa
 Visualizar seu código pode ajudar a localizar bugs com mais rapidez. Por exemplo, suponha que você estiver investigando um bug em um aplicativo de desenho. Quando você desenha uma linha e tenta desfazê-la, nada acontece até que você desenhe outra linha.

 Para que você define pontos de interrupção a `clear`, `undo`, e `Repaint` métodos, inicie a depuração e cria um mapa como este:

 ![Adicionar outra pilha de chamadas ao mapa de códigos](../debugger/media/debuggermap_addpaintobjectcallstack.png "DebuggerMap_AddPaintObjectCallStack")

 Você observará que todos os gestos do usuário no mapa chamam `Repaint`, exceto para `undo`. Isso pode explicar o motivo de `undo` não funcionar imediatamente.

 Depois de corrigir o bug e continuar a execução do aplicativo, o mapa adicionará a nova chamada de `undo` para `Repaint`:

 ![Adicionar nova pilha de chamada de método no mapa de códigos](../debugger/media/debuggermap_addnewcallforrepaint.png "DebuggerMap_AddNewCallForRepaint")

## <a name="share-the-map-with-others"></a>Compartilhar o mapa com outras pessoas

Exportar um mapa, enviá-lo para outras pessoas com o Microsoft Outlook, salvá-lo em sua solução e verificá-lo no controle de versão.

Para compartilhar ou salvar o mapa, use **compartilhar** na barra de ferramentas de mapa de código. 

![Mapa de códigos de pilha de chamada de compartilhamento com outras pessoas](../debugger/media/debuggermap_sharewithothers.png "mapa de códigos de pilha de chamada de compartilhamento com outras pessoas")

## <a name="see-also"></a>Consulte também
[Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)

[Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)

[Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)

[Procurar e reorganizar mapas de códigos](../modeling/browse-and-rearrange-code-maps.md)
