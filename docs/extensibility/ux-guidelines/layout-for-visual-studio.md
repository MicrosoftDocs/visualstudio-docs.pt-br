---
title: Layout do Visual Studio | Microsoft Docs
description: Saiba mais sobre layout para caixas de diálogo do Visual Studio, incluindo caixas de diálogo desnecessários e novas caixas de diálogo que têm uma aparência com tema.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: c19e3022-047c-43b6-a046-a82717efed4f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e52b7b3fd620080b73e8d3de80672003ecb8fcf7
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900519"
---
# <a name="layout-for-visual-studio"></a>Layout para Visual Studio
A maioria das caixas de diálogo do Visual Studio são o [layout da caixa de diálogo do utilitário](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_UtilityDialogLayout), que são as caixas de diálogo destinadas que seguem princípios padrão de layout de caixa de diálogo do [Windows Desktop](/windows/desktop/uxguide/win-dialog-box). À medida que o Visual Studio muda para atualizar sua interface do usuário, algumas das caixas de diálogo mais proeminentes têm um novo design que as estabelece como experiências de definição de produto. Esse [layout de caixa de diálogo com tema](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_ThemedDialogLayout) tem uma aparência com tema.

## <a name="utility-dialog-layout"></a><a name="BKMK_UtilityDialogLayout"></a> Layout da caixa de diálogo do utilitário

- Todos os controles dentro de uma caixa de diálogo do utilitário devem começar na parte superior/esquerda e fluir para baixo.

- Nunca centraliza os controles em uma caixa de diálogo para preencher uma área grande.

- Use a fonte de ambiente para todo o texto da caixa de diálogo. Ao escrever uma especificação Visual, especifique a fonte do ambiente em vez de selecionar uma fonte e um tamanho específicos. Consulte [a fonte do ambiente](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont).

- Use espaçamento de controle consistente e posicionamento para dar suporte à meta de qualidade no habilidade.

- As caixas de diálogo podem se tornar mais complexas de um número maior de controles, um Juxtaposition exclusivo de controles ou ambos. Para essas situações complexas, permita o espaço adequado entre os agrupamentos de controle para dar ao usuário um fluxo lógico a ser analisado.

### <a name="utility-dialog-layout-examples"></a>Exemplos de layout da caixa de diálogo do utilitário
 Todas as dimensões são expressas como pixels.

 ![Espaçamento de diálogo para rótulos acima dos controles](../../extensibility/ux-guidelines/media/0801-a_utilityspacingabove.png "0801-a_UtilitySpacingAbove")

 **Figura 8, 1-a: diretrizes de espaçamento para caixas de diálogo do utilitário com rótulos acima**

 ![Espaçamento de caixa de diálogo para rótulos à esquerda dos controles](../../extensibility/ux-guidelines/media/0801-b_utilityspacingleft.png "0801-b_UtilitySpacingLeft")

 **Figura 8, 1-b: diretrizes de espaçamento para caixas de diálogo do utilitário com rótulos à esquerda dos controles**

### <a name="layout-details"></a>Detalhes do layout

#### <a name="margins"></a>Margens

- Todas as caixas de diálogo devem ter uma borda de 12 pixels em torno de todas as bordas.

- As margens dentro de um quadro de grupo devem ser de 9 pixels a partir da borda do quadro.

- As margens dentro de um controle guia devem ser de 6 pixels da borda do controle guia.

#### <a name="command-buttons"></a>Botões de comando

- Os botões de comando operam no quadro da caixa de diálogo, não no conteúdo. Eles devem ser colocados na parte inferior direita e devem ter espaço de variável suficiente acima para definir os botões separados de DISTINCT.

- Se houver botões horizontais que operam dentro da caixa de diálogo, a configuração do botão de comando alternativo será uma pilha vertical no canto superior direito. Consulte os [botões de comando do interior](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_InteriorCommandButtons) abaixo.

- O espaço à esquerda dos botões de comando (inferior esquerdo/centro da caixa de diálogo) é considerado parte da "banda" dos controles de operação da caixa de diálogo. A única coisa que deve invasor nesse espaço é um link de ajuda que é relevante para a tarefa ou caixa de diálogo geral.

- Os botões de comando devem ser 75x23 pixels.

- Os botões de comando devem ter 6 pixels de distância.

  ![Alinhamento do botão básico](../../extensibility/ux-guidelines/media/0801-c_buttonalign.png "0801-c_ButtonAlign")

  **Figura 8, 1-c: alinhamento do botão básico**

#### <a name="labels"></a>Rótulos

- Alinhar todos os rótulos à esquerda.

- Para rótulos que ficam acima de um controle, eles devem se alinhar precisamente com o controle abaixo dele e a parte inferior do rótulo deve ter 5 pixels acima da parte superior do outro controle (por exemplo, uma caixa de combinação).

- Para rótulos que ficam à esquerda dos controles, a largura mínima entre o rótulo e o controle de entrada é de 10 pixels. Uma segunda coluna implícita deve ser estabelecida para alinhar as caixas de texto, caixas de combinação ou outros controles.

- Os rótulos são letras de sentença e são seguidos por dois-pontos. Consulte [estilo de texto](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle).

#### <a name="distance-between-controls"></a>Distância entre controles
 Controles de pilha razoavelmente. Não há nenhuma diretriz absoluta para o espaçamento entre os controles empilhados. A rígida entre os controles pode variar ligeiramente entre as caixas de diálogo. O espaçamento recomendado é de 20 pixels para pares de rótulo/controle vertical e 9 pixels para pares de controle/rótulo horizontais. O espaçamento mínimo de controle para pares horizontais é de 6 pixels.

 ![Distância recomendada entre controles](../../extensibility/ux-guidelines/media/0801-d_controldistance.png "0801-d_ControlDistance")

 **Figura 8, 1-d: recomendações para distância entre controles**

