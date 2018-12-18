---
title: Padrões de composição para Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e48ecfb2-f4b5-4d3a-b4a2-7a4d62fa4ec0
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 4460adc56b139cf89cbd0192efd9f453da9070b5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51734428"
---
# <a name="composite-patterns-for-visual-studio"></a>Padrões de composição para Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Padrões compostos combinam elementos de design e interação em configurações distintas. Alguns dos mais importantes compostos padrões no Visual Studio em relação à consistência incluem:  

-   [Visualização de dados](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_DataVisualization)  

-   [Interface do usuário no objeto e inspecionar](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_OnObjectUI)  

-   [Modelos de seleção](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_SelectionModels)  

-   [Salvando as configurações e persistência](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_PersistenceAndSavingSettings)  

-   [Entrada de toque](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_TouchInput)  

##  <a name="BKMK_DataVisualization"></a> Visualização de dados  

### <a name="overview"></a>Visão geral  
 Os gráficos são uma maneira visual de agregação e visualizar os dados a fim de melhorar a tomada de decisões. Eles podem ajudar os usuários enfrentados muitos dados, mas pouco ou seja, veja o que merece atenção e o que pode precisar de uma ação.  

 O usuário se beneficiará de um gráfico se qualquer uma das seguintes condições forem verdadeiras:  

-   O gráfico possam ajudar os usuários a identificar as tarefas que podem atuar em?  

-   O gráfico permitirá que os usuários prever as consequências de possíveis alterações?  

-   O gráfico ajudará os usuários descobrir tendências e identificar padrões?  

-   O gráfico permitirá que os usuários a tomar decisões melhores?  

-   O gráfico ajudará a responder a perguntas específicas que os usuários podem ter no contexto fornecido?  

#### <a name="general-rules-for-charts"></a>Regras gerais para gráficos  

-   Rotular dados claramente. Ilustrações sem explicação são apenas belas fotos.  

-   Inicie eixos em zero para evitar distorcer proporções. Tamanho da linha de comprimento e barra são indicações visuais importantes para entender as relações entre os pontos de dados.  

-   Crie gráficos, não infográficos. Infográficos são artísticas representações de dados e seu objetivo principal é narração visual. Gráficos pode (e deve) ser visualmente atraente, mas permitir que os dados falem por si próprios.  

-   Evite skeumorphism, ilustrados gráficos de barras, marcas de hash de contraste e outras toques do infográfico.  

-   Não use efeitos 3D como um elemento decorativo. Use-as apenas se eles realmente integral para a capacidade do usuário a compreender as informações.  

-   Evite usar várias linhas e preenchimentos, como mais de duas cores podem fazer esse tipo de gráfico difícil de ler e interpretar corretamente.  

-   Não use um gráfico (ou qualquer ilustração) como o único meio de um conceito de compreensão ou interagir com os dados. Isso apresenta dificuldades para os usuários com deficiências visuais.  

-   Não use gráficos como elementos decorativos ou gratuitos em uma página. Em outras palavras, se um gráfico não adiciona que qualquer valor ou ajuda usuários a resolver um problema, não o use.  

### <a name="chart-types"></a>Tipos de gráfico  
 Tipos de gráficos usados no Visual Studio incluem gráficos de barras, gráficos de linhas, um gráfico de pizza modificado, conhecido como um gráfico de anel ou "gráfico de rosca," linhas do tempo, gráficos (também chamados de "cluster gráficos") e os gráficos de Gantt de dispersão. Cada tipo de gráfico é útil para comunicar-se um tipo diferente de informações.  

### <a name="other-charting-considerations"></a>Outras considerações sobre a criação de gráficos  

#### <a name="color"></a>Cor  
 Há uma paleta específica dos gráficos de cores definidas para uso no Visual Studio. A paleta é acessível para os tipos principais de daltonismo e as cores podem ser diferenciadas, mesmo quando usados como muito estreitas fatias da cor. Você pode usar essas cores em qualquer combinação para qualquer tipo de gráfico na sua interface do usuário. Você não precisa usar todas as cores de sete, se você não precisa que muitas cores distintas. Essas cores não foram projetados para ser usado com qualquer elemento de primeiro plano, portanto, não coloque texto ou glifos sobre essas cores. Esses matizes devem ser embutido em código e expostas para personalização de usuário sob **Ferramentas > Opções** (consulte [expondo as cores para os usuários finais](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ExposingColorsForEndUsers)).  

|Amostra de|Hex|RGB|  
|------------|---------|---------|  
|![Amostra 71B252](../../extensibility/ux-guidelines/media/0711-71b252.png "0711_71B252")|#71B252|113,178,82|  
|![Amostra BF3F00](../../extensibility/ux-guidelines/media/0711-bf3f00.png "0711_BF3F00")|#BF3F00|191,63,0|  
|![Amostra FCB714](../../extensibility/ux-guidelines/media/0711-fcb714.png "0711_FCB714")|#FCB714|252,183,20|  
|![Amostra 903F8B](../../extensibility/ux-guidelines/media/0711-903f8b.png "0711_903F8B")|#903F8B|144,63,139|  
|![Amostra 117AD1](../../extensibility/ux-guidelines/media/0711-117ad1.png "0711_117AD1")|#117AD1|17,122,209|  
|![Amostra 79D7F2](../../extensibility/ux-guidelines/media/0711-79d7f2.png "0711_79D7F2")|#79D7F2|121,215,242|  
|![Amostra B5B5B5](../../extensibility/ux-guidelines/media/0711-b5b5b5.png "0711_B5B5B5")|#B5B5B5|181,181,181|  

##  <a name="BKMK_OnObjectUI"></a> Interface do usuário no objeto e inspecionar  
 Esta seção fornece contexto para inspecionar, também conhecida como exibição de inspeção de código, um tipo de interface do usuário no objeto exclusivo para o Visual Studio.  

### <a name="overview"></a>Visão geral  

- Interface de usuário no objeto deve dar ao usuário obter mais informações ou interatividade sem desviar a atenção de sua tarefa principal.  

- O padrão principal para de objeto da interface do usuário no Visual Studio é conhecido como "informações no ponto de atenção".  

