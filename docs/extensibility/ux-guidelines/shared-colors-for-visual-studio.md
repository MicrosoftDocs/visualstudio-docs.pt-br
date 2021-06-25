---
title: Cores compartilhadas para Visual Studio | Microsoft Docs
description: Saiba como usar elementos e temas Visual Studio shell comuns para criar sua própria interface do usuário personalizada consistente com o ambiente Visual Studio aplicativo.
ms.date: 04/26/2017
ms.topic: reference
ms.assetid: 8d11b9a0-6175-4f2e-8e7f-79daee1bfd41
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 262f90fb8d03a9404cdbba8b942e90f6fe6fd3aa
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903964"
---
# <a name="shared-colors-for-visual-studio"></a>Cores compartilhadas para Visual Studio
Quando você estiver projetando uma interface do usuário que usa elementos comuns do shell Visual Studio ou quiser que o elemento de interface seja consistente com recursos semelhantes, use nomes de token existentes em arquivos de definição de pacote para escolher e atribuir cores. Isso garante que sua interface do usuário permaneça consistente com o ambiente de Visual Studio geral e seja atualizada automaticamente quando os temas são adicionados ou atualizados.

Este artigo descreve os elementos comuns da interface do usuário e os nomes de token que eles usam, que você pode referenciar ao criar uma interface do usuário semelhante. Para obter informações específicas sobre como acessar esses tokens de cor, consulte [O serviço VSColor](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService).

Certifique-se de usar nomes de token corretamente:

- **Use nomes de token com base na função, não na cor em si.** As cores compartilhadas comuns são associadas a elementos de interface específicos e devem ser usadas apenas para os mesmos recursos ou semelhantes. Por exemplo, não reutilizar a cor de uma caixa de combinação pressionada para uma animação de progresso de rotação apenas porque você gosta da cor. As funções da caixa de combinação e da animação são diferentes e, se a cor associada à caixa de combinação mudar, ela poderá não ser mais uma cor apropriada para o elemento de animação. O uso consistente de cores ajuda a orientar seus usuários e evitar confusão.

- **Use as cores da plano de fundo e do texto na combinação correta.** As cores da tela de fundo que devem ser usadas com texto terão uma cor de texto associada. Não use cores de texto diferentes do que é especificado para essa plano de fundo. Se não houver uma cor de texto associada, não use essa cor da tela de fundo para nenhuma superfície na qual você espera exibir texto. Outras combinações de cores de texto e de plano de fundo podem resultar em uma interface ilegível.

- **Use cores de controle apropriadas para sua localização.** Em determinados estados, alguns Visual Studio controles não têm cores de borda e plano de fundo separadas. Em vez disso, eles escolhem essas cores das superfícies por trás delas. Certifique-se de sempre usar os nomes de token apropriados para o local em que você está colocando o controle.

> [!IMPORTANT]
> Não use tokens encontrados nas categorias "Página Inicial" ou "Cider".

## <a name="common-shared-controls"></a>Controles compartilhados comuns

Ao usar uma barra de Visual Studio padrão em seu recurso, você terá acesso aos controles de shell estilados. Você não deve re-modelo desses controles comuns. No entanto, se você precisar criar uma barra de comandos personalizada, talvez seja necessário criar controles personalizados também. Nesse caso, use os nomes de token corretos para cada um dos controles a seguir para que sua interface do usuário seja consistente com o restante Visual Studio.

### <a name="button-controls"></a>Controles de botão

![Linha vermelha do controle de botão](../../extensibility/ux-guidelines/media/0303-155_buttoncontrolredline.png "0303-155_ButtonControlRedline")

| Usar... | Não use ... |
| --- | --- |
| ... para botões no documento que você deseja integrar com Visual Studio temas (Claro, Escuro, Azul ou um tema Alto Contraste sistema). | ... para botões que serão exibidos em uma tela de fundo personalizada que não faz parte de um Visual Studio. |

**Botão: estado padrão**

![Botão Padrão](../../extensibility/ux-guidelines/media/03.03.Button.Standard.png "03.03.Button.Standard")<br />Botão Padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Botão | `CommonControls.Button` |
| Borda do botão | `CommonControls.ButtonBorder` |

**Botão: estado padrão**

![Botão Padrão](../../extensibility/ux-guidelines/media/03.03.Button.Default.png "03.03.Button.Default")<br />Botão Padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Botão | `CommonControls.ButtonDefault` |
| Borda do botão | `CommonControls.ButtonBorderDefault` |

**Botão: estado desabilitado**

![Botão Desabilitado](../../extensibility/ux-guidelines/media/03.03.Button.Disabled.png "03.03.Button.Disabled")<br />Botão Desabilitado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Botão | `CommonControls.ButtonDisabled` |
| Borda do botão | `CommonControls.ButtonBorderDisabled` |

**Botão: estado de foco**

![Botão ao passar o mouse](../../extensibility/ux-guidelines/media/03.03.Button.hover.png "03.03.Button.hover")<br />Botão ao passar o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Botão | `CommonControls.ButtonHover` |
| Borda do botão | `CommonControls.ButtonBorderHover` |

**Botão: estado pressionado**

![Botão pressionado](../../extensibility/ux-guidelines/media/03.03.Button.Pressed.png "03.03.Button.Pressed")<br />Botão pressionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Botão | `CommonControls.ButtonPressed` |
| Borda do botão | `CommonControls.ButtonBorderPressed` |

**Botão: estado focalizado**

![Botão focalizado](../../extensibility/ux-guidelines/media/03.03.Button.Focused.png "03.03.Button.Focused")<br />Botão focalizado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Botão | `CommonControls.ButtonFocused` |
| Borda do botão | `CommonControls.ButtonBorderFocused` |

