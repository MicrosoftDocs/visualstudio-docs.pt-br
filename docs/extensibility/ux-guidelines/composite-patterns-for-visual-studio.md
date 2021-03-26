---
title: Padrões de composição para o Visual Studio | Microsoft Docs
description: Saiba mais sobre padrões de composição importantes para consistência no Visual Studio. Padrões de composição combinam elementos de interação e design.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: e48ecfb2-f4b5-4d3a-b4a2-7a4d62fa4ec0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0c6f609842f2531fe39158e871a330e136603433
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090051"
---
# <a name="composite-patterns-for-visual-studio"></a>Padrões de composição para Visual Studio
Padrões de composição combinam elementos de interação e design em configurações distintas. Alguns dos padrões de composição mais importantes no Visual Studio em relação à consistência incluem:

- [Visualização de dados](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_DataVisualization)

- [Interface do usuário e inspeção do objeto](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_OnObjectUI)

- [Modelos de seleção](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_SelectionModels)

- [Configurações de persistência e salvamento](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_PersistenceAndSavingSettings)

- [Entrada por toque](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_TouchInput)

## <a name="data-visualization"></a><a name="BKMK_DataVisualization"></a> Visualização de dados

### <a name="overview"></a>Visão geral
 Os gráficos são uma maneira visual de agregar e Visualizar dados para aprimorar a tomada de decisões. Eles podem ajudar os usuários a enfrentar muitos dados, mas o significado é ver o que merece atenção e o que pode precisar de uma ação.

 O usuário se beneficiará de um gráfico se qualquer uma das seguintes condições for verdadeira:

- O gráfico ajudará os usuários a identificar as tarefas nas quais eles podem agir?

- O gráfico permitirá que os usuários prevejam consequências de possíveis alterações?

- O gráfico ajudará os usuários a descobrir tendências e identificar padrões?

- O gráfico permitirá que os usuários tomem decisões melhores?

- O gráfico ajudará a responder a uma pergunta específica que os usuários podem ter no contexto em questão?

#### <a name="general-rules-for-charts"></a>Regras gerais para gráficos

- Rotular dados claramente. Ilustrações sem explicação são apenas imagens.

- Inicie os eixos em zero para evitar as proporções de distorção. Comprimento de linha e tamanho de barra são indicações visuais importantes para entender as relações entre os pontos de dados.

- Crie gráficos, não infográficos. Infográficos são representações artísticas de dados, e sua meta principal é o Visual narração. Os gráficos podem (e devem) ser visualmente atraentes, mas permitem que os dados se comuniquem por si mesmos.

- Evite skeumorphisms, gráficos de barras de ilustrações, marcas de contraste e outros toques de infográfico.

- Não use efeitos 3D como um elemento decorativo. Use-os apenas se eles realmente integram a capacidade do usuário de compreender as informações.

- Evite usar várias linhas e preenchimentos, já que mais de duas cores podem tornar esse tipo de gráfico difícil de ler e interpretar corretamente.

- Não use um gráfico (ou qualquer ilustração) como o único meio de entender um conceito ou interagir com dados. Isso apresenta dificuldades para os usuários com deficiências visuais.

- Não use gráficos como elementos gratuito ou decorativos em uma página. Em outras palavras, se um gráfico não adicionar qualquer valor ou ajudar os usuários a resolver um problema, não o use.

### <a name="chart-types"></a>Tipos de gráfico
 Os tipos de gráficos usados no Visual Studio incluem gráficos de barras, gráficos de linhas, um gráfico de pizza modificado conhecido como um gráfico de toque ou "gráfico de rosca", linhas do tempo, gráficos de dispersão (também chamados de "gráficos de cluster") e de Gantt. Cada tipo de gráfico é útil para comunicar um tipo diferente de informações.

### <a name="other-charting-considerations"></a>Outras considerações sobre gráficos

#### <a name="color"></a>Color
 Há uma paleta específica de cores de gráfico definida para uso no Visual Studio. A paleta pode ser acessada para os principais tipos de cegueira de cor e as cores podem ser diferenciadas mesmo quando usadas como fatias muito estreitas de cor. Você pode usar essas cores em qualquer combinação para qualquer tipo de gráfico ou grafo na sua interface do usuário. Você não precisará usar todas as sete cores se não precisar de muitas cores distintas. Essas cores não foram projetadas para serem usadas com elementos de primeiro plano, portanto, não coloque texto nem glifos sobre essas cores. Esses matizes devem ser embutidos em código e expostos à personalização do usuário em **ferramentas > opções** (consulte [expondo cores para usuários finais](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ExposingColorsForEndUsers)).

|Essas|Hex|RGB|
|------------|---------|---------|
|![71B252 de amostra](../../extensibility/ux-guidelines/media/0711_71b252.png "0711_71B252")|#71B252|113178, 82|
|![BF3F00 de amostra](../../extensibility/ux-guidelines/media/0711_bf3f00.png "0711_BF3F00")|#BF3F00|191, 63, 0|
|![FCB714 de amostra](../../extensibility/ux-guidelines/media/0711_fcb714.png "0711_FCB714")|#FCB714|252183, 20|
|![903F8B de amostra](../../extensibility/ux-guidelines/media/0711_903f8b.png "0711_903F8B")|#903F8B|144, 63139|
|![117AD1 de amostra](../../extensibility/ux-guidelines/media/0711_117ad1.png "0711_117AD1")|#117AD1|17.122.209|
|![79D7F2 de amostra](../../extensibility/ux-guidelines/media/0711_79d7f2.png "0711_79D7F2")|#79D7F2|121.215.242|
|![B5B5B5 de amostra](../../extensibility/ux-guidelines/media/0711_b5b5b5.png "0711_B5B5B5")|#B5B5B5|181.181.181|

## <a name="on-object-ui-and-peeking"></a><a name="BKMK_OnObjectUI"></a> Interface do usuário e inspeção do objeto
 Esta seção fornece contexto para inspecionar, também conhecido como exibição de inspeção de código, um tipo de interface do usuário no objeto exclusiva do Visual Studio.

### <a name="overview"></a>Visão geral

- A interface de usuário no objeto deve dar ao usuário mais informações ou interatividade sem desviar de sua tarefa principal.

- O padrão principal para a interface do usuário no objeto no Visual Studio é conhecido como "informações no ponto de atenção".