- No objeto de interface de usuário no Visual Studio é um embutido ou flutuante e duráveis ou transitório.  

  -   Visualização de inspeção de código, um tipo de interface de usuário no objeto no Visual Studio, é embutida e duráveis.  

  -   O CodeLens, um tipo de interface de usuário no objeto no Visual Studio, é temporário e flutuante  

  Noções básicas sobre como funciona um trecho de código, ou localizar detalhes sobre esse código, geralmente requer um desenvolvedor alternar o contexto e vá para outros tipos de conteúdo ou de outra janela. Essas mudanças de contexto podem ser prejudicial, pois os usuários podem perder o foco na sua tarefa original se eles deixam a janela principal. Além disso, obtendo que back do contexto original pode ser difícil, especialmente se alternar windows causou seu código original para ser obscurecido por outro da interface do usuário.  

  Interface de usuário no objeto segue um padrão chamado "informações no ponto de atenção". Essas mensagens, janelas pop-up e caixas de diálogo dar aos usuários informações adicionais relevantes que adiciona esclarecimento ou interatividade sem perder o foco na sua tarefa principal. Exemplos de objeto da interface do usuário incluem janelas pop-up que aparecem quando um usuário passar o ponteiro sobre um ícone na área de notificação, o Rabisco vermelho sob uma palavra incorreta e o modo de exibição de espiada introduzido no Visual Studio 2013.  

### <a name="decision-points"></a>Pontos de decisão  
 No Visual Studio, há várias maneiras de usar esse padrão de informações no ponto de atenção. Escolhendo o mecanismo certo e implementá-lo de maneira consistente e previsível são essencial para a experiência geral. Caso contrário, podem ser apresentada aos usuários uma experiência confusa ou inconsistente que reduz o foco do próprio conteúdo.  

#### <a name="relationships-between-master-and-detail-content"></a>Relações entre o mestre e de conteúdo de detalhes  
 Informações no ponto de atenção são usadas para exibir uma relação entre o conteúdo que o usuário está focalizado (o conteúdo "mestre") e adicionais relacionados ao conteúdo (o conteúdo de "Detalhes"). Nesse padrão, o conteúdo de detalhes é claramente relacionado ao conteúdo o usuário está trabalhando com e pode ser exibido perto o conteúdo mestre. Informações complementares ou informações que não podem ser resumidas sem sobrecarregar o conteúdo mestre devem seguir o padrão de outro, como uma janela de ferramentas.  

-   **Sempre** exibir o conteúdo de detalhes em estreita proximidade com o conteúdo mestre.  

-   **Sempre** Certifique-se de que o conteúdo de detalhes ainda permite que um usuário concentre-se no conteúdo mestre. Muitas vezes, a melhor maneira de conseguir isso é renderizar o conteúdo de detalhes como perto o conteúdo mestre quanto possível. Isso pode ser feito ao processar o conteúdo de detalhes em uma janela pop-up ao lado do conteúdo mestre ou ao renderizar o conteúdo embutido de detalhes sob o conteúdo mestre.  

-   **Nunca** usar informações no ponto de atenção que leva o usuário para fora o conteúdo mestre. Se os usuários precisam exibir o conteúdo de detalhes separadamente, expor uma ação explícita que permite ao usuário fazer isso.  

#### <a name="design-details"></a>Detalhes de design  
 Depois de ter determinado no objeto de interface de usuário é a escolha certa, há quatro considerações de design principal:  

1. **Persistência:** o conteúdo deve ser durável ou transitório?   
   Os usuários desejam manter as informações visíveis para se referir a ou interagir com? Ou, os usuários desejarão olhei rapidamente as informações e, em seguida, continue com a sua principal tarefa?  

2. **Tipo de conteúdo:** o conteúdo será informativa, acionáveis ou navegação?   
   O usuário precisa obter mais detalhes sobre o conteúdo mestre? O usuário que precisa para concluir uma tarefa que afeta o conteúdo mestre? Ou o usuário precisa ser direcionado para outro recurso?  

3. **Tipo de indicador:** um indicador de ambiente faz sentido?   
   As informações podem ser resumidas de uma maneira útil e exibidas sem sobrecarregar o conteúdo mestre?  

4. **Gestos:** gestos do que serão usado para invocar e ignorar a interface do usuário?   
   Como será o usuário abrir o conteúdo de detalhes e enviá-lo imediatamente? Há um valor para adicionar um gesto, como fixação para alternar entre os estados transitórios e duráveis?  

   Cada um desses pontos de quatro decisão terá um impacto sobre os principais componentes da interface de usuário no objeto.  

### <a name="on-object-ui-components"></a>Componentes de interface do usuário no objeto  

1.  Tipo de contêiner (apresentador de conteúdo)  

    -   Flutuante  

    -   Embutido  

2.  Tipo de conteúdo  

    -   Informação: dados que podem ser estáticos ou dinâmicos  

    -   Acionáveis: comandos que alteram o conteúdo mestre  

    -   Navegação: links que levam o usuário a outra janela ou aplicativo, como o MSDN  

3.  Gestos  

    -   Invocação  

    -   Exoneração  

    -   A fixação  

    -   Outras interações  

4.  Modelo de persistência e confirmar  

    -   Transitório  

    -   duráveis  

    -   Automático  

    -   Sob demanda  

5.  Indicadores de ambientes (opcionais)  

    -   Sublinhado de rabisco  

    -   Ícone de marca inteligente  

    -   Outros indicadores de ambientes  

#### <a name="container-content-presenter-type"></a>Tipo de contêiner (apresentador de conteúdo)  
 Há duas opções principais disponíveis para apresentar conteúdo no ponto de atenção:  

1.  **Embutido:** um apresentador embutido, como a exibição de espiada que foi apresentado no Editor do Visual Studio 2013 código, torna o espaço para o novo conteúdo com a mudança de conteúdo existente.  

    -   **Prefira** embutido apresentadores se você espera que os usuários desejarão gastam uma quantidade significativa de tempo referindo-se a ou interagir com o conteúdo que você apresenta.  

    -   **Evite** embutido apresentadores se você espera que os usuários desejarão olhando as informações que você apresente e continuar sua tarefa principal com interrupção mínima.  

2.  **Flutuante:** um apresentador flutuante é posicionado o mais próximo possível conteúdo selecionado, mas não altera o layout do conteúdo existente. Várias estratégias podem ser empregadas, como a exibição de um painel flutuante de conteúdo sobre o mais próximo de espaço em branco disponível para o símbolo selecionado.  

    -   **Prefira** flutuante apresentadores se você espera que os usuários desejarão olhei as informações que você apresente e continuar sua tarefa principal com interrupção mínima.  

    -   **Evite** flutuante apresentadores se você espera que os usuários desejarão gastam uma quantidade significativa de tempo referindo-se a ou interagir com o conteúdo você presente.  

