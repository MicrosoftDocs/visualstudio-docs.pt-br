---
title: Editor de imagem
ms.date: 08/10/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
f1_keywords:
- vs.graphics.designer.imageeditor
- vs.graphics.imageeditor
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2149410782587d8472faff678cbc20bf1ea577c1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49878369"
---
# <a name="image-editor"></a>Editor de imagem

Este artigo descreve como trabalhar com o **Editor de Imagens** do Visual Studio para exibir e modificar os recursos de textura e de imagem.

Você pode usar o **Editor de Imagens** para trabalhar com os tipos de formatos avançados de textura e imagens que são usados no desenvolvimento de aplicativos DirectX. Isso inclui o suporte para formatos de arquivo de imagem populares e codificações de cor, recursos como canais alfa e mapeamento MIP e muitos dos formatos de textura altamente compactados e acelerados por hardware, que são compatíveis com o DirectX.

## <a name="supported-formats"></a>Formatos com suporte

O **Editor de Imagens** dá suporte aos seguintes formatos de imagem:

|Nome do formato|Extensão de nome de arquivo|
|-----------------| - |
|Formato PNG (Portable Network Graphics)|*.png*|
|JPEG|*.jpg*, *.jpeg*, *.jpe*, *.jfif*|
|Direct Draw Surface|*.dds*|
|Formato GIF (Graphics Interchange Format)|*.gif*|
|Bitmap|*.bmp*, *.dib*|
|Formato TIFF|*.tif*, *.tiff*|
|Formato TGA (Targa)|*.tga*|

## <a name="get-started"></a>Introdução

Esta seção descreve como adicionar uma imagem ao seu projeto do Visual Studio e configurá-lo para os seus requisitos.

### <a name="add-an-image-to-your-project"></a>Adicionar uma imagem ao seu projeto

1. No **Gerenciador de Soluções**, abra o menu de atalho do projeto ao qual você deseja adicionar a imagem e selecione **Adicionar** > **Novo Item**.

