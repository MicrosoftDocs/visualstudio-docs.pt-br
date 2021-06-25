---
title: Padrões de composição para o Visual Studio | Microsoft Docs
description: Saiba mais sobre padrões de composição importantes para consistência no Visual Studio. Padrões de composição combinam elementos de interação e design.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: e48ecfb2-f4b5-4d3a-b4a2-7a4d62fa4ec0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b8b84baa7be7449b8edb6241e415fc90c9acd594
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901416"
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

#### <a name="color"></a>Cor
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

1. **Persistência:** o conteúdo deve ser durável ou transitório?
   Os usuários querem manter as informações visíveis para se referirem ou interagirem? Ou os usuários querem ver rapidamente as informações e continuar com sua tarefa principal?

2. **Tipo de conteúdo:** o conteúdo será informacional, a actionable ou de navegação?
   O usuário precisa de detalhes adicionais sobre o conteúdo mestre? O usuário precisa concluir uma tarefa que afeta o conteúdo mestre? Ou o usuário precisa ser direcionado para outro recurso?

3. **Tipo de indicador:** um indicador de ambiente faz sentido?
   As informações podem ser resumidas de uma maneira útil e exibidas sem sobrecarregar o conteúdo mestre?

4. **Gestos:** quais gestos serão usados para invocar e descartar a interface do usuário?
   Como o usuário abrirá o conteúdo de detalhes e o enviará embora? Há valor para adicionar um gesto, como fixar para alternar entre estados transitórios e duráveis?

   Cada um desses quatro pontos de decisão terá um impacto sobre os principais componentes da interface do usuário no objeto.

### <a name="on-object-ui-components"></a>Componentes de interface do usuário no objeto

1. Tipo de contêiner (apresentador de conteúdo)

    - Flutuante

    - Embutido

2. Tipo de conteúdo

    - Informacional: dados que podem ser estáticos ou dinâmicos

    - A ação: comandos que alteram o conteúdo mestre

    - Navegação: links que levam o usuário para outra janela ou aplicativo, como o MSDN

3. Gestos

    - Invocação

    - Demissão

    - Fixação

    - Outras interações

4. Persistência e modelo de commit

    - Transitório

    - Durável

    - Automática

    - Sob demanda

5. Indicadores de ambiente (opcional)

    - Sublinhado de alternância

    - Ícone de marcação inteligente

    - Outros indicadores de ambiente

#### <a name="container-content-presenter-type"></a>Tipo de contêiner (apresentador de conteúdo)
 Há duas opções principais disponíveis para apresentar conteúdo no ponto de atenção:

1. **Em linha:** um apresentador em linha, como a exibição de espiar que foi introduzida no Editor de Código Visual Studio 2013, abre espaço para o novo conteúdo, deslocando o conteúdo existente.

    - **Prefira** os apresentadores em linha se você espera que os usuários deem uma quantidade significativa de tempo referindo-se ou interagindo com o conteúdo que você apresenta.

    - **Evite** os apresentadores em linha se você espera que os usuários quiserem dar uma olhada nas informações presentes e, em seguida, continuar com sua tarefa principal com interrupção mínima.

2. **Flutuante:** um apresentador flutuante é posicionado o mais próximo possível do conteúdo selecionado, mas não altera o layout do conteúdo existente. Várias estratégias podem ser empregadas, como exibir um painel de conteúdo flutuante sobre o espaço em branco mais próximo disponível para o símbolo selecionado.

    - **Prefira** os presentadores flutuantes se você espera que os usuários quiserem dar uma olhada nas informações presentes e, em seguida, continuar com sua tarefa principal com interrupção mínima.

    - **Evite** os presentadores flutuantes se você espera que os usuários deem uma quantidade significativa de tempo referindo-se ou interagindo com o conteúdo que você apresenta.

#### <a name="content-type"></a>Tipo de conteúdo
 Há três tipos principais de conteúdo que podem ser exibidos dentro de qualquer contêiner de interface do usuário no objeto. Qualquer combinação desses tipos de informações pode ser mostrada. Os três tipos são:

