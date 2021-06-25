---
title: Animações para Visual Studio | Microsoft Docs
description: Saiba mais sobre as regras que ajudam a garantir estilos de animação consistentes e amigáveis no Visual Studio IDE.
ms.custom: SEO-VS-2020
ms.date: 04/26/2017
ms.topic: reference
ms.assetid: 446773a9-e6f7-4c0c-8dbc-9e303bf32eb1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f1e8e61e5decea326fcb7f670ed2ab58f0137530
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902781"
---
# <a name="animations-for-visual-studio"></a>Animações para Visual Studio
## <a name="animation-fundamentals"></a>Conceitos básicos de animação

### <a name="animation-best-practices-in-visual-studio"></a>Práticas recomendadas de animação Visual Studio
Siga estas regras para garantir estilos de animação consistentes e amigáveis em todo o Visual Studio IDE.

- **Seja seletivo.** Limite animações às que atendem a finalidades específicas.

- **O tempo e a velocidade são importantes** para garantir que as transições se sintam rápidas e naturais:

  - Transições animadas completas em um segundo (500 milissegundos).

  - Animações que ocorrem com frequência precisam ser rápidas o suficiente para não interromperem o fluxo de trabalho do usuário. Observe a animação em um loop e ajuste o tempo até que ele se sinta correto.

  - As animações não devem ser tão rápidas nem jargões que seja difícil de entender, mas não tão lentas que faça com que seja difícil concluir a transição.

  - Use o tempo variável para enfatizar a importância. Por exemplo, ao navegar por uma sequência de itens em um diagrama de classe, acelere as transições entre itens e reduza a velocidade para se concentrar em itens importantes.

- **Use a easing gradual não linear** de um estado para outro, dando uma noção de movimento natural e normal.

- Quando possível, **use uma animação sutil ao passar o mouse** para indicar elementos interativos sob o mouse.

- Se você depender muito de animações em seus recursos, forneça um meio de autá-las **localmente** (para todos os seus recursos) como uma opção na caixa de diálogo Ferramentas **> Opções.**

- **Apenas uma animação deve ocorrer por vez e** transmitir apenas uma informação. Mais de um objeto se movendo ou tentando transmitir várias coisas pode ser confuso.

- **A sutileza é importante.** Na maioria dos casos, a animação não precisa exigir atenção do usuário para atender à sua finalidade. Alterações sutis no tempo, sequenciamento e comportamento podem afetar significativamente a percepção e podem fazer a diferença entre uma animação eficaz e ineficaz.

- Ao usar a animação para chamar a atenção para **algo,** certifique-se de que vale a pena interromper o treinamento de pensamento do usuário.

- **Ao mostrar o progresso ou o status por** meio da animação:

  - Pare de mostrar a movimentação de progresso quando o processo subjacente não estiver avançando.

  - Distinguir processos indeterminados de processos determinados.

  - Verifique se uma animação tem estados de conclusão e falha identificáveis.

  - Minimize o uso de animações de efeito que mostram o status e certifique-se de que elas tenham valor real fornecendo informações adicionais de uso real. Exemplos incluem alterações de status transitório e emergências

#### <a name="animation-donts"></a>A animação não é:

- Não use movimentos pequenos (movimento em um espaço pequeno). Prefira esmaecer e mudar em vez de mover objetos.

- Não use animações que ocorrem em uma grande área de imóveis de tela. Independentemente do tamanho, esse estilo de animação é uma distração para o usuário.

- Não use animações não relacionadas ao objeto em que o usuário está focado ou interagindo no momento.

- Não use animações que exigem interação do usuário para redefinir o estado, como forçar o usuário a responder a uma notificação intermitente para que ele pare de piscar. Interagir com eles de qualquer forma deve ser suficiente para descartá-los.