2. Na caixa de diálogo **Adicionar Novo Item**, em **Instalado**, selecione **Gráficos** e escolha um formato de arquivo apropriado para a imagem.

   > [!NOTE]
   > Se você não vir a categoria **Elementos Gráficos** na caixa de diálogo **Adicionar Novo Item**, talvez seja necessário instalar o componente **Editores de imagens e modelos 3D**. Feche a caixa de diálogo e, em seguida, selecione **Ferramentas** > **Obter Ferramentas e Recursos** na barra de menus para abrir o **Instalador do Visual Studio**. Selecione a guia **Componentes individuais** e, em seguida, selecione o componente **Editores de imagens e modelos 3D** na categoria **Jogos e Elementos Gráficos**. Selecione **Modificar**.
   >
   > ![Componente Editores de imagens e modelos 3D](media/image-3d-model-editors-component.png)

   Para obter informações sobre como escolher um formato de arquivo com base em seus requisitos, confira [Escolher o formato de imagem](#choose-the-image-format).

3. Especifique o **Nome** do arquivo de imagem e a **Localização** na qual você deseja que ele seja criado.

4. Escolha o botão **Adicionar**.

### <a name="choose-the-image-format"></a>Escolher o formato da imagem

Dependendo de como você planeja usar a imagem, determinados formatos de arquivo podem ser mais apropriados do que outros. Por exemplo, alguns formatos podem não dar suporte a um recurso que você precisa, por exemplo, a transparência ou um formato de cor específico. Alguns formatos podem não fornecer uma compactação adequada para o tipo de conteúdo de imagem que você planejou.

As informações a seguir podem ajudá-lo a escolher um formato de imagem que atenda às suas necessidades:

**Imagem de bitmap (.bmp)**

O formato de imagem de bitmap. Um formato de imagem não compactado que dá suporte a cores de 24 bits. O formato de bitmap não dá suporte a transparências.

**Imagem GIF (.gif)**

O formato de imagem GIF (Graphics Interchange Format). Um formato de imagem compactados em LZW sem perdas que dá suporte a até 256 cores. Inadequado para fotografias e imagens com uma quantidade significativa de detalhes de cores, porém fornece boas taxas de compactação para imagens com poucas cores que têm um alto grau de coerência de cor.

**Imagem JPG (.jpg)**

O formato de imagem JPEG (Joint Photographic Experts Group). Um formato de imagem altamente compactado e com perdas que dá suporte a cores de 24 bits e é adequado para a compactação de imagens de uso geral com um alto grau de coerência de cor.

**Imagem PNG (.png)**

O formato de imagem PNG (Portable Network Graphics). Um formato de imagem moderadamente compactado e sem perdas, que dá suporte a cores de 24 bits e transparência alfa. Ele é adequado para imagens naturais e artificiais, mas não oferece taxas de compactação tão boas quanto formatos com perda como JPG ou GIF.

**Imagem TIFF (.tif)**

O formato de imagem TIFF (ou TIF). Um formato de imagem flexível que dá suporte a vários esquemas de compactação.

**Textura DDS (.dds)**

O formato de textura DDS (DirectDraw Surface). Um formato de textura altamente compactado e com perdas, que dá suporte a cores de 24 bits e transparência alfa. Suas taxas de compactação chegam a até 8:1. Ele se baseia na compactação de Textura S3, que pode ser descompactada no hardware gráfico.

**Imagem TGA (.tga)**

O formato de imagem TGA (Truevision Graphics Adapter, também conhecido como Targa). Um formato de imagem compactado em RLE e sem perda que dá suporte a imagens com cores mapeadas (paleta de cores) e diretas de cores de até 24 bits e transparência alfa. Inadequado para fotografias e imagens com uma quantidade significativa de detalhes de cores, porém fornece boas taxas de compactação para imagens com longas extensões de cores idênticas.

### <a name="configure-the-image"></a>Configurar a imagem

Antes de começar a trabalhar com a imagem criada, você pode alterar sua configuração padrão. Por exemplo, você pode alterar suas dimensões ou o formato de cores que ela usa. Para obter informações sobre como configurar essas e outras propriedades da imagem, consulte [Propriedades da imagem](#image-properties).

> [!NOTE]
> Antes de salvar seu trabalho, verifique se a propriedade **Formato de Cor** foi definida se você quiser usar um formato de cor específico. Se o formato de arquivo der suporte à compactação, você poderá ajustar as configurações de compactação quando salvar o arquivo pela primeira vez ou ao escolher **Salvar como**.

## <a name="work-with-the-image-editor"></a>Trabalhar com o Editor de Imagens

Esta seção descreve como usar o **Editor de Imagens** para modificar texturas e imagens.

Os comandos que afetam o estado do **Editor de Imagens** estão localizados na barra de ferramentas **Modo do Editor de Imagens** junto com os comandos avançados. A barra de ferramentas está localizada na borda superior da área de design do **Editor de Imagens**. As ferramentas de desenho encontram-se na barra de ferramentas do **Editor de Imagens** na borda esquerda da área de design do **Editor de Imagens**.

### <a name="image-editor-mode-toolbar"></a>Barra de ferramentas Modo do Editor de Imagens

![Barra de ferramentas Modo do Editor de Imagens no Visual Studio](../designers/media/digit-tre-modal-toolbar.png)

A tabela a seguir descreve os itens na barra de ferramentas **Modo do Editor de Imagens**, que são listados na ordem em que são exibidos, da esquerda para a direita:

|Item da barra de ferramentas|Descrição|
|------------------|-----------------|
|**Selecionar**|Habilita a seleção de uma região retangular de uma imagem. Depois de selecionar uma região, você poderá recortar, copiar, mover, ajustar escala, girar, inverter ou excluir. Quando há uma seleção ativa, as ferramentas de desenho só afetam a região selecionada.|
|**Seleção Irregular**|Habilita a seleção de uma região irregular de uma imagem. Depois de selecionar uma região, você poderá recortar, copiar, mover, ajustar escala, girar, inverter ou excluir. Quando há uma seleção ativa, as ferramentas de desenho só afetam a região selecionada.|
|**Seleção de Varinha**|Habilita a seleção de uma região de cor semelhante de uma imagem. A *tolerância*, ou seja, a diferença máxima entre cores adjacentes na qual elas são consideradas semelhantes, pode ser configurada para incluir um intervalo maior ou menor de cores semelhantes. Depois de selecionar uma região, você poderá recortar, copiar, mover, ajustar escala, girar, inverter ou excluir. Quando há uma seleção ativa, as ferramentas de desenho só afetam a região selecionada.|
|**Panorâmica**|Habilita a movimentação da imagem em relação ao quadro de janela. No modo **Panorâmica**, selecione um ponto na imagem e mova-o.<br /><br /> Ative temporariamente o modo **Panorâmico** mantendo a tecla **Ctrl** pressionada.|
|**Zoom**|Habilita a exibição de mais ou menos detalhes da imagem em relação ao quadro de janela. No modo **Aplicar Zoom**, selecione um ponto na imagem e mova-o para a direita ou para baixo para ampliar ou para a esquerda ou para cima para reduzir.<br /><br /> Amplie ou reduza mantendo a tecla **Ctrl** pressionada enquanto usa o botão de rolagem do mouse ou pressiona o sinal de adição (**+**) ou de subtração (**-**).|
|**Aplicar Zoom para o Tamanho Real**|Exibe a imagem usando uma relacionamento 1:1 entre os pixels da imagem e os pixels da tela.|
|**Aplicar zoom para ajustar**|Exibe a imagem completa no quadro de janela.|
|**Zoom para a largura**|Exibe a largura completa da imagem no quadro de janela.|
|**Grade**|Habilita ou desabilita a grade que mostra os limites de pixel. A grade pode não aparecer até você ampliar a imagem.|
|**Exibição do Próximo Nível de MIP**|Ativa o próximo nível maior de MIP em uma cadeia de mapas MIP. O nível de MIP ativo é exibido na área de design. Este item só está disponível para texturas que têm níveis de MIP.|
|**Exibir um Nível de MIP Anterior**|Ativa o próximo nível menor de MIP em uma cadeia de mapas MIP. O nível de MIP ativo é exibido na área de design. Este item só está disponível para texturas que têm níveis de MIP.|
|**Canal vermelho**<br /><br /> **Canal verde**<br /><br /> **Canal azul**<br /><br /> **Canal alfa**|Habilita ou desabilita o canal da cor específica. **Observação:** habilitando ou desabilitando sistematicamente os canais de cor, você pode isolar problemas relacionados a um ou mais deles. Por exemplo, você poderia identificar a transparência alfa incorreta.|
|**Tela de Fundo**|Habilita ou desabilita a exibição da tela de fundo através das partes transparentes da imagem. Você pode configurar como a tela de fundo é exibida escolhendo entre estas opções:<br /><br /> **Quadriculado**<br /> Usa uma cor verde junto com a cor da tela de fundo especificada para exibir a tela de fundo como um padrão quadriculado. Você pode usar essa opção para ajudar a tornar as partes transparentes da imagem mais visíveis.<br /><br /> Tela de fundo branco<br /> Usa a cor branca para exibir a tela de fundo.<br /><br /> Tela de fundo preto<br /> Usa a cor preta para exibir a tela de fundo.<br /><br /> Animar a tela de fundo<br /> Movimenta o padrão quadriculado lentamente em panorâmica. Você pode usar essa opção para ajudar a tornar as partes transparentes da imagem mais visíveis.|
|**Propriedades**|Alterna entre abrir e fechar a janela **Propriedades**.|
|**Avançado**|Contém comandos e opções adicionais.<br /><br /> **Filtros**<br /><br /> Fornece vários filtros de imagem comuns: **Preto e branco**, **Desfoque**, **Iluminar**, **Escurecer**, **Detecção de borda**, **Colocar em alto-relevo**, **Inverter cores**, **Ripple**, **Tom sépia** e **Ajustar nitidez**.<br /><br /> **Mecanismos Gráficos**<br /><br /> **Renderizar com o D3D11**<br /> Usa o Direct3D 11 para renderizar a área de design do **Editor de Imagens**.<br /><br /> **Renderizar com o D3D11WARP**<br /> Usa o 11 WARP (Windows Advanced Rasterization Platform) do Direct3D para renderizar a área de design do **Editor de Imagens**.<br /><br /> **Ferramentas**<br /><br /> **Inverter Horizontalmente**<br /> Transpõe a imagem ao redor do seu eixo horizontal, também chamado x.<br /><br /> **Inverter Verticalmente**<br /> Transpõe a imagem ao redor do seu eixo vertical, também chamado y.<br /><br /> **Gerar Mips**<br /> Gera os níveis de MIP para uma imagem. Se os níveis de MIP já existirem, eles serão recriados do maior nível de MIP. Quaisquer alterações feitas aos níveis de MIP menores serão perdidas. Para salvar os níveis de MIP gerados, use o formato *.dds* para salvar a imagem.<br /><br /> **Exibir**<br /><br /> **Taxa de Quadros**<br /> Quando habilitado exibe a taxa de quadros no canto superior direito da área de design. A taxa de quadros é o número de quadros desenhados por segundo. **Dica:** escolha o botão **Avançado** para executar o último comando novamente.|

### <a name="image-editor-toolbar"></a>Barra de ferramentas do editor de imagens

![Barra de ferramentas do editor de imagens](../designers/media/digit-tre-toolbar.png)

A tabela a seguir descreve os itens da barra de ferramentas **Editor de Imagens**, que são listados na ordem em que aparecem, de cima para baixo:

|Item da barra de ferramentas|Descrição|
|------------------|-----------------|
|**Lápis**|Usa a seleção de cor ativa para desenhar um traço com alias. Você pode definir a cor e a espessura do traço na janela **Propriedades**.|
|**Pincel**|Usa a seleção de cor ativa para desenhar um traço suavizado. Você pode definir a cor e a espessura do traço na janela **Propriedades**.|
|**Spray**|Usa a seleção de cor ativa para desenhar um traço suavizado que se mescla à imagem e se torna mais saturado com o decorrer do tempo. Você pode definir a cor e a espessura do traço na janela **Propriedades**.|
|**Conta-gotas**|Define a seleção de cor ativa para a cor do pixel selecionado.|
|**Preenchimento**|Usa a seleção de cor ativa para preencher uma região da imagem. A região afetada é definida como o pixel em que o preenchimento é aplicado, junto com cada pixel conectado a ele por pixels da mesma cor e que são a mesma cor em si. Se o preenchimento for aplicado em uma seleção ativa, a região afetada ficará restringida pela seleção.<br /><br /> Por padrão, a seleção de cor ativa é mesclada com a região afetada da imagem de acordo com seu componente alfa. Para usar a seleção de cores ativa para substituir a região afetada, pressione e segure a tecla **Shift** ao usar a ferramenta de preenchimento.|
|**Borracha**|Define pixels para a cor totalmente transparente se a imagem der suporte a um canal alfa. Caso contrário, define os pixels para a cor da tela de fundo ativa.|
|**Linha**, **Retângulo**, **Retângulo Arredondado**, **Elipse**|Desenha uma forma na imagem. Você pode definir a cor e a espessura da estrutura de tópicos na janela **Propriedades**.<br /><br /> Para desenhar um primitivo com altura e largura iguais, pressione e segure a tecla **Shift** enquanto desenha.|
|**Texto**|Usa a seleção de cor de primeiro plano para desenhar o texto. A cor da tela de fundo é determinada pela seleção de cor da tela de fundo. Para uma tela de fundo transparente, o valor alfa da seleção da cor da tela de fundo deve ser 0. Quando a região de texto estiver ativa, você pode definir se o texto é desenhado com um traço suavizado ou pode definir o **Valor**, **Fonte**, **Tamanho** e o estilo — **Negrito**, **Itálico** ou **Sublinhado** — do texto na janela **Propriedades**. O conteúdo e a aparência do texto é finalizada quando a região de texto não está mais ativa.|
|**Girar**|Gira a imagem 90 graus no sentido horário.|
|**Cortar**|Corta a imagem para a seleção ativa.|

### <a name="work-with-mip-levels"></a>Trabalhar com níveis de MIP

Alguns formatos de imagem, por exemplo, o DirectDraw Surface (*.dds*) dão suporte a níveis de MIP para LOD (Nível de Detalhe) do espaço de textura. Para obter informações sobre como gerar e trabalhar com níveis de MIP, confira [Como criar e modificar níveis de MIP](../designers/how-to-create-and-modify-mip-levels.md)

### <a name="work-with-transparency"></a>Trabalhar com transparência

Alguns formatos de imagem, por exemplo, DirectDraw Surface (*.dds*), dão suporte a transparência. Há várias maneiras de usar a transparência, dependendo da ferramenta que está sendo usada. Para especificar o nível de transparência de uma seleção de cor, na janela **Propriedades**, defina o componente **A** (alfa) da seleção de cores.

A tabela a seguir descreve como os diferentes tipos ferramentas controlam como a transparência é aplicada:

|Ferramenta|Descrição|
|----------|-----------------|
|**Lápis**, **Pincel**, **Spray**, **Linha**, **Retângulo**, **Retângulo Arredondado**, **Elipse**, **Texto**|Para mesclar a seleção de cor ativa com a imagem na janela **Propriedades**, expanda o grupo de propriedades **Canais**, marque a caixa de seleção **Desenhar** no canal **Alfa** e desenhe normalmente.<br /><br /> Para desenhar usando a seleção de cor ativa e deixar o valor alfa da imagem em vigor, desmarque a caixa de seleção **Desenhar** do canal **Alfa** e, em seguida, desenhe normalmente.|
|**Preenchimento**|Para mesclar a seleção de cor ativa junto com a imagem, escolha a área a ser preenchida.<br /><br /> Para usar a seleção de cores ativa – incluindo o valor do canal alfa – para substituir a imagem, pressione e segure a tecla **Shift** e, em seguida, escolha a área a ser preenchida.|

### <a name="image-properties"></a>Propriedades da imagem

Você pode usar a janela **Propriedades** para especificar várias propriedades da imagem. Por exemplo, você pode definir as propriedades de largura e altura para redimensionar a imagem.

A tabela a seguir descreve as propriedades da imagem:

|Propriedade|Descrição|
|--------------|-----------------|
|Largura|A largura da imagem.|
|Altura|A altura da imagem.|
|Bits por Pixel|O número de bits que representa cada pixel. O valor desta propriedade depende do **Formato de Cor** da imagem.|
|Seleção Transparente|**True** para mesclar a camada de seleção com a imagem principal, com base no valor alfa da camada de seleção; caso contrário, **False**. Este item só está disponível para imagens que dão suporte a alfa.|
|Formatar|O formato de cor da imagem. É possível especificar uma variedade de formatos de cor, dependendo do formato da imagem. O formato de cor define o número e o tipo de canais de cor que estão incluídos na imagem e o tamanho e a codificação de vários canais.|
|Nível de MIP|O nível de MIP ativo. Este item só está disponível para texturas que têm níveis de MIP.|
|Contagem de Nível de Mip|O número total de níveis de MIP na imagem. Este item só está disponível para texturas que têm níveis de MIP.|
|Contagem de Quadros|O número total de quadros na imagem. Este item só está disponível para imagens que dão suporte a matrizes de textura.|
|Quadro|O quadro atual. Somente o primeiro quadro pode ser exibido; todos os outros quadros são perdidos quando a imagem é salva.|
|Contagem de Fatia de Profundidade|O número total de fatias de profundidade na imagem. Este item só está disponível para imagens que dão suporte a texturas de volume.|
|Fatia de Profundidade|A fatia de profundidade atual. Somente a primeira fatia pode ser exibida; todas as outras fatias são perdidas quando a imagem é salva.|

> [!NOTE]
> Como a propriedade **Girar por** se aplica a todas as ferramentas e regiões selecionadas, ela sempre aparece na parte inferior da janela **Propriedades** junto com outras propriedades de ferramenta. **Girar por** sempre é exibido, pois a imagem inteira é implicitamente selecionada quando não há nenhuma outra seleção ou ferramenta ativa. Para obter mais informações sobre a propriedade **Girar por**, confira [Propriedades da ferramenta](#tool -properties).

### <a name="resize-images"></a>Redimensionar imagens

Há duas maneiras de redimensionar uma imagem. Em ambos os casos, o **Editor de imagens** usa a interpolação bilinear para criar uma nova amostra da imagem.

- Na janela **Propriedades**, especifique os novos valores para as propriedades **Largura** e **Altura**.

- Selecione toda a imagem e use os marcadores de borda para redimensionar a imagem.

### <a name="selected-regions"></a>Regiões selecionadas

As seleções no **Editor de Imagens** definem as regiões da imagem que estão ativas. As regiões ativas são afetadas pelas ferramentas e transformações. Quando houver uma seleção ativa, as áreas fora da região selecionada não serão afetadas pela maioria das ferramentas e transformações. Se não houver uma seleção ativa, toda a imagem estará ativa.

A maioria das ferramentas (**Lápis**, **Pincel**, **Spray**, **Preenchimento**, **Borracha** e primitivas 2D) e transformações (**Girar**, **Cortar**, **Inverter Cores**, **Inverter Horizontalmente** e **Inverter Verticalmente**) são restritas ou definidas pela seleção ativa. No entanto, algumas ferramentas (**Conta-gotas** e **Texto**) e transformações (**Gerar Mips**) não são afetadas por nenhuma seleção ativa. Essas ferramentas sempre se comportam como se a imagem inteira fosse a seleção ativa.

Enquanto seleciona uma região, você pode pressionar e segurar a tecla **Shift** para fazer uma seleção proporcional (quadrada). Caso contrário, a seleção não será restrita.

#### <a name="resize-selections"></a>Redimensionar seleções

Depois de selecionar uma região, você poderá redimensioná-la ou ao seu conteúdo de imagem alterando o tamanho do marcador de seleção. Enquanto redimensiona a região selecionada, você pode usar as seguintes teclas modificadoras para alterar o comportamento da região selecionada ao redimensioná-la:

**Ctrl** – copia o conteúdo da região selecionada antes que ela seja redimensionada. Isso deixa a imagem original intacta enquanto a cópia é redimensionada.

**Shift** – redimensiona a região selecionada proporcionalmente ao tamanho original.

**Alt** – altera o tamanho da região da seleção. Isso deixa a imagem sem modificações.

A tabela a seguir descreve as combinações de teclas modificadoras válidas:

|Ctrl|Shift|Alt|Descrição|
|----------|-----------|---------|-----------------|
||||Redimensiona o conteúdo da região selecionada.|
||**Shift**||Redimensiona proporcionalmente o conteúdo da região selecionada.|
|||**Alt**|Redimensiona a região selecionada. Isso define uma nova região de seleção.|
||**Shift**|**Alt**|Redimensiona proporcionalmente a região selecionada. Isso define uma nova região de seleção.|
|**Ctrl**|||Copia e redimensiona o conteúdo da região selecionada.|
|**Ctrl**|**Shift**||Copia e redimensiona proporcionalmente o conteúdo da região selecionada.|

### <a name="tool-properties"></a>Propriedades da ferramenta

Embora uma ferramenta esteja selecionada, você pode usar a janela **Propriedades** para especificar os detalhes sobre como isso afeta a imagem. Por exemplo, você pode definir a espessura da ferramenta **Lápis** ou a cor da ferramenta **Pincel**.

Você pode definir uma cor de primeiro plano e uma cor da tela de fundo. Ambos dão suporte a um canal alfa para fornecer opacidade definida pelo usuário. As configurações se aplicam a todas as ferramentas. Se você usar um mouse, o botão esquerdo do mouse corresponderá à cor de primeiro plano e o botão direito do mouse corresponde à cor da tela de fundo.

A tabela a seguir descreve as propriedades da ferramenta:

|Ferramenta|Propriedades|
|----------|----------------|
|Todas as ferramentas e seleções|**Girar por**<br /> Define a quantidade, em graus, que o efeito da seleção ou ferramenta é girado no sentido horário.|
|**Lápis**, **Pincel**, **Spray**, **Borracha**|**Espessura**<br /> Define o tamanho da área afetada pela ferramenta.|
|**Texto**|**Antialias**<br /> Desenha o texto com bordas suavizadas. Isso fornece ao texto uma aparência mais suave.<br /><br /> **Valor**<br /> O texto a ser desenhado.<br /><br /> **Fonte**<br /> A fonte usada para desenhar o texto.<br /><br /> **Size**<br /> O tamanho do texto.<br /><br /> **Negrito**<br /> Transforma a fonte em negrito.<br /><br /> **Itálico**<br /> Transforma a fonte em itálico.<br /><br /> **Sublinhado**<br /> Transforma a fonte em sublinhado.|
|**Primitivo 2D**|**Antialias**<br /> Desenha primitivos com bordas suavizadas. Isso concede ao texto uma aparência mais suave.<br /><br /> **Espessura**<br /> Define a espessura da linha de que forma o limite do primitivo.<br /><br /> **Raio X**<br /> (Somente retângulo arredondado) Define o raio de arredondamento para as bordas superior e inferior do primitivo.<br /><br /> **Raio Y**<br /> (Somente retângulo arredondado) Define o raio de arredondamento para as bordas esquerda e direita do primitivo.|
|**Lápis**, **Pincel**, **Spray**, **Primitivo 2D**|**Canais**<br /> Habilita ou desabilita os canais de cor específicos para exibição e desenho. Se a **Exibição** for definida como um canal de cor específico, esse canal estará visível na imagem; caso contrário, ele não será visível. Se **Desenhar** estiver definido para um canal de cor específico, tal canal será afetado por operações de desenho; caso contrário, ele não será.|
|**Seleção de Varinha**, **Preenchimento**|**Tolerância**<br /> Define a diferença máxima entre cores adjacentes dentro da qual elas são consideradas semelhantes, para que cores menos ou mais semelhantes façam parte da região afetada ou selecionada. Por padrão, o valor é 32, o que significa que pixels adjacentes em 32 tons (mais claros ou mais escuros) da cor original são considerados como parte da região.|

## <a name="keyboard-shortcuts"></a>Atalhos de teclado

|Comando|Atalhos de teclado|
|-------------| - |
|Mudar para o modo **Selecionar**|**S**|
|Mudar para o modo **Zoom**|**Z**|
|Mudar para o modo **Panorâmico**|**K**|
|Selecionar tudo|**Ctrl**+**A**|
|Excluir a seleção atual|**Excluir**|
|Cancelar a seleção atual|**Esc** (Escape)|
|Ampliar|**Ctrl**+**Botão de rolagem do mouse para frente**<br /><br /> **Ctrl**+**PageUp**<br /><br /> Sinal de adição (**+**)|
|Reduzir|**Ctrl**-**Botão de rolagem do mouse para trás**<br /><br /> **Ctrl**-**PageDown**<br /><br /> Sinal de subtração (**-**)|
|Movimentar a imagem para cima em panorama|**Botão de rolagem do mouse para trás**<br /><br /> **PageDown**|
|Movimentar a imagem para baixo em panorama|**Botão de rolagem do mouse para frente**<br /><br /> **PageUp**|
|Movimentar a imagem para a esquerda em panorama|**Shift**+**Botão de rolagem do mouse para trás**<br /><br /> **Botão de rolagem do mouse para a esquerda**<br /><br /> **Shift**+**PageDown**|
|Movimentar a imagem para a direita em panorama|**Shift**+**Botão de rolagem do mouse para frente**<br /><br /> **Botão de rolagem do mouse para a direita**<br /><br /> **Shift**+**PageUp**|
|Aplicar zoom para o tamanho real|**Ctrl**+**0** (zero)|
|Ajustar a imagem à janela|**Ctrl**+**G**, **Ctrl**+**F**|
|Ajustar a imagem à largura da janela|**Ctrl**+**G**, **Ctrl**+**I**|
|Ativar/desativar grade|**Ctrl**+**G**, **Ctrl**+**G**|
|Recortar imagem para a seleção atual|**Ctrl**+**G**, **Ctrl**+**C**|
|Exibir próximo nível de MIP (mais detalhes)|**Ctrl**+**G**, **Ctrl**+**6**|
|Exibir nível anterior de MIP (menos detalhes)|**Ctrl**+**G**, **Ctrl**+**7**|
|Ativar/desativar canal de cor vermelha|**Ctrl**+**G**, **Ctrl**+**1**|
|Ativar/desativar canal de cor verde|**Ctrl**+**G**, **Ctrl**+**2**|
|Ativar/desativar canal de cor azul|**Ctrl**+**G**, **Ctrl**+**3**|
|Ativar/desativar o canal alfa (transparência)|**Ctrl**+**G**, **Ctrl**+**4**|
|Ativar/desativar o padrão quadriculado alfa|**Ctrl**+**G**, **Ctrl**+**B**|
|Mudar para a ferramenta Seleção Irregular|**L**|
|Mudar para a ferramenta Seleção de Varinha|**M**|
|Mudar para a ferramenta Lápis|**P**|
|Mudar para a ferramenta Pincel|**B**|
|Mudar para a ferramenta Preenchimento|**F**|
|Mudar para a ferramenta Borracha|**E**|
|Mudar para a ferramenta Texto|**T**|
|Mudar para a ferramenta Seleção de Cor (conta-gotas)|**I**|
|Move a seleção ativa e seu conteúdo.|Teclas de **direção**.|
|Redimensiona a seleção ativa e seu conteúdo.|**Ctrl**+**teclas de** direção|
|Move a seleção ativa, mas não seu conteúdo.|**Shift**+**teclas de** direção|
|Redimensiona a seleção ativa, mas não seu conteúdo.|**Shift**+**Ctrl**+**teclas de** direção|
|Confirmar a camada atual|**Return**|
|Diminuir a espessura da ferramenta|**[**|
|Aumentar a espessura da ferramenta|**]**|

## <a name="related-topics"></a>Tópicos relacionados

|Título|Descrição|
|-----------|-----------------|
|[Trabalhando com ativos 3D para jogos e aplicativos](../designers/working-with-3-d-assets-for-games-and-apps.md)|Fornece uma visão geral das ferramentas que você pode usar no Visual Studio para trabalhar com recursos gráficos, como texturas e imagens, modelos 3D e efeitos de sombreamento.|
|[Editor de modelos](../designers/model-editor.md)|Descreve como usar o Editor de Modelos do Visual Studio para trabalhar com modelos 3D.|
|[Designer de sombreador](../designers/shader-designer.md)|Descreve como usar o Designer de Sombreador do Visual Studio para trabalhar com sombreadores.|