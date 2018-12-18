---
title: Histórico de Pixel gráfico | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.graphics.pixelhistory
ms.assetid: 0a2cbde5-1ad9-487e-857c-a3664158c268
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9e0302e4b245a4fbf94d0eb49850101c404cd8a2
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31479949"
---
# <a name="graphics-pixel-history"></a>Histórico de pixel gráfico
A janela de histórico de Pixel gráfico no analisador de gráficos do Visual Studio ajuda a entender como um pixel específico é afetado pelos eventos Direct3D que ocorrem durante um intervalo de seu aplicativo ou um jogo.  
  
 Esta é a janela Histórico de Pixel:  
  
 ![Um pixel com três eventos Direct3D no seu histórico. ](media/gfx_diag_demo_pixel_history_orientation.png "gfx_diag_demo_pixel_history_orientation")  
  
## <a name="understanding-the-pixel-history-window"></a>Noções básicas sobre a janela Histórico de Pixel  
 Usando o histórico de Pixel, você pode analisar como um pixel específico do destino de renderização é afetado pelos eventos Direct3D durante um intervalo. Você pode identificar um problema de processamento de um evento específico do Direct3D, mesmo quando eventos subsequentes — ou primitivas subsequentes no mesmo evento — continuam a alterar o valor de cor final do pixel. Por exemplo, um pixel pode ser processado incorretamente e obscurecido por outro pixel semitransparente, para que as cores sejam combinadas no framebuffer. Esse tipo de problema seria difícil de diagnosticar se você tivesse apenas o conteúdo final do destino da renderização para orientá-lo.  
  
 A janela Histórico de Pixel exibe o histórico completo de um pixel ao longo do quadro selecionado. O **Buffer de quadro Final** na parte superior da janela exibe a cor que é gravada framebuffer no final do quadro, juntamente com informações adicionais sobre o pixel como sua tela e quadro que se trata de coordenadas. Esta área contém também o **renderizar Alpha** caixa de seleção. Quando essa caixa de seleção é selecionada, o **Buffer de quadro Final** valores de cor intermediária e cor são exibidos com transparência sobre um padrão quadriculado. Se a caixa de seleção estiver desmarcada, o canal alfa dos valores de cor será ignorado.  
  
 A parte inferior da janela exibe os eventos que teve a chance de afetar a cor do pixel, junto com o **inicial** e **Final** pseudo eventos que representam os valores das cores inicial e final o framebuffer no pixel. O valor de cor inicial é determinado pelo primeiro evento que alterou a cor do pixel (geralmente um evento `Clear`). Um pixel sempre tem esses dois pseudo-eventos no seu histórico, mesmo quando outros eventos não o afetaram. Quando outros eventos tinham a oportunidade de afetar o pixel, elas são exibidas entre o **inicial** e **Final** eventos. Os eventos podem ser expandidos para mostrar seus detalhes. No caso de eventos simples, como aqueles que limpam um destino de renderização, o efeito do evento é um valor de cor. Eventos mais complexos, como chamadas de desenho geram uma ou mais primitivas que podem colaborar com a cor do pixel.  
  
 As primitivas que foram desenhadas pelo evento são identificadas por seu tipo e índice de primitiva, com a contagem total de primitiva do objeto. Por exemplo, um identificador, como **triângulo (1456) (6214)** significa que o primitivo corresponde ao triângulo 1456th em um objeto que é composto de 6214 triângulos. À esquerda de cada identificador de primitiva há um ícone que resume o efeito que a primitiva tinha sobre o pixel. As primitivas que afetam a cor do pixel são representadas por um retângulo arredondado preenchido com a cor resultante. As primitivas que são excluídas devido a algum impacto sobre a cor do pixel são representadas por ícones que indicam o motivo pelo qual o pixel foi excluído. Esses ícones são descritos na seção [exclusão primitivo](#exclusion) posteriormente neste artigo.  
  
 É possível expandir cada primitiva para examinar como a saída do sombreador do pixel foi mesclada com a cor do pixel existente para produzir a cor resultante. A partir disso você também pode examinar ou depurar o código de sombreador de pixel que está associado à primitiva e ampliar o nó do sombreador de vértice para examinar a entrada do sombreador de vértice.  
  
###  <a name="exclusion"></a> Exclusão primitivo  
 Quando uma primitiva é excluída por afetar a cor do pixel, a exclusão pode ocorrer por diversos motivos. Cada motivo é representado por um ícone que é descrito nesta tabela:  
  
|Ícone|Motivo da exclusão|  
|----------|--------------------------|  
|![Ícone de falha de teste de profundidade. ](media/vsg_hist_icon_failed_depth.png "vsg_hist_icon_failed_depth")|O pixel foi excluído porque não passou no teste de profundidade.|  
|![Ícone de falha de teste de tesoura. ](media/vsg_hist_icon_failed_scissor.png "vsg_hist_icon_failed_scissor")|O pixel foi excluído porque não passou no teste de tesoura.|  
|![Ícone de falha de teste de estêncil. ](media/vsg_hist_icon_failed_stencil.png "vsg_hist_icon_failed_stencil")|O pixel foi excluído porque não passou no teste de estêncil.|  
  
### <a name="draw-call-exclusion"></a>Exclusão de chamada de desenho  
 Se todos as primitivas em uma chamada de desenho são excluídas por afetarem o destino de renderização porque não passaram em um teste, a chamada de desenho não pode ser expandida e um ícone que corresponde ao motivo da exclusão é exibido ao lado dela. Os motivos de exclusão da chamada de desenho se assemelha aos motivos de exclusão da primitiva e os ícones são semelhantes.  
  
### <a name="viewing-and-debugging-shader-code"></a>Exibição e depuração do código do sombreador  
 Você pode examinar e depurar o código de vértice, convexa, domínio, sombreadores de pixel e geometria usando os controles abaixo o primitivo associada com o sombreador.  
  
##### <a name="to-view-a-shaders-source-code"></a>Para exibir o código-fonte do sombreador  
  
1.  No **histórico de Pixel gráfico** janela, localize a chamada de desenho correspondente para o sombreador que deseja examinar e expandi-lo.  
  
2.  Sob o desenho chamar você acabou de expandir, selecione um primitivo que demonstra o problema que você está interessado e expandi-lo.  
  
3.  Sob o primitivo que você está interessado, siga o link de título do sombreador — por exemplo, siga o link **obj:30 de sombreador de vértice** para exibir o código de origem de sombreador de vértice.  
  
    > [!TIP]
    >  O número de objeto **obj:30**, identifica este sombreador em toda a interface de analisador de gráficos como a janela de estágios de pipeline e de tabela do objeto.  
  
##### <a name="to-debug-a-shader"></a>Para depurar um sombreador  
  
1.  No **histórico de Pixel gráfico** janela, localize a chamada de desenho correspondente para o sombreador que deseja examinar e expandi-lo.  
  
2.  Em seguida, em que a chamada de desenho você acabou de expandir, selecione um primitivo que demonstra o problema que você está interessado e expandi-lo.  
  
3.  Sob o primitivo que você está interessado, escolha **iniciar depuração**. Esse ponto de entrada para os padrões de depurador HLSL para a primeira invocação do sombreador para o primitivo correspondente — ou seja, a primeira pixel ou que é processado pelo sombreador de vértice. Há apenas um pixel associado com o primitivo, mas não há mais de um invocações de sombreador de vértice para linhas e triângulos.  
  
     Para depurar a invocação do sombreador de vértice de um vértice específico, expanda o link de título VertexShader e localize o vértice que você está interessado, escolha **iniciar depuração** ao lado dele.  
  
### <a name="links-to-graphics-objects"></a>Links a objetos de gráficos  
 Para entender os eventos de gráficos no histórico de pixel, talvez você precise obter informações sobre o estado do dispositivo no momento do evento ou sobre os objetos do Direct3D referenciados pelo evento. Para cada evento no histórico de pixel, o **histórico de Pixel gráfico** fornece links para o dispositivo atual estados e relacionados a objetos.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Objetos ausentes devido ao estado do dispositivo](walkthrough-missing-objects-due-to-device-state.md)   
 [Passo a passo: depurando erros de renderização devido ao sombreamento](walkthrough-debugging-rendering-errors-due-to-shading.md)