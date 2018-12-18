---
title: Editor de Imagens | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.graphics.designer.imageeditor
- vs.graphics.imageeditor
ms.assetid: fc71d502-c548-4863-8afc-12a1d3ec90d4
caps.latest.revision: 47
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 748d58ec8446841242fdf7b5b990eebe90df5ba1
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49185764"
---
# <a name="image-editor"></a>Editor de imagem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este documento descreve como trabalhar com o Editor de Imagens do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para exibir e modificar os recursos de textura e imagens.  
  
 Você pode usar o Editor de Imagens para trabalhar com os tipos de formatos de imagem e com textura avançada que são usados no desenvolvimento de aplicativos DirectX, incluindo o suporte para formatos de arquivos de imagem populares e codificações de cor, recursos como canais alfa e mapeamento de MIP e muitos dos formatos de textura altamente comprimidos e de aceleração de hardware com suporte no DirectX.  
  
## <a name="supported-formats"></a>Formatos com suporte  
 O Editor de Imagens dá suporte a esses formatos de imagem:  
  
|Nome do formato|Extensão de nome de arquivo|  
|-----------------|-------------------------|  
|Formato PNG (Portable Network Graphics)|.png|  
|JPEG|.jpg, .jpeg, .jpe, .jfif|  
|Direct Draw Surface|.dds|  
|Formato GIF (Graphics Interchange Format)|.gif|  
|Bitmap|.bmp, .dib|  
|Formato TIFF|.tif, .tiff|  
|Formato TGA (Targa)|.tga|  
  
## <a name="getting-started"></a>Introdução  
 Esta seção descreve como adicionar uma imagem ao seu projeto do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e configurá-lo para os seus requisitos.  
  
#### <a name="to-add-an-image-to-your-project"></a>Para adicionar uma imagem ao seu projeto  
  
1.  No **Gerenciador de Soluções**, abra o menu de atalho do projeto ao qual você deseja adicionar a imagem e selecione **Adicionar**, **Novo Item**.  
  
2.  Na caixa de diálogo **Adicionar Novo Item**, em **Instalado**, selecione **Gráficos** e escolha um formato de arquivo apropriado para a imagem. Para obter informações sobre como escolher um formato de arquivo com base nos seus requisitos, consulte a seção a seguir.  
  
3.  Especifique o **Nome** do arquivo de imagem e a **Localização** na qual você deseja que ele seja criado.  
  
4.  Escolha o botão **Adicionar**.  
  
### <a name="choosing-the-image-format"></a>Escolhendo o formato da imagem  
 Dependendo de como você planeja usar a imagem, determinados formatos de arquivo podem ser mais apropriados do que outros. Por exemplo, alguns formatos podem não dar suporte a um recurso que você precisa, como transparência ou um formato de cor específico ou então pode não oferecer uma compactação adequada para o tipo de conteúdo de imagem que você planeja.  
  
 As informações a seguir podem ajudar a escolher um formato de imagem que atenda às suas necessidades.  
  
 **Imagem de bitmap (.bmp)**  
 O formato de imagem de bitmap. Um formato de imagem não compactado que dá suporte a cores de 24 bits. O formato de bitmap não dá suporte a transparências.  
  
 **Imagem GIF (.gif)**  
 O formato de imagem GIF (Graphics Interchange Format). Um formato de imagem compactados em LZW sem perdas que dá suporte a até 256 cores. Inadequado para fotografias e imagens com uma quantidade significativa de detalhes de cores, porém fornece boas taxas de compactação para imagens com poucas cores que têm um alto grau de coerência de cor.  
  
 **Imagem JPG (.jpg)**  
 O formato de imagem JPEG (Joint Photographic Experts Group). Um formato de imagem altamente compactado e com perdas que dá suporte a cores de 24 bits e é adequado compactação de imagens de uso geral com um alto grau de coerência de cor.  
  
 **Imagem PNG (.png)**  
 O formato de imagem PNG (Portable Network Graphics). Um formato de imagem sem perdas e moderadamente compactado que dá suporte a cores de 24 bits e transparência alfa. Ele é adequado para imagens naturais e artificiais, mas não oferece taxas de compactação tão boas quanto formatos com perda como JPG ou GIF.  
  
 **Imagem TIFF (.tif)**  
 O formato de imagem TIFF (ou TIF). Um formato de imagem flexível que dá suporte a vários esquemas de compactação.  
  
 **Textura DDS (.dds)**  
 O formato de textura DDS (DirectDraw Surface). Um formato de textura com perdas e altamente compactado que dá suporte a cores de 24 bits e transparência alfa. Suas taxas de compactação chegam a até 8:1. Ele se baseia na compactação de Textura S3, que pode ser descompactada no hardware gráfico.  
  
 **Imagem TGA (.tga)**  
 O formato de imagem TGA (Truevision Graphics Adapter, também conhecido como Targa). Um formato de imagem compactado em RLE e sem perda que dá suporte a imagens com cores mapeadas (paleta de cores) e diretas de cores de até 24 bits e transparência alfa. Inadequado para fotografias e imagens com uma quantidade significativa de detalhes de cores, porém fornece boas taxas de compactação para imagens com longas extensões de cores idênticas.  
  
