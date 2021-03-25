---
title: Cores compartilhadas para o Visual Studio | Microsoft Docs
description: Saiba como usar elementos e temas comuns do shell do Visual Studio para criar sua própria interface do usuário personalizada consistente com o ambiente do Visual Studio.
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: 8d11b9a0-6175-4f2e-8e7f-79daee1bfd41
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8edd16744a6c094ece00ee5e4b8239f3d4f5a92e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054017"
---
# <a name="shared-colors-for-visual-studio"></a>Cores compartilhadas para o Visual Studio
Quando você está projetando a interface do usuário que usa elementos do shell do Visual Studio comuns ou deseja que seu elemento de interface seja consistente com recursos semelhantes, use nomes de token existentes em arquivos de definição de pacote para escolher e atribuir cores. Isso garante que sua interface do usuário permaneça consistente com o ambiente do Visual Studio geral e que seja atualizada automaticamente quando os temas forem adicionados ou atualizados.

Este artigo descreve os elementos comuns da interface do usuário e os nomes de token que eles usam, que você pode referenciar ao criar uma interface do usuário semelhante. Para obter informações específicas sobre como acessar esses tokens de cor, consulte [o serviço VSColor](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService).

Certifique-se de usar os nomes de token corretamente:

- **Use nomes de token com base na função, não na própria cor.** As cores compartilhadas comuns são associadas a elementos de interface específicos e devem ser usadas apenas para os mesmos ou recursos semelhantes. Por exemplo, não reutilize a cor de uma caixa de combinação pressionada para uma animação de progresso girando apenas porque você gosta da cor. As funções da caixa de combinação e da animação são diferentes e, se a cor associada à caixa de combinação for alterada, ela poderá não ser mais uma cor apropriada para o elemento de animação. O uso consistente da cor ajuda a orientar seus usuários e a evitar confusão.

- **Use cores de plano de fundo e texto na combinação correta.** As cores de plano de fundo que devem ser usadas com texto terão uma cor de texto associada. Não use cores de texto diferentes das especificadas para esse plano de fundo. Se não houver uma cor de texto associada, não use essa cor de plano de fundo para qualquer superfície em que você espera exibir texto. Outras combinações de cores de texto e de plano de fundo podem resultar em uma interface ilegível.

- **Use cores de controle apropriadas para seu local.** Em determinados Estados, alguns controles do Visual Studio não têm cores de borda e de plano de fundo separadas. Em vez disso, eles pegam essas cores nas superfícies por trás delas. Certifique-se de sempre usar os nomes de token apropriados para o local onde você está colocando o controle.

> [!IMPORTANT]
> Não use tokens encontrados nas categorias "página inicial" ou "Cider".

## <a name="common-shared-controls"></a>Controles compartilhados comuns

Ao usar uma barra de comandos padrão do Visual Studio em seu recurso, você terá acesso aos controles de shell com estilo. Você não deve modelar esses controles comuns. No entanto, se você precisar criar uma barra de comandos personalizada, talvez seja necessário também criar controles personalizados. Nesse caso, certifique-se de usar os nomes de token corretos para cada um dos controles a seguir para que sua interface do usuário seja consistente com o restante do Visual Studio.

### <a name="button-controls"></a>Controles de botão

![Redline de controle de botão](../../extensibility/ux-guidelines/media/0303-155_buttoncontrolredline.png "0303-155_ButtonControlRedline")

| Usar... | Não use... |
| --- | --- |
| ... para os botões no documento bem que você deseja integrar com temas do Visual Studio (claro, escuro, azul ou um tema de Alto Contraste do sistema). | ... para botões que serão exibidos em um plano de fundo personalizado que não faz parte de um tema do Visual Studio. |

**Botão: estado padrão**

![Botão padrão](../../extensibility/ux-guidelines/media/03.03.Button.Standard.png "03.03. Button. Standard")<br />Botão padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Botão | `CommonControls.Button` |
| Borda do botão | `CommonControls.ButtonBorder` |

**Botão: estado padrão**

![Botão padrão](../../extensibility/ux-guidelines/media/03.03.Button.Default.png "03.03. Button. Default")<br />Botão padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Botão | `CommonControls.ButtonDefault` |
| Borda do botão | `CommonControls.ButtonBorderDefault` |

**Botão: estado desabilitado**

![Botão desabilitado](../../extensibility/ux-guidelines/media/03.03.Button.Disabled.png "03.03. Button. Disabled")<br />Botão desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Botão | `CommonControls.ButtonDisabled` |
| Borda do botão | `CommonControls.ButtonBorderDisabled` |

**Botão: estado de foco**

![Botão ao focalizar](../../extensibility/ux-guidelines/media/03.03.Button.hover.png "03.03. Button. Hover")<br />Botão ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Botão | `CommonControls.ButtonHover` |
| Borda do botão | `CommonControls.ButtonBorderHover` |

**Botão: estado pressionado**

![Botão pressionado](../../extensibility/ux-guidelines/media/03.03.Button.Pressed.png "03.03. Button. pressionado")<br />Botão pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Botão | `CommonControls.ButtonPressed` |
| Borda do botão | `CommonControls.ButtonBorderPressed` |

**Botão: estado focalizado**

![Botão focalizado](../../extensibility/ux-guidelines/media/03.03.Button.Focused.png "03.03. Button. concentrou-se")<br />Botão focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Botão | `CommonControls.ButtonFocused` |
| Borda do botão | `CommonControls.ButtonBorderFocused` |

### <a name="check-box-controls"></a>Controles da caixa de seleção
![Caixa de seleção (Redline)](../../extensibility/ux-guidelines/media/0303-161_checkboxredline.png "0303-161_CheckboxRedline")<br />Caixa de seleção (Redline)

| Usar... | Não use... |
| --- | --- |
| ... para controles de caixa de seleção contidos no documento bem. | ... para qualquer interface do usuário que não seja um controle de caixa de seleção. |

**Caixa de seleção: estado padrão**

![Caixa de seleção](../../extensibility/ux-guidelines/media/0303-162_checkbox.png "0303-162_Checkbox")<br />Caixa de seleção padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `CommonControls.CheckBoxBackground` |
| Borda | `CommonControls.CheckBoxBorder` |
| Texto | `CommonControls.CheckBoxText` |
| Glifo | `CommonControls.CheckBoxGlyph` |

**Caixa de seleção: estado desabilitado**

![Caixa de seleção desabilitada](../../extensibility/ux-guidelines/media/0303-163_checkboxdisabled.png "0303-163_CheckboxDisabled")<br />Caixa de seleção desabilitada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `CommonControls.CheckBoxBackgroundDisabled` |
| Borda | `CommonControls.CheckBoxBorderDisabled` |
| Texto | `CommonControls.CheckBoxTextDisabled` |
| Glifo | `CommonControls.CheckBoxGlyphDisabled` |

**Caixa de seleção: estado de foco**

 ![Caixa de seleção ao focalizar](../../extensibility/ux-guidelines/media/0303-164_checkboxhover.png "0303-164_CheckboxHover")<br />Caixa de seleção ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `CommonControls.CheckBoxBackgroundHover` |
| Borda | `CommonControls.CheckBoxBorderHover` |
| Texto | `CommonControls.CheckBoxTextHover` |
| Glifo | `CommonControls.CheckBoxGlyphHover` |

**Caixa de seleção: estado pressionado**

![Caixa de seleção pressionada](../../extensibility/ux-guidelines/media/0303-165_checkboxpressed.png "0303-165_CheckboxPressed")<br />Caixa de seleção pressionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `CommonControls.CheckBoxBackgroundPressed` |
| Borda | `CommonControls.CheckBoxBorderPressed` |
| Texto | `CommonControls.CheckBoxTextPressed` |
| Glifo | `CommonControls.CheckBoxGlyphPressed` |

**Caixa de seleção: estado focalizado**

![Caixa de seleção focada](../../extensibility/ux-guidelines/media/0303-166_checkboxfocused.png "0303-166_CheckboxFocused")<br />Caixa de seleção focada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `CommonControls.CheckBoxBackgroundFocused` |
| Borda | `CommonControls.CheckBoxBorderFocused` |
| Texto | `CommonControls.CheckBoxTextFocused` |
| Glifo | `CommonControls.CheckBoxGlyphFocused` |

### <a name="drop-downs-and-combo-boxes"></a>Menus suspensos e caixas de combinação
![Lista suspensa/caixa de combinação (Redline)](../../extensibility/ux-guidelines/media/0303-167_dropdowncomboboxredline.png "0303-167_DropDownComboBoxRedline")<br />Lista suspensa/caixa de combinação (Redline)

| Usar... | Não use... |
| --- | --- |
| ... para menus suspensos e caixas de combinação no documento bem. | ... para qualquer interface do usuário que não seja uma lista suspensa ou uma caixa de combinação. |
| | ... para menus [suspensos](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandDropDown) ou [caixas de combinação](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandComboBox)da barra de comandos. |

**Lista suspensa e caixas de combinação: estado padrão**

![Lista suspensa padrão/caixa de combinação](../../extensibility/ux-guidelines/media/0303-168_dropdowncombobox.png "0303-168_DropDownComboBox")<br />Lista suspensa padrão/caixa de combinação

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `CommonControls.ComboBoxBackground` |
| Borda | `CommonControls.ComboBoxBorder` |
| Texto | `CommonControls.ComboBoxText` |
| Separador | `CommonControls.ComboBoxSeparator` |
| Glifo | `CommonControls.ComboBoxGlyph` |
| Plano de fundo do glifo | `CommonControls.ComboBoxGlyphBackground` |

**Lista suspensa e caixas de combinação: estado desabilitado**

