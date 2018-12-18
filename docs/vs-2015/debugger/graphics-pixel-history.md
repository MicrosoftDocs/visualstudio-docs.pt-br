---
title: Histórico de Pixel de gráficos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.graphics.pixelhistory
ms.assetid: 0a2cbde5-1ad9-487e-857c-a3664158c268
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 20b33c987cf7e2b1ab57160b4f4917246d9030b6
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51733158"
---
# <a name="graphics-pixel-history"></a>Histórico de pixel gráfico
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A janela de histórico de Pixel de gráficos no analisador de gráficos do Visual Studio ajuda a entender como um pixel específico é afetado pelos eventos Direct3D que ocorrem durante um quadro do seu jogo ou aplicativo.  
  
 Esta é a janela de histórico de Pixel:  
  
 ![Um pixel com três eventos de Direct3D em seu histórico. ](../debugger/media/gfx-diag-demo-pixel-history-orientation.png "gfx_diag_demo_pixel_history_orientation")  
  
## <a name="understanding-the-pixel-history-window"></a>Noções básicas sobre a janela de histórico de Pixel  
 Usando o histórico de Pixel, você pode analisar como um pixel específico do destino de renderização é afetado pelos eventos do Direct3D durante um intervalo. Você pode identificar um problema de processamento de um evento específico do Direct3D, mesmo quando eventos subsequentes — ou primitivas subsequentes no mesmo evento — continuam a alterar o valor de cor final do pixel. Por exemplo, um pixel pode ser processado incorretamente e obscurecido por outro pixel semitransparente, para que as cores sejam combinadas no framebuffer. Esse tipo de problema seria difícil de diagnosticar se você tivesse apenas o conteúdo final do destino da renderização para orientá-lo.  
  
 A janela de histórico de Pixel exibe o histórico completo de um pixel ao longo do quadro selecionado. O **Buffer de quadro Final** na parte superior da janela exibe a cor que é escrita no framebuffer no final do quadro, juntamente com informações adicionais sobre o pixel, como o quadro que eles vêm e sua tela coordenadas. Essa área também contém o **processar Alpha** caixa de seleção. Quando essa caixa de seleção é selecionada, o **Buffer de quadro Final** cor e valores de cor intermediários são exibidos com transparência sobre um padrão quadriculado. Se a caixa de seleção estiver desmarcada, o canal alfa dos valores de cor será ignorado.  
  
 A parte inferior da janela exibe os eventos que possam afetar a cor do pixel, juntamente com o **inicial** e **Final** pseudo-eventos que representam os valores de cor inicial e final do o pixel no framebuffer. O valor de cor inicial é determinado pelo primeiro evento que alterou a cor do pixel (geralmente um evento `Clear`). Um pixel sempre tem esses dois pseudo-eventos no seu histórico, mesmo quando outros eventos não o afetaram. Quando outros eventos podem afetar o pixel, eles são exibidos entre o **inicial** e **Final** eventos. Os eventos podem ser expandidos para mostrar seus detalhes. No caso de eventos simples, como aqueles que limpam um destino de renderização, o efeito do evento é um valor de cor. Eventos mais complexos, como chamadas de desenho geram uma ou mais primitivas que podem colaborar com a cor do pixel.  
  
 As primitivas que foram desenhadas pelo evento são identificadas por seu tipo e índice de primitiva, com a contagem total de primitiva do objeto. Por exemplo, um identificador, como **triângulo (1456) de (6214)** significa que a primitiva corresponde ao triângulo 1456 º em um objeto que é composto de 6214 triângulos. À esquerda de cada identificador de primitiva há um ícone que resume o efeito que a primitiva tinha sobre o pixel. As primitivas que afetam a cor do pixel são representadas por um retângulo arredondado preenchido com a cor resultante. As primitivas que são excluídas devido a algum impacto sobre a cor do pixel são representadas por ícones que indicam o motivo pelo qual o pixel foi excluído. Esses ícones são descritos na seção [exclusão da primitiva](../debugger/graphics-pixel-history.md#exclusion) mais adiante neste artigo.  
  
 É possível expandir cada primitiva para examinar como a saída do sombreador do pixel foi mesclada com a cor do pixel existente para produzir a cor resultante. A partir disso você também pode examinar ou depurar o código de sombreador de pixel que está associado à primitiva e ampliar o nó do sombreador de vértice para examinar a entrada do sombreador de vértice.  
  
###  <a name="exclusion"></a> Exclusão de primitiva  
 Quando uma primitiva é excluída por afetar a cor do pixel, a exclusão pode ocorrer por diversos motivos. Cada motivo é representado por um ícone que é descrito nesta tabela:  
  
|Ícone|Motivo da exclusão|  
|----------|--------------------------|  
|![Ícone de falha de teste de profundidade. ](../debugger/media/vsg-hist-icon-failed-depth.png "vsg_hist_icon_failed_depth")|O pixel foi excluído porque não passou no teste de profundidade.|  
|![Ícone de falha de teste de tesoura. ](../debugger/media/vsg-hist-icon-failed-scissor.png "vsg_hist_icon_failed_scissor")|O pixel foi excluído porque não passou no teste de tesoura.|  
|![Ícone de falha de teste de estêncil. ](../debugger/media/vsg-hist-icon-failed-stencil.png "vsg_hist_icon_failed_stencil")|O pixel foi excluído porque não passou no teste de estêncil.|  
  
### <a name="draw-call-exclusion"></a>Exclusão de chamada de desenho  
 Se todos as primitivas em uma chamada de desenho são excluídas por afetarem o destino de renderização porque não passaram em um teste, a chamada de desenho não pode ser expandida e um ícone que corresponde ao motivo da exclusão é exibido ao lado dela. Os motivos de exclusão da chamada de desenho se assemelha aos motivos de exclusão da primitiva e os ícones são semelhantes.  
  
### <a name="viewing-and-debugging-shader-code"></a>Exibição e depuração do código do sombreador  
 Você pode examinar e depurar o código para o vértice, hull, domínio, geometria e pixel shaders usando os controles abaixo da primitiva associada ao sombreador.  
  
##### <a name="to-view-a-shaders-source-code"></a>Para exibir o código-fonte do sombreador  
  
1.  No **histórico de Pixel de gráficos** janela, localize a chamada de desenho que corresponde ao sombreador que deseja examinar e expandi-lo.  
  
2.  Sob a desenhar ligar para você acabou de expandir, selecione um primitivo que demonstra o problema que você está interessado e expandi-lo.  
  
3.  Sob o primitivo que você está interessado, siga o link de título do sombreador — por exemplo, siga o link **obj:30 do sombreador de vértices** para exibir o código de origem do sombreador de vértice.  
  
    > [!TIP]
    >  O número de objeto **obj:30**, identifica esse sombreador em toda a interface de analisador de gráficos como a janela de estágios de pipeline e a tabela de objeto.  
  
##### <a name="to-debug-a-shader"></a>Para depurar um sombreador  
  
1.  No **histórico de Pixel de gráficos** janela, localize a chamada de desenho que corresponde ao sombreador que deseja examinar e expandi-lo.  
  
2.  Em seguida, sob a chamada de desenho você acabou de expandir, selecione um primitivo que demonstra o problema que você está interessado e expandi-lo.  
  
3.  Sob o primitivo que você está interessado, escolha **iniciar depuração**. Esse ponto de entrada para os padrões de depurador HLSL para a primeira invocação do sombreador para o primitivo correspondente — ou seja, o primeiro pixel ou que é processado pelo sombreador de vértice. Há apenas um pixel associado à primitiva, mas não há mais de um invocações de sombreador de vértice para linhas e triângulos.  
  
     Para depurar a invocação do sombreador de vértice de um vértice específico, expanda o link de título VertexShader e localize o vértice que você está interessado, escolha **iniciar depuração** ao lado dele.  
  
### <a name="links-to-graphics-objects"></a>Links a objetos de gráficos  
 Para entender os eventos de gráficos no histórico de pixel, talvez você precise obter informações sobre o estado do dispositivo no momento do evento ou sobre os objetos do Direct3D referenciados pelo evento. Para cada evento no histórico de pixel, o **histórico de Pixel de gráficos** fornece links para o dispositivo atual estados e para objetos relacionados.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Objetos ausentes devido ao estado do dispositivo](../debugger/walkthrough-missing-objects-due-to-device-state.md)   
 [Passo a passo: depurando erros de renderização devido ao sombreamento](../debugger/walkthrough-debugging-rendering-errors-due-to-shading.md)



