---
title: Imagens e ícones para o Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f410325e-9cf2-4f39-b6d7-b672121c2691
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 4ab668678a0ec867112f461b7978962d941bcdc8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51749180"
---
# <a name="images-and-icons-for-visual-studio"></a>Imagens e ícones para o Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

##  <a name="BKMK_ImageUseInVisualStudio"></a> Uso de imagens no Visual Studio  
 Antes de criar a arte final, considere fazer uso de mais de 1.000 imagens na [biblioteca de imagens do Visual Studio](http://www.microsoft.com/en-my/download/details.aspx?id=35825).  
  
### <a name="types-of-images"></a>Tipos de imagens  
  
-   **Ícones**. Imagens pequenas que aparecem nos comandos, hierarquias, modelos e assim por diante. O tamanho do ícone padrão usado no Visual Studio é um arquivo PNG de 16 x 16. Ícones produzidas pelo serviço de imagem automaticamente geram o formato XAML para suporte ao HDPI.  
  
     **Observação:** enquanto imagens são usadas no sistema de menu, você não deve criar um ícone para cada comando. Consultar [Menus e comandos para o Visual Studio](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md) para ver se o comando deve obter um ícone.  
  
-   **Miniaturas.** Imagens usadas na área de visualização da caixa de diálogo, como a caixa de diálogo Novo projeto.  
  
-   **Imagens de caixa de diálogo.** Imagens que aparecem em caixas de diálogo ou assistentes, como gráficos descritivos ou indicadores de mensagem. Use com pouca frequência e somente quando necessário para ilustrar um conceito difícil ou obter a atenção do usuário (aviso de alerta,).  
  
-   **Imagens animadas.** Usado em caixas de diálogo de operação, barras de status e indicadores de progresso.  
  
-   **Cursores.** Usado para indicar se uma operação é permitida usar o mouse, em que um objeto pode ser descartado e assim por diante.  
  
##  <a name="BKMK_IconDesign"></a> Design de ícone  
  
### <a name="overview"></a>Visão geral  
 O Visual Studio usa ícones de estilo moderno, que têm geometria limpa e um equilíbrio 50/50 positivos/negativos (claro/escuro) e usam metáforas diretas e legível. Design de ícone crucial pontos giram em torno de clareza, simplificação e contexto.  
  
- **Maior clareza:** enfocar a metáfora de núcleo que fornece um ícone de seu significado e individualidade.  
  
- **Simplificação:** reduzir o ícone para seu significado core – Obtenha o tema com elementos necessários e sem sofisticações.  
  
- **Contexto:** considerar todos os aspectos da função de um ícone durante o desenvolvimento de conceito, que é essencial ao decidir quais elementos constituem a metáfora de núcleo do ícone.  
  
  Com ícones, há um número de pontos de design para evitar:  
  
- Não use os ícones que significam os elementos de interface do usuário, exceto quando apropriado. Escolha uma abordagem mais abstrata ou simbólica quando o elemento de interface do usuário não é comum, evidente, nem exclusivo.  
  
- Não uso excessivo de elementos comuns, como documentos, pastas, setas e Lupa. Use esses elementos apenas quando essencial para o significado do ícone. Por exemplo, na lupa para a direita deve indicar somente pesquisar, procurar e localizar.  
  
- Embora alguns elementos de ícone herdado mantém o uso da perspectiva, não crie novos ícones com perspectiva, a menos que o elemento não tem a maior clareza sem ele.  
  
- Não espremer muitas informações em um ícone. Uma imagem simples que pode ser facilmente reconhecida ou aprendeu como um símbolo reconhecível é muito mais úteis do que uma imagem excessivamente complexa. Um ícone não pode contar a história inteira.  
  
### <a name="icon-creation"></a>Criação de ícone  
  
#### <a name="concept-development"></a>Desenvolvimento do conceito  
 Visual Studio tem dentro de sua interface do usuário uma ampla variedade de tipos de ícones. Considere cuidadosamente o tipo de ícone durante o desenvolvimento. Não use objetos de interface do usuário não está claras ou incomuns para elementos de ícone. Optar pelo simbólico nesses casos, como com o ícone de marca inteligente. Observe que o significado da marca abstrata à esquerda é mais evidente que a versão de vaga, baseada em interface do usuário, à direita:  
  
|||  
|-|-|  
|**Uso correto de imagens simbólico**|**Uso incorreto de imagens simbólico**|  
|![Ícone de marca inteligente correto](../../extensibility/ux-guidelines/media/0404-01-smarttagcorrect.png "01_SmartTagCorrect 0404")|![Ícone de marca inteligente incorreto](../../extensibility/ux-guidelines/media/0404-02-smarttagincorrect.png "02_SmartTagIncorrect 0404")|  
  
 Há instâncias em que os elementos de interface do usuário padrão, facilmente reconhecíveis funcionam bem para ícones. Adicione que janela é um exemplo:  
  
|||  
|-|-|  
|**Elemento de interface do usuário correto em um ícone**|**Elemento de interface do usuário incorreto em um ícone**|  
|![Ícone de janela Adicionar correto](../../extensibility/ux-guidelines/media/0404-03-addwindowcorrect.png "03_AddWindowCorrect 0404")|![Ícone de janela Adicionar incorreto](../../extensibility/ux-guidelines/media/0404-04-addwindowincorrect.png "04_AddWindowIncorrect 0404")|  
  
 Não use um documento como um elemento base, a menos que ele é essencial para o significado do ícone. Sem o documento for perdido, o elemento no documento de adicionar (o significado abaixo), enquanto com a atualização o elemento do documento é desnecessário para se comunicar o significado.  
  
|||  
|-|-|  
|**Uso correto de ícone do documento**|**Uso incorreto do ícone do documento**|  
|![Ícone de documento correto](../../extensibility/ux-guidelines/media/0404-05-documenticoncorrect.png "05_DocumentIconCorrect 0404")|![Ícone de documento incorreto](../../extensibility/ux-guidelines/media/0404-06-documenticonincorrect.png "06_DocumentIconIncorrect 0404")|  
  
 O conceito de "Mostrar" deve ser representado pelo ícone que ilustra melhor o que está sendo mostrado, tal como ocorre com o exemplo de mostrar todos os arquivos. Uma metáfora de Lente pode ser usada para indicar o conceito de "view", se necessário, como no exemplo de exibição de recurso.  
  
|||  
|-|-|  
|**"Mostrar"**|**"View"**|  
|![Mostrar ícone](../../extensibility/ux-guidelines/media/0404-07-show.png "07_Show 0404")|![Ícone do modo de exibição](../../extensibility/ux-guidelines/media/0404-08-view.png "08_View 0404")|  
  
 O para a direita ampliando o ícone de lupa deve representam apenas pesquisar, localizar e procurar. A variante voltado para a esquerda com o sinal de subtração ou sinal de adição deve representar somente zoom em / reduzir.  
  
|||  
|-|-|  
|**"Pesquisar"**|**"Ampliar"**|  
|![Ícone de pesquisa](../../extensibility/ux-guidelines/media/0404-09-search.png "09_Search 0404")|![Ícone de zoom](../../extensibility/ux-guidelines/media/0404-10-zoom.png "10_Zoom 0404")|  
  
 Nos modos de exibição de árvore, não use o ícone de pasta e um modificador. Quando estiverem disponíveis, use somente o modificador.  
  
|||  
|-|-|  
|**Ícones de modo de exibição de árvore correta**|**Ícones de modo de exibição de árvore incorreto**|  
|![Ícone do modo de exibição de árvore correta &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-11-treeviewcorrect1.png "0404 11_TreeViewCorrect1") ![ícone do modo de exibição de árvore correta &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-12-treeviewcorrect2.png "12_TreeViewCorrect2 0404")|![Ícone do modo de exibição de árvore incorreto &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-13-treeviewincorrect1.png "0404 13_TreeViewIncorrect1") ![ícone do modo de exibição de árvore incorreto &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-14-treeviewincorrect2.png "14_ 0404 TreeViewIncorrect2")|  
  
### <a name="style-details"></a>Detalhes de estilo  
  
#### <a name="layout"></a>Layout  
 Elementos da pilha conforme mostrado para os ícones de 16 x 16 padrão:  
  
 ![Pilha de layout para os ícones de 16 x 16](../../extensibility/ux-guidelines/media/0404-15-layoutstack.png "15_LayoutStack 0404")  
  
 **Pilha de layout para os ícones de 16 x 16**  
  
 Elementos de notificação de status são mais usados como ícones autônomo. Há contextos, no entanto, no qual uma notificação deve empilhada em elemento base, como com o ícone de tarefa concluída:  
  
 ![Notificações de autônomo no Visual Studio](../../extensibility/ux-guidelines/media/0404-16-standalonenotificationicons.png "16_StandaloneNotificationIcons 0404")  
  
 **Ícones de notificação autônomo**  
  
 ![Ícone da tarefa concluída](../../extensibility/ux-guidelines/media/0404-17-taskcomplete.png "17_TaskComplete 0404")  
  
 **Ícone da tarefa concluída**  
  
 Ícones de projeto normalmente são arquivos. ico que contêm vários tamanhos. A maioria dos ícones de 16 x 16 contêm os mesmos elementos. As versões de 32 x 32 têm mais detalhes, incluindo o tipo de projeto, quando aplicável.  
  
 ![Projeto ícones no Visual Studio](../../extensibility/ux-guidelines/media/0404-18-iconprojectthreesizes.png "18_IconProjectThreeSizes 0404")  
  
 **Ícones de projeto de biblioteca de controle de Windows do VB, 16 x 16 e 32 x 32**  
  
 Centro de um ícone dentro do quadro pixel. Se isso não é possível alinhe o ícone na parte superior e/ou à direita do quadro.  
  
 ![Ícone centralizado dentro do quadro de pixel](../../extensibility/ux-guidelines/media/0404-19-iconcentered.png "19_IconCentered 0404")  
  
 **Ícone centralizado dentro do quadro de pixel**  
  
 ![Ícone alinhado à parte superior direita do quadro de pixel](../../extensibility/ux-guidelines/media/0404-20-icontopright.png "20_IconTopRight 0404")  
  
 **Ícone alinhado na parte superior direita do quadro**  
  
 ![Ícone centralizada e alinhado à parte superior do quadro de pixel](../../extensibility/ux-guidelines/media/0404-21-icontopalign.png "21_IconTopAlign 0404")  
  
 **Ícone centralizada e alinhado à parte superior do quadro**  
  
 Para obter o saldo e o alinhamento ideal, evite obstruindo o elemento de base do ícone com os glifos de ação. Coloque o glifo na parte superior esquerdo do elemento base. Ao adicionar um elemento adicional, considere o alinhamento e o saldo do ícone.  
  
|||  
|-|-|  
|**Saldo e o alinhamento correto**|**Saldo e o alinhamento incorreto**|  
|![Corrija o saldo de ícone e o alinhamento](../../extensibility/ux-guidelines/media/0404-22-alignbalancecorrect.png "22_AlignBalanceCorrect 0404")|![Saldo de ícone incorreto e alinhamento](../../extensibility/ux-guidelines/media/0404-23-alignbalanceincorrect.png "23_AlignBalanceIncorrect 0404")|  
  
 Certifique-se de paridade de tamanho para os ícones que compartilham elementos e são usados em conjuntos. Observe que no emparelhamento incorreto, a seta e círculo forem muito grandes e não são correspondentes.  
  
|||  
|-|-|  
|**Paridade de tamanho correto**|**Paridade de tamanho incorreto**|  
|![Corrigir o tamanho do ícone e paridade](../../extensibility/ux-guidelines/media/0404-24-sizeparitycorrect.png "24_SizeParityCorrect 0404")|![Tamanho do ícone incorreto e paridade](../../extensibility/ux-guidelines/media/0404-25-sizeparityincorrect.png "25_SizeParityIncorrect 0404")|  
  
 Use pesos visual e linha consistentes. Avalie como o ícone que você está criando se compara com outros ícones usando uma comparação lado a lado. Nunca use todo o quadro de 16 x 16, use 15 x 15 ou menores. A taxa de (escuro para claro) negativo ao positivo deve ser 50/50.  
  
|||  
|-|-|  
|**Taxa de negativo ao positivo correta**|**Taxa de negativo ao positivo incorreta**|  
|![Corrija o peso visual para ícones &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-26-visualweightcorrect1.png "26_VisualWeightCorrect1 0404")<br /><br /> ![Corrija o peso visual para ícones &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-27-visualweightcorrect2.png "27_VisualWeightCorrect2 0404")<br /><br /> ![Corrija o peso visual para ícones &#40;3&#41;](../../extensibility/ux-guidelines/media/0404-28-visualweightcorrect3.png "28_VisualWeightCorrect3 0404")|![Peso incorreto de visual para ícones](../../extensibility/ux-guidelines/media/0404-29-visualweightincorrect.png "29_VisualWeightIncorrect 0404")|  
  
 Use formas simples, comparáveis e ângulos complementares para criar seus elementos sem sacrificar a integridade do elemento. Use os ângulos de 45° ou 90° sempre que possível.  
  
 ![Corrija os ângulos de ícone](../../extensibility/ux-guidelines/media/0404-30-iconanglescorrect.png "30_IconAnglesCorrect 0404")  
  
#### <a name="perspective"></a>Perspectiva  
 Mantenha o ícone claro e compreensível. Perspectiva de uso e uma fonte de luz somente quando necessário. Embora usando a perspectiva em elementos de ícone deve ser evitado, alguns elementos são irreconhecíveis sem ele. Nesses casos, uma perspectiva estilizada se comunica a clareza do elemento.  
  
 ![3&#45;ponto de Vista](../../extensibility/ux-guidelines/media/0404-31-3pointperspective.png "31_3PointPerspective 0404")  
  
 **perspectiva de ponto de 3**  
  
 ![1&#45;ponto de Vista](../../extensibility/ux-guidelines/media/0404-32-1pointperspective.png "32_1PointPerspective 0404")  
  
 **1 ponto perspectiva**  
  
 A maioria dos elementos deve ser voltado para a ou diagonal à direita.  
  
 ![Ícones de direito angular](../../extensibility/ux-guidelines/media/0404-33-angledright.png "33_AngledRight 0404")  
  
 Use fontes de luz somente quando adicionando clareza necessária a um objeto.  
  
|||  
|-|-|  
|**Fonte de luz correto**|**Fonte de luz incorreto**|  
|![Corrija as fontes de luz para ícones](../../extensibility/ux-guidelines/media/0404-34-lightsourcescorrect.png "34_LightSourcesCorrect 0404")|![Fontes de luz incorretos para ícones](../../extensibility/ux-guidelines/media/0404-35-lightsourcesincorrect.png "35_LightSourcesIncorrect 0404")|  
  
 Use contornos apenas para melhorar a legibilidade ou para comunicar melhor a metáfora. Saldo negativo positivo (claro-escuro) deve ser 50/50.  
  
|||  
|-|-|  
|**Uso correto de estruturas de tópicos**|**Uso incorreto de estruturas de tópicos**|  
|![Corrija os contornos](../../extensibility/ux-guidelines/media/0404-36-outlinescorrect.png "36_OutlinesCorrect 0404")|![Contornos incorretos](../../extensibility/ux-guidelines/media/0404-37-outlinesincorrect.png "37_OutlinesIncorrect 0404")|  
  
#### <a name="icon-types"></a>Tipos de ícones  
 **Barra de comandos e shell** ícones consistem em não mais do que três dos seguintes elementos: uma base, um modificador, uma ação ou um status.  
  
 ![Shell e ícones da barra de comando](../../extensibility/ux-guidelines/media/0404-38-shellicons.png "38_ShellIcons 0404")  
  
 **Exemplos de shell e ícones da barra de comando**  
  
 **Barra de comandos de janela de ferramenta** ícones consistem em não mais do que três dos seguintes elementos: uma base, um modificador, uma ação ou um status.  
  
 ![Ícones de barra de comandos de janela de ferramentas](../../extensibility/ux-guidelines/media/0404-39-toolwindowcommandbaricons.png "39_ToolWindowCommandBarIcons 0404")  
  
 **Exemplos de ícones da barra de ferramenta janela comando**  
  
 **Desambiguador do modo de exibição de árvore** ícones consistem em não mais do que três dos seguintes elementos: uma base, um modificador, uma ação ou um status.  
  
 ![Ícones de desambiguador do modo de exibição de árvore](../../extensibility/ux-guidelines/media/0404-40-treeviewicons.png "40_TreeViewIcons 0404")  
  
 **Exemplos de árvore exibir ícones desambiguador**  
  
 **Taxonomia de valor com base no estado** ícones existem nos seguintes estados: ativo, Active Directory desabilitada e inativos desabilitado.  
  
 ![Estado&#45;com base em ícones de valor de taxonomia](../../extensibility/ux-guidelines/media/0404-41-statebasedtaxonomy.png "41_StateBasedTaxonomy 0404")  
  
 **Exemplos de ícones de taxonomia de valor com base no estado**  
  
 **IntelliSense** ícones consistem em não mais do que três dos seguintes elementos: uma base de dados de um modificador e um status.  
  
 ![Ícones de IntelliSense](../../extensibility/ux-guidelines/media/0404-42-intellisenseicons.png "42_IntelliSenseIcons 0404")  
  
 **Exemplos de ícones do IntelliSense**  
  
 **Pequeno (16 x 16) projeto** ícones devem ter não mais de dois elementos: uma base e um modificador.  
  
 ![ícone do projeto de 16 x 16 &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-43-16x16project1.png "0404 43_16x16Project1") ![ícone do projeto de 16 x 16 &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-44-16x16project2.png "0404 44_16x16Project2") ![ícone do projeto de 16 x 16 &#40;3&#41;](../../extensibility/ux-guidelines/media/0404-45-16x16project3.png "45_16x16Project3 0404")  
  
 **Exemplos de ícones pequenos do projeto (16 x 16)**  
  
 **Grande (32 x 32) projeto** ícones consistem em não mais do que quatro dos seguintes elementos: uma base, um ou dois modificadores e uma linguagem de sobreposição.  
  
 ![ícones de projeto de 32 x 32](../../extensibility/ux-guidelines/media/0404-46-32x32project.png "46_32x32Project 0404")  
  
 **Exemplos de ícones grandes de projeto (32x32)**  
  
### <a name="production-details"></a>Detalhes de produção  
 Todos os novos elementos de interface do usuário devem ser criados usando o Windows Presentation Foundation (WPF) e todos os novos ícones para WPF devem estar no formato PNG de 32 bits. O PNG de 24 bits é um formato herdado que não oferece suporte a transparência e, portanto, não é recomendado para ícones.  
  
 Salve a resolução de 96 DPI.  
  
#### <a name="file-types"></a>Tipos de arquivo  
  
-   **PNG de 32 bits:** o formato preferencial para ícones. Um formato de arquivo de compactação sem perdas de dados que pode armazenar uma imagem de varredura única (pixel). arquivos PNG de 32 bits dão suporte a transparência de canal alfa, correção de gama e entrelaçamento.  
  
-   **BMP de 32 bits:** para controles não-WPF. Também chamado de XP ou colorido, 32-bit BMP é um formato de imagem RGB/A, uma imagem de true color com transparência de uma canal alfa. O canal alfa é uma camada de transparência designada do Adobe Photoshop, em seguida, é salvo dentro do bitmap como um adicional (quarta) canal de cor. Um plano de fundo preto é adicionado durante a produção de arte final para todos os arquivos BMP de 32 bits para fornecer uma indicação visual rápida sobre a intensidade de cor. Este plano de fundo preto representa a área a ser mascarado na interface do usuário.  
  
-   **ICO de 32 bits:** para ícones de projeto e adicionar o Item. Todos os arquivos ICO são cor true de 32 bits com transparência de canal alfa (A/RGB). Como os arquivos ICO podem armazenar vários tamanhos e intensidades de cores, ícones do Vista costumam ser em um formato ICO contendo 16 x 16, 32 x 32, 48 x 48 e tamanhos de imagem de 256 x 256. Para exibir corretamente no Windows Explorer, arquivos ICO devem ser salvo para baixo a intensidade de cor de 24 bits e de 8 bits para cada tamanho de imagem.  
  
-   **XAML:** para superfícies de design e os adornos de Windows. Ícones XAML são arquivos de imagem baseado em vetor que dão suporte ao dimensionamento, girar, arquivamento e transparência. Eles não são comuns no Visual Studio hoje, mas estão se tornando mais populares devido à sua flexibilidade.  
  
-   **SVG**  
  
-   **BMP de 24 bits:** para a barra de comando do Visual Studio. Um formato de imagem RGB true color, 24 bits BMP é uma convenção de ícone que cria uma camada de transparência usando magenta (255 = R, G = 0, B = 255) como uma chave de cor para uma camada de transparência de toque no-out. Em um BMP com 24 bits, todas as superfícies magenta são exibidas usando a cor do plano de fundo.  
  
-   **GIF de 24 bits:** para a barra de comando do Visual Studio. Um formato de imagem RGB true color que dá suporte à transparência. Arquivos GIF geralmente são usados em arte final do assistente e animações de GIF.  
  
### <a name="icon-construction"></a>Construção de ícone  
 O menor tamanho de ícone no Visual Studio é 16 x 16. O maior em comum o uso é 32 x 32. Tenha em mente, não para preencher todo o quadro de 16 x 16, 24 x 24 ou 32 x 32 durante a criação de um ícone. Construção de ícone uniforme, legível, é essencial para o reconhecimento de usuários. Seguem os seguintes pontos ao criar ícones.  
  
- Ícones devem ser consistente, clara e compreensível.  
  
- É melhor usar os elementos de notificação de status como ícones únicos e não a empilhá-los na parte superior de um elemento base do ícone. Em determinados contextos, a interface do usuário pode exigir o elemento de status a ser emparelhado com um elemento base.  
  
- Ícones de projeto geralmente são arquivos. ico que contêm vários tamanhos. Somente os ícones de 16 x 16, 24 x 24 e 32 x 32 estão sendo atualizados. A maioria dos ícones de 16 x 16 e 24 x 24 conterá os mesmos elementos. Os ícones de 32 x 32 contêm mais detalhes, incluindo o tipo de linguagem do projeto quando aplicável.  
  
- Para os ícones de 32 x 32, os elementos base geralmente têm um peso de linha 2 pixels. Um peso de linha de pixel de 1 ou 2 pode ser usado para elementos de detalhe. Use o bom senso para determinar qual é mais adequado.  
  
- Ter pelo menos um espaçamento de 1 pixel entre elementos de 16 x 16 e ícones de 24 x 24. Para os ícones de 32 x 32, use 2 pixels espaçamento entre elementos e entre o elemento base e o modificador.  
  
  ![Espaçamento de elementos para os ícones de 16 x 16, 24 x 24 e 32 x 32](../../extensibility/ux-guidelines/media/0404-47-elementspacing.png "47_ElementSpacing 0404")  
  
  **Espaçamento de elementos para os ícones em tamanho de 16 x 16, 24 x 24 e 32 x 32**  
  
#### <a name="color-and-accessibility"></a>Cor e acessibilidade  
 Diretrizes de conformidade do Visual Studio exigem que todos os ícones no produto passam os requisitos de acessibilidade para cor e contraste. Isso é feito por meio de inversão de ícone, e quando você está criando, você deve estar ciente que será ser invertidas programaticamente no produto.  
  
 Para obter mais informações sobre como usar cores de ícones do Visual Studio, consulte [usando a cor em imagens](../../extensibility/ux-guidelines/images-and-icons-for-visual-studio.md#BKMK_UsingColorInImages).  
  
##  <a name="BKMK_UsingColorInImages"></a> Usando a cor em imagens  
  
### <a name="overview"></a>Visão geral  
 Os ícones no Visual Studio são principalmente monocromáticos. Cor é reservada para transmitir informações específicas e nunca para a decoração. Cor é usada:  
  
-   para indicar uma ação  
  
-   para alertar o usuário para uma notificação de status  
  
-   para designar a afiliação do idioma  
  
-   para diferenciar itens dentro do IntelliSense  
  
### <a name="accessibility"></a>Acessibilidade  
 Diretrizes de conformidade do Visual Studio exigem que todos os ícones de check-in na passagem de produto os requisitos de acessibilidade para cor e contraste. As cores na paleta de linguagem visual foram testadas e atenderam a esses requisitos.  
  
#### <a name="color-inversion-for-dark-themes"></a>Inversão de cores para os temas escuros  
 Para fazer com que os ícones aparecem com a taxa de contraste correto no tema escuro Visual Studio uma inversão é aplicada por meio de programação. As cores neste guia foram escolhidas em parte, de modo que eles invertem corretamente. Restringir o uso de cores a essa paleta, ou você terá resultados imprevisíveis quando a inversão é aplicada.  
  
 ![Exemplos de ícones cujas cores têm sido invertidas](../../extensibility/ux-guidelines/media/0405-01-darkthemeinversion.png "01_DarkThemeInversion 0405")  
  
 **Exemplos de ícones que tiveram suas cores invertidas**  
  
### <a name="base-palette"></a>Paleta de base  
 Todos os ícones padrão contêm três cores de base. Ícones de não contenham nenhuma gradientes ou sombras, com uma ou duas exceções para os ícones de ferramenta 3D.  
  
|Uso|Nome|Valor (tema claro)|Amostra de|Exemplo|  
|-----------|----------|---------------------------|------------|-------------|  
|Em segundo plano/escuro|VS BG|424242 / 66,66,66|![Swatch 424242](../../extensibility/ux-guidelines/media/0405-424242.png "0405_424242")|![Exemplo de base paleta](../../extensibility/ux-guidelines/media/0405-02-basepaletteexample.png "02_BasePaletteExample 0405")|  
|Em primeiro plano/leve|VS FG|F0EFF1 / 240,239,241|![Swatch F0EFF1](../../extensibility/ux-guidelines/media/0405-f0eff1.png "0405_F0EFF1")||  
|Contorno|VS-Out|F6F6F6 / 246,246,246|![Swatch F6F6F6](../../extensibility/ux-guidelines/media/0405-f6f6f6.png "0405_F6F6F6")||  
  
 As cores de base, além de cada ícone pode conter adicionais em uma cor de paleta estendida.  
  
### <a name="extended-palette"></a>Paleta estendida  
  
#### <a name="action-modifiers"></a>Modificadores de ação  
 Quatro cores indicam os tipos de ações exigidas pelo modificadores de ação:  
  
|Uso|Nome|Valor (todos os temas)|Amostra de|  
|-----------|----------|--------------------------|------------|  
|Positivo|Verde de ação do VS|388A34 / 56,138,52|![Swatch 388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|  
|Negativo|Vermelho de ação do VS|A1260D / 161,38,13|![Swatch A1260D](../../extensibility/ux-guidelines/media/0405-a1260d.png "0405_A1260D")|  
|Neutro|VS ação azul|C 00539 / 0,83,156|![Swatch 00539C](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|  
|Criar/novo|VS ação laranja|C27D1A / 194,156,26|![Swatch C27D1A](../../extensibility/ux-guidelines/media/0405-c27d1a.png "0405_C27D1A")|  
  
##### <a name="examples"></a>Exemplos  
 Verde é usado para modificadores de ação positivo, como "Adicionar", "Executar", "Reproduzir" e "Validar".  
  
|||||  
|-|-|-|-|  
|![Ícone executar](../../extensibility/ux-guidelines/media/0405-03-actionmodifierrun.png "0405 03_ActionModifierRun") **executar**|![Ícone do executar consulta](../../extensibility/ux-guidelines/media/0405-04-executequery.png "0405 04_ExecuteQuery") **executar consulta**|![Ícone de todas as etapas de reproduzir](../../extensibility/ux-guidelines/media/0405-05-playallsteps.png "0405 05_PlayAllSteps") **reproduzir todas as etapas**|![Adicionar ícone do controle](../../extensibility/ux-guidelines/media/0405-06-addcontrol.png "0405 06_AddControl") **adicionar controle**|  
  
 Vermelho é usado para modificadores de ação negativo, como "Excluir," "Stop", "Cancelar" e "Fechar".  
  
|||||  
|-|-|-|-|  
|![Excluir ícone relacionamento](../../extensibility/ux-guidelines/media/0405-07-deleterelationship.png "0405 07_DeleteRelationship") **Excluir relação**|![Excluir coluna de ícone](../../extensibility/ux-guidelines/media/0405-08-deletecolumn.png "0405 08_DeleteColumn") **excluir coluna**|![Ícone de consulta de parada](../../extensibility/ux-guidelines/media/0405-09-stopquery.png "0405 09_StopQuery") **parar consulta**|![Ícone de Conexão off-line](../../extensibility/ux-guidelines/media/0405-10-connectionoffline.png "0405 10_ConnectionOffline") **Conexão Offline**|  
  
 Azul é aplicada à ação neutra modificadores mais comumente representadas como setas, tais como "Open," "Next", "Anterior", "Importar" e "Exportar".  
  
|||||  
|-|-|-|-|  
|![Vá para o ícone de campo](../../extensibility/ux-guidelines/media/0405-11-gotofield.png "0405 11_GoToField") **ir para o campo**|![Em lote de seleção&#45;no ícone](../../extensibility/ux-guidelines/media/0405-12-batchedcheckin.png "0405 12_BatchedCheckIn") **em lote Check-In**|![Ícone do editor de endereço](../../extensibility/ux-guidelines/media/0405-13-addresseditor.png "0405 13_AddressEditor") **Editor de endereço**|![Ícone do editor de associação](../../extensibility/ux-guidelines/media/0405-14-associationeditor.png "0405 14_AssociationEditor") **Editor de associação**|  
  
 Ouro-escuro é usado principalmente para o modificador "New".  
  
|||||  
|-|-|-|-|  
|![Ícone do novo projeto](../../extensibility/ux-guidelines/media/0405-15-newproject.png "0405 15_NewProject") **novo projeto**|![Criar novo ícone de gráfico](../../extensibility/ux-guidelines/media/0405-16-createnewgraph.png "0405 16_CreateNewGraph") **criar um novo gráfico**|![Novo ícone de teste de unidade](../../extensibility/ux-guidelines/media/0405-17-newunittest.png "0405 17_NewUnitTest") **novo teste de unidade**|![Ícone de novo item de lista](../../extensibility/ux-guidelines/media/0405-18-newlistitem.png "0405 18_NewListItem") **Novo Item de lista**|  
  
#### <a name="special-cases"></a>Casos especiais  
 Em casos especiais, um modificador de ação colorido pode ser usado independentemente como um ícone de autônomo. A cor usada para o ícone reflete as ações que o ícone está associado. Esse uso é limitado a um pequeno subconjunto de ícones, incluindo:  
  
||||||  
|-|-|-|-|-|  
|![Ícone executar](../../extensibility/ux-guidelines/media/0405-03-actionmodifierrun.png "0405 03_ActionModifierRun") **executar**|![Ícone de interrupção](../../extensibility/ux-guidelines/media/0405-19-stop.png "0405 19_Stop") **parar**|![Excluir ícone](../../extensibility/ux-guidelines/media/0405-20-delete.png "0405 20_Delete") **excluir**|![Ícone Salvar](../../extensibility/ux-guidelines/media/0405-21-save.png "0405 21_Save") **salvar**|![Ícone de voltar Navigate](../../extensibility/ux-guidelines/media/0405-22-navigateback.png "0405 22_NavigateBack") **navegue novamente**|  
  
### <a name="code-hierarchy-palette"></a>Paleta de hierarquia de código  
  
#### <a name="folder"></a>Pasta  
  
|Uso|Nome|Valor (todos os temas)|Amostra de|Exemplo|  
|-----------|----------|--------------------------|------------|-------------|  
|Pastas|Pasta|DCB67A / 220,182,122|![Swatch DCB67A](../../extensibility/ux-guidelines/media/0405-dcb67a.png "0405_DCB67A")|![Ícone de pasta de cor](../../extensibility/ux-guidelines/media/0405-23-foldercolor.png "23_FolderColor 0405")|  
  
#### <a name="visual-studio-languages"></a>Idiomas do Visual Studio  
 Cada um dos idiomas comum ou plataformas disponíveis no Visual Studio tem uma cor associada. Essas cores são usadas no ícone de base, ou em modificadores de linguagem que aparecem no canto superior direito dos ícones compostas.  
  
|Uso|Nome|Valor (todos os temas)|Amostra de|  
|-----------|----------|--------------------------|------------|  
|ASP, HTML, WPF|ASP HTML WPF azul|7 DE 0095D / 0,149,215|![Swatch 0095D7](../../extensibility/ux-guidelines/media/0405-0096d7.png "0405_0096D7")|  
|C++|CPP roxo|9B4F96 / 155,79,150|![Swatch 9B4F96](../../extensibility/ux-guidelines/media/0405-9b4f96.png "0405_9B4F96")|  
|C#|CS Green (verde de ação do VS)|388A34 / 56,138,52|![Swatch 388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|  
|CSS|Vermelho CSS|BD1E2D / 189,30,45|![Swatch BD1E2D](../../extensibility/ux-guidelines/media/0405-bd1e2d.png "0405_BD1E2D")|  
|F#|FS roxo|672878 / 103,40,120|![Swatch 672878](../../extensibility/ux-guidelines/media/0405-672878.png "0405_672878")|  
|JavaScript|Laranja JS|F16421 / 241,100,33|![Swatch F16421](../../extensibility/ux-guidelines/media/0405-f16421.png "0405_F16421")|  
|VB|VB Blue (azul de ação do VS)|C 00539 / 0,83,156|![Swatch 00539C](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|  
|TypeScript|TS laranja|E04C06 / 224,76,6|![Swatch E04C06](../../extensibility/ux-guidelines/media/0405-e04c06.png "0405_E04C06")|  
|Python|Aj verde|879636 / 135,150,54|![Swatch 879636](../../extensibility/ux-guidelines/media/0405-879636.png "0405_879636")|  
  
##### <a name="examples-of-icons-with-language-modifiers"></a>Exemplos de ícones com modificadores de linguagem  
  
|||||||  
|-|-|-|-|-|-|  
|![Ícone de Visual Basic](../../extensibility/ux-guidelines/media/0405-25-vb.png "0405 25_VB") **VB**|![C&#35; ícone](../../extensibility/ux-guidelines/media/0405-26-csharp.png "0405 26_CSharp")**C#**|![C&#43; &#43; ícone](../../extensibility/ux-guidelines/media/0405-27-cplusplus.png "0405 27_CPlusPlus") **C++**|![F&#35; ícone](../../extensibility/ux-guidelines/media/0405-28-fsharp.png "0405 28_FSharp")**F#**|![Ícone de JavaScript](../../extensibility/ux-guidelines/media/0405-29-javascript.png "0405 29_JavaScript") **JavaScript**|![Ícone do Python](../../extensibility/ux-guidelines/media/0405-30-python.png "0405 30_Python") **Python**|  
|![Ícone HTML](../../extensibility/ux-guidelines/media/0405-31-html.png "0405 31_HTML") **HTML**|![Ícone do WPF](../../extensibility/ux-guidelines/media/0405-32-wpf.png "0405 32_WPF") **WPF**|![Ícone ASP](../../extensibility/ux-guidelines/media/0405-33-asp.png "0405 33_ASP") **ASP**|![Ícone CSS](../../extensibility/ux-guidelines/media/0405-34-css.png "0405 34_CSS") **CSS**|![Ícone de TypeScript](../../extensibility/ux-guidelines/media/0405-35-typescript.png "0405 35_TypeScript") **TypeScript**||  
  
#### <a name="intellisense"></a>IntelliSense  
 Ícones de IntelliSense usam uma paleta de cores exclusivas. Essas cores são usadas para ajudar os usuários a distinguir rapidamente entre diferentes itens na lista de pop-up do IntelliSense.  
  
|Uso|Nome|Valor (todos os temas)|Amostra de|  
|-----------|----------|--------------------------|------------|  
|Classe de evento|VS ação laranja|C27D1A / 194,125,26|![Swatch C27D1A](../../extensibility/ux-guidelines/media/0405-c27d1a.png "0405_C27D1A")|  
|Método de extensão, método, módulo, delegado|VS ação roxo|652 90 DE D / 101,45,144|![Swatch 652D90](../../extensibility/ux-guidelines/media/0405-652d90.png "0405_652D90")|  
|Campo, Item de enumeração, Macro, estrutura, tipo de valor de união, operador, de Interface|VS ação azul|C 00539 / 0,83,156|![Swatch 00539C](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|  
|Objeto|Verde de ação do VS|388A34 / 56,138,52|![Swatch 388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|  
|Constante, exceção, Item de enumeração, mapa, Item de mapa, Namespace, modelo, definição de tipo|Em segundo plano (VS BG)|424242 / 66,66,66|![Swatch 424242](../../extensibility/ux-guidelines/media/0405-424242.png "0405_424242")|  
  
##### <a name="examples-of-intellisense-icons"></a>Exemplos de ícones do IntelliSense  
  
||||||  
|-|-|-|-|-|  
|![Ícone de classe do IntelliSense](../../extensibility/ux-guidelines/media/0405-36-intellisenseclass.png "0405 36_IntelliSenseClass") **classe**|![Ícone de evento particular do IntelliSense](../../extensibility/ux-guidelines/media/0405-37-intellisenseprivateevent.png "0405 37_IntelliSensePrivateEvent") **evento particular**|![Ícone de delegado do IntelliSense](../../extensibility/ux-guidelines/media/0405-38-intellisensedelegate.png "0405 38_IntelliSenseDelegate") **delegar**|![Ícone do IntelliSense método amigo](../../extensibility/ux-guidelines/media/0405-39-intellisensemethodfriend.png "0405 39_IntelliSenseMethodFriend") **amigo do método**|![Ícone de campo](../../extensibility/ux-guidelines/media/0405-40-field.png "0405 40_Field") **campo**|  
|![IntelliSense protegido ícone do item de enum](../../extensibility/ux-guidelines/media/0405-41-intellisenseprotectedenumitem.png "0405 41_IntelliSenseProtectedEnumItem") **Item protegido de Enum**|![Ícone de objeto do IntelliSense](../../extensibility/ux-guidelines/media/0405-42-intellisenseobject.png "0405 42_IntelliSenseObject") **objeto**|![Ícone de modelo do IntelliSense](../../extensibility/ux-guidelines/media/0405-43-intellisensetemplate.png "0405 43_IntelliSenseTemplate") **modelo**|![Ícone de atalho de exceção do IntelliSense](../../extensibility/ux-guidelines/media/0405-44-intellisenseexceptionshortcut.png "0405 44_IntelliSenseExceptionShortcut") **atalho de exceção**||  
  
### <a name="notifications"></a>Notificações  
 As notificações no Visual Studio são usadas para indicar o status. A paleta de notificação usa os seguintes quatro cores, bem como opções de preenchimento de primeiro plano preto ou branco, para definir notificações com os seguintes níveis de status.  
  
|Uso|Nome|Valor (todos os temas)|Amostra de|  
|-----------|----------|--------------------------|------------|  
|Status: neutro|Notificação azul (VS azul)|1BA1E2 / 27,161,226|![Amostra 1BA1E2](../../extensibility/ux-guidelines/media/0405-1ba1e2.png "0405_1BA1E2")|  
|Status: positivo|Notificação Green (verde VS)|339933 / 51,153,51|![Swatch 339933](../../extensibility/ux-guidelines/media/0405-339933.png "0405_339933")|  
|Status: negativo|Notificação Red (vermelho VS)|E51400 / 229,20,0|![Swatch E51400](../../extensibility/ux-guidelines/media/0405-e51400.png "0405_E51400")|  
|Status: aviso|Notificação amarelo (VS laranja)|FFCC00 / 255,204,0|![Swatch FFCC00](../../extensibility/ux-guidelines/media/0405-ffcc00.png "0405_FFCC00")|  
|Preenchimento de primeiro plano|Notificação preto (preto)|000000 / 0,0,0|![Swatch &#35;000000](../../extensibility/ux-guidelines/media/0405-000000.png "0405_000000")|  
|Preenchimento de primeiro plano|Notificação em branco (branco)|FFFFFF / 255,255,255|![Swatch FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|  
  
#### <a name="examples-of-notification-icons"></a>Exemplos de ícones de notificação  
  
|||||  
|-|-|-|-|  
|![Ícone de alerta](../../extensibility/ux-guidelines/media/0405-45-alert.png "0405 45_Alert") **alerta**|![Ícone de aviso](../../extensibility/ux-guidelines/media/0405-48-warning.png "0405 48_Warning") **aviso**|![Ícone concluído](../../extensibility/ux-guidelines/media/0405-46-complete.png "0405 46_Complete") **concluir**|![Ícone de interrupção](../../extensibility/ux-guidelines/media/0405-47-stop.png "0405 47_Stop") **parar**|  
  
### <a name="visual-studio-online"></a>Visual Studio Online  
 Em geral, o Visual Studio Online consiste em recursos hospedados em um navegador. A cor varia em ambientes diferentes, mas o estilo permanece o mesmo.  
  
|Grupo|Uso|Nome|Valor (todos os temas)|Amostra de|  
|-----------|-----------|----------|--------------------------|------------|  
|TFS|Informações preliminares|BG TFSO|656565/ 101, 101, 101|![Amostra de 656565](../../extensibility/ux-guidelines/media/0405-656565.png "0405_656565")|  
|TFS|Contorno|TFSO-OUT|FFFFFF / 255, 255, 255|![Swatch FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|  
|Napa|Informações preliminares|Branco|FFFFFF / 255, 255, 255|![Swatch FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|  
|Mônaco|Informações preliminares|Branco|FFFFFF / 255, 255, 255|![Swatch FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|  
|F12|Informações preliminares|Branco|FFFFFF / 255, 255, 255|![Swatch FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|  
|F12|Normal|Grey_Primary F12|555555 / 85, 85, 85|![Amostra de 555555](../../extensibility/ux-guidelines/media/0405-555555.png "0405_555555")|  
|F12|Passe o mouse|Blue_Hover F12|2279BF / 34,121,191|![Swatch 2279BF](../../extensibility/ux-guidelines/media/0405-2279bf.png "0405_2279BF")|  
|F12|Disabled|F12 LtGrey_Disabled|ABABAC / 171,171,172|![Swatch ABABAC](../../extensibility/ux-guidelines/media/0405-ababac.png "0405_ABABAC")|  
|F12|Passe o mouse em segundo plano|Passe o mouse bg|D9EBF7 / 217,235,247|![Swatch D9EBF7](../../extensibility/ux-guidelines/media/0405-d9ebf7.png "0405_D9EBF7")|  
|F12|Plano de fundo pressionado|Bg pressionado|B2D7F0 / 178,215,240|![Swatch B2D7F0](../../extensibility/ux-guidelines/media/0405-b2d7f0.png "0405_B2D7F0")|  
|F12|Contorno|VS-OUT|F6F6F6 / 246,246,246|![Swatch F6F6F6](../../extensibility/ux-guidelines/media/0405-f6f6f6.png "0405_F6F6F6")|  
|F12|Informações|Informações|00BCF2 / 0,188,242|![Swatch 00BCF2](../../extensibility/ux-guidelines/media/0405-00bcf2.png "0405_00BCF2")|  
|F12|Aviso|Aviso|F28300 / 242,131,0|![Swatch F28300](../../extensibility/ux-guidelines/media/0405-f28300.png "0405_F28300")|  
|F12|Erro / negativo|Error_Negative|E81123 / 232,17,35|![Swatch E81123](../../extensibility/ux-guidelines/media/0405-e81123.png "0405_E81123")|  
|F12|Iniciar / positivo|Start_Positive|009E49 / 0,158,73|![Swatch 009E49](../../extensibility/ux-guidelines/media/0405-009e49.png "0405_009E49")|  
|F12|Tipo de quebra|Tipo de quebra|9B4F96 / 155,79,150|![Swatch 9B4F96](../../extensibility/ux-guidelines/media/0405-9b4f96.png "0405_9B4F96")|  
|F12|Marca de evento|Marca de evento|A51F00 / 165,31,0|![Swatch A51F00](../../extensibility/ux-guidelines/media/0405-a51f00.png "0405_A51F00")|  
|F12|Marca de usuário|Marca de usuário|F16220 / 241,98,32|![Swatch F16220](../../extensibility/ux-guidelines/media/0405-f16220.png "0405_F16220")|  
  
#### <a name="examples-of-visual-studio-online-icons"></a>Exemplos de ícones do Visual Studio Online  
  
|TFS Online||||  
|----------------|-|-|-|  
|![Ícone de equipe TFS Online](../../extensibility/ux-guidelines/media/0405-49-tfsonlineteam.png "0405 49_TFSOnlineTeam") **equipe Online**|![Ícone de informações do TFS](../../extensibility/ux-guidelines/media/0405-50-tfsinformation.png "0405 50_TFSInformation") **informações**|![Ícone de histórico do TFS](../../extensibility/ux-guidelines/media/0405-51-tfshistory.png "0405 51_TFSHistory") **histórico**|![Ícone do branch TFS](../../extensibility/ux-guidelines/media/0405-52-tfsbranch.png "0405 52_TFSBranch") **Branch**|  
  
|Napa||||  
|----------|-|-|-|  
|![Ícone de conteúdo Napa](../../extensibility/ux-guidelines/media/0405-53-napacontent.png "0405 53_NapaContent") **conteúdo**|![Ícone de email do office Napa](../../extensibility/ux-guidelines/media/0405-54-napaofficemail.png "0405 54_NapaOfficeMail") **email do Office**|![Ícone do SharePoint Napa](../../extensibility/ux-guidelines/media/0405-55-napasharepoint.png "0405 55_NapaSharePoint") **SharePoint**|![Ícone do painel de tarefas Napa](../../extensibility/ux-guidelines/media/0405-56-napataskpane.png "0405 56_NapaTaskPane") **painel de tarefas**|  
  
|Mônaco||||  
|------------|-|-|-|  
|![Ícone de arquivos de Mônaco](../../extensibility/ux-guidelines/media/0405-57-monacofiles.png "0405 57_MonacoFiles") **arquivos**|![Ícone do Git Mônaco](../../extensibility/ux-guidelines/media/0405-58-monacogit.png "0405 58_MonacoGit") **Git**|![Ícone de pesquisa de Mônaco](../../extensibility/ux-guidelines/media/0405-59-monacosearch.png "0405 59_MonacoSearch") **pesquisa**|![Ícone de texto de Mônaco](../../extensibility/ux-guidelines/media/0405-60-monacotext.png "0405 60_MonacoText") **texto**|  
  
|F12||||  
|---------|-|-|-|  
|![Ícone de muito código F12](../../extensibility/ux-guidelines/media/0405-61-f12prettycode.png "0405 61_F12PrettyCode") **bastante código**|![Ícone de aviso de F12](../../extensibility/ux-guidelines/media/0405-62-f12warning.png "0405 62_F12Warning") **aviso**|![Ícone de F12 emular](../../extensibility/ux-guidelines/media/0405-63-f12emulate.png "0405 63_F12Emulate") **Emulate**|