#### <a name="control-indentation"></a>Recuo de controle
 Quando os controles são aninhados, alinha os controles internos horizontalmente com a borda esquerda do controle acima, geralmente o rótulo.

 ![Alinhamento de controle aninhado](../../extensibility/ux-guidelines/media/0801-e_controlalign.png "0801-e_ControlAlign")

 **Figura 8, 1-e: alinhamento de controle aninhado**

#### <a name="control-width"></a>Largura do controle
 A largura de uma caixa de texto ou outros controles semelhantes não deve ser maior do que a entrada média para o campo. A palavra em inglês médio é de cinco caracteres. Por exemplo, uma caixa de texto que requer um nome de caminho longo deve ser contanto que o layout horizontal permita, enquanto uma lista suspensa para nomes de plataforma deve ser apenas um comprimento que permita a entrada mais longa.

#### <a name="helper-text"></a>Texto do auxiliar

- Uma caixa de diálogo pode exibir o texto auxiliar que fornece mais informações sobre a finalidade da caixa de diálogo. Isso normalmente fica na parte superior e pode ser de 1-2 sentenças.

- O comprimento da linha deve ser uma largura confortável para um usuário analisar e ler. Uma caixa de diálogo média não deve ter mais de 550 pixels de largura.

#### <a name="interior-command-buttons"></a><a name="BKMK_InteriorCommandButtons"></a> Botões de comando interiores
 Em caixas de diálogo mais complexas, um controle interno pode ter seus próprios botões relacionados, o que pode afetar onde os botões de confirmação da caixa de diálogo estão localizados.

- Use um alinhamento vertical (coluna) de botões interiores quando **OK** / **Cancelar** é orientado horizontalmente no canto inferior direito.

- Use um alinhamento horizontal (linha) de botões interiores quando **OK** / **Cancelar** for verticalmente orientado no canto superior direito. Essa situação é menos comum.

- O tamanho do botão interior deve ser direcionado ao tamanho do botão padrão de pixels 75x23, correspondendo ao tamanho dos botões **OK** / **Cancel** quando possível. Se um rótulo de botão fizer com que o botão exceda o tamanho do botão padrão, os outros botões nesse conjunto deverão ser alinhados com esse tamanho maior.

  ![Botões horizontal OK e cancelar](../../extensibility/ux-guidelines/media/0801-f_horizokcan.png "0801-f_HorizOKCan")

  **Figura 8, 1-f: botões de interior vertical com OK/cancelamento horizontal**

  ![Botões vertical OK e cancelar](../../extensibility/ux-guidelines/media/0801-g_vertokcan.png "0801-g_VertOKCan")

  **Figura 8, 1-g: botões de interior horizontal com vertical OK/cancelar**

#### <a name="browse-button"></a>[Procurar...] Button
 **[Procurar...]** os botões que seguem uma caixa de texto devem soletrar "procurar..." por completo, incluindo as reticências. Se o espaço estiver apertado ou houver vários botões **[procurar...]** na tela, o botão poderá ser reduzido para apenas as reticências.

## <a name="themed-dialog-layout"></a><a name="BKMK_ThemedDialogLayout"></a> Layout de caixa de diálogo com tema
 As caixas de diálogo com tema no Visual Studio têm uma aparência mais clara e oferecem mais espaço em branco. A tipografia fornece mais ênfase e interesse, oferecendo mais espaçamento de linha aberta e uma variação de tamanhos e pesos de fontes. Sempre que possível, as barras Chrome e title foram reduzidas ou removidas. O layout dessas caixas de diálogo deve seguir este padrão básico:

1. O plano de fundo da caixa de diálogo é branco.

2. Há uma borda de regra de 1 pixel em um cinza de valor médio.

3. O título da caixa de diálogo não fica mais em uma barra de título, mas fornece interesse visual e ênfase em um tamanho de ponto maior. (Consulte a seção tamanho da fonte em [estilo de texto](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle).)

4. Rótulos acoplados a texto adicional, como uma descrição, devem ser **fonte de ambiente + negrito**.

5. As colunas interiores são separadas por uma regra de 1 pixel em cinza claro.

6. Os links padrão não têm sublinhado. Os Estados de mouse e pressionados têm uma alteração de cor e um sublinhado.

7. Botões de confirmação (como **OK** / **Cancelar**) ficam no canto inferior direito.

### <a name="themed-dialog-layout-examples"></a>Exemplos de layout de caixa de diálogo com tema
 ![Layout de caixa de diálogo com tema](../../extensibility/ux-guidelines/media/0801-h_themeddialog.png "0801-h_ThemedDialog")

 **Figura 8, 1-h: caixa de diálogo com tema**

 ![Dimensões da caixa de diálogo com tema](../../extensibility/ux-guidelines/media/0801-i_themeddialogdimensions.png "0801-i_ThemedDialogDimensions")

 **Figura 8, 1-i: caixa de diálogo com tema-dimensões**

 ![Fontes de diálogo com tema](../../extensibility/ux-guidelines/media/0801-j_themeddialogfonts.png "0801-j_ThemedDialogFonts")

 **Figura 8, 1-j: caixa de diálogo com tema-fontes**

 ![Cores da caixa de diálogo com temas](../../extensibility/ux-guidelines/media/0801-k_themeddialogcolors.png "0801-k_ThemedDialogColors")

 **Figura 08.01-k: caixa de diálogo com temas – Cores**

## <a name="see-also"></a>Confira também
- [Padrões de aplicativo para Visual Studio](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)
- [Controles (Windows)](/windows/desktop/uxguide/controls)
- [Caixas de diálogo (Windows)](/windows/desktop/uxguide/win-dialog-box)