- A interface do usuário no objeto no Visual Studio está embutida ou flutuante e pode ser durável ou transitória.

  - A exibição de inspeção de código, um tipo de interface do usuário no objeto no Visual Studio, é embutida e durável.

  - CodeLens, um tipo de interface do usuário no objeto no Visual Studio, é flutuante e transitório

  Entender como uma parte do código funciona ou encontrar detalhes sobre esse código, geralmente exige que um desenvolvedor Alterne o contexto e vá para outro conteúdo ou outra janela. Essas mudanças de contexto podem causar interrupções, pois os usuários podem perder o foco em sua tarefa original se deixarem a janela principal. Além disso, a obtenção desse contexto original pode ser difícil, especialmente se a troca de janelas fez com que seu código original fosse obscurecido por outra interface do usuário.

  A interface do usuário no objeto segue um padrão chamado "informações no ponto de atenção". Essas mensagens, janelas pop-up e caixas de diálogo fornecem aos usuários informações adicionais e relevantes que adicionam esclarecimentos ou interatividade sem perder o foco em sua tarefa principal. Exemplos de interface do usuário no objeto incluem janelas pop-up que aparecem quando um usuário passa o ponteiro do mouse sobre um ícone na área de notificação, o ondulado vermelho sob uma palavra incorreta e a exibição de inspeção introduzida no Visual Studio 2013.

### <a name="decision-points"></a>Pontos de decisão
 No Visual Studio, há várias maneiras de usar esse padrão de informações no ponto de atenção. Escolher o mecanismo certo e implementá-lo de maneira consistente e previsível é essencial para a experiência geral. Caso contrário, os usuários podem receber uma experiência confusa ou inconsistente que reduz o foco do conteúdo em si.

#### <a name="relationships-between-master-and-detail-content"></a>Relações entre conteúdo mestre e detalhado
 As informações no ponto de atenção são usadas para exibir uma relação entre o conteúdo no qual o usuário se concentra (o conteúdo "mestre") e o conteúdo adicional relacionado (o conteúdo de "detalhes"). Nesse padrão, o conteúdo detalhado está claramente relacionado ao conteúdo com o qual o usuário está trabalhando e pode ser exibido próximo ao conteúdo mestre. Informações complementares ou informações que não podem ser resumidas sem sobrecarregar o conteúdo mestre devem seguir outro padrão, como uma janela de ferramentas.

- **Sempre** exiba o conteúdo detalhado em proximidade com o conteúdo mestre.

- **Sempre** Verifique se o conteúdo detalhado ainda permite que um usuário permaneça focado no conteúdo mestre. Geralmente, a melhor maneira de conseguir isso é renderizar o conteúdo detalhado o mais próximo possível do conteúdo mestre. Isso pode ser feito renderizando o conteúdo detalhado em uma janela pop-up ao lado do conteúdo mestre ou renderizando o conteúdo detalhado embutido sob o conteúdo mestre.

- **Nunca** Use informações no ponto de atenção que leva o usuário para fora do conteúdo mestre. Se os usuários precisarem exibir o conteúdo detalhado separadamente, expor uma ação explícita que permite ao usuário fazer isso.

#### <a name="design-details"></a>Detalhes do design
 Depois de determinar que a interface do usuário no objeto é a escolha certa, há quatro considerações de design principais:

1. **Persistência:** o conteúdo é esperado como durável ou transitório?
   Os usuários desejarão manter as informações visíveis para se referirem ou interagirem? Ou os usuários desejarão rapidamente dar uma olhada nas informações e continuar com a tarefa principal?

2. **Tipo de conteúdo:** o conteúdo será informativo, acionável ou de navegação?
   O usuário precisa de mais detalhes sobre o conteúdo mestre? O usuário precisa concluir uma tarefa que afeta o conteúdo mestre? Ou o usuário precisa ser direcionado para outro recurso?

3. **Tipo de indicador:** um indicador de ambiente faz sentido?
   As informações podem ser resumidas de uma maneira útil e exibidas sem sobrecarregar o conteúdo mestre?

4. **Gestos:** quais gestos serão usados para invocar e ignorar a interface do usuário?
   Como o usuário abrirá o conteúdo detalhado e o enviará de longe? Há algum valor na adição de um gesto, como fixação para alternar entre Estados transitórios e duráveis?

   Cada um desses quatro pontos de decisão terá um impacto sobre os principais componentes da interface do usuário no objeto.

### <a name="on-object-ui-components"></a>Componentes da interface do usuário no objeto

1. Tipo de contêiner (apresentador de conteúdo)

    - Flutuante

    - Embutido

2. Tipo de conteúdo

    - Informativo: dados que podem ser estáticos ou dinâmicos

    - Acionável: comandos que alteram o conteúdo mestre

    - Navegação: links que levam o usuário para outra janela ou aplicativo, como o MSDN

3. Gestos

    - Invocação

    - Exoneração

    - Fixação

    - Outras interações

4. Modelo de persistência e confirmação

    - Transitório

    - Durável

    - Automática

    - Sob demanda

5. Indicadores de ambiente (opcional)

    - Sublinhado ondulado

    - Ícone de marca inteligente

    - Outros indicadores de ambiente

#### <a name="container-content-presenter-type"></a>Tipo de contêiner (apresentador de conteúdo)
 Há duas opções principais disponíveis para apresentar o conteúdo no ponto de atenção:

1. **Inline:** um apresentador embutido, como o modo de exibição de inspeção que foi introduzido no editor de código Visual Studio 2013, torna o espaço para o novo conteúdo, alterando o conteúdo existente.

    - **Prefira** apresentadores embutidos se você espera que os usuários desejam gastar um tempo significativo se referindo ou interagindo com o conteúdo que você apresenta.

    - **Evite** apresentadores embutidos se você espera que os usuários desejam dar uma olhada nas informações que você apresenta e continuar com a tarefa principal com interrupção mínima.

2. **Flutuante:** um apresentador flutuante é posicionado o mais próximo possível do conteúdo selecionado, mas não altera o layout do conteúdo existente. Várias estratégias podem ser empregadas, como exibir um painel de conteúdo flutuante sobre o espaço em branco mais próximo disponível para o símbolo selecionado.

    - **Prefira** apresentadores flutuantes se você esperar que os usuários desejam dar uma olhada nas informações que você apresenta e, em seguida, continuar com a tarefa principal com interrupção mínima.

    - **Evite** apresentadores flutuantes se você espera que os usuários desejam gastar um tempo significativo se referindo ou interagindo com o conteúdo que você apresenta.

