---
title: Compartilhado cores para o Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 8d11b9a0-6175-4f2e-8e7f-79daee1bfd41
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 19d628f2f83943b88a415699dddd78f033597983
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49833337"
---
# <a name="shared-colors-for-visual-studio"></a>Cores compartilhadas para o Visual Studio
Quando você está projetando a interface do usuário que usa elementos comuns de shell do Visual Studio, ou você gostaria de seu elemento de interface para ser consistente com recursos semelhantes, use nomes de token existentes nos arquivos de definição de pacote para escolher e atribuir cores. Isso garante que sua interface do usuário permaneça consistente com o ambiente geral do Visual Studio e que ele será atualizado automaticamente quando os temas são adicionados ou atualizados.  

Este artigo descreve os elementos de interface do usuário comuns e os nomes de token que eles usam, que você pode fazer referência ao criar a interface do usuário semelhante. Para obter informações específicas sobre como acessar esses tokens de cor, consulte [o serviço VSColor](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService).  

Certifique-se de usar nomes de token corretamente:  

-   **Use nomes de token com base em função, não na própria cor.** As cores compartilhadas comuns são associadas aos elementos de interface específica e destinam-se somente a ser usado para os recursos iguais ou semelhantes. Por exemplo, não reutilize a cor de uma caixa de combinação pressionado para uma animação de progresso de rotação simplesmente porque você gosta de cor. As funções de caixa de combinação e a animação são diferentes, e se a cor associada com as alterações de caixa de combinação, não pode ser uma cor apropriada para seu elemento de animação. Uso consistente de cor ajuda a orientar seus usuários e evitar confusão.  

-   **Use cores de plano de fundo e texto na combinação correta.** Cores de plano de fundo que se destinam a serem usadas com texto terá uma cor do texto associado. Não use cores de texto que não seja o que é especificado para esse plano de fundo. Se não houver uma cor do texto associado, não use essa cor do plano de fundo para qualquer superfície na qual você pretende exibir texto. Outras combinações de cores de plano de fundo e texto podem resultar em uma interface não pode ser lido.  

-   **Use cores do controle que são apropriadas para seu local.** Em alguns estados, alguns controles do Visual Studio não tem a borda separada e cores de plano de fundo. Em vez disso, eles selecionam essas cores de superfícies de por trás delas. Certifique-se de que você sempre use os nomes de token que são apropriados para o local onde você está colocando o controle.  

> [!IMPORTANT]
> Não use tokens localizadas nas categorias de "Página inicial" ou "Cider".  

## <a name="common-shared-controls"></a>Controles compartilhados comuns

Quando você usa uma barra de comandos padrão do Visual Studio em seu recurso, você terá acesso aos controles de shell com estilo. Você não deve re-modelo desses controles comuns. No entanto, se você precisar criar uma barra de comandos personalizada, você precisa criar controles personalizados também. Nesse caso, certifique-se de usar os nomes de token corretos para cada um dos seguintes controles para que sua interface do usuário seja consistente com o restante do Visual Studio.

### <a name="button-controls"></a>Controles de botão

![Aplicar linhas vermelhas no controle de botão](../../extensibility/ux-guidelines/media/0303-155_buttoncontrolredline.png "0303 155_ButtonControlRedline")

| Use... | Não use... |
| --- | --- |
| ... nos botões em do poço de documento que você deseja integrar com temas do Visual Studio (claro, escuro, azul ou um tema de alto contraste do sistema). | ... para os botões que serão exibidos em um plano de fundo personalizado que não faz parte de um tema do Visual Studio. |

**Botão: estado padrão**

![Botão padrão](../../extensibility/ux-guidelines/media/03.03.Button.Standard.png "03.03.Button.Standard")<br />Botão padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Botão | `CommonControls.Button` |
| Borda do botão | `CommonControls.ButtonBorder` |

**Botão: estado padrão**

![Botão padrão](../../extensibility/ux-guidelines/media/03.03.Button.Default.png "03.03.Button.Default")<br />Botão padrão

| Elemento | Nome do token: Category.color | 
| --- | --- | 
| Botão | `CommonControls.ButtonDefault` |
| Borda do botão | `CommonControls.ButtonBorderDefault` |

**Botão: estado desabilitado**  

![Botão desabilitado](../../extensibility/ux-guidelines/media/03.03.Button.Disabled.png "03.03.Button.Disabled")<br />Botão desabilitado  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Botão | `CommonControls.ButtonDisabled` |
| Borda do botão | `CommonControls.ButtonBorderDisabled` |

**Botão: estado de focalização**  

![Botão focalizar](../../extensibility/ux-guidelines/media/03.03.Button.hover.png "03.03.Button.hover")<br />Botão ao focalizar  

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

**Botão: estado de foco**  

![Botão com foco](../../extensibility/ux-guidelines/media/03.03.Button.Focused.png "03.03.Button.Focused")<br />Botão com foco  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Botão | `CommonControls.ButtonFocused` |
| Borda do botão | `CommonControls.ButtonBorderFocused` |