1. **Informativo: a** maioria dos contêineres de interface do usuário no objeto exibirá algum tipo de conteúdo informativo. O conteúdo pode representar informações sobre o estado atual do ambiente ou pode representar informações sobre um possível estado futuro do ambiente. Por exemplo, ele pode ser usado para mostrar o efeito de um comando específico, como uma refactoring, no código existente.

    - **Sempre** use a representação canônica das informações exibidas. Por exemplo, o código deve ser parecido com código, completo com realce de sintaxe e deve respeitar qualquer fonte e outras configurações de ambiente definidas pelo usuário.

    - **Sempre** considere dar suporte a qualquer ação sobre o conteúdo informacional que seria possível se essas mesmas informações são apresentadas como conteúdo mestre. Por exemplo, se estiver apresentando código existente dentro de um contêiner de interface do usuário no objeto, considere fortemente dar suporte à capacidade de procurar e modificar esse código.

    - **Sempre** considere usar uma cor da tela de fundo diferente se apresentar conteúdo informativo que representa um possível estado futuro.

2. A ação: alguns contêineres de interface do usuário no objeto fornecerão a capacidade de executar alguma ação sobre o conteúdo mestre, como executar uma operação de refactoring.

    - **Sempre** posicione comandos acionáveis separadamente do conteúdo informacional.

    - **Sempre** habilita e desabilita ações quando apropriado.

    - **Sempre** consulte as diretrizes padrão para representar comandos dentro das caixas de diálogo.

    - **Sempre** mantenha o número de ações expostas em um contêiner de interface do usuário no objeto para um mínimo absoluto. Interagir com a interface do usuário no objeto deve ser uma experiência leve e rápida. O usuário não deve ter que gastar energia para gerenciar o próprio contêiner de interface do usuário no objeto.

    - **Sempre** considere como e quando um contêiner de interface do usuário no objeto será fechado ou ignorado. Como melhor prática, qualquer ação que conclua a caixa de diálogo entre o conteúdo mestre e detalhado também deve fechar o contêiner de interface do usuário no objeto quando essa ação for invocada.

3. **Navegação: alguns** contêineres de interface do usuário no objeto incluem links que levam o usuário para outra janela ou aplicativo, como abrir um artigo do MSDN no navegador da Web do usuário.

    - **Sempre** preenda qualquer link de navegação com "Abrir" para que os usuários não se desempenhem ao serem navegados para algum outro conteúdo.

    - **Sempre** separe links de navegação de links a ação.

#### <a name="ambient-indicators-optional"></a>Indicadores de ambiente (opcional)
 Os indicadores de ambiente podem ser sutis, incluindo o texto apresentado em uma cor contrastada do restante do código ou óbvios, incluindo símbolos de cor mais simples, como sublinhados de alternância e ícones de marca inteligente. Os indicadores de ambiente comunicam a disponibilidade de informações adicionais e relevantes. O ideal é que eles forneçam informações úteis mesmo sem exigir que o usuário interaja com eles.

- **Sempre** posicione um indicador de ambiente para que ele não a distração nem sobrecarregar o usuário. Se for impossível posicionar um indicador de ambiente dessa maneira, considere outra solução.

- **Sempre** posicione o indicador de ambiente o mais próximo possível do conteúdo ao que ele está relacionado.

- **Sempre** tente criar um indicador que resume as informações disponibilizadas. Considere fornecer uma contagem do número de itens de dados disponíveis (por exemplo, "3 referências" em vez de simplesmente "Referências") ou pensar em alguma outra maneira de resumir os dados.

  - Nos casos em que os dados de um indicador não podem sempre ser computados e exibidos, considere imediatamente fornecer comentários progressivos à medida que os valores são computados. Por exemplo, considere animar alterações que refletem atualizações nos dados disponíveis, semelhante à maneira como o email ao vivo no Windows Phone é atualizado à medida que o número de emails não lidos aumenta.

- **Nunca** adicione mais indicadores do que um usuário pode aceitar razoavelmente para uma determinada parte do conteúdo. Os indicadores de ambiente devem ser úteis sem a necessidade de interação do usuário. Os indicadores perderão a ambiência se exigirem estouro e outros controles de gerenciamento para exibi-los.