#### <a name="content-type"></a>Tipo de conteúdo  
 Há três principais tipos de conteúdo que pode ser exibido dentro de qualquer contêiner de interface do usuário no objeto. Qualquer combinação desses tipos de informações pode ser mostrada. Os três tipos são:  

1.  **Informação:** mais contêineres de interface do usuário exibirá algum tipo de conteúdo informativo ao objeto. O conteúdo pode representar informações sobre o estado atual do ambiente ou ele pode representar informações sobre uma potencial estado futuras do ambiente. Por exemplo, ele pode ser usado para mostrar o efeito de um comando específico, como uma refatoração, no código existente.  

    -   **Sempre** usar as informações que você exibir a representação canônica. Por exemplo, o código deve se parecer com o código, completo com realce de sintaxe e deve respeitar a fonte e outras configurações de ambiente que o usuário tiver definido.  

    -   **Sempre** considere dar suporte a quaisquer ações sobre o conteúdo informativo que seria possível se a mesma informação é apresentada como conteúdo mestre. Por exemplo, se apresentar o código existente dentro de um contêiner de interface do usuário no objeto, considere seriamente a capacidade de navegar e modificar o código de suporte.  

    -   **Sempre** considere o uso de uma cor de plano de fundo diferente se apresentar o conteúdo informativo que representa um estado de futuras potencial.  

2.  Acionáveis: alguns contêineres de interface do usuário no objeto fornecerá a capacidade de realizar alguma ação sobre o conteúdo mestre, como executar uma operação de refatoração.  

    -   **Sempre** posicionar acionáveis comandos separadamente do conteúdo informativo.  

    -   **Sempre** habilitar e desabilitar ações quando apropriado.  

    -   **Sempre** consulte as diretrizes padrão para representar os comandos nas caixas de diálogo.  

    -   **Sempre** manter o número de ações que são expostas em um contêiner de interface do usuário no objeto absoluta mínimo. Interagindo com a interface de usuário no objeto deve ser uma experiência leve e rápida. O usuário não deve ter com o custo de energia sobre como gerenciar o contêiner de interface do usuário no objeto em si.  

    -   **Sempre** considerar como e quando um contêiner de interface do usuário no objeto será fechado ou descartado. Como prática recomendada, qualquer ação que conclui a caixa de diálogo entre o mestre e de conteúdo de detalhes deve fechar também o contêiner de interface do usuário no objeto quando essa ação é invocada.  

3.  **Navegação:** alguns no objeto contêineres de interface do usuário incluem links que levam o usuário a outra janela ou aplicativo, como a abertura de um artigo do MSDN no navegador do usuário.  

    -   **Sempre** preceder qualquer link de navegação com "Abrir" para que os usuários não ficará surpreso com a qual se está navegando para algum outro conteúdo.  

    -   **Sempre** separar os links de navegação dos links acionáveis.  

#### <a name="ambient-indicators-optional"></a>Indicadores de ambientes (opcionais)  
 Indicadores de ambientes podem ser sutil, incluindo texto apresentado em uma cor contrastante do restante do código, ou óbvio, incluindo símbolos tickler como sublinhados rabisco e ícones de marca inteligente. Indicadores de ambientes se comunicar a disponibilidade de informações adicionais relevantes. O ideal é que eles fornecem informações úteis mesmo sem exigir que o usuário interagir com eles.  

-   **Sempre** posicionar um indicador de ambiente para que ele não for distraí-lo ou sobrecarregar o usuário. Se for impossível para um ambiente indicador de posição de forma, considere a possibilidade de outra solução.  

-   **Sempre** posicionar o indicador de ambiente mais próximo possível para o conteúdo que está relacionado ao.  

-   **Sempre** tentar criar um indicador que resume as informações que ele disponibiliza. Recomenda-se fornecer uma contagem do número de itens de dados disponíveis (por exemplo, "3 referências", em vez de simplesmente "Referências") ou pensar em alguma outra maneira para resumir os dados.  

    -   Em casos em que os dados para um indicador não podem sempre ser computados e exibidos, considere imediatamente fornecendo comentários progressivo, como os valores são computados. Por exemplo, considere animando alterações que refletem as atualizações dos dados disponíveis, semelhantes à forma como o bloco dinâmico de email no Windows Phone é atualizada conforme o número de aumentos de emails não lidos.  

-   **Nunca** adicionar indicadores mais do que um usuário pode realizar razoavelmente para uma determinada parte do conteúdo. Indicadores de ambientes devem ser útil sem exigir qualquer interação do usuário. Indicadores de perdem seu ambiente se precisarem de estouro e outros controles de gerenciamento para colocá-los em modo de exibição.  

#### <a name="gestures"></a>Gestos  
 Um aspecto importante de permitir que o usuário manter o foco no conteúdo mestre está dando suporte os gestos direito para abrir e ignorar o conteúdo de detalhes adicionais.  

-   **Sempre** exigem que o usuário executar alguma gesto explícito para abrir o conteúdo adicional. Gestos abertos comuns incluem:  

    -   **Passe o mouse:** dicas de ferramenta ou conteúdo informativo não interativo  

    -   **Comando explícito:** apresentador embutido  

    -   **Clique duas vezes o indicador de ambiente:** janela pop-up do CodeLens  

-   **Sempre** ignorar o conteúdo de detalhes, sempre que o usuário pressiona a tecla Esc.  

-   **Sempre** considerar o contexto da interface do usuário no objeto. Para conteúdo apresentadores que permitem a interação dentro do contêiner, considere cuidadosamente se deseja mostrar informações adicionais ao focalizar, que é a probabilidade de ser perturbador para o fluxo de trabalho do usuário.  

-   **Nunca** exibir o conteúdo ao passar o que parece ser editável ou convida interação do usuário. Esse comportamento pode frustrar os usuários se eles tentarem move o cursor sobre o conteúdo de detalhes, como o comportamento padrão para uma dica de ferramenta é descartar imediatamente quando o cursor não estiver mais sobre o mestre de conteúdo que o produziu.  

##  <a name="BKMK_SelectionModels"></a> Modelos de seleção  

