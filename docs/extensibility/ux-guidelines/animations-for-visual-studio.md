---
title: Animações para Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 446773a9-e6f7-4c0c-8dbc-9e303bf32eb1
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3f28e4d6f9ae1a0af060723047621b3e205d012c
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31148932"
---
# <a name="animations-for-visual-studio"></a>Animações para Visual Studio
## <a name="animation-fundamentals"></a>Conceitos básicos de animação  
  
### <a name="animation-best-practices-in-visual-studio"></a>Práticas recomendadas de animação no Visual Studio  
Siga estas regras para garantir estilos de animação consistentes e amigável entre o Visual Studio IDE.  
  
-   **Tome cuidado.** Limitar animações para aqueles que servem para propósitos específicos.  
  
-   **Tempo e velocidade são importantes** para garantir que faz a transição se sentir natural e rápida:  
  
    -   Conclua as transições animadas no meio de um segundo (500 milissegundos).  
  
    -   Animações que podem ocorrer com frequência precisam ser rápido o suficiente para que eles não interrompam o fluxo de trabalho do usuário. Assista a animação em um loop e ajustar o tempo até que parece correto. 
  
    -   Animações não devem ser tão rápido ou gritante que é difícil de entender, mas não tão lento que faz um impaciente a transição concluir.  
  
    -   Use o tempo de variável para enfatizar a importância. Por exemplo, ao navegar por meio de uma sequência de itens em um diagrama de classe, velocidade por meio de transições entre itens e lenta para se concentrar em itens importantes.  
  
-   **Usar a atenuação não linear gradual** de um estado para outro, dar movimento calmo e natural.  
  
-   Quando possível, **usar uma animação sutil em foco** para indicar os elementos interativos sob o mouse.  
  
-   Se você depende fortemente de animações em seus recursos, em seguida, **fornecem um meio para desativá-los** localmente (para todos os seus recursos) como uma opção no **Ferramentas > Opções** caixa de diálogo.  
  
-   **Apenas uma animação deve ocorrer em um horário** e transmitir apenas uma parte das informações. Mais de um objeto movendo ou tentando transmitir várias coisas que pode ser confuso. 
  
-   **Recurso é importante.** Na maioria dos casos, animação não precisa de atenção do usuário de demanda para atender a sua finalidade. Alterações sutis no tempo, sequenciamento e comportamento podem afetar significativamente a percepção e podem fazer a diferença entre uma animação eficaz e eficiente.  
  
-   Ao usar animação para chamar a atenção para algo, **Certifique-se de que vale a pena interromper o usuário**da sequência de ideias.  
  
-   **Ao mostrar o progresso ou status** através de animação:  
  
    -   Pare de mostrar com que o movimento de progresso quando o processo subjacente não Avançar. 
  
    -   Distingui indeterminados processos dos processos de determinada.  
  
    -   Verifique se uma animação tem identificação de estados de conclusão e falha.  
  
    -   Minimize o uso de animações do efeito que mostram o status e certifique-se de que eles têm valor real, fornecendo informações adicionais de uso real. Em caso de emergência e alterações de status transitório exemplos  
  
#### <a name="animation-donts"></a>Dicas de animação:
  
-   Não use pequenos movimentos (movimentação em uma superfície pequena). Preferir fades e muda com movimentação de objetos.  
  
-   Não use animações que ocorrem em uma grande área da tela de imóveis. Independentemente do tamanho, esse estilo de animação é causa uma distração para o usuário.  
  
-   Não use animações não relacionados para o objeto que o usuário está atualmente focalizado ou interagir com.  
  
-   Não use animações que requerem interação do usuário para redefinir o estado, como forçar o usuário a responder a uma notificação intermitente para ativá-lo parar piscando. Interagir com eles, de qualquer forma deve ser suficiente para descartá-los.  
  
