---
title: Imagens e ícones para Visual Studio | Microsoft Docs
description: Saiba mais sobre os conceitos de design usados para criar imagens e ícones para Visual Studio.
ms.date: 04/26/2017
ms.topic: reference
ms.assetid: f410325e-9cf2-4f39-b6d7-b672121c2691
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 36b77dc79574b1741c8feaded65104810e58c2fb
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898786"
---
# <a name="images-and-icons-for-visual-studio"></a>Imagens e ícones para o Visual Studio
## <a name="image-use-in-visual-studio"></a><a name="BKMK_ImageUseInVisualStudio"></a> Uso de imagem em Visual Studio
 Antes de criar a arte, considere usar as mais de 1.000 imagens na [biblioteca Visual Studio imagem.](https://www.microsoft.com/download/details.aspx?id=35825)

### <a name="types-of-images"></a>Tipos de imagens

- **Ícones**. Imagens pequenas que aparecem em comandos, hierarquias, modelos e assim por diante. O tamanho do ícone padrão usado Visual Studio é um PNG 16x16. Ícones produzidos pelo serviço de imagem geram automaticamente o formato XAML para suporte ao HDPI.

    > [!NOTE]
    > Embora as imagens sejam usadas no sistema de menus, você não deve criar um ícone para cada comando. Consulte [Menus e comandos para Visual Studio](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md) para ver se o comando deve obter um ícone.

- **Miniaturas.** Imagens usadas na área de visualização de uma caixa de diálogo, como a caixa de diálogo Novo Projeto.

- **Imagens de caixa de diálogo.** Imagens que aparecem em caixas de diálogo ou assistentes, como gráficos descritivos ou indicadores de mensagem. Use raramente e somente quando necessário para ilustrar um conceito difícil ou obter a atenção do usuário (alerta, aviso).

- **Imagens animadas.** Usado em indicadores de andamento, barras de status e caixas de diálogo de operação.

- **Cursores.** Usado para indicar se uma operação é permitida usando o mouse, em que um objeto pode ser descartado e assim por diante.

## <a name="icon-design"></a><a name="BKMK_IconDesign"></a> Design de ícone

### <a name="overview"></a>Visão geral
 Visual Studio usa ícones de estilo moderno, que têm geometria limpa e um saldo 50/50 de positivo/negativo (claro/escuro) e usam metáforas diretas e compreensíveis. Os pontos de design de ícone cruciais se centro em torno da clareza, da simplificação e do contexto.

- **Clareza:** concentre-se na metáfora principal que fornece a um ícone seu significado e individualidade.

- **Simplificação:** reduza o ícone para seu significado principal – obter o tema apenas com os elementos necessários e sem frills.

- **Contexto:** considere todos os aspectos da função de um ícone durante o desenvolvimento de conceitos, o que é crucial ao decidir quais elementos constituem a metáfora principal do ícone.

  Com ícones, há vários pontos de design a evitar:

- Não use ícones que significam elementos de interface do usuário, exceto quando apropriado. Escolha uma abordagem mais abstrata ou simbólica quando o elemento da interface do usuário não for comum, evidente nem exclusivo.

- Não superutilizar elementos comuns, como documentos, pastas, setas e lupa. Use esses elementos somente quando for essencial para o significado do ícone. Por exemplo, a lupa voltada para a direita deve indicar apenas Pesquisar, Procurar e Encontrar.

- Embora alguns elementos de ícone herdados mantenham o uso da perspectiva, não crie novos ícones com perspectiva, a menos que o elemento não tenha clareza sem ela.

- Não cram muitas informações em um ícone. Uma imagem simples que pode ser facilmente reconhecida ou aprendida como um símbolo reconhecível é muito mais útil do que uma imagem muito complexa. Um ícone não pode contar toda a história.

### <a name="icon-creation"></a>Criação de ícone

#### <a name="concept-development"></a>Desenvolvimento de conceito
 Visual Studio tem em sua interface do usuário uma ampla variedade de tipos de ícones. Considere cuidadosamente o tipo de ícone durante o desenvolvimento. Não use objetos de interface do usuário incertos ou incomuns para seus elementos de ícone. Opte pelo simbólico nesses casos, como com o ícone de Marca Inteligente. Observe que o significado da marca abstrata à esquerda é mais óbvio do que a versão baseada em interface do usuário à direita:

|**Uso correto de imagens simbólicas**|**Uso incorreto de imagens simbólicas**|
|-|-|
|![Ícone corrigir marcação inteligente](../../extensibility/ux-guidelines/media/0404-01_smarttagcorrect.png "0404-01_SmartTagCorrect")|![Ícone de Marca Inteligente Incorreta](../../extensibility/ux-guidelines/media/0404-02_smarttagincorrect.png "0404-02_SmartTagIncorrect")|

 Há instâncias em que elementos de interface do usuário padrão e facilmente reconhecíveis funcionam bem para ícones. Adicionar Janela é um exemplo:

|**Elemento de interface do usuário correto em um ícone**|**Elemento de interface do usuário incorreto em um ícone**|
|-|-|
|![Ícone Corrigir Adicionar Janela](../../extensibility/ux-guidelines/media/0404-03_addwindowcorrect.png "0404-03_AddWindowCorrect")|![Ícone adicionar janela incorreto](../../extensibility/ux-guidelines/media/0404-04_addwindowincorrect.png "0404-04_AddWindowIncorrect")|

 Não use um documento como um elemento base, a menos que ele seja essencial para o significado do ícone. Sem o elemento de documento em Adicionar Documento (abaixo), o significado é perdido, enquanto com Atualizar o elemento de documento é desnecessário para comunicar o significado.

|**Corrigir o uso do ícone de documento**|**Uso incorreto do ícone de documento**|
|-|-|
|![Ícone corrigir documento](../../extensibility/ux-guidelines/media/0404-05_documenticoncorrect.png "0404-05_DocumentIconCorrect")|![Ícone de documento incorreto](../../extensibility/ux-guidelines/media/0404-06_documenticonincorrect.png "0404-06_DocumentIconIncorrect")|

 O conceito de "mostrar" deve ser representado pelo ícone que melhor ilustra o que está sendo mostrado, como no exemplo Mostrar Todos os Arquivos. Uma metáfora de lente pode ser usada para indicar o conceito de "exibição", se necessário, como com o Modo de Exibição de Recursos exemplo.

|**"Mostrar"**|**"Exibir"**|
|-|-|
|![Ícone Mostrar](../../extensibility/ux-guidelines/media/0404-07_show.png "0404-07_Show")|![Ícone de exibição](../../extensibility/ux-guidelines/media/0404-08_view.png "0404-08_View")|

 O ícone de lupa voltado para a direita deve representar apenas Pesquisar, Encontrar e Procurar. A variante voltada para a esquerda com o sinal de adoção ou sinal de subtração deve representar apenas ampliar/reduzir.

|**"Pesquisar"**|**"Zoom"**|
|-|-|
|![Ícone de pesquisa](../../extensibility/ux-guidelines/media/0404-09_search.png "0404-09_Search")|![Ícone de zoom](../../extensibility/ux-guidelines/media/0404-10_zoom.png "0404-10_Zoom")|

 Em exibições de árvore, não use o ícone de pasta e um modificador. Quando disponível, use apenas o modificador .

|**Ícones de exibição de árvore corretos**|**Ícones de exibição de árvore incorretos**|
|-|-|
|![Ícone de exibição de árvore &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-11_treeviewcorrect1.png "0404-11_TreeViewCorrect1") Ícone de exibição de ![árvore correto &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-12_treeviewcorrect2.png "0404-12_TreeViewCorrect2")|![Ícone de exibição de árvore incorreto &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-13_treeviewincorrect1.png "0404-13_TreeViewIncorrect1") exibição de árvore ![incorreto &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-14_treeviewincorrect2.png "0404-14_TreeViewIncorrect2")|

### <a name="style-details"></a>Detalhes de estilo

#### <a name="layout"></a>Layout
 Elementos de pilha, conforme mostrado para ícones padrão 16x16:

 ![Pilha de layout para ícones 16x16](../../extensibility/ux-guidelines/media/0404-15_layoutstack.png "0404-15_LayoutStack")<br />Pilha de layout para ícones 16x16

 Os elementos de notificação de status são mais bem usados como ícones autônomos. No entanto, há contextos em que uma notificação deve ser empilhada no elemento base, como com o ícone Tarefa Concluída:

 ![Notificações autônomas no Visual Studio](../../extensibility/ux-guidelines/media/0404-16_standalonenotificationicons.png "0404-16_StandaloneNotificationIcons")<br />Ícones de notificação autônomos

 ![Ícone de conclusão da tarefa](../../extensibility/ux-guidelines/media/0404-17_taskcomplete.png "0404-17_TaskComplete")<br />Ícone De conclusão da tarefa

 Os ícones de projeto normalmente são arquivos .ico que contêm vários tamanhos. A maioria dos ícones 16x16 contém os mesmos elementos. As versões 32x32 têm mais detalhes, incluindo o tipo de projeto quando aplicável.

 ![Ícones de projeto no Visual Studio](../../extensibility/ux-guidelines/media/0404-18_iconprojectthreesizes.png "0404-18_IconProjectThreeSizes")<br />Ícones do Projeto da Biblioteca de Controle do Windows VB, 16x16 e 32x32

 Centralmente um ícone dentro de seu quadro de pixel. Se isso não for possível, alinhe o ícone à parte superior e/ou direita do quadro.

 ![Ícone centralizado dentro do quadro de pixel](../../extensibility/ux-guidelines/media/0404-19_iconcentered.png "0404-19_IconCentered")<br />Ícone centralizado dentro do quadro de pixel

 ![Ícone alinhado à parte superior direita do quadro de pixel](../../extensibility/ux-guidelines/media/0404-20_icontopright.png "0404-20_IconTopRight")<br />Ícone alinhado à parte superior direita do quadro

 ![Ícone centralizado e alinhado à parte superior do quadro do pixel](../../extensibility/ux-guidelines/media/0404-21_icontopalign.png "0404-21_IconTopAlign")<br />Ícone centralizado e alinhado à parte superior do quadro

 Para obter o alinhamento e o equilíbrio ideais, evite obstruir o elemento base do ícone com glifos de ação. Coloque o glifo próximo à parte superior esquerda do elemento base. Ao adicionar um elemento adicional, considere o alinhamento e o equilíbrio do ícone.

|**Corrigir alinhamento e saldo**|**Alinhamento e saldo incorretos**|
|-|-|
|![Corrigir o equilíbrio e o alinhamento dos ícones](../../extensibility/ux-guidelines/media/0404-22_alignbalancecorrect.png "0404-22_AlignBalanceCorrect")|![Saldo e alinhamento de ícone incorretos](../../extensibility/ux-guidelines/media/0404-23_alignbalanceincorrect.png "0404-23_AlignBalanceIncorrect")|

 Garanta a paridade de tamanho para ícones que compartilham elementos e são usados em conjuntos. Observe que, no emparelhamento incorreto, o círculo e a seta estão superdimensionados e não correspondem.

|**Paridade de tamanho correta**|**Paridade de tamanho incorreta**|
|-|-|
|![Tamanho e paridade corretos do ícone](../../extensibility/ux-guidelines/media/0404-24_sizeparitycorrect.png "0404-24_SizeParityCorrect")|![Tamanho e paridade de ícone incorretos](../../extensibility/ux-guidelines/media/0404-25_sizeparityincorrect.png "0404-25_SizeParityIncorrect")|

 Use linhas consistentes e pesos visuais. Avalie como o ícone que você está criando se compara a outros ícones usando uma comparação lado a lado. Nunca use o quadro 16x16 inteiro, use 15x15 ou menor. A proporção de negativo para positivo (escuro-para-claro) deve ser 50/50.

|**Corrigir a proporção de negativo para positivo**|**Taxa incorreta de negativo para positivo**|
|-|-|
|![Corrigir o peso Visual para os ícones &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-26_visualweightcorrect1.png "0404-26_VisualWeightCorrect1")<br /><br /> ![Corrigir o peso Visual para os ícones &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-27_visualweightcorrect2.png "0404-27_VisualWeightCorrect2")<br /><br /> ![Corrigir o peso visual dos ícones &#40;3&#41;](../../extensibility/ux-guidelines/media/0404-28_visualweightcorrect3.png "0404-28_VisualWeightCorrect3")|![Peso Visual incorreto para ícones](../../extensibility/ux-guidelines/media/0404-29_visualweightincorrect.png "0404-29_VisualWeightIncorrect")|

 Use formas simples e comparáveis e ângulos complementares para criar seus elementos sem sacrificar a integridade do elemento. Use ângulos de 45 ° ou 90 ° onde for possível.

 ![Corrigir ângulos do ícone](../../extensibility/ux-guidelines/media/0404-30_iconanglescorrect.png "0404-30_IconAnglesCorrect")

#### <a name="perspective"></a>Perspectiva
 Mantenha o ícone claro e compreensível. Use a perspectiva e uma fonte de luz somente quando necessário. Embora o uso da perspectiva em elementos Icon deva ser evitado, alguns elementos não podem ser reconhecidos sem ele. Nesses casos, uma perspectiva estilizada comunica a clareza do elemento.

 ![perspectiva de três pontos](../../extensibility/ux-guidelines/media/0404-31_3pointperspective.png "0404-31_3PointPerspective")<br />perspectiva de três pontos

 ![perspectiva de um ponto](../../extensibility/ux-guidelines/media/0404-32_1pointperspective.png "0404-32_1PointPerspective")<br />perspectiva de um ponto

 A maioria dos elementos deve ser oposta ou angular à direita:

 ![Ícones angulares à direita](../../extensibility/ux-guidelines/media/0404-33_angledright.png "0404-33_AngledRight")

 Use fontes de luz somente quando adicionar a clareza necessária a um objeto.

|**Fonte de luz correta**|**Fonte de luz incorreta**|
|-|-|
|![Corrigir fontes de luz para ícones](../../extensibility/ux-guidelines/media/0404-34_lightsourcescorrect.png "0404-34_LightSourcesCorrect")|![Fontes de luz incorretas para ícones](../../extensibility/ux-guidelines/media/0404-35_lightsourcesincorrect.png "0404-35_LightSourcesIncorrect")|

 Use contornos apenas para melhorar a legibilidade ou para comunicar melhor a metáfora. O saldo negativo positivo (escuro-claro) deve ser 50/50.

|**Corrigir o uso de contornos**|**Uso incorreto de contornos**|
|-|-|
|![Contornos corretos](../../extensibility/ux-guidelines/media/0404-36_outlinescorrect.png "0404-36_OutlinesCorrect")|![Contornos incorretos](../../extensibility/ux-guidelines/media/0404-37_outlinesincorrect.png "0404-37_OutlinesIncorrect")|

#### <a name="icon-types"></a>Tipos de ícone
 Os ícones de **shell e de barra de comandos** consistem em não mais do que três dos seguintes elementos: uma base, um modificador, uma ação ou um status.

 ![Exemplos de ícones de shell e de barra de comandos](../../extensibility/ux-guidelines/media/0404-38_shellicons.png "0404-38_ShellIcons")<br />Exemplos de ícones de shell e de barra de comandos

 Os ícones da **barra de comandos da janela de ferramentas** consistem em não mais do que três dos seguintes elementos: uma base, um modificador, uma ação ou um status.

 ![Exemplos de ícones da barra de comandos da janela de ferramentas](../../extensibility/ux-guidelines/media/0404-39_toolwindowcommandbaricons.png "0404-39_ToolWindowCommandBarIcons")<br />Exemplos de ícones da barra de comandos da janela de ferramentas

 Os ícones do **desambiguador de exibição de árvore** consistem em não mais do que três dos seguintes elementos: uma base, um modificador, uma ação ou um status.

 ![Exemplos de ícones de desambiguador de exibição de árvore](../../extensibility/ux-guidelines/media/0404-40_treeviewicons.png "0404-40_TreeViewIcons")<br />Exemplos de ícones de desambiguador de exibição de árvore

 Os ícones de **taxonomia de valor baseado em estado** existem nos seguintes Estados: ativo, ativo desabilitado e inativo desabilitado.

 ![Exemplos de ícones de taxonomia de valor baseado em estado](../../extensibility/ux-guidelines/media/0404-41_statebasedtaxonomy.png "0404-41_StateBasedTaxonomy")<br />Exemplos de ícones de taxonomia de valor baseado em estado

 Os ícones do **IntelliSense** consistem em não mais do que três dos seguintes elementos: uma base, um modificador e um status.

 ![Exemplos de ícones do IntelliSense](../../extensibility/ux-guidelines/media/0404-42_intellisenseicons.png "0404-42_IntelliSenseIcons")<br />Exemplos de ícones do IntelliSense

 Ícones de **projetos pequenos (16x16)** não devem ter mais do que dois elementos: uma base e um modificador.

 ![Exemplos de ícones de projeto pequenos (16x16) ícone de](../../extensibility/ux-guidelines/media/0404-43_16x16project1.png "0404-43_16x16Project1") projeto ![16x16 &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-44_16x16project2.png "0404-44_16x16Project2") ![ícone de projeto de 16x16 &#40;3&#41;](../../extensibility/ux-guidelines/media/0404-45_16x16project3.png "0404-45_16x16Project3")<br />Exemplos de ícones de projetos pequenos (16x16)

 Ícones de **projeto grandes (32x32)** consistem em não mais do que quatro dos seguintes elementos: uma base, um a dois modificadores e uma sobreposição de idioma.

 ![Exemplos de ícones de projeto grandes (32x32)](../../extensibility/ux-guidelines/media/0404-46_32x32project.png "0404-46_32x32Project")<br />Exemplos de ícones de projeto grandes (32x32)

### <a name="production-details"></a>Detalhes da produção
 Todos os novos elementos da interface do usuário devem ser criados usando Windows Presentation Foundation (WPF) e todos os novos ícones para o WPF devem estar no formato PNG de 32 bits. O PNG de 24 bits é um formato herdado que não dá suporte à transparência e, portanto, não é recomendado para ícones.

 Salve a resolução em 96 DPI.

#### <a name="file-types"></a>Tipos de arquivo

- **png de 32 bits:** o formato preferencial para ícones. Um formato de arquivo de compactação de dados sem perdas que pode armazenar uma única imagem rasterizada (pixel). os arquivos PNG de 32 bits dão suporte a transparência de canal alfa, correção gama e entrelaçamento.

- **bmp de 32 bits:** para controles que não são do WPF. Também chamado de XP ou High Color, o BMP de 32 bits é um formato de imagem RGB/A, uma imagem true-color com transparência de canal alfa. O canal alfa é uma camada de transparência designada no Adobe Photoshop que é salva no bitmap como um canal de cores adicional (quarto). Um plano de fundo preto é adicionado durante a produção do trabalho artístico a todos os arquivos BMP de 32 bits para fornecer uma indicação visual rápida sobre a intensidade de cor. Este plano de fundo preto representa a área a ser mascarada na interface do usuário.

- **32-bit ico:** para ícones de projeto e Adicionar item. Todos os arquivos ICO são cor true de 32 bits com transparência de canal alfa (RGB/A). Como os arquivos ICO podem armazenar vários tamanhos e profundidades de cores, os ícones do vista geralmente estão em um formato ICO contendo tamanhos de imagem 16x16, 32x32, 48x48 e 256x256. Para exibir corretamente no Windows Explorer, os arquivos ICO devem ser salvos em profundidade de cores de 24 e 8 bits para cada tamanho de imagem.

- **XAML:** para superfícies de design e adornos do Windows. Os ícones XAML são arquivos de imagem baseados em vetor que dão suporte ao dimensionamento, rotação, arquivamento e transparência. Eles não são comuns no Visual Studio hoje, mas estão se tornando mais populares devido à sua flexibilidade.

- **SVG**

- **bmp de 24 bits:** para a barra de comandos do Visual Studio. Um formato de imagem RGB true-color, BMP de 24 bits, é uma Convenção de ícones que cria uma camada de transparência usando magenta (R = 255, G = 0, B = 255) como uma chave de cor para uma camada de transparência vazada. Em um BMP de 24 bits, todas as superfícies magenta são exibidas usando a cor do plano de fundo.

- **GIF de 24 bits:** para a barra de comandos do Visual Studio. Um formato de imagem RGB True-Color que dá suporte à transparência. Os arquivos GIF costumam ser usados em animações de arte do assistente e GIF.

### <a name="icon-construction"></a>Construção de ícone
 O menor tamanho do ícone no Visual Studio é 16x16. O maior em uso comum é 32x32. Lembre-se de não preencher todo o quadro 16x16, 24x24 ou 32x32 ao criar um ícone. A construção de ícone uniforme e legível é essencial para o reconhecimento do usuário. Adera aos pontos a seguir ao criar ícones.

- Os ícones devem ser claros, compreensíveis e consistentes.

- É melhor usar os elementos de notificação de status como ícones individuais e não empilha-los sobre um elemento base de ícone. Em determinados contextos, a interface do usuário pode exigir que o elemento de status seja emparelhado com um elemento base.

- Ícones de projeto geralmente são arquivos .ico que contêm vários tamanhos. Somente os ícones 16x16, 24x24 e 32x32 estão sendo atualizados. A maioria dos ícones 16x16 e 24x24 conterá os mesmos elementos. Os ícones 32x32 contêm mais detalhes, incluindo o tipo de linguagem de projeto quando aplicável.

- Para ícones 32x32, os elementos base geralmente têm um peso de linha de 2 pixels. Um peso de linha de 1 ou 2 pixels pode ser usado para elementos de detalhes. Use seu melhor julgamento para determinar qual é mais adequado.

- Ter pelo menos um espaçamento de 1 pixel entre elementos para ícones 16x16 e 24x24. Para ícones 32x32, use o espaçamento de 2 pixels entre elementos e entre o modificador e o elemento base.

  ![Espaçamento de elemento para ícones dimensionado 16x16, 24x24 e 32x32](../../extensibility/ux-guidelines/media/0404-47_elementspacing.png "0404-47_ElementSpacing")<br />Espaçamento de elemento para ícones dimensionado 16x16, 24x24 e 32x32

#### <a name="color-and-accessibility"></a>Cor e acessibilidade
 Visual Studio de conformidade exigem que todos os ícones no produto passem os requisitos de acessibilidade para cor e contraste. Isso é feito por meio da inversão de ícone e, quando você estiver projetando, deve estar ciente de que eles serão invertidos programaticamente no produto.

 Para obter mais informações sobre como usar cores Visual Studio ícones, consulte [Usando cor em imagens](../../extensibility/ux-guidelines/images-and-icons-for-visual-studio.md#BKMK_UsingColorInImages).

## <a name="using-color-in-images"></a><a name="BKMK_UsingColorInImages"></a> Usando cor em imagens

### <a name="overview"></a>Visão geral
 Os ícones Visual Studio são principalmente monocromáticos. A cor é reservada para transmitir informações específicas e nunca para decoração. A cor é usada:

- para indicar uma ação

- para alertar o usuário sobre uma notificação de status

- para designar a afiliação de idioma

- para diferenciar itens no IntelliSense

### <a name="accessibility"></a>Acessibilidade
 Visual Studio de conformidade exigem que todos os ícones verificados no produto passem os requisitos de acessibilidade para cor e contraste. As cores na paleta de linguagem visual foram testadas e atendem a esses requisitos.

#### <a name="color-inversion-for-dark-themes"></a>Inversão de cor para temas escuros
 Para fazer com que os ícones apareçam com a taxa de contraste correta no Visual Studio escuro, uma inversão é aplicada programaticamente. As cores neste guia foram escolhidas em parte para que elas invertam corretamente. Restrinja o uso de cores a essa paleta ou você obterá resultados imprevisíveis quando a inversão for aplicada.

 ![Exemplos de ícones que tiveram suas cores invertidas](../../extensibility/ux-guidelines/media/0405-01_darkthemeinversion.png "0405-01_DarkThemeInversion")<br />Exemplos de ícones que tiveram suas cores invertidas

### <a name="base-palette"></a>Paleta base
 Todos os ícones padrão contêm três cores base. Os ícones não contêm gradientes nem sombras, com uma ou duas exceções para ícones de ferramenta 3D.

|Uso|Nome|Valor (tema claro)|Swatch|Exemplo|
|-----------|----------|---------------------------|------------|-------------|
|Plano de fundo/escuro|VS BG|424242 / 66,66,66|![Swatch 424242](../../extensibility/ux-guidelines/media/0405_424242.png "0405_424242")|![Exemplo de paleta base](../../extensibility/ux-guidelines/media/0405-02_basepaletteexample.png "0405-02_BasePaletteExample")|
|Primeiro plano/luz|VS FG|F0EFF1 / 240.239.241|![Swatch F0EFF1](../../extensibility/ux-guidelines/media/0405_f0eff1.png "0405_F0EFF1")||
|Contorno|VS Out|F6F6F6 / 246.246.246|![Swatch F6F6F6](../../extensibility/ux-guidelines/media/0405_f6f6f6.png "0405_F6F6F6")||

 Além das cores base, cada ícone pode conter uma cor adicional da paleta estendida.

### <a name="extended-palette"></a>Paleta estendida

#### <a name="action-modifiers"></a>Modificadores de ação
 As quatro cores abaixo indicam os tipos de ações exigidas pelos modificadores de ação:

|Uso|Nome|Valor (todos os temas)|Swatch|
|-----------|----------|--------------------------|------------|
|Positivo|Verde da Ação do VS|388A34 / 56.138,52|![Swatch 388A34](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|Negativo|VS Action Red|A1260D /161,38,13|![Swatch A1260D](../../extensibility/ux-guidelines/media/0405_a1260d.png "0405_A1260D")|
|Neutro|Ação do VS azul|00539C / 0,83.156|![Swatch 00539C](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|Criar/Novo|VS Action Orange|C27D1A / 194.156,26|![Swatch C27D1A](../../extensibility/ux-guidelines/media/0405_c27d1a.png "0405_C27D1A")|

##### <a name="examples"></a>Exemplos
 Verde é usado para modificadores de ação positivos, como "Adicionar", "Executar", "Reproduzir" e "Validar".

|Executar|Executar consulta|Reproduzir todas as etapas|Adicionar controle|
|-|-|-|-|
|![Ícone executar](../../extensibility/ux-guidelines/media/0405-03_actionmodifierrun.png "0405-03_ActionModifierRun")|![Ícone Executar consulta](../../extensibility/ux-guidelines/media/0405-04_executequery.png "0405-04_ExecuteQuery")|![Ícone Reproduzir todas as etapas](../../extensibility/ux-guidelines/media/0405-05_playallsteps.png "0405-05_PlayAllSteps")|![Ícone Adicionar controle](../../extensibility/ux-guidelines/media/0405-06_addcontrol.png "0405-06_AddControl")|

 Vermelho é usado para modificadores de ação negativos, como "Excluir", "Parar", "Cancelar" e "Fechar".

|Excluir Relação|Excluir Coluna|Parar consulta|Conexão offline|
|-|-|-|-|
|![Ícone Excluir relação](../../extensibility/ux-guidelines/media/0405-07_deleterelationship.png "0405-07_DeleteRelationship")|![Ícone Excluir coluna](../../extensibility/ux-guidelines/media/0405-08_deletecolumn.png "0405-08_DeleteColumn")|![Ícone de consulta de parada](../../extensibility/ux-guidelines/media/0405-09_stopquery.png "0405-09_StopQuery")|![Ícone de conexão offline](../../extensibility/ux-guidelines/media/0405-10_connectionoffline.png "0405-10_ConnectionOffline")|

 O azul é aplicado aos modificadores de ação neutros mais comumente representados como setas, como "abrir", "Avançar", "anterior", "importar" e "exportar".

|Ir para o campo|Check-In em lote|Editor de endereço|Editor de associação|
|-|-|-|-|
|![Ir para o ícone de campo](../../extensibility/ux-guidelines/media/0405-11_gotofield.png "0405-11_GoToField")|![&#45;de verificação em lote no ícone](../../extensibility/ux-guidelines/media/0405-12_batchedcheckin.png "0405-12_BatchedCheckIn")|![Ícone do editor de endereços](../../extensibility/ux-guidelines/media/0405-13_addresseditor.png "0405-13_AddressEditor")|![Ícone do editor de associação](../../extensibility/ux-guidelines/media/0405-14_associationeditor.png "0405-14_AssociationEditor")|

 O Gold escuro é usado principalmente para o modificador "New".

|Novo Projeto|Criar novo grafo|Novo teste de unidade|Novo item de lista|
|-|-|-|-|
|![Ícone de novo projeto](../../extensibility/ux-guidelines/media/0405-15_newproject.png "0405-15_NewProject")|![Ícone criar novo grafo](../../extensibility/ux-guidelines/media/0405-16_createnewgraph.png "0405-16_CreateNewGraph")|![Ícone de novo teste de unidade](../../extensibility/ux-guidelines/media/0405-17_newunittest.png "0405-17_NewUnitTest")|![Ícone de novo item de lista](../../extensibility/ux-guidelines/media/0405-18_newlistitem.png "0405-18_NewListItem")|

#### <a name="special-cases"></a>Casos especiais
 Em casos especiais, um modificador de ação colorida pode ser usado independentemente como um ícone autônomo. A cor usada para o ícone reflete as ações com as quais o ícone está associado. Esse uso é limitado a um pequeno subconjunto de ícones, incluindo:

|Executar|Stop|Excluir|Salvar|Navegação Regressiva|
|-|-|-|-|-|
|![Ícone de execução](../../extensibility/ux-guidelines/media/0405-03_actionmodifierrun.png "0405-03_ActionModifierRun")|![Ícone de parada – quadrado vermelho sólido.](../../extensibility/ux-guidelines/media/0405-19_stop.png "0405-19_Stop")|![Ícone excluir](../../extensibility/ux-guidelines/media/0405-20_delete.png "0405-20_Delete")|![Ícone Salvar](../../extensibility/ux-guidelines/media/0405-21_save.png "0405-21_Save")|![Ícone navegar para trás](../../extensibility/ux-guidelines/media/0405-22_navigateback.png "0405-22_NavigateBack")|

### <a name="code-hierarchy-palette"></a>Paleta de hierarquia de código

#### <a name="folder"></a>Pasta

|Uso|Nome|Valor (todos os temas)|Essas|Exemplo|
|-----------|----------|--------------------------|------------|-------------|
|Pastas|Pasta|DCB67A/220.182.122|![DCB67A de amostra](../../extensibility/ux-guidelines/media/0405_dcb67a.png "0405_DCB67A")|![Ícone de cor da pasta](../../extensibility/ux-guidelines/media/0405-23_foldercolor.png "0405-23_FolderColor")|

#### <a name="visual-studio-languages"></a>Linguagens do Visual Studio
 Cada um dos idiomas ou plataformas comuns disponíveis no Visual Studio tem uma cor associada. Essas cores são usadas no ícone base ou em modificadores de idioma que aparecem no canto superior direito dos ícones compostos.

|Uso|Nome|Valor (todos os temas)|Essas|
|-----------|----------|--------------------------|------------|
|ASP, HTML, WPF|HTML ASP WPF azul|0095D7/0149.215|![0095D7 de amostra](../../extensibility/ux-guidelines/media/0405_0096d7.png "0405_0096D7")|
|C++|CPP roxo|9B4F96/155, 79150|![9B4F96 de amostra](../../extensibility/ux-guidelines/media/0405_9b4f96.png "0405_9B4F96")|
|C#|CS verde (VS ação verde)|388A34/56138, 52|![388A34 de amostra](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|CSS|CSS vermelho|BD1E2D/189, 30, 45|![BD1E2D de amostra](../../extensibility/ux-guidelines/media/0405_bd1e2d.png "0405_BD1E2D")|
|F#|Roxo de FS|672878/103, 40120|![Amostra 672878](../../extensibility/ux-guidelines/media/0405_672878.png "0405_672878")|
|JavaScript|Laranja do JS|F16421/241100, 33|![F16421 de amostra](../../extensibility/ux-guidelines/media/0405_f16421.png "0405_F16421")|
|VB|VB azul (VS Action azul)|00539C/0, 83156|![00539C de amostra](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|TypeScript|Orange do TS|E04C06/224, 76, 6|![E04C06 de amostra](../../extensibility/ux-guidelines/media/0405_e04c06.png "0405_E04C06")|
|Python|AJ por verde|879636/135150, 54|![Amostra 879636](../../extensibility/ux-guidelines/media/0405_879636.png "0405_879636")|

##### <a name="examples-of-icons-with-language-modifiers"></a>Exemplos de ícones com modificadores de idioma

|VB|C#|C++|F#|JavaScript|Python|
|-|-|-|-|-|-|
|![Visual Basic ícone](../../extensibility/ux-guidelines/media/0405-25_vb.png "0405-25_VB")|![Ícone&#35; C](../../extensibility/ux-guidelines/media/0405-26_csharp.png "0405-26_CSharp")|![Ícone&#43;&#43; C](../../extensibility/ux-guidelines/media/0405-27_cplusplus.png "0405-27_CPlusPlus")|![Ícone&#35; F](../../extensibility/ux-guidelines/media/0405-28_fsharp.png "0405-28_FSharp")|![Ícone de JavaScript](../../extensibility/ux-guidelines/media/0405-29_javascript.png "0405-29_JavaScript")|![Ícone do Python](../../extensibility/ux-guidelines/media/0405-30_python.png "0405-30_Python")|

|HTML|WPF|ASP|CSS|TypeScript|
|-|-|-|-|-|
|![Ícone HTML](../../extensibility/ux-guidelines/media/0405-31_html.png "0405-31_HTML")<br />HTML|![Ícone do WPF](../../extensibility/ux-guidelines/media/0405-32_wpf.png "0405-32_WPF")<br />WPF|![Ícone do ASP](../../extensibility/ux-guidelines/media/0405-33_asp.png "0405-33_ASP")<br />ASP|![Ícone de CSS](../../extensibility/ux-guidelines/media/0405-34_css.png "0405-34_CSS")<br />CSS|![Ícone typeScript](../../extensibility/ux-guidelines/media/0405-35_typescript.png "0405-35_TypeScript")<br />TypeScript|

#### <a name="intellisense"></a>IntelliSense
 Os ícones do IntelliSense usam uma paleta de cores exclusiva. Essas cores são usadas para ajudar os usuários a distinguir rapidamente entre os diferentes itens na lista pop-up do IntelliSense.

|Uso|Nome|Valor (todos os temas)|Swatch|
|-----------|----------|--------------------------|------------|
|Classe, Evento|VS Action Orange|C27D1A /194.125,26|![Swatch C27D1A](../../extensibility/ux-guidelines/media/0405_c27d1a.png "0405_C27D1A")|
|Método de extensão, método, módulo, delegado|Ação vs roxo|652D90 /101.45.144|![Swatch 652D90](../../extensibility/ux-guidelines/media/0405_652d90.png "0405_652D90")|
|Campo, Item de Enum, Macro, Estrutura, Tipo de Valor de União, Operador, Interface|Ação do VS azul|00539C / 0,83.156|![Swatch 00539C](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|Objeto|Verde da Ação do VS|388A34 / 56.138,52|![Swatch 388A34](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|Constant, Exception, Enum Item, Map, Map Item, Namespace, Template, Type Definition|Background (VS BG)|424242 / 66,66,66|![Swatch 424242](../../extensibility/ux-guidelines/media/0405_424242.png "0405_424242")|

##### <a name="examples-of-intellisense-icons"></a>Exemplos de ícones do IntelliSense

|Classe|Evento privado|Delegar|Método Friend|Campo|
|-|-|-|-|-|
|![Ícone de classe do IntelliSense](../../extensibility/ux-guidelines/media/0405-36_intellisenseclass.png "0405-36_IntelliSenseClass")|![Ícone de evento privado do IntelliSense](../../extensibility/ux-guidelines/media/0405-37_intellisenseprivateevent.png "0405-37_IntelliSensePrivateEvent")|![Ícone de delegado do IntelliSense](../../extensibility/ux-guidelines/media/0405-38_intellisensedelegate.png "0405-38_IntelliSenseDelegate")|![Ícone de amigo do método IntelliSense](../../extensibility/ux-guidelines/media/0405-39_intellisensemethodfriend.png "0405-39_IntelliSenseMethodFriend")|![Ícone de campo](../../extensibility/ux-guidelines/media/0405-40_field.png "0405-40_Field")|

|Item de enum protegido|Objeto|Modelo|Atalho de exceção|
|-|-|-|-|
|![Ícone de item de enum protegido pelo IntelliSense](../../extensibility/ux-guidelines/media/0405-41_intellisenseprotectedenumitem.png "0405-41_IntelliSenseProtectedEnumItem")|![Ícone de objeto do IntelliSense](../../extensibility/ux-guidelines/media/0405-42_intellisenseobject.png "0405-42_IntelliSenseObject")|![Ícone de modelo do IntelliSense](../../extensibility/ux-guidelines/media/0405-43_intellisensetemplate.png "0405-43_IntelliSenseTemplate")|![Ícone de atalho de exceção do IntelliSense](../../extensibility/ux-guidelines/media/0405-44_intellisenseexceptionshortcut.png "0405-44_IntelliSenseExceptionShortcut")|

### <a name="notifications"></a>Notificações
 As notificações no Visual Studio são usadas para indicar o status. A paleta de notificação usa as quatro cores a seguir, bem como as opções de preenchimento em primeiro plano preto ou branco, para definir notificações com os seguintes níveis de status.

|Uso|Nome|Valor (todos os temas)|Swatch|
|-----------|----------|--------------------------|------------|
|Status: neutro|Notificação azul (VS Blue)|1BA1E2 /27.161.226|![Swatch 1BA1E2](../../extensibility/ux-guidelines/media/0405_1ba1e2.png "0405_1BA1E2")|
|Status: positivo|Verde da notificação (VS Verde)|339933 / 51,153,51|![Swatch 339933](../../extensibility/ux-guidelines/media/0405_339933.png "0405_339933")|
|Status: negativo|Notificação vermelha (VS Vermelho)|E51400/229,20,0|![Swatch E51400](../../extensibility/ux-guidelines/media/0405_e51400.png "0405_E51400")|
|Status: aviso|Amarelo de Notificação (VS Orange)|FFCC00 / 255.204,0|![Swatch FFCC00](../../extensibility/ux-guidelines/media/0405_ffcc00.png "0405_FFCC00")|
|Preenchimento em primeiro plano|Notificação preta (preto)|000000 / 0,0,0|![Swatch &#35;000000](../../extensibility/ux-guidelines/media/0405_000000.png "0405_000000")|
|Preenchimento em primeiro plano|Notificação em branco (branco)|FFFFFF /255.255.255|![Swatch FFFFFF](../../extensibility/ux-guidelines/media/0405_ffffff.png "0405_FFFFFF")|

#### <a name="examples-of-notification-icons"></a>Exemplos de ícones de notificação

|Alerta|Aviso|Concluir|Stop|
|-|-|-|-|
|![Ícone de alerta](../../extensibility/ux-guidelines/media/0405-45_alert.png "0405-45_Alert")|![Ícone de aviso:](../../extensibility/ux-guidelines/media/0405-48_warning.png "0405-48_Warning")|![Ícone completo](../../extensibility/ux-guidelines/media/0405-46_complete.png "0405-46_Complete")|![Ícone de parada – círculo vermelho sólido com um quadrado branco no centro.](../../extensibility/ux-guidelines/media/0405-47_stop.png "0405-47_Stop")|