![Lista suspensa desabilitada/caixa de combinação](../../extensibility/ux-guidelines/media/0303-169_dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")<br />Lista suspensa desabilitada/caixa de combinação

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `CommonControls.ComboBoxBackgroundDisabled` |
| Borda | `CommonControls.ComboBoxBorderDisabled` |
| Texto | `CommonControls.ComboBoxTextDisabled` |
| Separador | `CommonControls.ComboBoxSeparatorDisabled` |
| Glifo | `CommonControls.ComboBoxGlyphDisabled` |
| Plano de fundo do glifo | `CommonControls.ComboBoxGlyphBackgroundDisabled` |

**Lista suspensas e caixas de combinação: estado de foco**

![Lista suspensa/caixa de combinação ao focalizar](../../extensibility/ux-guidelines/media/0303-170_dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")<br />Lista suspensa/caixa de combinação ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `CommonControls.ComboBoxBackgroundHover` |
| Borda | `CommonControls.ComboBoxBorderHover` |
| Texto | `CommonControls.ComboBoxTextHover` |
| Separador | `CommonControls.ComboBoxSeparatorHover` |
| Glifo | `CommonControls.ComboBoxGlyphHover` |
| Plano de fundo do glifo | `CommonControls.ComboBoxGlyphBackgroundHover` |

**Lista suspensas e caixas de combinação: estado pressionado**

![Lista suspensa pressionado/caixa de combinação](../../extensibility/ux-guidelines/media/0303-171_dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")<br />Lista suspensa pressionado/caixa de combinação

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `CommonControls.ComboBoxBackgroundPressed` |
| Borda | `CommonControls.ComboBoxBorderPressed` |
| Texto | `CommonControls.ComboBoxTextPressed` |
| Separador | `CommonControls.ComboBoxSeparatorPressed` |
| Glifo | `CommonControls.ComboBoxGlyphPressed` |
| Plano de fundo do glifo | `CommonControls.ComboBoxGlyphBackgroundPressed` |

**Exibição de item de lista suspensas e caixas de combinação: estado pressionado**

 ![Modo de exibição de item lista suspensa pressionado por caixa de combinação](../../extensibility/ux-guidelines/media/0303-174_dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")<br />Modo de exibição de item lista suspensa pressionado por caixa de combinação

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `CommonControls.ComboBoxListBackground`<br />`CommonControls.ComboBoxListBackgroundHover`<br />`CommonControls.ComboBoxListItemBackgroundPressed`<br />`CommonControls.ComboBoxListItemBackgroundFocused` |
| Borda | `CommonControls.ComboBoxListBorder`<br />`CommonControls.ComboBoxListBorderHover`<br />`CommonControls.ComboBoxListBorderPressed`<br />`CommonControls.ComboBoxListBorderFocused` |
| Texto do item | `CommonControls.ComboBoxListItemText`<br /> `CommonControls.ComboBoxListItemTextHover`<br />`CommonControls.ComboBoxListItemTextPressed`<br />`CommonControls.ComboBoxListItemTextFocused` |
| Sombra em segundo plano | `CommonControls.ComboBoxListBackgroundShadow` |

**Lista suspensas e caixas de combinação: estado focalizado**

![Lista suspensa/caixa de combinação com foco](../../extensibility/ux-guidelines/media/0303-172_dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")<br />Lista suspensa/caixa de combinação com foco

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `CommonControls.ComboBoxBackgroundFocused` |
| Borda | `CommonControls.ComboBoxBorderFocused` |
| Texto | `CommonControls.ComboBoxTextFocused` |
| Separador | `CommonControls.ComboBoxSeparatorFocused` |
| Glifo | `CommonControls.ComboBoxGlyphFocused` |
| Plano de fundo do glifo | `CommonControls.ComboBoxGlyphBackgroundFocused` |

**Lista suspensas e caixas de combinação: seleção de entrada de texto**

![Seleção de entrada de texto de caixa suspensa/de combinação](../../extensibility/ux-guidelines/media/0303-173_dropdowncomboboxtextinput.png "0303-173_DropDownComboBoxTextInput")<br />Seleção de entrada de texto de caixa suspensa/de combinação

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Realce | `CommonControls.ComboBoxTextInputSelection` |

### <a name="tabular-data-grid-controls"></a>Controles de dados tabulares (grade)
Controles de dados tabulares, também conhecidos como controles de grade, são controles comuns para o Visual Studio que podem ser usados para apresentar grandes quantidades de dados em várias colunas. Os controles de dados de tabela padrão podem ser encontrados em vários locais no Visual Studio: a janela de ferramentas Lista de Erros, os relatórios do IntelliTrace e a exibição de heap de memória, entre outros. Sempre use os controles de dados tabulares padrão fornecidos. Em algumas instâncias raras, talvez você não tenha acesso aos controles de dados tabulares padrão. Nessas situações, use os nomes de token a seguir para garantir que sua interface do usuário seja consistente com outros controles de dados de tabela no Visual Studio.

![Controle de grade/dados de tabela (Redline)](../../extensibility/ux-guidelines/media/0303-197_tabulardatagridcontrolredline.png "0303-197_TabularDataGridControlRedline")<br />Controle de grade/dados de tabela (Redline)

| Usar... | Não use... |
| --- | --- |
| ... para controles de tabela ou de grade. | ... para qualquer interface do usuário que não seja um controle de tabela ou de grade. |

#### <a name="column-headers"></a>Cabeçalhos da coluna
Os cabeçalhos de coluna consistem em um plano de fundo, uma borda, o texto do título e um glifo opcional geralmente usado quando uma grade é classificada por essa coluna.

**Cabeçalho da coluna: estado padrão**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Header.Default` |
| Primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Primeiro plano (glifo) | `Header.Glyph` |
| Borda | `Header.SeparatorLine` |

**Cabeçalho da coluna: estado de foco**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Header.MouseOver` |
| Primeiro plano (texto) | `Environment.CommandBarTextHover` |
| Primeiro plano (glifo) | `Header.MouseOverGlyph` |
| Borda | `Header.SeparatorLine` |

**Cabeçalho da coluna: estado pressionado**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `CommonControls.CheckBoxBackgroundPressed` |
| Primeiro plano (texto) | `CommonControls.CheckBoxBorderPressed` |
| Primeiro plano (glifo) | `CommonControls.CheckBoxTextPressed` |
| Borda | `CommonControls.CheckBoxGlyphPressed` |

#### <a name="list-view-items"></a>Listar itens de exibição
 Os itens de exibição de lista consistem em um plano de fundo e o conteúdo. O conteúdo pode ser texto, um ícone ou ambos.

**Itens de exibição de lista: estado padrão**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | Transparente |
| Primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Borda | Nenhum |

**Itens de exibição de lista: estado ativo**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `TreeView.SelectedItemActive` |
| Primeiro plano (texto) | `TreeView.SelectedItemActiveText` |
| Borda | Nenhum |

**Itens de exibição de lista: estado inativo**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `TreeView.SelectedItemInactive` |
| Primeiro plano (texto) | `TreeView.SelectedItemInactiveText` |
| Borda | Nenhum |

### <a name="ui-text"></a>Texto da interface do usuário

#### <a name="instructional-text"></a>Texto de instrução
O texto instrutivo dá uma explicação importante sobre o que fazer em uma página de diálogo ou documento.

![Texto de instrução padrão](../../extensibility/ux-guidelines/media/0303_InstructionalText.png "0303_InstructionalText.png")<br />Texto de instrução padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `Environment.ControlText` |

#### <a name="secondary-instructional-text"></a>Texto de instrução secundário
Em páginas de documento com muitos textos e controles, alguns textos instrutivos usam um valor de cor diferente. Isso ajuda a transmitir quais informações são mais importantes e diminuir a densidade geral dos elementos da interface do usuário. (Veja também a seção abaixo sobre o texto de dica.)

![Texto de instrução secundário](../../extensibility/ux-guidelines/media/0303_SecondaryInstructionalText.png "0303_SecondaryInstructionalText.png")<br />Texto de instrução secundário

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `Environment.ControlEditHintText` |

#### <a name="hint-text"></a>Texto de dica
O texto de dica aparece em um controle vazio, abaixo de um controle ou em uma superfície de documento vazia para mostrar ao usuário o que fazer em seguida. Você pode usar o texto de dica com planos de fundo de janela ou de controle.

**Texto de dica padrão**

![Texto de dica padrão](../../extensibility/ux-guidelines/media/0303_HintText.png "0303_HintText.png")<br />Texto de dica padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `Environment.ControlEditHintText` |

**Texto de dica necessário**

![Texto de dica necessário](../../extensibility/ux-guidelines/media/0303_RequiredHintText.png "0303_RequiredHintText.png")<br />Texto de dica necessário

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `Environment.ControlRequiredHintText` |
| Segundo plano | `Environment.ControlRequiredBackground` |

**Texto de controle da caixa de pesquisa**

> Consulte as [caixas de pesquisa](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_SearchBoxes) para outros tokens de cor relacionados ao controle de pesquisa.

![Texto de controle da caixa de pesquisa](../../extensibility/ux-guidelines/media/0303_SearchBoxControl.png "0303_SearchBoxControl.png")<br />Texto de controle da caixa de pesquisa

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `SearchControl.UnfocusedWatermarkText` |

### <a name="hyperlink"></a>Hyperlink
O hiperlink é um controle que não tem um par de primeiro plano/segundo plano. Em todos os casos, use a cor do hiperlink de primeiro plano, que será exibida corretamente em planos de fundo escuros, cinzas e brancos. Se você não usar o token de cor para o controle hiperlink, verá a cor padrão do sistema para "pressionado", que piscará vermelho. Esse é o sinal de que o controle não está usando o token de cor de ambiente correto.

![Hiperlink (Redline)](../../extensibility/ux-guidelines/media/0303-133_hyperlinkredline.png "0303-133_HyperlinkRedline")<br />Hiperlink (Redline)

| Usar... | Não use... |
| --- | --- |
| ... Quando você precisar criar um hiperlink personalizado. | ... para qualquer coisa que não seja um hiperlink. |

**Hiperlink: estado padrão**

![Hiperlink padrão](../../extensibility/ux-guidelines/media/0303-134_hyperlink.png "0303-134_Hyperlink")<br />Hiperlink padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `Environment.PanelHyperlink` |

**Hiperlink: estado de foco**

![Hiperlink ao focalizar](../../extensibility/ux-guidelines/media/0303-135_hyperlinkhover.png "0303-135_HyperlinkHover")<br />Hiperlink ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `Environment.PanelHyperlinkHover` |

**Hiperlink: estado pressionado**

![Hiperlink pressionado](../../extensibility/ux-guidelines/media/0303-136_hyperlinkpressed.png "0303-136_HyperlinkPressed")<br />Hiperlink pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `Environment.PanelHyperlinkPressed` |

**Hiperlink: estado desabilitado**

![Hiperlink desabilitado](../../extensibility/ux-guidelines/media/0303-137_hyperlinkdisabled.png "0303-137_HyperlinkDisabled")<br />Hiperlink desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `Environment.PanelHyperlinkDisabled` |

### <a name="infobars"></a>Infobars
Infobars são usados para fornecer mais informações sobre um determinado contexto e sempre aparecem na parte superior de uma janela de documento ou janela de ferramentas.

![Barra de Redline (o)](../../extensibility/ux-guidelines/media/0303-138_infobarredline.png "0303-138_InfobarRedline")<br />Barra de Redline (o)

| Usar... | Não use... |
| --- | --- |
| ... ao criar infobars personalizado. | ... para elementos de interface do usuário que não são semelhantes a uma barra de erro. |

**Barra de status: estado padrão**

![Barra de a padrão](../../extensibility/ux-guidelines/media/0303-139_infobar.png "0303-139_Infobar")<br />Barra de a padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `InfoBar.InfoBarBackground` |
| Primeiro plano (texto) | `InfoBar.InfoBar` |
| Borda | `InfoBar.InfoBarBorder` |

**Botão de fechamento da barra de status &times; : estado padrão**

![Botão de fechamento da barra de somente padrão &times;](../../extensibility/ux-guidelines/media/0303_InfobarCloseDefault.png "0303_InfobarCloseDefault.png")<br />Botão de fechamento da barra de somente padrão &times;

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `InfoBar.CloseButton` |
| Borda | `InfoBar.CloseButtonBorder` |
| Glifo | `InfoBar.CloseButtonGlyph` |

**Botão de fechamento da barra de status &times; : estado de foco**

![&times;Botão de fechamento da barra de cursor () ao focalizar](../../extensibility/ux-guidelines/media/0303_InfobarCloseHover.png "0303_InfobarCloseHover.png")<br />&times;Botão de fechamento da barra de cursor () ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `InfoBar.CloseButtonHover` |
| Borda | `InfoBar.CloseButtonHoverBorder` |
| Glifo | `InfoBar.CloseButtonHoverGlyph` |

**Botão de fechamento da barra de status &times; : estado pressionado**

![Botão fechar da barra de medida ( &times; ) pressionado](../../extensibility/ux-guidelines/media/0303_InfobarClosePressed.png "0303_InfobarClosePressed.png")<br />Botão fechar da barra de medida ( &times; ) pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `InfoBar.CloseButtonDown` |
| Borda | `InfoBar.CloseButtonDownBorder` |
| Glifo | `InfoBar.CloseButtonDownGlyph` |

**Botão de hiperlink da barra de controle: estado padrão**

![Botão de hiperlink de barra de somente padrão](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonDefault.png "0303_InfobarHyperlinkButtonDefault.png")<br />Botão de hiperlink de barra de somente padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `InfoBar.Hyperlink` |

**Botão de hiperlink da barra de controle: estado de foco**

![Botão de hiperlink da barra de do mouse ao focalizar](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonHover.png "0303_InfobarHyperlinkButtonHover.png")<br />Botão de hiperlink da barra de do mouse ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `Infobar.HyperlinkMouseOver`<br />(Com sublinhado) |

**Botão de hiperlink da barra de controle: estado pressionado**

![Botão de hiperlink da barra de botões pressionado](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonPressed.png "0303_InfobarHyperlinkButtonPressed.png")<br />Botão de hiperlink da barra de botões pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `Infobar.HyperlinkMouseDown`<br />(Com sublinhado) |

**Hiperlink embutido da barra de controle (dentro de uma sentença): estado padrão**

![Botão de hiperlink de barra de forma embutida padrão](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonDefault.png "0303_InfobarHyperlinkButtonDefault.png")<br />Botão de hiperlink de barra de forma embutida padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `InfoBar.Hyperlink` |

**Hiperlink embutido da barra de controle (dentro de uma sentença): estado de foco**

![Botão de hiperlink em linha da barra de posição ao focalizar](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkInlineHover.png "0303_InfobarHyperlinkInlineHover.png")<br />Botão de hiperlink em linha da barra de posição ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `Infobar.HyperlinkMouseOver`<br />(Com sublinhado) |

**Hiperlink embutido da barra de controle (dentro de uma sentença): estado pressionado**

![Botão de hiperlink embutido da barra de linhas pressionado](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkInlinePressed.png "0303_InfobarHyperlinkInlinePressed.png")<br />Botão de hiperlink embutido da barra de linhas pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `Infobar.HyperlinkMouseDown`<br />(Com sublinhado) |

**Botão de barra de status: estado padrão**

![Botão de barra de somente padrão](../../extensibility/ux-guidelines/media/0303_InfobarButtonDefault.png "0303_InfobarButtonDefault.png")<br />Botão de barra de somente padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `InfoBar.Button` |
| Primeiro plano (texto) | `InfoBar.Button` |
| Borda | `InfoBar.ButtonBorder` |

**Botão de barra de status: estado de foco**

![Botão de barra de somente ao focalizar](../../extensibility/ux-guidelines/media/0303_InfobarButtonHover.png "0303_InfobarButtonHover.png")<br />Botão de barra de somente ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `InfoBar.ButtonMouseOver` |
| Primeiro plano (texto) | `InfoBar.ButtonMouseOver` |
| Borda | `InfoBar.ButtonMouseOverBorder` |

**Botão de barra de status: estado pressionado**

![Botão da barra de a pressionado](../../extensibility/ux-guidelines/media/0303_InfobarButtonPressed.png "0303_InfobarButtonPressed.png")<br />Botão da barra de a pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `InfoBar.ButtonMouseDown` |
| Primeiro plano (texto) | `InfoBar.ButtonMouseDown` |
| Borda | `InfoBar.ButtonMouseDownBorder` |

**Botão de barra de status: estado desabilitado**

![Botão de barra de somente desabilitado](../../extensibility/ux-guidelines/media/0303_InfobarButtonDisabled.png "0303_InfobarButtonDisabled.png")<br />Botão de barra de somente desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `InfoBar.ButtonDisabled` |
| Primeiro plano (texto) | `InfoBar.ButtonDisabled` |
| Borda | `InfoBar.ButtonDisabledBorder` |

**Botão de barra de visão: estado focalizado**

![Botão de barra de visão focalizado](../../extensibility/ux-guidelines/media/0303_InfobarButtonFocus.png "0303_InfobarButtonFocus.png")<br />Botão de barra de visão focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `InfoBar.ButtonFocus` |
| Primeiro plano (texto) | `InfoBar.ButtonFocus` |
| Borda | `InfoBar.ButtonFocusBorder` |

### <a name="scroll-bars"></a>Barras de rolagem
As barras de rolagem são estilizadas pelo ambiente do Visual Studio e não precisam ser modeladas. No entanto, você pode decidir que deseja aproveitar as cores usadas nas barras de rolagem para que sua interface do usuário sempre pareça consistente com essa parte do ambiente do Visual Studio.

![Barra de rolagem (Redline)](../../extensibility/ux-guidelines/media/0303-140_scrollbarredline.png "0303-140_ScrollbarRedline")<br />Barra de rolagem (Redline)

| Usar... | Não use... |
| --- | --- |
| ... Quando você estiver criando a interface do usuário que deseja corresponder às barras de rolagem do Visual Studio. | ... para qualquer coisa que você não queira sempre corresponder à interface do usuário da barra de rolagem. |

**Barra de rolagem: estado padrão**

![Barra de rolagem padrão](../../extensibility/ux-guidelines/media/0303-141_scrollbar.png "0303-141_Scrollbar")<br />Barra de rolagem padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Barra de rolagem | `Environment.ScrollBarBackground` |
| Primeiro plano (Thumb) | `Environment.ScrollBarThumbBackground` |

**Barra de rolagem: estado de foco**

![Barra de rolagem ao focalizar](../../extensibility/ux-guidelines/media/0303-143_scrollbarhover.png "0303-143_ScrollbarHover")<br />Barra de rolagem ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Barra de rolagem | `Environment.ScrollBarBackground` |
| Primeiro plano (Thumb) | `Environment.ScrollBarThumbMouseOverBackground` |

*Barra de rolagem: estado pressionado**

![Barra de rolagem pressionada](../../extensibility/ux-guidelines/media/0303-145_scrollbarpressed.png "0303-145_ScrollbarPressed")<br />Barra de rolagem pressionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Barra de rolagem | `Environment.ScrollBarBackground` |
| Primeiro plano (Thumb) | `Environment.ScrollBarThumbPressedBackground` |

**Seta da barra de rolagem: estado padrão**

![Seta da barra de rolagem padrão](../../extensibility/ux-guidelines/media/0303-142_scrollbararrow.png "0303-142_ScrollbarArrow")<br />Seta da barra de rolagem padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ScrollBarArrowBackground`<br />(Defina para a mesma cor que a barra de rolagem.) |
| Primeiro plano (glifo) | `Environment.ScrollBarArrowGlyph` |

**Seta da barra de rolagem: estado de foco**

![Seta da barra de rolagem ao focalizar](../../extensibility/ux-guidelines/media/0303-144_scrollbararrowhover.png "0303-144_ScrollbarArrowHover")<br />Seta da barra de rolagem ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ScrollBarArrowMouseOverBackground`<br />(Defina para a mesma cor que a barra de rolagem.) |
| Primeiro plano (glifo) | `Environment.ScrollBarArrowGlyphMouseOver` |

**Seta da barra de rolagem: estado pressionado**

![Seta da barra de rolagem pressionada](../../extensibility/ux-guidelines/media/0303-146_scrollbararrowpressed.png "0303-146_ScrollbarArrowPressed")<br />Seta da barra de rolagem pressionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ScrollBarArrowPressedBackground`<br />(Defina para a mesma cor que a barra de rolagem.) |
| Primeiro plano (glifo) | `Environment.ScrollBarArrowGlyphPressed` |

### <a name="search-boxes"></a><a name="BKMK_SearchBoxes"></a>Caixas de pesquisa
Sempre que possível, use o controle de pesquisa comum fornecido pelo ambiente do Visual Studio. As cores da caixa de pesquisa são encontradas na categoria "SearchControl" no arquivo **ShellColors. pkgdef** , que contém nomes de token para o campo de entrada, botão de ação, botão suspenso e menu suspenso.

Uma caixa de pesquisa pode ser um dos vários Estados, algumas das quais são mutuamente exclusivas:

- "Focalizado" ou "sem foco" refere-se a se o cursor está ou não na caixa de texto.

- "Ativo" ou "inativo" refere-se a se o usuário tem entrada em uma consulta de pesquisa na caixa de texto.

- "Hover" significa que o usuário fez o mouse sobre a caixa de pesquisa com o mouse (esse estado substitui todos os outros Estados).

- "Disabled" significa que a funcionalidade de pesquisa está desativada para o contexto atual.

![Caixa de pesquisa (Redline)](../../extensibility/ux-guidelines/media/0303-110_searchboxredline.png "0303-110_SearchBoxRedline")<br />Caixa de pesquisa (Redline)

| Usar... | Não use... |
| --- | --- |
| ... Quando você estiver criando uma caixa de pesquisa personalizada. | ... para qualquer coisa que não seja uma caixa de pesquisa. |
| | ... para qualquer coisa que você não queira sempre corresponder à interface do usuário da caixa de pesquisa. |

**Campo de entrada de pesquisa focado**

![Campo de entrada de pesquisa focado](../../extensibility/ux-guidelines/media/0303-111_searchinputfieldfocused.png "0303-111_SearchInputFieldFocused")<br />Campo de entrada de pesquisa focado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `SearchControl.FocusedBackground` |
| Primeiro plano (texto) | `SearchControl.FocusedBackground` |
| Borda | `SearchControl.FocusedBorder` |
| Separador | `SearchControl.FocusedDropDownSeparator` |

**Campo de entrada de pesquisa ativo não focalizado**

![Campo de entrada de pesquisa não focalizado](../../extensibility/ux-guidelines/media/0303-114_searchinputfieldunfocused.png "0303-114_SearchInputFieldUnfocused")<br />Campo de entrada de pesquisa ativo não focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `SearchControl.SearchActiveBackground` |
| Primeiro plano (texto) | `SearchControl.SearchActiveBackground` |
| Borda | `SearchControl.UnfocusedBorder` |
| Separador | `SearchControl.DropDownSeparator` |

**Campo de entrada de pesquisa inativo e não focalizado**

![Campo de entrada de pesquisa inativo e não focalizado](../../extensibility/ux-guidelines/media/0303-114-1_searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")<br />Campo de entrada de pesquisa inativo e não focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `SearchControl.Unfocused` |
| Primeiro plano (texto) | `SearchControl.Unfocused` |
| Borda | `SearchControl.UnfocusedBorder` |
| Separador | `SearchControl.DropDownSeparator` |

**Campo de entrada de pesquisa realçado (somente texto)**

![Campo de entrada de pesquisa realçado](../../extensibility/ux-guidelines/media/0303-120_searchinputfieldhighlight.png "0303-120_SearchInputFieldHighlight")<br />Campo de entrada de pesquisa realçado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `SearchControl.Selection` |
| Primeiro plano (texto) | `SearchControl.FocusedBackground` |
| Borda | Nenhum |
| Separador | `SearchControl.FocusedDropDownSeparator` |

**Campo de entrada de pesquisa desabilitado**

![Campo de entrada de pesquisa desabilitado](../../extensibility/ux-guidelines/media/0303-121_searchinputfielddisabled.png "0303-121_SearchInputFieldDisabled")<br />Campo de entrada de pesquisa desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `SearchControl.Disabled` |
| Primeiro plano (texto) | `SearchControl.Disabled` |
| Borda | `SearchControl.DisabledBorder` |
| Separador | `SearchControl.DropDownSeparator` |

**Botão de ação de pesquisa focado**

![Foco no botão de ação de pesquisa](../../extensibility/ux-guidelines/media/0303-112_searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br />Botão de ação de pesquisa focado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | Nenhum |
| Primeiro plano (glifo de pesquisa) | `SearchControl.SearchGlyph` |
| Primeiro plano (glifo de parada) | `SearchControl.StopGlyph` |
| Primeiro plano (limpar glifo) | `SearchControl.ClearGlyph` |
| Borda | N/D |

**Botão de ação de pesquisa não focalizado**

![Botão de ação de pesquisa não focalizado](../../extensibility/ux-guidelines/media/0303-115_searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br />Botão de ação de pesquisa não focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | N/D |
| Primeiro plano (glifo de pesquisa) | `SearchControl.SearchGlyph` |
| Primeiro plano (glifo de parada) | `SearchControl.StopGlyph` |
| Primeiro plano (limpar glifo) | `SearchControl.ClearGlyph` |
| Borda | N/D |

**Botão de ação de pesquisa pressionado**

![Botão de ação de pesquisa pressionado](../../extensibility/ux-guidelines/media/0303-116-1_searchactionbuttonpressed.png "0303-116-1_SearchActionButtonPressed")<br />Botão de ação de pesquisa pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `SearchControl.ActionButtonMouseDown` |
| Primeiro plano (glifo) | `SearchControl.ActionButtonMouseDownGlyph` |
| Borda | `SearchControl.ActionButtonMouseDownBorder` |

**Botão de ação de pesquisa desabilitado**

![Botão de ação de pesquisa desabilitado](../../extensibility/ux-guidelines/media/0303-122_searchactionbuttondisabled.png "0303-122_SearchActionButtonDisabled")<br />Botão de ação de pesquisa desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | Nenhum |
| Primeiro plano (glifo) | `SearchControl.ActionButtonDisabledGlyph` |
| Borda | Nenhum |

**Botão suspenso de pesquisa focado**

![Botão suspenso de pesquisa focado](../../extensibility/ux-guidelines/media/0303-113_searchdropdownbuttonfocused.png "0303-113_SearchDropdownButtonFocused")<br />Botão suspenso de pesquisa focado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `SearchControl.FocusedDropDownButton` |
| Primeiro plano (glifo) | `SearchControl.FocusedDropDownButtonGlyph` |
| Borda | `SearchControl.FocusedDropDownButtonBorder` |

**Botão suspenso de pesquisa não focalizado**

![Botão suspenso de pesquisa não focalizado](../../extensibility/ux-guidelines/media/0303-116_searchdropdownbuttonunfocused.png "0303-116_SearchDropdownButtonUnfocused")<br />Botão suspenso de pesquisa não focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `SearchControl.UnfocusedDropDownButton` |
| Primeiro plano (glifo) | `SearchControl.UnfocusedDropDownButtonGlyph` |
| Borda | `SearchControl.UnfocusedDropDownButtonBorder` |

**Botão suspenso de pesquisa pressionado**

![Botão suspenso de pesquisa pressionado](../../extensibility/ux-guidelines/media/0303-116-2_searchdropdownbuttonpressed.png "0303-116-2_SearchDropdownButtonPressed")<br />Botão suspenso de pesquisa pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `SearchControl.MouseDownDropDownButton` |
| Primeiro plano (glifo) | `SearchControl.MouseDownDropDownButtonGlyph` |
| Borda | `SearchControl.MouseDownDropDownButtonBorder` |

**Botão suspenso de pesquisa desabilitado**

![Botão suspenso de pesquisa desabilitado](../../extensibility/ux-guidelines/media/0303-123_searchdropdownbuttondisabled.png "0303-123_SearchDropdownButtonDisabled")<br />Botão suspenso de pesquisa desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | Nenhum |
| Primeiro plano (glifo) | `SearchControl.DisabledDownButtonGlyph` |
| Borda | Nenhum |

#### <a name="search-drop-down-lists"></a>Listas suspensas de pesquisa
O menu suspenso caixa de pesquisa tem o potencial de ser um pouco mais complexo do que outros menus suspensos no Visual Studio. As seções "pesquisas sugeridas" e "opções de pesquisa" podem aparecer sozinhas ou juntas no menu, e cada uma é colorida separadamente. Uma linha também separa essas duas seções quando elas aparecem juntas e uma borda circunda todo o menu suspenso.

![Lista suspensa de pesquisa (Redline)](../../extensibility/ux-guidelines/media/0303-124_searchdropdownredline.png "0303-124_SearchDropdownRedline")<br />Lista suspensa de pesquisa (Redline)

| Usar... | Não use... |
| --- | --- |
| ... Quando você estiver criando uma lista suspensa de pesquisa personalizada. | ... para listas suspensas que aparecem em outros contextos. |
| ... os nomes de token corretos para os componentes de lista corretos. | ... em qualquer combinação de plano de fundo/primeiro plano diferente de especificada. |

**Pesquisar elementos da lista suspensa**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Borda | `SearchControl.PopupBorder` |
| Separador | `SearchControl.PopupSectionHeaderSeparator` |
| Shadow | `Environment.DropShadowBackground` |

**Pesquisas sugeridas: estado padrão**

![Pesquisas padrão sugeridas](../../extensibility/ux-guidelines/media/0303-125_searchsuggested.png "0303-125_SearchSuggested")<br />Pesquisas padrão sugeridas

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `SearchControl.PopupItemsListBackgroundGradientBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `SearchControl.PopupItemText` |

**Pesquisas sugeridas: estado de foco**

![Pesquisas sugeridas ao focalizar](../../extensibility/ux-guidelines/media/0303-128_searchsuggestedhover.png "0303-128_SearchSuggestedHover")<br />Pesquisas sugeridas ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `SearchControl.PopupMouseOverItemText` |
| Borda | `SearchControl.PopupControlMouseOverBorder` |

**Opções de pesquisa: estado padrão**

![Caixa de seleção Pesquisar](../../extensibility/ux-guidelines/media/0303-126_searchcheckbox.png "0303-126_SearchCheckbox")<br />Opções de pesquisa padrão (caixa de seleção)

![Opções de pesquisa](../../extensibility/ux-guidelines/media/0303-127_searchoptions.png "0303-127_SearchOptions")<br />Opções de pesquisa padrão (link)

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `SearchControl.PopupSectionBackgroundGradientBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto da caixa de seleção) | `SearchControl.PopupCheckboxText` |
| Primeiro plano (texto do link) | `SearchControl.PopupButtonText` |
| Plano de fundo do cabeçalho | `SearchControl.PopupSectionHeaderGradientBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto do cabeçalho) | `SearchControl.PopupSectionHeaderText` |

**Opções de pesquisa: estado de foco**

![Opções de pesquisa (caixa de seleção) ao focalizar](../../extensibility/ux-guidelines/media/0303-129_searchcheckboxhover.png "0303-129_SearchCheckboxHover")<br />Opções de pesquisa (caixa de seleção) ao focalizar

![Opções de pesquisa (link) ao focalizar](../../extensibility/ux-guidelines/media/0303-130_searchoptionshover.png "0303-130_SearchOptionsHover")<br />Opções de pesquisa (link) ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto da caixa de seleção) | `SearchControl.PopupCheckboxMouseDownText` |
| Primeiro plano (texto do link) | `SearchControl.PopupButtonMouseDownText` |
| Borda | `SearchControl.PopupControlMouseOverBorder` |

**Opções de pesquisa: estado pressionado**

![Opções de pesquisa pressionadas (caixa de seleção)](../../extensibility/ux-guidelines/media/0303-131_searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br />Opções de pesquisa pressionadas (caixa de seleção)

![Opções de pesquisa pressionadas (link)](../../extensibility/ux-guidelines/media/0303-132_searchoptionspressed.png "0303-132_SearchOptionsPressed")<br />Opções de pesquisa pressionadas (link)

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Plano de fundo da caixa de seleção | `SearchControl.PopupControlMouseDownBackgroundGradientBegin`<br />`SearchControl.PopupControlMouseDownBackgroundGradientEnd`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto da caixa de seleção) | `SearchControl.PopupCheckboxMouseDownText` |
| Vincular plano de fundo | `SearchControl.PopupButtonMouseDownBackgroundGradientBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto do link) | `SearchControl.PopupButtonMouseDownText` |

### <a name="tree-views"></a><a name="BKMK_TreeView"></a> Exibições de árvore
Várias janelas de ferramentas, incluindo a Gerenciador de Soluções, Gerenciador de Servidores e Modo de Exibição de Classe, implementam um esquema organizacional hierárquico cujas cores são controladas por nomes de cores na `TreeView` categoria. Todos os itens em um modo de exibição de árvore têm cores de texto e em segundo plano. Os itens que têm elementos filho aninhados também têm glifos que indicam se o item está expandido ou recolhido.

![Modo de exibição de árvore (Redline)](../../extensibility/ux-guidelines/media/0303-147_treeviewredline.png "0303-147_TreeViewRedline")<br />Modo de exibição de árvore (Redline)

| Usar... | Não use... |
| --- | --- |
| ... em qualquer lugar, você precisa implementar uma exibição organizacional hierárquica. | ... para qualquer coisa que não seja semelhante a uma exibição de árvore. |
| | ... em qualquer combinação de plano de fundo/primeiro plano diferente de especificada. |

**Item de exibição de árvore: estado padrão**

![Item de exibição de árvore padrão](../../extensibility/ux-guidelines/media/0303-148_treeview.png "0303-148_TreeView")<br />Item de exibição de árvore padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `TreeView.Background` |
| Primeiro plano (texto) | `TreeView.Background` |
| Primeiro plano (glifo) | `TreeView.Glyph` |
| Borda | Nenhum |

**Item de exibição de árvore: estado de foco**

![Item de exibição de árvore ao focalizar](../../extensibility/ux-guidelines/media/0303-149_treeviewhover.png "0303-149_TreeViewHover")<br />Item de exibição de árvore ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `TreeView.Background` |
| Primeiro plano (texto) | `TreeView.Background` |
| Primeiro plano (glifo) | `TreeView.GlyphMouseOver` |
| Borda | Nenhum |

**Item de exibição de árvore: arraste sobre o estado**

![Item de exibição de árvore ao arrastar sobre](../../extensibility/ux-guidelines/media/0303-150_treeviewdragover.png "0303-150_TreeViewDragOver")<br />Item de exibição de árvore ao arrastar sobre

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `TreeView.DragOverItem` |
| Primeiro plano (texto) | `TreeView.DragOverItem` |
| Primeiro plano (glifo) | `TreeView.DragOverItemGlyph` |
| Borda | Nenhum |

**Item de modo de exibição de árvore: selecionado, estado focalizado**

![Item de exibição de árvore selecionado e focalizado](../../extensibility/ux-guidelines/media/0303-151_treeviewfocused.png "0303-151_TreeViewFocused")<br />Item de exibição de árvore selecionado e focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `TreeView.SelectedItemActive` |
| Primeiro plano (texto) | `TreeView.SelectedItemActive` |
| Primeiro plano (glifo) | `TreeView.SelectedItemActiveGlyph` |
| Borda | `TreeView.FocusVisualBorder` |

**Item de modo de exibição de árvore: selecionado, estado não focalizado**

![Item de exibição de árvore selecionado e não focalizado](../../extensibility/ux-guidelines/media/0303-152_treeviewunfocused.png "0303-152_TreeViewUnfocused")<br />Item de exibição de árvore selecionado e não focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `TreeView.SelectedItemInactive` |
| Primeiro plano (texto) | `TreeView.SelectedItemInactive` |
| Primeiro plano (glifo) | `TreeView.SelectedItemInactiveGlyph` |
| Borda | Nenhum |

**Item de exibição de árvore: focalizado, selecionado e estado focalizado**

![Item de exibição de árvore marcada e focalizado ao focalizar](../../extensibility/ux-guidelines/media/0303-153_treeviewfocusedhover.png "0303-153_TreeViewFocusedHover")<br />Item de exibição de árvore marcada e focalizado ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `TreeView.SelectedItemActive` |
| Primeiro plano (texto) | `TreeView.SelectedItemActive` |
| Primeiro plano (glifo) | `TreeView.SelectedItemActiveGlyphMouseOver` |
| Borda | `TreeView.FocusVisualBorder` |

**Item de exibição de árvore: estado focalizado, selecionado e não focalizado**

![Item de exibição de árvore selecionado e não focalizado ao focalizar](../../extensibility/ux-guidelines/media/0303-154_treeviewunfocusedhover.png "0303-154_TreeViewUnfocusedHover")<br />Item de exibição de árvore selecionado e não focalizado ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `TreeView.SelectedItemInactive` |
| Primeiro plano (texto) | `TreeView.SelectedItemInactive` |
| Primeiro plano (glifo) | `TreeView.SelectedItemActiveGlyphMouseOver` |
| Borda | Nenhum |

## <a name="shell-appearance"></a>Aparência do Shell

### <a name="background"></a>Segundo plano
O plano de fundo do ambiente consiste em duas camadas. A camada inferior é uma cor sólida que cobre todo o IDE. A camada superior se ajusta na prateleira de comando e entre a janela de ferramentas oculta automaticamente os canais nas bordas esquerda e direita do IDE. As camadas de plano de fundo superior e inferior são definidas com a mesma cor nos temas claro e escuro.

![Plano de fundo do shell do Visual Studio (Redline)](../../extensibility/ux-guidelines/media/0303-187_shellbackgroundredline.png "0303-187_ShellBackgroundRedline")<br />Plano de fundo do shell do Visual Studio (Redline)

| Usar... | Não use... |
| --- | --- |
| ... para locais onde você deseja corresponder ao plano de fundo do ambiente do Visual Studio. | ... como um preenchimento para locais que não são superfícies de segundo plano. |
| | ... como um plano de fundo no qual inserir elementos de primeiro plano. |

**Aparência do Shell de camada inferior**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.EnvironmentBackground` |

**Aparência do Shell de camada superior**

> As interrupções de gradiente são definidas com o mesmo valor de cor nos temas Visual Studio 2013 claro e escuro.

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.EnvironmentBackgroundGradientBegin`<br />`Environment.EnvironmentBackgroundGradientEnd`<br />`Environment.EnvironmentBackgroundGradientMiddle1`<br />`Environment.EnvironmentBackgroundGradientMiddle2` |

### <a name="command-shelf"></a>Prateleira de comando
Dois conjuntos de nomes de token são usados para os planos de fundo de prateleira de comando: um conjunto para o local em que a barra de menus reside e um para onde as barras de comando ficam. Um grupo de barras de comando individual tem seus próprios valores de cor de plano de fundo, que são discutidos com mais detalhes na seção "barra de comandos". A barra de menus e o texto da barra de comandos são discutidos nas seções do menu e da barra de comandos, respectivamente.

![Prateleira de comandos do Visual Studio (Redline)](../../extensibility/ux-guidelines/media/0303-188_commandshelfredline.png "0303-188_CommandShelfRedline")<br />Prateleira de comandos do Visual Studio (Redline)

| Usar... | Não use... |
| --- | --- |
| ... para áreas em que você coloca menus ou barras de ferramentas. | ... para áreas que não são semelhantes a uma prateleira de comando. |
|... com a combinação correta de nome de token de segundo plano/primeiro plano. | |

**Barra de menus da prateleira de comando**

> As interrupções de gradiente são definidas com o mesmo valor de cor nos temas Visual Studio 2013 claro e escuro.

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandShelfHighlightGradientBegin`<br /><br />`Environment.CommandShelfHighlightGradientMiddle`<br />`Environment.CommandShelfHighlightGradientEnd` |

**Barra de comandos da prateleira de comando**

> As interrupções de gradiente são definidas com o mesmo valor de cor nos temas Visual Studio 2013 claro e escuro.

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandShelfBackgroundGradientBegin`<br />`Environment.CommandShelfBackgroundGradientMiddle`<br />`Environment.CommandShelfBackgroundGradientEnd` |

## <a name="manifest-designer"></a>Designer de manifesto
O designer de manifesto foi projetado como uma maneira de facilitar a edição do arquivo de manifesto nos projetos do Windows 8 e do Windows Phone 8. Embora não haja nenhuma estrutura compartilhada disponível para consumo, pode ser apropriado que você corresponda ao layout de design e às cores das guias de orientação/navegação e da estrutura geral. Para obter mais informações sobre detalhes de layout, consulte [layout para Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md).

![Designer de manifesto (Redline)](../../extensibility/ux-guidelines/media/0303-175_manifestdesignerredline.png "0303-175_ManifestDesignerRedline")<br />Designer de manifesto (Redline)

| Usar... | Não use... |
| --- | --- |
| ... para designers semelhantes ao designer de manifesto. | ... Se você tiver mais de seis guias. |
| ... em vez de usar os controles de guia comuns na parte superior de um editor dentro do bem do documento. | ... para qualquer interface do usuário que não esteja estruturada como o designer de manifesto. |

**Guia selecionada do designer de manifesto: estado padrão**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `ManifestDesigner.TabActive` |
| Borda | Nenhum |

**Painel de descrição selecionado do designer de manifesto: estado padrão**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `ManifestDesigner.DescriptionPane` |

**Página de conteúdo selecionada do designer de manifesto: estado padrão**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `ManifestDesigner.Background` |
| Texto auxiliar de diálogo | `ManifestDesigner.WatermarkText`<br />(Esse nome de token não corresponde à sua função.) |

**Guia Designer de manifesto: estado não selecionado**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `ManifestDesigner.Tab.Inactive` |

**Guia Designer de manifesto: estado de foco**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `ManifestDesigner.Tab.Mouseover` |

## <a name="command-structures"></a>Estruturas de comando

### <a name="menus"></a><a name="BKMK_CommandMenus"></a> Completos
Os menus podem ocorrer em vários locais no Visual Studio: a barra de menus principal, inserida em janelas de documentos ou ferramentas, ou clique com o botão direito do mouse em vários locais em todo o IDE. Implementações de menus associados a outros elementos da interface do usuário são discutidas na seção para o respectivo elemento. Você sempre deve usar a implementação de menu padrão fornecida pelo ambiente do Visual Studio. No entanto, em algumas instâncias raras, talvez você não tenha acesso aos menus padrão do Visual Studio. Nessas situações, use os nomes de token a seguir para garantir que sua interface do usuário seja consistente com outros menus do Visual Studio.

![Menu do Visual Studio (Redline)](../../extensibility/ux-guidelines/media/0303-000_menuredline.png "0303-000_MenuRedline")<br />Menu do Visual Studio (Redline)

| Usar... | Não use... |
| --- | --- |
| ... Quando você precisar criar um menu personalizado.| ... apenas a cor do plano de fundo. Sempre use a combinação de plano de fundo/primeiro plano como especificado. |
| ... Quando você tem um novo componente de interface do usuário que deseja corresponder aos menus do Visual Studio.| |

#### <a name="menu-titles"></a>Títulos de menu
Os títulos de menu consistem em um plano de fundo, uma borda e o texto do título, bem como um glifo opcional, geralmente quando o menu é encontrado em uma barra de comandos.

![Título do menu (Redline)](../../extensibility/ux-guidelines/media/0303-001_menutitleredline.png "0303-001_MenuTitleRedline")<br />Título do menu (Redline)

| Usar... | Não use... |
| --- | --- |
| ... sempre que você estiver criando um título de menu personalizado. | ... para qualquer coisa que você não queira que corresponda sempre ao título do menu. |
| | ... em qualquer combinação de plano de fundo/primeiro plano diferente de especificada. |

**Título do menu: estado padrão**

![Título de menu padrão](../../extensibility/ux-guidelines/media/0303-002_menutitledefault.png "0303-002_MenuTitleDefault")<br />Título de menu padrão

![Título de menu padrão com glifo](../../extensibility/ux-guidelines/media/0303-003_menutitlewithglyphdefault.png "0303-003_MenuTitleWithGlyphDefault")<br />Título de menu padrão com glifo

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | Nenhum |
| Primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Primeiro plano (glifo) | `Environment.CommandBarMenuGlyph` |
| Borda | Nenhum |

**Título do menu: estado de foco**

![Título do menu ao focalizar](../../extensibility/ux-guidelines/media/0303-004_menutitlehover.png "0303-004_MenuTitleHover")<br />Título do menu ao focalizar

![Título do menu com glifo ao focalizar](../../extensibility/ux-guidelines/media/0303-005_menutitlewithglyphhover.png "0303-005_MenuTitleWithGlyphHover")<br />Título do menu com glifo ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandBarMouseOverBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.CommandBarTextHover` |
| Primeiro plano (glifo) | `Environment.CommandBarMenuMouseOverGlyph` |
| Borda | `Environment.CommandBarBorder` |

**Título do menu: estado pressionado**

![Título do menu pressionado](../../extensibility/ux-guidelines/media/0303-006_menutitlepressed.png "0303-006_MenuTitlePressed")<br />Título do menu pressionado

![Título do menu pressionado com glifo](../../extensibility/ux-guidelines/media/0303-007_menutitlewithglyphpressed.png "0303-007_MenuTitleWithGlyphPressed")<br />Título do menu pressionado com glifo

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandBarMenuBackgroundGradientBegin`<br/>(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Primeiro plano (glifo) | `Environment.CommandBarMenuMouseDownGlyph` |
| Borda | `Environment.CommandBarMenuBorder`<br />(Somente laterais esquerda, superior e direita.) |

**Título do menu: estado desabilitado**

![Título do menu desabilitado com glifo](../../extensibility/ux-guidelines/media/0303-008_menutitlewithglyphdisabled.png "0303-008_MenuTitleWithGlyphDisabled")<br />Título do menu desabilitado com glifo

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | Nenhum |
| Primeiro plano (texto) | `Environment.CommandBarTextInactive` |
| Primeiro plano (glifo) | `Environment.CommandBarTextInactive` |
| Borda | Nenhum |

#### <a name="menu-items"></a>Itens de menu
Um item de menu individual consiste no texto do menu e em um ícone opcional, caixa de seleção ou glifo de submenu. Sua cor de plano de fundo e de texto é alterada ao focalizar. Esse token de cor é um par de plano de fundo/primeiro plano.

![Itens de menu Redline](../../extensibility/ux-guidelines/media/0303-009_menuitemredline.png "0303-009_MenuItemRedline")

| Usar... | Não use... |
|---|---|
| ... para qualquer lista suspensa iniciada em uma barra de menus ou barra de comandos. | ... para qualquer lista suspensa em outro contexto. |
| | ... em qualquer combinação de plano de fundo/primeiro plano diferente de especificada. |

**Itens de menu: estado padrão**

![Itens de menu padrão](../../extensibility/ux-guidelines/media/0303-010_menudefault.png "0303-010_MenuDefault")<br />Itens de menu padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandBarMenuBackgroundGradientBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Primeiro plano (glifo do submenu) | `Environment.CommandBarMenuSubmenuGlyph` |
| Borda | `Environment.CommandBarMenuBorder` |
| Plano de fundo do canal de ícone | `Environment.CommandBarMenuIconBackground` |
| Separador | `Environment.CommandBarMenuSeparator` |
| Shadow | `Environment.DropShadowBackground` |

**Itens de menu: Estados marcados e selecionados**

![Menu marcado](../../extensibility/ux-guidelines/media/0303-011_menuchecked.png "0303-011_MenuChecked")<br />Item de menu selecionado

![Menu selecionado](../../extensibility/ux-guidelines/media/0303-012_menuselected.png "0303-012_MenuSelected")<br />Item de menu selecionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Marca de seleção | `Environment.CommandBarCheckBox` |
| Plano de fundo de marca de seleção | `Environment.CommandBarSelectedIcon` |
| Plano de fundo do ícone | `Environment.CommandBarSelected` |
| Borda do ícone | `Environment.CommandBarSelectedBorder` |

**Itens de menu: estado de foco**

![Focalização do menu](../../extensibility/ux-guidelines/media/0303-013_menuhover.png "0303-013_MenuHover")<br />Item de menu ao focalizar

![Foco do menu verificado](../../extensibility/ux-guidelines/media/0303-014_menuhoverchecked.png "0303-014_MenuHoverChecked")<br />Item de menu selecionado ao focalizar

![Menu focalizado selecionado](../../extensibility/ux-guidelines/media/0303-015_menuhoverselected.png "0303-015_MenuHoverSelected")<br />Item de menu selecionado ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandBarMenuItemMouseOver` |
| Primeiro plano (texto) | `Environment.CommandBarMenuItemMouseOverText` |
| Primeiro plano (glifo do submenu) | `Environment.CommandBarMenuMouseOverSubmenuGlyph` |
| Marca de seleção | `Environment.CommandBarCheckBoxMouseOver` |
| Plano de fundo de marca de seleção | `Environment.CommandBarHoverOverSelectedIcon` |
| Plano de fundo do ícone | `Environment.CommandBarHoverOverSelected` |
| Borda do ícone | `Environment.CommandBarHoverOverSelectedIconBorder` |

**Itens de menu: estado desabilitado**

![Menu desabilitado](../../extensibility/ux-guidelines/media/0303-016_menudisabled.png "0303-016_MenuDisabled")<br />Item de menu desabilitado

![Menu desabilitado marcado](../../extensibility/ux-guidelines/media/0303-017_menudisabledchecked.png "0303-017_MenuDisabledChecked")<br />Item de menu desabilitado com marca de seleção

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Primeiro plano (texto) | `Environment.CommandBarTextInactive` |
| Primeiro plano (glifo do submenu) | `Environment.CommandBarMenuSubmenuGlyph` |
| Marca de seleção | `Environment.CommandBarCheckBoxDisabled` |
| Plano de fundo de marca de seleção | `Environment.CommandBarSelectedIconDisabled` |

### <a name="command-bars"></a>Barras de comando
Uma barra de comandos pode aparecer em vários locais no IDE do Visual Studio, mais notavelmente a prateleira de comandos e incorporada em janelas de ferramentas ou documentos.

Em geral, sempre use a implementação da barra de comandos padrão fornecida pelo ambiente do Visual Studio. O uso do mecanismo padrão garante que todos os detalhes visuais apareçam corretamente e que os elementos interativos se comportem de forma consistente com outros controles de barra de comandos do Visual Studio. No entanto, se for necessário que você crie sua própria barra de comandos, certifique-se de estilizar corretamente usando os nomes de token a seguir.

![Redline da barra de comandos](../../extensibility/ux-guidelines/media/0303-018_commandbarredline.png "0303-018_CommandBarRedline")<br />Barra de comandos (Redline)

![Botão de estouro Redline](../../extensibility/ux-guidelines/media/0303-019_overflowbuttonredline.png "0303-019_OverflowButtonRedline")<br />Botão de estouro (Redline)

| Usar... | Não use... |
| --- | --- |
| ... em locais onde você precisa de uma barra de comandos inserida, mas não é possível usar a implementação padrão da barra de comandos do Visual Studio. | ... para elementos de interface do usuário que não são semelhantes a uma barra de comandos. |
| | ... para componentes da barra de comandos diferentes daqueles para os quais os nomes de token são especificados. |

#### <a name="command-bar-groups"></a>Grupos de barras de comandos
Um grupo de barras de comando consiste em um conjunto relacionado de controles de barra de comandos e pode conter qualquer número de botões, botões de divisão, menus suspensos, caixas de combinação ou menus. As cores desses controles são regulamentadas por nomes de token separados e são discutidas individualmente em outro lugar neste guia. Uma linha separadora é usada para dividir um grupo de barras de comandos em subgrupos relacionados.

![Grupo de barras de comandos Redline](../../extensibility/ux-guidelines/media/0303-020_commandbargroupredline.png "0303-020_CommandBarGroupRedline")<br />Grupo de barras de comandos (Redline)

| Usar... | Não use... |
| --- | --- |
| ... em locais onde você precisa de uma barra de comandos inserida, mas não é possível usar a implementação padrão da barra de comandos do Visual Studio. | ... para elementos de interface do usuário que não são semelhantes a uma barra de comandos. |
| | ... para componentes da barra de comandos diferentes daqueles para os quais os nomes de token são especificados. |

**Grupo de barras de comando: estado padrão**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandBarGradientBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Borda | `Environment.CommandBarToolBarBorder` |
| Identificador de arrastar | `Environment.CommandBarDragHandle` |
| Separador | `Environment.CommandBarToolBarSeparator`<br />`Environment.CommandBarToolBarSeparatorHighlight` |

#### <a name="command-icons"></a>Ícones de comando
![Ícone de comando Redline](../../extensibility/ux-guidelines/media/0303-021_commandiconredline1.png "0303-021_CommandIconRedline1")<br />Ícone de comando (Redline)

![Ícone de comando com texto Redline](../../extensibility/ux-guidelines/media/0303-022_commandiconredline2.png "0303-022_CommandIconRedline2")<br />Ícone de comando com texto (Redline)

| Usar... | Não use... |
| --- | --- |
| ... para todos os botões que serão colocados em uma barra de comandos. | ... para controles que têm seus próprios nomes de token. |
| | ... em qualquer combinação de plano de fundo/primeiro plano diferente de especificada. |

**Ícone de comando: estado padrão**

![Ícone de comando padrão](../../extensibility/ux-guidelines/media/0303-023_commandicondefault.png "0303-023_CommandIconDefault")<br />Ícone de comando padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | N/A (herda do plano de fundo da barra de comandos) |
| Primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Borda | N/D |

**Ícone de comando: estado padrão, selecionado**

![Padrão, ícone de comando selecionado](../../extensibility/ux-guidelines/media/0303-024_commandicondefaultselected.png "0303-024_CommandIconDefaultSelected")<br />Padrão, ícone de comando selecionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandBarSelected` |
| Primeiro plano (texto) | `Environment.CommandBarTextSelected` |
| Borda | `Environment.CommandBarSelectedBorder` |

**Ícone de comando: Estados de foco ou de foco**

![Ícone de comando ao focalizar ou focalizar](../../extensibility/ux-guidelines/media/0303-025_commandiconhover.png "0303-025_CommandIconHover")<br />Ícone de comando ao focalizar ou focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandBarMouseOverBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.CommandBarTextHover` |
| Borda | `Environment.CommandBarBorder` |

**Ícone de comando: Estados de foco ou foco, selecionado**

![Ícone de comando selecionado ao focalizar ou focalizar](../../extensibility/ux-guidelines/media/0303-026_commandiconhoverselected.png "0303-026_CommandIconHoverSelected")<br />Ícone de comando selecionado ao focalizar ou focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandBarHoverOverSelected` |
| Primeiro plano (texto) | `Environment.CommandBarTextHoverOverSelected` |
| Borda | `Environment.CommandBarHoverOverSelectedIconBorder` |

 **Ícone de comando: estado pressionado**

![Ícone de comando pressionado](../../extensibility/ux-guidelines/media/0303-027_commandiconpressed.png "0303-027_CommandIconPressed")<br />Ícone de comando pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandBarMouseDownBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.CommandBarTextMouseDown` |
| Borda | `Environment.CommandBarBorder` |

**Ícone de comando: estado desabilitado**

![Ícone de comando desabilitado](../../extensibility/ux-guidelines/media/0303-028_commandicondisabled.png "0303-028_CommandIconDisabled")<br />Ícone de comando desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | N/A (herda do plano de fundo da barra de comandos) |
| Primeiro plano (texto) | `Environment.CommandBarTextInactive` |
| Borda | N/D |

#### <a name="command-bar-combo-boxes"></a><a name="BKMK_CommandComboBox"></a> Caixas de combinação da barra de comandos

> [!IMPORTANT]
> As caixas de combinação são semelhantes a menus suspensos, mas incluem uma região de texto editável. Se o menu suspenso não incluir uma região de texto editável, use os tokens de cor para os menus [suspensos da barra de comandos](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandDropDown).

![Caixa de combinação da barra de comandos Redline](../../extensibility/ux-guidelines/media/0303-029_comboboxredline.png "0303-029_ComboBoxRedline")<br />Caixa de combinação da barra de comandos (Redline)

| Usar... | Não use... |
| --- | --- |
| ... ao criar caixas de combinação personalizadas. | ... para tudo o que você não quer que corresponda sempre à interface do usuário da barra de comandos. |
| ... ao criar um controle de barra de comandos semelhante a uma caixa de combinação. | ... Quando você tem acesso a uma caixa de combinação com estilo. |

**Campo de entrada da caixa de combinação da barra de comandos: estado padrão**

![Campo de entrada da caixa de combinação da barra de comandos](../../extensibility/ux-guidelines/media/0303-030_comboboxinputfield.png "0303-030_ComboBoxInputField")<br />Campo de entrada da caixa de combinação da barra de comandos

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ComboBoxBackground` |
| Primeiro plano (texto) | `Environment.ComboBoxText` |
| Borda | `Environment.ComboBoxBorder` |
| Separador | Sem separador |

**Botão suspenso da barra de comandos: estado padrão**

![Botão de remoção de&#45;caixa de combinação](../../extensibility/ux-guidelines/media/0303-031_comboboxdropdownbutton.png "0303-031_ComboBoxDropdownButton")<br />Botão suspenso da barra de comandos

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | N/A (herda do plano de fundo da barra de comandos) |
| Primeiro plano (glifo) | `Environment.ComboBoxGlyph` |

**Lista suspensa da barra de comandos: estado padrão**

![Lista suspensa da barra de comandos](../../extensibility/ux-guidelines/media/0303-032_comboboxdropdownlist.png "0303-032_ComboBoxDropdownList")<br />Lista suspensa da barra de comandos

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ComboBoxPopupBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.ComboBoxItemText` |
| Borda | `Environment.ComboBoxPopupBorder` |

**Campo de entrada da caixa de combinação da barra de comandos: estado de foco**

![Campo de entrada da caixa de combinação da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-033_comboboxinputfieldhover.png "0303-033_ComboBoxInputFieldHover")<br />Campo de entrada da caixa de combinação da barra de comandos ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ComboBoxMouseOverBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.ComboBoxMouseOverText` |
| Borda | `Environment.ComboBoxMouseOverBorder` |
| Separador | `Environment.ComboBoxMouseOverSeparator` |

 **Botão suspenso da barra de comandos: estado de foco**

![Botão suspenso da caixa de combinação da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-034_comboboxdropdownbuttonhover.png "0303-034_ComboBoxDropdownButtonHover")<br />Botão suspenso da barra de comandos ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ComboBoxButtonMouseOverBackground` |
| Primeiro plano (glifo) | `Environment.ComboBoxMouseOverGlyph` |

**Lista suspensa da barra de comandos: estado de foco**

 ![Lista suspensa da caixa de combinação da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-035_comboboxdropdownlisthover.png "0303-035_ComboBoxDropdownListHover")<br />Lista suspensa da barra de comandos ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Plano de fundo (item de menu) | `Environment.ComboBoxItemMouseOverBackground` |
| Primeiro plano (texto) | `Environment.ComboBoxItemMouseOverText` |
| Border (item de menu) | `Environment.ComboBoxItemMouseOverBorder` |

 **Campo de entrada da caixa de combinação da barra de comandos: estado focalizado**

![Campo de entrada da caixa de combinação da barra de comandos focado](../../extensibility/ux-guidelines/media/0303-036_comboboxinputfieldfocused.png "0303-036_ComboBoxInputFieldFocused")<br />Campo de entrada da caixa de combinação da barra de comandos focado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ComboBoxFocusedBackground` |
| Primeiro plano (texto) | `Environment.ComboBoxFocusedText` |
| Borda | `Environment.ComboBoxFocusedBorder` |
| Separador | `Environment.ComboBoxFocusedButtonSeparator` |

**Botão suspenso da barra de comandos: estado focalizado**

![Botão suspenso de barra de comandos focado](../../extensibility/ux-guidelines/media/0303-037_comboboxdropdownbuttonfocused.png "0303-037_ComboBoxDropdownButtonFocused")<br />Botão suspenso de barra de comandos focado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ComboBoxFocusedButtonBackground` |
| Primeiro plano (glifo) | `Environment.ComboBoxFocusedGlyph` |

 **Campo de entrada da caixa de combinação da barra de comandos: estado pressionado**

![Campo de entrada da caixa de combinação da barra de comandos pressionada](../../extensibility/ux-guidelines/media/0303-038_comboboxinputfieldpressed.png "0303-038_ComboBoxInputFieldPressed")<br />Campo de entrada da caixa de combinação da barra de comandos pressionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ComboBoxMouseDownBackground` |
| Primeiro plano (texto) | `Environment.ComboBoxMouseDownText` |
| Borda | `Environment.ComboBoxMouseDownBorder` |
| Separador | `Environment.ComboBoxMouseDownSeparator` |

**Botão suspenso da barra de comandos: estado pressionado**

![Botão suspenso da caixa de combinação da barra de comandos pressionada](../../extensibility/ux-guidelines/media/0303-039_comboboxdropdownbuttonpressed.png "0303-039_ComboBoxDropdownButtonPressed")<br />Botão suspenso da barra de comandos pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ComboBoxButtonMouseDownBackground` |
| Primeiro plano (glifo) | `Environment.ComboBoxMouseDownGlyph` |

**Campo de entrada da caixa de combinação da barra de comandos: estado desabilitado**

![Campo de entrada da caixa de combinação desabilitada da barra de comandos](../../extensibility/ux-guidelines/media/0303-041_comboboxinputfielddisabled.png "0303-041_ComboBoxInputFieldDisabled")<br />Campo de entrada da caixa de combinação desabilitada da barra de comandos

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ComboBoxDisabledBackground` |
| Primeiro plano (texto) | `Environment.ComboBoxDisabledText` |
| Borda | `Environment.ComboBoxDisabledBorder` |
| Separador | Sem separador |

**Botão suspenso da barra de comandos: estado desabilitado**

![Botão suspenso da caixa de combinação da barra de comandos desabilitada](../../extensibility/ux-guidelines/media/0303-040_comboboxdropdownbuttondisabled.png "0303-040_ComboBoxDropdownButtonDisabled")<br />Botão suspenso da barra de comandos desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | Nenhum |
| Primeiro plano (glifo) | `Environment.ComboBoxDisabledGlyph` |

#### <a name="command-bar-drop-downs"></a><a name="BKMK_CommandDropDown"></a> Menus suspensos da barra de comandos

> [!IMPORTANT]
> Os menus suspensos são semelhantes às caixas de combinação, mas não têm regiões de texto editáveis. Se a lista suspensa incluir uma região de texto editável, use os tokens de cor das [caixas de combinação da barra de comandos](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandComboBox).

![Menu suspenso da barra de comandos (Redline)](../../extensibility/ux-guidelines/media/0303-042_dropdownredline.png "0303-042_DropdownRedline")<br />Menu suspenso da barra de comandos (Redline)

| Usar... | Não use... |
| --- | --- |
| ... Quando você estiver criando controles de lista suspensa personalizados. | ... para qualquer coisa que não seja semelhante a uma lista suspensa. |
| | ... para caixas de combinação ou botões de divisão. |

**Campo de seleção suspensa da barra de comandos: estado padrão**

![Campo de seleção suspensa da barra de comandos padrão](../../extensibility/ux-guidelines/media/0303-043_dropdownselectionfield.png "0303-043_DropdownSelectionField")<br />Campo de seleção suspensa da barra de comandos padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.DropDownBackground` |
| Primeiro plano (texto) | `DropDownText` |
| Borda | `DropDownBorder` |
| Separador | Sem separador |

**Botão suspenso da barra de comandos: estado padrão**

![Botão suspenso da barra de comandos padrão](../../extensibility/ux-guidelines/media/0303-044_dropdownbutton.png "0303-044_DropdownButton")<br />Botão suspenso da barra de comandos padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | Nenhum |
| Primeiro plano (glifo) | `Environment.DropDownGlyph` |

**Lista suspensa da barra de comandos: estado padrão**

![Lista suspensa da barra de comandos padrão](../../extensibility/ux-guidelines/media/0303-045_dropdownlist.png "0303-045_DropdownList")<br />Lista suspensa da barra de comandos padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.DropDownPopupBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.ComboBoxItemText` |
| Borda | `Environment.DropDownPopupBorder` |
| Shadow | `Environment.DropShadowBackground` |

**Campo de seleção suspensa da barra de comandos: estado de foco**

![Campo de seleção suspensa da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-046_dropdownselectionfieldhover.png "0303-046_DropdownSelectionFieldHover")<br />Campo de seleção suspensa da barra de comandos ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.DropDownMouseOverBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.DropDownMouseOverText` |
| Borda | `Environment.DropDownMouseOverBorder` |
| Separador | `Environment.DropDownButtonMouseOverSeparator` |

**Botão suspenso da barra de comandos: estado de foco**

![Botão suspenso da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-047_dropdownbuttonhover.png "0303-047_DropdownButtonHover")<br />Botão suspenso da barra de comandos ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.DropDownButtonMouseOverBackground` |
| Primeiro plano (glifo) | `Environment.DropDownMouseOverGlyph` |

**Lista suspensa da barra de comandos: estado de foco**

![Lista suspensa da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-048_dropdownlisthover.png "0303-048_DropdownListHover")<br />Lista suspensa da barra de comandos ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Plano de fundo (item de menu) | `Environment.ComboBoxItemMouseOverBackground` |
| Primeiro plano (texto) | `Environment.ComboBoxItemMouseOverText` |
| Border (item de menu) | `Environment.ComboBoxItemMouseOverBorder` |

 **Campo de seleção suspensa da barra de comandos: estado pressionado**

![Descartar&#45;campo de seleção pressionado](../../extensibility/ux-guidelines/media/0303-049_dropdownselectionfieldpressed.png "0303-049_DropdownSelectionFieldPressed")<br />Campo de seleção suspensa da barra de comandos pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.DropDownMouseDownBackground` |
| Primeiro plano (texto) | `Environment.DropDownMouseDownText` |
| Borda | `Environment.DropDownMouseDownBorder` |
| Separador | `Environment.DropDownButtonMouseDownSeparator` |

**Botão suspenso da barra de comandos: estado pressionado**

![Botão suspenso da barra de comandos pressionado](../../extensibility/ux-guidelines/media/0303-050_dropdownbuttonpressed.png "0303-050_DropdownButtonPressed")<br />Botão suspenso da barra de comandos pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.DropDownButtonMouseDownBackground` |
| Primeiro plano (glifo) | `Environment.DropDownMouseDownGlyph` |

**Campo de seleção suspensa da barra de comandos: estado desabilitado**

![Campo de seleção suspensa da barra de comandos desabilitada](../../extensibility/ux-guidelines/media/0303-051_dropdownselectionfielddisabled.png "0303-051_DropdownSelectionFieldDisabled")<br />Campo de seleção suspensa da barra de comandos desabilitada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.DropDownDisabledBackground` |
| Primeiro plano (texto) | `Environment.DropDownDisabledText` |
| Borda | `Environment.DropDownDisabledBorder` |
| Separador | Sem separador |

**Botão suspenso da barra de comandos: estado desabilitado**

![Botão suspenso da barra de comandos desabilitado](../../extensibility/ux-guidelines/media/0303-052_dropdownbuttondisabled.png "0303-052_DropdownButtonDisabled")<br />Botão suspenso da barra de comandos desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | N/D |
| Primeiro plano (glifo) | `Environment.DropDownDisabledGlyph` |

#### <a name="command-bar-split-buttons"></a>Botões de divisão da barra de comandos
Os botões de divisão compartilham vários nomes de token com outros controles de barra de comandos, como botões, menus e texto da barra de comandos. Todos os nomes de token de ações e botões suspensos necessários são repetidos aqui para sua conveniência. As listas suspensas do botão de divisão são implementações dos [menus da barra de comandos](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandMenus).

![Botão de divisão Redline](../../extensibility/ux-guidelines/media/0303-053_splitbuttonredline.png "0303-053_SplitButtonRedline")<br />Botão de divisão da barra de comandos (Redline)

| Usar... | Não use... |
| --- | --- |
| ... Quando você estiver criando um botão de divisão personalizado. | ... para outros tipos de botões. |
| | ... em qualquer combinação de plano de fundo/primeiro plano diferente de especificada. |

**Botão de divisão da barra de comandos: estado padrão**

![Botão de divisão da barra de comandos padrão](../../extensibility/ux-guidelines/media/0303-054_splitbutton.png "0303-054_SplitButton")<br />Botão de divisão da barra de comandos padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | Nenhum |
| Primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Primeiro plano (glifo) | `Environment.CommandBarSplitButtonGlyph` |
| Borda | N/D |
| Separador | N/D |

**Botão de divisão da barra de comandos: estado de foco**

![Botão de divisão da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-055_splitbuttonhover.png "0303-055_SplitButtonHover")<br />Botão de divisão da barra de comandos ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandBarMouseOverBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.CommandBarTextHover` |
| Primeiro plano (glifo) | `Environment.CommandBarSplitButtonMouseOverGlyph` |
| Borda | `Environment.CommandBarBorder` |
| Separador | `Environment.CommandBarSplitButtonSeparator` |

**Botão de divisão da barra de comandos: estado pressionado**

![Botão de divisão da barra de comandos pressionado](../../extensibility/ux-guidelines/media/0303-056_splitbuttonpressed.png "0303-056_SplitButtonPressed")<br />Botão de divisão da barra de comandos pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandBarMouseDownBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.CommandBarTextMouseDown` |
| Primeiro plano (glifo) | `Environment.CommandBarSplitButtonMouseDownGlyph` |
| Borda | `Environment.CommandBarBorder` |
| Separador | N/D |

**Botão de divisão da barra de comandos: estado desabilitado**

![Botão de divisão da barra de comandos desabilitado](../../extensibility/ux-guidelines/media/0303-057_splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br />Botão de divisão da barra de comandos desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | N/D |
| Primeiro plano (texto) | `Environment.ComboBoxItemTextInactive` |
| Primeiro plano (glifo) | `Environment.CommandBarTextInactive` |
| Borda | N/D |
| Separador | N/D |

#### <a name="command-bar-more-options-and-overflow-buttons"></a>Botões ' mais opções ' e ' estouro ' da barra de comandos
O botão "mais opções" é usado quando um grupo de barras de comandos é personalizável com a adição ou remoção de botões de barra de comandos relacionados. O botão "estouro" é exibido quando uma barra de comandos é truncada devido à falta de espaço horizontal e, ao clicar, mostra um menu contendo os botões da barra de comandos que não podem ser exibidos. As cores desses dois botões são controladas pelo mesmo conjunto de nomes de token.

![Botão ' mais opções ' da barra de comandos (Redline)](../../extensibility/ux-guidelines/media/0303-058_moreoptionsredline.png "0303-058_MoreOptionsRedline")<br />Botão ' mais opções ' da barra de comandos (Redline)

| Usar... | Não use... |
| --- | --- |
| ... para os botões ' mais opções ' ou ' estouro ' personalizados. | ... para botões que não têm funcionalidade semelhante a um botão ' mais opções ' ou ' estouro '. |

**Botões ' mais opções ' e ' estouro ' da barra de comandos: estado padrão**

![Botão ' mais opções ' da barra de comandos padrão](../../extensibility/ux-guidelines/media/0303-059_moreoptions.png "0303-059_MoreOptions")<br />Botão ' mais opções ' da barra de comandos padrão

![Botão ' estouro ' da barra de comandos padrão](../../extensibility/ux-guidelines/media/0303-060_overflow.png "0303-060_Overflow")<br />Botão ' estouro ' da barra de comandos padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandBarOptionsBackground` |
| Primeiro plano (glifo) | `Environment.CommandBarOptionsGlyph` |

**Botões ' mais opções ' e ' estouro ' da barra de comandos: estado de foco**

![Botão ' mais opções ' da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-061_moreoptionshover.png "0303-061_MoreOptionsHover")<br />Botão ' mais opções ' da barra de comandos ao focalizar

![Botão "estouro" da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-062_overflowoptions.png "0303-062_OverflowOptions")<br />Botão "estouro" da barra de comandos ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandBarOptionsMouseOverBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (glifo) | `Environment.CommandBarOptionsMouseDownGlyph` |

**Botões ' mais opções ' e ' estouro ' da barra de comandos: estado pressionado**

![Botão ' mais opções ' da barra de comandos pressionado](../../extensibility/ux-guidelines/media/0303-063_moreoptionspressed.png "0303-063_MoreOptionsPressed")<br />Botão ' mais opções ' da barra de comandos pressionado

![Estouro pressionado](../../extensibility/ux-guidelines/media/0303-064_overflowpressed.png "0303-064_OverflowPressed")<br />Botão ' estouro ' da barra de comandos pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.CommandBarOptionsMouseDownBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (glifo) | `Environment.CommandBarOptionsMouseDownGlyph` |

## <a name="document-windows"></a>Janelas de documentos
Não é necessário replicar as janelas de documentos, pois elas são fornecidas pelo ambiente do Visual Studio. No entanto, você pode decidir que deseja aproveitar as cores usadas em janelas de documentos para que sua interface do usuário sempre pareça consistente com essa parte do ambiente do Visual Studio.

Ao usar os tokens de cor da janela do documento, tenha cuidado para usá-los somente para elementos semelhantes e sempre em pares. Se você não fizer isso, poderá obter resultados inesperados em sua interface do usuário.

### <a name="document-window-frames"></a>Quadros de janela do documento
As janelas de documentos podem ser encaixadas no IDE ou flutuantes como uma janela separada. Quando uma janela de documento está flutuante fora do IDE, ela ainda fica em um bom documento e tem cores de plano de fundo, borda, texto e tabulação que são iguais a quando faz parte do IDE. No entanto, o documento fica dentro de um quadro que tem suas próprias cores de plano de fundo, borda e texto. Quando janelas de ferramentas são encaixadas no documento bem, elas herdam o comportamento e a cor de suas guias dos nomes de token da janela do documento.

![Janela de documento encaixado (Redline)](../../extensibility/ux-guidelines/media/0303-065_dockeddocumentwindowredline.png "0303-065_DockedDocumentWindowRedline")<br />Janela de documento encaixado (Redline)

![Janela de documento flutuante (Redline)](../../extensibility/ux-guidelines/media/0303-066_floatingdocumentwindowredline.png "0303-066_FloatingDocumentWindowRedline")<br />Janela de documento flutuante (Redline)

| Usar... | Não use... |
| --- | --- |
| ... em qualquer lugar em que você esteja criando a interface do usuário que deseja corresponder à janela do documento. | ...  para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema. |

**Janela de documento encaixada ou flutuante: estado padrão**

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | Depende do tipo de documento |
| Primeiro plano (texto) | Depende do tipo de documento |
| Borda | `Environment.ToolWindowBorder` |

**Quadro de janela de documento flutuante focalizado: estado padrão**

![Quadro de janela de documento flutuante com foco padrão](../../extensibility/ux-guidelines/media/0303-067_framefocused.png "0303-067_FrameFocused")<br />Quadro de janela de documento flutuante com foco padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolWindowFloatingFrame` |
| Primeiro plano (texto) | `Environment.ToolWindowFloatingFrame` |
| Primeiro plano (glifo) | `Environment.RaftedWindowButtonActiveGlyph` |
| Borda | `Environment.MainWindowActiveDefaultBorder` |
| Borda (glifo) | `Environment.RaftedWindowButtonActiveBorder`<br />(Definido como transparente) |

**Quadro de janela de documento flutuante sem foco: estado padrão**

![Quadro de janela de documento flutuante padrão sem foco](../../extensibility/ux-guidelines/media/0303-068_frameunfocused.png "0303-068_FrameUnfocused")<br />Quadro de janela de documento flutuante padrão sem foco

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolWindowFloatingFrameInactive` |
| Primeiro plano (texto) | `Environment.ToolWindowFloatingFrameInactive` |
| Primeiro plano (glifo) | `Environment.RaftedWindowButtonInactiveGlyph` |
| Borda | `Environment.MainWindowInactiveBorder` |
| Borda (glifo) | `Environment.RaftedWindowButtonInactiveBorder`<br />(Definido como transparente) |

**Quadro de janela de documento flutuante focalizado: estado de foco**

![Quadro de janela de documento flutuante focalizado e focalizado](../../extensibility/ux-guidelines/media/0303-069_framefocusedhover.png "0303-069_FrameFocusedHover")<br />Quadro de janela de documento flutuante focalizado e focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Plano de fundo (glifo) | `Environment.RaftedWindowButtonHoverActive` |
| Primeiro plano (glifo) | `Environment.RaftedWindowButtonHoverActiveGlyph` |
| Borda (glifo) | `Environment.RaftedWindowButtonHoverActiveBorder` |

**Quadro de janela de documento flutuante, não focalizado: estado de foco**

![Quadro de janela de documento flutuante sem foco ao focalizar](../../extensibility/ux-guidelines/media/0303-070_frameunfocusedhover.png "0303-070_FrameUnfocusedHover")<br />Quadro de janela de documento flutuante sem foco ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Plano de fundo (glifo) | `EnvironmentRaftedWindowButtonHoverInactive` |
| Primeiro plano (glifo) | `Environment.RaftedWindowButtonHoverInactiveGlyph` |
| Borda (glifo) | `Environment.RaftedWindowButtonHoverInactiveBorder` |

**Quadro de janela de documento flutuante focalizado: pressionado estado**

![Quadro de janela de documento flutuante focalizado ao pressionar](../../extensibility/ux-guidelines/media/0303-071_framefocusedpressed.png "0303-071_FrameFocusedPressed")<br />Quadro de janela de documento flutuante focalizado ao pressionar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Plano de fundo (glifo) | `Environment.RaftedWindowButtonDown` |
| Primeiro plano (glifo) | `Environment.RaftedWindowButtonDownGlyph` |
| Borda (glifo) | `Environment.RaftedWindowButtonDownBorder` |

### <a name="document-tabs"></a>Guias de documento
As guias de documento ficam no canal de guia para indicar quais documentos estão abertos no momento, juntamente com qual deles é o documento atual selecionado ou ativo. As janelas de ferramentas também podem ser encaixadas no canal da guia do documento se o usuário as colocar lá. Nessa situação, eles usam as mesmas cores de guia que as janelas de documentos. Se você estiver criando a interface do usuário que deseja sempre corresponder às cores da janela do documento (incluindo atualizações de tema ou se novos temas estiverem instalados), faça referência a esses tokens de cor.

![Guias de documento (Redline)](../../extensibility/ux-guidelines/media/0303-072_documenttabredline.png "0303-072_DocumentTabRedline")<br />Guias de documento (Redline)

| Usar... | Não use... |
| --- | --- |
| ... em qualquer lugar em que você estiver criando a interface do usuário que deseja corresponder às guias de documentos e selecionar automaticamente as atualizações de tema ou novas cores de tema. | ... para qualquer interface do usuário que você não deseja alterar automaticamente quando o Shell tem uma atualização de tema. |

#### <a name="open-document-tabs"></a>Abrir guias de documento
Cada documento aberto tem uma guia no canal da guia do documento que exibe seu nome. Os documentos podem ser selecionados ou abertos em segundo plano, e suas guias refletem esses Estados:

- A guia selecionada representa o documento que está atualmente exibido no documento. Uma guia selecionada tem uma borda de documento que se estende pela borda superior do documento bem.

- As guias de segundo plano são guias de documentos que não são a guia selecionada no momento. Depois de clicados, eles se tornam a guia selecionada e adquirem todas as cores de plano de fundo, borda e texto desses nomes de token.

![Abrir a guia documento (Redline)](../../extensibility/ux-guidelines/media/0303-073_opendocumenttabredline.png "0303-073_OpenDocumentTabRedline")<br />Abrir a guia documento (Redline)

| Usar... | Não use... |
| --- | --- |
| ... Quando você estiver criando guias de documento personalizado. | ... para obter as guias provisórios (visualização). |
| | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema. |

**Selecionado, guia documento focalizado**

![Selecionado, guia documento focalizado](../../extensibility/ux-guidelines/media/0303-074_selectedtabfocused.png "0303-074_SelectedTabFocused")<br />Selecionado, guia documento focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.FileTabSelectedGradientTop`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.FileTabSelectedText` |
| Borda | `Environment.FileTabSelectedBorder`<br />(Defina como a mesma cor como plano de fundo.) |
| Borda do documento | `Environment.FileTabDocumentBorderBackground` |

**Selecionado, guia documento não focalizado**

![Selecionado, guia documento não focalizado](../../extensibility/ux-guidelines/media/0303-075_selectedtabunfocused.png "0303-075_SelectedTabUnfocused")<br />Selecionado, guia documento não focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.FileTabInactiveGradientTop`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.FileTabInactiveText` |
| Borda | `Environment.FileTabInactiveBorder`<br />(Defina como a mesma cor como plano de fundo.) |
| Borda do documento | `Environment.FileTabInactiveDocumentBorderBackground` |

**Guia documento em segundo plano: estado padrão**

![Guia documento de plano de fundo padrão](../../extensibility/ux-guidelines/media/0303-076_backgroundtab.png "0303-076_BackgroundTab")<br />Guia documento de plano de fundo padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.FileTabBackground` |
| Primeiro plano (texto) | `Environment.FileTabText` |
| Borda | `Environment.FileTabBorder`<br />(Defina como a mesma cor como plano de fundo.) |

**Guia documento de plano de fundo: estado de foco**

![Guia documento de plano de fundo ao focalizar](../../extensibility/ux-guidelines/media/0303-077_backgroundtabhover.png "0303-077_BackgroundTabHover")<br />Guia documento de plano de fundo ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.FileTabHotGradientTop`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.FileTabHotText` |
| Borda | `Environment.FileTabHotBorder`<br />(Defina como a mesma cor como plano de fundo.) |

#### <a name="preview-tab"></a>Guia de visualização
Também chamada de guia "provisionar". A guia Visualização é exibida no lado direito do canal da guia do documento quando o usuário clica em um item na janela de ferramentas do Gerenciador de Soluções. Ele atua como uma visualização do documento e também dá ao usuário a opção de manter o documento aberto no lado esquerdo do canal da guia do documento. Somente uma guia de visualização aberta pode ser aberta por vez. As guias de visualização têm os Estados de segundo plano e selecionados, como guias abertas e podem ser focadas ou desfocadas em seu estado ativo.

![Guia de visualização (Redline)](../../extensibility/ux-guidelines/media/0303-078_previewtabredline.png "0303-078_PreviewTabRedline")<br />Guia de visualização (Redline)

| Usar... | Não use... |
| --- | --- |
| ... em qualquer lugar que você esteja criando a visualização provisória e queira que algum elemento corresponda à cor da guia de visualização atual. | ... para qualquer tipo de documento ou guia que não seja provisório (versão prévia). |
| | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema. |

**Com foco, guia de visualização selecionada**

![Com foco, guia de visualização selecionada](../../extensibility/ux-guidelines/media/0303-079_previewtabfocused.png "0303-079_PreviewTabFocused")<br />Com foco, guia de visualização selecionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.FileTabProvisionalSelectedActive` |
| Primeiro plano (texto) | `Environment.FileTabProvisionalSelectedActiveForeground` |
| Borda | `Environment.FileTabProvisionalSelectedActiveBorder`<br />(Defina como a mesma cor como plano de fundo.) |
| Borda do documento | `Environment.FileTabProvisionalSelectedActiveBorder` |

**Não focalizado, guia de visualização selecionada**

![Não focalizado, guia de visualização selecionada](../../extensibility/ux-guidelines/media/0303-080_previewtabunfocused.png "0303-080_PreviewTabUnfocused")<br />Não focalizado, guia de visualização selecionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.FileTabProvisionalSelectedInactive` |
| Primeiro plano (texto) | `Environment.FileTabProvisionalSelectedInactiveForeground` |
| Borda | `Environment.FileTabProvisionalSelectedInactiveBorder` |
| Borda do documento | `Environment.FileTabProvisionalSelectedInactiveBorder` |

**Guia de visualização em segundo plano: estado padrão**

![Guia de visualização de segundo plano padrão](../../extensibility/ux-guidelines/media/0303-081_previewbackgroundtab.png "0303-081_PreviewBackgroundTab")<br />Guia de visualização de segundo plano padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.FileTabProvisionalInactive` |
| Primeiro plano (texto) | `Environment.FileTabProvisionalInactiveForeground` |
| Borda | `Environment.FileTabProvisionalInactiveBorder`<br />(Defina como a mesma cor como plano de fundo.) |

**Guia de visualização em segundo plano: estado de foco**

![Guia de visualização em segundo plano ao focalizar](../../extensibility/ux-guidelines/media/0303-082_previewbackgroundtabhover.png "0303-082_PreviewBackgroundTabHover")<br />Guia de visualização em segundo plano ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.FileTabProvisionalHover` |
| Primeiro plano (texto) | `Environment.FileTabProvisionalHoverForeground` |
| Borda | `Environment.FileTabProvisionalHoverBorder`<br />(Defina como a mesma cor como plano de fundo.) |

#### <a name="document-overflow-button"></a>Botão de estouro de documento
O botão de estouro de documento estará presente se houver um ou mais documentos abertos, independentemente de haver espaço vertical na configuração atual para ajustar todas as guias do documento. O menu suspenso de estouro de documento, que é controlado pelas cores do [menu da barra de comandos](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandMenus) , exibe uma lista de todos os documentos abertos, visíveis e ocultos, e as alterações de glifos de estouro, dependendo se todos os documentos abertos são exibidos no canal de guia.

![Botão de estouro de documento (Redline)](../../extensibility/ux-guidelines/media/0303-083_overflowredline.png "0303-083_OverflowRedline")<br />Botão de estouro de documento (Redline)

| Usar... | Não use... |
| --- | --- |
| ... Quando você estiver criando um botão de estouro de documento personalizado. | ... para a interface do usuário que não é semelhante a um botão de estouro. |
| | ... para botões de estouro da barra de comandos. |

**Botão de estouro de documento: estado padrão**

![Botão de estouro de documento padrão](../../extensibility/ux-guidelines/media/0303-084_overflow.png "0303-084_Overflow")<br />Botão de estouro de documento padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.DocWellOverflowButtonBackground` |
| Primeiro plano (glifo) | `Environment.DocWellOverflowButtonGlyph` |
| Borda | N/D |

**Botão de estouro de documento: estado de foco**

![Botão de estouro de documento ao focalizar](../../extensibility/ux-guidelines/media/0303-085_overflowhover.png "0303-085_OverflowHover")<br />Botão de estouro de documento ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.DocWellOverflowButtonMouseOverBackground` |
| Primeiro plano (glifo) | `Environment.DocWellOverflowButtonMouseOverGlyph` |
| Borda | `Environment.DocWellOverflowButtonMouseOverBorder` |

**Botão de estouro de documento: estado pressionado**

![Botão de estouro de documento ao pressionar](../../extensibility/ux-guidelines/media/0303-086_overflowpressed.png "0303-086_OverflowPressed")<br />Botão de estouro de documento ao pressionar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.DocWellOverflowButtonMouseDownBackground` |
| Primeiro plano (glifo) | `Environment.DocWellOverflowButtonMouseDownGlyph` |
| Borda | `Environment.DocWellOverflowButtonMouseDownBorder` |

### <a name="tagging"></a>Marcação
O Visual Studio dá suporte à marcação, que permite que um usuário declare palavras-chave pesquisáveis para fins de acompanhamento. Por exemplo, gerentes de projeto e desenvolvedores podem usar Team Foundation Server (TFS) para marcar itens de trabalho. As tabelas a seguir fornecem nomes de cor para a marca em si e o glifo "ícone de fechamento" que aparece nos Estados de focalizar e selecionados.

![Marcação no Visual Studio (Redline)](../../extensibility/ux-guidelines/media/0303-176_taggingredline.png "0303-176_TaggingRedline")<br />Marcação no Visual Studio (Redline)

| Usar... | Não use... |
| --- | --- |
| ... para a interface do usuário que dá suporte à marcação. | ... para qualquer outro tipo de interface do usuário. |

#### <a name="tags"></a>Marcações

**Marca: estado padrão**

![Marca padrão](../../extensibility/ux-guidelines/media/0303-177_tag.png "0303-177_Tag")<br />Marca padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Tag.Background` |
| Primeiro plano (texto) | `Tag.Background` |

**Marca: estado de foco**

![Marca ao focalizar](../../extensibility/ux-guidelines/media/0303-178_taghover.png "0303-178_TagHover")<br />Marca ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Tag.HoverBackground` |
| Primeiro plano (texto) | `Tag.HoverBackgroundText` |

**Marca: estado pressionado**

![Marca pressionada](../../extensibility/ux-guidelines/media/0303-179_tagpressed.png "0303-179_TagPressed")<br />Marca pressionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Tag.PressedBackground` |
| Primeiro plano (texto) | `Tag.PressedBackgroundText` |

**Marca: estado selecionado**

![Marca selecionada](../../extensibility/ux-guidelines/media/0303-180_tagselected.png "0303-180_TagSelected")<br />Marca selecionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Tag.SelectedBackground` |
| Primeiro plano (texto) | `Tag.SelectedBackgroundText` |

#### <a name="close-times-tag-glyph"></a>Glifo de marca de fechamento ( &times; )

**Glifo de marca de fechamento ( &times; ): estado padrão**

![Glifo de marca de fechamento padrão ( &times; )](../../extensibility/ux-guidelines/media/0303-181_tagglyph.png "0303-181_TagGlyph")<br />Glifo de marca de fechamento padrão ( &times; )

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | N/D |
| Primeiro plano (glifo) | `Tag.TagHoverGlyph` |

**Glifo de marca de fechamento ( &times; ): estado de foco**

![Fechar ( &times; ) glifo de marca ao focalizar](../../extensibility/ux-guidelines/media/0303-182_tagglyphhover.png "0303-182_TagGlyphHover")<br />Fechar ( &times; ) glifo de marca ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Tag.TagHoverGlyphHoverBackground` |
| Primeiro plano (glifo) | `Tag.TagHoverGlyphHover` |
| Borda | `Tag.TagHoverGlyphHoverBorder` |

**Glifo de &times; marca Close (): estado pressionado**

![Glifo de marca Close ( &times; ) pressionado](../../extensibility/ux-guidelines/media/0303-183_tagglyphpressed.png "0303-183_TagGlyphPressed")<br />Glifo de marca Close ( &times; ) pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Tag.TagHoverGlyphPressedBackground` |
| Primeiro plano (glifo) | `Tag.TagHoverGlyphPressed` |
| Borda | `Tag.TagHoverGlyphPressedBorder` |

**Marca selecionada com glifo de fechamento ( &times; ): estado padrão**

![Marca padrão selecionada com glifo de fechamento ( &times; )](../../extensibility/ux-guidelines/media/0303-184_tagselected.png "0303-184_TagSelected")<br />Marca padrão selecionada com glifo de fechamento ( &times; )

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | N/D |
| Primeiro plano (glifo) | `Tag.TagSelectedGlyph` |

**Marca selecionada com glifo de fechamento ( &times; ): estado de foco**

![Marca selecionada com glifo de fechamento ( &times; ) ao focalizar](../../extensibility/ux-guidelines/media/0303-185_tagselectedhover.png "0303-185_TagSelectedHover")<br />Marca selecionada com glifo de fechamento ( &times; ) ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Tag.TagSelectedGlyphHoverBackground` |
| Primeiro plano (glifo) | `Tag.TagSelectedGlyphHover` |
| Borda | `Tag.TagSelectedGlyphHoverBorder` |

**Marca selecionada com glifo de fechamento ( &times; ): estado pressionado**

![Marcada, marca pressionada com glifo de fechamento ( &times; )](../../extensibility/ux-guidelines/media/0303-186_tagselectedpressed.png "0303-186_TagSelectedPressed")<br />Marcada, marca pressionada com glifo de fechamento ( &times; )

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Tag.TagSelectedGlyphPressedBackground` |
| Primeiro plano (glifo) | `Tag.TagSelectedGlyphPressed` |
| Borda | `Tag.TagSelectedGlyphPressedBorder` |

## <a name="tool-windows"></a>Janelas da ferramenta
Não há necessidade de replicar janelas de ferramentas, pois elas são fornecidas pelo ambiente do Visual Studio. No entanto, você pode decidir que deseja aproveitar as cores usadas nas janelas de ferramentas para que sua interface do usuário sempre pareça consistente com essa parte do ambiente do Visual Studio.

![Janela de ferramentas (Redline)](../../extensibility/ux-guidelines/media/0303-087_toolwindowredline.png "0303-087_ToolWindowRedline")<br />Janela de ferramentas (Redline)

| Usar... | Não use... |
| --- | --- |
| ... em qualquer lugar que você esteja criando a interface do usuário que deseja corresponder às janelas de ferramentas. | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema. |

### <a name="tool-window-frame"></a>Quadro da janela de ferramentas
Janelas de ferramentas no Visual Studio são usadas para várias tarefas diferentes e podem existir em um de vários Estados diferentes. Se uma janela de ferramenta estiver aberta, ela poderá ser atribuída a qualquer um dos quatro lados da área do documento. As janelas de ferramentas também podem flutuar fora do IDE, o que permite que elas sejam reposicionadas em qualquer lugar na tela do usuário. Janelas flutuantes sempre ficam na parte superior do IDE. Por fim, as janelas de ferramentas podem ser encaixadas como janelas de documentos e exibidas também como uma guia no documento. Janelas de ferramentas que foram encaixadas como janelas de documentos são coloridas em parte usando nomes de token de janela de documento.

![Quadro de janela de ferramenta (Redline)](../../extensibility/ux-guidelines/media/0303-088_toolwindowframeredline.png "0303-088_ToolWindowFrameRedline")<br />Quadro de janela de ferramenta (Redline)

| Usar... | Não use... |
| --- | --- |
| ...  em qualquer lugar que você esteja criando a interface do usuário que deseja corresponder às janelas de ferramentas. | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema. |

**Janela de ferramentas encaixada**

![Janela de ferramentas encaixada](../../extensibility/ux-guidelines/media/0303-089_toolwindowdocked.png "0303-089_ToolWindowDocked")<br />Janela de ferramentas encaixada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolWindowBackground` |
| Borda | `Environment.ToolWindowBorder` |

**Janela de ferramentas flutuante e focalizada**

![Janela de ferramentas flutuante e focalizada](../../extensibility/ux-guidelines/media/0303-090_toolwindowfocused.png "0303-090_ToolWindowFocused")<br />Janela de ferramentas flutuante e focalizada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolWindowBackground` |
| Borda | `Environment.MainWindowActiveDefaultBorder` |

**Janela de ferramentas flutuante, desfocada**

![Janela de ferramentas flutuante, desfocada](../../extensibility/ux-guidelines/media/0303-091_toolwindowunfocused.png "0303-091_ToolWindowUnfocused")<br />Janela de ferramentas flutuante, desfocada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolWindowBackground` |
| Borda | `Environment.MainWindowInactiveBorder` |

### <a name="toolbox-like-windows"></a>Caixa de ferramentas-como Windows
A caixa de ferramentas é uma das janelas de ferramentas comuns usadas com mais frequência no Visual Studio. Ele é essencialmente um controle de árvore com um tema e estilo especiais aplicados.

![Janela semelhante a caixa de ferramentas (Redline)](../../extensibility/ux-guidelines/media/0303-189_toolboxredline.png "0303-189_ToolboxRedline")<br />Janela semelhante a caixa de ferramentas (Redline)

| Usar... | Não use... |
| --- | --- |
| ... Quando você está criando uma janela de ferramentas que deseja sempre consistente com a caixa de ferramentas do Shell. | ... para qualquer coisa que não seja semelhante à interface do usuário da caixa de ferramentas, ou se você não tiver certeza se a sua interface do usuário terá problemas se as cores da caixa de ferramentas do Shell forem alteradas. |

**Nós da caixa de ferramentas: estado padrão**

![Nó pai da caixa de ferramentas padrão](../../extensibility/ux-guidelines/media/0303-190_toolboxparentnode.png "0303-190_ToolboxParentNode")<br />Nó pai da caixa de ferramentas padrão

![Nó filho da caixa de ferramentas padrão](../../extensibility/ux-guidelines/media/0303-191_toolboxchildnode.png "0303-191_ToolboxChildNode")<br />Nó filho da caixa de ferramentas padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolboxContent`<br />Títulos |
| Segundo plano | `Environment.ToolWindowBackground`<br />(Itens individuais ou janela inteira, se não houver controles disponíveis) |
| Borda | Nenhum |
| Primeiro plano (glifo) | `Environment.ToolboxContent` |
| Primeiro plano (texto) | `Environment.ToolboxContent` |

**Nós filho da caixa de ferramentas: estado de foco**

![Nó filho da caixa de ferramentas ao focalizar](../../extensibility/ux-guidelines/media/0303-192_toolboxchildnodehover.png "0303-192_ToolboxChildNodeHover")<br />Nó filho da caixa de ferramentas ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolboxContentMouseOver`<br />(Somente itens individuais) |
| Borda | Nenhum |
| Primeiro plano (texto) | `Environment.ToolboxContentMouseOver`<br />(Somente itens individuais) |

**Nós da caixa de ferramentas selecionados: estado focalizado**

![Foco, nó pai da caixa de ferramentas selecionada](../../extensibility/ux-guidelines/media/0303-193_toolboxparentnodefocused.png "0303-193_ToolboxParentNodeFocused")<br />Foco, nó pai da caixa de ferramentas selecionada

![Foco, nó filho da caixa de ferramentas selecionada](../../extensibility/ux-guidelines/media/0303-194_toolboxchildnodefocused.png "0303-194_ToolboxChildNodeFocused")<br />Foco, nó filho da caixa de ferramentas selecionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `TreeView.SelectedItemActive`<br />Categoria da [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) |
| Borda | `TreeView.FocusVisualBorder`<br />Categoria da [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) |
| Primeiro plano (glifo) | `TreeView.SelectedItemActive`<br />Categoria da [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) |
| Primeiro plano (texto) | `TreeView.SelectedItemActive`<br />Categoria da [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) |

**Nós da caixa de ferramentas selecionados: estado não focalizado**

![Nó pai da caixa de ferramentas selecionado, não focalizado](../../extensibility/ux-guidelines/media/0303-195_toolboxparentnodeunfocused.png "0303-195_ToolboxParentNodeUnfocused")<br />Nó pai da caixa de ferramentas selecionado, não focalizado

![Nó filho da caixa de ferramentas selecionado, não focalizado](../../extensibility/ux-guidelines/media/0303-196_toolboxchildnodeunfocused.png "0303-196_ToolboxChildNodeUnfocused")<br />Nó filho da caixa de ferramentas selecionado, não focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `TreeView.SelectedItemInactive`<br />Categoria da [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) |
| Borda | Nenhum |
| Primeiro plano (glifo) | `TreeView.SelectedItemInactive`<br />Categoria da [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) |
| Primeiro plano (texto) | `TreeView.SelectedItemInactive`<br />Categoria da [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) |

### <a name="tool-window-title-bar"></a>Barra de título da janela de ferramentas
A borda da barra de título não é uma borda verdadeira, é uma linha espessa na parte superior da barra de título. Ele não tem um nome de token para seu estado sem foco.

![Barra de título da janela de ferramentas (Redline)](../../extensibility/ux-guidelines/media/0303-092_toolwindowtitlebarredline.png "0303-092_ToolWindowTitleBarRedline")<br />Barra de título da janela de ferramentas (Redline)

| Usar... | Não use... |
| --- | --- |
| ... em qualquer lugar que você esteja criando a interface do usuário que deseja corresponder às janelas de ferramentas. | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema. |

**Barra de título focalizada**

![Barra de título focalizada](../../extensibility/ux-guidelines/media/0303-093_titlebarfocused.png "0303-093_TitleBarFocused")<br />Barra de título focalizada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.TitleBarActiveGradientBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.TitleBarActiveText` |
| Borda | `Environment.TitleBarActiveBorder`<br />(Defina como a mesma cor como plano de fundo.) |
| Identificador de arrastar | `Environment.TitleBarDragHandleActive` |

**Barra de título sem foco**

![Barra de título desfocada](../../extensibility/ux-guidelines/media/0303-094_titlebarunfocused.png "0303-094_TitleBarUnfocused")<br />Barra de título sem foco

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.TitleBarInactiveGradientBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.TitleBarInactiveText` |
| Borda | N/D |
| Identificador de arrastar | `Environment.TitleBarDragHandle` |

#### <a name="tool-window-title-bar-buttons"></a>Botões da barra de título da janela de ferramentas
![Botão da barra de título (Redline)](../../extensibility/ux-guidelines/media/0303-095_titlebarbuttonredline.png "0303-095_TitleBarButtonRedline")<br />Botão da barra de título (Redline)

| Usar... | Não use... |
| --- | --- |
| ... para botões que aparecem na interface do usuário que usa tokens de cor das barras de título da janela de ferramentas. | ... para botões que aparecem em outros locais. |
| | ... em qualquer combinação de plano de fundo/primeiro plano diferente de especificada. |

**Botões da barra de título focalizado: estado padrão**

![Padrão, botões de barra de título focalizados](../../extensibility/ux-guidelines/media/0303-096_titlebarbuttonfocused.png "0303-096_TitleBarButtonFocused")<br />Padrão, botões de barra de título focalizados

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | N/D |
| Primeiro plano (glifo) | `Environment.ToolWindowButtonActiveGlyph` |
| Borda | N/D |

**Botões da barra de título sem foco: estado padrão**

![Padrão, botões de barra de título sem foco](../../extensibility/ux-guidelines/media/0303-097_titlebarbuttonunfocused.png "0303-097_TitleBarButtonUnfocused")<br />Padrão, botões de barra de título sem foco

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | N/D |
| Primeiro plano (glifo) | `Environment.ToolWindowButtonInactiveGlyph` |
| Borda | N/D |

**Botões da barra de título focalizado: estado de foco**

![Botões da barra de título focalizados ao focalizar](../../extensibility/ux-guidelines/media/0303-098_titlebarbuttonfocusedhover.png "0303-098_TitleBarButtonFocusedHover")<br />Botões da barra de título focalizados ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolWindowButtonHoverActive` |
| Primeiro plano (glifo) | `Environment.ToolWindowButtonHoverActiveGlyph` |
| Borda | `Environment.ToolWindowButtonHoverActiveBorder` |

**Botões da barra de título sem foco: estado de foco**

![Botões da barra de título sem foco ao focalizar](../../extensibility/ux-guidelines/media/0303-099_titlebarbuttonunfocusedhover.png "0303-099_TitleBarButtonUnfocusedHover")<br />Botões da barra de título sem foco ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolWindowButtonHoverInactive` |
| Primeiro plano (glifo) | `Environment.ToolWindowButtonHoverInactiveGlyph` |
| Borda | `Environment.ToolWindowButtonHoverInactiveBorder` |

**Botões da barra de título focalizado: estado pressionado**

![Botões da barra de título focalizados ao pressionar](../../extensibility/ux-guidelines/media/0303-100_titlebarbuttonfocusedpressed.png "0303-100_TitleBarButtonFocusedPressed")<br />Botões da barra de título focalizados ao pressionar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolWindowButtonDown` |
| Primeiro plano (glifo) | `Environment.ToolWindowButtonDownActiveGlyph` |
| Borda | `Environment.ToolWindowButtonDownBorder` |

**Botões da barra de título sem foco: estado pressionado**

![Botões da barra de título sem foco ao pressionar](../../extensibility/ux-guidelines/media/0303-101_titlebarbuttonunfocusedpressed.png "0303-101_TitleBarButtonUnfocusedPressed")<br />Botões da barra de título sem foco ao pressionar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolWindowButtonDown` |
| Primeiro plano (glifo) | `Environment.ToolWindowButtonDownInactiveGlyph` |
| Borda | `Environment.ToolWindowButtonDownBorder` |

### <a name="tool-window-tabs"></a>Guias da janela de ferramentas
![Guia da janela de ferramentas (Redline)](../../extensibility/ux-guidelines/media/0303-102_toolwindowtabredline.png "0303-102_ToolWindowTabRedline")<br />Guia da janela de ferramentas (Redline)

| Usar... | Não use... |
| --- | --- |
| ... em qualquer lugar que você esteja criando a interface do usuário que deseja corresponder às janelas de ferramentas. | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema. |

**Guia da janela de ferramentas focalizada selecionada**

![Guia da janela de ferramentas focalizada selecionada](../../extensibility/ux-guidelines/media/0303-103_toolwindowtabfocused.png "0303-103_ToolWindowTabFocused")<br />Guia da janela de ferramentas focalizada selecionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolWindowTabSelectedTab` |
| Primeiro plano (texto) | `Environment.ToolWindowTabSelectedActiveText` |
| Borda | `Environment.ToolWindowTabSelectedBorder`<br />(Defina como a mesma cor como plano de fundo.) |

**Selecionada, guia de janela de ferramentas não focalizada**

![Selecionada, guia de janela de ferramentas não focalizada](../../extensibility/ux-guidelines/media/0303-104_toolwindowtabunfocused.png "0303-104_ToolWindowTabUnfocused")<br />Selecionada, guia de janela de ferramentas não focalizada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolWindowTabSelectedTab` |
| Primeiro plano (texto) | `Environment.ToolWindowTabSelectedText` |
| Borda | `Environment.ToolWindowTabSelectedBorder`<br />(Defina como a mesma cor como plano de fundo.) |

**Guia da janela da ferramenta de segundo plano: estado padrão**

![Guia de janela da ferramenta de segundo plano padrão](../../extensibility/ux-guidelines/media/0303-105_toolwindowbackgroundtab.png "0303-105_ToolWindowBackgroundTab")<br />Guia de janela da ferramenta de segundo plano padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolWindowTabGradientBegin`<br />`Environment.ToolWindowTabGradientEnd`<br />(As interrupções de gradiente são definidas com o mesmo valor de cor em Visual Studio 2013.) |
| Primeiro plano (texto) | `Environment.ToolWindowTabText` |
| Borda | `Environment.ToolWindowTabBorder` |

**Guia da janela da ferramenta de segundo plano: estado de foco**

![Guia da janela da ferramenta de segundo plano ao focalizar](../../extensibility/ux-guidelines/media/0303-106_toolwindowbackgroundtabhover.png "0303-106_ToolWindowBackgroundTabHover")<br />Guia da janela da ferramenta de segundo plano ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.ToolWindowTabMouseOverBackgroundBegin`<br />`Environment.ToolWindowTabMouseOverBackgroundEnd`<br />(As interrupções de gradiente são definidas com o mesmo valor de cor em Visual Studio 2013.) |
| Primeiro plano (texto) | `Environment.ToolWindowTabMouseOverText` |
| Borda | `Environment.ToolWindowTabMouseOverBorder`<br />(Defina como a mesma cor como plano de fundo.) |

### <a name="auto-hide-tabs"></a>Ocultar guias automaticamente

![Ocultar guias automaticamente (Redline)](../../extensibility/ux-guidelines/media/0303-107_autohideredline.png "0303-107_AutoHideRedline") Ocultar guias automaticamente (Redline)

| Usar... | Não use... |
| --- | --- |
| ... em qualquer lugar em que você esteja criando a interface do usuário que deseja corresponder às guias da janela de ferramentas ocultas automaticamente. | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema. |

**Ocultar guias automaticamente: estado padrão**

![Guia ocultar automaticamente padrão](../../extensibility/ux-guidelines/media/0303-108_autohidetab.png "0303-108_AutoHideTab")<br />Guia ocultar automaticamente padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.AutoHideTabBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.AutoHideTabText` |
| Borda | `Environment.AutoHideTabBorder` |

**Ocultar guias automaticamente: estado de foco**

![Ocultar guia automaticamente ao focalizar](../../extensibility/ux-guidelines/media/0303-109_autohidetabhover.png "0303-109_AutoHideTabHover")<br />Ocultar guia automaticamente ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Segundo plano | `Environment.AutoHideTabMouseOverBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.AutoHideTabMouseOverText` |
| Borda | `Environment.AutoHideTabMouseOverBorder` |
