---
title: Mapear métodos na pilha de chamadas durante a depuração no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
ms.assetid: d6a72e5e-f88d-46fc-94a3-1789d34805ef
caps.latest.revision: 43
author: MikeJo5000
ms.author: gewarren
manager: douge
ms.openlocfilehash: f67a891327d179ffd23b56eb5bae951309bab8da
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51725609"
---
# <a name="map-methods-on-the-call-stack-while-debugging-in-visual-studio"></a>Mapear métodos na pilha de chamadas ao depurar no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Crie um mapa de códigos para acompanhar visualmente a pilha de chamadas durante a depuração. Você pode fazer anotações no mapa para acompanhar o que o código está fazendo, de modo a se concentrar na localização de bugs.  
  
 ![Depuração com pilhas de chamadas em mapas de códigos](../debugger/media/debuggermap-overview.png "DebuggerMap_Overview")  
  
 Itens necessários:  
  
- [Visual Studio Enterprise](https://www.visualstudio.com/downloads/download-visual-studio-vs)  
  
- Código que você pode depurar, como Visual c# .NET, Visual Basic .NET, C++, JavaScript ou X + +  
  
  Consulte: [vídeo: depurar visualmente com a integração do depurador mapa de códigos (Channel 9)](http://go.microsoft.com/fwlink/?LinkId=293418) • [mapear a pilha de chamadas](#MapStack) • [fazer anotações sobre o código](#MakeNotes) • [atualizar o mapa com o próxima pilha de chamadas](#UpdateMap) • [adicionar código relacionado ao mapa](#AddRelatedCode) • [localizar bugs usando o mapa](#FindBugs) • [p e r](#QA)  
  
  Para obter detalhes sobre os comandos e ações que você pode usar ao trabalhar com mapas de código, consulte [procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md).  
  
##  <a name="MapStack"></a> Mapear a pilha de chamadas  
  
1.  Inicie a depuração. (Teclado: **F5**)  
  
2.  Depois que seu aplicativo entra em modo de interrupção ou entrar em uma função, escolha **mapa de código**. (Teclado: **Ctrl** + **Shift** + **`**)  
  
     ![Escolha o mapa de código para iniciar a pilha de chamadas de mapeamento](../debugger/media/debuggermap-choosecodemap.png "DebuggerMap_ChooseCodeMap")  
  
     A pilha de chamadas atual aparece em laranja em um novo mapeamento de código:  
  
     ![Ver a pilha de chamadas no mapa de códigos](../debugger/media/debuggermap-seeundocallstack.png "DebuggerMap_SeeUndoCallStack")  
  
     O mapa será atualizado automaticamente enquanto você continua a depuração. Ver [atualizar o mapa com a próxima pilha de chamadas](#UpdateMap).  
  
##  <a name="MakeNotes"></a> Fazer anotações sobre o código  
 Adicione comentários para acompanhar o que está acontecendo no código. Para adicionar uma nova linha em um comentário, pressione **Shift + Return**.  
  
 ![Adicionar comentário para a pilha de chamadas no mapa de códigos](../debugger/media/debuggermap-addcomment.png "DebuggerMap_AddComment")  
  
##  <a name="UpdateMap"></a> Atualizar o mapa com a próxima pilha de chamadas  
 Execute o aplicativo até o próximo ponto de interrupção ou siga uma função. O mapa adiciona uma nova pilha de chamadas.  
  
 ![Mapa de código de atualização com a próxima pilha de chamadas](../debugger/media/debuggermap-addclearcallstack.png "DebuggerMap_AddClearCallStack")  
  
##  <a name="AddRelatedCode"></a> Adicionar código relacionado ao mapa  
 Agora você tem um mapa. Qual é a próxima etapa? Se você estiver trabalhando com o Visual C# .NET ou com o Visual Basic .NET, adicione itens, como campos, propriedades e outros métodos, para acompanhar o que está acontecendo no código.  
  
 Clique duas vezes em um método para ver sua definição de código ou use o menu de atalho para o método. (Teclado: selecione o método no mapa e pressione **F12**)  
  
 ![Ir para definição de código para um método no mapa de códigos](../debugger/media/debuggermap-gotocodedefinition.png "DebuggerMap_GoToCodeDefinition")  
  
 Adicione os itens que você deseja rastrear no mapa.  
  
 ![Mostrar campos em um método no mapa de códigos de pilha de chamadas](../debugger/media/debuggermap-showfields.png "DebuggerMap_ShowFields")  
  
> [!NOTE]
>  Por padrão, a adição de itens no mapa também adiciona os nós do grupo pai, como a classe, namespace e assembly. Embora isso seja útil, você pode manter o mapa simples desativando esse recurso usando o **incluem pais** botão na barra de ferramentas do mapa ou pressionando **CTRL** quando você adiciona itens.  
  
 ![Campos relacionados a um método no mapa de códigos de pilha de chamadas](../debugger/media/debuggermap-showedfields.png "DebuggerMap_ShowedFields")  
  
 Aqui, você pode visualizar facilmente quais métodos usam os mesmos campos. Os itens mais recentemente adicionados aparecem em verde.  
  
 Continue criando o mapa para ver mais código.  
  
 ![Consulte os métodos que usam um campo: mapa de códigos de pilha de chamadas](../debugger/media/debuggermap-findallreferences.png "DebuggerMap_FindAllReferences")  
  
 ![Métodos que usam um campo no mapa de códigos de pilha de chamadas](../debugger/media/debuggermap-foundallreferences.png "DebuggerMap_FoundAllReferences")  
  
##  <a name="FindBugs"></a> Localizar bugs usando o mapa  
 Visualizar seu código pode ajudar a localizar bugs com mais rapidez. Por exemplo, suponha que você esteja investigando um bug em um programa de desenho. Quando você desenha uma linha e tenta desfazê-la, nada acontece até que você desenhe outra linha.  
  
 Para que você define pontos de interrupção a `clear`, `undo`, e `Repaint` métodos, inicie a depuração e cria um mapa como este:  
  
 ![Adicionar outra pilha de chamadas ao mapa de códigos](../debugger/media/debuggermap-addpaintobjectcallstack.png "DebuggerMap_AddPaintObjectCallStack")  
  
 Você observará que todos os gestos do usuário no mapa chamam `Repaint`, exceto para `undo`. Isso pode explicar o motivo de `undo` não funcionar imediatamente.  
  
 Após corrigir o bug e continuar executando o programa, o mapa adicionará a nova chamada de `undo` para `Repaint`:  
  
 ![Adicionar nova pilha de chamada de método no mapa de códigos](../debugger/media/debuggermap-addnewcallforrepaint.png "DebuggerMap_AddNewCallForRepaint")  
  
##  <a name="QA"></a> Perguntas e respostas  
  
- **Nem todas as chamadas aparecem no mapa. Por quê?**  
  
   Por padrão, somente seu próprio código aparece no mapa. Para ver o código externo, ativá-lo na **pilha de chamadas** janela:  
  
   ![Exibir código externo usando a janela pilha de chamadas](../debugger/media/debuggermap-callstackmenu.png "DebuggerMap_CallStackMenu")  
  
   ou desative **habilitar apenas meu código** em Opções de depuração do Visual Studio:  
  
   ![Mostrar código externo usando a caixa de diálogo Opções](../debugger/media/debuggermap-debugoptions.png "DebuggerMap_DebugOptions")  
  
- **Alterar o mapa afeta o código?**  
  
   Alterar o mapeamento não afeta o código de maneira alguma. Sinta-se à vontade para renomear, mover ou remover qualquer item no mapa.  
  
- **O que significa esta mensagem: "o diagrama pode ser baseado em uma versão mais antiga do código"?**  
  
   O código pode ter sido alterado depois que você alterou o mapa pela última vez. Por exemplo, uma chamada no mapa pode não existir mais no código. Feche a mensagem e tente recriar a solução antes de atualizar o mapa outra vez.  
  
- **Como controlar o layout do mapa?**  
  
   Abra o **Layout** menu na barra de ferramentas do mapa:  
  
  -   Altere o layout padrão.  
  
  -   Para parar de reorganizar o mapa automaticamente, desative **Layout automaticamente ao depurar**.  
  
  -   Para reorganizar o mapa o mínimo possível quando você adicionar itens, desative **Layout Incremental**.  
  
- **Pode compartilhar o mapa com outras pessoas?**  
  
   É possível exportar o mapa, enviá-lo a outras pessoas se tiver o Microsoft Outlook ou salvá-lo em sua solução para que você possa verificá-lo no Controle de versão do Team Foundation.  
  
   ![Mapa de códigos de pilha de chamada de compartilhamento com outras pessoas](../debugger/media/debuggermap-sharewithothers.png "DebuggerMap_ShareWithOthers")  
  
- **Como posso impedir que o mapa de adicionar novas pilhas de chamadas automaticamente?**  
  
   Escolher ![botão &#45; pilha de chamadas de mostrar no mapa de códigos automaticamente](../debugger/media/debuggermap-automaticupdateicon.gif "DebuggerMap_AutomaticUpdateIcon") na barra de ferramentas do mapa. Para adicionar manualmente a pilha de chamadas atual ao mapa, pressione **Ctrl** + **Shift** + **`**.  
  
   O mapa continuará realçando as pilhas de chamadas existentes no mapa enquanto você estiver depurando.  
  
- **O que os ícones de item e setas significam?**  
  
   Para obter mais informações sobre um item, move o ponteiro do mouse sobre ele e examine a dica de ferramenta do item. Você também pode examinar a **legenda** para saber o que significa cada ícone.  
  
   ![O que significam os ícones no mapa de código da pilha de chamada? ](../debugger/media/debuggermap-showlegend.png "DebuggerMap_ShowLegend")  
  
  Consulte: [mapear a pilha de chamadas](#MapStack) • [fazer anotações sobre o código](#MakeNotes) • [atualizar o mapa com a próxima pilha de chamadas](#UpdateMap) • [adicionar código relacionado ao mapa](#AddRelatedCode) • [ Localizar bugs usando o mapa](#FindBugs)  
  
## <a name="see-also"></a>Consulte também  
 [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)   
 [Usar mapas de códigos para depurar seus aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)   
 [Localizar possíveis problemas usando analisadores de mapa de código](../modeling/find-potential-problems-using-code-map-analyzers.md)   
 [Procurar e reorganizar mapas de códigos](../modeling/browse-and-rearrange-code-maps.md)