#### <a name="content-type"></a>Tipo de conteúdo
 Há três tipos principais de conteúdo que podem ser exibidos dentro de qualquer contêiner de interface do usuário no objeto. Qualquer combinação desses tipos de informações pode ser mostrada. Os três tipos são:

1. **Informativo:** a maioria dos contêineres de interface do usuário no objeto exibirá algum tipo de conteúdo informativo. O conteúdo pode representar informações sobre o estado atual do ambiente ou pode representar informações sobre um potencial estado futuro do ambiente. Por exemplo, ele pode ser usado para mostrar o efeito de um comando específico, como uma refatoração, no código existente.

    - **Sempre** use a representação canônica das informações exibidas. Por exemplo, o código deve ser semelhante a um código, completo com realce de sintaxe e deve respeitar qualquer fonte e outras configurações de ambiente definidas pelo usuário.

    - **Sempre** considere o suporte a qualquer ação no conteúdo informativo que seria possível se essa mesma informação fosse apresentada como conteúdo mestre. Por exemplo, se estiver apresentando o código existente dentro de um contêiner de interface do usuário no objeto, leve em consideração o suporte à capacidade de procurar e modificar esse código.

    - **Sempre** considere usar uma cor de plano de fundo diferente se apresentar conteúdo informativo que representa um estado futuro potencial.

2. Acionável: alguns contêineres de interface do usuário no objeto fornecerão a capacidade de executar alguma ação no conteúdo mestre, como a execução de uma operação de refatoração.

    - **Sempre** Posicione comandos acionáveis separadamente do conteúdo informativo.

    - **Sempre** habilite e desabilite ações quando apropriado.

    - **Sempre** consulte as diretrizes padrão para representar comandos dentro das caixas de diálogo.

    - **Sempre** Mantenha o número de ações que são expostas em um contêiner de interface do usuário no objeto para um mínimo absoluto. Interagir com a interface do usuário no objeto deve ser uma experiência leve e rápida. O usuário não deve ter que gastar energia no gerenciamento do próprio contêiner da interface do usuário no objeto.

    - **Sempre** considere como e quando um contêiner de interface do usuário no objeto será fechado ou descartado. Como prática recomendada, qualquer ação que conclua a caixa de diálogo entre o conteúdo mestre e de detalhes também deve fechar o contêiner da interface do usuário do objeto quando essa ação é chamada.

3. **Navegação:** alguns contêineres de interface do usuário no objeto incluem links que levam o usuário para outra janela ou aplicativo, como abrir um artigo do MSDN no navegador da Web do usuário.

    - **Sempre** preceder qualquer link de navegação com "aberto" para que os usuários não se surpreendam com a navegação para algum outro conteúdo.

    - **Sempre** separe os links de navegação de links acionáveis.

#### <a name="ambient-indicators-optional"></a>Indicadores de ambiente (opcional)
 Os indicadores de ambiente podem ser sutis, incluindo o texto apresentado em uma cor de contraste do restante do código ou óbvio, incluindo símbolos tickler, como sublinhados ondulados e ícones de marca inteligente. Os indicadores de ambiente comunicam a disponibilidade de informações adicionais e relevantes. O ideal é que eles forneçam informações úteis mesmo sem exigir que o usuário interaja com eles.

- **Sempre** Posicione um indicador de ambiente para que ele não distraia ou sobrecarregue o usuário. Se for impossível posicionar um indicador de ambiente de forma tão importante, considere outra solução.

- **Sempre** Posicione o indicador de ambiente o mais próximo possível do conteúdo ao qual ele está relacionado.

- **Sempre** tente criar um indicador que resuma as informações disponibilizadas. Considere fornecer uma contagem do número de itens de dados disponíveis (por exemplo, "3 referências" em vez de simplesmente "referências") ou pense em alguma outra maneira de resumir os dados.

  - Nos casos em que os dados de um indicador nem sempre podem ser computados e exibidos, considere imediatamente fornecer comentários progressivos à medida que os valores são computados. Por exemplo, considere a animação de alterações que refletem atualizações para os dados disponíveis, de forma semelhante à maneira como o bloco de emails dinâmicos no Windows Phone é atualizado à medida que o número de emails não lidos aumenta.

- **Nunca** adicione mais indicadores do que um usuário pode usar razoavelmente para um determinado conteúdo. Os indicadores de ambiente devem ser úteis sem a necessidade de qualquer interação do usuário. Os indicadores perdem seus Ambience se exigirem um estouro e outros controles de gerenciamento para colocá-los em exibição.

#### <a name="gestures"></a>Gestos
 Um aspecto importante de permitir que o usuário Mantenha o foco no conteúdo mestre é dar suporte aos gestos certos para abrir e ignorar o conteúdo adicional de detalhes.

- **Sempre** exija que o usuário execute algum gesto explícito para abrir o conteúdo adicional. Os gestos de abertura comuns incluem:

  - **Hover:** dicas de ferramenta ou conteúdo informativo não interativo

  - **Comando explícito:** apresentador embutido

  - **Clique duas vezes no indicador ambiente:** Janela pop-up CodeLens

- **Sempre** ignore o conteúdo de detalhes sempre que o usuário pressionar a tecla ESC.

- **Sempre** considere o contexto da interface do usuário no objeto. Para os apresentadores de conteúdo que permitem a interação dentro do contêiner, considere atentamente se as informações adicionais devem ser exibidas ao focalizar, o que provavelmente causem interrupções no fluxo de trabalho do usuário.

- **Nunca** exibir conteúdo em foco que pareça ser editável ou convidar a interação do usuário. Esse comportamento pode frustrar os usuários se eles tentarem mover o cursor sobre o conteúdo de detalhes, uma vez que o comportamento padrão de uma dica de ferramenta é descartar imediatamente quando o cursor não estiver mais sobre o conteúdo mestre que o produziu.

## <a name="selection-models"></a><a name="BKMK_SelectionModels"></a> Modelos de seleção