### <a name="check-box-controls"></a>Controles de caixa de seleção  
![Caixa de seleção (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-161_checkboxredline.png "0303 161_CheckboxRedline")<br />Caixa de seleção (corte de funcionários)  

| Use... | Não use... |
| --- | --- |
| ... para controles de caixa de seleção contidos no documento bem. | ... para qualquer interface do usuário que não é um controle de caixa de seleção. |

**Caixa de seleção: estado padrão**  

![Caixa de seleção](../../extensibility/ux-guidelines/media/0303-162_checkbox.png "0303 162_Checkbox")<br />Caixa de seleção padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `CommonControls.CheckBoxBackground` |
| Borda | `CommonControls.CheckBoxBorder` |
| Texto | `CommonControls.CheckBoxText` |
| Glifo | `CommonControls.CheckBoxGlyph` |

**Caixa de seleção: estado desabilitado**  

![Caixa de seleção desabilitada](../../extensibility/ux-guidelines/media/0303-163_checkboxdisabled.png "0303 163_CheckboxDisabled")<br />Caixa de seleção desabilitada  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `CommonControls.CheckBoxBackgroundDisabled` |
| Borda | `CommonControls.CheckBoxBorderDisabled` |
| Texto | `CommonControls.CheckBoxTextDisabled` |
| Glifo | `CommonControls.CheckBoxGlyphDisabled` |

**Caixa de seleção: passe o mouse de estado**  

 ![Caixa de seleção ao focalizar](../../extensibility/ux-guidelines/media/0303-164_checkboxhover.png "0303 164_CheckboxHover")<br />Caixa de seleção ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `CommonControls.CheckBoxBackgroundHover` |
| Borda | `CommonControls.CheckBoxBorderHover` |
| Texto | `CommonControls.CheckBoxTextHover` |
| Glifo | `CommonControls.CheckBoxGlyphHover` |  

**Caixa de seleção: estado pressionado**  

![Caixa de seleção pressionada](../../extensibility/ux-guidelines/media/0303-165_checkboxpressed.png "0303 165_CheckboxPressed")<br />Caixa de seleção pressionada  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `CommonControls.CheckBoxBackgroundPressed` |
| Borda | `CommonControls.CheckBoxBorderPressed` |
| Texto | `CommonControls.CheckBoxTextPressed` |
| Glifo | `CommonControls.CheckBoxGlyphPressed` |  

**Caixa de seleção: voltada para o estado**  

![Caixa de seleção focalizada](../../extensibility/ux-guidelines/media/0303-166_checkboxfocused.png "0303 166_CheckboxFocused")<br />Caixa de seleção com foco  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `CommonControls.CheckBoxBackgroundFocused` |
| Borda | `CommonControls.CheckBoxBorderFocused` |
| Texto | `CommonControls.CheckBoxTextFocused` |
| Glifo | `CommonControls.CheckBoxGlyphFocused` |

### <a name="drop-downs-and-combo-boxes"></a>Menus suspensos e combinação caixas
![Caixa de combinação/drop-down (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-167_dropdowncomboboxredline.png "0303 167_DropDownComboBoxRedline")<br />Caixa de combinação/drop-down (corte de funcionários)  

| Use... | Não use... |
| --- | --- |
| ... para listas suspensas e combinação caixas no documento bem. | ... para qualquer interface do usuário que não é uma lista suspensa ou caixa de combinação. |  
| | ... para a barra de comandos [menus suspensos](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandDropDown) ou [caixas de combinação](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandComboBox). |

**Menus suspensos e combinação caixas: estado padrão**  

![Caixa de combinação/drop-down padrão](../../extensibility/ux-guidelines/media/0303-168_dropdowncombobox.png "0303 168_DropDownComboBox")<br />Caixa de combinação/drop-down padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `CommonControls.ComboBoxBackground` |
| Borda | `CommonControls.ComboBoxBorder` |
| Texto | `CommonControls.ComboBoxText` |
| Separador | `CommonControls.ComboBoxSeparator` |
| Glifo | `CommonControls.ComboBoxGlyph` |
| Plano de fundo de glifo | `CommonControls.ComboBoxGlyphBackground` |

**Menus suspensos e combinação caixas: estado desabilitado**  

![Caixa de combinação/drop-down desabilitada](../../extensibility/ux-guidelines/media/0303-169_dropdowncomboboxdisabled.png "0303 169_DropDownComboBoxDisabled")<br />Caixa de combinação/drop-down desabilitada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `CommonControls.ComboBoxBackgroundDisabled` |
| Borda | `CommonControls.ComboBoxBorderDisabled` |
| Texto | `CommonControls.ComboBoxTextDisabled` |
| Separador | `CommonControls.ComboBoxSeparatorDisabled` |
| Glifo | `CommonControls.ComboBoxGlyphDisabled` |
| Plano de fundo de glifo | `CommonControls.ComboBoxGlyphBackgroundDisabled` |

**Menus suspensos e combinação caixas: passe o mouse de estado**  

![Caixa de combinação/drop-down focalizar](../../extensibility/ux-guidelines/media/0303-170_dropdowncomboboxhover.png "0303 170_DropDownComboBoxHover")<br />Caixa de combinação/drop-down em foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `CommonControls.ComboBoxBackgroundHover` |
| Borda | `CommonControls.ComboBoxBorderHover` |
| Texto | `CommonControls.ComboBoxTextHover` |
| Separador | `CommonControls.ComboBoxSeparatorHover` |
| Glifo | `CommonControls.ComboBoxGlyphHover` |
| Plano de fundo de glifo | `CommonControls.ComboBoxGlyphBackgroundHover` |

**Menus suspensos e combinação caixas: estado pressionado**  

![Caixa de combinação/drop-down de pressionado](../../extensibility/ux-guidelines/media/0303-171_dropdowncomboboxpressed.png "0303 171_DropDownComboBoxPressed")<br />Caixa de combinação/drop-down pressionada  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `CommonControls.ComboBoxBackgroundPressed` |
| Borda | `CommonControls.ComboBoxBorderPressed` |
| Texto | `CommonControls.ComboBoxTextPressed` |
| Separador | `CommonControls.ComboBoxSeparatorPressed` |
| Glifo | `CommonControls.ComboBoxGlyphPressed` |
| Plano de fundo de glifo | `CommonControls.ComboBoxGlyphBackgroundPressed` |

**Exibição de item de lista de caixas de listas suspensas e combinação: estado pressionado**  

 ![Caixa de combinação/drop-down pressionado o modo de exibição de item de lista](../../extensibility/ux-guidelines/media/0303-174_dropdowncomboboxlistview.png "0303 174_DropDownComboBoxListView")<br />Caixa de combinação/drop-down pressionado o modo de exibição de item de lista  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `CommonControls.ComboBoxListBackground`<br />`CommonControls.ComboBoxListBackgroundHover`<br />`CommonControls.ComboBoxListItemBackgroundPressed`<br />`CommonControls.ComboBoxListItemBackgroundFocused` |
| Borda | `CommonControls.ComboBoxListBorder`<br />`CommonControls.ComboBoxListBorderHover`<br />`CommonControls.ComboBoxListBorderPressed`<br />`CommonControls.ComboBoxListBorderFocused` |
| Texto do item | `CommonControls.ComboBoxListItemText`<br /> `CommonControls.ComboBoxListItemTextHover`<br />`CommonControls.ComboBoxListItemTextPressed`<br />`CommonControls.ComboBoxListItemTextFocused` |
| Sombra do plano de fundo | `CommonControls.ComboBoxListBackgroundShadow` |

**Menus suspensos e combinação caixas: voltada para o estado**  

![Caixa de combinação/drop-down com foco](../../extensibility/ux-guidelines/media/0303-172_dropdowncomboboxfocused.png "0303 172_DropDownComboBoxFocused")<br />Caixa de combinação/drop-down com foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `CommonControls.ComboBoxBackgroundFocused` |
| Borda | `CommonControls.ComboBoxBorderFocused` |
| Texto | `CommonControls.ComboBoxTextFocused` |
| Separador | `CommonControls.ComboBoxSeparatorFocused` |
| Glifo | `CommonControls.ComboBoxGlyphFocused` |
| Plano de fundo de glifo | `CommonControls.ComboBoxGlyphBackgroundFocused` |

**Menus suspensos e combinação caixas: seleção de entrada de texto**  

![Seleção de entrada de texto da caixa de combinação/drop-down](../../extensibility/ux-guidelines/media/0303-173_dropdowncomboboxtextinput.png "0303 173_DropDownComboBoxTextInput")<br />Seleção de entrada de texto da caixa de combinação/drop-down  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Realce | `CommonControls.ComboBoxTextInputSelection` |

### <a name="tabular-data-grid-controls"></a>Controles de dados tabulares (grade)  
Controles de dados de tabela, também conhecido como controles de grade, são controles comuns do Visual Studio que pode ser usado para apresentar grandes quantidades de dados em várias colunas. Controles de dados de tabela padrão podem ser encontrados em vários lugares dentro do Visual Studio: a janela de ferramentas da lista de erros, os relatórios de IntelliTrace e exibição de heap de memória, entre outros. Sempre use os controles de dados de tabela padrão fornecidos. Em alguns casos raros, talvez você não tenha acesso aos controles de dados de tabela padrão. Nessas situações, use os seguintes nomes de token para garantir que sua interface do usuário seja consistente com outros controles de dados tabulares no Visual Studio.  

![Controle de grade/dados tabulares (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-197_tabulardatagridcontrolredline.png "0303 197_TabularDataGridControlRedline")<br />Controle de grade/dados tabulares (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... por tabela ou controles de grade. | ... para qualquer interface do usuário que não é um controle de tabela ou grade. |

#### <a name="column-headers"></a>Cabeçalhos de coluna  
Cabeçalhos de coluna consistem em um plano de fundo, uma borda, o texto do título e um glifo opcional que geralmente usado quando uma grade é classificada pela coluna.  

**Cabeçalho de coluna: estado padrão**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Header.Default` |
| Em primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Em primeiro plano (glifo) | `Header.Glyph` |
| Borda | `Header.SeparatorLine` |

**Cabeçalho de coluna: passe o mouse de estado**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Header.MouseOver` |
| Em primeiro plano (texto) | `Environment.CommandBarTextHover` |
| Em primeiro plano (glifo) | `Header.MouseOverGlyph` |
| Borda | `Header.SeparatorLine` |

**Cabeçalho de coluna: estado pressionado**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `CommonControls.CheckBoxBackgroundPressed` |
| Em primeiro plano (texto) | `CommonControls.CheckBoxBorderPressed` |
| Em primeiro plano (glifo) | `CommonControls.CheckBoxTextPressed` |
| Borda | `CommonControls.CheckBoxGlyphPressed` |

#### <a name="list-view-items"></a>Exibir itens de lista  
 Exibir itens de lista consistem em um plano de fundo e o conteúdo. O conteúdo pode ser texto, um ícone ou ambos.  

**Itens de exibição de lista: estado padrão**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | Transparente |
| Em primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Borda | Nenhum |

**Itens de exibição de lista: estado ativo**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `TreeView.SelectedItemActive` |
| Em primeiro plano (texto) | `TreeView.SelectedItemActiveText` |
| Borda | Nenhum |

**Itens de exibição de lista: estado inativo**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `TreeView.SelectedItemInactive` |
| Em primeiro plano (texto) | `TreeView.SelectedItemInactiveText` |
| Borda | Nenhum |  

### <a name="ui-text"></a>Texto da interface do usuário

#### <a name="instructional-text"></a>Texto de instrução
Texto de instrução fornece uma explicação principal proeminente do que fazer em uma página da caixa de diálogo ou documento.

![Padrão de texto de instrução](../../extensibility/ux-guidelines/media/0303_InstructionalText.png "0303_InstructionalText.png")<br />Padrão de texto com instrução

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `Environment.ControlText` |

#### <a name="secondary-instructional-text"></a>Texto de instrução secundário
Nas páginas de documento com muito texto e controles, algum texto de instrução usa um valor de cor diferente. Isso ajuda a transmitir a quais informações são mais importantes e diminuir a densidade geral dos elementos da interface do usuário. (Consulte também a seção no texto de dica abaixo.)

![Texto de instrução secundário](../../extensibility/ux-guidelines/media/0303_SecondaryInstructionalText.png "0303_SecondaryInstructionalText.png")<br />Texto de instrução secundário

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `Environment.ControlEditHintText` |

#### <a name="hint-text"></a>Texto de dica
Texto de dica é exibido em um controle vazio, abaixo de um controle ou em uma superfície de documento vazio para mostrar ao usuário o que fazer em seguida. Você pode usar o texto de dica com planos de fundo de janela ou controle.

**Texto de dica de padrão**

![Padrão de texto de dica](../../extensibility/ux-guidelines/media/0303_HintText.png "0303_HintText.png")<br />Texto de dica de padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `Environment.ControlEditHintText` |

**Texto de dica necessária**

![Texto de dica necessário](../../extensibility/ux-guidelines/media/0303_RequiredHintText.png "0303_RequiredHintText.png")<br />Texto de dica necessária

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `Environment.ControlRequiredHintText` |
| Informações preliminares | `Environment.ControlRequiredBackground` |

**Texto de controle de caixa de pesquisa**

> Ver [caixas de pesquisa](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_SearchBoxes) para outros tokens de cor relacionados ao controle de pesquisa.

![Texto de controle de caixa de pesquisa](../../extensibility/ux-guidelines/media/0303_SearchBoxControl.png "0303_SearchBoxControl.png")<br />Texto de controle de caixa de pesquisa

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `SearchControl.UnfocusedWatermarkText` |

### <a name="hyperlink"></a>Hiperlink  
O hiperlink é um controle que não tem um par de primeiro e segundo plano. Em todos os casos, use a cor de hiperlink de primeiro plano, que será exibido corretamente em planos de fundo escuros, cinzas e brancos. Se você não usar o token de cor para o controle de hiperlink, você verá a cor padrão do sistema para "pressionado", que piscará vermelho. Esse é o sinal de que o controle não estiver usando o token de cor de ambiente correta.  

![Hiperlink (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-133_hyperlinkredline.png "0303 133_HyperlinkRedline")<br />Hiperlink (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... quando você precisa criar um hiperlink personalizado. | ... para qualquer coisa que não é um hiperlink. |

**Hiperlink: estado padrão**  

![Hiperlink padrão](../../extensibility/ux-guidelines/media/0303-134_hyperlink.png "0303 134_Hyperlink")<br />Hiperlink padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `Environment.PanelHyperlink` |

**Hiperlink: estado de focalização**

![Hiperlink focalizar](../../extensibility/ux-guidelines/media/0303-135_hyperlinkhover.png "0303 135_HyperlinkHover")<br />Hiperlink ao focalizar  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `Environment.PanelHyperlinkHover` |

**Hiperlink: estado pressionado**

![Hiperlink pressionado](../../extensibility/ux-guidelines/media/0303-136_hyperlinkpressed.png "0303 136_HyperlinkPressed")<br />Hiperlink pressionado  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `Environment.PanelHyperlinkPressed` |

**Hiperlink: estado desabilitado**

![Hiperlink desabilitado](../../extensibility/ux-guidelines/media/0303-137_hyperlinkdisabled.png "0303 137_HyperlinkDisabled")<br />Hiperlink desabilitado  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `Environment.PanelHyperlinkDisabled` |

### <a name="infobars"></a>Infobars  
Infobars são usados para fornecer mais informações sobre um determinado contexto e sempre serão exibidos na parte superior de uma janela de documento ou janela de ferramentas.  

![Barra de informações (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-138_infobarredline.png "0303 138_InfobarRedline")<br />Barra de informações (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... ao criar infobars personalizados. | ... para elementos de interface do usuário que não são semelhantes a uma barra de informações. |

**Barra de informações: estado padrão**

![Padrão da barra de informações](../../extensibility/ux-guidelines/media/0303-139_infobar.png "0303 139_Infobar")<br />Barra de informações padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `InfoBar.InfoBarBackground` |
| Em primeiro plano (texto) | `InfoBar.InfoBar` |
| Borda | `InfoBar.InfoBarBorder` |

**Fechar barra de informações (&times;) botão: estado padrão**

![Fechar barra de informações de padrão (&times;) botão](../../extensibility/ux-guidelines/media/0303_InfobarCloseDefault.png "0303_InfobarCloseDefault.png")<br />Fechar barra de informações de padrão (&times;) botão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `InfoBar.CloseButton` |
| Borda | `InfoBar.CloseButtonBorder` |
| Glifo | `InfoBar.CloseButtonGlyph` |

**Fechar barra de informações (&times;) botão: passe o mouse de estado**

![Fechar barra de informações (&times;) botão focalizar](../../extensibility/ux-guidelines/media/0303_InfobarCloseHover.png "0303_InfobarCloseHover.png")<br />Fechar barra de informações (&times;) botão ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `InfoBar.CloseButtonHover` |
| Borda | `InfoBar.CloseButtonHoverBorder` |
| Glifo | `InfoBar.CloseButtonHoverGlyph` |

**Fechar barra de informações (&times;) botão: estado pressionado**

![Fechar barra de informações de pressionado (&times;) botão](../../extensibility/ux-guidelines/media/0303_InfobarClosePressed.png "0303_InfobarClosePressed.png")<br />Fechar barra de informações de pressionado (&times;) botão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `InfoBar.CloseButtonDown` |
| Borda | `InfoBar.CloseButtonDownBorder` |
| Glifo | `InfoBar.CloseButtonDownGlyph` |

**Botão de hiperlink de barra de informações: estado padrão**

![Botão de hiperlink padrão da barra de informações](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonDefault.png "0303_InfobarHyperlinkButtonDefault.png")<br />Botão de hiperlink padrão da barra de informações

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `InfoBar.Hyperlink` |

**Botão de hiperlink de barra de informações: passe o mouse de estado**

![Botão de hiperlink de barra de informações ao focalizar](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonHover.png "0303_InfobarHyperlinkButtonHover.png")<br />Botão de hiperlink de barra de informações ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `Infobar.HyperlinkMouseOver`<br />(Com sublinhado) |

**Botão de hiperlink de barra de informações: estado pressionado**

![Botão de hiperlink de barra de informações pressionado](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonPressed.png "0303_InfobarHyperlinkButtonPressed.png")<br />Botão de hiperlink pressionado da barra de informações

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `Infobar.HyperlinkMouseDown`<br />(Com sublinhado) |

**Barra de informações embutido hyperlink (dentro de uma sentença): estado padrão**

![Botão de hiperlink padrão embutido da barra de informações](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonDefault.png "0303_InfobarHyperlinkButtonDefault.png")<br />Botão de hiperlink padrão embutido da barra de informações

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `InfoBar.Hyperlink` |

**Barra de informações embutido hyperlink (dentro de uma sentença): passe o mouse de estado**

![Botão de hiperlink embutido da barra de informações ao focalizar](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkInlineHover.png "0303_InfobarHyperlinkInlineHover.png")<br />Botão de hiperlink embutido da barra de informações ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `Infobar.HyperlinkMouseOver`<br />(Com sublinhado) |

**Barra de informações embutido hyperlink (dentro de uma sentença): estado pressionado**

![Botão de hiperlink embutido da barra de informações pressionado](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkInlinePressed.png "0303_InfobarHyperlinkInlinePressed.png")<br />Barra de informações embutido hyperlink botão pressionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `Infobar.HyperlinkMouseDown`<br />(Com sublinhado) |

**Botão de barra de informações: estado padrão**

![Botão de barra de informações padrão](../../extensibility/ux-guidelines/media/0303_InfobarButtonDefault.png "0303_InfobarButtonDefault.png")<br />Botão de barra de informações padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `InfoBar.Button` |
| Em primeiro plano (texto) | `InfoBar.Button` |
| Borda | `InfoBar.ButtonBorder` |

**Botão de barra de informações: passe o mouse de estado**

![Botão de barra de informações ao focalizar](../../extensibility/ux-guidelines/media/0303_InfobarButtonHover.png "0303_InfobarButtonHover.png")<br />Botão de barra de informações ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `InfoBar.ButtonMouseOver` |
| Em primeiro plano (texto) | `InfoBar.ButtonMouseOver` |
| Borda | `InfoBar.ButtonMouseOverBorder` |

**Botão de barra de informações: estado pressionado**

![Botão de barra de informações pressionado](../../extensibility/ux-guidelines/media/0303_InfobarButtonPressed.png "0303_InfobarButtonPressed.png")<br />Botão de barra de informações pressionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `InfoBar.ButtonMouseDown` |
| Em primeiro plano (texto) | `InfoBar.ButtonMouseDown` |
| Borda | `InfoBar.ButtonMouseDownBorder` |

**Botão de barra de informações: estado desabilitado**

![Botão de barra de informações desabilitado](../../extensibility/ux-guidelines/media/0303_InfobarButtonDisabled.png "0303_InfobarButtonDisabled.png")<br />Botão de barra de informações desabilitado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `InfoBar.ButtonDisabled` |
| Em primeiro plano (texto) | `InfoBar.ButtonDisabled` |
| Borda | `InfoBar.ButtonDisabledBorder` |

**Botão de barra de informações: voltada para o estado**

![Botão de barra de informações focalizado](../../extensibility/ux-guidelines/media/0303_InfobarButtonFocus.png "0303_InfobarButtonFocus.png")<br />Botão de barra de informações com foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `InfoBar.ButtonFocus` |
| Em primeiro plano (texto) | `InfoBar.ButtonFocus` |
| Borda | `InfoBar.ButtonFocusBorder` |

### <a name="scroll-bars"></a>Barras de rolagem  
Barras de rolagem são denominadas pelo ambiente do Visual Studio e não precisará ser com tema. No entanto, você pode decidir o que você deseja aproveitar as cores usadas nas barras de rolagem para que sua interface do usuário apareça sempre consistente com essa parte do ambiente do Visual Studio.  

![Barra de rolagem (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-140_scrollbarredline.png "0303 140_ScrollbarRedline")<br />Barra de rolagem (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... quando você estiver criando interface do usuário que você deseja corresponder as barras de rolagem do Visual Studio. | ... para que você não quiser sempre corresponder da interface do usuário da barra de rolagem. |

**Barra de rolagem: estado padrão**  

![Barra de rolagem padrão](../../extensibility/ux-guidelines/media/0303-141_scrollbar.png "0303 141_Scrollbar")<br />Barra de rolagem padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Barra de rolagem | `Environment.ScrollBarBackground` |
| Em primeiro plano (Thumb) | `Environment.ScrollBarThumbBackground` |

**Barra de rolagem: passe o mouse de estado**

![Barra de rolagem ao passar](../../extensibility/ux-guidelines/media/0303-143_scrollbarhover.png "0303 143_ScrollbarHover")<br />Barra de rolagem ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Barra de rolagem | `Environment.ScrollBarBackground` |
| Em primeiro plano (Thumb) | `Environment.ScrollBarThumbMouseOverBackground` |

*Barra de rolagem: estado pressionado**

![Barra de rolagem pressionado](../../extensibility/ux-guidelines/media/0303-145_scrollbarpressed.png "0303 145_ScrollbarPressed")<br />Pressionada a barra de rolagem  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Barra de rolagem | `Environment.ScrollBarBackground` |
| Em primeiro plano (Thumb) | `Environment.ScrollBarThumbPressedBackground` |

**Seta da barra de rolagem: estado padrão**  

![Seta padrão da barra de rolagem](../../extensibility/ux-guidelines/media/0303-142_scrollbararrow.png "0303 142_ScrollbarArrow")<br />Seta de barra de rolagem padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ScrollBarArrowBackground`<br />(Definido para a mesma cor de barra de rolagem). |
| Em primeiro plano (glifo) | `Environment.ScrollBarArrowGlyph` |

**Seta da barra de rolagem: passe o mouse de estado**

![Seta no foco da barra de rolagem](../../extensibility/ux-guidelines/media/0303-144_scrollbararrowhover.png "0303 144_ScrollbarArrowHover")<br />Seta de barra de rolagem ao focalizar  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ScrollBarArrowMouseOverBackground`<br />(Definido para a mesma cor de barra de rolagem). |
| Em primeiro plano (glifo) | `Environment.ScrollBarArrowGlyphMouseOver` |

**Seta da barra de rolagem: estado pressionado**  

![Seta de barra de rolagem pressionado](../../extensibility/ux-guidelines/media/0303-146_scrollbararrowpressed.png "0303 146_ScrollbarArrowPressed")<br />Pressionado seta da barra de rolagem

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ScrollBarArrowPressedBackground`<br />(Definido para a mesma cor de barra de rolagem). |
| Em primeiro plano (glifo) | `Environment.ScrollBarArrowGlyphPressed` |

### <a name="BKMK_SearchBoxes"></a>Caixas de pesquisa  
Sempre que possível, use o controle de pesquisa comum fornecido pelo ambiente do Visual Studio. Cores de caixa de pesquisa são encontradas na categoria "SearchControl" no **ShellColors.pkgdef** arquivo, que contém nomes de token para o campo de entrada, o botão de ação, o botão suspenso e o menu suspenso.  

Uma caixa de pesquisa pode ser um dos vários estados, algumas das quais são mutuamente exclusivas:  

-   "Concentradas" ou "sem foco" refere-se a ou não o cursor estiver na caixa de texto.  

-   "Active" ou "inativos" refere-se de se o usuário inseriu uma consulta de pesquisa na caixa de texto.  

-   "Passagem" significa que o usuário tem moused sobre a caixa de pesquisa com o mouse (esse estado substitui todos os outros estados).  

-   "Desabilitada" significa que a funcionalidade de pesquisa está desativada para o contexto atual.  

![Caixa de pesquisa (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-110_searchboxredline.png "0303 110_SearchBoxRedline")<br />Caixa de pesquisa (corte de funcionários)  

| Use... | Não use... |
| --- | --- |
| ... quando você estiver criando uma caixa de pesquisa personalizada. | ... para qualquer coisa que não seja uma caixa de pesquisa. |
| | ... para qualquer coisa que você não deseja sempre correspondem à pesquisa de caixa de interface do usuário. |

**Voltada para o campo de entrada de pesquisa**

![Campo de entrada de pesquisa restrita](../../extensibility/ux-guidelines/media/0303-111_searchinputfieldfocused.png "0303 111_SearchInputFieldFocused")<br />Voltada para o campo de entrada de pesquisa  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `SearchControl.FocusedBackground` |
| Em primeiro plano (texto) | `SearchControl.FocusedBackground` |
| Borda | `SearchControl.FocusedBorder` |
| Separador | `SearchControl.FocusedDropDownSeparator` |

**Campo de entrada de pesquisa sem foco, Active Directory**

![Campo de pesquisa sem foco](../../extensibility/ux-guidelines/media/0303-114_searchinputfieldunfocused.png "0303 114_SearchInputFieldUnfocused")<br />Campo de entrada de pesquisa sem foco, Active Directory

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `SearchControl.SearchActiveBackground` |
| Em primeiro plano (texto) | `SearchControl.SearchActiveBackground` |
| Borda | `SearchControl.UnfocusedBorder` |
| Separador | `SearchControl.DropDownSeparator` |

**Campo de entrada de pesquisa sem foco, inativo**

![Campo de entrada de pesquisa sem foco, inativa](../../extensibility/ux-guidelines/media/0303-114-1_searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")<br />Campo de entrada de pesquisa sem foco, inativo  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `SearchControl.Unfocused` |
| Em primeiro plano (texto) | `SearchControl.Unfocused` |
| Borda | `SearchControl.UnfocusedBorder` |
| Separador | `SearchControl.DropDownSeparator` |

**Campo de entrada de pesquisa realçado (texto)**

![Campo de entrada de pesquisa realçado](../../extensibility/ux-guidelines/media/0303-120_searchinputfieldhighlight.png "0303 120_SearchInputFieldHighlight")<br />Campo de entrada de pesquisa realçado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `SearchControl.Selection` |
| Em primeiro plano (texto) | `SearchControl.FocusedBackground` |
| Borda | Nenhum |
| Separador | `SearchControl.FocusedDropDownSeparator` |

**Campo de entrada de pesquisa desabilitado**

![Campo de entrada de pesquisar desabilitada](../../extensibility/ux-guidelines/media/0303-121_searchinputfielddisabled.png "0303 121_SearchInputFieldDisabled")<br />Campo de entrada de pesquisa desabilitado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `SearchControl.Disabled` |
| Em primeiro plano (texto) | `SearchControl.Disabled` |
| Borda | `SearchControl.DisabledBorder` |
| Separador | `SearchControl.DropDownSeparator` |

**Botão de ação de pesquisa restrita**

![Botão de ação de pesquisa com foco](../../extensibility/ux-guidelines/media/0303-112_searchactionbuttonfocused.png "0303 112_SearchActionButtonFocused")<br />Botão de ação de pesquisa restrita

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | Nenhum |
| Em primeiro plano (glifo de pesquisa) | `SearchControl.SearchGlyph` |
| Em primeiro plano (Stop glifo) | `SearchControl.StopGlyph` |
| Em primeiro plano (glifo não criptografado) | `SearchControl.ClearGlyph` |
| Borda | N/D |

**Botão de ação de pesquisa sem foco**  

![Botão de ação de pesquisa sem foco](../../extensibility/ux-guidelines/media/0303-115_searchactionbuttonunfocused.png "0303 115_SearchActionButtonUnfocused")<br />Botão de ação de pesquisa sem foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | N/D |
| Em primeiro plano (glifo de pesquisa) | `SearchControl.SearchGlyph` |
| Em primeiro plano (Stop glifo) | `SearchControl.StopGlyph` |
| Em primeiro plano (glifo não criptografado) | `SearchControl.ClearGlyph` |
| Borda | N/D |

**Pressionado o botão de ação de pesquisa**

![Botão de ação de pesquisa pressionado](../../extensibility/ux-guidelines/media/0303-116-1_searchactionbuttonpressed.png "0303-116-1_SearchActionButtonPressed")<br />Pressionado o botão de ação de pesquisa

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `SearchControl.ActionButtonMouseDown` |
| Em primeiro plano (glifo) | `SearchControl.ActionButtonMouseDownGlyph` |
| Borda | `SearchControl.ActionButtonMouseDownBorder` |

**Botão de ação de pesquisar desabilitada**

![Botão de ação de pesquisar desabilitada](../../extensibility/ux-guidelines/media/0303-122_searchactionbuttondisabled.png "0303 122_SearchActionButtonDisabled")<br />Botão de ação de pesquisar desabilitada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | Nenhum |
| Em primeiro plano (glifo) | `SearchControl.ActionButtonDisabledGlyph` |
| Borda | Nenhum |

**Botão suspenso de pesquisa restrita**

![Botão suspenso de pesquisa restrita](../../extensibility/ux-guidelines/media/0303-113_searchdropdownbuttonfocused.png "0303 113_SearchDropdownButtonFocused")<br />Botão suspenso de pesquisa restrita

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `SearchControl.FocusedDropDownButton` |
| Em primeiro plano (glifo) | `SearchControl.FocusedDropDownButtonGlyph` |
| Borda | `SearchControl.FocusedDropDownButtonBorder` |

**Botão de lista suspensa de pesquisa sem foco**

![Botão de lista suspensa de pesquisa sem foco](../../extensibility/ux-guidelines/media/0303-116_searchdropdownbuttonunfocused.png "0303 116_SearchDropdownButtonUnfocused")<br />Botão de lista suspensa de pesquisa sem foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `SearchControl.UnfocusedDropDownButton` |
| Em primeiro plano (glifo) | `SearchControl.UnfocusedDropDownButtonGlyph` |
| Borda | `SearchControl.UnfocusedDropDownButtonBorder` |

**Pressionado o botão de lista suspensa de pesquisa**

![Botão de lista suspensa de pesquisa pressionado](../../extensibility/ux-guidelines/media/0303-116-2_searchdropdownbuttonpressed.png "0303-116-2_SearchDropdownButtonPressed")<br />Pressionado o botão de lista suspensa de pesquisa

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `SearchControl.MouseDownDropDownButton` |
| Em primeiro plano (glifo) | `SearchControl.MouseDownDropDownButtonGlyph` |
| Borda | `SearchControl.MouseDownDropDownButtonBorder` |

**Botão suspenso de pesquisar desabilitada**

![Botão suspenso de pesquisar desabilitada](../../extensibility/ux-guidelines/media/0303-123_searchdropdownbuttondisabled.png "0303 123_SearchDropdownButtonDisabled")<br />Botão suspenso de pesquisar desabilitada

| Elemento | Nome do token: Category.color |
| --- | --- |  
| Informações preliminares | Nenhum |
| Em primeiro plano (glifo) | `SearchControl.DisabledDownButtonGlyph` |
| Borda | Nenhum |

#### <a name="search-drop-down-lists"></a>Listas suspensas de pesquisa  
O menu de lista suspensa de caixa de pesquisa tem o potencial para ser um pouco mais complexo do que outros menus suspensos no Visual Studio. As seções "opções de pesquisa" e "pesquisas sugeridas" podem aparecer sozinho ou em conjunto no menu, e cada uma delas é colorida separadamente. Uma linha também separa nessas duas seções quando aparecem juntos e uma borda ao redor de menu suspenso de inteiro.  

![Lista suspensa de pesquisa (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-124_searchdropdownredline.png "0303 124_SearchDropdownRedline")<br />Lista suspensa de pesquisa (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... quando você estiver criando uma lista suspensa de pesquisa personalizada. | ... em listas suspensas que aparecem em outros contextos. |
| ... os nomes de token corretos para os componentes da lista correta. | ... em qualquer combinação de plano de fundo/primeiro plano diferente do especificado. |

**Elementos de lista suspensa de pesquisa**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Borda | `SearchControl.PopupBorder` |
| Separador | `SearchControl.PopupSectionHeaderSeparator` |
| Sombra | `Environment.DropShadowBackground` |

**Sugerido pesquisas: estado padrão**

![Padrão de pesquisas sugeridas](../../extensibility/ux-guidelines/media/0303-125_searchsuggested.png "0303 125_SearchSuggested")<br />Padrão de pesquisas sugeridas  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `SearchControl.PopupItemsListBackgroundGradientBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `SearchControl.PopupItemText` |

**Sugerido pesquisas: passe o mouse de estado**

![Sugerido pesquisas ao focalizar](../../extensibility/ux-guidelines/media/0303-128_searchsuggestedhover.png "0303 128_SearchSuggestedHover")<br />Pesquisas sugeridas ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `SearchControl.PopupMouseOverItemText` |
| Borda | `SearchControl.PopupControlMouseOverBorder` |

**Opções de pesquisa: estado padrão**

![Caixa de seleção de pesquisa](../../extensibility/ux-guidelines/media/0303-126_searchcheckbox.png "0303 126_SearchCheckbox")<br />Opções de pesquisa padrão (caixa de seleção)  

![Opções de pesquisa](../../extensibility/ux-guidelines/media/0303-127_searchoptions.png "0303 127_SearchOptions")<br />Opções de pesquisa padrão (link)  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `SearchControl.PopupSectionBackgroundGradientBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (caixa de texto) | `SearchControl.PopupCheckboxText` |
| Em primeiro plano (texto do Link) | `SearchControl.PopupButtonText` |
| Plano de fundo do cabeçalho | `SearchControl.PopupSectionHeaderGradientBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto do cabeçalho) | `SearchControl.PopupSectionHeaderText` |

**Opções de pesquisa: passe o mouse de estado**

![Opções (caixa de seleção) de pesquisa ao focalizar](../../extensibility/ux-guidelines/media/0303-129_searchcheckboxhover.png "0303 129_SearchCheckboxHover")<br />Opções de pesquisa (caixa de seleção) ao focalizar  

![Opções (link) de pesquisa ao focalizar](../../extensibility/ux-guidelines/media/0303-130_searchoptionshover.png "0303 130_SearchOptionsHover")<br />Opções de pesquisa (link) ao focalizar  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (caixa de texto) | `SearchControl.PopupCheckboxMouseDownText` |
| Em primeiro plano (texto do Link) | `SearchControl.PopupButtonMouseDownText` |
| Borda | `SearchControl.PopupControlMouseOverBorder` |

**Opções de pesquisa: estado pressionado**  

![Pressionado (caixa de seleção) opções de pesquisa](../../extensibility/ux-guidelines/media/0303-131_searchsuggestedpressed.png "0303 131_SearchSuggestedPressed")<br />Pressionado opções de pesquisa (caixa de seleção)   

![Pressionado (link) opções de pesquisa](../../extensibility/ux-guidelines/media/0303-132_searchoptionspressed.png "0303 132_SearchOptionsPressed")<br />Pressionado opções de pesquisa (link)  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Plano de fundo da caixa de seleção | `SearchControl.PopupControlMouseDownBackgroundGradientBegin`<br />`SearchControl.PopupControlMouseDownBackgroundGradientEnd`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (caixa de texto) | `SearchControl.PopupCheckboxMouseDownText` |
| Plano de fundo do link | `SearchControl.PopupButtonMouseDownBackgroundGradientBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto do Link) | `SearchControl.PopupButtonMouseDownText` |

###  <a name="BKMK_TreeView"></a> Modos de exibição de árvore  
Várias janelas de ferramentas, incluindo o Gerenciador de soluções, Gerenciador de servidores e modo de exibição de classe, implementam um esquema de organizacional hierárquico cujas cores são controlados pelos nomes de cor no `TreeView` categoria. Todos os itens em uma exibição de árvore têm cores de plano de fundo e texto. Itens que tem elementos filho aninhados também têm glifos que indicam se o item é expandido ou recolhido.  

![Exibição de árvore (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-147_treeviewredline.png "0303 147_TreeViewRedline")<br />Exibição de árvore (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... em qualquer lugar, você precisará implementar uma exibição hierárquica de organizacional. | ... para qualquer coisa que não é semelhante a uma exibição de árvore. |
| | ... em qualquer combinação de plano de fundo/primeiro plano diferente do especificado. |

**Item de exibição de árvore: estado padrão**

![Item de exibição de árvore padrão](../../extensibility/ux-guidelines/media/0303-148_treeview.png "0303 148_TreeView")<br />Item de exibição de árvore padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `TreeView.Background` |
| Em primeiro plano (texto) | `TreeView.Background` |
| Em primeiro plano (glifo) | `TreeView.Glyph` |
| Borda | Nenhum |

**Item de exibição de árvore: passe o mouse de estado**

![Item de exibição de árvore ao focalizar](../../extensibility/ux-guidelines/media/0303-149_treeviewhover.png "0303 149_TreeViewHover")<br />Item de exibição de árvore ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `TreeView.Background` |  
| Em primeiro plano (texto) | `TreeView.Background` |
| Em primeiro plano (glifo) | `TreeView.GlyphMouseOver` |
| Borda | Nenhum |

**Item de exibição de árvore: arraste sobre estado**

![Árvore de item de exibição de arrastar sobre](../../extensibility/ux-guidelines/media/0303-150_treeviewdragover.png "0303 150_TreeViewDragOver")<br />Arraste o item de exibição de árvore em sobre  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `TreeView.DragOverItem` |
| Em primeiro plano (texto) | `TreeView.DragOverItem` |
| Em primeiro plano (glifo) | `TreeView.DragOverItemGlyph` |
| Borda | Nenhum |

**Item de exibição de árvore: selecionada, voltada para o estado**

![Selecionado e voltada para o item de exibição de árvore](../../extensibility/ux-guidelines/media/0303-151_treeviewfocused.png "0303 151_TreeViewFocused")<br />Item de exibição de árvore selecionado e focados

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `TreeView.SelectedItemActive` |
| Em primeiro plano (texto) | `TreeView.SelectedItemActive` |
| Em primeiro plano (glifo) | `TreeView.SelectedItemActiveGlyph` |
| Borda | `TreeView.FocusVisualBorder` |

**Item de exibição de árvore: estado selecionado, sem foco**  

![Item de exibição de árvore selecionado e sem foco](../../extensibility/ux-guidelines/media/0303-152_treeviewunfocused.png "0303 152_TreeViewUnfocused")<br />Item de exibição de árvore selecionado e sem foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `TreeView.SelectedItemInactive` |
| Em primeiro plano (texto) | `TreeView.SelectedItemInactive` |
| Em primeiro plano (glifo) | `TreeView.SelectedItemInactiveGlyph` |
| Borda | Nenhum |

**Item de exibição de árvore: focalizado, selecionados e voltada para o estado**

![Selecionado e voltada para o item de exibição de árvore ao focalizar](../../extensibility/ux-guidelines/media/0303-153_treeviewfocusedhover.png "0303 153_TreeViewFocusedHover")<br />Item de exibição de árvore selecionado e com foco em foco  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `TreeView.SelectedItemActive` |
| Em primeiro plano (texto) | `TreeView.SelectedItemActive` |
| Em primeiro plano (glifo) | `TreeView.SelectedItemActiveGlyphMouseOver` |
| Borda | `TreeView.FocusVisualBorder` |

**Item de exibição de árvore: estado focalizado, selecionado e sem foco**

![Item de exibição de árvore selecionado e sem foco ao passar](../../extensibility/ux-guidelines/media/0303-154_treeviewunfocusedhover.png "0303 154_TreeViewUnfocusedHover")<br />Item de exibição de árvore selecionado e sem foco ao focalizar  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `TreeView.SelectedItemInactive` |
| Em primeiro plano (texto) | `TreeView.SelectedItemInactive` |
| Em primeiro plano (glifo) | `TreeView.SelectedItemActiveGlyphMouseOver` |
| Borda | Nenhum |

## <a name="shell-appearance"></a>Aparência do shell

### <a name="background"></a>Informações preliminares  
O plano de fundo ambiente consiste em duas camadas. A camada inferior é uma cor sólida que abrange todo o IDE. A camada superior se encaixa em prateleira de comando e entre os canais de ocultar automaticamente janela ferramenta nas bordas esquerdas e direita do IDE. As camadas de plano de fundo superior e inferior são definidas para a mesma cor nos temas claro e escuro.  

![O plano de fundo do Visual Studio shell (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-187_shellbackgroundredline.png "0303 187_ShellBackgroundRedline")<br />O plano de fundo do Visual Studio shell (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... para lugares onde você deseja corresponder ao plano de fundo do ambiente do Visual Studio. | ... como um preenchimento de locais que não são as superfícies de plano de fundo. |
| | ... como um plano de fundo para colocar os elementos de primeiro plano no. |

**Aparência de shell de camada inferior**

| Elemento | Nome do token: Category.color |
| --- | --- |  
| Informações preliminares | `Environment.EnvironmentBackground` |

**Aparência do shell de camada superior**

> Conjunto com o mesmo valor de cor em temas claros de 2013 do Visual Studio e escuros marcas de gradiente.

| Elemento | Nome do token: Category.color |
| --- | --- |  
| Informações preliminares | `Environment.EnvironmentBackgroundGradientBegin`<br />`Environment.EnvironmentBackgroundGradientEnd`<br />`Environment.EnvironmentBackgroundGradientMiddle1`<br />`Environment.EnvironmentBackgroundGradientMiddle2` |  

### <a name="command-shelf"></a>Prateleira de comando  
Dois conjuntos de nomes de token são usados para os planos de fundo de prateleira do comando: um conjunto para onde fica a barra de menus e outro para onde as barras de comandos ficam. Um grupo de barra de comandos individuais tem seus próprios valores de cor do plano de fundo, que serão discutidos mais detalhadamente na seção "barra de comandos". Barra de menus de barra e comando texto é discutidos nas seções a barra menu e o comando, respectivamente.  

![Prateleira de comando do Visual Studio (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-188_commandshelfredline.png "0303 188_CommandShelfRedline")<br />Prateleira de comando do Visual Studio (corte de funcionários)  

| Use... | Não use... |
| --- | --- |
| ... para áreas onde você coloca menus ou barras de ferramentas. | ... para as áreas que não são semelhantes a uma prateleira de comando. |
|... com a combinação de nome de token correto em segundo plano/primeiro plano. | |

**Barra de menus de prateleira do comando**

> Conjunto com o mesmo valor de cor em temas claros de 2013 do Visual Studio e escuros marcas de gradiente.

| Elemento | Nome do token: Category.color |
| --- | --- |  
| Informações preliminares | `Environment.CommandShelfHighlightGradientBegin`<br /><br />`Environment.CommandShelfHighlightGradientMiddle`<br />`Environment.CommandShelfHighlightGradientEnd` |

* * Comando prateleira comando barra * *

> Conjunto com o mesmo valor de cor em temas claros de 2013 do Visual Studio e escuros marcas de gradiente.

| Elemento | Nome do token: Category.color |
| --- | --- |  
| Informações preliminares | `Environment.CommandShelfBackgroundGradientBegin`<br />`Environment.CommandShelfBackgroundGradientMiddle`<br />`Environment.CommandShelfBackgroundGradientEnd` |

## <a name="manifest-designer"></a>Designer de manifesto  
O Designer de manifesto foi projetado como uma maneira de tornar mais fácil de editar o arquivo de manifesto em projetos do Windows 8 e Windows Phone 8. Embora não haja nenhuma estrutura compartilhada disponíveis para consumo, pode ser apropriado para a correspondência entre as cores da estrutura geral e guias de navegação/orientação e o layout de design. Para obter mais informações sobre os detalhes de layout, consulte [Layout para o Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md).  

![Designer de manifesto (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-175_manifestdesignerredline.png "0303 175_ManifestDesignerRedline")<br />Designer de manifesto (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... para designers que são semelhantes para o Designer de manifesto. | ... Se você tiver mais de seis guias. |
| ... em vez de usar controles de guia comum na parte superior de um editor dentro do documento bem. | ... para qualquer interface do usuário estruturados, como o Designer de manifesto. |

**Guia manifesto de Designer selecionado: estado padrão**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `ManifestDesigner.TabActive` |
| Borda | Nenhum |

**Painel de descrição selecionado Designer manifesto: estado padrão**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `ManifestDesigner.DescriptionPane` |

**Página de conteúdo selecionada manifesto do Designer: estado padrão**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `ManifestDesigner.Background` |
| Texto do auxiliar de diálogo | `ManifestDesigner.WatermarkText`<br />(Esse nome do token não corresponde a sua função.) |

**Guia de Designer de manifesto: cancelou a seleção de estado**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `ManifestDesigner.Tab.Inactive` |

**Guia de Designer de manifesto: passe o mouse de estado**

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `ManifestDesigner.Tab.Mouseover` |

## <a name="command-structures"></a>Estruturas de comando  

###  <a name="BKMK_CommandMenus"></a> Menus  
Menus podem ocorrer em vários locais dentro do Visual Studio: barra de menu principal, inserida no documento ou a ferramenta windows ou no botão direito do mouse em vários locais em todo o IDE. Implementações de menus associados com outros elementos de interface do usuário são discutidas na seção do elemento do respectivo. Você sempre deve usar a implementação de menu padrão fornecida pelo ambiente do Visual Studio. No entanto, em alguns casos raros talvez você não tenha acesso aos menus padrão do Visual Studio. Nessas situações, use os seguintes nomes de token para garantir que sua interface do usuário seja consistente com outros menus no Visual Studio.  

![Menu do Visual Studio (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-000_menuredline.png "0303 000_MenuRedline")<br />Menu do Visual Studio (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... quando você precisa criar um menu personalizado.| ... a cor de plano de fundo sozinha. Sempre use a combinação de plano de fundo/primeiro plano conforme especificado. |
| ... quando você tem um novo componente de interface do usuário que você deseja correspondência com os menus do Visual Studio.| |

#### <a name="menu-titles"></a>Títulos de menus  
Títulos de menus consistem em um plano de fundo, uma borda e o texto do título, bem como um glifo opcional, normalmente, quando o menu é encontrado em uma barra de comandos.  

![Título de menu (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-001_menutitleredline.png "0303 001_MenuTitleRedline")<br />Título de menu (corte de funcionários)  

| Use... | Não use... |
| --- | --- |
| ... sempre que você está criando um título de menu personalizado. | ... para qualquer coisa que você não deseja sempre corresponde ao título de menu. |
| | ... em qualquer combinação de plano de fundo/primeiro plano diferente do especificado. |

**Título de menu: estado padrão**

![Padrão de título de menu](../../extensibility/ux-guidelines/media/0303-002_menutitledefault.png "0303 002_MenuTitleDefault")<br />Título de menu padrão

![Padrão de título de menu com o glifo](../../extensibility/ux-guidelines/media/0303-003_menutitlewithglyphdefault.png "0303 003_MenuTitleWithGlyphDefault")<br />Título de menu padrão com o glifo

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | Nenhum |
| Em primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Em primeiro plano (glifo) | `Environment.CommandBarMenuGlyph` |
| Borda | Nenhum |

**Título de menu: passe o mouse de estado**  

![Título de menu ao focalizar](../../extensibility/ux-guidelines/media/0303-004_menutitlehover.png "0303 004_MenuTitleHover")<br />Título de menu ao focalizar  

![Título de menu com o glifo focalizar](../../extensibility/ux-guidelines/media/0303-005_menutitlewithglyphhover.png "0303 005_MenuTitleWithGlyphHover")<br />Título de menu com o glifo ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.CommandBarMouseOverBackgroundBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.CommandBarTextHover` |
| Em primeiro plano (glifo) | `Environment.CommandBarMenuMouseOverGlyph` |  
| Borda | `Environment.CommandBarBorder` |

**Título de menu: estado pressionado**  

![Pressionado o título de menu](../../extensibility/ux-guidelines/media/0303-006_menutitlepressed.png "0303 006_MenuTitlePressed")<br />Título de menu pressionado

![Pressionado o título de menu com o glifo](../../extensibility/ux-guidelines/media/0303-007_menutitlewithglyphpressed.png "0303 007_MenuTitleWithGlyphPressed")<br />Título de menu com o glifo de pressionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.CommandBarMenuBackgroundGradientBegin`<br/>(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Em primeiro plano (glifo) | `Environment.CommandBarMenuMouseDownGlyph` |
| Borda | `Environment.CommandBarMenuBorder`<br />(Somente à esquerda, superior e à direita.) |  

**Título de menu: estado desabilitado**  

![Desabilitado o título de menu com o glifo](../../extensibility/ux-guidelines/media/0303-008_menutitlewithglyphdisabled.png "0303 008_MenuTitleWithGlyphDisabled")<br />Título de menu desabilitados com o glifo

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | Nenhum |
| Em primeiro plano (texto) | `Environment.CommandBarTextInactive` |
| Em primeiro plano (glifo) | `Environment.CommandBarTextInactive` |
| Borda | Nenhum |

#### <a name="menu-items"></a>Itens de menu
Um item de menu individuais consiste o texto do menu e um ícone opcional, a caixa de seleção ou o glifo de submenu. Sua alteração de cor do plano de fundo e texto em foco. Esse token de cor é um par de plano de fundo/primeiro plano.  

![Corte de funcionários em itens de menu](../../extensibility/ux-guidelines/media/0303-009_menuitemredline.png "0303 009_MenuItemRedline")  

| Use... | Não use... |
|---|---|
| ... para qualquer lista suspensa que é iniciado de uma barra de menu ou barra de comandos. | ... por qualquer lista suspensa em outro contexto. |
| | ... em qualquer combinação de plano de fundo/primeiro plano diferente do especificado. |

**Itens de menu: estado padrão**

![Itens de menu padrão](../../extensibility/ux-guidelines/media/0303-010_menudefault.png "0303 010_MenuDefault")<br />Itens de menu padrão  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.CommandBarMenuBackgroundGradientBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Em primeiro plano (glifo de Submenu) | `Environment.CommandBarMenuSubmenuGlyph` |
| Borda | `Environment.CommandBarMenuBorder` |
| O plano de fundo do ícone canal | `Environment.CommandBarMenuIconBackground` |
| Separador | `Environment.CommandBarMenuSeparator` |
| Sombra | `Environment.DropShadowBackground` |

**Itens de menu: marcado e selecionado Estados**  

![Menu marcada](../../extensibility/ux-guidelines/media/0303-011_menuchecked.png "0303 011_MenuChecked")<br />Item de menu selecionado

![Menu selecionado](../../extensibility/ux-guidelines/media/0303-012_menuselected.png "0303 012_MenuSelected")<br />Item de menu selecionado    

| Elemento | Nome do token: Category.color |
| --- | --- |
| Marca de seleção | `Environment.CommandBarCheckBox` |  
| Plano de fundo de marca de seleção | `Environment.CommandBarSelectedIcon` |  
| Plano de fundo do ícone | `Environment.CommandBarSelected` |
| Borda de ícone | `Environment.CommandBarSelectedBorder` |

**Itens de menu: passe o mouse de estado**  

![Passe o mouse menu](../../extensibility/ux-guidelines/media/0303-013_menuhover.png "0303 013_MenuHover")<br />Item de menu ao focalizar

![Em foco o menu marcado](../../extensibility/ux-guidelines/media/0303-014_menuhoverchecked.png "0303 014_MenuHoverChecked")<br />Verificado o item de menu ao focalizar

![Passe o mouse menu selecionado](../../extensibility/ux-guidelines/media/0303-015_menuhoverselected.png "0303 015_MenuHoverSelected")<br />Item de menu selecionado ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.CommandBarMenuItemMouseOver` |
| Em primeiro plano (texto) | `Environment.CommandBarMenuItemMouseOver` |
| Em primeiro plano (glifo de Submenu) | `Environment.CommandBarMenuMouseOverSubmenuGlyph` |
| Marca de seleção | `Environment.CommandBarCheckBoxMouseOver` |
| Plano de fundo de marca de seleção | `Environment.CommandBarHoverOverSelectedIcon` |
| Plano de fundo do ícone | `Environment.CommandBarHoverOverSelected` |
| Borda de ícone | `Environment.CommandBarHoverOverSelectedIconBorder` |

**Itens de menu: estado desabilitado**  

![Menu desabilitado](../../extensibility/ux-guidelines/media/0303-016_menudisabled.png "0303 016_MenuDisabled")<br />Item de menu desabilitado

![Menu desabilitado marcada](../../extensibility/ux-guidelines/media/0303-017_menudisabledchecked.png "0303 017_MenuDisabledChecked")<br />Item de menu desabilitado com marca de seleção

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em primeiro plano (texto) | `Environment.CommandBarTextInactive` |
| Em primeiro plano (glifo de Submenu) | `Environment.CommandBarMenuSubmenuGlyph` |
| Marca de seleção | `Environment.CommandBarCheckBoxDisabled` |
| Plano de fundo de marca de seleção | `Environment.CommandBarSelectedIconDisabled` |

### <a name="command-bars"></a>Barras de comando  
Uma barra de comandos pode aparecer em vários lugares dentro do IDE do Visual Studio, mais notavelmente comando comercial e inseridos na ferramenta ou janelas de documento.  

Em geral, sempre use a implementação da barra de comando padrão fornecida pelo ambiente do Visual Studio. Usando o mecanismo padrão garante que todos os detalhes visuais sejam exibidos corretamente e que elementos interativos, será se comportam de maneira consistente com outros controles de barra de comando do Visual Studio. No entanto, se for necessário para você criar sua própria barra de comandos, verifique se que você definir o estilo corretamente usando os seguintes nomes de token.  

![Corte de funcionários da barra de comandos](../../extensibility/ux-guidelines/media/0303-018_commandbarredline.png "0303 018_CommandBarRedline")<br />Barra de comandos (corte de funcionários)  

![Aplicar linhas vermelhas no botão de estouro](../../extensibility/ux-guidelines/media/0303-019_overflowbuttonredline.png "0303 019_OverflowButtonRedline")<br />Botão de estouro (corte de funcionários)  

| Use... | Não use... |
| --- | --- |
| ... em lugares onde você precisa de uma barra de comandos inseridos, mas são não é possível usar a implementação padrão de barra de comando Visual Studio. | ... para elementos de interface do usuário que não são semelhantes a uma barra de comandos. |
| | ... para componentes de barra de comando que não sejam aqueles para os quais nomes de token são especificados. |

#### <a name="command-bar-groups"></a>Grupos de barra de comando  
Um grupo de barra de comandos consiste em um conjunto de controles de barra de comandos relacionados e pode conter qualquer número de botões, dividir os menus suspensos, botões, caixas de combinação ou menus. Cores para esses controles são governadas por nomes de token separados e são discutidas individualmente em outro lugar neste guia. Uma linha separadora é usada para dividir um grupo de barra de comandos em subgrupos relacionados.  

![Aplicar linhas vermelhas no grupo de barra de comandos](../../extensibility/ux-guidelines/media/0303-020_commandbargroupredline.png "0303 020_CommandBarGroupRedline")<br />Grupo de barra de comandos (corte de funcionários)

| Use... | Não use... |
| --- | --- |  
| ... em lugares onde você precisa de uma barra de comandos inseridos, mas são não é possível usar a implementação padrão de barra de comando Visual Studio. | ... para elementos de interface do usuário que não são semelhantes a uma barra de comandos. |
| | ... para componentes de barra de comando que não sejam aqueles para os quais nomes de token são especificados. |

**Grupo de barra de comandos: estado padrão**  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.CommandBarGradientBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Borda | `Environment.CommandBarToolBarBorder` |
| Arraste a alça | `Environment.CommandBarDragHandle` |
| Separador | `Environment.CommandBarToolBarSeparator`<br />`Environment.CommandBarToolBarSeparatorHighlight` |

#### <a name="command-icons"></a>Ícones de comando  
![Aplicar linhas vermelhas no ícone do comando](../../extensibility/ux-guidelines/media/0303-021_commandiconredline1.png "0303 021_CommandIconRedline1")<br />Ícone do comando (corte de funcionários)  

![Aplicar linhas vermelhas no ícone do comando com texto](../../extensibility/ux-guidelines/media/0303-022_commandiconredline2.png "0303 022_CommandIconRedline2")<br />Ícone do comando com o texto (corte de funcionários)  

| Use... | Não use... |
| --- | --- |
| ... para quaisquer botões que serão colocadas em uma barra de comandos. | ... para controles que têm seus próprios nomes de token. |
| | ... em qualquer combinação de plano de fundo/primeiro plano diferente do especificado. |

**Ícone do comando: estado padrão**  

![Comando padrão do ícone](../../extensibility/ux-guidelines/media/0303-023_commandicondefault.png "0303 023_CommandIconDefault")<br />Ícone do comando padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | N/d (herda de fundo da barra de comando) |
| Em primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Borda | N/D |

**Ícone do comando: padrão de estado, selecionado**

![Padrão, o ícone do comando selecionado](../../extensibility/ux-guidelines/media/0303-024_commandicondefaultselected.png "0303 024_CommandIconDefaultSelected")<br />Padrão, o ícone do comando selecionado  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.CommandBarSelected` |
| Em primeiro plano (texto) | `Environment.CommandBarTextSelected` |
| Borda | `Environment.CommandBarSelectedBorder` |

**Ícone do comando: Estados de focalização ou o foco**  

![Ícone do comando em foco ou de focalização](../../extensibility/ux-guidelines/media/0303-025_commandiconhover.png "0303 025_CommandIconHover")<br />Ícone do comando em foco ou passe o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.CommandBarMouseOverBackgroundBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.CommandBarTextHover` |
| Borda | `Environment.CommandBarBorder` |

**Ícone do comando: Estados de focalização ou o foco, selecionados**

![Selecionado o ícone do comando em foco ou passe o mouse](../../extensibility/ux-guidelines/media/0303-026_commandiconhoverselected.png "0303 026_CommandIconHoverSelected")<br />Ícone do comando selecionado no foco ou passe o mouse

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.CommandBarHoverOverSelected` |
| Em primeiro plano (texto) | `Environment.CommandBarTextHoverOverSelected` |
| Borda | `Environment.CommandBarHoverOverSelectedIconBorder` |

 **Ícone do comando: estado pressionado**  

![Pressionado o ícone do comando](../../extensibility/ux-guidelines/media/0303-027_commandiconpressed.png "0303 027_CommandIconPressed")<br />Ícone do comando pressionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.CommandBarMouseDownBackgroundBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.CommandBarTextMouseDown` |
| Borda | `Environment.CommandBarBorder` |

**Ícone do comando: estado desabilitado**  

![Ícone do comando desabilitado](../../extensibility/ux-guidelines/media/0303-028_commandicondisabled.png "0303 028_CommandIconDisabled")<br />Ícone do comando desabilitado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | N/d (herda de fundo da barra de comando) |
| Em primeiro plano (texto) | `Environment.CommandBarTextInactive` |
| Borda | N/D |

####  <a name="BKMK_CommandComboBox"></a> Caixas de combinação de barra de comando

> [!IMPORTANT]
> Caixas de combinação são semelhantes às listas suspensas, mas incluam uma região de texto editável. Se sua lista suspensa não incluir uma região editável de texto, use os tokens de cor para [menus suspensos de barra de comandos](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandDropDown).  

![Aplicar linhas vermelhas no comando barra da caixa de combinação](../../extensibility/ux-guidelines/media/0303-029_comboboxredline.png "0303 029_ComboBoxRedline")<br />Caixa de combinação de barra de comando (corte de funcionários)  

| Use... | Não use... |
| --- | --- |
| ... ao criar caixas de combinação personalizada. | ... para qualquer coisa que você não deseja sempre coincidir com o comando da barra da interface do usuário. |
| ... ao criar um controle de barra de comando é semelhante a uma caixa de combinação. | ... quando você tem acesso a uma caixa de combinação com estilo. |

**Campo de caixa de combinação barra de comando entrada: estado padrão**

![Campo de caixa de combinação entrada barra comando](../../extensibility/ux-guidelines/media/0303-030_comboboxinputfield.png "0303 030_ComboBoxInputField")<br />Campo de caixa de combinação barra de comando entrada  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ComboBoxBackground` |
| Em primeiro plano (texto) | `Environment.ComboBoxText` |
| Borda | `Environment.ComboBoxBorder` |
| Separador | Nenhum separador |

**Botão de lista suspensa da barra de comandos: estado padrão**  

![Soltar da caixa de combinação&#45;botão pressionado](../../extensibility/ux-guidelines/media/0303-031_comboboxdropdownbutton.png "0303 031_ComboBoxDropdownButton")<br />Botão de lista suspensa da barra de comandos

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | N/d (herda de fundo da barra de comando) |
| Em primeiro plano (glifo) | `Environment.ComboBoxGlyph` |

**Lista de lista suspensa de barra de comandos: estado padrão**

![Lista de lista suspensa de barra de comandos](../../extensibility/ux-guidelines/media/0303-032_comboboxdropdownlist.png "0303 032_ComboBoxDropdownList")<br />Lista de lista suspensa de barra de comandos

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ComboBoxPopupBackgroundBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.ComboBoxItemText` |
| Borda | `Environment.ComboBoxPopupBorder` |

**Campo de caixa de combinação barra de comando entrada: passe o mouse de estado**  

![Comando barra combinação caixa campo de entrada ao focalizar](../../extensibility/ux-guidelines/media/0303-033_comboboxinputfieldhover.png "0303 033_ComboBoxInputFieldHover")<br />Comando barra combinação caixa campo de entrada ao focalizar  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ComboBoxMouseOverBackgroundBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.ComboBoxMouseOverText` |
| Borda | `Environment.ComboBoxMouseOverBorder` |
| Separador | `Environment.ComboBoxMouseOverSeparator` |

 **Botão de lista suspensa da barra de comandos: passe o mouse de estado**  

![Botão de lista suspensa de barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-034_comboboxdropdownbuttonhover.png "0303 034_ComboBoxDropdownButtonHover")<br />Botão de lista suspensa de barra de comandos ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ComboBoxButtonMouseOverBackground` |
| Em primeiro plano (glifo) | `Environment.ComboBoxMouseOverGlyph` |

**Lista de lista suspensa de barra de comandos: passe o mouse de estado**

 ![Lista de lista suspensa de barra de comando ao focalizar](../../extensibility/ux-guidelines/media/0303-035_comboboxdropdownlisthover.png "0303 035_ComboBoxDropdownListHover")<br />Lista de lista suspensa de barra de comando ao focalizar  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em segundo plano (item de Menu) | `Environment.ComboBoxItemMouseOverBackground` |
| Em primeiro plano (texto) | `Environment.ComboBoxItemMouseOverText` |
| Borda (item de Menu) | `Environment.ComboBoxItemMouseOverBorder` |

 **Campo de caixa de combinação barra de comando entrada: voltada para o estado**  

![Voltada para o campo de entrada de caixa de combinação da barra de comandos](../../extensibility/ux-guidelines/media/0303-036_comboboxinputfieldfocused.png "0303 036_ComboBoxInputFieldFocused")<br />Voltada para o campo de caixa de combinação barra de comando entrada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ComboBoxFocusedBackground` |
| Em primeiro plano (texto) | `Environment.ComboBoxFocusedText` |
| Borda | `Environment.ComboBoxFocusedBorder` |
| Separador | `Environment.ComboBoxFocusedButtonSeparator` |

**Botão de lista suspensa da barra de comandos: voltada para o estado**  

![Voltada para o botão suspenso da barra de comandos](../../extensibility/ux-guidelines/media/0303-037_comboboxdropdownbuttonfocused.png "0303 037_ComboBoxDropdownButtonFocused")<br />Comando focalizado botão suspenso da barra

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ComboBoxFocusedButtonBackground` |
| Em primeiro plano (glifo) | `Environment.ComboBoxFocusedGlyph` |

 **Campo de caixa de combinação barra de comando entrada: estado pressionado**  

![Pressionado comando barra campo de entrada de caixa de combinação](../../extensibility/ux-guidelines/media/0303-038_comboboxinputfieldpressed.png "0303 038_ComboBoxInputFieldPressed")<br />Campo de caixa de combinação barra de comando entrada de pressionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ComboBoxMouseDownBackground` |
| Em primeiro plano (texto) | `Environment.ComboBoxMouseDownText` |
| Borda | `Environment.ComboBoxMouseDownBorder` |
| Separador | `Environment.ComboBoxMouseDownSeparator` |

**Botão de lista suspensa da barra de comandos: estado pressionado**

![Pressionado o botão suspenso da barra de comandos](../../extensibility/ux-guidelines/media/0303-039_comboboxdropdownbuttonpressed.png "0303 039_ComboBoxDropdownButtonPressed")<br />Pressionado o botão suspenso da barra de comandos  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ComboBoxButtonMouseDownBackground` |
| Em primeiro plano (glifo) | `Environment.ComboBoxMouseDownGlyph` |

**Campo de caixa de combinação barra de comando entrada: estado desabilitado**  

![Desabilitado o campo de entrada de caixa de combinação da barra de comandos](../../extensibility/ux-guidelines/media/0303-041_comboboxinputfielddisabled.png "0303 041_ComboBoxInputFieldDisabled")<br />Barra de campo de entrada de caixa de combinação, os comandos desabilitados  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ComboBoxDisabledBackground` |
| Em primeiro plano (texto) | `Environment.ComboBoxDisabledText` |
| Borda | `Environment.ComboBoxDisabledBorder` |
| Separador | Nenhum separador |

**Botão de lista suspensa da barra de comandos: estado desabilitado**  

![Desabilitado o botão suspenso da barra de comandos](../../extensibility/ux-guidelines/media/0303-040_comboboxdropdownbuttondisabled.png "0303 040_ComboBoxDropdownButtonDisabled")<br />Comando desabilitado o botão de lista suspensa da barra

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | Nenhum |
| Em primeiro plano (glifo) | `Environment.ComboBoxDisabledGlyph` |

####  <a name="BKMK_CommandDropDown"></a> Comando barra menus suspensos

> [!IMPORTANT]
>  Menus suspensos são semelhantes às caixas de combinação, mas não têm regiões de texto editável. Se o menu suspenso inclui uma região de texto editável, use os tokens de cor para [caixas de combinação de barra de comandos](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandComboBox).  

![Lista suspensa da barra de comandos (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-042_dropdownredline.png "0303 042_DropdownRedline")<br />Lista suspensa da barra de comandos (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... quando você estiver criando controles personalizados na lista suspensa. | ... para qualquer coisa que não é semelhante a uma lista suspensa. |
| | ... para caixas de combinação ou botões de divisão. |   

**Campo de seleção de lista suspensa de barra de comando: estado padrão**  

![Padrão de campo de seleção de lista suspensa da barra de comandos](../../extensibility/ux-guidelines/media/0303-043_dropdownselectionfield.png "0303 043_DropdownSelectionField")<br />Campo de seleção de lista suspensa de barra de comando padrão  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.DropDownBackground` |
| Em primeiro plano (texto) | `DropDownText` |
| Borda | `DropDownBorder` |
| Separador | Nenhum separador |

**Botão de lista suspensa da barra de comandos: estado padrão**

![Padrão do botão suspenso da barra de comandos](../../extensibility/ux-guidelines/media/0303-044_dropdownbutton.png "0303 044_DropdownButton")<br />Botão de lista suspensa de barra de comandos padrão  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | Nenhum |
| Em primeiro plano (glifo) | `Environment.DropDownGlyph` |

**Lista de lista suspensa de barra de comandos: estado padrão**

![Padrão de lista suspensa da barra de comandos](../../extensibility/ux-guidelines/media/0303-045_dropdownlist.png "0303 045_DropdownList")<br />Lista de lista suspensa de barra de comandos padrão  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.DropDownPopupBackgroundBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.ComboBoxItemText` |
| Borda | `Environment.DropDownPopupBorder` |
| Sombra | `Environment.DropShadowBackground` |

**Campo de seleção de lista suspensa de barra de comando: passe o mouse de estado**  

![Campo de seleção de lista suspensa de barra de comando ao focalizar](../../extensibility/ux-guidelines/media/0303-046_dropdownselectionfieldhover.png "0303 046_DropdownSelectionFieldHover")<br />Campo de seleção de lista suspensa de barra de comando ao focalizar  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.DropDownMouseOverBackgroundBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.DropDownMouseOverText` |
| Borda | `Environment.DropDownMouseOverBorder` |
| Separador | `Environment.DropDownButtonMouseOverSeparator` |

**Botão de lista suspensa da barra de comandos: passe o mouse de estado**  

![Botão de lista suspensa de barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-047_dropdownbuttonhover.png "0303 047_DropdownButtonHover")<br />Botão de lista suspensa de barra de comandos ao focalizar  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.DropDownButtonMouseOverBackground` |
| Em primeiro plano (glifo) | `Environment.DropDownMouseOverGlyph` |

**Lista de lista suspensa de barra de comandos: passe o mouse de estado**  

![Lista de lista suspensa de barra de comando ao focalizar](../../extensibility/ux-guidelines/media/0303-048_dropdownlisthover.png "0303 048_DropdownListHover")<br />Lista de lista suspensa de barra de comando ao focalizar  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em segundo plano (item de Menu) | `Environment.ComboBoxItemMouseOverBackground` |
| Em primeiro plano (texto) | `Environment.ComboBoxItemMouseOverText` |
| Borda (item de Menu) | `Environment.ComboBoxItemMouseOverBorder` |

 **Campo de seleção de lista suspensa de barra de comando: estado pressionado**  

![Remova&#45;para baixo de campo de seleção pressionado](../../extensibility/ux-guidelines/media/0303-049_dropdownselectionfieldpressed.png "0303 049_DropdownSelectionFieldPressed")<br />Pressionado comando campo de seleção de lista suspensa da barra

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.DropDownMouseDownBackground` |
| Em primeiro plano (texto) | `Environment.DropDownMouseDownText` |
| Borda | `Environment.DropDownMouseDownBorder` |
| Separador | `Environment.DropDownButtonMouseDownSeparator` |

**Botão de lista suspensa da barra de comandos: estado pressionado**

![Pressionado o botão suspenso da barra de comandos](../../extensibility/ux-guidelines/media/0303-050_dropdownbuttonpressed.png "0303 050_DropdownButtonPressed")<br />Pressionado o botão suspenso da barra de comandos  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.DropDownButtonMouseDownBackground` |
| Em primeiro plano (glifo) | `Environment.DropDownMouseDownGlyph` |

**Campo de seleção de lista suspensa de barra de comando: estado desabilitado**  

![Desabilitado o campo de seleção de lista suspensa da barra de comandos](../../extensibility/ux-guidelines/media/0303-051_dropdownselectionfielddisabled.png "0303 051_DropdownSelectionFieldDisabled")<br />Comando desabilitado o campo de seleção suspensa da barra

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.DropDownDisabledBackground` |
| Em primeiro plano (texto) | `Environment.DropDownDisabledText` |
| Borda | `Environment.DropDownDisabledBorder` |
| Separador | Nenhum separador |

**Botão de lista suspensa da barra de comandos: estado desabilitado**

![Desabilitado o botão suspenso da barra de comandos](../../extensibility/ux-guidelines/media/0303-052_dropdownbuttondisabled.png "0303 052_DropdownButtonDisabled")<br />Comando desabilitado o botão de lista suspensa da barra

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | N/D |
| Em primeiro plano (glifo) | `Environment.DropDownDisabledGlyph` |

#### <a name="command-bar-split-buttons"></a>Barra de comandos dividir botões
Botões de divisão compartilham muitos nomes de token com outros controles de barra de comando, como botões, menus e texto da barra de comando. Todas as ações necessárias e nomes de token do botão suspenso são repetidos aqui para sua conveniência. Listas de lista suspensa do botão de divisão são implementações de [menus de barra de comandos](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandMenus).  

![Aplicar linhas vermelhas no botão de divisão](../../extensibility/ux-guidelines/media/0303-053_splitbuttonredline.png "0303 053_SplitButtonRedline")<br />Botão de divisão de barra de comandos (corte de funcionários)  

| Use... | Não use... |
| --- | --- |
| ... quando você estiver criando um botão de divisão personalizado. | ... para outros tipos de botões. |
| | ... em qualquer combinação de plano de fundo/primeiro plano diferente do especificado. |

**Botão de divisão de barra de comandos: estado padrão**  

![Padrão do botão de divisão de barra de comando](../../extensibility/ux-guidelines/media/0303-054_splitbutton.png "0303 054_SplitButton")<br />Botão de divisão de barra de comandos padrão  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | Nenhum |
| Em primeiro plano (texto) | `Environment.CommandBarTextActive` |
| Em primeiro plano (glifo) | `Environment.CommandBarSplitButtonGlyph` |
| Borda | N/D |
| Separador | N/D |

**Botão de divisão de barra de comandos: passe o mouse de estado**  

![Botão ao passar de divisão de barra de comandos](../../extensibility/ux-guidelines/media/0303-055_splitbuttonhover.png "0303 055_SplitButtonHover")<br />Botão ao passar de divisão de barra de comandos

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.CommandBarMouseOverBackgroundBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.CommandBarTextHover` |
| Em primeiro plano (glifo) | `Environment.CommandBarSplitButtonMouseOverGlyph` |
| Borda | `Environment.CommandBarBorder` |
| Separador | `Environment.CommandBarSplitButtonSeparator` |

**Botão de divisão de barra de comandos: estado pressionado**  

![Pressionado o botão de divisão de barra de comando](../../extensibility/ux-guidelines/media/0303-056_splitbuttonpressed.png "0303 056_SplitButtonPressed")<br />Barra de comandos pressionado o botão de divisão  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.CommandBarMouseDownBackgroundBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.CommandBarTextMouseDown` |
| Em primeiro plano (glifo) | `Environment.CommandBarSplitButtonMouseDownGlyph` |
| Borda | `Environment.CommandBarBorder` |
| Separador | N/D |

**Botão de divisão de barra de comandos: estado desabilitado**

![Desabilitado o botão de divisão de barra de comando](../../extensibility/ux-guidelines/media/0303-057_splitbuttondisabled.png "0303 057_SplitButtonDisabled")<br />Botão de divisão de barra de comandos desabilitada

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | N/D |
| Em primeiro plano (texto) | `Environment.ComboBoxItemTextInactive` |
| Em primeiro plano (glifo) | `Environment.CommandBarTextInactive` |
| Borda | N/D |
| Separador | N/D |

#### <a name="command-bar-more-options-and-overflow-buttons"></a>Botões de comando da barra 'Mais opções' e 'Overflow'  
O botão "Mais opções" é usado quando um grupo de barra de comandos é personalizável pelo adicionando ou removendo os botões da barra de comando relacionado. O botão de "Estouro" aparece quando uma barra de comandos é truncada devido à falta de espaço horizontal e clique mostra um menu que contém os botões da barra de comando que não podem ser exibidos. Cores desses dois botões são controladas pelo mesmo conjunto de nomes de token.  

![Comando barra botão 'Mais opções' (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-058_moreoptionsredline.png "0303 058_MoreOptionsRedline")<br />Comando barra botão 'Mais opções' (corte de funcionários)  

| Use... | Não use... |
| --- | --- |
| ... para personalizado 'mais opções' ou 'Overflow' botões. | ... para botões que não têm uma funcionalidade semelhante a um 'Mais opções' ou o botão de 'estouro de '. |

**'Mais opções' e 'Overflow' botões de barra de comandos: estado padrão**  

![Padrão do botão 'Mais opções' da barra de comandos](../../extensibility/ux-guidelines/media/0303-059_moreoptions.png "0303 059_MoreOptions")<br />Barra de comandos 'Mais opções' botão padrão

![Padrão de 'Overflow' botão da barra de comandos](../../extensibility/ux-guidelines/media/0303-060_overflow.png "0303 060_Overflow")<br />'Overflow' botão de barra de comandos padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.CommandBarOptionsBackground` |
| Em primeiro plano (glifo) | `Environment.CommandBarOptionsGlyph` |

**'Mais opções' e 'Overflow' botões de barra de comandos: passe o mouse de estado**

![Comando botão 'Mais opções' no foco da barra](../../extensibility/ux-guidelines/media/0303-061_moreoptionshover.png "0303 061_MoreOptionsHover")<br />Botão 'Mais opções' no foco da barra de comandos  

![Botão de 'Overflow' de barra de comandos ao focalizar](../../extensibility/ux-guidelines/media/0303-062_overflowoptions.png "0303 062_OverflowOptions")<br />Botão de 'Overflow' de barra de comandos ao focalizar   

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.CommandBarOptionsMouseOverBackgroundBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (glifo) | `Environment.CommandBarOptionsMouseDownGlyph` |

**'Mais opções' e 'Overflow' botões de barra de comandos: estado pressionado**  

![Pressionado o botão 'Mais opções' da barra de comandos](../../extensibility/ux-guidelines/media/0303-063_moreoptionspressed.png "0303 063_MoreOptionsPressed")<br />Pressionado o botão 'Mais opções' da barra de comandos  

![Estouro pressionado](../../extensibility/ux-guidelines/media/0303-064_overflowpressed.png "0303 064_OverflowPressed")<br />Pressionado o botão da barra de comando 'Overflow'  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.CommandBarOptionsMouseDownBackgroundBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (glifo) | `Environment.CommandBarOptionsMouseDownGlyph` |

## <a name="document-windows"></a>Janelas de documento  
Não é necessário para replicar as janelas de documento, pois elas são fornecidas pelo ambiente do Visual Studio. No entanto, você pode decidir o que você deseja aproveitar as cores usadas em janelas de documento para que sua interface do usuário apareça sempre consistente com essa parte do ambiente do Visual Studio.  

Ao usar tokens de cor de janela de documento, tenha cuidado para usá-los somente para elementos semelhantes e sempre em pares. Se você não fizer isso, você pode obter resultados inesperados em sua interface do usuário.  

### <a name="document-window-frames"></a>Quadros de janela de documento  
Janelas de documento podem ser encaixada no IDE ou flutuante como uma janela separada. Quando uma janela de documento é flutuante fora do IDE, ele ainda se encontra em um bem de documento e tem o plano de fundo, borda, texto e guia de cores que é os mesmos de quando ele é parte do IDE. No entanto, o documento se encontra dentro de um quadro que tem seu próprio plano de fundo, borda e cores do texto. Quando as janelas de ferramentas são encaixadas do poço de documento, eles herdam o comportamento e a cor de suas guias de nomes de token de janela do documento.  

![Janela encaixada de documento (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-065_dockeddocumentwindowredline.png "0303 065_DockedDocumentWindowRedline")<br />Janela encaixada de documento (corte de funcionários)  

![Janela de documentos flutuante (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-066_floatingdocumentwindowredline.png "0303 066_FloatingDocumentWindowRedline")<br />Janela de documentos flutuante (corte de funcionários)  

| Use... | Não use... |
| --- | --- |
| ... em qualquer lugar você está criando a interface do usuário que você deseja correspondência com a janela do documento. | ... para qualquer interface do usuário que você não deseja automaticamente alterado se o shell tem uma atualização de tema. |

**Janela do documento encaixado ou flutuante: estado padrão**  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | Depende do tipo de documento |
| Em primeiro plano (texto) | Depende do tipo de documento |
| Borda | `Environment.ToolWindowBorder` |

**Com foco, flutuante quadro de janela de documento: estado padrão**

![Padrão centrado, flutuante quadro de janela de documento](../../extensibility/ux-guidelines/media/0303-067_framefocused.png "0303 067_FrameFocused")<br />Padrão centrado, flutuante quadro de janela de documento

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolWindowFloatingFrame` |
| Em primeiro plano (texto) | `Environment.ToolWindowFloatingFrame` |
| Em primeiro plano (glifo) | `Environment.RaftedWindowButtonActiveGlyph` |
| Borda | `Environment.MainWindowActiveDefaultBorder` |
| Borda (glifo) | `Environment.RaftedWindowButtonActiveBorder`<br />(Definido como transparente) |

**Quadro de janela do documento sem foco, flutuante: estado padrão**  

![Quadro de janela de documentos flutuante sem foco padrão](../../extensibility/ux-guidelines/media/0303-068_frameunfocused.png "0303 068_FrameUnfocused")<br />Padrão de quadro de janela de documentos flutuante sem foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolWindowFloatingFrameInactive` |
| Em primeiro plano (texto) | `Environment.ToolWindowFloatingFrameInactive` |
| Em primeiro plano (glifo) | `Environment.RaftedWindowButtonInactiveGlyph` |
| Borda | `Environment.MainWindowInactiveBorder` |
| Borda (glifo) | `Environment.RaftedWindowButtonInactiveBorder`<br />(Definido como transparente) |

**Com foco, flutuante quadro de janela de documento: passe o mouse de estado**

![Com foco, flutuante quadro de janela de documento em foco](../../extensibility/ux-guidelines/media/0303-069_framefocusedhover.png "0303 069_FrameFocusedHover")<br />Com foco, flutuante quadro de janela de documento em foco  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em segundo plano (glifo) | `Environment.RaftedWindowButtonHoverActive` |
| Em primeiro plano (glifo) | `Environment.RaftedWindowButtonHoverActiveGlyph` |
| Borda (glifo) | `Environment.RaftedWindowButtonHoverActiveBorder` |

**Quadro de janela do documento sem foco, flutuante: passe o mouse de estado**  

![Quadro de janela de documentos flutuante sem foco ao passar](../../extensibility/ux-guidelines/media/0303-070_frameunfocusedhover.png "0303 070_FrameUnfocusedHover")<br />Quadro de janela de documentos flutuante sem foco ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em segundo plano (glifo) | `EnvironmentRaftedWindowButtonHoverInactive` |
| Em primeiro plano (glifo) | `Environment.RaftedWindowButtonHoverInactiveGlyph` |
| Borda (glifo) | `Environment.RaftedWindowButtonHoverInactiveBorder` |

**Com foco, flutuante quadro de janela de documento: estado pressionado**  

![Focadas e flutuante quadro de janela de documento em press](../../extensibility/ux-guidelines/media/0303-071_framefocusedpressed.png "0303 071_FrameFocusedPressed")<br />Com foco, flutuante quadro de janela de documento em pressione

| Elemento | Nome do token: Category.color |
| --- | --- |
| Em segundo plano (glifo) | `Environment.RaftedWindowButtonDown` |
| Em primeiro plano (glifo) | `Environment.RaftedWindowButtonDownGlyph` |
| Borda (glifo) | `Environment.RaftedWindowButtonDownBorder` |

### <a name="document-tabs"></a>Guias de documento  
Guias do documento ficam no canal de guia para indicar quais documentos estão abertos no momento, junto com o qual é o atual selecionado ou o documento ativo. Janelas de ferramenta também podem ser encaixadas no canal de guia de documento, se o usuário coloca lá. Nessa situação, eles usam as mesmas cores do guia como janelas de documentos. Se você estiver criando interface do usuário que você deseja sempre coincidir com as cores da janela de documento (incluindo atualizações de tema ou se novos temas instalados), em seguida, fazer referência a esses tokens de cor.  

![Guias de documento (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-072_documenttabredline.png "0303 072_DocumentTabRedline")<br />Guias de documento (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... em qualquer lugar você está criando a interface do usuário que você deseja corresponder guias do documento e separar automaticamente atualizações do tema ou novas cores de tema. | ... para qualquer interface do usuário que você não deseja alterar automaticamente quando o shell tem um tema de atualização. |

#### <a name="open-document-tabs"></a>Guias de documento aberto  
Cada documento aberto tem uma guia no canal de guia de documento que exibe seu nome. Documentos podem ser selecionados ou abra em segundo plano, e suas guias refletem esses estados:  

-   A guia selecionada representa o documento que está sendo exibido no documento bem. Uma guia selecionada tem uma borda de documento que estende bem em toda a borda superior do documento.  

-   Guias de plano de fundo são guias qualquer documento que não estão na guia selecionada no momento. Quando clicado, eles tornam-se a guia selecionada e adquirem todas as cores de plano de fundo, borda e texto desses nomes de token.  

![Guia de documento aberto (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-073_opendocumenttabredline.png "0303 073_OpenDocumentTabRedline")<br />Guia de documento aberto (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... quando você estiver criando guias de documento personalizado. | ... por guias provisionados (visualização). |
| | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tem uma atualização de tema. |

**Guia de documento selecionado, com foco**  

![Selecionado, voltada para a guia de documento](../../extensibility/ux-guidelines/media/0303-074_selectedtabfocused.png "0303 074_SelectedTabFocused")<br />Guia de documento selecionado, com foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.FileTabSelectedGradientTop`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.FileTabSelectedText` |
| Borda | `Environment.FileTabSelectedBorder`<br />(Definido para a mesma cor do plano de fundo). |
| Borda de documento | `Environment.FileTabDocumentBorderBackground` |

**Guia de documento selecionado, sem foco**

![Guia de documento selecionado, sem foco](../../extensibility/ux-guidelines/media/0303-075_selectedtabunfocused.png "0303 075_SelectedTabUnfocused")<br />Guia de documento selecionado, sem foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.FileTabInactiveGradientTop`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.FileTabInactiveText` |
| Borda | `Environment.FileTabInactiveBorder`<br />(Definido para a mesma cor do plano de fundo). |
| Borda de documento | `Environment.FileTabInactiveDocumentBorderBackground` |

**Guia de plano de fundo do documento: estado padrão**  

![Guia de documento do plano de fundo padrão](../../extensibility/ux-guidelines/media/0303-076_backgroundtab.png "0303 076_BackgroundTab")<br />Guia de documento do plano de fundo padrão  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.FileTabBackground` |
| Em primeiro plano (texto) | `Environment.FileTabText` |
| Borda | `Environment.FileTabBorder`<br />(Definido para a mesma cor do plano de fundo). |

**Guia de plano de fundo do documento: passe o mouse de estado**  

![Guia de documento do plano de fundo ao focalizar](../../extensibility/ux-guidelines/media/0303-077_backgroundtabhover.png "0303 077_BackgroundTabHover")<br />Guia de documento do plano de fundo ao focalizar  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.FileTabHotGradientTop`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.FileTabHotText` |
| Borda | `Environment.FileTabHotBorder`<br />(Definido para a mesma cor do plano de fundo). |

#### <a name="preview-tab"></a>Guia de visualização  
Também chamado de uma guia "provisória". Na guia Visualização aparece à direita do canal de guia de documento quando o usuário clica em um item na janela da ferramenta Gerenciador de soluções. Ele atua como uma visualização do documento e também fornece ao usuário a opção para manter o documento aberto no lado esquerdo do canal de guia de documento. Guia de apenas uma visualização aberta pode ser aberto por vez. Guias de visualização têm ambos em segundo plano e estados selecionados, como guias abertas e pode ser focalizado ou sem foco em seu estado ativo.  

![Guia de visualização (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-078_previewtabredline.png "0303 078_PreviewTabRedline")<br />Guia de visualização (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... em qualquer lugar em que você está criando provisória visualizar e deseja que algum elemento para coincidir com a cor de guia de visualização atual. | ... para qualquer tipo de documento ou a guia não é provisório (visualização). |
| | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tem uma atualização de tema. |

**Guia de visualização com foco, selecionado**  

![Guia de visualização selecionado, focalizado](../../extensibility/ux-guidelines/media/0303-079_previewtabfocused.png "0303 079_PreviewTabFocused")<br />Guia de visualização com foco, selecionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.FileTabProvisionalSelectedActive` |
| Em primeiro plano (texto) | `Environment.FileTabProvisionalSelectedActiveForeground` |
| Borda | `Environment.FileTabProvisionalSelectedActiveBorder`<br />(Definido para a mesma cor do plano de fundo). |
| Borda de documento | `Environment.FileTabProvisionalSelectedActiveBorder` |

**Guia de visualização sem foco, selecionado**  

![Guia de visualização selecionada, sem foco](../../extensibility/ux-guidelines/media/0303-080_previewtabunfocused.png "0303 080_PreviewTabUnfocused")<br />Guia de visualização sem foco, selecionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.FileTabProvisionalSelectedInactive` |
| Em primeiro plano (texto) | `Environment.FileTabProvisionalSelectedInactiveForeground` |
| Borda | `Environment.FileTabProvisionalSelectedInactiveBorder` |
| Borda de documento | `Environment.FileTabProvisionalSelectedInactiveBorder` |

**Guia de visualização do plano de fundo: estado padrão**  

![Guia de visualização do plano de fundo padrão](../../extensibility/ux-guidelines/media/0303-081_previewbackgroundtab.png "0303 081_PreviewBackgroundTab")<br />Guia de visualização do plano de fundo padrão  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.FileTabProvisionalInactive` |
| Em primeiro plano (texto) | `Environment.FileTabProvisionalInactiveForeground` |
| Borda | `Environment.FileTabProvisionalInactiveBorder`<br />(Definido para a mesma cor do plano de fundo). |

**Guia de visualização do plano de fundo: passe o mouse de estado**  

![Guia de visualização do plano de fundo ao focalizar](../../extensibility/ux-guidelines/media/0303-082_previewbackgroundtabhover.png "0303 082_PreviewBackgroundTabHover")<br />Guia de visualização do plano de fundo ao focalizar  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.FileTabProvisionalHover` |
| Em primeiro plano (texto) | `Environment.FileTabProvisionalHoverForeground` |
| Borda | `Environment.FileTabProvisionalHoverBorder`<br />(Definido para a mesma cor do plano de fundo). |

#### <a name="document-overflow-button"></a>Botão de estouro de documento  
O botão de estouro do documento está presente se há um ou mais documentos abertos, independentemente se há espaço vertical na configuração atual de acordo com todas as guias de documento. O menu suspenso de estouro de documento, que é controlado pela [menu da barra de comando](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandMenus) cores, exibe uma lista de todos os documentos abertos, visíveis e ocultos e o estouro glifo se altera dependendo se são todos os documentos abertos exibido no canal de guia.  

![Botão de estouro de documento (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-083_overflowredline.png "0303 083_OverflowRedline")<br />Botão de estouro de documento (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... quando você estiver criando um botão de estouro do documento personalizado. | ... para interface do usuário que não é semelhante a um botão de estouro. |
| | ... para botões de estouro da barra de comando. |

**Botão de estouro de documento: estado padrão**  

![Botão de estouro de documento padrão](../../extensibility/ux-guidelines/media/0303-084_overflow.png "0303 084_Overflow")<br />Botão de estouro de documento padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.DocWellOverflowButtonBackground` |
| Em primeiro plano (glifo) | `Environment.DocWellOverflowButtonGlyph` |
| Borda | N/D |

**Botão de estouro de documento: passe o mouse de estado**

![Botão de estouro de documento em foco](../../extensibility/ux-guidelines/media/0303-085_overflowhover.png "0303 085_OverflowHover")<br />Botão de estouro de documento em foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.DocWellOverflowButtonMouseOverBackground` |
| Em primeiro plano (glifo) | `Environment.DocWellOverflowButtonMouseOverGlyph` |
| Borda | `Environment.DocWellOverflowButtonMouseOverBorder` |

**Botão de estouro de documento: estado pressionado**  

![Botão de estouro de documento na imprensa](../../extensibility/ux-guidelines/media/0303-086_overflowpressed.png "0303 086_OverflowPressed")<br />Botão de estouro de documento na imprensa

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.DocWellOverflowButtonMouseDownBackground` |
| Em primeiro plano (glifo) | `Environment.DocWellOverflowButtonMouseDownGlyph` |
| Borda | `Environment.DocWellOverflowButtonMouseDownBorder` |

### <a name="tagging"></a>Marcação  
Visual Studio dá suporte à marcação, que permite que um usuário declarar as palavras-chave pesquisável para fins de acompanhamento. Por exemplo, os desenvolvedores e gerentes de projeto podem usar o Team Foundation Server (TFS) para marcar os itens de trabalho. As tabelas a seguir dar nomes de cor para a marca em si e o glifo "ícone de fechar" que aparece nos Estados selecionados e passe o mouse.  

![Marcação no Visual Studio (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-176_taggingredline.png "0303 176_TaggingRedline")<br />Marcação no Visual Studio (corte de funcionários)  

| Use... | Não use... |
| --- | --- |
| ... para interface do usuário que dá suporte à marcação. | ... para qualquer outro tipo de interface do usuário. |

#### <a name="tags"></a>Marcas  

**Marca: estado padrão**

![Marca padrão](../../extensibility/ux-guidelines/media/0303-177_tag.png "0303 177_Tag")<br />Marca padrão

| Elemento | Nome do token: Category.color |
| --- | --- |  
| Informações preliminares | `Tag.Background` |
| Em primeiro plano (texto) | `Tag.Background` |

**Marca: estado de focalização**  

![Marca ao focalizar](../../extensibility/ux-guidelines/media/0303-178_taghover.png "0303 178_TagHover")<br />Marca ao focalizar  

| Elemento | Nome do token: Category.color |
| --- | --- |  
| Informações preliminares | `Tag.HoverBackground` |
| Em primeiro plano (texto) | `Tag.HoverBackgroundText` |

**Marca: estado de pressionamento**

![Pressionado a marca](../../extensibility/ux-guidelines/media/0303-179_tagpressed.png "0303 179_TagPressed")<br />Marca pressionada  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Tag.PressedBackground` |
| Em primeiro plano (texto) | `Tag.PressedBackgroundText` |

**Marca: estado selecionado**

![Selecionado marca](../../extensibility/ux-guidelines/media/0303-180_tagselected.png "0303 180_TagSelected")<br />Marca selecionada  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Tag.SelectedBackground` |
| Em primeiro plano (texto) | `Tag.SelectedBackgroundText` |

#### <a name="close-times-tag-glyph"></a>Fechar (&times;) glifo de marca

**Fechar (&times;) glifo de marca: estado padrão**

![Padrão de fechamento (&times;) glifo de marca](../../extensibility/ux-guidelines/media/0303-181_tagglyph.png "0303 181_TagGlyph")<br />Padrão de fechamento (&times;) glifo de marca

| Elemento | Nome do token: Category.color |
| --- | --- |  
| Informações preliminares | N/D |
| Em primeiro plano (glifo) | `Tag.TagHoverGlyph` |

**Fechar (&times;) glifo de marca: passe o mouse de estado**

![Fechar (&times;) glifo de marca ao focalizar](../../extensibility/ux-guidelines/media/0303-182_tagglyphhover.png "0303 182_TagGlyphHover")<br />Fechar (&times;) glifo de marca ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Tag.TagHoverGlyphHoverBackground` |
| Em primeiro plano (glifo) | `Tag.TagHoverGlyphHover` |
| Borda | `Tag.TagHoverGlyphHoverBorder` |

**Fechar (&times;) glifo de marca: estado pressionado**

![Pressionado Close (&times;) glifo de marca](../../extensibility/ux-guidelines/media/0303-183_tagglyphpressed.png "0303 183_TagGlyphPressed")<br />Pressionado Close (&times;) glifo de marca

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Tag.TagHoverGlyphPressedBackground` |
| Em primeiro plano (glifo) | `Tag.TagHoverGlyphPressed` |
| Borda | `Tag.TagHoverGlyphPressedBorder` |

**Selecionado de marca de fechamento (&times;) glifo: estado padrão**

![A marca selecionada com o fechamento padrão (&times;) glifo](../../extensibility/ux-guidelines/media/0303-184_tagselected.png "0303 184_TagSelected")<br />A marca selecionada com o fechamento padrão (&times;) glifo

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | N/D |
| Em primeiro plano (glifo) | `Tag.TagSelectedGlyph` |

**Selecionado de marca de fechamento (&times;) glifo: passe o mouse de estado**  

![Selecionado de marca de fechamento (&times;) glifo focalizar](../../extensibility/ux-guidelines/media/0303-185_tagselectedhover.png "0303 185_TagSelectedHover")<br />Selecionado de marca de fechamento (&times;) glifo ao focalizar  


| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Tag.TagSelectedGlyphHoverBackground` |
| Em primeiro plano (glifo) | `Tag.TagSelectedGlyphHover` |
| Borda | `Tag.TagSelectedGlyphHoverBorder` |

**Selecionado de marca de fechamento (&times;) glifo: estado pressionado**  

![Selecionado, pressionado a marca de fechamento (&times;) glifo](../../extensibility/ux-guidelines/media/0303-186_tagselectedpressed.png "0303 186_TagSelectedPressed")<br />Selecionado, pressionado a marca de fechamento (&times;) glifo

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Tag.TagSelectedGlyphPressedBackground` |
| Foreground(glyph) | `Tag.TagSelectedGlyphPressed` |
| Borda | `Tag.TagSelectedGlyphPressedBorder` |

## <a name="tool-windows"></a>Janelas de ferramentas  
Não é necessário para replicar as janelas de ferramentas, porque elas são fornecidas pelo ambiente do Visual Studio. No entanto, você pode decidir o que você deseja aproveitar as cores usadas em janelas de ferramentas para que sua interface do usuário apareça sempre consistente com essa parte do ambiente do Visual Studio.  

![Janela de ferramentas (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-087_toolwindowredline.png "0303 087_ToolWindowRedline")<br />Janela de ferramentas (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... em qualquer lugar você está criando a interface do usuário que você deseja correspondência com janelas de ferramentas. | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tem uma atualização de tema. |

### <a name="tool-window-frame"></a>Quadro de janela de ferramenta  
Janelas de ferramenta no Visual Studio são usadas para muitas tarefas diferentes e podem existir em um de vários estados diferentes. Se uma janela de ferramentas estiver aberta, podem ser atribuído a qualquer um dos quatro lados da área do documento. Janelas de ferramenta também podem flutuar fora do IDE, o que lhes permite ser reposicionadas em qualquer lugar na tela do usuário. Janelas flutuantes sempre ficam na parte superior do IDE. Por fim, as janelas de ferramentas podem ser encaixadas como janelas de documentos e aparecem como uma guia no documento bem. Janelas de ferramentas que foram encaixadas como janelas de documentos são coloridas em parte, usando nomes de token de janela do documento.  

![Quadro de janela da ferramenta (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-088_toolwindowframeredline.png "0303 088_ToolWindowFrameRedline")<br />Quadro de janela da ferramenta (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... em qualquer lugar você está criando a interface do usuário que você deseja correspondência com janelas de ferramentas. | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tem uma atualização de tema. |

**Janela de ferramentas encaixada**  

![Janela de ferramentas encaixadas](../../extensibility/ux-guidelines/media/0303-089_toolwindowdocked.png "0303 089_ToolWindowDocked")<br />Janela de ferramentas encaixada  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolWindowBackground` |
| Borda | `Environment.ToolWindowBorder` |

**Flutuante, voltada para a janela de ferramentas**

![Flutuante, voltada para a janela de ferramentas](../../extensibility/ux-guidelines/media/0303-090_toolwindowfocused.png "0303 090_ToolWindowFocused")<br />Flutuante, voltada para a janela de ferramentas

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolWindowBackground` |
| Borda | `Environment.MainWindowActiveDefaultBorder` |

**Flutuante, a janela da ferramenta sem foco**  

![Janela de ferramentas flutuantes, sem foco](../../extensibility/ux-guidelines/media/0303-091_toolwindowunfocused.png "0303 091_ToolWindowUnfocused")<br />Flutuante, a janela da ferramenta sem foco  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolWindowBackground` |
| Borda | `Environment.MainWindowInactiveBorder` |

### <a name="toolbox-like-windows"></a>Caixa de ferramentas como windows
A caixa de ferramentas é uma das janelas de ferramentas comuns usados com mais frequência no Visual Studio. Ele é essencialmente um controle de árvore com um tema especial e o estilo aplicado.  

![Janela de caixa de ferramentas (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-189_toolboxredline.png "0303 189_ToolboxRedline")<br />Janela de caixa de ferramentas (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... quando você está projetando uma janela de ferramentas que você deseja sempre são consistentes com a caixa de ferramentas do shell. | ... para qualquer coisa que não seja semelhante à caixa de ferramentas da interface do usuário, ou se você não tiver certeza se a interface do usuário poderão ter problemas se a caixa de ferramentas do shell de alteração de cores. |

**Nós de caixa de ferramentas: estado padrão**

![Nó de pai da caixa de ferramentas padrão](../../extensibility/ux-guidelines/media/0303-190_toolboxparentnode.png "0303 190_ToolboxParentNode")<br />Nó de pai da caixa de ferramentas padrão

![Nó de filho de caixa de ferramentas padrão](../../extensibility/ux-guidelines/media/0303-191_toolboxchildnode.png "0303 191_ToolboxChildNode")<br />Nó de filho de caixa de ferramentas padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolboxContent`<br />(Cabeçalhos) |
| Informações preliminares | `Environment.ToolWindowBackground`<br />(Itens individuais ou toda a janela se nenhum controle disponível) |
| Borda | Nenhum |
| Em primeiro plano (glifo) | `Environment.ToolboxContent` |
| Em primeiro plano (texto) | `Environment.ToolboxContent` |

**Nós filho de caixa de ferramentas: passe o mouse de estado**

![Nó filho de caixa de ferramentas ao focalizar](../../extensibility/ux-guidelines/media/0303-192_toolboxchildnodehover.png "0303 192_ToolboxChildNodeHover")<br />Nó filho de caixa de ferramentas ao focalizar  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolboxContentMouseOver`<br />(Somente para itens individuais) |
| Borda | Nenhum |
| Em primeiro plano (texto) | `Environment.ToolboxContentMouseOver`<br />(Somente para itens individuais) |

**Caixa de ferramentas nós selecionados: voltada para o estado**

![Nó pai de caixa de ferramentas com foco, selecionado](../../extensibility/ux-guidelines/media/0303-193_toolboxparentnodefocused.png "0303 193_ToolboxParentNodeFocused")<br />Nó pai de caixa de ferramentas com foco, selecionado  

![Nó filho de caixa de ferramentas com foco, selecionado](../../extensibility/ux-guidelines/media/0303-194_toolboxchildnodefocused.png "0303 194_ToolboxChildNodeFocused")<br />Nó filho de caixa de ferramentas com foco, selecionado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `TreeView.SelectedItemActive`<br />Partir [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) categoria |
| Borda | `TreeView.FocusVisualBorder`<br />Partir [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) categoria |
| Em primeiro plano (glifo) | `TreeView.SelectedItemActive`<br />Partir [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) categoria |
| Em primeiro plano (texto) | `TreeView.SelectedItemActive`<br />Partir [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) categoria |

**Caixa de ferramentas nós selecionados: estado sem foco**

![Nó pai de caixa de ferramentas selecionado, sem foco](../../extensibility/ux-guidelines/media/0303-195_toolboxparentnodeunfocused.png "0303 195_ToolboxParentNodeUnfocused")<br />Nó pai de selecionada, uma caixa de ferramentas  

![Nó filho de caixa de ferramentas selecionado, sem foco](../../extensibility/ux-guidelines/media/0303-196_toolboxchildnodeunfocused.png "0303 196_ToolboxChildNodeUnfocused")<br />Nó de filho selecionado, uma caixa de ferramentas  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `TreeView.SelectedItemInactive`<br />Partir [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) categoria |
| Borda | Nenhum |
| Em primeiro plano (glifo) | `TreeView.SelectedItemInactive`<br />Partir [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) categoria |
| Em primeiro plano (texto) | `TreeView.SelectedItemInactive`<br />Partir [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) categoria |

### <a name="tool-window-title-bar"></a>Barra de título de janela de ferramenta  
A borda da barra de título não é uma borda true, ele é uma linha espessa na parte superior da barra de título. Ele não tem um nome de token para seu estado sem foco.  

![Barra de título de janela de ferramenta (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-092_toolwindowtitlebarredline.png "0303 092_ToolWindowTitleBarRedline")<br />Barra de título de janela de ferramenta (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... em qualquer lugar você está criando a interface do usuário que você deseja correspondência com janelas de ferramentas. | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tem uma atualização de tema. |

**Barra de título focalizado**

![Barra de título focalizado](../../extensibility/ux-guidelines/media/0303-093_titlebarfocused.png "0303 093_TitleBarFocused")<br />Barra de título focalizado

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.TitleBarActiveGradientBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.TitleBarActiveText` |
| Borda | `Environment.TitleBarActiveBorder`<br />(Definido para a mesma cor do plano de fundo). |
| Arraste a alça | `Environment.TitleBarDragHandleActive` |

**Barra de título sem foco**  

![Barra de título sem foco](../../extensibility/ux-guidelines/media/0303-094_titlebarunfocused.png "0303 094_TitleBarUnfocused")<br />Barra de título sem foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.TitleBarInactiveGradientBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.TitleBarInactiveText` |
| Borda | N/D |
| Arraste a alça | `Environment.TitleBarDragHandle` |

#### <a name="tool-window-title-bar-buttons"></a>Botões de barra de título de janela de ferramenta  
![Botão da barra de título (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-095_titlebarbuttonredline.png "0303 095_TitleBarButtonRedline")<br />Botão da barra de título (corte de funcionários)  

| Use... | Não use... |
| --- | --- |
| ... para os botões que aparecem na interface do usuário que usa tokens de cor das barras de título da janela de ferramenta. | ... para os botões que aparecem em outros locais. |
| | ... em qualquer combinação de plano de fundo/primeiro plano diferente do especificado. |

**Voltada para botões da barra de título: estado padrão**

![Padrão, voltada para botões da barra de título](../../extensibility/ux-guidelines/media/0303-096_titlebarbuttonfocused.png "0303 096_TitleBarButtonFocused")<br />Padrão, os botões da barra de título focalizado  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | N/D |
| Em primeiro plano (glifo) | `Environment.ToolWindowButtonActiveGlyph` |
| Borda | N/D |

**Botões da barra de título sem foco: estado padrão**

![Padrão, os botões da barra de título sem foco](../../extensibility/ux-guidelines/media/0303-097_titlebarbuttonunfocused.png "0303 097_TitleBarButtonUnfocused")<br />Padrão, os botões da barra de título sem foco    

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | N/D |
| Em primeiro plano (glifo) | `Environment.ToolWindowButtonInactiveGlyph` |
| Borda | N/D |

**Voltada para botões da barra de título: passe o mouse de estado**  

![Voltada para botões da barra de título ao focalizar](../../extensibility/ux-guidelines/media/0303-098_titlebarbuttonfocusedhover.png "0303 098_TitleBarButtonFocusedHover")<br />Botões da barra de título com foco em foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolWindowButtonHoverActive` |
| Em primeiro plano (glifo) | `Environment.ToolWindowButtonHoverActiveGlyph` |
| Borda | `Environment.ToolWindowButtonHoverActiveBorder` |

**Botões da barra de título sem foco: passe o mouse de estado**  

![Botões da barra de título sem foco ao passar](../../extensibility/ux-guidelines/media/0303-099_titlebarbuttonunfocusedhover.png "0303 099_TitleBarButtonUnfocusedHover")<br />Botões da barra de título sem foco ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolWindowButtonHoverInactive` |
| Em primeiro plano (glifo) | `Environment.ToolWindowButtonHoverInactiveGlyph` |
| Borda | `Environment.ToolWindowButtonHoverInactiveBorder` |

**Voltada para botões da barra de título: estado pressionado**

![Voltada para botões da barra de título press](../../extensibility/ux-guidelines/media/0303-100_titlebarbuttonfocusedpressed.png "0303 100_TitleBarButtonFocusedPressed")<br />Botões da barra de título com foco na imprensa

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolWindowButtonDown` |
| Em primeiro plano (glifo) | `Environment.ToolWindowButtonDownActiveGlyph` |
| Borda | `Environment.ToolWindowButtonDownBorder` |

**Botões da barra de título sem foco: estado pressionado**

![Botões da barra de título sem foco pressionar](../../extensibility/ux-guidelines/media/0303-101_titlebarbuttonunfocusedpressed.png "0303 101_TitleBarButtonUnfocusedPressed")<br />Botões da barra de título sem foco na imprensa  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolWindowButtonDown` |
| Em primeiro plano (glifo) | `Environment.ToolWindowButtonDownInactiveGlyph` |
| Borda | `Environment.ToolWindowButtonDownBorder` |

### <a name="tool-window-tabs"></a>Guias da janela de ferramenta  
![Guia da janela de ferramenta (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-102_toolwindowtabredline.png "0303 102_ToolWindowTabRedline")<br />Guia da janela de ferramenta (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... em qualquer lugar você está criando a interface do usuário que você deseja correspondência com janelas de ferramentas. | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tem uma atualização de tema. |

**Guia da janela de ferramenta selecionada, com foco**

![Selecionado, voltada para a guia da janela de ferramenta](../../extensibility/ux-guidelines/media/0303-103_toolwindowtabfocused.png "0303 103_ToolWindowTabFocused")<br />Guia da janela de ferramenta selecionada, com foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolWindowTabSelectedTab` |
| Em primeiro plano (texto) | `Environment.ToolWindowTabSelectedActiveText` |
| Borda | `Environment.ToolWindowTabSelectedBorder`<br />(Definido para a mesma cor do plano de fundo). |

**Guia da janela de ferramenta selecionada, sem foco**  

![Guia da janela de ferramenta selecionada, sem foco](../../extensibility/ux-guidelines/media/0303-104_toolwindowtabunfocused.png "0303 104_ToolWindowTabUnfocused")<br />Guia da janela de ferramenta selecionada, sem foco

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolWindowTabSelectedTab` |
| Em primeiro plano (texto) | `Environment.ToolWindowTabSelectedText` |
| Borda | `Environment.ToolWindowTabSelectedBorder`<br />(Definido para a mesma cor do plano de fundo). |

**Guia de janela de ferramenta do plano de fundo: estado padrão**

![Guia de janela de ferramenta padrão em segundo plano](../../extensibility/ux-guidelines/media/0303-105_toolwindowbackgroundtab.png "0303 105_ToolWindowBackgroundTab")<br />Guia de janela de ferramenta de plano de fundo padrão  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolWindowTabGradientBegin`<br />`Environment.ToolWindowTabGradientEnd`<br />(Marcas de gradiente definido como o mesmo valor de cor no Visual Studio 2013.) |
| Em primeiro plano (texto) | `Environment.ToolWindowTabText` |
| Borda | `Environment.ToolWindowTabBorder` |

**Guia de janela de ferramenta do plano de fundo: passe o mouse de estado**

![Guia de janela de ferramenta do plano de fundo ao focalizar](../../extensibility/ux-guidelines/media/0303-106_toolwindowbackgroundtabhover.png "0303 106_ToolWindowBackgroundTabHover")<br />Guia de janela de ferramenta do plano de fundo ao focalizar

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.ToolWindowTabMouseOverBackgroundBegin`<br />`Environment.ToolWindowTabMouseOverBackgroundEnd`<br />(Marcas de gradiente definido como o mesmo valor de cor no Visual Studio 2013.) |
| Em primeiro plano (texto) | `Environment.ToolWindowTabMouseOverText` |
| Borda | `Environment.ToolWindowTabMouseOverBorder`<br />(Definido para a mesma cor do plano de fundo). |  

### <a name="auto-hide-tabs"></a>Guias de ocultar automaticamente  

![Guias de ocultação automática (corte de funcionários)](../../extensibility/ux-guidelines/media/0303-107_autohideredline.png "0303 107_AutoHideRedline")guias de ocultação automática (corte de funcionários)

| Use... | Não use... |
| --- | --- |
| ... em qualquer lugar você está criando a interface do usuário que você deseja correspondência com guias da janela de ferramenta ocultos automaticamente. | ... para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tem uma atualização de tema. |

**Ocultar automaticamente guias: estado padrão**  

![Guia de ocultação automática padrão](../../extensibility/ux-guidelines/media/0303-108_autohidetab.png "0303 108_AutoHideTab")<br />Guia de ocultação automática padrão

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.AutoHideTabBackgroundBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.AutoHideTabText` |
| Borda | `Environment.AutoHideTabBorder` |

**Ocultar automaticamente guias: passe o mouse de estado**

![Guia de ocultamento automático ao passar](../../extensibility/ux-guidelines/media/0303-109_autohidetabhover.png "0303 109_AutoHideTabHover")<br />Guia de ocultamento automático ao focalizar  

| Elemento | Nome do token: Category.color |
| --- | --- |
| Informações preliminares | `Environment.AutoHideTabMouseOverBackgroundBegin`<br />(Marcas de gradiente para este token não é usado na interface do usuário com tema.) |
| Em primeiro plano (texto) | `Environment.AutoHideTabMouseOverText` |
| Borda | `Environment.AutoHideTabMouseOverBorder` |