#### <a name="gestures"></a>Gestos
 Um aspecto importante de permitir que o usuário mantenha o foco no conteúdo mestre é dar suporte aos gestos certos para abrir e descartar o conteúdo de detalhes adicional.

- **Sempre** exigir que o usuário execute algum gesto explícito para abrir o conteúdo adicional. Os gestos abertos comuns incluem:

  - **Passar o mouse:** dicas de ferramenta ou conteúdo informacional não interativo

  - **Comando explícito:** apresentador em linha

  - **Clique duas vezes no indicador de ambiente:** Janela pop-up do CodeLens

- **Sempre** descarte o conteúdo de detalhes sempre que o usuário pressionar a tecla Esc.

- **Sempre** considere o contexto da interface do usuário no objeto. Para os presentadores de conteúdo que permitem a interação dentro do contêiner, considere cuidadosamente se é preciso mostrar informações adicionais sobre o foco, o que provavelmente poderá ser uma interrupção para o fluxo de trabalho do usuário.

- **Nunca** exibir conteúdo ao passar o mouse que parece ser editável ou convida a interação do usuário. Esse comportamento pode frustrar os usuários se tentarem mover o cursor sobre o conteúdo de detalhes, pois o comportamento padrão de uma dica de ferramenta é descartar imediatamente quando o cursor não estiver mais sobre o conteúdo mestre que o produziu.

## <a name="selection-models"></a><a name="BKMK_SelectionModels"></a> Modelos de seleção

### <a name="overview"></a>Visão geral
 Um modelo de seleção é o mecanismo usado para indicar e confirmar operações em um ou mais objetos de interesse na interface do usuário. Este tópico discute os padrões de interação de seleção Visual Studio editores de documentos: editores de texto, superfícies de design e superfícies de modelagem.

 Os usuários devem ter uma maneira de indicar Visual Studio no que estão trabalhando e Visual Studio devem responder de forma previsível com comentários aos usuários sobre o que ele está operando. Diferenças ou um erro de comunicação entre o usuário e a interface do usuário podem fazer com que o usuário não perceba uma ação, o que pode ter consequências não intencionais. Geralmente, o erro passa despercebido até que o usuário veja que algo está ausente ou foi alterado. Os modelos de seleção são, portanto, uma das partes mais críticas do design de interface do usuário. Embora os modelos de seleção Visual Studio sejam consistentes com o Windows, há pequenas variações.

 No Visual Studio, como no Windows, os modelos de seleção diferem dependendo do contexto no qual a interação ocorre. As seleções podem ocorrer em quatro tipos de objetos:

- Texto

- Objetos gráficos

- Listas e árvores

- Grades

  Dentro desses objetos, há três tipos de seleções:

- Contíguo

- Separado

- Região

#### <a name="scope"></a>Escopo
 O componente mais importante da seleção é garantir que o usuário saiba em qual janela ele está trabalhando (ativação) e onde o foco está localizado (seleção). Visual Studio estende a funcionalidade de gerenciamento de janelas no Windows, mas o esquema de ativação é o mesmo: interagir com uma janela traz o foco para a janela. Visual Studio tem dois indicadores para ativação: um para janelas de documentos e outro para janelas de ferramentas.

 Para janelas de documentos, a janela ativa é indicada por uma guia da janela do documento que chega à frente e altera sua cor da tela de fundo:

 ![Seleção de guias ativas Visual Studio](../../extensibility/ux-guidelines/media/0713-01_activetab.png "0713-01_ActiveTab")

 **Seleção de guia ativa**

 Para janelas de ferramentas, a janela ativa é indicada por uma alteração na cor da área da barra de título da janela de ferramentas:

 ![Seleção de janela de ferramentas ativa Visual Studio](../../extensibility/ux-guidelines/media/0713-02_activetoolwindow.png "0713-02_ActiveToolWindow")

 **Janela de ferramentas ativa mostrando a seleção primária de um nó**

 ![Seleção de janela de ferramentas inativas Visual Studio](../../extensibility/ux-guidelines/media/0713-03_inactivetoolwindow.png "0713-03_InactiveToolWindow")

 **Janela de ferramentas inativa, mostrando a seleção latente do nó**

 Quando uma janela está ativa, seu foco é indicado de acordo com os modelos de seleção descritos nesta seção das diretrizes.