### <a name="overview"></a>Visão geral
 Um modelo de seleção é o mecanismo usado para indicar e confirmar operações em um ou mais objetos de interesse na interface do usuário. Este tópico discute os padrões de interação de seleção nos editores de documento do Visual Studio: editores de texto, superfícies de design e superfícies de modelagem.

 Os usuários devem ter uma maneira de indicar ao Visual Studio o que eles estão trabalhando, e o Visual Studio deve responder de forma previsível com os comentários para os usuários sobre o que está operando. As diferenças ou uma comunicação insuficiente entre o usuário e a interface do usuário podem fazer com que o usuário não perceba uma ação, o que pode ter consequências indesejadas. Geralmente, o erro fica desnotado até que o usuário veja que algo está ausente ou foi alterado. Os modelos de seleção são, portanto, uma das partes mais importantes do design da interface do usuário. Embora os modelos de seleção no Visual Studio sejam consistentes com o Windows, há pequenas variações.

 No Visual Studio, como no Windows, os modelos de seleção diferem de acordo com o contexto no qual ocorre a interação. As seleções podem ocorrer em quatro tipos de objetos:

- Texto

- Objetos gráficos

- Listas e árvores

- Grades

  Nesses objetos, há três tipos de seleções:

- Vizinha

- Não contíguo

- Região

#### <a name="scope"></a>Escopo
 O componente mais importante da seleção é garantir que o usuário saiba em qual janela ele está trabalhando (ativação) e onde o foco está localizado (seleção). O Visual Studio estende a funcionalidade de gerenciamento de janelas no Windows, mas o esquema de ativação é o mesmo: interagir com uma janela leva o foco para a janela. O Visual Studio tem dois indicadores para ativação: um para janelas de documentos e outro para janelas de ferramentas.

 Para janelas de documentos, a janela ativa é indicada por uma guia de janela de documento chegando à frente e alterando sua cor de fundo:

 ![Seleção de guia ativa no Visual Studio](../../extensibility/ux-guidelines/media/0713-01_activetab.png "0713-01_ActiveTab")

 **Seleção de guia ativa**

 Para janelas de ferramentas, a janela ativa é indicada por uma alteração na cor da área da barra de título da janela de ferramentas:

 ![Seleção da janela da ferramenta ativa no Visual Studio](../../extensibility/ux-guidelines/media/0713-02_activetoolwindow.png "0713-02_ActiveToolWindow")

 **Janela de ferramenta ativa mostrando a seleção primária de um nó**

 ![Seleção de janela de ferramenta inativa no Visual Studio](../../extensibility/ux-guidelines/media/0713-03_inactivetoolwindow.png "0713-03_InactiveToolWindow")

 **Janela de ferramentas inativas, mostrando a seleção latente do nó**

 Quando uma janela estiver ativa, seu foco será indicado de acordo com os modelos de seleção descritos nesta seção de diretrizes.

#### <a name="context"></a>Contexto
 O Visual Studio foi projetado para manter um conceito forte de contexto, mantendo o controle de onde o usuário está trabalhando. Somente uma janela está ativa, seja uma ferramenta ou janela de documento. No entanto, a janela do documento na extremidade superior sempre retém uma seleção latente. Embora o foco possa estar em uma janela de ferramentas, a janela do documento que foi ativada pela última vez exibe uma seleção, mesmo em um estado inativo. Isso é feito para manter o contexto do usuário no documento que eles estavam editando, mostrando que o Visual Studio manteve seu estado para que eles possam retornar e mudar diretamente entre janelas de ferramentas e janelas de documentos.

### <a name="text-selection"></a>Seleção de texto
 Os editores do Visual Studio que são estritamente textuais, como o editor de texto interno, usam o mesmo modelo de seleção de texto e a aparência descritas na página [mouse e ponteiros](/windows/desktop/uxguide/inter-mouse) das diretrizes de interação da experiência do usuário do Windows no msdn. O foco de entrada no editor de texto é indicado por uma barra vertical chamada ponto de inserção. O ponto de inserção é um único pixel espesso e colorido como o inverso do que aparece por trás dele. Ele pisca de acordo com a taxa definida pela configuração de **taxa de intermitência do cursor** na guia **velocidade** do applet do **teclado** no painel de controle.

#### <a name="contiguous-and-disjoint-selection"></a>Seleção contígua e não contíguo
 A seleção dentro do editor de texto é apenas contígua. As seleções de texto não são permitidas, mas devem ser abordadas em editores de objeto gráfico. Quando o ponteiro do mouse do usuário está sobre uma área de texto, o cursor muda para um feixe. Um único clique coloca o ponto de inserção no editor de texto no local do clique. Pressionar o botão do mouse para baixo inicia um realce de seleção e soltar o botão do mouse termina o realce da seleção.