Para obter mais informações sobre aplicativos essas práticas recomendadas, consulte [padrões de animação](../../extensibility/ux-guidelines/animations-for-visual-studio.md#BKMK_AnimationPatterns).  
  
### <a name="animation-metrics"></a>Métricas de animação  
  
-   O sistema visivelmente deve reagir a gestos do usuário em menos de 10 milissegundos.  
  
-   Transições animadas não devem levar mais de 500 milissegundos para concluir.  
  
-   É uma maneira para compensar transições que exigem mais vezes para separá-lo em duas partes. Por exemplo, a primeira parte de uma animação poderia ser o contêiner de conteúdo vazio (até 500 milissegundos), seguido de esmaecimento do conteúdo no contêiner (até 500 milissegundos).  
  
-   Para os tempos de carregamento podem ser calculados, um indicador de progresso determinante (indicador de progresso feito por cento) é preferencial.  
  
-   Para os tempos de carregamento não podem ser calculados, um indicador de disponibilidade como um cursor ou animação giratório inseridos (ou indicador do trabalho de carregamento) é apropriado.  
  
### <a name="animation-as-communicator"></a>Animação como communicator  
Na IU do Visual Studio, animação funciona apenas como uma ferramenta de comunicação.  Ele é usado para comunicar uma variedade de informações, como alterações estruturais na interface de usuário (por exemplo, quando um menu é aberta ou fechada). Animação pode ajudar a visualizar o comportamento dependente de tempo dos sistemas complexos, como a visualização de andamento da instalação. Animações também podem ser usadas para atrair atenção com alertas e notificações.  
  
 Animações de interface do usuário normalmente funcionam em quatro maneiras: visualizar, atrair atenção, simular, e tempos de resposta/indicadores de progresso.  
  
#### <a name="visualize"></a>Visualizar  
Animação pode enfatizar a natureza tridimensional de objetos e tornar mais fácil para os usuários visualizar sua estrutura espacial. Para fazer isso, a animação pode necessário para girar o objeto em um círculo completo, lentamente ativá-la e para trás, ou colocar o objeto mais próximo e ligeiramente aumentar seu tamanho para enfatizar a substituição ou o foco.  
  
Embora objetos tridimensionais podem ser movidos com o controle de usuário, o designer deve determinar antecipadamente (programaticamente ou manualmente) como a melhor animar um movimento que fornece melhor compreensão do objeto. Isso programado animação pode então ser ativado pelo usuário, colocando o cursor sobre o objeto, enquanto movimentações controlado pelo usuário requerem que o usuário entender como manipular o objeto. Limitar a movimentação para um único eixo ou orientação ao mesmo tempo; em escala, girar, ou converter, mas não faça mais de uma simultaneamente.  
  
A categoria de visualizar inclui os aspectos dos dados, relacionamentos, estado, estrutura, a sequência e tempo.  
  
##### <a name="data"></a>Dados  
Ilustram as informações de variáveis e complexas:  
  
-   Movendo por meio de visualizações de informações como quadros e gráficos  
  
-   Percorrendo uma sequência tour guiado e paginação  
  
-   Chamada de detalhes, apontando e realce informações específicas  
  
-   Sobreposição de detalhes e informações adicionais sobre um elemento focalizado atualmente
  
-   Metamorfose de uma representação estrutural ou organizacional para outro  
  
-   Que representa as alterações ao longo do tempo usando controles deslizantes de tempo, rodas giratória e painel e os controles de transporte (reproduzir, parar e Pausar) 
  
##### <a name="relationships"></a>Relações  
  
-   Ilustrar como os itens estão relacionados entre si ou quais itens estão relacionados a um determinado item
  
-   Mostrar hierarquias e pai-filho ou irmão relações
  
-   Um elemento gera outra
  
-   Um elemento minimiza a outro elemento
  
-   Um elemento vinculado para outra
  
##### <a name="state"></a>Estado  
  
-   Atualizações de conteúdo
  
-   A seleção e o foco do usuário  
  
-   Progresso  
  
-   Erros  
  
##### <a name="structure"></a>Estrutura  
  
-   A estrutura em um nó a dinamização  
  
-   Reorientação  
  
-   Minimizar e maximizar, ou expandir e recolher  
  
##### <a name="sequence"></a>Sequência  
  
-   Sequência de apresentação de slides  
  
-   Invertendo por meio de imagens  
  
##### <a name="time"></a>Hora  
  
-   Alteração de mostrar ao longo do tempo, tempo decorrido e screencast  
  
-   Mover para a Lixeira, desfazer e refazer  
  
-   Restaurar o estado do histórico  
  
#### <a name="attract-attention"></a>Atrair atenção  
Se a meta é chamar a atenção do usuário para um único elemento fora várias ou para alertar o usuário para as informações atualizadas, uma animação talvez seja adequada. Por exemplo, sua página inicial do aplicativo pode usar um botão de Introdução slides em vigor depois que a página for carregada.  
  
Como regra, o último elemento móvel na tela atrai do usuário.  Em uma série de elementos animados, a atenção do usuário será feita após o último objeto móvel.  
  
##### <a name="alert"></a>Alerta  
  
-   Alertar o usuário, chamar a atenção, mostrar o progresso  
  
-   Mostrar que algo está sendo feito corretamente ou não ou mostrar o progresso ou as alterações de andamento  
  
-   Solicitar que os usuários durante uma tarefa, como localizar mais informações online ou aprendendo sobre a tarefa atual  
  
##### <a name="notifications"></a>Notificações  
  
-   Alertar o usuário sobre uma condição de erro  
  
-   Interromper o usuário para ver se gostaria de participar de outra coisa  
  
-   Com cuidado, informar ao usuário que um processo foi concluído ou alterada, como quando um download for concluído.  
  
#### <a name="simulate"></a>Simular  
Esta categoria abrange relacionamento físico tem posto e dimensionalidade.  
  
-   Ilustrar onde os objetos vêm do ou em que eles ir para  
  
-   Expandir e recolher ou abrir e fechar  
  
-   Ativa o movimento panorâmico rolagem e página  
  
-   Empilhamento e ordem z  
  
-   Carrossel e accordion  
  
-   Invertendo e girando da interface do usuário  
  
#### <a name="response-and-progress-indicators"></a>Indicadores de progresso e de resposta  
Indicadores de progresso tem algumas vantagens importantes:  
  
-   Ambos os indicadores de progresso determinada e indeterminado garantir que o usuário que o sistema não falhou e o problema está trabalhando.  
  
-   Indicadores de determinada dar ao usuário que uma noção da quanto ao longo de ação está em andamento, bem como a sensação de receber mais próximo o término.  
  
##  <a name="BKMK_AnimationPatterns"></a> Padrões de animação  
  
### <a name="overview"></a>Visão geral  
Animações no Visual Studio devem atender a uma função específica sem diminuir a produtividade do usuário. Geralmente, animações no Visual Studio devem ser:  
  
-   Pequenas e discreto  
  
-   Naturais e realistas  
  
-   Sutis e subdued  
  
-   Rápidos e eficientes  
  
-   Relaxada, não com pressa  
  
Esta ilustração mostra os estilos de animação, que é recomendável para o Visual Studio. Nenhuma animação ou animações sutis que desaparecer / desaparecer são usadas com mais frequência. Aplicativo limitado de animações de movimento como expandir e contrair, posições de X e Y alteração e a rotação. 
  
![Estilos de animação recomendados para o Visual Studio](../../extensibility/ux-guidelines/media/1202-a_vsanimstyles.png "a_VSAnimStyles 1202")<br />Estilos de animação recomendado para o Visual Studio
  
#### <a name="appear-and-disappear"></a>Aparecem e desaparecem  
Com esse padrão, um elemento alterna do visível para fora do modo de exibição e sem uma animação de transição.  
  
![Aparecem e desaparecem animação](../../extensibility/ux-guidelines/media/1202-b_appearanddisappear.png "b_AppearAndDisappear 1202")<br />Aparecem e desaparecem animação  
  
##### <a name="correct-usage"></a>Uso correto  
Elementos de interface do usuário atualizados que precisam instantaneamente aparecer ou desaparecer para que o usuário não é distraiam nem obstruído. Além disso, animações lentos, podem ser consideradas como arrastar um desempenho, o que não ocorre com o estilo aparecem e desaparecem.  
  
##### <a name="incorrect-usage"></a>Uso incorreto  
Casos em que interface do usuário aparece abruptamente que o usuário tem não sabe o que aconteceu e ajuda a adicionar uma animação com entendimento contextual.  
  
##### <a name="animation-properties"></a>Propriedades de animação  
Geralmente, o tempo de espera é zero segundos.  
  
##### <a name="examples"></a>Exemplos    
-   Janelas de ferramentas de ocultar automaticamente  
  
-   Editor de teclado ativado da interface do usuário, como IntelliSense e a Ajuda do parâmetro  
  
-   Regiões de expandir e recolher código  
  
#### <a name="fade-in-and-fade-out"></a>Fade in e fade-out  
Com esse padrão, um elemento de interface do usuário faz a transição de não visível (0% de opacidade) visível (100% de opacidade) ou vice-versa.  
  
![Animação gradualmente e esmaecimento](../../extensibility/ux-guidelines/media/1202-c_fadeinfadeout.png "c_FadeInFadeOut 1202")<br />Animação gradualmente e esmaecimento  
  
##### <a name="correct-usage"></a>Uso correto  
Isso é o mais recomendado animação de interface do usuário. É um efeito sutil que adiciona interesse sem interromper o fluxo. Em alguns casos, o usuário pode nem mesmo perceber que há uma animação perceber um smooth e fluxo de sistema de interface do usuário.  
  
##### <a name="animation-properties"></a>Propriedades de animação  
  
-   Iniciando a opacidade: 0% para gradualmente, 100% de esmaecimento  
  
-   Terminando a opacidade: 100% para gradualmente, 0% de esmaecimento  
  
-   Duração: 200 milissegundos autônomo, 100 milissegundos quando usado como parte de uma sequência de animação de combinação  
  
-   Estilo de atenuação: InOut seno  
  
##### <a name="examples"></a>Exemplos  
  
-   Janelas de ferramentas de ocultar automaticamente  
  
-   Menu de abertura e fechamento  
  
-   Transições de guia de plano e plano de fundo  
  
#### <a name="color-blend-from-a-to-b"></a>Mistura de cores de A para B  
Com esse padrão, um elemento de interface do usuário muda de cor A cor B.  
  
![Cor do blend animação](../../extensibility/ux-guidelines/media/1202-d_colorblend.png "d_ColorBlend 1202")<br />Animação de mesclagem de cor  
  
##### <a name="correct-usage"></a>Uso correto  
Como uma transição animada quando um elemento de interface do usuário altera a cor de um contexto ou estado para outro.  
  
##### <a name="animation-properties"></a>Propriedades de animação  
  
-   A cor inicial: interface do usuário específico  
  
-   Terminando cor: interface do usuário específico  
  
-   Duração: 200 milissegundos autônomo, 100 milissegundos quando usado como parte de uma sequência de animação de combinação  
  
-   Estilo de atenuação: InOut seno  
  
##### <a name="examples"></a>Exemplos  
  
-   Transições de estado da janela de documento (ativo, última ativas e inativas)  
  
-   Transições de estado da janela de ferramenta (focada e foco)  
  
#### <a name="expand-and-contract"></a>Expandir e contrair  
Com esse padrão, um elemento de interface do usuário se expande em X, Y ou ambas as direções.  
  
![Expandir e contrair animação](../../extensibility/ux-guidelines/media/1202-e_expandcontract.png "e_ExpandContract 1202")<br />Expandir e contrair de animação  
  
##### <a name="correct-usage"></a>Uso correto  
Como uma transição animada quando um elemento de interface do usuário altera o tamanho de um contexto para outro.  
  
##### <a name="animation-properties"></a>Propriedades de animação  
  
-   Escala x: % ou uma dimensão específica (em pixels)  
  
-   Escala Y: % ou uma dimensão específica (em pixels)  
  
-   Posição de ancoragem: geralmente superior esquerda (para idiomas da esquerda para direita) ou superior direito (para idiomas da direita para esquerda)  
  
-   Duração: 200 milissegundos autônomo, 100 milissegundos quando usado como parte de uma sequência de animação de combinação  
  
##### <a name="examples"></a>Exemplos  
  
-   Painel do Explorer de arquitetura de expansão e recolhimento  
  
-   Item de página inicial expandir e recolher  
  
#### <a name="x-y-position-change"></a>Alteração de posição X-Y  
Com esse padrão, um elemento de interface do usuário altera a posição X ou Y ou ambos.  
  
![Alterar a posição de X-Y animação](../../extensibility/ux-guidelines/media/1202-f_xypositionchange.png "f_XYPositionChange 1202")<br />Animação de alteração de posição X-Y  
  
##### <a name="correct-usage"></a>Uso correto  
Como uma transição animada quando um elemento de interface do usuário altera a posição de um contexto para outro.  
  
##### <a name="animation-properties"></a>Propriedades de animação  
  
-   Posição inicial X e Y: interface do usuário específico  
  
-   Posição final X e Y: interface do usuário específico  
  
-   Caminho de movimento: nenhum  
  
-   Duração: 200 milissegundos autônomo, 100 milissegundos quando usado como parte de uma sequência de animação de combinação  
  
-   Estilo de atenuação: InOut seno  
  
##### <a name="example"></a>Exemplo  
Reorganização de guia  
  
#### <a name="rotate"></a>Girar  
Com esse padrão, o elemento de interface do usuário gira.  
  
![Animação de rotação do elemento de interface do usuário](../../extensibility/ux-guidelines/media/1202-g_rotate.png "g_Rotate 1202")<br />Animação de rotação do elemento de interface do usuário  
  
##### <a name="correct-usage"></a>Uso correto  
Somente para o indicador de progresso indeterminado giratório.  
  
##### <a name="animation-properties"></a>Propriedades de animação  
  
-   Grau de rotação: 360  
  
-   Centro de rotação: intermediária do objeto  
  
-   Duração: contínua  
  
##### <a name="example"></a>Exemplo  
Indicador de progresso indeterminado (rotação)  
  
### <a name="common-shell-ui-actions-and-recommended-animations"></a>Ações de interface de usuário comuns do shell e animações recomendadas  
  
#### <a name="tab-open"></a>Guia Abrir  
![Guia animação abrir](../../extensibility/ux-guidelines/media/1202-h_tabopen.png "h_TabOpen 1202")<br />Animação aberta TAB  
    
-   Estilo: aparecem  
  
-   Duração: segundos zero  

#### <a name="tab-close"></a>Guia fechar  
![Guia animação fechar](../../extensibility/ux-guidelines/media/1202-i_tabclose.png "i_TabClose 1202")<br />Animação de fechamento de guia  
  
-   Estilo: Alteração da posição X  
  
-   Duração: 200 milissegundos  
  
#### <a name="tab-reorder"></a>Guia reordenar  
![Guia reordenar animação no Visual Studio](../../extensibility/ux-guidelines/media/1202-j_tabreorder.png "j_TabReorder 1202")<br />Guia reordenar animação

-   Estilo: Alteração da posição X  
  
-   Duração: 200 milissegundos  
    
#### <a name="close-floating-document"></a>Fechar documentos flutuante  
![Fechar flutuante animação documento](../../extensibility/ux-guidelines/media/1202-k_closefloatingdocument.png "k_CloseFloatingDocument 1202")<br />Animação de documentos flutuante fechar  
   
-   Estilo: aparecem  
  
-   Duração: 200 milissegundos   
 
#### <a name="window-state-transition"></a>Transição de estado da janela  
![Animação de transição de estado de janela](../../extensibility/ux-guidelines/media/1202-l_windowstatetransition.png "l_WindowStateTransition 1202")<br />Animação de transição de estado de janela  
    
-   Estilo: para ser consistente com outras janelas, permitem que o sistema operacional atual defina animação de fechar o documento.  
  
-   Duração: 200 milissegundos  
  
#### <a name="menu-open"></a>Menu Abrir  
![Animação abrir menu](../../extensibility/ux-guidelines/media/1202-m_menuopen.png "m_MenuOpen 1202")<br />Animação abrir menu  
    
-   Estilo: gradualmente  
  
-   Duração: 200 milissegundos  
  
#### <a name="menu-close"></a>Feche o menu  
![Animação de menu fechar](../../extensibility/ux-guidelines/media/1202-n_menuclose.png "n_MenuClose 1202")<br />Animação de fechamento de menu  
    
-   Estilo: esmaecimento  
  
-   Duração: 200 milissegundos  
  
#### <a name="auto-hide-tool-window-reveal"></a>Ocultar automaticamente revelação da janela de ferramenta  
![Ocultar automaticamente animação de revelação de janela de ferramenta](../../extensibility/ux-guidelines/media/1202-o_autohidetoolwindowreveal.png "o_AutoHideToolWindowReveal 1202")<br />Ocultar automaticamente animação de revelação de janela de ferramenta  

-   Estilo: aparecem  
  
-   Duração: segundos zero