#### <a name="context"></a>Contexto
 Visual Studio foi projetado para manter um conceito forte de contexto, mantendo o controle de onde o usuário está trabalhando. Apenas uma janela está ativa, seja uma janela de ferramenta ou de documento. No entanto, a janela de documentos mais alta sempre retém uma seleção latente. Embora o foco possa estar em uma janela de ferramentas, a janela do documento que estava ativa pela última vez exibe uma seleção, mesmo em um estado inativo. Isso é feito para manter o contexto do usuário no documento que ele estava editando, mostrando que o Visual Studio retém seu estado para que ele possa retornar e mudar perfeitamente entre janelas de ferramentas e janelas de documentos.

### <a name="text-selection"></a>Seleção de texto
 Visual Studio editores que são estritamente textuais, como o editor de texto integrado, usam o mesmo modelo de seleção de texto e aparência descritos na página Mouse e [Ponteiros](/windows/desktop/uxguide/inter-mouse) das Diretrizes de Interação do Usuário do Windows no MSDN. O foco de entrada no editor de texto é indicado por uma barra vertical chamada ponto de inserção. O ponto de inserção é um único pixel espesso e colorido como o inverso de tudo o que aparece atrás dele. Ele pisca de acordo com a taxa definida pela  configuração de taxa de piscar **cursor** na guia Velocidade do **applet** Teclado no Painel de Controle.

#### <a name="contiguous-and-disjoint-selection"></a>Seleção contígua e não contígua
 A seleção no editor de texto é somente contígua. As seleções de texto não são permitidas, mas devem ser abordadas em editores de objetos gráficos. Quando o ponteiro do mouse do usuário está sobre uma área de texto, o cursor muda para um raio I. Um único clique coloca o ponto de inserção no editor de texto no local do clique. Manter o botão do mouse pressionado inicia um realçamento de seleção e a liberação do botão do mouse encerra o realçamento da seleção.