### <a name="overview"></a>Visão geral  
 Um modelo de seleção é o mecanismo usado para indicar e confirmar as operações em um ou mais objetos de interesse na interface do usuário. Este tópico aborda os padrões de interação de seleção em editores de documento do Visual Studio: editores de texto, superfícies de design e modelagem de superfícies.  

 Os usuários devem ter uma maneira de indicar para o Visual Studio que eles estão trabalhando, e Visual Studio deve responder previsível com comentários aos usuários sobre o que ele está funcionando no. Diferenças ou um erro de comunicação entre o usuário e a interface do usuário pode resultar no usuário não observar que uma ação, que pode ter consequências não intencionais. Muitas vezes, o erro passa despercebido até que o usuário vê que algo está faltando ou foi alterada. Modelos de seleção, portanto, são uma das partes mais importantes de design da interface do usuário. Embora modelos de seleção no Visual Studio são consistentes com o Windows, há algumas pequenas variações.  

 No Visual Studio, como no Windows, os modelos de seleção diferem dependendo do contexto no qual a interação ocorre. Seleções podem ocorrer em quatro tipos de objetos:  

- Texto  

- Objetos gráficos  

- Listas e árvores  

- Grades  

  Dentro desses objetos, há três tipos de seleções:  

- Contíguos  

- Não contíguas  

- Região  

#### <a name="scope"></a>Escopo  
 O componente mais importante da seleção é garantir que o usuário sabe em qual janela estão trabalhando (ativação) e onde o foco está localizada (seleção). O Visual Studio estende a funcionalidade de gerenciamento de janela no Windows, mas o esquema de ativação é o mesmo: interagir com uma janela traz o foco para a janela. O Visual Studio tem dois indicadores para ativação: um para as janelas do documento e outro para janelas de ferramentas.  

 Para janelas de documento, a janela ativa é indicada por uma guia de janela de documento disponível para a frente e alterando sua cor de plano de fundo:  

 ![Seleção da guia ativa no Visual Studio](../../extensibility/ux-guidelines/media/0713-01-activetab.png "0713 01_ActiveTab")  

 **Seleção da guia ativa**  

 Para janelas de ferramentas, a janela ativa é indicada por uma alteração na cor da área da barra de título da janela de ferramenta:  

 ![Seleção de janela da ferramenta ativa no Visual Studio](../../extensibility/ux-guidelines/media/0713-02-activetoolwindow.png "0713 02_ActiveToolWindow")  

 **Janela da ferramenta ativa está mostrando a seleção primária de um nó**  

 ![Seleção de janela de ferramenta inativos no Visual Studio](../../extensibility/ux-guidelines/media/0713-03-inactivetoolwindow.png "0713 03_InactiveToolWindow")  

 **Janela de ferramenta inativos, mostrando latente seleção do nó**  

 Quando uma janela está ativa, seu foco é indicado acordo com os modelos de seleção descritos nesta seção das diretrizes.  

#### <a name="context"></a>Contexto  
 Visual Studio foi projetado para manter um forte conceito de contexto, controlando de onde o usuário está trabalhando. Apenas uma janela está ativa, se ele é uma janela de ferramenta ou documento. No entanto, a janela de nível mais alto de documento sempre retém uma seleção latente. Embora o foco pode estar em uma janela de ferramentas, a janela de documento que estava ativo pela última vez exibe uma seleção, até mesmo em um estado inativo. Isso é feito para manter o contexto do usuário no documento estava editando, mostrando-lhes o Visual Studio manteve seu estado para que eles podem retornar- and -shift perfeitamente entre janelas de ferramentas e janelas de documento.  

