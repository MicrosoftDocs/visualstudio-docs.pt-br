---
title: Layout para o Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: c19e3022-047c-43b6-a046-a82717efed4f
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 638cfc29ed2aa05a8576a2244b81f0625453076d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49816671"
---
# <a name="layout-for-visual-studio"></a>Layout para o Visual Studio
A maioria das caixas de diálogo do Visual Studio estão [layout de caixa de diálogo do utilitário](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_UtilityDialogLayout), que são o unthemed esse padrão de acompanhamento de caixas de diálogo [princípios de layout de caixa de diálogo de área de trabalho do Windows](/windows/desktop/uxguide/win-dialog-box). Como o Visual Studio moverá atualizar sua interface do usuário, algumas das caixas de diálogo mais proeminentes têm um novo design que estabelece a eles como definição de produto experiências. Eles [layout da caixa de diálogo com tema](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_ThemedDialogLayout) têm uma aparência com tema.  
  
##  <a name="BKMK_UtilityDialogLayout"></a> Layout da caixa de diálogo de utilitário  
  
-   Todos os controles dentro de uma caixa de diálogo do utilitário devem começar na parte superior/esquerda e para baixo de fluxo.  
  
-   Nunca center controles em uma caixa de diálogo para preencher uma grande área.  
  
-   Use a fonte de ambiente para todo o texto de caixa de diálogo. Ao escrever uma especificação de visual, especifica a fonte de ambiente em vez de selecionar uma fonte específica e tamanho. Ver [a fonte de ambiente](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont).  
  
-   Para usar espaçamento de controle consistente e posicionamento para dar suporte a meta para qualidade na habilidade.  
  
-   Caixas de diálogo podem se tornar mais complexas de um grande número de controles, um juxtaposition exclusivo dos controles ou ambos. Essas situações complexas, permitir espaço suficiente entre os agrupamentos de controle para dar ao usuário um fluxo lógico para analisar.  
  
### <a name="utility-dialog-layout-examples"></a>Exemplos de layout de caixa de diálogo de utilitário  
 Todas as dimensões são expressas em pixels.  
  
 ![Espaçamento de caixa de diálogo para rótulos acima dos controles](../../extensibility/ux-guidelines/media/0801-a_utilityspacingabove.png "0801 a_UtilitySpacingAbove")  
  
 **Figura 08.01-r: Diretrizes para caixas de diálogo de utilitário com rótulos acima dos controles de espaçamento**  
  
 ![Espaçamento de caixa de diálogo para rótulos para a esquerda dos controles](../../extensibility/ux-guidelines/media/0801-b_utilityspacingleft.png "0801 b_UtilitySpacingLeft")  
  
 **Figura 08.01-b: Diretrizes para as caixas de diálogo do utilitário com rótulos à esquerda dos controles de espaçamento**  
  
### <a name="layout-details"></a>Detalhes de layout  
  
#### <a name="margins"></a>Margens  
  
-   Todas as caixas de diálogo devem ter uma borda de 12 pixels ao redor de todas as bordas.  
  
-   Margens de um quadro de grupo devem ser 9 pixels da borda do quadro.  
  
-   Margens de um controle guia devem ser 6 pixels da borda do controle guia.  
  
#### <a name="command-buttons"></a>Botões de comando  
  
- Botões de comando operam no quadro da caixa de diálogo, não no conteúdo. Eles devem ser colocados na parte inferior direita e devem ter espaço suficiente variável acima para definir os botões separadas.  
  
- Se houver botões horizontais que operam na caixa de diálogo, a configuração de botão de comando alternativo é uma pilha vertical na parte superior direita. Ver [botões de comando interiores](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_InteriorCommandButtons) abaixo.  
  
- O espaço à esquerda dos botões de comando (esquerda/central inferior da caixa de diálogo) é considerado parte da "faixa" dos controles de operação da caixa de diálogo. A única coisa que deve atrapalham a que o espaço é um link de Ajuda que é relevante para a tarefa geral ou a caixa de diálogo.  
  