### <a name="check-box-controls"></a>Controles de caixa de seleção
![Caixa de seleção (linha vermelha)](../../extensibility/ux-guidelines/media/0303-161_checkboxredline.png "0303-161_CheckboxRedline")<br />Caixa de seleção (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... para controles de caixa de seleção contidos no documento. | ... para qualquer interface do usuário que não seja um controle de caixa de seleção. |

**Caixa de seleção: estado padrão**

![Caixa de seleção](../../extensibility/ux-guidelines/media/0303-162_checkbox.png "0303-162_Checkbox")<br />Caixa de seleção Padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `CommonControls.CheckBoxBackground` |
| Borda | `CommonControls.CheckBoxBorder` |
| Texto | `CommonControls.CheckBoxText` |
| Glifo | `CommonControls.CheckBoxGlyph` |

**Caixa de seleção: estado desabilitado**

![Caixa de seleção Desabilitada](../../extensibility/ux-guidelines/media/0303-163_checkboxdisabled.png "0303-163_CheckboxDisabled")<br />Caixa de seleção Desabilitada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `CommonControls.CheckBoxBackgroundDisabled` |
| Borda | `CommonControls.CheckBoxBorderDisabled` |
| Texto | `CommonControls.CheckBoxTextDisabled` |
| Glifo | `CommonControls.CheckBoxGlyphDisabled` |

**Caixa de seleção: estado de foco**

 ![Caixa de seleção ao passar o mouse](../../extensibility/ux-guidelines/media/0303-164_checkboxhover.png "0303-164_CheckboxHover")<br />Caixa de seleção ao passar o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `CommonControls.CheckBoxBackgroundHover` |
| Borda | `CommonControls.CheckBoxBorderHover` |
| Texto | `CommonControls.CheckBoxTextHover` |
| Glifo | `CommonControls.CheckBoxGlyphHover` |

**Caixa de seleção: estado pressionado**

![Caixa de seleção pressionada](../../extensibility/ux-guidelines/media/0303-165_checkboxpressed.png "0303-165_CheckboxPressed")<br />Caixa de seleção pressionada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `CommonControls.CheckBoxBackgroundPressed` |
| Borda | `CommonControls.CheckBoxBorderPressed` |
| Texto | `CommonControls.CheckBoxTextPressed` |
| Glifo | `CommonControls.CheckBoxGlyphPressed` |

**Caixa de seleção: estado focalizado**

![Caixa de seleção Focalizada](../../extensibility/ux-guidelines/media/0303-166_checkboxfocused.png "0303-166_CheckboxFocused")<br />Caixa de seleção Focalizada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `CommonControls.CheckBoxBackgroundFocused` |
| Borda | `CommonControls.CheckBoxBorderFocused` |
| Texto | `CommonControls.CheckBoxTextFocused` |
| Glifo | `CommonControls.CheckBoxGlyphFocused` |

### <a name="drop-downs-and-combo-boxes"></a>Listadas e caixas de combinação
![Caixa de combinação/lista listada (linha vermelha)](../../extensibility/ux-guidelines/media/0303-167_dropdowncomboboxredline.png "0303-167_DropDownComboBoxRedline")<br />Caixa de combinação/lista listada (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... para listadas e caixas de combinação na caixa de documento. | ... para qualquer interface do usuário que não seja uma caixa de combinação ou lista de combinação. |
| | ... para as caixas de combinação [ou listadas](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandDropDown) [da barra de comandos](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandComboBox). |

**Listadas e caixas de combinação: estado padrão**

![Caixa de combinação/lista de combinação padrão](../../extensibility/ux-guidelines/media/0303-168_dropdowncombobox.png "0303-168_DropDownComboBox")<br />Caixa de combinação/lista de combinação padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `CommonControls.ComboBoxBackground` |
| Borda | `CommonControls.ComboBoxBorder` |
| Texto | `CommonControls.ComboBoxText` |
| Separador | `CommonControls.ComboBoxSeparator` |
| Glifo | `CommonControls.ComboBoxGlyph` |
| Plano de fundo do glifo | `CommonControls.ComboBoxGlyphBackground` |

**Listadas e caixas de combinação: estado desabilitado**

![Caixa de combinação/lista de combinação desabilitada](../../extensibility/ux-guidelines/media/0303-169_dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")<br />Caixa de combinação/lista de combinação desabilitada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `CommonControls.ComboBoxBackgroundDisabled` |
| Borda | `CommonControls.ComboBoxBorderDisabled` |
| Texto | `CommonControls.ComboBoxTextDisabled` |
| Separador | `CommonControls.ComboBoxSeparatorDisabled` |
| Glifo | `CommonControls.ComboBoxGlyphDisabled` |
| Plano de fundo do glifo | `CommonControls.ComboBoxGlyphBackgroundDisabled` |

**Listadas e caixas de combinação: estado de foco**

![Caixa de combinação/lista listada ao passar o mouse](../../extensibility/ux-guidelines/media/0303-170_dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")<br />Caixa de combinação/lista listada ao passar o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `CommonControls.ComboBoxBackgroundHover` |
| Borda | `CommonControls.ComboBoxBorderHover` |
| Texto | `CommonControls.ComboBoxTextHover` |
| Separador | `CommonControls.ComboBoxSeparatorHover` |
| Glifo | `CommonControls.ComboBoxGlyphHover` |
| Plano de fundo do glifo | `CommonControls.ComboBoxGlyphBackgroundHover` |

**Listadas e caixas de combinação: estado pressionado**

![Caixa de combinação/lista de combinação pressionada](../../extensibility/ux-guidelines/media/0303-171_dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")<br />Caixa de combinação/lista de combinação pressionada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `CommonControls.ComboBoxBackgroundPressed` |
| Borda | `CommonControls.ComboBoxBorderPressed` |
| Texto | `CommonControls.ComboBoxTextPressed` |
| Separador | `CommonControls.ComboBoxSeparatorPressed` |
| Glifo | `CommonControls.ComboBoxGlyphPressed` |
| Plano de fundo do glifo | `CommonControls.ComboBoxGlyphBackgroundPressed` |

**Exibição de item de lista de caixas de combinação e listas de listas de listas: estado pressionado**

 ![Exibição de item de lista pressionada/caixa de combinação pressionada](../../extensibility/ux-guidelines/media/0303-174_dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")<br />Exibição de item de lista pressionada/caixa de combinação pressionada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `CommonControls.ComboBoxListBackground`<br />`CommonControls.ComboBoxListBackgroundHover`<br />`CommonControls.ComboBoxListItemBackgroundPressed`<br />`CommonControls.ComboBoxListItemBackgroundFocused` |
| Borda | `CommonControls.ComboBoxListBorder`<br />`CommonControls.ComboBoxListBorderHover`<br />`CommonControls.ComboBoxListBorderPressed`<br />`CommonControls.ComboBoxListBorderFocused` |
| Texto do item | `CommonControls.ComboBoxListItemText`<br /> `CommonControls.ComboBoxListItemTextHover`<br />`CommonControls.ComboBoxListItemTextPressed`<br />`CommonControls.ComboBoxListItemTextFocused` |
| Sombra de plano de fundo | `CommonControls.ComboBoxListBackgroundShadow` |

**Listadas e caixas de combinação: estado focalizado**

![Caixa de combinação/lista de lista com foco](../../extensibility/ux-guidelines/media/0303-172_dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")<br />Caixa de combinação/lista de lista com foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `CommonControls.ComboBoxBackgroundFocused` |
| Borda | `CommonControls.ComboBoxBorderFocused` |
| Texto | `CommonControls.ComboBoxTextFocused` |
| Separador | `CommonControls.ComboBoxSeparatorFocused` |
| Glifo | `CommonControls.ComboBoxGlyphFocused` |
| Plano de fundo do glifo | `CommonControls.ComboBoxGlyphBackgroundFocused` |

**Listadas e caixas de combinação: seleção de entrada de texto**

![Seleção de entrada de texto da caixa de combinação/lista de opções](../../extensibility/ux-guidelines/media/0303-173_dropdowncomboboxtextinput.png "0303-173_DropDownComboBoxTextInput")<br />Seleção de entrada de texto da caixa de combinação/lista de opções

| Elemento | Nome do token: Category.color |
| --- | --- |
| Realce | `CommonControls.ComboBoxTextInputSelection` |

### <a name="tabular-data-grid-controls"></a>Controles de dados tabular (grade)
Controles de dados tabular, também conhecidos como controles de grade, são controles comuns para Visual Studio que podem ser usados para apresentar grandes quantidades de dados em várias colunas. Os controles de dados tabular padrão podem ser encontrados em vários locais no Visual Studio: a janela da ferramenta Lista de Erros, os relatórios do IntelliTrace e a exibição de heap de memória, entre outros. Sempre use os controles de dados tabular padrão fornecidos. Em algumas instâncias raras, talvez você não tenha acesso aos controles de dados tabular padrão. Nessas situações, use os nomes de token a seguir para garantir que sua interface do usuário seja consistente com outros controles de dados tabular Visual Studio.

![Controle de dados/grade tabular (linha vermelha)](../../extensibility/ux-guidelines/media/0303-197_tabulardatagridcontrolredline.png "0303-197_TabularDataGridControlRedline")<br />Controle de dados/grade tabular (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... para controles tabular ou de grade. | ... para qualquer interface do usuário que não seja um controle tabular ou de grade. |

#### <a name="column-headers"></a>Cabeçalhos da coluna
Os títulos de coluna consistem em uma plano de fundo, uma borda, o texto do título e um glifo opcional geralmente usado quando uma grade é classificação por essa coluna.

**Header de coluna: estado padrão**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Header.Default` |
| Primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Primeiro plano (glifo) | `Header.Glyph` |
| Borda | `Header.SeparatorLine` |

**Header da coluna: estado de foco**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Header.MouseOver` |
| Primeiro plano (texto) | `Environment.CommandBarTextHover` |
| Primeiro plano (glifo) | `Header.MouseOverGlyph` |
| Borda | `Header.SeparatorLine` |

**Header da coluna: estado pressionado**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `CommonControls.CheckBoxBackgroundPressed` |
| Primeiro plano (texto) | `CommonControls.CheckBoxBorderPressed` |
| Primeiro plano (glifo) | `CommonControls.CheckBoxTextPressed` |
| Borda | `CommonControls.CheckBoxGlyphPressed` |

#### <a name="list-view-items"></a>Listar itens de exibição
 Os itens de exibição de lista consistem em um plano de fundo e no conteúdo. O conteúdo pode ser texto, ícone ou ambos.

**Itens de exibição de lista: estado padrão**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | Transparente |
| Primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Borda | Nenhum |

**Itens de exibição de lista: estado ativo**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `TreeView.SelectedItemActive` |
| Primeiro plano (texto) | `TreeView.SelectedItemActiveText` |
| Borda | Nenhum |

**Itens de exibição de lista: estado inativo**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `TreeView.SelectedItemInactive` |
| Primeiro plano (texto) | `TreeView.SelectedItemInactiveText` |
| Borda | Nenhum |

### <a name="ui-text"></a>Texto da interface do usuário

#### <a name="instructional-text"></a>Texto de instrução
O texto de instrução fornece uma explicação principal importante do que fazer em uma página de diálogo ou documento.

![Texto de instrução padrão](../../extensibility/ux-guidelines/media/0303_InstructionalText.png "0303_InstructionalText.png")<br />Texto de instrução padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `Environment.ControlText` |

#### <a name="secondary-instructional-text"></a>Texto de instrução secundário
Em páginas de documento com muitos textos e controles, algum texto de instrução usa um valor de cor diferente. Isso ajuda a transmitir quais informações são mais importantes e diminuir a densidade geral dos elementos da interface do usuário. (Consulte também a seção abaixo sobre o texto da dica.)

![Texto de instrução secundário](../../extensibility/ux-guidelines/media/0303_SecondaryInstructionalText.png "0303_SecondaryInstructionalText.png")<br />Texto de instrução secundário

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `Environment.ControlEditHintText` |

#### <a name="hint-text"></a>Texto da dica
O texto de dica aparece em um controle vazio, abaixo de um controle ou em uma superfície de documento vazia para mostrar ao usuário o que fazer em seguida. Você pode usar texto de dica com janela ou plano de fundo de controle.

**Texto de dica padrão**

![Texto de dica padrão](../../extensibility/ux-guidelines/media/0303_HintText.png "0303_HintText.png")<br />Texto de dica padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `Environment.ControlEditHintText` |

**Texto da dica necessária**

![Texto da dica necessária](../../extensibility/ux-guidelines/media/0303_RequiredHintText.png "0303_RequiredHintText.png")<br />Texto da dica necessária

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `Environment.ControlRequiredHintText` |
| Tela de fundo | `Environment.ControlRequiredBackground` |

**Texto de controle da caixa de pesquisa**

> Confira [Caixas de pesquisa](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_SearchBoxes) para outros tokens de cor relacionados ao controle Pesquisar.

![Texto de controle da caixa de pesquisa](../../extensibility/ux-guidelines/media/0303_SearchBoxControl.png "0303_SearchBoxControl.png")<br />Texto de controle da caixa de pesquisa

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `SearchControl.UnfocusedWatermarkText` |

### <a name="hyperlink"></a>Hyperlink
O hiperlink é um controle que não tem um par de primeiro plano/plano de fundo. Em todos os casos, use a cor do hiperlink em primeiro plano, que aparecerá corretamente em telas de fundo escuras, cinzas e brancas. Se você não usar o token de cor para o controle de hiperlink, verá a cor padrão do sistema para "pressionado", que piscará em vermelho. Esse é o sinal de que o controle não está usando o token de cor do ambiente correto.

![Hiperlink (linha vermelha)](../../extensibility/ux-guidelines/media/0303-133_hyperlinkredline.png "0303-133_HyperlinkRedline")<br />Hiperlink (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... quando você precisa criar um hiperlink personalizado. | ... para qualquer coisa que não seja um hiperlink. |

**Hiperlink: estado padrão**

![Hiperlink padrão](../../extensibility/ux-guidelines/media/0303-134_hyperlink.png "0303-134_Hyperlink")<br />Hiperlink padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `Environment.PanelHyperlink` |

**Hiperlink: estado de foco**

![Hiperlink ao passar o mouse](../../extensibility/ux-guidelines/media/0303-135_hyperlinkhover.png "0303-135_HyperlinkHover")<br />Hiperlink ao passar o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `Environment.PanelHyperlinkHover` |

**Hiperlink: estado pressionado**

![Hiperlink pressionado](../../extensibility/ux-guidelines/media/0303-136_hyperlinkpressed.png "0303-136_HyperlinkPressed")<br />Hiperlink pressionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `Environment.PanelHyperlinkPressed` |

**Hiperlink: estado desabilitado**

![Hiperlink desabilitado](../../extensibility/ux-guidelines/media/0303-137_hyperlinkdisabled.png "0303-137_HyperlinkDisabled")<br />Hiperlink desabilitado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `Environment.PanelHyperlinkDisabled` |

### <a name="infobars"></a>Barras de informações
As barras de informações são usadas para fornecer mais informações sobre um determinado contexto e sempre aparecem na parte superior de uma janela de documento ou janela de ferramentas.

![Barra de informações (linha vermelha)](../../extensibility/ux-guidelines/media/0303-138_infobarredline.png "0303-138_InfobarRedline")<br />Barra de informações (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... ao criar barras de informações personalizadas. | ... para elementos de interface do usuário que não são semelhantes a uma barra de informações. |

**Barra de informações: estado padrão**

![Barra de informações padrão](../../extensibility/ux-guidelines/media/0303-139_infobar.png "0303-139_Infobar")<br />Barra de informações padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `InfoBar.InfoBarBackground` |
| Primeiro plano (texto) | `InfoBar.InfoBar` |
| Borda | `InfoBar.InfoBarBorder` |

**Botão Fechar da barra de informações ( &times; ) : estado padrão**

![Botão Fechar ( ) da barra &times; de informações padrão](../../extensibility/ux-guidelines/media/0303_InfobarCloseDefault.png "0303_InfobarCloseDefault.png")<br />Botão Fechar ( ) da barra &times; de informações padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `InfoBar.CloseButton` |
| Borda | `InfoBar.CloseButtonBorder` |
| Glifo | `InfoBar.CloseButtonGlyph` |

**Botão Fechar da barra de informações ( &times; ) : estado de foco**

![Botão Fechar da barra de informações ( &times; ) ao passar o mouse](../../extensibility/ux-guidelines/media/0303_InfobarCloseHover.png "0303_InfobarCloseHover.png")<br />Botão Fechar da barra de informações ( &times; ) ao passar o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `InfoBar.CloseButtonHover` |
| Borda | `InfoBar.CloseButtonHoverBorder` |
| Glifo | `InfoBar.CloseButtonHoverGlyph` |

**Botão Fechar da &times; barra de informações ( ) : estado pressionado**

![Botão Fechar ( ) da barra &times; de informações pressionada](../../extensibility/ux-guidelines/media/0303_InfobarClosePressed.png "0303_InfobarClosePressed.png")<br />Botão Fechar ( ) da barra &times; de informações pressionada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `InfoBar.CloseButtonDown` |
| Borda | `InfoBar.CloseButtonDownBorder` |
| Glifo | `InfoBar.CloseButtonDownGlyph` |

**Botão de hiperlink da barra de informações: estado padrão**

![Botão de hiperlink da barra de informações padrão](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonDefault.png "0303_InfobarHyperlinkButtonDefault.png")<br />Botão de hiperlink da barra de informações padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `InfoBar.Hyperlink` |

**Botão de hiperlink da barra de informações: estado de foco**

![Botão de hiperlink da barra de informações ao passar o mouse](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonHover.png "0303_InfobarHyperlinkButtonHover.png")<br />Botão de hiperlink da barra de informações ao passar o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `Infobar.HyperlinkMouseOver`<br />(Com sublinhado) |

**Botão de hiperlink da barra de informações: estado pressionado**

![Botão de hiperlink da barra de informações pressionado](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonPressed.png "0303_InfobarHyperlinkButtonPressed.png")<br />Botão de hiperlink da barra de informações pressionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `Infobar.HyperlinkMouseDown`<br />(Com sublinhado) |

**Hiperlink em linha da barra de informações (dentro de uma frase): estado padrão**

![Botão de hiperlink da barra de informações em linha padrão](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonDefault.png "0303_InfobarHyperlinkButtonDefault.png")<br />Botão de hiperlink da barra de informações em linha padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `InfoBar.Hyperlink` |

**Hiperlink em linha da barra de informações (dentro de uma frase): estado de foco**

![Botão de hiperlink em linha da barra de informações ao passar o mouse](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkInlineHover.png "0303_InfobarHyperlinkInlineHover.png")<br />Botão de hiperlink em linha da barra de informações ao passar o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `Infobar.HyperlinkMouseOver`<br />(Com sublinhado) |

**Hiperlink em linha da barra de informações (dentro de uma frase): estado pressionado**

![Botão de hiperlink em linha da barra de informações pressionado](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkInlinePressed.png "0303_InfobarHyperlinkInlinePressed.png")<br />Botão de hiperlink em linha da barra de informações pressionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `Infobar.HyperlinkMouseDown`<br />(Com sublinhado) |

**Botão da barra de informações: estado padrão**

![Botão da barra de informações padrão](../../extensibility/ux-guidelines/media/0303_InfobarButtonDefault.png "0303_InfobarButtonDefault.png")<br />Botão da barra de informações padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `InfoBar.Button` |
| Primeiro plano (texto) | `InfoBar.Button` |
| Borda | `InfoBar.ButtonBorder` |

**Botão da barra de informações: estado de foco**

![Botão da barra de informações ao passar o mouse](../../extensibility/ux-guidelines/media/0303_InfobarButtonHover.png "0303_InfobarButtonHover.png")<br />Botão da barra de informações ao passar o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `InfoBar.ButtonMouseOver` |
| Primeiro plano (texto) | `InfoBar.ButtonMouseOver` |
| Borda | `InfoBar.ButtonMouseOverBorder` |

**Botão da barra de informações: estado pressionado**

![Botão de barra de informações pressionado](../../extensibility/ux-guidelines/media/0303_InfobarButtonPressed.png "0303_InfobarButtonPressed.png")<br />Botão de barra de informações pressionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `InfoBar.ButtonMouseDown` |
| Primeiro plano (texto) | `InfoBar.ButtonMouseDown` |
| Borda | `InfoBar.ButtonMouseDownBorder` |

**Botão da barra de informações: estado desabilitado**

![Botão da barra de informações desabilitado](../../extensibility/ux-guidelines/media/0303_InfobarButtonDisabled.png "0303_InfobarButtonDisabled.png")<br />Botão da barra de informações desabilitado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `InfoBar.ButtonDisabled` |
| Primeiro plano (texto) | `InfoBar.ButtonDisabled` |
| Borda | `InfoBar.ButtonDisabledBorder` |

**Botão da barra de informações: estado focalizado**

![Botão da barra de informações focalizada](../../extensibility/ux-guidelines/media/0303_InfobarButtonFocus.png "0303_InfobarButtonFocus.png")<br />Botão da barra de informações focalizada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `InfoBar.ButtonFocus` |
| Primeiro plano (texto) | `InfoBar.ButtonFocus` |
| Borda | `InfoBar.ButtonFocusBorder` |

### <a name="scroll-bars"></a>Barras de rolagem
As barras de rolagem são estil Visual Studio ambiente e não precisarão ser temas. No entanto, você pode decidir que deseja aproveitar as cores usadas em barras de rolagem para que sua interface do usuário sempre pareça consistente com essa parte do ambiente Visual Studio ambiente.

![Barra de rolagem (linha vermelha)](../../extensibility/ux-guidelines/media/0303-140_scrollbarredline.png "0303-140_ScrollbarRedline")<br />Barra de rolagem (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... ao criar uma interface do usuário que você deseja corresponder Visual Studio de rolagem. | ... para qualquer coisa que você não queira sempre corresponder à interface do usuário da barra de rolagem. |

**Barra de rolagem: estado padrão**

![Barra de rolagem padrão](../../extensibility/ux-guidelines/media/0303-141_scrollbar.png "0303-141_Scrollbar")<br />Barra de rolagem padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Barra de rolagem | `Environment.ScrollBarBackground` |
| Primeiro plano (thumb) | `Environment.ScrollBarThumbBackground` |

**Barra de rolagem: estado de foco**

![Barra de rolagem ao passar o mouse](../../extensibility/ux-guidelines/media/0303-143_scrollbarhover.png "0303-143_ScrollbarHover")<br />Barra de rolagem ao passar o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Barra de rolagem | `Environment.ScrollBarBackground` |
| Primeiro plano (thumb) | `Environment.ScrollBarThumbMouseOverBackground` |

*Barra de rolagem: estado pressionado**

![Barra de rolagem pressionada](../../extensibility/ux-guidelines/media/0303-145_scrollbarpressed.png "0303-145_ScrollbarPressed")<br />Barra de rolagem pressionada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Barra de rolagem | `Environment.ScrollBarBackground` |
| Primeiro plano (thumb) | `Environment.ScrollBarThumbPressedBackground` |

**Seta da barra de rolagem: estado padrão**

![Seta da barra de rolagem padrão](../../extensibility/ux-guidelines/media/0303-142_scrollbararrow.png "0303-142_ScrollbarArrow")<br />Seta da barra de rolagem padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.ScrollBarArrowBackground`<br />(Definido como a mesma cor que a barra de rolagem.) |
| Primeiro plano (glifo) | `Environment.ScrollBarArrowGlyph` |

**Seta da barra de rolagem: estado de foco**

![Seta da barra de rolagem ao focalizar](../../extensibility/ux-guidelines/media/0303-144_scrollbararrowhover.png "0303-144_ScrollbarArrowHover")<br />Seta da barra de rolagem ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ScrollBarArrowMouseOverBackground`<br />(Defina para a mesma cor que a barra de rolagem.) |
| Primeiro plano (glifo) | `Environment.ScrollBarArrowGlyphMouseOver` |

**Seta da barra de rolagem: estado pressionado**

![Seta da barra de rolagem pressionada](../../extensibility/ux-guidelines/media/0303-146_scrollbararrowpressed.png "0303-146_ScrollbarArrowPressed")<br />Seta da barra de rolagem pressionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ScrollBarArrowPressedBackground`<br />(Defina para a mesma cor que a barra de rolagem.) |
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
| Tela de fundo | `SearchControl.FocusedBackground` |
| Primeiro plano (texto) | `SearchControl.FocusedBackground` |
| Borda | `SearchControl.FocusedBorder` |
| Separador | `SearchControl.FocusedDropDownSeparator` |

**Campo de entrada de pesquisa ativo não focalizado**

![Campo de entrada de pesquisa não focalizado](../../extensibility/ux-guidelines/media/0303-114_searchinputfieldunfocused.png "0303-114_SearchInputFieldUnfocused")<br />Campo de entrada de pesquisa ativo não focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `SearchControl.SearchActiveBackground` |
| Primeiro plano (texto) | `SearchControl.SearchActiveBackground` |
| Borda | `SearchControl.UnfocusedBorder` |
| Separador | `SearchControl.DropDownSeparator` |

**Campo de entrada de pesquisa inativo e não focalizado**

![Campo de entrada de pesquisa inativo e não focalizado](../../extensibility/ux-guidelines/media/0303-114-1_searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")<br />Campo de entrada de pesquisa inativo e não focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `SearchControl.Unfocused` |
| Primeiro plano (texto) | `SearchControl.Unfocused` |
| Borda | `SearchControl.UnfocusedBorder` |
| Separador | `SearchControl.DropDownSeparator` |

**Campo de entrada de pesquisa realçado (somente texto)**

![Campo de entrada de pesquisa realçado](../../extensibility/ux-guidelines/media/0303-120_searchinputfieldhighlight.png "0303-120_SearchInputFieldHighlight")<br />Campo de entrada de pesquisa realçado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `SearchControl.Selection` |
| Primeiro plano (texto) | `SearchControl.FocusedBackground` |
| Borda | Nenhum |
| Separador | `SearchControl.FocusedDropDownSeparator` |

**Campo de entrada de pesquisa desabilitado**

![Campo de entrada de pesquisa desabilitado](../../extensibility/ux-guidelines/media/0303-121_searchinputfielddisabled.png "0303-121_SearchInputFieldDisabled")<br />Campo de entrada de pesquisa desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `SearchControl.Disabled` |
| Primeiro plano (texto) | `SearchControl.Disabled` |
| Borda | `SearchControl.DisabledBorder` |
| Separador | `SearchControl.DropDownSeparator` |

**Botão de ação de pesquisa focado**

![Foco no botão de ação de pesquisa](../../extensibility/ux-guidelines/media/0303-112_searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br />Botão de ação de pesquisa focado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | Nenhum |
| Primeiro plano (glifo de pesquisa) | `SearchControl.SearchGlyph` |
| Primeiro plano (glifo de parada) | `SearchControl.StopGlyph` |
| Primeiro plano (limpar glifo) | `SearchControl.ClearGlyph` |
| Borda | N/D |

**Botão de ação de pesquisa não focalizado**

![Botão de ação de pesquisa não focalizado](../../extensibility/ux-guidelines/media/0303-115_searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br />Botão de ação de pesquisa não focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | N/D |
| Primeiro plano (glifo de pesquisa) | `SearchControl.SearchGlyph` |
| Primeiro plano (glifo de parada) | `SearchControl.StopGlyph` |
| Primeiro plano (limpar glifo) | `SearchControl.ClearGlyph` |
| Borda | N/D |

**Botão de ação de pesquisa pressionado**

![Botão de ação de pesquisa pressionado](../../extensibility/ux-guidelines/media/0303-116-1_searchactionbuttonpressed.png "0303-116-1_SearchActionButtonPressed")<br />Botão de ação de pesquisa pressionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `SearchControl.ActionButtonMouseDown` |
| Primeiro plano (glifo) | `SearchControl.ActionButtonMouseDownGlyph` |
| Borda | `SearchControl.ActionButtonMouseDownBorder` |

**Botão de ação de pesquisa desabilitado**

![Botão de ação de pesquisa desabilitado](../../extensibility/ux-guidelines/media/0303-122_searchactionbuttondisabled.png "0303-122_SearchActionButtonDisabled")<br />Botão de ação de pesquisa desabilitado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | Nenhum |
| Primeiro plano (glifo) | `SearchControl.ActionButtonDisabledGlyph` |
| Borda | Nenhum |

**Botão de lista de pesquisa focalizada**

![Botão de lista de pesquisa focalizada](../../extensibility/ux-guidelines/media/0303-113_searchdropdownbuttonfocused.png "0303-113_SearchDropdownButtonFocused")<br />Botão de lista de pesquisa focalizada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `SearchControl.FocusedDropDownButton` |
| Primeiro plano (glifo) | `SearchControl.FocusedDropDownButtonGlyph` |
| Borda | `SearchControl.FocusedDropDownButtonBorder` |

**Botão de lista de pesquisa desfocarada**

![Botão de lista de pesquisa desfocarada](../../extensibility/ux-guidelines/media/0303-116_searchdropdownbuttonunfocused.png "0303-116_SearchDropdownButtonUnfocused")<br />Botão de lista de pesquisa desfocarada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `SearchControl.UnfocusedDropDownButton` |
| Primeiro plano (glifo) | `SearchControl.UnfocusedDropDownButtonGlyph` |
| Borda | `SearchControl.UnfocusedDropDownButtonBorder` |

**Botão de lista de pesquisa pressionado**

![Botão de lista de pesquisa pressionado](../../extensibility/ux-guidelines/media/0303-116-2_searchdropdownbuttonpressed.png "0303-116-2_SearchDropdownButtonPressed")<br />Botão de lista de pesquisa pressionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `SearchControl.MouseDownDropDownButton` |
| Primeiro plano (glifo) | `SearchControl.MouseDownDropDownButtonGlyph` |
| Borda | `SearchControl.MouseDownDropDownButtonBorder` |

**Botão de lista de pesquisa desabilitado**

![Botão de lista de pesquisa desabilitado](../../extensibility/ux-guidelines/media/0303-123_searchdropdownbuttondisabled.png "0303-123_SearchDropdownButtonDisabled")<br />Botão de lista de pesquisa desabilitado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | Nenhum |
| Primeiro plano (glifo) | `SearchControl.DisabledDownButtonGlyph` |
| Borda | Nenhum |

#### <a name="search-drop-down-lists"></a>Pesquisar listas listadas
O menu suspenso da caixa de pesquisa tem o potencial de ser um pouco mais complexo do que outros menus suspensos Visual Studio. As seções "pesquisas sugeridas" e "opções de pesquisa" podem aparecer sozinhas ou juntas no menu, e cada uma delas é colorida separadamente. Uma linha também separa essas duas seções quando elas aparecem juntas e uma borda envolve todo o menu suspenso.

![Lista de listas de pesquisa (linha vermelha)](../../extensibility/ux-guidelines/media/0303-124_searchdropdownredline.png "0303-124_SearchDropdownRedline")<br />Lista de listas de pesquisa (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... quando você estiver criando uma lista de pesquisa personalizada. | ... para listas listadas que aparecem em outros contextos. |
| ... os nomes de token corretos para os componentes de lista corretos. | ... em qualquer combinação de plano de fundo/primeiro plano diferente do especificado. |

**Pesquisar elementos da lista de listas**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Borda | `SearchControl.PopupBorder` |
| Separador | `SearchControl.PopupSectionHeaderSeparator` |
| Shadow | `Environment.DropShadowBackground` |

**Pesquisas sugeridas: estado padrão**

![Pesquisas sugeridas padrão](../../extensibility/ux-guidelines/media/0303-125_searchsuggested.png "0303-125_SearchSuggested")<br />Pesquisas sugeridas padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `SearchControl.PopupItemsListBackgroundGradientBegin`<br />(As paradas de gradiente para esse token não são usadas na interface do usuário com temas.) |
| Primeiro plano (texto) | `SearchControl.PopupItemText` |

**Pesquisas sugeridas: estado de foco**

![Pesquisas sugeridas ao passar o mouse](../../extensibility/ux-guidelines/media/0303-128_searchsuggestedhover.png "0303-128_SearchSuggestedHover")<br />Pesquisas sugeridas ao passar o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br />(As paradas de gradiente para esse token não são usadas na interface do usuário com temas.) |
| Primeiro plano (texto) | `SearchControl.PopupMouseOverItemText` |
| Borda | `SearchControl.PopupControlMouseOverBorder` |

**Opções de pesquisa: estado padrão**

![Caixa de seleção Pesquisar](../../extensibility/ux-guidelines/media/0303-126_searchcheckbox.png "0303-126_SearchCheckbox")<br />Opções de pesquisa padrão (caixa de seleção)

![Opções de pesquisa](../../extensibility/ux-guidelines/media/0303-127_searchoptions.png "0303-127_SearchOptions")<br />Opções de pesquisa padrão (link)

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `SearchControl.PopupSectionBackgroundGradientBegin`<br />(As paradas de gradiente para esse token não são usadas na interface do usuário com temas.) |
| Primeiro plano (texto da caixa de seleção) | `SearchControl.PopupCheckboxText` |
| Primeiro plano (texto do link) | `SearchControl.PopupButtonText` |
| Plano de fundo do header | `SearchControl.PopupSectionHeaderGradientBegin`<br />(As paradas de gradiente para esse token não são usadas na interface do usuário com temas.) |
| Primeiro plano (texto do header) | `SearchControl.PopupSectionHeaderText` |

**Opções de pesquisa: estado de foco**

![Opções de pesquisa (caixa de seleção) ao passar o mouse](../../extensibility/ux-guidelines/media/0303-129_searchcheckboxhover.png "0303-129_SearchCheckboxHover")<br />Opções de pesquisa (caixa de seleção) ao passar o mouse

![Opções de pesquisa (link) ao passar o mouse](../../extensibility/ux-guidelines/media/0303-130_searchoptionshover.png "0303-130_SearchOptionsHover")<br />Opções de pesquisa (link) ao passar o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br />(As paradas de gradiente para esse token não são usadas na interface do usuário com temas.) |
| Primeiro plano (texto da caixa de seleção) | `SearchControl.PopupCheckboxMouseDownText` |
| Primeiro plano (texto do link) | `SearchControl.PopupButtonMouseDownText` |
| Borda | `SearchControl.PopupControlMouseOverBorder` |

**Opções de pesquisa: estado pressionado**

![Opções de pesquisa pressionadas (caixa de seleção)](../../extensibility/ux-guidelines/media/0303-131_searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br />Opções de pesquisa pressionadas (caixa de seleção)

![Opções de pesquisa pressionadas (link)](../../extensibility/ux-guidelines/media/0303-132_searchoptionspressed.png "0303-132_SearchOptionsPressed")<br />Opções de pesquisa pressionadas (link)

| Elemento | Nome do token: Category.color |
| --- | --- |
| Plano de fundo da caixa de seleção | `SearchControl.PopupControlMouseDownBackgroundGradientBegin`<br />`SearchControl.PopupControlMouseDownBackgroundGradientEnd`<br />(As paradas de gradiente para esse token não são usadas na interface do usuário com temas.) |
| Primeiro plano (texto da caixa de seleção) | `SearchControl.PopupCheckboxMouseDownText` |
| Plano de fundo do link | `SearchControl.PopupButtonMouseDownBackgroundGradientBegin`<br />(As paradas de gradiente para esse token não são usadas na interface do usuário com temas.) |
| Primeiro plano (texto do link) | `SearchControl.PopupButtonMouseDownText` |

### <a name="tree-views"></a><a name="BKMK_TreeView"></a> Exibições de árvore
Várias janelas de ferramentas, incluindo Gerenciador de Soluções, Gerenciador de Servidores e Modo de Exibição de Classe, implementam um esquema organizacional hierárquico cujas cores são controladas por nomes de cores na `TreeView` categoria. Todos os itens em um exibição de árvore têm cores de plano de fundo e texto. Itens que têm elementos filho aninhados também têm glifos que indicam se o item é expandido ou recolhido.

![Exibição de árvore (linha vermelha)](../../extensibility/ux-guidelines/media/0303-147_treeviewredline.png "0303-147_TreeViewRedline")<br />Exibição de árvore (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... em qualquer lugar em que você precise implementar uma exibição organizacional hierárquica. | ... para qualquer coisa que não seja semelhante a um modo de exibição de árvore. |
| | ... em qualquer combinação de plano de fundo/primeiro plano diferente do especificado. |

**Item de exibição de árvore: estado padrão**

![Item de exibição de árvore padrão](../../extensibility/ux-guidelines/media/0303-148_treeview.png "0303-148_TreeView")<br />Item de exibição de árvore padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `TreeView.Background` |
| Primeiro plano (texto) | `TreeView.Background` |
| Primeiro plano (glifo) | `TreeView.Glyph` |
| Borda | Nenhum |

**Item de exibição de árvore: estado de foco**

![Item de exibição de árvore ao passar o mouse](../../extensibility/ux-guidelines/media/0303-149_treeviewhover.png "0303-149_TreeViewHover")<br />Item de exibição de árvore ao passar o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `TreeView.Background` |
| Primeiro plano (texto) | `TreeView.Background` |
| Primeiro plano (glifo) | `TreeView.GlyphMouseOver` |
| Borda | Nenhum |

**Item de exibição de árvore: arrastar sobre o estado**

![Item de exibição de árvore ao arrastar sobre](../../extensibility/ux-guidelines/media/0303-150_treeviewdragover.png "0303-150_TreeViewDragOver")<br />Item de exibição de árvore ao arrastar sobre

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `TreeView.DragOverItem` |
| Primeiro plano (texto) | `TreeView.DragOverItem` |
| Primeiro plano (glifo) | `TreeView.DragOverItemGlyph` |
| Borda | Nenhum |

**Item de exibição de árvore: selecionado, estado focalizado**

![Item de exibição de árvore selecionado e focalizado](../../extensibility/ux-guidelines/media/0303-151_treeviewfocused.png "0303-151_TreeViewFocused")<br />Item de exibição de árvore selecionado e focalizado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `TreeView.SelectedItemActive` |
| Primeiro plano (texto) | `TreeView.SelectedItemActive` |
| Primeiro plano (glifo) | `TreeView.SelectedItemActiveGlyph` |
| Borda | `TreeView.FocusVisualBorder` |

**Item de exibição de árvore: estado selecionado e desfoco**

![Item de exibição de árvore selecionado e desfoco](../../extensibility/ux-guidelines/media/0303-152_treeviewunfocused.png "0303-152_TreeViewUnfocused")<br />Item de exibição de árvore selecionado e desfoco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `TreeView.SelectedItemInactive` |
| Primeiro plano (texto) | `TreeView.SelectedItemInactive` |
| Primeiro plano (glifo) | `TreeView.SelectedItemInactiveGlyph` |
| Borda | Nenhum |

**Item de exibição de árvore: focalizado, selecionado e estado focalizado**

![Item de exibição de árvore selecionado e focalizado ao focalizar](../../extensibility/ux-guidelines/media/0303-153_treeviewfocusedhover.png "0303-153_TreeViewFocusedHover")<br />Item de exibição de árvore selecionado e focalizado ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `TreeView.SelectedItemActive` |
| Primeiro plano (texto) | `TreeView.SelectedItemActive` |
| Primeiro plano (glifo) | `TreeView.SelectedItemActiveGlyphMouseOver` |
| Borda | `TreeView.FocusVisualBorder` |

**Item de exibição de árvore: estado com foco, selecionado e desfoco**

![Item de exibição de árvore selecionado e desfoco ao passar o mouse](../../extensibility/ux-guidelines/media/0303-154_treeviewunfocusedhover.png "0303-154_TreeViewUnfocusedHover")<br />Item de exibição de árvore selecionado e desfoco ao passar o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `TreeView.SelectedItemInactive` |
| Primeiro plano (texto) | `TreeView.SelectedItemInactive` |
| Primeiro plano (glifo) | `TreeView.SelectedItemActiveGlyphMouseOver` |
| Borda | Nenhum |

## <a name="shell-appearance"></a>Aparência do Shell

### <a name="background"></a>Tela de fundo
O plano de fundo do ambiente consiste em duas camadas. A camada inferior é uma cor sólida que abrange todo o IDE. A camada superior se encaixa na prateleira do comando e entre os canais de ocultação automática da janela de ferramentas nas bordas esquerda e direita do IDE. As camadas de tela de fundo superior e inferior são definidas com a mesma cor nos temas Claro e Escuro.

![Visual Studio plano de fundo do shell (linha vermelha)](../../extensibility/ux-guidelines/media/0303-187_shellbackgroundredline.png "0303-187_ShellBackgroundRedline")<br />Visual Studio plano de fundo do shell (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... para locais em que você deseja corresponder à parte de fundo do Visual Studio ambiente. | ... como um preenchimento para locais que não são superfícies de plano de fundo. |
| | ... como uma plano de fundo para colocar elementos em primeiro plano. |

**Aparência do shell da camada inferior**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.EnvironmentBackground` |

**Aparência do shell de camada superior**

> As paradas de gradiente são definidas com o mesmo valor de cor Visual Studio 2013 temas Claro e Escuro.

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.EnvironmentBackgroundGradientBegin`<br />`Environment.EnvironmentBackgroundGradientEnd`<br />`Environment.EnvironmentBackgroundGradientMiddle1`<br />`Environment.EnvironmentBackgroundGradientMiddle2` |

### <a name="command-shelf"></a>Prateleira de comando
Dois conjuntos de nomes de token são usados para os bastidores da prateleira de comando: um definido para onde a barra de menus fica e outro para onde as barras de comando ficam. Um grupo de barras de comandos individual tem seus próprios valores de cor da tela de fundo, que são discutidos mais detalhadamente na seção "barra de comandos". O texto da barra de menus e da barra de comandos é discutido nas seções menu e barra de comandos, respectivamente.

![Visual Studio de comando (linha vermelha)](../../extensibility/ux-guidelines/media/0303-188_commandshelfredline.png "0303-188_CommandShelfRedline")<br />Visual Studio de comando (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... para áreas em que você coloca menus ou barras de ferramentas. | ... para áreas que não são semelhantes a uma prateleira de comando. |
|... com a combinação correta de nome de token em segundo plano/plano. | |

**Barra de menus da prateleira comando**

> As paradas de gradiente são definidas com o mesmo valor de cor Visual Studio 2013 temas Claro e Escuro.

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.CommandShelfHighlightGradientBegin`<br /><br />`Environment.CommandShelfHighlightGradientMiddle`<br />`Environment.CommandShelfHighlightGradientEnd` |

**Barra de comandos da estante de comandos**

> As paradas de gradiente são definidas com o mesmo valor de cor Visual Studio 2013 temas Claro e Escuro.

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.CommandShelfBackgroundGradientBegin`<br />`Environment.CommandShelfBackgroundGradientMiddle`<br />`Environment.CommandShelfBackgroundGradientEnd` |

## <a name="manifest-designer"></a>Designer de manifesto
O Designer de Manifesto foi projetado como uma maneira de facilitar a edição do arquivo de manifesto em projetos Windows 8 e Windows Phone 8. Embora não haja nenhuma estrutura compartilhada disponível para consumo, pode ser apropriado corresponder ao layout de design e às cores das guias de orientação/navegação e da estrutura geral. Para obter mais informações sobre detalhes de layout, [consulte Layout para Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md).

![Designer de Manifesto (linha vermelha)](../../extensibility/ux-guidelines/media/0303-175_manifestdesignerredline.png "0303-175_ManifestDesignerRedline")<br />Designer de Manifesto (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... para designers semelhantes ao Designer de Manifesto. | ... se você tiver mais de seis guias. |
| ... em vez de usar controles de tabulação comuns na parte superior de um editor dentro do documento. | ... para qualquer interface do usuário que não seja estruturada como o Designer de Manifesto. |

**Guia selecionada do Designer de Manifesto: estado padrão**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `ManifestDesigner.TabActive` |
| Borda | Nenhum |

**Painel de descrição selecionado do Designer de Manifesto: estado padrão**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `ManifestDesigner.DescriptionPane` |

**Página de conteúdo selecionada do Designer de Manifesto: estado padrão**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `ManifestDesigner.Background` |
| Texto auxiliar da caixa de diálogo | `ManifestDesigner.WatermarkText`<br />(Esse nome de token não combina com sua função.) |

**Guia Designer de Manifesto: estado não selecionado**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `ManifestDesigner.Tab.Inactive` |

**Guia Designer de Manifesto: estado de foco**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `ManifestDesigner.Tab.Mouseover` |

## <a name="command-structures"></a>Estruturas de comando

### <a name="menus"></a><a name="BKMK_CommandMenus"></a> Menus
Os menus podem ocorrer em vários locais no Visual Studio: a barra de menus principal, inserida nas janelas de documentos ou ferramentas ou ao clicar com o botão direito do mouse em vários locais em todo o IDE. Implementações de menus associados a outros elementos da interface do usuário são discutidas na seção para o respectivo elemento. Você sempre deve usar a implementação de menu padrão fornecida pelo Visual Studio ambiente. No entanto, em algumas instâncias raras, talvez você não tenha acesso aos menus Visual Studio padrão. Nessas situações, use os nomes de token a seguir para garantir que sua interface do usuário seja consistente com outros menus Visual Studio.

![Visual Studio menu (linha vermelha)](../../extensibility/ux-guidelines/media/0303-000_menuredline.png "0303-000_MenuRedline")<br />Visual Studio menu (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... quando você precisa criar um menu personalizado.| ... a cor da tela de fundo sozinha. Sempre use a combinação de plano de fundo/primeiro plano, conforme especificado. |
| ... quando você tiver um novo componente de interface do usuário que deseja corresponder aos Visual Studio menus.| |

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
| Tela de fundo | Nenhum |
| Primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Primeiro plano (glifo) | `Environment.CommandBarMenuGlyph` |
| Borda | Nenhum |

**Título do menu: estado de foco**

![Título do menu ao focalizar](../../extensibility/ux-guidelines/media/0303-004_menutitlehover.png "0303-004_MenuTitleHover")<br />Título do menu ao focalizar

![Título do menu com glifo ao focalizar](../../extensibility/ux-guidelines/media/0303-005_menutitlewithglyphhover.png "0303-005_MenuTitleWithGlyphHover")<br />Título do menu com glifo ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.CommandBarMouseOverBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.CommandBarTextHover` |
| Primeiro plano (glifo) | `Environment.CommandBarMenuMouseOverGlyph` |
| Borda | `Environment.CommandBarBorder` |

**Título do menu: estado pressionado**

![Título do menu pressionado](../../extensibility/ux-guidelines/media/0303-006_menutitlepressed.png "0303-006_MenuTitlePressed")<br />Título do menu pressionado

![Título do menu pressionado com glifo](../../extensibility/ux-guidelines/media/0303-007_menutitlewithglyphpressed.png "0303-007_MenuTitleWithGlyphPressed")<br />Título do menu pressionado com glifo

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.CommandBarMenuBackgroundGradientBegin`<br/>(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Primeiro plano (glifo) | `Environment.CommandBarMenuMouseDownGlyph` |
| Borda | `Environment.CommandBarMenuBorder`<br />(Somente laterais esquerda, superior e direita.) |

**Título do menu: estado desabilitado**

![Título do menu desabilitado com glifo](../../extensibility/ux-guidelines/media/0303-008_menutitlewithglyphdisabled.png "0303-008_MenuTitleWithGlyphDisabled")<br />Título do menu desabilitado com glifo

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | Nenhum |
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
| Tela de fundo | `Environment.CommandBarMenuBackgroundGradientBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
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
| Tela de fundo | `Environment.CommandBarMenuItemMouseOver` |
| Primeiro plano (texto) | `Environment.CommandBarMenuItemMouseOverText` |
| Primeiro plano (glifo de submenu) | `Environment.CommandBarMenuMouseOverSubmenuGlyph` |
| Marca de seleção | `Environment.CommandBarCheckBoxMouseOver` |
| Plano de fundo da marca de seleção | `Environment.CommandBarHoverOverSelectedIcon` |
| Plano de fundo do ícone | `Environment.CommandBarHoverOverSelected` |
| Borda do ícone | `Environment.CommandBarHoverOverSelectedIconBorder` |

**Itens de menu: estado desabilitado**

![Menu desabilitado](../../extensibility/ux-guidelines/media/0303-016_menudisabled.png "0303-016_MenuDisabled")<br />Item de menu desabilitado

![Menu desabilitado marcado](../../extensibility/ux-guidelines/media/0303-017_menudisabledchecked.png "0303-017_MenuDisabledChecked")<br />Item de menu desabilitado com marca de seleção

| Elemento | Nome do token: Category.color |
| --- | --- |
| Primeiro plano (texto) | `Environment.CommandBarTextInactive` |
| Primeiro plano (glifo de submenu) | `Environment.CommandBarMenuSubmenuGlyph` |
| Marca de seleção | `Environment.CommandBarCheckBoxDisabled` |
| Plano de fundo da marca de seleção | `Environment.CommandBarSelectedIconDisabled` |

### <a name="command-bars"></a>Barras de comando
Uma barra de comandos pode aparecer em vários locais no Visual Studio IDE, mais notavelmente na prateleira do comando e inserida nas janelas de ferramentas ou documentos.

Em geral, sempre use a implementação da barra de comandos padrão fornecida pelo Visual Studio ambiente. O uso do mecanismo padrão garante que todos os detalhes visuais apareçam corretamente e que os elementos interativos se comportem consistentemente com outros controles Visual Studio barra de comandos. No entanto, se for necessário criar sua própria barra de comandos, certifique-se de estilizar corretamente usando os nomes de token a seguir.

![Linha vermelha da barra de comandos](../../extensibility/ux-guidelines/media/0303-018_commandbarredline.png "0303-018_CommandBarRedline")<br />Barra de comandos (linha vermelha)

![Linha vermelha do botão estouro](../../extensibility/ux-guidelines/media/0303-019_overflowbuttonredline.png "0303-019_OverflowButtonRedline")<br />Botão Estouro (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... em locais em que você precisa de uma barra de comandos inserida, mas não pode usar a implementação da Visual Studio da barra de comandos padrão. | ... para elementos de interface do usuário que não são semelhantes a uma barra de comandos. |
| | ... para componentes de barra de comandos que não sejam aqueles para os quais os nomes de token são especificados. |

#### <a name="command-bar-groups"></a>Grupos de barras de comando
Um grupo de barras de comandos consiste em um conjunto relacionado de controles de barra de comandos e pode conter qualquer número de botões, botões divididos, menus suspensos, caixas de combinação ou menus. As cores desses controles são regulamentadas por nomes de token separados e são discutidas individualmente em outro lugar neste guia. Uma linha de separador é usada para dividir um grupo de barras de comando em subgrupos relacionados.

![Linha vermelha do grupo de barras de comando](../../extensibility/ux-guidelines/media/0303-020_commandbargroupredline.png "0303-020_CommandBarGroupRedline")<br />Grupo de barras de comandos (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... em locais em que você precisa de uma barra de comandos inserida, mas não pode usar a implementação da Visual Studio da barra de comandos padrão. | ... para elementos de interface do usuário que não são semelhantes a uma barra de comandos. |
| | ... para componentes de barra de comandos que não sejam aqueles para os quais os nomes de token são especificados. |

**Grupo de barras de comando: estado padrão**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.CommandBarGradientBegin`<br />(As paradas de gradiente para esse token não são usadas na interface do usuário com temas.) |
| Borda | `Environment.CommandBarToolBarBorder` |
| Identificador de arrastar | `Environment.CommandBarDragHandle` |
| Separador | `Environment.CommandBarToolBarSeparator`<br />`Environment.CommandBarToolBarSeparatorHighlight` |

#### <a name="command-icons"></a>Ícones de comando
![Ícone de comando em linha vermelha](../../extensibility/ux-guidelines/media/0303-021_commandiconredline1.png "0303-021_CommandIconRedline1")<br />Ícone de comando (linha vermelha)

![Ícone de comando com linha vermelha de texto](../../extensibility/ux-guidelines/media/0303-022_commandiconredline2.png "0303-022_CommandIconRedline2")<br />Ícone de comando com texto (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... para todos os botões que serão colocados em uma barra de comandos. | ... para controles que têm seus próprios nomes de token. |
| | ... em qualquer combinação de plano de fundo/primeiro plano diferente do especificado. |

**Ícone de comando: estado padrão**

![Padrão do ícone de comando](../../extensibility/ux-guidelines/media/0303-023_commandicondefault.png "0303-023_CommandIconDefault")<br />Ícone de comando padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | N/A (herda do plano de fundo da barra de comandos) |
| Primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Borda | N/D |

**Ícone de comando: estado padrão, selecionado**

![Ícone de comando padrão selecionado](../../extensibility/ux-guidelines/media/0303-024_commandicondefaultselected.png "0303-024_CommandIconDefaultSelected")<br />Ícone de comando padrão selecionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.CommandBarSelected` |
| Primeiro plano (texto) | `Environment.CommandBarTextSelected` |
| Borda | `Environment.CommandBarSelectedBorder` |

**Ícone de comando: focalizar ou focalizar estados**

![Ícone de comando ao focalizar ou focalizar](../../extensibility/ux-guidelines/media/0303-025_commandiconhover.png "0303-025_CommandIconHover")<br />Ícone de comando ao focalizar ou focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.CommandBarMouseOverBackgroundBegin`<br />(As paradas de gradiente para esse token não são usadas na interface do usuário com temas.) |
| Primeiro plano (texto) | `Environment.CommandBarTextHover` |
| Borda | `Environment.CommandBarBorder` |

**Ícone de comando: focalizar ou focalizar estados, selecionado**

![Ícone de comando selecionado ao focalizar ou focalizar](../../extensibility/ux-guidelines/media/0303-026_commandiconhoverselected.png "0303-026_CommandIconHoverSelected")<br />Ícone de comando selecionado ao focalizar ou focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.CommandBarHoverOverSelected` |
| Primeiro plano (texto) | `Environment.CommandBarTextHoverOverSelected` |
| Borda | `Environment.CommandBarHoverOverSelectedIconBorder` |

 **Ícone de comando: estado pressionado**

![Ícone de comando pressionado](../../extensibility/ux-guidelines/media/0303-027_commandiconpressed.png "0303-027_CommandIconPressed")<br />Ícone de comando pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.CommandBarMouseDownBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.CommandBarTextMouseDown` |
| Borda | `Environment.CommandBarBorder` |

**Ícone de comando: estado desabilitado**

![Ícone de comando desabilitado](../../extensibility/ux-guidelines/media/0303-028_commandicondisabled.png "0303-028_CommandIconDisabled")<br />Ícone de comando desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | N/A (herda do plano de fundo da barra de comandos) |
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
| Tela de fundo | `Environment.ComboBoxBackground` |
| Primeiro plano (texto) | `Environment.ComboBoxText` |
| Borda | `Environment.ComboBoxBorder` |
| Separador | Sem separador |

**Botão suspenso da barra de comandos: estado padrão**

![Botão de remoção de&#45;caixa de combinação](../../extensibility/ux-guidelines/media/0303-031_comboboxdropdownbutton.png "0303-031_ComboBoxDropdownButton")<br />Botão suspenso da barra de comandos

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | N/A (herda do plano de fundo da barra de comandos) |
| Primeiro plano (glifo) | `Environment.ComboBoxGlyph` |

**Lista suspensa da barra de comandos: estado padrão**

![Lista suspensa da barra de comandos](../../extensibility/ux-guidelines/media/0303-032_comboboxdropdownlist.png "0303-032_ComboBoxDropdownList")<br />Lista suspensa da barra de comandos

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ComboBoxPopupBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.ComboBoxItemText` |
| Borda | `Environment.ComboBoxPopupBorder` |

**Campo de entrada da caixa de combinação da barra de comandos: estado de foco**

![Campo de entrada da caixa de combinação da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-033_comboboxinputfieldhover.png "0303-033_ComboBoxInputFieldHover")<br />Campo de entrada da caixa de combinação da barra de comandos ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ComboBoxMouseOverBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.ComboBoxMouseOverText` |
| Borda | `Environment.ComboBoxMouseOverBorder` |
| Separador | `Environment.ComboBoxMouseOverSeparator` |

 **Botão suspenso da barra de comandos: estado de foco**

![Botão suspenso da caixa de combinação da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-034_comboboxdropdownbuttonhover.png "0303-034_ComboBoxDropdownButtonHover")<br />Botão suspenso da barra de comandos ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ComboBoxButtonMouseOverBackground` |
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
| Tela de fundo | `Environment.ComboBoxFocusedBackground` |
| Primeiro plano (texto) | `Environment.ComboBoxFocusedText` |
| Borda | `Environment.ComboBoxFocusedBorder` |
| Separador | `Environment.ComboBoxFocusedButtonSeparator` |

**Botão suspenso da barra de comandos: estado focalizado**

![Botão suspenso de barra de comandos focado](../../extensibility/ux-guidelines/media/0303-037_comboboxdropdownbuttonfocused.png "0303-037_ComboBoxDropdownButtonFocused")<br />Botão suspenso de barra de comandos focado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ComboBoxFocusedButtonBackground` |
| Primeiro plano (glifo) | `Environment.ComboBoxFocusedGlyph` |

 **Campo de entrada da caixa de combinação da barra de comandos: estado pressionado**

![Campo de entrada da caixa de combinação da barra de comandos pressionada](../../extensibility/ux-guidelines/media/0303-038_comboboxinputfieldpressed.png "0303-038_ComboBoxInputFieldPressed")<br />Campo de entrada da caixa de combinação da barra de comandos pressionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ComboBoxMouseDownBackground` |
| Primeiro plano (texto) | `Environment.ComboBoxMouseDownText` |
| Borda | `Environment.ComboBoxMouseDownBorder` |
| Separador | `Environment.ComboBoxMouseDownSeparator` |

**Botão suspenso da barra de comandos: estado pressionado**

![Botão suspenso da caixa de combinação da barra de comandos pressionada](../../extensibility/ux-guidelines/media/0303-039_comboboxdropdownbuttonpressed.png "0303-039_ComboBoxDropdownButtonPressed")<br />Botão suspenso da barra de comandos pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ComboBoxButtonMouseDownBackground` |
| Primeiro plano (glifo) | `Environment.ComboBoxMouseDownGlyph` |

**Campo de entrada da caixa de combinação da barra de comandos: estado desabilitado**

![Campo de entrada da caixa de combinação desabilitada da barra de comandos](../../extensibility/ux-guidelines/media/0303-041_comboboxinputfielddisabled.png "0303-041_ComboBoxInputFieldDisabled")<br />Campo de entrada da caixa de combinação desabilitada da barra de comandos

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ComboBoxDisabledBackground` |
| Primeiro plano (texto) | `Environment.ComboBoxDisabledText` |
| Borda | `Environment.ComboBoxDisabledBorder` |
| Separador | Sem separador |

**Botão suspenso da barra de comandos: estado desabilitado**

![Botão suspenso da caixa de combinação da barra de comandos desabilitada](../../extensibility/ux-guidelines/media/0303-040_comboboxdropdownbuttondisabled.png "0303-040_ComboBoxDropdownButtonDisabled")<br />Botão suspenso da barra de comandos desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | Nenhum |
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
| Tela de fundo | `Environment.DropDownBackground` |
| Primeiro plano (texto) | `DropDownText` |
| Borda | `DropDownBorder` |
| Separador | Sem separador |

**Botão suspenso da barra de comandos: estado padrão**

![Botão suspenso da barra de comandos padrão](../../extensibility/ux-guidelines/media/0303-044_dropdownbutton.png "0303-044_DropdownButton")<br />Botão suspenso da barra de comandos padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | Nenhum |
| Primeiro plano (glifo) | `Environment.DropDownGlyph` |

**Lista suspensa da barra de comandos: estado padrão**

![Lista suspensa da barra de comandos padrão](../../extensibility/ux-guidelines/media/0303-045_dropdownlist.png "0303-045_DropdownList")<br />Lista suspensa da barra de comandos padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.DropDownPopupBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.ComboBoxItemText` |
| Borda | `Environment.DropDownPopupBorder` |
| Shadow | `Environment.DropShadowBackground` |

**Campo de seleção suspensa da barra de comandos: estado de foco**

![Campo de seleção suspensa da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-046_dropdownselectionfieldhover.png "0303-046_DropdownSelectionFieldHover")<br />Campo de seleção suspensa da barra de comandos ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.DropDownMouseOverBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.DropDownMouseOverText` |
| Borda | `Environment.DropDownMouseOverBorder` |
| Separador | `Environment.DropDownButtonMouseOverSeparator` |

**Botão suspenso da barra de comandos: estado de foco**

![Botão suspenso da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-047_dropdownbuttonhover.png "0303-047_DropdownButtonHover")<br />Botão suspenso da barra de comandos ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.DropDownButtonMouseOverBackground` |
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
| Tela de fundo | `Environment.DropDownMouseDownBackground` |
| Primeiro plano (texto) | `Environment.DropDownMouseDownText` |
| Borda | `Environment.DropDownMouseDownBorder` |
| Separador | `Environment.DropDownButtonMouseDownSeparator` |

**Botão suspenso da barra de comandos: estado pressionado**

![Botão suspenso da barra de comandos pressionado](../../extensibility/ux-guidelines/media/0303-050_dropdownbuttonpressed.png "0303-050_DropdownButtonPressed")<br />Botão suspenso da barra de comandos pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.DropDownButtonMouseDownBackground` |
| Primeiro plano (glifo) | `Environment.DropDownMouseDownGlyph` |

**Campo de seleção suspensa da barra de comandos: estado desabilitado**

![Campo de seleção suspensa da barra de comandos desabilitada](../../extensibility/ux-guidelines/media/0303-051_dropdownselectionfielddisabled.png "0303-051_DropdownSelectionFieldDisabled")<br />Campo de seleção suspensa da barra de comandos desabilitada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.DropDownDisabledBackground` |
| Primeiro plano (texto) | `Environment.DropDownDisabledText` |
| Borda | `Environment.DropDownDisabledBorder` |
| Separador | Sem separador |

**Botão suspenso da barra de comandos: estado desabilitado**

![Botão suspenso da barra de comandos desabilitado](../../extensibility/ux-guidelines/media/0303-052_dropdownbuttondisabled.png "0303-052_DropdownButtonDisabled")<br />Botão suspenso da barra de comandos desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | N/D |
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
| Tela de fundo | Nenhum |
| Primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Primeiro plano (glifo) | `Environment.CommandBarSplitButtonGlyph` |
| Borda | N/D |
| Separador | N/D |

**Botão de divisão da barra de comandos: estado de foco**

![Botão de divisão da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-055_splitbuttonhover.png "0303-055_SplitButtonHover")<br />Botão de divisão da barra de comandos ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.CommandBarMouseOverBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.CommandBarTextHover` |
| Primeiro plano (glifo) | `Environment.CommandBarSplitButtonMouseOverGlyph` |
| Borda | `Environment.CommandBarBorder` |
| Separador | `Environment.CommandBarSplitButtonSeparator` |

**Botão de divisão da barra de comandos: estado pressionado**

![Botão de divisão da barra de comandos pressionado](../../extensibility/ux-guidelines/media/0303-056_splitbuttonpressed.png "0303-056_SplitButtonPressed")<br />Botão de divisão da barra de comandos pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.CommandBarMouseDownBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.CommandBarTextMouseDown` |
| Primeiro plano (glifo) | `Environment.CommandBarSplitButtonMouseDownGlyph` |
| Borda | `Environment.CommandBarBorder` |
| Separador | N/D |

**Botão de divisão da barra de comandos: estado desabilitado**

![Botão de divisão da barra de comandos desabilitado](../../extensibility/ux-guidelines/media/0303-057_splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br />Botão de divisão da barra de comandos desabilitado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | N/D |
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
| Tela de fundo | `Environment.CommandBarOptionsBackground` |
| Primeiro plano (glifo) | `Environment.CommandBarOptionsGlyph` |

**Botões ' mais opções ' e ' estouro ' da barra de comandos: estado de foco**

![Botão ' mais opções ' da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-061_moreoptionshover.png "0303-061_MoreOptionsHover")<br />Botão ' mais opções ' da barra de comandos ao focalizar

![Botão "estouro" da barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-062_overflowoptions.png "0303-062_OverflowOptions")<br />Botão "estouro" da barra de comandos ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.CommandBarOptionsMouseOverBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (glifo) | `Environment.CommandBarOptionsMouseDownGlyph` |

**Botões ' mais opções ' e ' estouro ' da barra de comandos: estado pressionado**

![Botão ' mais opções ' da barra de comandos pressionado](../../extensibility/ux-guidelines/media/0303-063_moreoptionspressed.png "0303-063_MoreOptionsPressed")<br />Botão ' mais opções ' da barra de comandos pressionado

![Estouro pressionado](../../extensibility/ux-guidelines/media/0303-064_overflowpressed.png "0303-064_OverflowPressed")<br />Botão ' estouro ' da barra de comandos pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.CommandBarOptionsMouseDownBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
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
| Tela de fundo | Depende do tipo de documento |
| Primeiro plano (texto) | Depende do tipo de documento |
| Borda | `Environment.ToolWindowBorder` |

**Quadro de janela de documento flutuante focalizado: estado padrão**

![Quadro de janela de documento flutuante com foco padrão](../../extensibility/ux-guidelines/media/0303-067_framefocused.png "0303-067_FrameFocused")<br />Quadro de janela de documento flutuante com foco padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ToolWindowFloatingFrame` |
| Primeiro plano (texto) | `Environment.ToolWindowFloatingFrame` |
| Primeiro plano (glifo) | `Environment.RaftedWindowButtonActiveGlyph` |
| Borda | `Environment.MainWindowActiveDefaultBorder` |
| Borda (glifo) | `Environment.RaftedWindowButtonActiveBorder`<br />(Definido como transparente) |

**Quadro de janela de documento flutuante sem foco: estado padrão**

![Quadro de janela de documento flutuante padrão sem foco](../../extensibility/ux-guidelines/media/0303-068_frameunfocused.png "0303-068_FrameUnfocused")<br />Quadro de janela de documento flutuante padrão sem foco

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ToolWindowFloatingFrameInactive` |
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
As guias de documento ficam no canal de guia para indicar quais documentos estão abertos no momento, juntamente com qual deles é o documento atual selecionado ou ativo. As janelas de ferramentas também podem ser encaixadas no canal da guia do documento se o usuário as colocar lá. Nessa situação, eles usam as mesmas cores de guia que as janelas de documentos. Se você estiver criando uma interface do usuário que deseja sempre corresponder às cores da janela do documento (incluindo atualizações de tema ou se novos temas estão instalados), então, consulte esses tokens de cor.

![Guias do documento (linha vermelha)](../../extensibility/ux-guidelines/media/0303-072_documenttabredline.png "0303-072_DocumentTabRedline")<br />Guias do documento (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... em qualquer lugar em que você esteja criando uma interface do usuário que você deseja corresponder às guias de documento e escolha automaticamente as atualizações de tema ou as novas cores do tema. | ... para qualquer interface do usuário que você não deseja alterar automaticamente quando o shell tem uma atualização de tema. |

#### <a name="open-document-tabs"></a>Abrir guias de documento
Cada documento aberto tem uma guia no canal de guia do documento que exibe seu nome. Os documentos podem ser selecionados ou abertos em segundo plano e suas guias refletem estes estados:

- A guia selecionada representa o documento exibido no momento na área do documento. Uma guia selecionada tem uma borda de documento que se estende pela borda superior do documento.

- As guias em segundo plano são todas as guias de documento que não são a guia selecionada no momento. Depois de clicados, eles se tornam a guia selecionada e adquirem todas as cores de plano de fundo, borda e texto desses nomes de token.

![Abrir a guia documento (linha vermelha)](../../extensibility/ux-guidelines/media/0303-073_opendocumenttabredline.png "0303-073_OpenDocumentTabRedline")<br />Abrir a guia documento (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... ao criar guias de documento personalizadas. | ... para guias provisórios (versão prévia). |
| | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tiver uma atualização de tema. |

**Guia de documento selecionada e focada**

![Guia de documento selecionada e focada](../../extensibility/ux-guidelines/media/0303-074_selectedtabfocused.png "0303-074_SelectedTabFocused")<br />Guia de documento selecionada e focada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.FileTabSelectedGradientTop`<br />(As paradas de gradiente para esse token não são usadas na interface do usuário com temas.) |
| Primeiro plano (texto) | `Environment.FileTabSelectedText` |
| Borda | `Environment.FileTabSelectedBorder`<br />(Definido como a mesma cor da tela de fundo.) |
| Borda do documento | `Environment.FileTabDocumentBorderBackground` |

**Guia do documento selecionado e desfoco**

![Guia do documento selecionado e desfoco](../../extensibility/ux-guidelines/media/0303-075_selectedtabunfocused.png "0303-075_SelectedTabUnfocused")<br />Guia do documento selecionado e desfoco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.FileTabInactiveGradientTop`<br />(As paradas de gradiente para esse token não são usadas na interface do usuário com temas.) |
| Primeiro plano (texto) | `Environment.FileTabInactiveText` |
| Borda | `Environment.FileTabInactiveBorder`<br />(Definido como a mesma cor da tela de fundo.) |
| Borda do documento | `Environment.FileTabInactiveDocumentBorderBackground` |

**Guia Documento em segundo plano: estado padrão**

![Guia documento em segundo plano padrão](../../extensibility/ux-guidelines/media/0303-076_backgroundtab.png "0303-076_BackgroundTab")<br />Guia documento em segundo plano padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.FileTabBackground` |
| Primeiro plano (texto) | `Environment.FileTabText` |
| Borda | `Environment.FileTabBorder`<br />(Definido como a mesma cor da tela de fundo.) |

**Guia documento em segundo plano: estado de foco**

![Guia documento em segundo plano ao passar o mouse](../../extensibility/ux-guidelines/media/0303-077_backgroundtabhover.png "0303-077_BackgroundTabHover")<br />Guia documento em segundo plano ao passar o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.FileTabHotGradientTop`<br />(As paradas de gradiente para esse token não são usadas na interface do usuário com temas.) |
| Primeiro plano (texto) | `Environment.FileTabHotText` |
| Borda | `Environment.FileTabHotBorder`<br />(Definido como a mesma cor da tela de fundo.) |

#### <a name="preview-tab"></a>Guia Visualização
Também chamada de guia "provisório". A guia visualização aparece no lado direito do canal da guia do documento quando o usuário clica em um item na janela Gerenciador de Soluções ferramenta. Ele atua como uma visualização do documento e também oferece ao usuário a opção de manter o documento aberto no lado esquerdo do canal de guia do documento. Somente uma guia de visualização aberta pode ser aberta por vez. As guias de visualização têm estados selecionados e em segundo plano, como guias abertas, e podem ser focadas ou desfocados em seu estado ativo.

![Guia Visualização (linha vermelha)](../../extensibility/ux-guidelines/media/0303-078_previewtabredline.png "0303-078_PreviewTabRedline")<br />Guia Visualização (linha vermelha)

| Usar... | Não use ... |
| --- | --- |
| ... em qualquer lugar em que você esteja criando uma versão prévia e queira que algum elemento seja igual à cor da guia de visualização atual. | ... para qualquer tipo de documento ou guia que não seja provisório (versão prévia). |
| | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tiver uma atualização de tema. |

**Guia De visualização focalizada e selecionada**

![Guia De visualização focalizada e selecionada](../../extensibility/ux-guidelines/media/0303-079_previewtabfocused.png "0303-079_PreviewTabFocused")<br />Guia De visualização focalizada e selecionada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.FileTabProvisionalSelectedActive` |
| Primeiro plano (texto) | `Environment.FileTabProvisionalSelectedActiveForeground` |
| Borda | `Environment.FileTabProvisionalSelectedActiveBorder`<br />(Definido como a mesma cor da tela de fundo.) |
| Borda do documento | `Environment.FileTabProvisionalSelectedActiveBorder` |

**Guia de visualização não desfocarada e selecionada**

![Guia de visualização não desfocarada e selecionada](../../extensibility/ux-guidelines/media/0303-080_previewtabunfocused.png "0303-080_PreviewTabUnfocused")<br />Guia de visualização não desfocarada e selecionada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.FileTabProvisionalSelectedInactive` |
| Primeiro plano (texto) | `Environment.FileTabProvisionalSelectedInactiveForeground` |
| Borda | `Environment.FileTabProvisionalSelectedInactiveBorder` |
| Borda do documento | `Environment.FileTabProvisionalSelectedInactiveBorder` |

**Guia Visualização em segundo plano: estado padrão**

![Guia de visualização em segundo plano padrão](../../extensibility/ux-guidelines/media/0303-081_previewbackgroundtab.png "0303-081_PreviewBackgroundTab")<br />Guia de visualização em segundo plano padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Tela de fundo | `Environment.FileTabProvisionalInactive` |
| Primeiro plano (texto) | `Environment.FileTabProvisionalInactiveForeground` |
| Borda | `Environment.FileTabProvisionalInactiveBorder`<br />(Defina como a mesma cor como plano de fundo.) |

**Guia de visualização em segundo plano: estado de foco**

![Guia de visualização em segundo plano ao focalizar](../../extensibility/ux-guidelines/media/0303-082_previewbackgroundtabhover.png "0303-082_PreviewBackgroundTabHover")<br />Guia de visualização em segundo plano ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.FileTabProvisionalHover` |
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
| Tela de fundo | `Environment.DocWellOverflowButtonBackground` |
| Primeiro plano (glifo) | `Environment.DocWellOverflowButtonGlyph` |
| Borda | N/D |

**Botão de estouro de documento: estado de foco**

![Botão de estouro de documento ao focalizar](../../extensibility/ux-guidelines/media/0303-085_overflowhover.png "0303-085_OverflowHover")<br />Botão de estouro de documento ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.DocWellOverflowButtonMouseOverBackground` |
| Primeiro plano (glifo) | `Environment.DocWellOverflowButtonMouseOverGlyph` |
| Borda | `Environment.DocWellOverflowButtonMouseOverBorder` |

**Botão de estouro de documento: estado pressionado**

![Botão de estouro de documento ao pressionar](../../extensibility/ux-guidelines/media/0303-086_overflowpressed.png "0303-086_OverflowPressed")<br />Botão de estouro de documento ao pressionar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.DocWellOverflowButtonMouseDownBackground` |
| Primeiro plano (glifo) | `Environment.DocWellOverflowButtonMouseDownGlyph` |
| Borda | `Environment.DocWellOverflowButtonMouseDownBorder` |

### <a name="tagging"></a>Marcação
O Visual Studio dá suporte à marcação, que permite que um usuário declare palavras-chave pesquisáveis para fins de acompanhamento. Por exemplo, gerentes de projeto e desenvolvedores podem usar Team Foundation Server (TFS) para marcar itens de trabalho. As tabelas a seguir fornecem nomes de cor para a marca em si e o glifo "ícone de fechamento" que aparece nos Estados de focalizar e selecionados.

![Marcação no Visual Studio (Redline)](../../extensibility/ux-guidelines/media/0303-176_taggingredline.png "0303-176_TaggingRedline")<br />Marcação no Visual Studio (Redline)

| Usar... | Não use... |
| --- | --- |
| ... para a interface do usuário que dá suporte à marcação. | ... para qualquer outro tipo de interface do usuário. |

#### <a name="tags"></a>Marcas

**Marca: estado padrão**

![Marca padrão](../../extensibility/ux-guidelines/media/0303-177_tag.png "0303-177_Tag")<br />Marca padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Tag.Background` |
| Primeiro plano (texto) | `Tag.Background` |

**Marca: estado de foco**

![Marca ao focalizar](../../extensibility/ux-guidelines/media/0303-178_taghover.png "0303-178_TagHover")<br />Marca ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Tag.HoverBackground` |
| Primeiro plano (texto) | `Tag.HoverBackgroundText` |

**Marca: estado pressionado**

![Marca pressionada](../../extensibility/ux-guidelines/media/0303-179_tagpressed.png "0303-179_TagPressed")<br />Marca pressionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Tag.PressedBackground` |
| Primeiro plano (texto) | `Tag.PressedBackgroundText` |

**Marca: estado selecionado**

![Marca selecionada](../../extensibility/ux-guidelines/media/0303-180_tagselected.png "0303-180_TagSelected")<br />Marca selecionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Tag.SelectedBackground` |
| Primeiro plano (texto) | `Tag.SelectedBackgroundText` |

#### <a name="close-times-tag-glyph"></a>Glifo de marca de fechamento ( &times; )

**Glifo de marca de fechamento ( &times; ): estado padrão**

![Glifo de marca de fechamento padrão ( &times; )](../../extensibility/ux-guidelines/media/0303-181_tagglyph.png "0303-181_TagGlyph")<br />Glifo de marca de fechamento padrão ( &times; )

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | N/D |
| Primeiro plano (glifo) | `Tag.TagHoverGlyph` |

**Glifo de marca de fechamento ( &times; ): estado de foco**

![Fechar ( &times; ) glifo de marca ao focalizar](../../extensibility/ux-guidelines/media/0303-182_tagglyphhover.png "0303-182_TagGlyphHover")<br />Fechar ( &times; ) glifo de marca ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Tag.TagHoverGlyphHoverBackground` |
| Primeiro plano (glifo) | `Tag.TagHoverGlyphHover` |
| Borda | `Tag.TagHoverGlyphHoverBorder` |

**Glifo de &times; marca Close (): estado pressionado**

![Glifo de marca Close ( &times; ) pressionado](../../extensibility/ux-guidelines/media/0303-183_tagglyphpressed.png "0303-183_TagGlyphPressed")<br />Glifo de marca Close ( &times; ) pressionado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Tag.TagHoverGlyphPressedBackground` |
| Primeiro plano (glifo) | `Tag.TagHoverGlyphPressed` |
| Borda | `Tag.TagHoverGlyphPressedBorder` |

**Marca selecionada com glifo de fechamento ( &times; ): estado padrão**

![Marca padrão selecionada com glifo de fechamento ( &times; )](../../extensibility/ux-guidelines/media/0303-184_tagselected.png "0303-184_TagSelected")<br />Marca padrão selecionada com glifo de fechamento ( &times; )

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | N/D |
| Primeiro plano (glifo) | `Tag.TagSelectedGlyph` |

**Marca selecionada com glifo de fechamento ( &times; ): estado de foco**

![Marca selecionada com glifo de fechamento ( &times; ) ao focalizar](../../extensibility/ux-guidelines/media/0303-185_tagselectedhover.png "0303-185_TagSelectedHover")<br />Marca selecionada com glifo de fechamento ( &times; ) ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Tag.TagSelectedGlyphHoverBackground` |
| Primeiro plano (glifo) | `Tag.TagSelectedGlyphHover` |
| Borda | `Tag.TagSelectedGlyphHoverBorder` |

**Marca selecionada com glifo de fechamento ( &times; ): estado pressionado**

![Marcada, marca pressionada com glifo de fechamento ( &times; )](../../extensibility/ux-guidelines/media/0303-186_tagselectedpressed.png "0303-186_TagSelectedPressed")<br />Marcada, marca pressionada com glifo de fechamento ( &times; )

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Tag.TagSelectedGlyphPressedBackground` |
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
| Tela de fundo | `Environment.ToolWindowBackground` |
| Borda | `Environment.ToolWindowBorder` |

**Janela de ferramentas flutuante e focalizada**

![Janela de ferramentas flutuante e focalizada](../../extensibility/ux-guidelines/media/0303-090_toolwindowfocused.png "0303-090_ToolWindowFocused")<br />Janela de ferramentas flutuante e focalizada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ToolWindowBackground` |
| Borda | `Environment.MainWindowActiveDefaultBorder` |

**Janela de ferramentas flutuante, desfocada**

![Janela de ferramentas flutuante, desfocada](../../extensibility/ux-guidelines/media/0303-091_toolwindowunfocused.png "0303-091_ToolWindowUnfocused")<br />Janela de ferramentas flutuante, desfocada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ToolWindowBackground` |
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
| Tela de fundo | `Environment.ToolboxContent`<br />Títulos |
| Tela de fundo | `Environment.ToolWindowBackground`<br />(Itens individuais ou janela inteira, se não houver controles disponíveis) |
| Borda | Nenhum |
| Primeiro plano (glifo) | `Environment.ToolboxContent` |
| Primeiro plano (texto) | `Environment.ToolboxContent` |

**Nós filho da caixa de ferramentas: estado de foco**

![Nó filho da caixa de ferramentas ao focalizar](../../extensibility/ux-guidelines/media/0303-192_toolboxchildnodehover.png "0303-192_ToolboxChildNodeHover")<br />Nó filho da caixa de ferramentas ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ToolboxContentMouseOver`<br />(Somente itens individuais) |
| Borda | Nenhum |
| Primeiro plano (texto) | `Environment.ToolboxContentMouseOver`<br />(Somente itens individuais) |

**Nós da caixa de ferramentas selecionados: estado focalizado**

![Foco, nó pai da caixa de ferramentas selecionada](../../extensibility/ux-guidelines/media/0303-193_toolboxparentnodefocused.png "0303-193_ToolboxParentNodeFocused")<br />Foco, nó pai da caixa de ferramentas selecionada

![Foco, nó filho da caixa de ferramentas selecionada](../../extensibility/ux-guidelines/media/0303-194_toolboxchildnodefocused.png "0303-194_ToolboxChildNodeFocused")<br />Foco, nó filho da caixa de ferramentas selecionada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `TreeView.SelectedItemActive`<br />Categoria da [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) |
| Borda | `TreeView.FocusVisualBorder`<br />Categoria da [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) |
| Primeiro plano (glifo) | `TreeView.SelectedItemActive`<br />Categoria da [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) |
| Primeiro plano (texto) | `TreeView.SelectedItemActive`<br />Categoria da [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) |

**Nós da caixa de ferramentas selecionados: estado não focalizado**

![Nó pai da caixa de ferramentas selecionado, não focalizado](../../extensibility/ux-guidelines/media/0303-195_toolboxparentnodeunfocused.png "0303-195_ToolboxParentNodeUnfocused")<br />Nó pai da caixa de ferramentas selecionado, não focalizado

![Nó filho da caixa de ferramentas selecionado, não focalizado](../../extensibility/ux-guidelines/media/0303-196_toolboxchildnodeunfocused.png "0303-196_ToolboxChildNodeUnfocused")<br />Nó filho da caixa de ferramentas selecionado, não focalizado

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `TreeView.SelectedItemInactive`<br />Categoria da [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) |
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
| Tela de fundo | `Environment.TitleBarActiveGradientBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.TitleBarActiveText` |
| Borda | `Environment.TitleBarActiveBorder`<br />(Defina como a mesma cor como plano de fundo.) |
| Identificador de arrastar | `Environment.TitleBarDragHandleActive` |

**Barra de título sem foco**

![Barra de título desfocada](../../extensibility/ux-guidelines/media/0303-094_titlebarunfocused.png "0303-094_TitleBarUnfocused")<br />Barra de título sem foco

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.TitleBarInactiveGradientBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
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
| Tela de fundo | N/D |
| Primeiro plano (glifo) | `Environment.ToolWindowButtonActiveGlyph` |
| Borda | N/D |

**Botões da barra de título sem foco: estado padrão**

![Padrão, botões de barra de título sem foco](../../extensibility/ux-guidelines/media/0303-097_titlebarbuttonunfocused.png "0303-097_TitleBarButtonUnfocused")<br />Padrão, botões de barra de título sem foco

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | N/D |
| Primeiro plano (glifo) | `Environment.ToolWindowButtonInactiveGlyph` |
| Borda | N/D |

**Botões da barra de título focalizado: estado de foco**

![Botões da barra de título focalizados ao focalizar](../../extensibility/ux-guidelines/media/0303-098_titlebarbuttonfocusedhover.png "0303-098_TitleBarButtonFocusedHover")<br />Botões da barra de título focalizados ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ToolWindowButtonHoverActive` |
| Primeiro plano (glifo) | `Environment.ToolWindowButtonHoverActiveGlyph` |
| Borda | `Environment.ToolWindowButtonHoverActiveBorder` |

**Botões da barra de título sem foco: estado de foco**

![Botões da barra de título sem foco ao focalizar](../../extensibility/ux-guidelines/media/0303-099_titlebarbuttonunfocusedhover.png "0303-099_TitleBarButtonUnfocusedHover")<br />Botões da barra de título sem foco ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ToolWindowButtonHoverInactive` |
| Primeiro plano (glifo) | `Environment.ToolWindowButtonHoverInactiveGlyph` |
| Borda | `Environment.ToolWindowButtonHoverInactiveBorder` |

**Botões da barra de título focalizado: estado pressionado**

![Botões da barra de título focalizados ao pressionar](../../extensibility/ux-guidelines/media/0303-100_titlebarbuttonfocusedpressed.png "0303-100_TitleBarButtonFocusedPressed")<br />Botões da barra de título focalizados ao pressionar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ToolWindowButtonDown` |
| Primeiro plano (glifo) | `Environment.ToolWindowButtonDownActiveGlyph` |
| Borda | `Environment.ToolWindowButtonDownBorder` |

**Botões da barra de título sem foco: estado pressionado**

![Botões da barra de título sem foco ao pressionar](../../extensibility/ux-guidelines/media/0303-101_titlebarbuttonunfocusedpressed.png "0303-101_TitleBarButtonUnfocusedPressed")<br />Botões da barra de título sem foco ao pressionar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ToolWindowButtonDown` |
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
| Tela de fundo | `Environment.ToolWindowTabSelectedTab` |
| Primeiro plano (texto) | `Environment.ToolWindowTabSelectedActiveText` |
| Borda | `Environment.ToolWindowTabSelectedBorder`<br />(Defina como a mesma cor como plano de fundo.) |

**Selecionada, guia de janela de ferramentas não focalizada**

![Selecionada, guia de janela de ferramentas não focalizada](../../extensibility/ux-guidelines/media/0303-104_toolwindowtabunfocused.png "0303-104_ToolWindowTabUnfocused")<br />Selecionada, guia de janela de ferramentas não focalizada

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ToolWindowTabSelectedTab` |
| Primeiro plano (texto) | `Environment.ToolWindowTabSelectedText` |
| Borda | `Environment.ToolWindowTabSelectedBorder`<br />(Defina como a mesma cor como plano de fundo.) |

**Guia da janela da ferramenta de segundo plano: estado padrão**

![Guia de janela da ferramenta de segundo plano padrão](../../extensibility/ux-guidelines/media/0303-105_toolwindowbackgroundtab.png "0303-105_ToolWindowBackgroundTab")<br />Guia de janela da ferramenta de segundo plano padrão

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ToolWindowTabGradientBegin`<br />`Environment.ToolWindowTabGradientEnd`<br />(As interrupções de gradiente são definidas com o mesmo valor de cor em Visual Studio 2013.) |
| Primeiro plano (texto) | `Environment.ToolWindowTabText` |
| Borda | `Environment.ToolWindowTabBorder` |

**Guia da janela da ferramenta de segundo plano: estado de foco**

![Guia da janela da ferramenta de segundo plano ao focalizar](../../extensibility/ux-guidelines/media/0303-106_toolwindowbackgroundtabhover.png "0303-106_ToolWindowBackgroundTabHover")<br />Guia da janela da ferramenta de segundo plano ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.ToolWindowTabMouseOverBackgroundBegin`<br />`Environment.ToolWindowTabMouseOverBackgroundEnd`<br />(As interrupções de gradiente são definidas com o mesmo valor de cor em Visual Studio 2013.) |
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
| Tela de fundo | `Environment.AutoHideTabBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.AutoHideTabText` |
| Borda | `Environment.AutoHideTabBorder` |

**Ocultar guias automaticamente: estado de foco**

![Ocultar guia automaticamente ao focalizar](../../extensibility/ux-guidelines/media/0303-109_autohidetabhover.png "0303-109_AutoHideTabHover")<br />Ocultar guia automaticamente ao focalizar

| Elemento | Nome do token: categoria. cor |
| --- | --- |
| Tela de fundo | `Environment.AutoHideTabMouseOverBackgroundBegin`<br />(As interrupções de gradiente para esse token não são usadas na interface do usuário com tema.) |
| Primeiro plano (texto) | `Environment.AutoHideTabMouseOverText` |
| Borda | `Environment.AutoHideTabMouseOverBorder` |