### <a name="configuring-the-image"></a>Configurando a imagem  
 Antes de começar a trabalhar com a imagem que você acabou de criar, você pode alterar sua configuração padrão. Por exemplo, você pode alterar suas dimensões ou o formato de cores que ela usa. Para obter informações sobre como configurar essas e outras propriedades da imagem, consulte [Propriedades da imagem](#ImageProperties).  
  
> [!NOTE]
>  Antes de salvar seu trabalho, verifique se a propriedade **Formato de Cor** foi definida se você quiser usar um formato de cor específico. Se o formato de arquivo der suporte à compactação, você poderá ajustar as configurações de compactação quando salvar o arquivo pela primeira vez ou ao escolher **Salvar como**.  
  
## <a name="working-with-the-image-editor"></a>Trabalhando com o Editor de Imagens  
 Essa seção descreve como usar o Editor de Imagens para modificar texturas e imagens.  
  
### <a name="image-editor-toolbars"></a>Barras de ferramentas do Editor de Imagens  
 As barras de ferramentas do Editor de Imagens contêm comandos que ajudam a trabalhar com imagens.  
  
 Comandos que afetam o estado do Editor de Imagens encontram-se na barra de ferramentas **Modo do Editor de Imagens** junto com os comandos avançados. A barra de ferramentas está localizada na borda superior da área de design do Editor de Imagens. As ferramentas de desenho encontram-se na barra de ferramentas **Editor de Imagens** na borda esquerda da área de design do Editor de Imagens.  
  
 Esta é a barra de ferramentas do **Modo do Editor de Imagens**:  
  
 ![A barra de ferramentas modal do Editor de Imagens.](../designers/media/digit-tre-modal-toolbar.png "Digit-TRE-Modal-Toolbar")  
  
 Esta tabela descreve os itens na barra de ferramentas **Modo do Editor de Imagens**, que são listados na ordem em que aparecem, da esquerda para a direita.  
  
|Item da barra de ferramentas|Descrição|  
|------------------|-----------------|  
|**Selecionar**|Habilita a seleção de uma região retangular de uma imagem. Depois de selecionar uma região, você poderá recortar, copiar, mover, ajustar escala, girar, inverter ou excluir. Quando há uma seleção ativa, as ferramentas de desenho só afetam a região selecionada.|  
|**Seleção Irregular**|Habilita a seleção de uma região irregular de uma imagem. Depois de selecionar uma região, você poderá recortar, copiar, mover, ajustar escala, girar, inverter ou excluir. Quando há uma seleção ativa, as ferramentas de desenho só afetam a região selecionada.|  
|**Seleção de Varinha**|Habilita a seleção de uma região de cor semelhante de uma imagem. A *tolerância*, ou seja, a diferença máxima entre cores adjacentes na qual elas são consideradas semelhantes, pode ser configurada para incluir um intervalo maior ou menor de cores semelhantes. Depois de selecionar uma região, você poderá recortar, copiar, mover, ajustar escala, girar, inverter ou excluir. Quando há uma seleção ativa, as ferramentas de desenho só afetam a região selecionada.|  
|**Panorâmica**|Habilita a movimentação da imagem em relação ao quadro de janela. No modo **Panorâmica**, selecione um ponto na imagem e mova-o.<br /><br /> Você pode ativar temporariamente o modo **Panorâmica** mantendo pressionada a tecla Ctrl.|  
|**Zoom**|Habilita a exibição de mais ou menos detalhes da imagem em relação ao quadro de janela. No modo **Aplicar Zoom**, selecione um ponto na imagem e mova-o para a direita ou para baixo para ampliar ou para a esquerda ou para cima para reduzir.<br /><br /> Você pode ampliar ou reduzir mantendo Ctrl pressionado enquanto você use a roda do mouse ou pressiona o sinal de adição (+) ou de subtração (-).|  
|**Aplicar Zoom para o Tamanho Real**|Exibe a imagem usando uma relacionamento 1:1 entre os pixels da imagem e os pixels da tela.|  
|**Aplicar zoom para ajustar**|Exibe a imagem completa no quadro de janela.|  
|**Zoom para a largura**|Exibe a largura completa da imagem no quadro de janela.|  
|**Grade**|Habilita ou desabilita a grade que mostra os limites de pixel. A grade pode não aparecer até você ampliar a imagem.|  
|**Exibição do Próximo Nível de MIP**|Ativa o próximo nível maior de MIP em uma cadeia de mapas MIP. O nível de MIP ativo é exibido na área de design. Este item só está disponível para texturas que têm níveis de MIP.|  
|**Exibir um Nível de MIP Anterior**|Ativa o próximo nível menor de MIP em uma cadeia de mapas MIP. O nível de MIP ativo é exibido na área de design. Este item só está disponível para texturas que têm níveis de MIP.|  
|**Canal vermelho**<br /><br /> **Canal verde**<br /><br /> **Canal azul**<br /><br /> **Canal alfa**|Habilita ou desabilita o canal da cor específica. **Observação:** habilitando ou desabilitando sistematicamente os canais de cor, você pode isolar problemas relacionados a um ou mais deles. Por exemplo, você poderia identificar a transparência alfa incorreta.|  
|**Tela de Fundo**|Habilita ou desabilita a exibição da tela de fundo através das partes transparentes da imagem. Você pode configurar como a tela de fundo é exibida escolhendo entre estas opções:<br /><br /> **Quadriculado**<br /> Usa uma cor verde junto com a cor da tela de fundo especificada para exibir a tela de fundo como um padrão quadriculado. Você pode usar essa opção para ajudar a tornar as partes transparentes da imagem mais visíveis.<br /><br /> Tela de fundo branco<br /> Usa a cor branca para exibir a tela de fundo.<br /><br /> Tela de fundo preto<br /> Usa a cor preta para exibir a tela de fundo.<br /><br /> Animar a tela de fundo<br /> Movimenta o padrão quadriculado lentamente em panorâmica. Você pode usar essa opção para ajudar a tornar as partes transparentes da imagem mais visíveis.|  
|**Propriedades**|Alterna entre abrir e fechar a janela **Propriedades**.|  
|**Avançado**|Contém comandos e opções adicionais.<br /><br /> **Filtros**<br /><br /> Fornece vários filtros de imagem comuns: **Preto e branco**, **Desfoque**, **Iluminar**, **Escurecer**, **Detecção de borda**, **Colocar em alto-relevo**, **Inverter cores**, **Ripple**, **Tom sépia** e **Ajustar nitidez**.<br /><br /> **Mecanismos Gráficos**<br /><br /> **Renderizar com o D3D11**<br /> Use o Direct3D 11 para renderizar a área de design do Editor de Imagens.<br /><br /> **Renderizar com o D3D11WARP**<br /> Use o Direct3D 11 WARP (Windows Advanced Rasterization Platform) para renderizar a área de design do Editor de Imagens.<br /><br /> **Ferramentas**<br /><br /> **Inverter Horizontalmente**<br /> Transpõe a imagem ao redor do seu eixo horizontal, também chamado x.<br /><br /> **Inverter Verticalmente**<br /> Transpõe a imagem ao redor do seu eixo vertical, também chamado y.<br /><br /> **Gerar Mips**<br /> Gera os níveis de MIP para uma imagem. Se os níveis de MIP já existirem, eles serão recriados do maior nível de MIP. Quaisquer alterações feitas aos níveis de MIP menores serão perdidas. Para salvar os níveis de MIP que você tiver gerado, você deverá usar o formato .dds para salvar a imagem.<br /><br /> **Exibir**<br /><br /> **Taxa de Quadros**<br /> Quando habilitado exibe a taxa de quadros no canto superior direito da área de design. A taxa de quadros é o número de quadros desenhados por segundo. **Dica:** você pode escolher o botão **Avançado** para executar novamente o último comando.|  
  
 Esta é a barra de ferramentas do **Editor de Imagens**.  
  
 ![Barra de ferramentas do Editor de Imagens](../designers/media/digit-tre-toolbar.png "Digit-TRE-Toolbar")  
  
 A tabela a seguir descreve os itens da barra de ferramentas **Editor de Imagens**, que são listados na ordem em que aparecem, de cima para baixo.  
  
|Item da barra de ferramentas|Descrição|  
|------------------|-----------------|  
|**Lápis**|Usa a seleção de cor ativa para desenhar um traço com alias. Você pode definir a cor e a espessura do traço na janela **Propriedades**.|  
|**Pincel**|Usa a seleção de cor ativa para desenhar um traço suavizado. Você pode definir a cor e a espessura do traço na janela **Propriedades**.|  
|**Spray**|Usa a seleção de cor ativa para desenhar um traço suavizado que se mescla à imagem e se torna mais saturado com o decorrer do tempo. Você pode definir a cor e a espessura do traço na janela **Propriedades**.|  
|**Conta-gotas**|Define a seleção de cor ativa para a cor do pixel selecionado.|  
|**Preenchimento**|Usa a seleção de cor ativa para preencher uma região da imagem. A região afetada é definida como o pixel em que o preenchimento é aplicado, junto com cada pixel conectado a ele por pixels da mesma cor e que são a mesma cor em si. Se o preenchimento for aplicado em uma seleção ativa, a região afetada ficará restringida pela seleção.<br /><br /> Por padrão, a seleção de cor ativa é mesclada com a região afetada da imagem de acordo com seu componente alfa. Para usar a seleção de cor ativa para substituir a região afetada, mantenha pressionada a tecla Shift ao usar a ferramenta de preenchimento.|  
|**Borracha**|Define pixels para a cor totalmente transparente se a imagem der suporte a um canal alfa. Caso contrário, define os pixels para a cor da tela de fundo ativa.|  
|**Linha**, **Retângulo**, **Retângulo Arredondado**, **Elipse**|Desenha uma forma na imagem. Você pode definir a cor e a espessura da estrutura de tópicos na janela **Propriedades**.<br /><br /> Para desenhar um primitivo com altura e largura iguais, mantenha pressionada a tecla Shift enquanto desenha.|  
|**Texto**|Usa a seleção de cor de primeiro plano para desenhar o texto. A cor da tela de fundo é determinada pela seleção de cor da tela de fundo. Para uma tela de fundo transparente, o valor alfa da seleção da cor da tela de fundo deve ser 0. Quando a região de texto estiver ativa, você pode definir se o texto é desenhado com um traço suavizado ou pode definir o **Valor**, **Fonte**, **Tamanho** e o estilo — **Negrito**, **Itálico** ou **Sublinhado** — do texto na janela **Propriedades**. O conteúdo e a aparência do texto é finalizada quando a região de texto não está mais ativa.|  
|**Girar**|Gira a imagem 90 graus no sentido horário.|  
|**Cortar**|Corta a imagem para a seleção ativa.|  
  
### <a name="working-with-mip-levels"></a>Trabalhando com níveis de MIP  
 Alguns formatos de imagem — por exemplo, DirectDraw Surface (.dds) — dão suporte a níveis de MIP para LOD (Nível de Detalhe) de espaço de texturas. Para obter informações sobre como gerar e trabalhar com níveis de MIP, consulte [Como criar e modificar níveis de MIP](../designers/how-to-create-and-modify-mip-levels.md)  
  
### <a name="working-with-transparency"></a>Trabalhando com transparência  
 Alguns formatos de imagem — por exemplo, DirectDraw Surface (.dds) — dão suporte a transparência. Há várias maneiras de usar transparências, dependendo da ferramenta que você está usando. Para especificar o nível de transparência de uma seleção de cor, na janela **Propriedades**, defina o componente **A** (alfa) da seleção de cores. Veja aqui como a transparência é aplicada nos diferentes tipos de controle de ferramentas:  
  
|Ferramenta|Descrição|  
|----------|-----------------|  
|**Lápis**, **Pincel**, **Spray**, **Linha**, **Retângulo**, **Retângulo Arredondado**, **Elipse**, **Texto**|Para mesclar a seleção de cor ativa com a imagem na janela **Propriedades**, expanda o grupo de propriedades **Canais**, marque a caixa de seleção **Desenhar** no canal **Alfa** e desenhe normalmente.<br /><br /> Para desenhar usando a seleção de cor ativa e deixar o valor alfa da imagem em vigor, desmarque a caixa de seleção **Desenhar** do canal **Alfa** e, em seguida, desenhe normalmente.|  
|**Preenchimento**|Para mesclar a seleção de cor ativa junto com a imagem, escolha a área a ser preenchida.<br /><br /> Para usar a seleção de cor ativa, incluindo o valor do canal alfa, para substituir a imagem, mantenha a tecla Shift pressionada e escolha a área a ser preenchida.|  
  
###  <a name="ImageProperties"></a> Propriedades da imagem  
 Você pode usar a janela **Propriedades** para especificar várias propriedades da imagem. Por exemplo, você pode definir as propriedades Largura e Altura para redimensionar a imagem.  
  
 A tabela a seguir descreve as propriedades da imagem.  
  
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
|Fatia de Profundidade|A fatia de profundidade atual. Somente a primeira fatia pode ser exibida; todas as demais fatias são perdidas quando a imagem é salva.|  
  
> [!NOTE]
>  Como a propriedade **Girar por** se aplica a todas as ferramentas e regiões selecionadas, ela sempre aparece na parte inferior da janela **Propriedades** junto com outras propriedades de ferramenta. **Girar por** sempre é exibido, pois a imagem inteira é implicitamente selecionada quando não há nenhuma outra seleção ou ferramenta ativa. Para obter mais informações sobre a propriedade **Girar por**, consulte as [Propriedades de Ferramenta](#ToolProperties).  
  
#### <a name="resizing-images"></a>Redimensionando imagens  
 Essas são duas maneiras de redimensionar uma imagem. Em ambos os casos, o Editor de Imagens usa interpolação bi-linear para obter uma nova amostra da imagem.  
  
-   Na janela **Propriedades**, especifique os novos valores para as propriedades **Largura** e **Altura**.  
  
-   Selecione toda a imagem e use os marcadores de borda para redimensionar a imagem.  
  
### <a name="working-with-tools"></a>Trabalhando com ferramentas  
  
#### <a name="selected-regions"></a>Regiões selecionadas  
 As seleções no Editor de Imagens definem as regiões da imagem que estão ativas, ou seja, a região será afetada pelas ferramentas e transformações. Quando houver uma seleção ativa, as áreas fora da região selecionada não serão afetadas pela maioria das ferramentas e transformações. Se não houver uma seleção ativa, toda a imagem estará ativa.  
  
 A maioria das ferramentas —**Lápis**, **Pincel**, **Spray**, **Preenchimento**, **Borracha**e primitivos 2D — e transformações —**Girar**, **Cortar**, **Inverter cores**, **Inverter horizontalmente** e **Inverter verticalmente**— são restritos ou definidos pela seleção ativa. No entanto, algumas ferramentas —**Conta-gotas** e **Texto**— e transformações —**Gerar Mips**— não são afetadas por nenhuma seleção ativa; essas ferramentas sempre se comportam como se a imagem inteira fosse a seleção ativa.  
  
 Enquanto você estiver selecionando uma região, mantenha a tecla Shift pressionada ao fazer uma seleção proporcional (quadrada); caso contrário, a seleção não ficará restrita.  
  
##### <a name="resizing-selections"></a>Redimensionando seleções  
 Depois de selecionar uma região, você poderá redimensioná-la ou ao seu conteúdo de imagem alterando o tamanho do marcador de seleção. Enquanto redimensiona a região selecionada, você pode usar as seguintes teclas modificadoras para alterar o comportamento da região selecionada ao redimensioná-la (mantenha a tecla pressionada ao redimensionar).  
  
 Ctrl  
 Copia o conteúdo da região selecionada antes de ser redimensionada. Isso deixa a imagem original intacta enquanto a cópia é redimensionada.  
  
 Shift  
 Redimensiona a região selecionada em relação proporcional ao seu tamanho original.  
  
 Alt  
 Altera o tamanho da região de seleção. Isso deixa a imagem sem modificações.  
  
 Essas são as combinações de teclas modificadoras válidas:  
  
|Ctrl|Shift|Alt|Descrição|  
|----------|-----------|---------|-----------------|  
||||Redimensiona o conteúdo da região selecionada.|  
||Shift||Redimensiona proporcionalmente o conteúdo da região selecionada.|  
|||Alt|Redimensiona a região selecionada. Isso define uma nova região de seleção.|  
||Shift|Alt|Redimensiona proporcionalmente a região selecionada. Isso define uma nova região de seleção.|  
|Ctrl|||Copia e redimensiona o conteúdo da região selecionada.|  
|Ctrl|Shift||Copia e redimensiona proporcionalmente o conteúdo da região selecionada.|  
  
####  <a name="ToolProperties"></a> Propriedades da ferramenta  
 Embora uma ferramenta esteja selecionada, você pode usar a janela **Propriedades** para especificar os detalhes sobre como isso afeta a imagem. Por exemplo, você pode definir a espessura da ferramenta **Lápis** ou a cor da ferramenta **Pincel**.  
  
 Você pode definir uma cor de primeiro plano e uma cor da tela de fundo. Ambos dão suporte a um canal alfa para fornecer opacidade definida pelo usuário. As configurações se aplicam a todas as ferramentas. Se você usar um mouse, o botão esquerdo do mouse corresponderá à cor de primeiro plano e o botão direito do mouse corresponde à cor da tela de fundo.  
  
 A tabela a seguir descreve as propriedades da ferramenta.  
  
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
|-------------|------------------------|  
|Mudar para o modo **Selecionar**|S|  
|Mudar para o modo **Zoom**|Z|  
|Mudar para o modo **Panorâmico**|M|  
|Selecionar tudo|Ctrl+A|  
|Excluir a seleção atual|Excluir|  
|Cancelar a seleção atual|Escape|  
|Ampliar|Ctrl+Roda do mouse para frente<br /><br /> Ctrl+PageUp<br /><br /> Sinal de mais (+)|  
|Reduzir|Ctrl+Roda do mouse para trás<br /><br /> Ctrl-PageDown<br /><br /> Sinal de menos (-)|  
|Movimentar a imagem para cima em panorama|Roda do mouse para trás<br /><br /> PageDown|  
|Movimentar a imagem para baixo em panorama|Roda do mouse para frente<br /><br /> PageUp|  
|Movimentar a imagem para a esquerda em panorama|Shift+Roda do mouse para trás<br /><br /> Roda do mouse para a esquerda<br /><br /> Shift+PageDown|  
|Movimentar a imagem para a direita em panorama|Shift+Roda do mouse para frente<br /><br /> Roda do mouse para a direita<br /><br /> Shift+PageUp|  
|Aplicar zoom para o tamanho real|Ctrl+0 (zero)|  
|Ajustar a imagem à janela|Ctrl+G, Ctrl+F|  
|Ajustar a imagem à largura da janela|Ctrl+G, Ctrl+I|  
|Ativar/desativar grade|Ctrl+G, Ctrl+G|  
|Recortar imagem para a seleção atual|Ctrl+G, Ctrl+C|  
|Exibir próximo nível de MIP (mais detalhes)|Ctrl+G, Ctrl+6|  
|Exibir nível anterior de MIP (menos detalhes)|Ctrl+G, Ctrl+7|  
|Ativar/desativar canal de cor vermelha|Ctrl+G, Ctrl+1|  
|Ativar/desativar canal de cor verde|Ctrl+G, Ctrl+2|  
|Ativar/desativar canal de cor azul|Ctrl+G, Ctrl+3|  
|Ativar/desativar o canal alfa (transparência)|Ctrl+G, Ctrl+4|  
|Ativar/desativar o padrão quadriculado alfa|Ctrl+G, Ctrl+B|  
|Mudar para a ferramenta Seleção Irregular|L|  
|Mudar para a ferramenta Seleção de Varinha|M|  
|Mudar para a ferramenta Lápis|P|  
|Mudar para a ferramenta Pincel|B|  
|Mudar para a ferramenta Preenchimento|F|  
|Mudar para a ferramenta Borracha|E|  
|Mudar para a ferramenta Texto|T|  
|Mudar para a ferramenta Seleção de Cor (conta-gotas)|I|  
|Move a seleção ativa e seu conteúdo.|Teclas de direção.|  
|Redimensiona a seleção ativa e seu conteúdo.|Ctrl+Teclas de direção|  
|Move a seleção ativa, mas não seu conteúdo.|Shift+Teclas de direção|  
|Redimensiona a seleção ativa, mas não seu conteúdo.|Shift+Ctrl+Teclas de direção|  
|Confirmar a camada atual|Valor de|  
|Diminuir a espessura da ferramenta|[|  
|Aumentar a espessura da ferramenta|]|  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Trabalhando com ativos 3D para jogos e aplicativos](../designers/working-with-3-d-assets-for-games-and-apps.md)|Fornece uma visão geral das ferramenta que você pode usar no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para trabalhar com recursos gráficos, como texturas e imagens, modelos 3D e efeitos de sombreamento.|  
|[Editor de modelo](../designers/model-editor.md)|Descreve como usar o Editor de Modelos [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para trabalhar com modelos 3D.|  
|[Designer de Sombreador](../designers/shader-designer.md)|Descreve como usar o Designer de Sombreador do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para trabalhar com sombreadores.|