### <a name="text-selection"></a>Seleção de texto  
 Os editores do Visual Studio que são estritamente textuais, como o editor de texto interno, usam o mesmo modelo de seleção de texto e aparência descrito o [Mouse e ponteiros](https://msdn.microsoft.com/library/dn742466.aspx) página das diretrizes de interação de experiência de usuário Windows no MSDN. O foco de entrada no editor de texto é indicado por uma barra vertical, chamada de ponto de inserção. O ponto de inserção é um único pixel espesso e colorido, como o inverso de tudo o que aparece por trás dele. Ele pisca de acordo com a taxa definida pela **de intermitência do Cursor** definindo na **velocidade** guia dos **teclado** miniaplicativo Painel de controle.  

#### <a name="contiguous-and-disjoint-selection"></a>Seleção contígua e não contíguo  
 Seleção de dentro do editor de texto só é contígua. Não contíguas texto seleções não são permitidas, mas devem ser resolvidas nos editores do objeto gráfico. Quando o ponteiro do mouse do usuário está sobre uma área de texto, o cursor muda para uma forma de i. Um único clique coloca o ponto de inserção no editor de texto no local do clique. Segurando o botão do mouse é iniciado um realce de seleção e liberar o botão do mouse termina o realce de seleção.  

#### <a name="region-selection-box-selection"></a>Seleção de região (seleção de caixa)  
 Visual Studio oferece suporte a seleções de região no editor de texto, e isso é chamado de seleção da caixa. Caixa de seleção permite que o usuário selecione uma região de texto que não segue o fluxo de texto normal. Assim como acontece com a seleção de texto padrão, a seleção deve ser contígua. Caixa de seleção é iniciada pelo mantendo pressionada a tecla Alt enquanto arrasta o mouse. Caixa de seleção também pode ser iniciada, mantenha pressionada as teclas Shift e Alt ao usando as teclas de direção para indicar a região de seleção. Caixa de seleção usa o realce de seleção normal e mostra o cursor de ponto de inserção piscando no final da área de seleção.  

 ![Regional &#40;caixa de&#41; seleção no Visual Studio](../../extensibility/ux-guidelines/media/0713-04-boxselection.png "0713 04_BoxSelection")  

 **Seleção de região (caixa) no Visual Studio**  

#### <a name="text-selection-appearance"></a>Aparência da seleção de texto  
 As cores usadas para seleção ativa e inativa no editor podem ser personalizadas. Para personalizar a aparência visual do editor, um usuário pode ir para **Ferramentas > Opções**e, em seguida, procure **ambiente > fontes e cores > Editor de texto**.  

### <a name="graphical-selection"></a>Seleção de gráfica  

#### <a name="interaction"></a>Interação  
 Seleção de objetos gráficos pode ser complexa e depende de vários fatores:  

-   **Modelo de seleção primária do editor.** Os editores que contêm objetos gráficos também podem ser usados para editar o texto ou grades. Por exemplo, o editor pode ser um editor de texto que também oferece suporte a colocação de objetos gráficos, como o designer XAML do Visual Studio. Suporte a vários tipos de objeto pode afetar como o usuário seleciona grupos compostos por diferentes tipos de objetos.  

-   **Suporte para os estados de seleção primária e secundária.** Um editor pode fornecer uma seleção primária e secundária estados para que os objetos podem ser editados de forma sincronizada, alinhados entre si, redimensionado juntos, e assim por diante.  

-   **Suporte de edição in-loco.** Editores também podem permitir que o conteúdo de seus objetos de gráficos a ser editado. Por exemplo, uma forma de retângulo também pode conter texto interno que pode ser alterado pelo usuário. Além disso, esse texto pode ser centralizado ou justificado. Edição in-loco envolve um nível mais detalhado de interação do usuário e, portanto, requer um conjunto apropriado de indicações visuais para apresentar informações de estado para o usuário.  

#### <a name="mouse-interaction"></a>Interação do mouse  

|Entrada|Resultado|  
|-----------|------------|  
|Clique em um objeto não selecionado|Seleciona o objeto e exibe uma linha tracejada e as alças de seleção, se o objeto é redimensionável.|  
|Clique em um objeto selecionado|Ativa a edição in-loco, se o objeto der suporte a ele. Clicar fora do objeto desativa o modo de edição in-loco.|  
|Clique duas vezes em um objeto|Abre o código por trás do objeto para edição e pode inserir um manipulador de evento padrão, se apropriado.|  
|Aponte para um objeto|Altera o ponteiro para o cursor de movimento. Aparência do objeto, como seu luminosidade ou a cor, pode ser alterada.|  
|Aponte para uma alça de seleção|Altera o ponteiro para o cursor de redimensionamento. Para objetos que oferecem suporte a rotação, alguns identificadores de seleção podem alterar o ponteiro para um cursor girar conforme o ponteiro está posicionado diferente (por exemplo, movido para longe) em relação a alça de seleção.|  
|Arraste|Mesmo se o objeto não está selecionado anteriormente, altera o ponteiro para o cursor de movimento e move o objeto.|  
|Editor perde o foco|Desativa o modo de edição in-loco, embora o objeto retém o conteúdo e a aparência que tinha durante seu último estado de seleção da operação /.|  
|Seleção de objetos|Indicado por uma borda, linha pontilhada ou outro tratamento visualmente distinto para destacar os limites do objeto.|  
|Redimensionar um objeto selecionado|Indicado pela alças de seleção.<br /><br /> Um objeto redimensionável tem oito alças, que representa cada direção na qual ela pode ser redimensionada. Menos identificadores podem ser usados se o objeto pode ser redimensionado somente em determinadas direções. Quando o usuário dimensiona um objeto para baixo até onde oito alças não é interativas, quatro identificadores podem ser usados. Tamanhos de identificador devem ser vinculados para as métricas de borda e a borda de janela com o **GetSystemMetrics** função de API para tamanho proporcionalmente a resolução de vídeo.<br /><br /> ![Alças de redimensionamento](../../extensibility/ux-guidelines/media/0713-05-resizehandles.png "0713 05_ResizeHandles")|  
|Girar um objeto selecionado|![Alças de rotação](../../extensibility/ux-guidelines/media/0713-06-rotate.png "0713 06_Rotate")|  

#### <a name="keyboard-interaction"></a>Interação do teclado  

|Entrada|Resultado|  
|-----------|------------|  
|Tabulação|Move o indicador de foco entre a ordem lógica dos objetos no editor. Isso pode ser esquerda para a direita ou de cima para baixo dependendo **TabIndex** (ou equivalente) o valor da propriedade, a ordem da criação do objeto e a finalidade geral do editor. Shift + Tab inverte a direção do indicador de foco.|  
|Barra de espaços|Ativa o modo de panorâmica enquanto o pressionamento de tecla é mantido. Entrada de mouse adicional é necessária para deslocar para a posição do visor.|  
|Ctrl+Barra de espaços|Ativa o modo de zoom enquanto o pressionamento de tecla é mantido. Entrada de mouse adicional é necessária para aumentar e diminuir o fator de zoom.|  
|Ctrl + Alt + sinal de subtração|Diminui o fator de zoom em um nível.|  
|Ctrl + Alt + sinal de adição|Aumenta o fator de zoom em um nível.|  
|Ctrl ou SHIFT|Adiciona o objeto para o grupo de seleção. CTRL também permite que você remova objetos individualmente a partir do grupo de seleção.|  
|Enter|Executa o comando padrão para o objeto (geralmente abrir ou editar).|  
|F2|Ativa a edição in-loco para o objeto.|  
|Teclas de direção|Move os objetos selecionados na direção da tecla pressionada, em pequenos incrementos (por exemplo, 1 pixel por vez)|  
|CTRL + teclas de direção|Move os objetos selecionados na direção da tecla pressionada, em incrementos maiores (por exemplo, 10 pixels por vez)|  
|SHIFT + seta para chaves|Redimensiona os objetos selecionados na respectiva direção, em pequenos incrementos (por exemplo, 1 pixel por vez)|  
|Ctrl + Shift + teclas de direção|Redimensiona os objetos selecionados na respectiva direção, em incrementos maiores (por exemplo, 10 pixels por vez)|  

 Quando os usuários editar controles em vigor, ele pode fazer sentido para os objetos para redimensionar automaticamente com a entrada do usuário. Por exemplo, se o usuário edita um controle de rótulo, o rótulo deve aumentar para exibir o texto que o usuário acabou de digitar. Se isso não for feito, o usuário deve redimensionar o controle manualmente depois de editar o texto. Se o usuário tem muitos dos controles, isso se torna um atividades rotineiras e tarefa improdutiva.  

#### <a name="graphical-containers"></a>Contêineres de gráficos  
 Em alguns casos, os editores gráficos fornecem contêineres para outros objetos gráficos, como o controle de painel dos Windows Forms ou o controle de Layout de grade no designer de HTML. Se seu editor fornece contêineres para outros objetos gráficos, o modelo de seleção a seguir deve ser usado para apenas o contêiner (objetos dentro o acompanhamento de contêiner, o modelo padrão como descrito acima):  

|Entrada|Resultado|  
|-----------|------------|  
|Clique no contêiner único|Seleciona o objeto de contêiner sem selecionando qualquer um dos objetos contidos diretamente. O contêiner pode movido e/ou redimensionado com padrão de mouse e teclado de entrada (como descrito acima). Objetos contidos são movidos em relação ao contêiner, mas os objetos contidos não são redimensionados, a menos que eles sejam selecionados também diretamente.|  
|Passe o mouse sobre a região de limites do contêiner|Transforma o mouse no cursor de movimento, indicando que o contêiner pode ser movido.|  
|Arraste a região de limites do contêiner|Altera o mouse para o cursor de movimento e move o contêiner (e os objetos contidos em). O contêiner não pode ser movido sem primeiro selecionado com um único clique.|  
|Clique em um objeto dentro do contêiner único|Anula a seleção de contêiner (caso selecionado) e seleciona apenas o objeto clicado.|  
|SHIFT + clique ou Ctrl + clique em um objeto contido e/ou o contêiner|Adiciona o objeto clicado para um grupo de seleção ou uma seleção existente. Se o objeto clicado já for um membro do grupo de seleção, ele é removido do grupo de seleção.|  

 Os objetos contidos devem seguir o modelo básico de seleção conforme descrito na seção anterior. Do teste de usabilidade do Windows Forms designer, os usuários esperado acesso contínuo para os objetos contidos sem etapas intermediárias (impostas pelo objeto confinamento).  

#### <a name="disjoint-and-region-selections"></a>Não contíguas e as seleções de região  
 Editores de objeto gráfico devem dar suporte a seleções não contíguas. Observe que este gráfico não mostra a aparência do controle para o Visual Studio. Ver [aparência da seleção de objeto gráfico](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_GraphicalObjectSelectionAppearance) para especificações detalhadas de visual.  

 ![Não contíguas e seletores de região](../../extensibility/ux-guidelines/media/0713-07-disjointregionselectors.png "0713 07_DisjointRegionSelectors")  

 **Seleção de disjunção**  

 Editores gráficos também devem fornecer as seleções de região com um indicador de seleção do tipo de marca de seleção. Se o editor gráfico oferece suporte a outros tipos de objeto (como texto), em seguida, seleções de região talvez não seja possíveis dependendo das restrições desses outros tipos de objeto.  

 ![Marca de seleção](../../extensibility/ux-guidelines/media/0713-08-marqueeselection.png "0713 08_MarqueeSelection")  

 **Marca de seleção**  

#### <a name="primary-and-secondary-selections"></a>Seleções de primárias e secundárias  
 Alguns editores de objeto gráfico é permitir que o usuário edite ou alinhar objetos em grupos. Nesse caso, o conceito de seleções de primários e secundários precisa ser introduzido. A seleção principal é o objeto ao qual todos os outros objetos respondem para operações de grupo. O objeto que o usuário seleciona primeiro se torna o controle principal e seleções subsequentes se tornam as seleções secundárias. A seleção primária tem um tratamento visual distinto das seleções de secundários para indicar qual objeto está primário:  

 ![Seleção de primária e secundária](../../extensibility/ux-guidelines/media/0713-09-primarysecondary.png "0713 09_PrimarySecondary")  

 **Seleção primária com duas seleções secundárias**  

####  <a name="BKMK_GraphicalObjectSelectionAppearance"></a> Aparência da seleção de objeto gráfico  
 As alças de seleção são desenhados em um padrão retangular ao redor da caixa delimitadora do objeto de quadrados. O gráfico abaixo mostra exemplos de vários estados em que um objeto gráfico pode ter com a alça de dimensionamento e aparência de edição in-loco. O tamanho dos identificadores deve ser vinculado a borda da janela e métricas de borda usando o **GetSystemMetrics** API.  


|          Estado          |  Aparência   |                                                                  Detalhes do Visual                                                                  |
|-------------------------|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
|     **Não selecionado**      |    Padrão    |                 ![Estado do botão padrão](../../extensibility/ux-guidelines/media/0713-10-defaultstate.png "0713 10_DefaultState")                 |
|  **Seleção primária**  |   Redimensionável   |       ![A seleção principal com alças de redimensionamento](../../extensibility/ux-guidelines/media/0713-11-primaryresize.png "0713 11_PrimaryResize")        |
|  **Seleção primária**  | Não é redimensionável |    ![A seleção principal sem alças de redimensionamento](../../extensibility/ux-guidelines/media/0713-13-primarynoresize.png "0713 13_PrimaryNoResize")    |
|  **Seleção primária**  |    Bloqueado     |              ![Seleção primária bloqueada](../../extensibility/ux-guidelines/media/0713-15-primarylocked.png "0713 15_PrimaryLocked")              |
| **Seleção de secundária** |   Redimensionável   |    ![Secundária seleção com alças de redimensionamento](../../extensibility/ux-guidelines/media/0713-17-secondaryresize.png "0713 17_SecondaryResize")     |
| **Seleção de secundária** | Não é redimensionável | ![Alças de redimensionamento de seleção secundária sem](../../extensibility/ux-guidelines/media/0713-19-secondarynoresize.png "0713 19_SecondaryNoResize") |
| **Seleção de secundária** |    Bloqueado     |           ![Seleção secundária bloqueada](../../extensibility/ux-guidelines/media/0713-21-secondarylocked.png "0713 21_SecondaryLocked")           |
|      **Interface do usuário do Active Directory**      |    Padrão    |                       ![Estado de interface do usuário ativo](../../extensibility/ux-guidelines/media/0713-23-uiactive.png "0713 23_UIActive")                        |

### <a name="view-selection-models"></a>Modelos de seleção de exibição  

#### <a name="tree-view"></a>Exibição de árvore  
 Seleção em uma exibição de árvore é mostrada com um realce simple. Se o usuário clica em um nome de nó ou um ícone de nó, o nó se torna selecionado. Os glifos triangulares à esquerda do nó de expandir ou contrato de controle de árvore, mas não afetam a seleção do usuário, com uma exceção: ao recolher um nó pai quando a seleção estiver em um filho do nó, a seleção se move para o pai.  

 ![Modo de exibição de árvore típico no Visual Studio](../../extensibility/ux-guidelines/media/0713-25-treeview.png "0713 25_TreeView")  

 **Modo de exibição de árvore típico no Visual Studio**  

 Modos de exibição de árvore podem dar suporte a seleções contíguas e não contíguas, até mesmo em vários níveis na árvore. Contíguas ou não contíguo várias seleções devem ser feitas em nós de árvore visível. Se um nó estiver recolhido, a seleção não contíguo é perdida e o nó que foi recolhido obtém a seleção. Dessa forma, o usuário pode ver os nós que serão afetados por uma operação. Quando os nós são recolhidos, torna-se claro quais nós podem ser afetados.  

 Quando um nó pai é selecionado, a operação seja aplicada ao pai, embora possa haver casos em que faz sentido para uma operação aplicar o pai e todos os seus filhos. Nesse caso, forneça adicional da interface do usuário durante a operação, como uma caixa de seleção ou a caixa de diálogo de confirmação para tornar a opção "aplicar a todos os filhos" explícito para o usuário.  

##### <a name="renaming"></a>Renomear  
 Se nós na árvore dá suporte à renomeação, renomeando deve ser feito em vigor. A operação no local deve ser o padrão em todos os controles de árvore no Visual Studio. Forneça um comando de renomeação que ativa imediatamente o modo de edição in-loco, com a seleção de texto que abrange o nome completo do nó, pronto para aceitar a entrada do usuário. Se o nó representa um arquivo, o nome do arquivo deve conter a extensão. O realce de seleção deve incluir somente o corpo de nome de arquivo e não a extensão.  

|Entrada|Resultado|  
|-----------|------------|  
|Tecla Enter|Confirma a operação de renomeação|  
|Tecla ESC|Cancela a operação de renomeação|  
|Clicar fora da região de edição in-loco|Confirma a operação de renomeação|  
|Desfazer|Fornecer fácil desfazer para cancelar a operação de renomeação|  

#### <a name="selection-within-lists-and-grid-controls"></a>Seleção em listas e controles de grade  
 O conceito fundamental na seleção de lista é que ele é baseado em linha, que significa que, quando uma seleção é feita em toda a linha está selecionada como uma unidade. Por outro lado, grades podem permitir a células específicas a ser selecionado sem afetar qualquer outro aspecto da linha. Grades também podem conter uma hierarquia de linhas aninhadas (como em uma grade de árvore) que permitem que todo ramificações da hierarquia a ser selecionada e desmarcada com a interação com as linhas pai. Seleção em listas é mostrada por uma cor de realce simples em toda a linha de dados. O foco é mostrado por uma borda pontilhada de pixel único ao redor da linha editável atual ou uma célula (linha se todas as células são somente leitura).  

> [!NOTE]
>  **Foco** e **seleção** são conceitos diferentes. *Foco* é uma indicação de qual interface do usuário do elemento é direcionado para receber entrada dirigida não explicitamente a outro objeto, enquanto *seleção* refere-se ao estado da inclusão de um objeto em um conjunto de objetos dos quais subsequentes as operações podem ocorrer.  

 As seleções nas listas podem ser contíguos, não contíguo, ou região. Quando várias seleções são permitidas, contíguos e seleção de disjunção sempre deve ser compatível, enquanto o suporte para as seleções de região (caixa) são opcional. Seleções de região são iniciadas, arrastando o espaço em branco do corpo da lista.  


| Objeto | Seleção  |
|--------|------------|
|  Lista  | Contíguos |
|  Lista  |  Não contíguas  |
|  Lista  |   Região   |

 Clicar uma vez em uma lista seleciona a linha onde ocorreu o clique. Se o usuário clicar em uma célula de lista que dá suporte à edição in-loco, a célula imediatamente também é ativada para edição no local. Caso contrário, a linha inteira imediatamente é selecionada e mostra um realce.  

 Arrastar no corpo da lista faz uma das três coisas:  

-   Inicia uma seleção de região, se a lista dá suporte a ele e o mouse para baixo no espaço em branco  

-   Inicia uma operação de arrastar/soltar se a lista de célula ou linha dá suporte a que está sendo uma origem do arrasto  

-   Seleciona a linha atual  

##### <a name="in-place-editing"></a>Edição in-loco  
 Quando é permitido edição in-loco, há dois modelos básicos: Seletor de propriedade e controle de edição simples. Com um controle de edição simples, o conteúdo é realçado e está pronto para edição no local é ativado assim que de entrada do usuário. Sempre que um seletor de propriedade é implementado, o botão que invoca o seletor de propriedades é exibido depois que o modo de edição no local é ativado, e a seleção atual não é realçada. O botão de seletor deve ser justificado à direita da célula. Para obter exemplos de edição in-loco, consulte a **janela de propriedades** e **lista de tarefas** no Visual Studio.  

##### <a name="keyboard-support"></a>Suporte ao teclado  
 Suporte de teclado para a seleção em listas e grades segue as convenções padrão do Windows:  

-   Teclas de seta para navegar pela lista, selecionando cada célula da linha/como o foco é movido.  

-   SHIFT + seta executa uma seleção contígua na direção das teclas de direção.  

-   CTRL + seta para a seguido de barra de espaço alterna entre adicionando e removendo itens da lista de seleção, a criação de uma seleção não contíguo.  

-   Para as grades que contenham hierarquias aninhadas, a tecla de seta para a direita expande uma linha pai e a tecla de seta para a esquerda recolhe um.  

-   A tecla Tab move o foco entre as células na linha atual, se as células são editáveis.  

-   A tecla Enter executa o comando padrão no item na lista (geralmente **abrir**).  

-   A tecla F2 ativa a edição in-loco para a célula selecionada no momento.  

##  <a name="BKMK_PersistenceAndSavingSettings"></a> Salvando as configurações e persistência  

### <a name="overview"></a>Visão geral  
 Embora cada componente de software no Visual Studio é geralmente responsável por seu próprio estado e persistência, o Visual Studio salva automaticamente as configurações em alguns casos, como com posições e tamanhos de janela. A tabela a seguir é uma combinação de configurações salvas automaticamente e que exigem um usuário explícito ou programado a ação a ser executada.  

|Objeto|O que salvar|Quando salvar|Onde salvar|  
|------------|------------------|------------------|-------------------|  
|Objeto selecionável (por exemplo, uma linha de código)|Um ponto de interrupção em uma linha de código<br /><br /> Um atalho de usuário associado com a linha de código|Quando o projeto é salvo|O **opções do usuário (. suo)** arquivo de projeto|  
|Caixa de diálogo|O local da caixa de diálogo, se ele tivesse sido movido<br /><br /> O modo de exibição que o usuário é usado pela última vez na caixa de diálogo|Quando a caixa de diálogo é fechada<br /><br /> Quando termina a sessão do Visual Studio|Na memória<br /><br /> Registro no **HKEY_Current_User**|  
|Janela|O tamanho e local da janela|Quando a janela é fechada<br /><br /> Quando o modo do Visual Studio é alterado<br /><br /> Quando termina a sessão do Visual Studio|O **opções do usuário (. suo)** arquivo de projeto<br /><br /> Arquivo de opções personalizadas para as configurações da janela|  
|Documento|A seleção atual no documento<br /><br /> O modo de exibição do documento<br /><br /> Os último vários lugares que o usuário visitou|Quando o documento é salvo|O **opções do usuário (. suo)** arquivo de projeto|  
|Projeto|Referências aos arquivos<br /><br /> Referências aos diretórios no disco<br /><br /> Referências a outros softwares<br /><br /> Componentes<br /><br /> Informações de estado sobre o projeto em si|Quando o projeto é salvo|O arquivo de projeto|  
|Solução|Referências a projetos<br /><br /> Referências aos arquivos|Quando a solução ou projeto é salvo|O **solução (. sln)** arquivo|  
|As configurações no **Ferramentas > Opções**|Personalizações de teclado<br /><br /> Personalizações da barra de ferramentas<br /><br /> Esquemas de cores|Quando o **Ferramentas > Opções** caixa de diálogo é fechada<br /><br /> Quando termina a sessão do Visual Studio|Registro no **HKEY_Current_User**|  

 O que o usuário está fazendo e quando eles estão fazendo, determina se uma configuração está sendo salvo na memória (durante a sessão), salva em disco (entre as sessões como uma configuração de registro), como parte do projeto ou solução de arquivo em si, como parte do **solução Opções (. suo)** de arquivo, ou como um configurações personalizadas de arquivo que somente esse componente de software conhecem. A tabela acima mostra vários eventos no qual as configurações podem ser salvas. No entanto, existem outras ocasiões em que deseja salvar o estado:  

-   Quando o usuário altera o local dentro de uma caixa de diálogo ou janela  

-   Quando o usuário transfere o foco para outra janela  

-   Quando o usuário alterna de design para o modo de depuração  

-   Quando o usuário fizer logoff de sua conta  

-   Quando o computador entra em hibernação ou desligado  

-   Quando o computador/disco rígido está prestes a ser reformatado e configure novamente  

### <a name="window-configurations"></a>Configurações de janela  
 Uma configuração de janela é a apresentação básica do ambiente de desenvolvimento – é um esquema consiste em lista de janelas de ferramenta presentes e a maneira na qual eles são organizados. Para o windows gerenciados pelo IDE (janelas do IDE), informações de layout são mantidas por usuário, portanto, quando um usuário inicia o IDE, o layout da janela é exibida mesmo que, quando elas duram, Visual Studio foi encerrado. O estado e a posição das janelas do IDE é mantido em um arquivo de opções personalizadas em formato XML. Janelas de ferramentas que são criadas por pacotes carregados no IDE manter suas informações de estado no registro e podem ou não ser por usuário.  

#### <a name="profile-specific-layouts"></a>Layouts de específico para o perfil  
 Cada perfil inclui layouts de janela da ferramenta, organizados de forma familiar para pessoas específicas do desenvolvedor (os desenvolvedores de Visual C++ esperam ver a **Gerenciador de soluções** no lado esquerdo do IDE, enquanto os desenvolvedores de c# esperam ver o  **Gerenciador de soluções** à direita). Layouts de janela específico para o perfil são carregados depois que o usuário escolhe um perfil na inicialização. Um autor do pacote deve determinar o layout da janela mais adequado para a experiência de seus clientes, sabendo que as alterações que o usuário faz a configuração de janela, em seguida, ser persistente.  

##  <a name="BKMK_TouchInput"></a> Entrada de toque  
 Os usuários estão usando cada vez mais produtos de desenvolvimento da Microsoft nos dispositivos de toque. No entanto, há barreiras que tornam difícil usar ferramentas de desenvolvimento em dispositivos sensíveis ao toque. Usuários esperam que nossos produtos para fornecer uma experiência de toque precisas e confiáveis. A intenção dessas diretrizes é informar decisões sobre quais recursos de toque para incorporar e incentivar uma experiência de toque consistente entre o Visual Studio e produtos relacionados.  

### <a name="levels-of-experience"></a>Níveis de experiência  
 Os seguintes níveis de experiência destinam-se a servir como um guia para ajudar as equipes a decidir quais recursos de toque para oferecer com base em seu nível desejado de interesse de investimento em contato.  

-   O **experiência básica** é para equipes que desejam fornecer recursos de toque para que não há nenhum ineficiência ao longo de seu trabalho.  

-   O **otimizado experiência** é para equipes que desejam fornecer a maioria dos recursos comuns de toque (por exemplo, aqueles normalmente disponíveis em aplicativos de navegador da internet).  

-   O **elevados experiência** é para equipes que desejam adicionar recursos tais como gestos ou outros recursos opcionais que podem tornar seus aplicativos de primeiro toque amigável.  

||Experiência básica|Experiência otimizada|Experiência com privilégios elevados|  
|-|----------------------|--------------------------|-------------------------|  
|Permite que os usuários...|Corrigir o código e a solução/nível de projeto de leitura sem extremidades de mensagens mortas|Executar tarefas de manutenção, refatorações e navegação|Operar em uma experiência consistente, intuitiva e fluida com confiança|  
|Editor|Movimento panorâmico por toque e seleção<br /><br /> Barra de rolagem toque para saltar e pressione + arrastar|Aperto zoom<br /><br /> Rolagem rápida<br /><br /> Seleção<br /><br /> Fácil de usar do menu de contexto||  
|Janelas de ferramentas superior|Lista de movimento panorâmico<br /><br /> Seleção de item<br /><br /> Barra de rolagem toque para saltar e pressione + arrastar|Rolagem de item fácil e seleção||  
|Janelas||Redimensionar a janela<br /><br /> Acesso rápido||  
|Documente também||Facilitar a navegação entre arquivos abertos||  
|Gestos||Certifique-se de gestos comuns trabalhar no IDE|Ações de gesto<br /><br /> Suporte a arrastar-e-soltar e designers|  
|Outras considerações|||Teclado na tela personalizado|  

#### <a name="gestures"></a>Gestos  
 Gestos de fornecem aos usuários um atalho para comandos que, caso contrário, podem exigir uma interação mais complicada. Consulte as diretrizes do Windows no [gestos de toque comuns para aplicativos de área de trabalho](http://msdn.microsoft.com/library/windows/desktop/dd940543\(v=vs.85\).aspx)e siga estas diretrizes para a maioria dos gestos, incluindo gestos simples, como de Panorâmica e zoom.