#### <a name="region-selection-box-selection"></a>Seleção de região (seleção de caixa)
 Visual Studio dá suporte a seleções de região no editor de texto e isso é chamado de seleção de caixa. A seleção de caixa permite que o usuário selecione uma região de texto que não segue o fluxo de texto normal. Assim como na seleção de texto padrão, a seleção deve ser contígua. A seleção de caixa é iniciada mantendo a tecla Alt para baixo ao arrastar com o mouse. A seleção de caixa também pode ser iniciada mantendo as teclas Alt e Shift ao usar as teclas de seta para indicar a região da seleção. A seleção de caixa usa o realçamento de seleção normal e mostra o cursor do ponto de inserção piscando no final da área de seleção.

 ![Caixa &#40;caixa&#41; seleção no Visual Studio](../../extensibility/ux-guidelines/media/0713-04_boxselection.png "0713-04_BoxSelection")

 **Seleção de região (caixa) Visual Studio**

#### <a name="text-selection-appearance"></a>Aparência da seleção de texto
 As cores usadas para seleção ativa e inativa no editor podem ser personalizadas. Para personalizar a aparência visual do editor, um usuário pode ir para Ferramentas **> Opções** e, em seguida, procurar Em Ambiente **> Fontes** e Cores > Editor de Texto .

### <a name="graphical-selection"></a>Seleção gráfica

#### <a name="interaction"></a>Interação
 A seleção de objeto gráfico pode ser complexa e depende de vários fatores:

- **O modelo de seleção principal do editor.** Editores que contêm objetos gráficos também podem ser usados para editar texto ou grades. Por exemplo, o editor pode ser um editor baseado em texto que também dá suporte ao posicionamento de objetos gráficos, como o designer Visual Studio XAML. O suporte a vários tipos de objeto pode afetar a maneira como o usuário seleciona grupos de diferentes tipos de objetos.

- **Suporte para estados de seleção primária e secundária.** Um editor pode fornecer estados de seleção primária e secundária para que os objetos possam ser editados em uníson, alinhados entre si, reorganizados juntos e assim por diante.

- **Suporte à edição in-in-place.** Os editores também podem permitir que o conteúdo de seus objetos gráficos seja editado. Por exemplo, uma forma de retângulo também pode conter texto no interior que pode ser alterado pelo usuário. Além disso, esse texto pode ser centralizado ou justificado. A edição in-locar envolve um nível mais detalhado de interação do usuário e, portanto, requer um conjunto apropriado de responsabilidades visuais para apresentar informações de estado ao usuário.

#### <a name="mouse-interaction"></a>Interação do mouse

|Entrada|Resultado|
|-----------|------------|
|Clique em um objeto não selecionado|Seleciona o objeto e exibe uma linha tracejada e identificador de seleção, se o objeto for resizável.|
|Clique em um objeto selecionado|Ativa a edição in-locar se o objeto dá suporte a ela. Clicar fora do objeto desativa o modo de edição in-place.|
|Clique duas vezes em um objeto|Abre o código por trás do objeto para edição e pode inserir um manipulador de eventos padrão, se apropriado.|
|Apontar para um objeto|Altera o ponteiro para o cursor de movimentação. A aparência do objeto, como sua luminosidade ou cor, pode mudar.|
|Apontar para um alça de seleção|Altera o ponteiro para o cursor de resize. Para objetos que suportam a rotação, alguns alças de seleção podem alterar o ponteiro para um cursor de rotação, pois o ponteiro é posicionado de forma diferente (por exemplo, movido para mais longe) em relação à alça de seleção.|
|Arrastar|Mesmo que o objeto não seja selecionado anteriormente, altera o ponteiro para o cursor de movimentação e move o objeto.|
|O editor perde o foco|Desativa o modo de edição in-loco, embora o objeto mantenha o conteúdo e a aparência que tinha durante seu último estado de operação/seleção.|
|Seleção de objeto|Indicado por uma borda, linha pontilhada ou outro tratamento visualmente distinto para realça o limite do objeto.|
|Resize um objeto selecionado|Indicado por alças de seleção.<br /><br /> Um objeto reizável tem oito identificador, representando cada direção na qual ele pode ser reessado. Menos identificador podem ser usados se o objeto só puder ser resized em determinadas direções. Quando o usuário tamanho um objeto para baixo até onde oito identificador não seriam interativos, quatro identificador podem ser usados. Os tamanhos de alça devem ser vinculados às métricas de borda e borda da janela com a função da API **GetSystemMetrics** para o tamanho proporcional à resolução de exibição.<br /><br /> ![Alças de redimensionamentos](../../extensibility/ux-guidelines/media/0713-05_resizehandles.png "0713-05_ResizeHandles")|
|Girar um objeto selecionado|![Girar alças](../../extensibility/ux-guidelines/media/0713-06_rotate.png "0713-06_Rotate")|

#### <a name="keyboard-interaction"></a>Interação do teclado

|Entrada|Resultado|
|-----------|------------|
|Tab|Move o indicador de foco entre a ordem lógica dos objetos no editor. Isso pode ser da esquerda para a direita ou de cima para baixo, dependendo do valor da propriedade **TabIndex** (ou equivalente), da ordem de criação do objeto e da finalidade geral do editor. Shift+Tab inverte a direção do indicador de foco.|
|Barra de espaços|Ativa o modo de panorâmico enquanto o controle de teclas é mantido. A entrada adicional do mouse é necessária para panorcar a posição do viewport.|
|Ctrl+Barra de espaços|Ativa o modo de zoom enquanto o controle de teclas é mantido. A entrada adicional do mouse é necessária para aumentar e diminuir o fator de zoom.|
|Ctrl+Alt+Sinal de subtração|Diminui o fator de zoom em um nível.|
|Ctrl+Alt+Sinal de adição|Aumenta o fator de zoom em um nível.|
|Shift OR Ctrl|Adiciona o objeto ao grupo de seleção. Ctrl também permite remover objetos individualmente do grupo de seleção.|
|Digite|Executa o comando padrão para o objeto (geralmente Abrir ou Editar).|
|F2|Ativa a edição in-place para o objeto .|
|Teclas de direção|Move os objetos selecionados na direção da tecla de direção pressionada, em incrementos pequenos (por exemplo, 1 pixel por vez)|
|Teclas ctrl+seta|Move os objetos selecionados na direção da tecla de direção pressionada, em incrementos maiores (por exemplo, 10 pixels por vez)|
|Shift+teclas de direção|Resize os objetos selecionados na respectiva direção, em incrementos pequenos (por exemplo, 1 pixel por vez)|
|Teclas Ctrl+Shift+seta|Resize os objetos selecionados na respectiva direção, em incrementos maiores (por exemplo, 10 pixels por vez)|

 Quando os usuários editam controles no local, pode fazer sentido que os objetos reizem automaticamente com a entrada do usuário. Por exemplo, se o usuário editar um controle de rótulo, o rótulo deverá aumentar para exibir o texto que o usuário acabou de digitar. Se isso não for feito, o usuário deverá reorganizar o controle manualmente depois de editar o texto. Se o usuário tiver muitos controles, isso se tornará uma tarefa roteável e não produtiva.

#### <a name="graphical-containers"></a>Contêineres gráficos
 Em alguns casos, os editores gráficos fornecem contêineres para outros objetos gráficos, como o controle painel Windows Forms ou o controle Layout de Grade no designer HTML. Se o editor fornece contêineres para outros objetos gráficos, o modelo de seleção a seguir deve ser usado somente para o contêiner (os objetos dentro do contêiner seguem o modelo padrão, conforme descrito acima):

|Entrada|Resultado|
|-----------|------------|
|Clique com um único clique no contêiner|Seleciona o objeto de contêiner sem selecionar diretamente nenhum dos objetos contidos. O contêiner pode ser movido e/ou reorganizado com entrada padrão de mouse e teclado (conforme descrito acima). Os objetos contidos são movidos em relação ao contêiner, mas os objetos contidos não são resized, a menos que também sejam selecionados diretamente.|
|Passe o mouse sobre a região de limite do contêiner|Transforma o mouse no cursor de movimentação, indicando que o contêiner pode ser movido.|
|Arrastar a região de limite do contêiner|Altera o mouse para o cursor de movimentação e move o contêiner (e os objetos contidos dentro). O contêiner não pode ser movido sem primeiro ser selecionado com um único clique.|
|Clique com um único clique em um objeto dentro do contêiner|Desmarca o contêiner (se selecionado) e seleciona apenas o objeto clicado.|
|Shift+clique em OU Ctrl+clique em um objeto contido e/ou contêiner|Adiciona o objeto clicado a um grupo de seleção ou seleção existente. Se o objeto clicado já for um membro do grupo de seleção, ele será removido do grupo de seleção.|

 Os objetos contidos devem aderir ao modelo de seleção básico, conforme descrito na seção anterior. Do teste de usabilidade do designer Windows Forms, os usuários esperaram acesso contínuo aos objetos contidos sem intervir em etapas (impostas pelo objeto de contenção).

#### <a name="disjoint-and-region-selections"></a>Seleções de regiões e não adjacentes
 Os editores de objetos gráficos devem dar suporte a seleções não adjacentes. Observe que este gráfico não mostra a aparência do controle para Visual Studio. Confira [Aparência de seleção de objeto gráfico](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_GraphicalObjectSelectionAppearance) para ver especificações visuais detalhadas.

 ![Seletores de região e desaconsuletores](../../extensibility/ux-guidelines/media/0713-07_disjointregionselectors.png "0713-07_DisjointRegionSelectors")

 **Seleção desconsint**

 Os editores gráficos também devem fornecer seleções de região com um indicador de seleção de tipo de letreiro. Se o editor gráfico for compatível com outros tipos de objeto (como texto), as seleções de região poderão não ser possíveis dependendo das restrições desses outros tipos de objeto.

 ![Seleção de letreiro](../../extensibility/ux-guidelines/media/0713-08_marqueeselection.png "0713-08_MarqueeSelection")

 **Seleção de letreiro**

#### <a name="primary-and-secondary-selections"></a>Seleções primárias e secundárias
 Alguns editores de objetos gráficos permitem que o usuário edite ou alinhe objetos em grupos. Nesse caso, o conceito de seleções primárias e secundárias precisa ser introduzido. A seleção primária é o objeto ao qual todos os outros objetos respondem para operações de grupo. O objeto que o usuário seleciona primeiro se torna o controle primário e as seleções subsequentes se tornam as seleções secundárias. A seleção primária tem um tratamento visual distinto das seleções secundárias para indicar qual objeto é primário:

 ![Seleção primária e secundária](../../extensibility/ux-guidelines/media/0713-09_primarysecondary.png "0713-09_PrimarySecondary")

 **Seleção primária com duas seleções secundárias**

#### <a name="graphical-object-selection-appearance"></a><a name="BKMK_GraphicalObjectSelectionAppearance"></a> Aparência da seleção de objeto gráfico
 As alças de seleção são quadrados desenhados em um padrão retangular em torno da caixa delimitada do objeto. O gráfico a seguir mostra exemplos dos vários estados que um objeto gráfico pode ter com a aparência de edição no local, o tamanho e o identificador. O tamanho dos alças deve ser vinculado às métricas de borda e borda da janela usando a API **GetSystemMetrics.**

| Estado | Aparência | Detalhes visuais |
|-------------------------|---------------| - |
| **Não selecionado** | Padrão | ![Estado do botão padrão](../../extensibility/ux-guidelines/media/0713-10_defaultstate.png "0713-10_DefaultState") |
| **Seleção primária** | Redimensionável | ![Seleção primária com alças de reeslização](../../extensibility/ux-guidelines/media/0713-11_primaryresize.png "0713-11_PrimaryResize") |
| **Seleção primária** | Não reizável | ![Seleção primária sem alças de reeslização](../../extensibility/ux-guidelines/media/0713-13_primarynoresize.png "0713-13_PrimaryNoResize") |
| **Seleção primária** | Bloqueado | ![Seleção primária bloqueada](../../extensibility/ux-guidelines/media/0713-15_primarylocked.png "0713-15_PrimaryLocked") |
| **Seleção secundária** | Redimensionável | ![Seleção secundária com alças de reeslização](../../extensibility/ux-guidelines/media/0713-17_secondaryresize.png "0713-17_SecondaryResize") |
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
|Janela|O tamanho e o local da janela|Quando a janela é fechada<br /><br /> Quando o modo de Visual Studio é muda<br /><br /> Quando a sessão Visual Studio termina|O **arquivo de opções do usuário (.suo)** para o projeto<br /><br /> Arquivo de opções personalizadas para configurações de janela|
|Documento|A seleção atual no documento<br /><br /> A exibição do documento<br /><br /> Os últimos lugares que o usuário visitou|Quando o documento é salvo|O **arquivo de opções do usuário (.suo)** para o projeto|
|Project|Referências a arquivos<br /><br /> Referências a diretórios em disco<br /><br /> Referências a outros softwares<br /><br /> Componentes<br /><br /> Informações de estado sobre o projeto em si|Quando o projeto é salvo|O arquivo de projeto|
|Solução|Referências a projetos<br /><br /> Referências a arquivos|Quando o projeto ou a solução é salvo|O **arquivo de solução (.sln)**|
|Configurações em **Ferramentas > Opções**|Personalizações de teclado<br /><br /> Personalizações da barra de ferramentas<br /><br /> Esquemas de cor|Quando a **caixa de diálogo > Ferramentas é** fechado<br /><br /> Quando a sessão Visual Studio termina|Registro no **HKEY_Current_User**|

 O que o usuário está fazendo e quando ele está fazendo isso determina se uma configuração está sendo salva na memória (durante a sessão), salva no disco (entre sessões como uma configuração do Registro), como parte do próprio arquivo de projeto ou solução, como parte do arquivo de opções de solução **(.suo)** ou como um arquivo de configurações personalizadas que apenas esse componente de software conhece. A tabela acima mostra vários eventos nos quais as configurações podem ser salvas. No entanto, há outras vezes em que talvez você queira salvar o estado:

- Quando o usuário altera o local dentro de uma caixa de diálogo ou janela

- Quando o usuário transfere o foco para outra janela

- Quando o usuário alterna do design para o modo de depuração

- Quando o usuário faz o logs de sua conta

- Quando o computador entra em hibernação ou é desligado

- Quando o computador/disco rígido estiver prestes a ser reformatado e configurar novamente

### <a name="window-configurations"></a>Configurações de janela
 Uma configuração de janela é a apresentação básica do ambiente de desenvolvimento – é um esquema que consiste na lista de janelas de ferramentas presentes e na maneira como elas são organizadas. Para janelas gerenciadas pelo IDE (janelas IDE), as informações de layout são persistidas por usuário, portanto, quando um usuário inicia o IDE, o layout da janela aparece igual ao da última vez que saiu do Visual Studio. O estado e a posição das janelas IDE são persistentes em um arquivo de opções personalizado no formato XML. As janelas de ferramentas criadas por pacotes carregados no IDE persistem suas informações de estado no Registro e podem ou não ser por usuário.

#### <a name="profile-specific-layouts"></a>Layouts específicos do perfil
 Cada perfil inclui layouts de janela de ferramentas, organizados de maneira familiar a personas específicas do desenvolvedor (os desenvolvedores Visual C++ esperam ver o **Gerenciador de Soluções** no lado esquerdo do IDE, enquanto os desenvolvedores de C# esperam ver o **Gerenciador de Soluções** à direita). Os layouts de janela específicos do perfil são carregados depois que o usuário escolhe um perfil na inicialização. Um autor do pacote deve determinar o layout da janela mais adequado para a experiência do cliente, sabendo que as alterações feitas pelo usuário na configuração da janela serão persistida.

## <a name="touch-input"></a><a name="BKMK_TouchInput"></a> Entrada de toque
 Os usuários estão cada vez mais usando produtos de desenvolvimento da Microsoft em dispositivos touch. No entanto, há barreiras que dificultam o uso de ferramentas de desenvolvimento em dispositivos de toque. Os usuários esperarão que nossos produtos forneçam uma experiência de toque confiável e precisa. A intenção dessas diretrizes é informar as decisões sobre quais recursos de toque incorporar e incentivar uma experiência de toque consistente entre Visual Studio produtos relacionados.

### <a name="levels-of-experience"></a>Níveis de experiência
 Os níveis de experiência a seguir destinam-se a servir como um guia para ajudar as equipes a decidir quais recursos de toque oferecer com base no nível desejado de interesse de investimento em contato.

- A **experiência básica é** para equipes que querem fornecer funcionalidades de toque para que não haja nenhum dead ends em todo o trabalho.

- A **experiência otimizada é** para equipes que querem fornecer as funcionalidades de toque mais comuns (por exemplo, aquelas normalmente disponíveis em aplicativos de navegador da Internet).

- A **experiência elevada é para** equipes que querem adicionar funcionalidades como gestos ou outros recursos opcionais que podem tornar seu aplicativo amigável.

||Experiência básica|Experiência otimizada|Experiência elevada|
|-|----------------------|--------------------------|-------------------------|
|**Permite que os usuários...**|Corrigir a leitura em nível de código e solução/projeto sem dead ends|Executar tarefas de manutenção, de refactors e de navegação|Operar em uma experiência consistente, intuitiva e fluida com confiança|
|**Editor**|Seleção e panorâmico de toque<br /><br /> Toque na barra de rolagem para pular e pressionar +arrastar|Zoom de pinçar<br /><br /> Rolagem rápida<br /><br /> Seleção<br /><br /> Fácil uso do menu de contexto||
|**Principais janelas de ferramentas**|Panorâmico de lista<br /><br /> Seleção de item<br /><br /> Toque na barra de rolagem para pular e pressionar +arrastar|Rolagem e seleção de itens fáceis||
|**Windowing**||Janela Resize<br /><br /> Acesso rápido||
|**Documentar bem**||Navegação fácil entre arquivos abertos||
|**Gestos**||Garantir que os gestos comuns funcionem no IDE|Ações baseadas em gesto<br /><br /> Suporte a designers e arrastar e soltar|
|**Outras considerações**|||Teclado na tela personalizado|

#### <a name="gestures"></a>Gestos
 Gestos fornecem aos usuários um atalho para comandos que, de outra forma, podem exigir uma interação mais complicada. Consulte as diretrizes do Windows sobre gestos de toque comuns para [aplicativos](/windows/desktop/wintouch/windows-touch-gestures-overview)da área de trabalho e siga estas diretrizes para a maioria dos gestos, incluindo gestos simples, como panorâmico e zoom.