- Botões de comando devem ser 75 x 23 pixels.  
  
- Botões de comando devem ser 6 pixels de distância.  
  
  ![Alinhamento de botão básica](../../extensibility/ux-guidelines/media/0801-c_buttonalign.png "0801 c_ButtonAlign")  
  
  **Figura 08.01-c: Alinhamento de botão básica**  
  
#### <a name="labels"></a>Rótulos  
  
-   Alinhar à esquerda todos os rótulos.  
  
-   Para rótulos que ficam acima de um controle, eles devem Alinhar à esquerda precisamente com o controle abaixo dele e a parte inferior do rótulo deve ser 5 pixels acima da parte superior de outro controle (por exemplo, uma caixa de combinação).  
  
-   Para rótulos que ficam à esquerda dos controles, a largura mínima entre o rótulo e o controle de entrada é de 10 pixels. Uma segunda coluna implícita deve ser estabelecida para alinhar as caixas de texto, caixas de combinação ou outros controles.  
  
-   Rótulos diferenciam maiusculas de minúsculas e são seguidos por dois-pontos. Ver [estilo de texto](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle).  
  
#### <a name="distance-between-controls"></a>Distância entre os controles  
 Controles de pilha razoavelmente. Não há nenhuma diretriz absoluto para o espaçamento entre controles de gráfico empilhados. Abruptas entre os controles podem variar ligeiramente entre as caixas de diálogo. O espaçamento recomendado é 20 pixels para um controle vertical/pares e 9 pixels para um controle horizontal/pares. O espaçamento mínimo do controle para pares horizontais é 6 pixels.  
  
 ![Recomendado a distância entre os controles](../../extensibility/ux-guidelines/media/0801-d_controldistance.png "0801 d_ControlDistance")  
  
 **Figura 08.01-d: Recomendações para a distância entre os controles**  
  
#### <a name="control-indentation"></a>Recuo do controle  
 Quando os controles são aninhados, alinhe controles internos horizontalmente com a borda esquerda do controle acima, geralmente o rótulo.  
  
 ![Alinhamento do controle de aninhado](../../extensibility/ux-guidelines/media/0801-e_controlalign.png "0801 e_ControlAlign")  
  
 **Figura 08.01-e: Alinhamento do controle de aninhado**  
  
#### <a name="control-width"></a>Largura do controle  
 A largura de uma caixa de texto ou outros controles semelhantes deve ter menos de entrada média para o campo. A palavra em inglês média é cinco caracteres. Por exemplo, uma caixa de texto que requer um nome de caminho longo deve ser, desde que permite que o layout horizontal, enquanto uma lista suspensa de nomes de plataforma somente devem ser um comprimento que permite a entrada mais longa.  
  
#### <a name="helper-text"></a>Texto de auxiliar  
  
-   Uma caixa de diálogo pode exibir o texto de auxiliar que fornece mais informações sobre a finalidade da caixa de diálogo. Isso normalmente fica na parte superior e pode ser frases de 1 a 2.  
  
-   O comprimento da linha deve ser uma largura à vontade para um usuário analisar e ler. Uma caixa de diálogo médio deve ser não mais do que 550 pixels de largura.  
  
####  <a name="BKMK_InteriorCommandButtons"></a> Botões de comando interior  
 Caixas de diálogo mais complexos, um controle interno pode ter seus próprios botões relacionados, que podem afetar onde se encontram botões de confirmação da caixa de diálogo.  
  
- Use um alinhamento vertical (coluna) do interior botões quando **Okey**/**Cancelar** são orientado horizontalmente no canto inferior direito.  
  
- Use um alinhamento horizontal (linha) do interior botões quando **Okey**/**Cancelar** são orientados verticalmente no canto superior direito. Essa situação é menos comum.  
  