#### <a name="region-selection-box-selection"></a>Seleção de região (seleção de caixa)
 O Visual Studio dá suporte a seleções de região no editor de texto, e isso é chamado de seleção de caixa. A seleção de caixa permite que o usuário selecione uma região de texto que não segue o fluxo de texto regular. Assim como acontece com a seleção de texto padrão, a seleção deve ser contígua. A seleção de caixa é iniciada mantendo a tecla Alt pressionada enquanto arrasta com o mouse. A seleção de caixa também pode ser iniciada mantendo as teclas ALT e SHIFT pressionadas ao usar as teclas de direção para indicar a região de seleção. A seleção de caixa usa o realce de seleção normal e mostra o cursor de ponto de inserção piscando no final da área de seleção.

 ![Caixa de &#40;regional&#41; seleção no Visual Studio](../../extensibility/ux-guidelines/media/0713-04_boxselection.png "0713-04_BoxSelection")

 **Seleção de região (caixa) no Visual Studio**

#### <a name="text-selection-appearance"></a>Aparência da seleção de texto
 As cores usadas para seleção ativa e inativa no editor podem ser personalizadas. Para personalizar a aparência visual do editor, um usuário pode ir para **ferramentas > opções** e, em seguida, examinar o **ambiente > fontes e cores > editor de texto**.

### <a name="graphical-selection"></a>Seleção gráfica

#### <a name="interaction"></a>Interação
 A seleção de objeto gráfico pode ser complexa e depende de vários fatores:

- **O modelo de seleção principal do editor.** Os editores que contêm objetos gráficos também podem ser usados para editar texto ou grades. Por exemplo, o editor pode ser um editor baseado em texto que também dá suporte ao posicionamento de objetos gráficos, como o Visual Studio XAML designer. O suporte a vários tipos de objeto pode afetar a forma como o usuário seleciona grupos compostos de diferentes tipos de objetos.

- **Suporte para Estados de seleção primário e secundário.** Um editor pode fornecer Estados de seleção primários e secundários para que os objetos possam ser editados de forma não ativa, alinhados entre si, redimensionados juntos e assim por diante.

- **Suporte à edição in-loco.** Os editores também podem permitir que o conteúdo de seus objetos gráficos seja editado. Por exemplo, uma forma de retângulo também pode conter texto no interior que pode ser alterado pelo usuário. Além disso, esse texto pode ser centralizado ou justificado. A edição in-loco envolve um nível mais detalhado de interação do usuário e, portanto, requer um conjunto apropriado de indicações visuais para apresentar informações de estado ao usuário.

#### <a name="mouse-interaction"></a>Interação com o mouse

|Entrada|Resultado|
|-----------|------------|
|Clique em um objeto não selecionado|Seleciona o objeto e exibe uma linha tracejada e alças de seleção, se o objeto for redimensionável.|
|Clique em um objeto selecionado|Ativa a edição in-loco se o objeto der suporte a ele. Clicar fora do objeto desativa o modo de edição in-loco.|
|Clique duas vezes em um objeto|Abre o código por trás do objeto para edição e pode inserir um manipulador de eventos padrão, se apropriado.|
|Apontar para um objeto|Altera o ponteiro para o cursor de movimentação. A aparência do objeto, como sua luminosidade ou cor, pode ser alterada.|
|Apontar para uma alça de seleção|Altera o ponteiro para o cursor de redimensionamento. Para objetos que dão suporte à rotação, alguns identificadores de seleção podem alterar o ponteiro para um cursor de rotação à medida que o ponteiro é posicionado de forma diferente (por exemplo, movido para fora) em relação à alça de seleção.|
|Arrastar|Mesmo que o objeto não esteja selecionado anteriormente, o altera o ponteiro para o cursor de movimentação e move o objeto.|
|O editor perde o foco|Desativa o modo de edição in-loco, embora o objeto retenha o conteúdo e a aparência que ele tinha durante seu último estado de operação/seleção.|
|Seleção de objeto|Indicado por uma borda, linha pontilhada ou outro tratamento visualmente distinto para realçar o limite do objeto.|
|Redimensionar um objeto selecionado|Indicado por alças de seleção.<br /><br /> Um objeto redimensionável tem oito identificadores, representando cada direção na qual ele pode ser redimensionado. Menos identificadores poderão ser usados se o objeto só puder ser redimensionado em determinadas direções. Quando o usuário dimensiona um objeto para onde oito identificadores não seriam interativos, então quatro identificadores podem ser usados. Os tamanhos de identificador devem ser vinculados à borda da janela e às métricas de borda com a função de API **GetSystemMetrics** para dimensionar em proporção à resolução de vídeo.<br /><br /> ![Alças de redimensionamentos](../../extensibility/ux-guidelines/media/0713-05_resizehandles.png "0713-05_ResizeHandles")|
|Girar um objeto selecionado|![Alças de rotação](../../extensibility/ux-guidelines/media/0713-06_rotate.png "0713-06_Rotate")|

#### <a name="keyboard-interaction"></a>Interação do teclado

|Entrada|Resultado|
|-----------|------------|
|Tab|Move o indicador de foco entre a ordem lógica dos objetos no editor. Isso pode ser da esquerda para a direita ou de cima para baixo, dependendo do valor da propriedade **TabIndex** (ou equivalente), da ordem de criação do objeto e da finalidade geral do editor. Shift + Tab inverte a direção do indicador de foco.|
|Barra de espaços|Ativa o modo panorâmico enquanto a tecla é mantida. A entrada adicional do mouse é necessária para deslocar a posição do visor.|
|Ctrl+Barra de espaços|Ativa o modo de zoom enquanto a tecla é mantida. A entrada adicional do mouse é necessária para aumentar e diminuir o fator de zoom.|
|CTRL + ALT + sinal de subtração|Diminui o fator de zoom em um nível.|
|CTRL + ALT + sinal de adição|Aumenta o fator de zoom em um nível.|
|Shift ou CTRL|Adiciona o objeto ao grupo de seleção. CTRL também permite remover objetos individualmente do grupo de seleção.|
|Digite|Executa o comando padrão para o objeto (geralmente aberto ou Edit).|
|F2|Ativa a edição in-loco para o objeto.|
|Teclas de direção|Move os objetos selecionados na direção da tecla de direção pressionada, em pequenos incrementos (por exemplo, 1 pixel por vez)|
|CTRL + teclas de direção|Move os objetos selecionados na direção da tecla de direção pressionada, em incrementos maiores (por exemplo, 10 pixels de cada vez)|
|Shift + teclas de direção|Redimensiona os objetos selecionados na respectiva direção, em pequenos incrementos (por exemplo, 1 pixel por vez)|
|Ctrl + Shift + teclas de direção|Redimensiona os objetos selecionados na respectiva direção, em incrementos maiores (por exemplo, 10 pixels de cada vez)|

 Quando os usuários editam controles em vigor, pode fazer sentido que os objetos sejam redimensionados automaticamente com a entrada do usuário. Por exemplo, se o usuário editar um controle rótulo, o rótulo deverá aumentar para exibir o texto que o usuário acabou de digitar. Se isso não for feito, o usuário deverá redimensionar o controle manualmente depois de editar o texto. Se o usuário tiver muitos controles, isso se tornará uma tarefa atividades rotineiras e não-técnica.

#### <a name="graphical-containers"></a>Contêineres gráficos
 Em alguns casos, os editores gráficos fornecem contêineres para outros objetos gráficos, como o controle de painel de Windows Forms ou o controle de layout de grade no designer de HTML. Se o seu editor fornece contêineres para outros objetos gráficos, o modelo de seleção a seguir deve ser usado somente para o contêiner (os objetos dentro do contêiner seguem o modelo padrão, conforme descrito acima):

|Entrada|Resultado|
|-----------|------------|
|Clique uma vez no contêiner|Seleciona o objeto de contêiner sem selecionar diretamente nenhum dos objetos contidos. O contêiner pode ser movido e/ou redimensionado com a entrada padrão do mouse e do teclado (conforme descrito acima). Os objetos contidos são movidos em relação ao contêiner, mas os objetos contidos não são redimensionados, a menos que também sejam selecionados diretamente.|
|Passe o mouse sobre a região de limite do contêiner|Transforma o mouse no cursor de movimentação, indicando que o contêiner pode ser movido.|
|Arraste a região de limite do contêiner|Altera o mouse para o cursor de movimentação e move o contêiner (e os objetos contidos dentro). O contêiner não pode ser movido sem ser selecionado primeiro com um único clique.|
|Clique uma vez em um objeto dentro do contêiner|Anula a seleção do contêiner (se selecionado) e seleciona apenas o objeto clicado.|
|Shift + clique ou CTRL + clique em um objeto e/ou contêiner contido|Adiciona o objeto clicado a uma seleção ou grupo de seleção existente. Se o objeto clicado já for um membro do grupo de seleção, ele será removido do grupo de seleção.|

 Os objetos contidos devem aderir ao modelo de seleção básico, conforme descrito na seção anterior. Do teste de usabilidade do designer de Windows Forms, os usuários esperavam acesso contínuo aos objetos contidos sem etapas intermediárias (impostas pelo objeto de confinamento).

#### <a name="disjoint-and-region-selections"></a>Seleções de separação e de região
 Os editores de objeto gráfico devem dar suporte a seleções não junção. Observe que esse gráfico não mostra a aparência do controle do Visual Studio. Consulte [aparência da seleção de objeto gráfico](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_GraphicalObjectSelectionAppearance) para obter especificações visuais detalhadas.

 ![Seletores de região e não contíguos](../../extensibility/ux-guidelines/media/0713-07_disjointregionselectors.png "0713-07_DisjointRegionSelectors")

 **Seleção não contíguo**

 Os editores gráficos também devem fornecer seleções de região com um indicador de seleção de tipo de letreiro. Se o editor gráfico oferecer suporte a outros tipos de objeto (como texto), as seleções de região poderão não ser possíveis dependendo das restrições desses outros tipos de objeto.

 ![Seleção de letreiro](../../extensibility/ux-guidelines/media/0713-08_marqueeselection.png "0713-08_MarqueeSelection")

 **Seleção de letreiro**

#### <a name="primary-and-secondary-selections"></a>Seleções primárias e secundárias
 Alguns editores de objeto gráfico permitem que o usuário edite ou alinhe objetos em grupos. Nesse caso, o conceito de seleções primárias e secundárias precisa ser introduzido. A seleção principal é o objeto ao qual todos os outros objetos respondem para operações de grupo. O objeto que o usuário seleciona primeiro se torna o controle principal e as seleções subsequentes se tornam as seleções secundárias. A seleção principal tem um tratamento visual distinto das seleções secundárias para indicar qual objeto é primário:

 ![Seleção primária e secundária](../../extensibility/ux-guidelines/media/0713-09_primarysecondary.png "0713-09_PrimarySecondary")

 **Seleção primária com duas seleções secundárias**

#### <a name="graphical-object-selection-appearance"></a><a name="BKMK_GraphicalObjectSelectionAppearance"></a> Aparência da seleção de objeto gráfico
 As alças de seleção são quadrados desenhados em um padrão retangular ao redor da caixa delimitadora do objeto. O gráfico a seguir mostra exemplos dos vários Estados que um objeto gráfico pode ter com identificador, dimensionamento e aparência de edição in-loco. O tamanho dos identificadores deve ser vinculado à borda da janela e às métricas de borda usando a API **GetSystemMetrics** .

| Estado | Aparência | Detalhes visuais |
|-------------------------|---------------| - |
| **Não selecionado** | Padrão | ![Estado do botão padrão](../../extensibility/ux-guidelines/media/0713-10_defaultstate.png "0713-10_DefaultState") |
| **Seleção primária** | Redimensionável | ![Seleção primária com alças de redimensionamento](../../extensibility/ux-guidelines/media/0713-11_primaryresize.png "0713-11_PrimaryResize") |
| **Seleção primária** | Não redimensionável | ![Seleção primária sem identificadores de redimensionamento](../../extensibility/ux-guidelines/media/0713-13_primarynoresize.png "0713-13_PrimaryNoResize") |
| **Seleção primária** | Bloqueado | ![Seleção primária bloqueada](../../extensibility/ux-guidelines/media/0713-15_primarylocked.png "0713-15_PrimaryLocked") |
| **Seleção secundária** | Redimensionável | ![Seleção secundária com alças de redimensionamento](../../extensibility/ux-guidelines/media/0713-17_secondaryresize.png "0713-17_SecondaryResize") |
| **Seleção secundária** | Não redimensionável | ![Seleção secundária sem identificadores de redimensionamento](../../extensibility/ux-guidelines/media/0713-19_secondarynoresize.png "0713-19_SecondaryNoResize") |
| **Seleção secundária** | Bloqueado | ![Seleção secundária bloqueada](../../extensibility/ux-guidelines/media/0713-21_secondarylocked.png "0713-21_SecondaryLocked") |
| **IU ativa** | Padrão | ![Estado ativo da interface do usuário](../../extensibility/ux-guidelines/media/0713-23_uiactive.png "0713-23_UIActive") |

### <a name="view-selection-models"></a>Exibir modelos de seleção

#### <a name="tree-view"></a>Exibição em árvore
 A seleção em um modo de exibição de árvore é mostrada com um realce simples. Se o usuário clicar em um nome de nó ou um ícone de nó, o nó será selecionado. Os glifos triangulares à esquerda do nó expandem ou contratam o controle de árvore, mas não afetam a seleção do usuário, com uma exceção: ao recolher um nó pai quando a seleção está em um filho desse nó, a seleção é movida para o pai.

 ![Modo de exibição de árvore típico no Visual Studio](../../extensibility/ux-guidelines/media/0713-25_treeview.png "0713-25_TreeView")

 **Modo de exibição de árvore típico no Visual Studio**

 As exibições de árvore podem dar suporte a seleções contíguas e não interjunção, mesmo em vários níveis na árvore. Várias seleções contíguas ou não interjunçãos devem ser feitas em nós de árvore visíveis. Se um nó for recolhido, a seleção não contíguo será perdida e o nó que foi recolhido obterá a seleção. Dessa forma, o usuário pode ver os nós que serão afetados por uma operação. Quando os nós são recolhidos, fica claro quais nós podem ser afetados.

 Quando um nó pai é selecionado, a operação deve ser aplicada ao pai, embora possa haver casos em que faz sentido que uma operação seja aplicada ao pai e a todos os seus filhos. Nesse caso, forneça uma interface do usuário adicional durante a operação, como uma caixa de seleção ou diálogo de confirmação para tornar a opção "aplicar a todos os filhos" explícita ao usuário.

##### <a name="renaming"></a>Renomear
 Se os nós na árvore oferecerem suporte à renomeação, a renomeação deverá ser feita em vigor. A operação in-loco deve ser a padrão em todos os controles de árvore no Visual Studio. Forneça um comando de renomeação que ativa imediatamente o modo de edição in-loco, com a seleção de texto que cobre o nome completo do nó, pronto para aceitar a entrada do usuário. Se o nó representar um arquivo, o nome do arquivo deverá conter a extensão. O realce de seleção deve incluir apenas o corpo do nome de arquivo e não a extensão.

|Entrada|Resultado|
|-----------|------------|
|Tecla Enter|Confirma a operação de renomeação|
|Tecla Esc|Cancela a operação de renomeação|
|Clicando fora da região de edição in-loco|Confirma a operação de renomeação|
|Desfazer|Fornecer fácil desfazer para cancelar a operação de renomeação|

#### <a name="selection-within-lists-and-grid-controls"></a>Seleção dentro de listas e controles de grade
 O conceito-chave na seleção de lista é que ele é baseado em linha, o que significa que quando uma seleção é feita, a linha inteira é selecionada como uma unidade. Por outro lado, as grades podem permitir que células específicas sejam selecionadas sem afetar nenhum outro aspecto da linha. As grades também podem conter uma hierarquia de linhas aninhadas (como em um árvore) que permitem que branches inteiros da hierarquia sejam selecionados e desmarcados pela interação com as linhas pai. A seleção nas listas é mostrada por uma cor de realce simples em toda a linha de dados. O foco é mostrado por uma borda pontilhada de pixel único em torno da linha editável atual ou da célula (linha se todas as células são somente leitura).

> [!NOTE]
> O **foco** e a **seleção** são conceitos diferentes. *Focus* é uma indicação de qual elemento de interface do usuário é destinado a receber entrada não explicitamente direcionada a outro objeto, enquanto a *seleção* refere-se ao estado da inclusão de um objeto em um conjunto de objetos nos quais as operações subsequentes podem ocorrer.

 Seleções em listas podem ser contíguas, não junção ou região. Quando várias seleções são permitidas, a seleção contígua e não-junção sempre deve ser suportada, enquanto o suporte para seleções de região (caixa) é opcional. As seleções de região são iniciadas arrastando no espaço em branco do corpo da lista.

| Objeto | Seleção |
|--------|------------|
| Lista | Vizinha |
| Lista | Não contíguo |
| Lista | Região |

 Clicar uma vez em uma lista seleciona a linha na qual o clique ocorreu. Se o usuário for clicar em uma célula de lista que dá suporte à edição in-loco, a célula também será imediatamente ativada para edição in-loco. Caso contrário, a linha inteira será selecionada imediatamente e mostrará um realce.

 Arrastar no corpo da lista faz uma das três coisas:

- Iniciará uma seleção de região se a lista der suporte e o mouse-Down estiver em espaço em branco

- Inicia uma operação de arrastar/soltar se a célula de lista ou linha oferece suporte a uma origem de arrastar

- Seleciona a linha atual

##### <a name="in-place-editing"></a>Edição in-loco
 Quando a edição in-loco é permitida, há dois modelos básicos: controle de edição simples e seletor de propriedade. Com um controle de edição simples, o conteúdo é realçado e está pronto para entrada do usuário assim que a edição in-loco é ativada. Onde um seletor de propriedade é implementado, o botão que invoca o seletor de propriedade é exibido quando o modo de edição in-loco é ativado e a seleção atual não é realçada. O botão do seletor deve ser justificado à direita na célula. Para obter exemplos de edição in-loco, consulte a **janela Propriedades** e **lista de tarefas** no Visual Studio.

##### <a name="keyboard-support"></a>Suporte de teclado
 O suporte do teclado para seleção em listas e grades segue as convenções padrão do Windows:

- As teclas de direção navegam na lista, selecionando cada linha/célula à medida que o foco é movido.

- Shift + seta executa uma seleção contígua na direção das teclas de direção.

- CTRL + seta seguida por barra de espaços alterna entre adicionar e remover itens de lista da seleção, criando uma seleção não junção.

- Para grades que contêm hierarquias aninhadas, a tecla de seta para a direita expande uma linha pai e a tecla de seta para a esquerda recolhe uma.

- A tecla TAB move o foco entre as células na linha atual se as células forem editáveis.

- A tecla Enter executa o comando padrão no item da lista (geralmente **aberto**).

- A tecla F2 ativa a edição in-loco para a célula selecionada no momento.

## <a name="persistence-and-saving-settings"></a><a name="BKMK_PersistenceAndSavingSettings"></a> Configurações de persistência e salvamento

### <a name="overview"></a>Visão geral
 Embora cada componente de software no Visual Studio seja geralmente responsável por seu próprio Estado e persistência, o Visual Studio salva automaticamente as configurações em alguns casos, como com tamanhos e posições de janela. A tabela a seguir é uma combinação de configurações salvas automaticamente e configurações que exigem um usuário explícito ou uma ação programada a ser executada.

|Objeto|O que salvar|Quando salvar|Onde salvar|
|------------|------------------|------------------|-------------------|
|Objeto selecionável (por exemplo, uma linha de código)|Um ponto de interrupção em uma linha de código<br /><br /> Um atalho de usuário associado à linha de código|Quando o projeto é salvo|O arquivo de **Opções do usuário (. suo)** para o projeto|
|caixa de diálogo|O local da caixa de diálogo, se tiver sido movido<br /><br /> A exibição que o usuário usou pela última vez na caixa de diálogo|Quando a caixa de diálogo fechar<br /><br /> Quando a sessão do Visual Studio termina|Na memória<br /><br /> Registro no **HKEY_CURRENT_USER**|
|Janela|O tamanho e o local da janela|Quando a janela for fechada<br /><br /> Quando o modo do Visual Studio é alterado<br /><br /> Quando a sessão do Visual Studio termina|O arquivo de **Opções do usuário (. suo)** para o projeto<br /><br /> Arquivo de opções personalizadas para configurações de janela|
|Documento|A seleção atual no documento<br /><br /> A exibição do documento<br /><br /> Os últimos vários locais que o usuário visitou|Quando o documento é salvo|O arquivo de **Opções do usuário (. suo)** para o projeto|
|Project|Referências a arquivos<br /><br /> Referências a diretórios em disco<br /><br /> Referências a outros softwares<br /><br /> Componentes<br /><br /> Informações de estado sobre o projeto em si|Quando o projeto é salvo|O arquivo de projeto|
|Solução|Referências a projetos<br /><br /> Referências a arquivos|Quando o projeto ou a solução é salva|O arquivo da **solução (. sln)**|
|Configurações em **ferramentas > opções**|Personalizações do teclado<br /><br /> Personalizações da barra de ferramentas<br /><br /> Esquemas de cor|Quando a caixa de diálogo **ferramentas > opções** for fechada<br /><br /> Quando a sessão do Visual Studio termina|Registro no **HKEY_CURRENT_USER**|

 O que o usuário está fazendo e quando eles estão fazendo isso, determina se uma configuração está sendo salva na memória (durante a sessão), salva em disco (entre sessões como uma configuração de registro), como parte do próprio arquivo de projeto ou de solução, como parte do arquivo de **Opções de solução (. suo)** ou como um arquivo de configurações personalizado que só esse componente de software sabe. A tabela acima mostra vários eventos em que as configurações podem ser salvas. No entanto, há outras ocasiões em que você talvez queira salvar o estado:

- Quando o usuário altera o local dentro de uma caixa de diálogo ou janela

- Quando o usuário transfere o foco para outra janela

- Quando o usuário alterna do design para o modo de depuração

- Quando o usuário faz logoff de sua conta

- Quando o computador entra em hibernação ou é desligado

- Quando o computador/disco rígido está prestes a ser reformatado e configurado novamente

### <a name="window-configurations"></a>Configurações de janela
 Uma configuração de janela é a apresentação básica do ambiente de desenvolvimento – é um esquema que consiste na lista de janelas de ferramentas presente e no modo como elas são organizadas. Para o Windows gerenciado pelo IDE (IDE Windows), as informações de layout são persistidas por usuário, portanto, quando um usuário inicia o IDE, o layout da janela é exibido da mesma forma que quando o Visual Studio foi encerrado pela última vez. O estado e a posição de janelas do IDE são persistidos em um arquivo de opções personalizado em formato XML. As janelas de ferramentas criadas por pacotes carregados no IDE persistem suas informações de estado no registro e podem ou não ser por usuário.

#### <a name="profile-specific-layouts"></a>Layouts específicos de perfil
 Cada perfil inclui layouts de janela de ferramentas, organizados de uma maneira familiar a pessoas de desenvolvedor específicas (Visual C++ os desenvolvedores esperam ver a **Gerenciador de soluções** no lado esquerdo do IDE, enquanto os desenvolvedores de C# esperam ver a **Gerenciador de soluções** à direita). Layouts de janela específicos de perfil são carregados depois que o usuário escolhe um perfil na inicialização. Um autor de pacote deve determinar o layout da janela mais adequado para a experiência do cliente, sabendo que as alterações feitas pelo usuário para a configuração da janela serão persistidas.

## <a name="touch-input"></a><a name="BKMK_TouchInput"></a> Entrada por toque
 Os usuários estão cada vez mais usando produtos de desenvolvimento da Microsoft em dispositivos de toque. No entanto, há barreiras que dificultam o uso de ferramentas de desenvolvimento em dispositivos sensíveis ao toque. Os usuários esperam que nossos produtos forneçam uma experiência de toque confiável e precisa. A intenção dessas diretrizes é informar as decisões sobre quais recursos de toque incorporar e incentivar uma experiência de toque consistente no Visual Studio e em produtos relacionados.

### <a name="levels-of-experience"></a>Níveis de experiência
 Os níveis de experiência a seguir destinam-se a servir como um guia para ajudar as equipes a decidir quais recursos de toque oferecer com base no nível desejado de interesse de investimento em contato.

- A **experiência básica** é para as equipes que desejam fornecer recursos de toque para que não haja nenhum inatividade em todo o trabalho.

- A **experiência otimizada** é para as equipes que desejam fornecer os recursos de toque mais comuns (por exemplo, aqueles normalmente disponíveis em aplicativos de navegador da Internet).

- A **experiência elevada** é para as equipes que desejam adicionar recursos como gestos ou outros recursos opcionais que podem tornar seu aplicativo amigável para o toque primeiro.

||Experiência básica|Experiência otimizada|Experiência elevada|
|-|----------------------|--------------------------|-------------------------|
|**Permite que os usuários...**|Corrigir a leitura de código e de solução/nível de projeto sem inatividade|Executar tarefas de manutenção, refactores e navegação|Opere em uma experiência consistente, intuitiva e fluida com confiança|
|**Editor**|Panorâmica e seleção de toque<br /><br /> Toque de ScrollBar para saltar e pressione + arrastar|Pinçar zoom<br /><br /> Rolagem rápida<br /><br /> Seleção<br /><br /> Fácil utilização do menu de contexto||
|**Principais janelas de ferramentas**|Listar movimento panorâmico<br /><br /> Seleção de item<br /><br /> Toque de ScrollBar para saltar e pressione + arrastar|Fácil rolagem e seleção de itens||
|**Windowing**||Redimensionar janela<br /><br /> Acesso rápido||
|**Bem-documento**||Navegação fácil entre arquivos abertos||
|**Gestos**||Garantir que os gestos comuns funcionem pelo IDE|Ações baseadas em gestos<br /><br /> Suporte a arrastar e soltar e designers|
|**Outras considerações**|||Teclado personalizado na tela|

#### <a name="gestures"></a>Gestos
 Os gestos fornecem aos usuários um atalho para comandos que, de outra forma, poderiam exigir uma interação mais complicada. Consulte as diretrizes do Windows sobre [gestos de toque comuns para aplicativos de área de trabalho](/windows/desktop/wintouch/windows-touch-gestures-overview)e siga estas diretrizes para a maioria dos gestos, incluindo gestos simples, como movimento panorâmico e zoom.