Para obter mais informações sobre aplicativos para essas práticas recomendadas, consulte [Padrões de animação](../../extensibility/ux-guidelines/animations-for-visual-studio.md#BKMK_AnimationPatterns).

### <a name="animation-metrics"></a>Métricas de animação

- O sistema deve reagir visivelmente aos gestos do usuário em menos de 10 milissegundos.

- Transições animadas não devem levar mais de 500 milissegundos para ser concluídas.

- Uma maneira de compensar as transições que exigem tempos mais longos é separá-la em duas partes. Por exemplo, a primeira parte de uma animação pode ser o contêiner de conteúdo vazio (até 500 milissegundos), seguido pelo desbotamento do conteúdo no contêiner (até 500 milissegundos).

- Para tempos de carregamento que podem ser calculados, é preferível um indicador de progresso determinante (indicador de progresso de porcentagem feita).

- Para tempos de carregamento que não podem ser calculados, um indicador ocupado como um cursor ou animação de rotação inserida (indicador de carregamento ou trabalho) é apropriado.

### <a name="animation-as-communicator"></a>Animação como comunicador
Na Visual Studio interface do usuário, a animação funciona apenas como uma ferramenta de comunicação.  Ele é usado para comunicar uma variedade de informações, como alterações estruturais na interface do usuário (por exemplo, quando um menu é aberto ou fechado). A animação pode ajudar a visualizar o comportamento dependente de tempo de sistemas complexos, como a visualização do progresso da instalação. Animações também podem ser usadas para chamar a atenção com alertas e notificações.

 As animações da interface do usuário normalmente funcionam de quatro maneiras: visualizar, chamar atenção, simular e indicadores de tempos de resposta/progresso.

#### <a name="visualize"></a>Visualizar
A animação pode enfatizar a natureza tridimensional dos objetos e facilitar a visualização da estrutura espacial pelos usuários. Para fazer isso, a animação pode precisar girar o objeto em um círculo completo, auxirá-lo lentamente e voltar ou aproximar o objeto e aumentar ligeiramente seu tamanho para enfatizar a sobrepor ou o foco.

Embora objetos tridimensionais possam ser movidos com o controle de usuário, o designer deve determinar com antecedência (programaticamente ou manualmente) como animar melhor um movimento que fornece uma compreensão ideal do objeto. Essa animação programada pode ser ativada pelo usuário colocando o cursor sobre o objeto, enquanto os movimentos controlados pelo usuário exigem que o usuário entenda como manipular o objeto. Limitar o movimento a um único eixo ou orientação por vez; dimensione, gire ou traduza, mas não faça mais de um simultaneamente.

A categoria Visualizar inclui os aspectos de dados, relações, estado, estrutura, sequência e tempo.

##### <a name="data"></a>Dados
Ilustrar informações complexas e variáveis:

- Movendo visualizações de informações como gráficos e grafos

- Percorrendo uma sequência, um tour guiado e paging

- Chamando detalhes, apontando e realçando informações específicas

- Sobreposição de detalhes e informações adicionais sobre um elemento focalizado

- Transformação de uma representação estrutural ou organizacional para outra

- Representando alterações ao longo do tempo usando controles deslizantes de tempo, rodinhas e botões de corrida e controles de transporte (reproduzir, parar e pausar)

##### <a name="relationships"></a>Relações

- Ilustrar como os itens se relacionam entre si ou quais itens estão relacionados a um determinado item

- Mostrar hierarquias e relações pai-filho ou irmão

- Um elemento gera outro

- Um elemento minimiza para outro elemento

- Um elemento entre si

##### <a name="state"></a>Estado

- Atualizações de conteúdo

- Seleção e foco do usuário

- Progresso

- Errors

##### <a name="structure"></a>Estrutura

- Pivoting da estrutura em um nó

- Reorientando

- Minimizar e maximizar ou expandir e ressuir

##### <a name="sequence"></a>Sequência

- Sequência de apresentação de slides

- Invertendo imagens

##### <a name="time"></a>Hora

- Mostrar alteração ao longo do tempo, tempo de tempo e screencast

- Mover para lixeira, desfazer e refazer

- Restaurar o estado histórico

#### <a name="attract-attention"></a>Chamar a atenção
Se o objetivo for chamar a atenção do usuário para um único elemento de vários ou para alertar o usuário sobre as informações atualizadas, uma animação poderá ser apropriada. Por exemplo, a página inicial do aplicativo pode empregar um Ponto de Partida que desliza para o local após o carregamento da página.

Como regra, o último elemento móvel na tela chama a atenção do usuário.  Em uma série de elementos animados, a atenção do usuário seguirá o último objeto móvel.

##### <a name="alert"></a>Alerta

- Alertar o usuário, obter atenção, mostrar o progresso

- Mostrar que algo está sendo feito corretamente ou incorretamente ou mostrar alterações de progresso ou progresso

- Solicitar usuários durante uma tarefa, como localizar mais informações online ou aprender sobre a tarefa atual

##### <a name="notifications"></a>Notificações

- Alertar o usuário sobre uma condição de erro

- Interromper o usuário para ver se ele gostaria de participar de outra coisa

- Os princípios informam ao usuário que um processo foi concluído ou alterado, como quando um download é concluído.

#### <a name="simulate"></a>Simular
Essa categoria aborda a física e a dimensionalidade.

- Ilustrar de onde os objetos vêm ou para onde eles vão

- Expandir e fechar ou abrir e fechar

- Panorâmico, rolagem e turnos de página

- Empilhamento e ordenação z

- Carrossel e sanfona

- Invertendo e girando a interface do usuário

#### <a name="response-and-progress-indicators"></a>Indicadores de resposta e progresso
Os indicadores de progresso têm algumas vantagens importantes:

- Os indicadores de progresso determinados e indeterminados garantem ao usuário que o sistema não teve uma queda e está trabalhando no problema.

- Indicadores determinados dão ao usuário uma noção de até que ponto a ação está progredindo, bem como uma sensação de se aproximar do final.

## <a name="animation-patterns"></a><a name="BKMK_AnimationPatterns"></a> Padrões de animação

### <a name="overview"></a>Visão geral
Animações no Visual Studio devem servir a uma função específica sem prejudicar a produtividade do usuário. Em geral, as animações Visual Studio devem ser:

- Pequeno e não discreto

- Natural e realista

- Sutil e desleixado

- Rápido e eficiente

- Descontraído, não ressuída

Esta ilustração mostra os estilos de animação que recomendamos para Visual Studio. Nenhuma animação ou animações sutis, como esmaecer/esmaecer, são usadas com mais frequência. Há uma aplicação limitada de animações de movimento, como expansão e contrato, alteração de posição X e Y e rotação.

![Estilos de animação recomendados para Visual Studio](../../extensibility/ux-guidelines/media/1202-a_vsanimstyles.png "1202-a_VSAnimStyles")<br />Estilos de animação recomendados para Visual Studio

#### <a name="appear-and-disappear"></a>Aparecer e desaparecer
Com esse padrão, um elemento muda de visível para fora de exibição e de volta sem uma animação de transição.

![Animação de aparecer e desaparecer](../../extensibility/ux-guidelines/media/1202-b_appearanddisappear.png "1202-b_AppearAndDisappear")<br />Animação de aparecer e desaparecer

##### <a name="correct-usage"></a>Uso correto
Novos elementos de interface do usuário que precisam aparecer ou desaparecer instantaneamente para que o usuário não seja desamarmado nem desalocarado. Além disso, animações lentas podem ser percebidas como um arrastar de desempenho, o que não ocorrerá com o estilo de aparecer e desaparecer.

##### <a name="incorrect-usage"></a>Uso incorreto
Casos em que a interface do usuário aparece tão de forma tão repentina que o usuário não tem ideia do que aconteceu e adicionar uma animação ajudaria com a compreensão contextual.

##### <a name="animation-properties"></a>Propriedades de animação
O atraso de tempo geralmente é zero segundos.

##### <a name="examples"></a>Exemplos
- Ocultar janelas de ferramentas automaticamente

- Interface do usuário do editor ativado por teclado, como IntelliSense e Ajuda de parâmetro

- Expandir e regiões de código

#### <a name="fade-in-and-fade-out"></a>Esmaecer e esmaecer
Com esse padrão, um elemento de interface do usuário faz a transição de não visível (0% de opacidade) para visível (100% de opacidade) ou vice-versa.

![Animação de esmaeçando e esmaeçando](../../extensibility/ux-guidelines/media/1202-c_fadeinfadeout.png "1202-c_FadeInFadeOut")<br />Animação de esmaeçando e esmaeçando

##### <a name="correct-usage"></a>Uso correto
Essa é a animação de interface do usuário mais comumente recomendada. É um efeito sutil que adiciona interesse sem interromper o fluxo. Em alguns casos, o usuário pode nem perceber que há uma animação, envolvendo um sistema de interface do usuário suave e fluindo.

##### <a name="animation-properties"></a>Propriedades de animação

- Opacidade inicial: 0% para esmaeçando, 100% para esmaecer

- Opacidade final: 100% para esmaeçando, 0% para esmaecer

- Duração: 200 milissegundos autônomos, 100 milissegundos quando usado como parte de uma sequência de animação de combinação

- Estilo de easing: Sine InOut

##### <a name="examples"></a>Exemplos

- Ocultar janelas de ferramentas automaticamente

- Menu abrir e fechar

- Transições de guia em segundo plano e plano

#### <a name="color-blend-from-a-to-b"></a>Combinação de cores de A a B
Com esse padrão, um elemento de interface do usuário muda da cor A para a cor B.

![Animação de combinação de cores](../../extensibility/ux-guidelines/media/1202-d_colorblend.png "1202-d_ColorBlend")<br />Animação de combinação de cores

##### <a name="correct-usage"></a>Uso correto
Como uma transição animada quando um elemento de interface do usuário altera a cor de um contexto ou estado para outro.

##### <a name="animation-properties"></a>Propriedades de animação

- Cor inicial: específica da interface do usuário

- Cor final: específica da interface do usuário

- Duração: 200 milissegundos autônomos, 100 milissegundos quando usado como parte de uma sequência de animação de combinação

- Estilo de easing: Sine InOut

##### <a name="examples"></a>Exemplos

- Transições de estado da janela do documento (ativa, última ativa e inativa)

- Transições de estado da janela de ferramentas (focadas e desfocaradas)

#### <a name="expand-and-contract"></a>Expandir e contrato
Com esse padrão, um elemento de interface do usuário se expande no X, Y ou em ambas as direções.

![Animação de expansão e contrato](../../extensibility/ux-guidelines/media/1202-e_expandcontract.png "1202-e_ExpandContract")<br />Animação de expansão e contrato

##### <a name="correct-usage"></a>Uso correto
Como uma transição animada quando um elemento de interface do usuário altera o tamanho de um contexto para outro.

##### <a name="animation-properties"></a>Propriedades de animação

- Escala X: % ou dimensão específica (em pixels)

- Escala Y: % ou dimensão específica (em pixels)

- Posição da âncora: geralmente superior esquerdo (para idiomas da esquerda para a direita) ou superior direito (para idiomas da direita para a esquerda)

- Duração: 200 milissegundos autônomos, 100 milissegundos quando usado como parte de uma sequência de animação de combinação

##### <a name="examples"></a>Exemplos

- Expandir e ressuar no painel do Explorador de Arquitetura

- Visual Studio item Página Inicial de 2017 expanda e ressumente

#### <a name="x-y-position-change"></a>Alteração de posição X-Y
Com esse padrão, um elemento de interface do usuário altera sua posição X ou Y ou ambos.

![Animação de alteração de posição X-Y](../../extensibility/ux-guidelines/media/1202-f_xypositionchange.png "1202-f_XYPositionChange")<br />Animação de alteração de posição X-Y

##### <a name="correct-usage"></a>Uso correto
Como uma transição animada quando um elemento de interface do usuário muda de posição de um contexto para outro.

##### <a name="animation-properties"></a>Propriedades de animação

- Iniciando a posição X e Y: específica da interface do usuário

- Terminando a posição X e Y: específica da interface do usuário

- Caminho de movimento: nenhum

- Duração: 200 milissegundos autônomos, 100 milissegundos quando usado como parte de uma sequência de animação de combinação

- Estilo de easing: Sine InOut

##### <a name="example"></a>Exemplo
Reordenação de guias

#### <a name="rotate"></a>Rotate
Com esse padrão, o elemento de interface do usuário gira.

![Animação de rotação do elemento da interface do usuário](../../extensibility/ux-guidelines/media/1202-g_rotate.png "1202-g_Rotate")<br />Animação de rotação do elemento da interface do usuário

##### <a name="correct-usage"></a>Uso correto
Somente para o indicador de progresso de rotação indeterminado.

##### <a name="animation-properties"></a>Propriedades da animação

- Grau de rotação: 360

- Centro de rotação: meio do objeto

- Duração: contínua

##### <a name="example"></a>Exemplo
Indicador de progresso indeterminado (girando)

### <a name="common-shell-ui-actions-and-recommended-animations"></a>Ações de interface do usuário do Shell comuns e animações recomendadas

#### <a name="tab-open"></a>Abrir guia
![Animação aberta de tabulação](../../extensibility/ux-guidelines/media/1202-h_tabopen.png "1202-h_TabOpen")<br />Animação aberta de tabulação

- Estilo: aparece

- Duração: zero segundos

#### <a name="tab-close"></a>Fechamento de guia
![Animação de fechamento de guia](../../extensibility/ux-guidelines/media/1202-i_tabclose.png "1202-i_TabClose")<br />Animação de fechamento de guia

- Estilo: alteração da posição X

- Duração: 200 milissegundos

#### <a name="tab-reorder"></a>Reordenação da guia
![Reordenar animação de guia no Visual Studio](../../extensibility/ux-guidelines/media/1202-j_tabreorder.png "1202-j_TabReorder")<br />Animação reordenar a guia

- Estilo: alteração da posição X

- Duração: 200 milissegundos

#### <a name="close-floating-document"></a>Fechar documento flutuante
![Fechar animação de documento flutuante](../../extensibility/ux-guidelines/media/1202-k_closefloatingdocument.png "1202-k_CloseFloatingDocument")<br />Fechar animação de documento flutuante

- Estilo: aparece

- Duração: 200 milissegundos

#### <a name="window-state-transition"></a>Transição de estado da janela
![Animação da transição de estado da janela](../../extensibility/ux-guidelines/media/1202-l_windowstatetransition.png "1202-l_WindowStateTransition")<br />Animação da transição de estado da janela

- Estilo: para ser consistente com outras janelas, deixe que o sistema operacional atual defina a animação fechar documento.

- Duração: 200 milissegundos

#### <a name="menu-open"></a>Menu aberto
![Menu abrir animação](../../extensibility/ux-guidelines/media/1202-m_menuopen.png "1202-m_MenuOpen")<br />Menu abrir animação

- Estilo: fade-in

- Duração: 200 milissegundos

#### <a name="menu-close"></a>Fechar menu
![Animação do menu fechar](../../extensibility/ux-guidelines/media/1202-n_menuclose.png "1202-n_MenuClose")<br />Animação do menu fechar

- Estilo: esmaecimento

- Duração: 200 milissegundos

#### <a name="auto-hide-tool-window-reveal"></a>Revelar a janela de ferramentas automaticamente
![Mostrar animação da janela de ferramentas automaticamente](../../extensibility/ux-guidelines/media/1202-o_autohidetoolwindowreveal.png "1202-o_AutoHideToolWindowReveal")<br />Mostrar animação da janela de ferramentas automaticamente

- Estilo: aparece

- Duração: zero segundos