- Tamanho do botão interior deve ter como destino o tamanho do botão padrão de 75 x 23 pixels, correspondência de tamanho de **Okey**/**Cancelar** botões quando possível. Se o rótulo do botão faz com que o botão exceder o tamanho do botão padrão, os outros botões nesse conjunto devem ser alinhadas com que o tamanho mais amplo.  
  
  ![Botões horizontal Okey e Cancel](../../extensibility/ux-guidelines/media/0801-f_horizokcan.png "0801 f_HorizOKCan")  
  
  **Figura 08.01-f: Botões de Interior Vertical com Okey horizontal/Cancelar**  
  
  ![Botões Okey vertical e Cancel](../../extensibility/ux-guidelines/media/0801-g_vertokcan.png "0801 g_VertOKCan")  
  
  **Figura 08.01-g: Botões de interiores Horizontal com Okey vertical/Cancelar**  
  
#### <a name="browse-button"></a>[Procurar...] botão  
 **[Procurar...]**  botões que seguem uma caixa de texto devem esclarecer "Procurar..." por completo, incluindo o botão de reticências. Se o espaço é forte ou haja diversas **[procurar...]**  botões na tela, o botão podem ser reduzido para apenas o botão de reticências.  
  
##  <a name="BKMK_ThemedDialogLayout"></a> Layout da caixa de diálogo com temas  
 As caixas de diálogo com temas no Visual Studio têm uma aparência mais clara e oferecem mais espaço em branco. Tipografia fornece mais ênfase e juros, oferecendo mais aberto de espaçamento entre linhas e uma variação de tamanhos de fonte e pesos. Sempre que possível, as barras de título e chrome foram reduzidas ou removidas. O layout dessas caixas de diálogo deve seguir esse padrão básico:  
  
1.  O plano de fundo da caixa de diálogo é branco.  
  
2.  Há uma borda da regra 1 pixel em um valor intermediário cinza.  
  
3.  O título da caixa de diálogo não reside em uma barra de título, mas fornece interesse visual e ênfase em um tamanho maior de ponto. (Consulte a seção de tamanho de fonte no [estilo de texto](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle).)  
  
4.  Juntamente com o texto adicional, como uma descrição de rótulos devem ser **fonte de ambiente + negrito**.  
  
5.  Interiores colunas são separadas por uma regra de 1 pixel em cinza claro.  
  
6.  Links de padrão têm sem sublinhado. Passe o mouse e os estados pressionados tem uma alteração de cor mais o sublinhado.  
  
7.  Botões de confirmação (como **Okey**/**Cancelar**) ficam no canto inferior direito.  
  
### <a name="themed-dialog-layout-examples"></a>Exemplos de layout de caixa de diálogo com temas  
 ![Layout da caixa de diálogo com tema](../../extensibility/ux-guidelines/media/0801-h_themeddialog.png "0801 h_ThemedDialog")  
  
 **Figura 08.01-h: Caixa de diálogo com tema**  
  
 ![Dimensões da caixa de diálogo com tema](../../extensibility/ux-guidelines/media/0801-i_themeddialogdimensions.png "0801 i_ThemedDialogDimensions")  
  
 **Figura 08.01-i: Caixa de diálogo de tema – dimensões**  
  
 ![Fontes de caixa de diálogo com tema](../../extensibility/ux-guidelines/media/0801-j_themeddialogfonts.png "0801 j_ThemedDialogFonts")  
  
 **Figura 08.01-j: Caixa de diálogo de tema – fontes**  
  
 ![Cores de tema de caixa de diálogo](../../extensibility/ux-guidelines/media/0801-k_themeddialogcolors.png "0801 k_ThemedDialogColors")  
  
 **Figura 08.01-k: Caixa de diálogo de tema-cores**  
  
## <a name="see-also"></a>Consulte também  
 [Padrões de aplicativo para o Visual Studio](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)   
 [Controles (Windows)](/windows/desktop/uxguide/controls)   
 [Caixas de diálogo (Windows)](/windows/desktop/uxguide/win-dialog-box)