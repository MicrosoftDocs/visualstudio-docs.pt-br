---
title: Compartilhado cores para o Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8d11b9a0-6175-4f2e-8e7f-79daee1bfd41
caps.latest.revision: 6
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 7c0cccf5787d635db9ab04c70df1be97fc0c82d8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51723685"
---
# <a name="shared-colors-for-visual-studio"></a>Cores compartilhadas para o Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Quando você está projetando a interface do usuário que usa elementos comuns de shell do Visual Studio, ou você gostaria de seu elemento de interface para ser consistente com recursos semelhantes, use nomes de token existentes nos arquivos de definição de pacote para escolher e atribuir cores. Isso garante que sua interface do usuário permaneça consistente com o ambiente geral do Visual Studio e que ele será atualizado automaticamente quando os temas são adicionados ou atualizados.  
  
 Este artigo descreve os elementos de interface do usuário comuns e os nomes de token que eles usam, que você pode fazer referência ao criar a interface do usuário semelhante. Para obter informações específicas sobre como acessar esses tokens de cor, consulte [o serviço VSColor](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService).  
  
 Certifique-se de usar nomes de token corretamente:  
  
-   **Use nomes de token com base em função, não na própria cor.** As cores compartilhadas comuns são associadas aos elementos de interface específica e destinam-se somente a ser usado para os recursos iguais ou semelhantes. Por exemplo, não reutilize a cor de uma caixa de combinação pressionado para uma animação de progresso de rotação simplesmente porque você gosta de cor. As funções de caixa de combinação e a animação são diferentes, e se a cor associados com as alterações de caixa de combinação, ele pode não estar mais uma cor apropriada para seu elemento de animação. Uso consistente de cor ajuda a orientar seus usuários e evitar confusão.  
  
-   **Use cores de plano de fundo e texto na combinação correta.** Cores de plano de fundo que se destinam a serem usadas com texto terá uma cor do texto associado. Não use cores de texto que não seja o que é especificado para esse plano de fundo. Se não for uma cor do texto associado, não use essa cor do plano de fundo para qualquer superfície na qual você pretende exibir texto. Outras combinações de cores de plano de fundo e texto podem resultar em uma interface não pode ser lido.  
  
-   **Use cores do controle que são apropriadas para seu local.** Em alguns estados, alguns controles do Visual Studio não tem borda separada e cores de plano de fundo. Em vez disso, eles selecionam essas cores de superfícies de por trás delas. Certifique-se de que você sempre use os nomes de token que são apropriados para o local onde você está colocando o controle.  
  
> [!IMPORTANT]
>  Não use tokens localizadas nas categorias de "Página inicial" ou "Cider".  
  
## <a name="command-structures"></a>Estruturas de comando  
  
###  <a name="BKMK_CommandMenus"></a> Menus  
 Menus podem ocorrer em vários locais dentro do Visual Studio: barra de menu principal, inserida no documento ou a ferramenta windows ou no botão direito do mouse em vários locais em todo o IDE. Implementações de menus associados com outros elementos de interface do usuário são discutidas na seção do elemento do respectivo. Você sempre deve usar a implementação de menu padrão fornecida pelo ambiente do Visual Studio. No entanto, em alguns casos raros talvez você não tenha acesso aos menus padrão do Visual Studio. Nessas situações, use os seguintes nomes de token para garantir que sua interface do usuário seja consistente com outros menus no Visual Studio.  
  
 ![Corte de funcionários em menus](../../extensibility/ux-guidelines/media/0303-000-menuredline.png "0303 000_MenuRedline")  
  
 Use...  
 -   sempre que você precisa criar um menu personalizado.  
  
- Quando você tem um novo componente de interface do usuário que você deseja correspondência com os menus do Visual Studio.  
  
  Não use...  
  a cor de plano de fundo sozinha. Sempre use a combinação de plano de fundo/primeiro plano conforme especificado.  
  
#### <a name="menu-title"></a>Título de menu  
 Títulos de menus consistem em um plano de fundo, uma borda e o texto do título, bem como um glifo opcional, normalmente, quando o menu é encontrado em uma barra de comandos.  
  
 ![Aplicar linhas vermelhas no título de menu](../../extensibility/ux-guidelines/media/0303-001-menutitleredline.png "0303 001_MenuTitleRedline")  
  
 Use...  
 sempre que você está criando um título de menu personalizado.  
  
 Não use...  
 -   para qualquer coisa que você não deseja sempre corresponde ao título de menu.  
  
- em qualquer combinação de plano de fundo/primeiro plano diferente do especificado.  
  
  **Padrão**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Padrão de título de menu](../../extensibility/ux-guidelines/media/0303-002-menutitledefault.png "0303 002_MenuTitleDefault")  
  
  **Título de menu**  
  
  Informações preliminares  
  
  Nenhum  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextActive`  
  
  ![Título de menu com o padrão de glifo](../../extensibility/ux-guidelines/media/0303-003-menutitlewithglyphdefault.png "0303 003_MenuTitleWithGlyphDefault")  
  
  **Título de menu com o glifo**  
  
  Em primeiro plano (glifo)  
  
  `Environment.CommandBarMenuGlyph`  
  
  Borda  
  
  Nenhum  
  
  **Passe o mouse**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Título de menu ao focalizar](../../extensibility/ux-guidelines/media/0303-004-menutitlehover.png "0303 004_MenuTitleHover")  
  
  **Título de menu**  
  
  Informações preliminares  
  
  `Environment.CommandBarMouseOverBackgroundBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextHover`  
  
  ![Título de menu com o glifo focalizar](../../extensibility/ux-guidelines/media/0303-005-menutitlewithglyphhover.png "0303 005_MenuTitleWithGlyphHover")  
  
  **Título de menu com o glifo**  
  
  Em primeiro plano (glifo)  
  
  `Environment.CommandBarMenuMouseOverGlyph`  
  
  Borda  
  
  `Environment.CommandBarBorder`  
  
  **Pressionado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Título de menu pressionado](../../extensibility/ux-guidelines/media/0303-006-menutitlepressed.png "0303 006_MenuTitlePressed")  
  
  **Título de menu**  
  
  Informações preliminares  
  
  `Environment.CommandBarMenuBackgroundGradientBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextActive`  
  
  ![Título de menu com o glifo pressionado](../../extensibility/ux-guidelines/media/0303-007-menutitlewithglyphpressed.png "0303 007_MenuTitleWithGlyphPressed")  
  
  **Título de menu com o glifo**  
  
  Em primeiro plano (glifo)  
  
  `Environment.CommandBarMenuMouseDownGlyph`  
  
  Borda  
  
  `Environment.CommandBarMenuBorder`  
  
  Somente à esquerda, superior e à direita.  
  
  **Desabilitado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Título de menu com o glifo desabilitado](../../extensibility/ux-guidelines/media/0303-008-menutitlewithglyphdisabled.png "0303 008_MenuTitleWithGlyphDisabled")  
  
  **Título de menu com o glifo**  
  
  Informações preliminares  
  
  Nenhum  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextInactive`  
  
  Em primeiro plano (glifo)  
  
  `Environment.CommandBarTextInactive`  
  
  Borda  
  
  Nenhum  
  
#### <a name="menu"></a>Menu  
 Um item de menu individuais consiste o texto do menu e um ícone opcional, a caixa de seleção ou o glifo de submenu. Sua alteração de cor do plano de fundo e texto em foco. Esse token de cor é um par de plano de fundo/primeiro plano.  
  
 ![Corte de funcionários em itens de menu](../../extensibility/ux-guidelines/media/0303-009-menuitemredline.png "0303 009_MenuItemRedline")  
  
 Use...  
 para qualquer lista suspensa que é iniciada a partir de uma barra de menu ou barra de comando.  
  
 Não use...  
 -   para qualquer lista suspensa que ocorre em outro contexto.  
  
- em qualquer combinação de plano de fundo/primeiro plano diferente do especificado.  
  
  **Padrão**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Padrão de menu](../../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303 010_MenuDefault")  
  
  **Menu**  
  
  Informações preliminares  
  
  `Environment.CommandBarMenuBackgroundGradientBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextActive`  
  
  Em primeiro plano (glifo de Submenu)  
  
  `Environment.CommandBarMenuSubmenuGlyph`  
  
  Borda  
  
  `Environment.CommandBarMenuBorder`  
  
  O plano de fundo do ícone canal  
  
  `Environment.CommandBarMenuIconBackground`  
  
  Separador  
  
  `Environment.CommandBarMenuSeparator`  
  
  Sombra  
  
  `Environment.DropShadowBackground`  
  
  ![Menu marcada](../../extensibility/ux-guidelines/media/0303-011-menuchecked.png "0303 011_MenuChecked")  
  
  **Verificado**  
  
  Marca de seleção  
  
  `Environment.CommandBarCheckBox`  
  
  Plano de fundo de marca de seleção  
  
  `Environment.CommandBarSelectedIcon`  
  
  ![Menu selecionado](../../extensibility/ux-guidelines/media/0303-012-menuselected.png "0303 012_MenuSelected")  
  
  **Selecionado**  
  
  Plano de fundo do ícone  
  
  `Environment.CommandBarSelected`  
  
  Borda de ícone  
  
  `Environment.CommandBarSelectedBorder`  
  
  **Passe o mouse**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Passe o mouse menu](../../extensibility/ux-guidelines/media/0303-013-menuhover.png "0303 013_MenuHover")  
  
  **Item de menu**  
  
  Informações preliminares  
  
  `Environment.CommandBarMenuItemMouseOver`  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarMenuItemMouseOver`  
  
  Em primeiro plano (glifo de Submenu)  
  
  `Environment.CommandBarMenuMouseOverSubmenuGlyph`  
  
  ![Em foco o menu marcado](../../extensibility/ux-guidelines/media/0303-014-menuhoverchecked.png "0303 014_MenuHoverChecked")  
  
  **Verificado**  
  
  Marca de seleção  
  
  `Environment.CommandBarCheckBoxMouseOver`  
  
  Plano de fundo de marca de seleção  
  
  `Environment.CommandBarHoverOverSelectedIcon`  
  
  ![Passe o mouse menu selecionado](../../extensibility/ux-guidelines/media/0303-015-menuhoverselected.png "0303 015_MenuHoverSelected")  
  
  **Selecionado**  
  
  Plano de fundo do ícone  
  
  `Environment.CommandBarHoverOverSelected`  
  
  Borda de ícone  
  
  `Environment.CommandBarHoverOverSelectedIconBorder`  
  
  **Desabilitado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Menu desabilitado](../../extensibility/ux-guidelines/media/0303-016-menudisabled.png "0303 016_MenuDisabled")  
  
  Item de menu  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextInactive`  
  
  Em primeiro plano (glifo de Submenu)  
  
  `Environment.CommandBarMenuSubmenuGlyph`  
  
  ![Menu desabilitado marcada](../../extensibility/ux-guidelines/media/0303-017-menudisabledchecked.png "0303 017_MenuDisabledChecked")  
  
  Selecionado  
  
  Marca de seleção  
  
  `Environment.CommandBarCheckBoxDisabled`  
  
  Plano de fundo de marca de seleção  
  
  `Environment.CommandBarSelectedIconDisabled`  
  
### <a name="command-bar"></a>Barra de comandos  
 Barra de comandos pode aparecer em vários lugares dentro do IDE do Visual Studio, mais notavelmente comando comercial e inseridos na ferramenta ou janelas de documento.  
  
 Em geral, sempre use a implementação da barra de comando padrão fornecida pelo ambiente do Visual Studio. Usando o mecanismo padrão garante que todos os detalhes visuais sejam exibidos corretamente e que elementos interativos, será se comportam de maneira consistente com outros controles de barra de comando do Visual Studio. No entanto, se for necessário para você criar sua própria barra de comandos, verifique se que você definir o estilo corretamente usando os seguintes nomes de token.  
  
 ![Corte de funcionários da barra de comandos](../../extensibility/ux-guidelines/media/0303-018-commandbarredline.png "0303 018_CommandBarRedline")  
  
 ![Aplicar linhas vermelhas no botão de estouro](../../extensibility/ux-guidelines/media/0303-019-overflowbuttonredline.png "0303 019_OverflowButtonRedline")  
  
 Use...  
 em locais em que você precisa de um comando inserido barra, mas são não é possível usar a implementação padrão de barra de comando Visual Studio.  
  
 Não use...  
 -   para elementos de interface do usuário que não são semelhantes a uma barra de comandos.  
  
-   para componentes de barra de comando que não sejam aqueles para os quais nomes de token são especificados.  
  
#### <a name="command-bar-group"></a>Grupo de barra de comandos  
 Um grupo de barra de comandos consiste em um conjunto de controles de barra de comandos relacionados e pode conter qualquer número de botões, dividir os menus suspensos, botões, caixas de combinação ou menus. Cores para esses controles são governadas por nomes de token separados e são discutidas individualmente em outro lugar neste guia. Uma linha separadora é usada para dividir um grupo de barra de comandos em subgrupos relacionados.  
  
 ![Aplicar linhas vermelhas no grupo de barra de comandos](../../extensibility/ux-guidelines/media/0303-020-commandbargroupredline.png "0303 020_CommandBarGroupRedline")  
  
 Use...  
 em locais em que você precisa de um comando inserido barra, mas são não é possível usar a implementação padrão de barra de comando Visual Studio.  
  
 Não use...  
 -   para elementos de interface do usuário que não são semelhantes a uma barra de comandos.  
  
- para componentes de barra de comando que não sejam aqueles para os quais nomes de token são especificados.  
  
  **Padrão** (nenhum outro estado)  
  
  Elemento  
  
  Nome do token: Category.color  
  
  Informações preliminares  
  
  `Environment.CommandBarGradientBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Borda  
  
  `Environment.CommandBarToolBarBorder`  
  
  Arraste a alça  
  
  `Environment.CommandBarDragHandle`  
  
  Separador  
  
  `Environment.CommandBarToolBarSeparator`  
  
  `Environment.CommandBarToolBarSeparatorHighlight`  
  
#### <a name="command-icons"></a>Ícones de comando  
 ![Aplicar linhas vermelhas no ícone do comando](../../extensibility/ux-guidelines/media/0303-021-commandiconredline1.png "0303 021_CommandIconRedline1")  
  
 ![Aplicar linhas vermelhas no ícone do comando](../../extensibility/ux-guidelines/media/0303-022-commandiconredline2.png "0303 022_CommandIconRedline2")  
  
 Use...  
 para qualquer botões que serão colocadas em uma barra de comandos.  
  
 Não use...  
 -   para controles que têm seus próprios nomes de token.  
  
- em qualquer combinação de plano de fundo/primeiro plano diferente do especificado.  
  
  **Padrão**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Comando padrão do ícone](../../extensibility/ux-guidelines/media/0303-023-commandicondefault.png "0303 023_CommandIconDefault")  
  
  **Padrão**  
  
  Informações preliminares  
  
  N/d (herda de fundo da barra de comando)  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextActive`  
  
  Borda  
  
  N/D  
  
  ![Comando padrão do ícone selecionado](../../extensibility/ux-guidelines/media/0303-024-commandicondefaultselected.png "0303 024_CommandIconDefaultSelected")  
  
  **Selecionado**  
  
  Informações preliminares  
  
  `Environment.CommandBarSelected`  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextSelected`  
  
  Borda  
  
  `Environment.CommandBarSelectedBorder`  
  
  **Passe o mouse e teclado focalizado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Sobreposição de ícone do comando](../../extensibility/ux-guidelines/media/0303-025-commandiconhover.png "0303 025_CommandIconHover")  
  
  **Padrão ao focalizar**  
  
  Informações preliminares  
  
  `Environment.CommandBarMouseOverBackgroundBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextHover`  
  
  Borda  
  
  `Environment.CommandBarBorder`  
  
  ![Comando de passagem do ícone selecionada](../../extensibility/ux-guidelines/media/0303-026-commandiconhoverselected.png "0303 026_CommandIconHoverSelected")  
  
  **Selecionado ao focalizar**  
  
  Informações preliminares  
  
  `Environment.CommandBarHoverOverSelected`  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextHoverOverSelected`  
  
  Borda  
  
  `Environment.CommandBarHoverOverSelectedIconBorder`  
  
  **Pressionado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Ícone do comando pressionado](../../extensibility/ux-guidelines/media/0303-027-commandiconpressed.png "0303 027_CommandIconPressed")  
  
  **Ícone do comando pressionado**  
  
  Informações preliminares  
  
  `Environment.CommandBarMouseDownBackgroundBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextMouseDown`  
  
  Borda  
  
  `Environment.CommandBarBorder`  
  
  **Desabilitado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Ícone do comando desabilitado](../../extensibility/ux-guidelines/media/0303-028-commandicondisabled.png "0303 028_CommandIconDisabled")  
  
  **Ícone do comando desabilitado**  
  
  Informações preliminares  
  
  N/d (herda de fundo da barra de comando)  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextInactive`  
  
  Borda  
  
  N/D  
  
####  <a name="BKMK_CommandComboBox"></a> Caixa de combinação  
  
> [!IMPORTANT]
>  Caixas de combinação são semelhantes às listas suspensas, mas incluam uma região de texto editável. Se sua lista suspensa não incluir uma região de texto editável, usar os tokens de cor encontrados em [suspensa](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandDropDown).  
  
 ![Corte de funcionários da caixa de combinação](../../extensibility/ux-guidelines/media/0303-029-comboboxredline.png "0303 029_ComboBoxRedline")  
  
 Use...  
 -   ao criar caixas de combinação personalizada.  
  
- ao criar um controle de barra de comando é semelhante a uma caixa de combinação.  
  
  Não use...  
  -   para qualquer coisa que você não deseja sempre coincidir com o comando da barra da interface do usuário.  
  
- Quando você tem acesso a uma caixa de combinação com estilo.  
  
  **Padrão**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Campo de entrada de caixa de combinação](../../extensibility/ux-guidelines/media/0303-030-comboboxinputfield.png "0303 030_ComboBoxInputField")  
  
  **Campo de entrada**  
  
  Informações preliminares  
  
  `Environment.ComboBoxBackground`  
  
  Em primeiro plano (texto)  
  
  `Environment.ComboBoxText`  
  
  Borda  
  
  `Environment.ComboBoxBorder`  
  
  Separador  
  
  Nenhum separador  
  
  ![Soltar da caixa de combinação&#45;botão pressionado](../../extensibility/ux-guidelines/media/0303-031-comboboxdropdownbutton.png "0303 031_ComboBoxDropdownButton")  
  
  **Botão suspenso**  
  
  Informações preliminares  
  
  N/d (herdado)  
  
  Em primeiro plano (glifo)  
  
  `Environment.ComboBoxGlyph`  
  
  ![Caixa de combinação&#47;descartar&#45;para baixo na lista](../../extensibility/ux-guidelines/media/0303-032-comboboxdropdownlist.png "0303 032_ComboBoxDropdownList")  
  
  **Lista suspensa**  
  
  Informações preliminares  
  
  `Environment.ComboBoxPopupBackgroundBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto)  
  
  `Environment.ComboBoxItemText`  
  
  Borda  
  
  `Environment.ComboBoxPopupBorder`  
  
  **Passe o mouse**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Campo de entrada de caixa de combinação focalizar](../../extensibility/ux-guidelines/media/0303-033-comboboxinputfieldhover.png "0303 033_ComboBoxInputFieldHover")  
  
  **Campo de entrada**  
  
  Informações preliminares  
  
  `Environment.ComboBoxMouseOverBackgroundBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto)  
  
  `Environment.ComboBoxMouseOverText`  
  
  Borda  
  
  `Environment.ComboBoxMouseOverBorder`  
  
  Separador  
  
  `Environment.ComboBoxMouseOverSeparator`  
  
  ![Caixa de combinação&#47;descartar&#45;para baixo do botão focalizar](../../extensibility/ux-guidelines/media/0303-034-comboboxdropdownbuttonhover.png "0303 034_ComboBoxDropdownButtonHover")  
  
  **Botão suspenso**  
  
  Informações preliminares  
  
  `Environment.ComboBoxButtonMouseOverBackground`  
  
  Em primeiro plano (glifo)  
  
  `Environment.ComboBoxMouseOverGlyph`  
  
  ![Caixa de combinação&#47;descartar&#45;para baixo na lista ao focalizar](../../extensibility/ux-guidelines/media/0303-035-comboboxdropdownlisthover.png "0303 035_ComboBoxDropdownListHover")  
  
  **Lista suspensa**  
  
  Em segundo plano (item de Menu)  
  
  `Environment.ComboBoxItemMouseOverBackground`  
  
  Em primeiro plano (texto)  
  
  `Environment.ComboBoxItemMouseOverText`  
  
  Borda (item de Menu)  
  
  `Environment.ComboBoxItemMouseOverBorder`  
  
  **Com foco**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Color.category  
  
  ![Campo de entrada caixa de combinação focado](../../extensibility/ux-guidelines/media/0303-036-comboboxinputfieldfocused.png "0303 036_ComboBoxInputFieldFocused")  
  
  **Campo de entrada**  
  
  Informações preliminares  
  
  `Environment.ComboBoxFocusedBackground`  
  
  Em primeiro plano (texto)  
  
  `Environment.ComboBoxFocusedText`  
  
  Borda  
  
  `Environment.ComboBoxFocusedBorder`  
  
  Separador  
  
  `Environment.ComboBoxFocusedButtonSeparator`  
  
  ![Caixa de combinação&#47;descartar&#45;para baixo do botão com foco](../../extensibility/ux-guidelines/media/0303-037-comboboxdropdownbuttonfocused.png "0303 037_ComboBoxDropdownButtonFocused")  
  
  **Botão suspenso**  
  
  Informações preliminares  
  
  `Environment.ComboBoxFocusedButtonBackground`  
  
  Em primeiro plano (glifo)  
  
  `Environment.ComboBoxFocusedGlyph`  
  
  **Pressionado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Color.category  
  
  ![Campo de entrada caixa de combinação pressionado](../../extensibility/ux-guidelines/media/0303-038-comboboxinputfieldpressed.png "0303 038_ComboBoxInputFieldPressed")  
  
  **Campo de entrada**  
  
  Informações preliminares  
  
  `Environment.ComboBoxMouseDownBackground`  
  
  Em primeiro plano (texto)  
  
  `Environment.ComboBoxMouseDownText`  
  
  Borda  
  
  `Environment.ComboBoxMouseDownBorder`  
  
  Separador  
  
  `Environment.ComboBoxMouseDownSeparator`  
  
  ![Caixa de combinação&#47;descartar&#45;para baixo do botão foi pressionado](../../extensibility/ux-guidelines/media/0303-039-comboboxdropdownbuttonpressed.png "0303 039_ComboBoxDropdownButtonPressed")  
  
  **Botão suspenso**  
  
  Informações preliminares  
  
  `Environment.ComboBoxButtonMouseDownBackground`  
  
  Em primeiro plano (glifo)  
  
  `Environment.ComboBoxMouseDownGlyph`  
  
  **Desabilitado**  
  
  ![Campo de entrada caixa de combinação desabilitado](../../extensibility/ux-guidelines/media/0303-041-comboboxinputfielddisabled.png "0303 041_ComboBoxInputFieldDisabled")  
  
  **Campo de entrada**  
  
  Informações preliminares  
  
  `Environment.ComboBoxDisabledBackground`  
  
  Em primeiro plano (texto)  
  
  `Environment.ComboBoxDisabledText`  
  
  Borda  
  
  `Environment.ComboBoxDisabledBorder`  
  
  Separador  
  
  Nenhum separador  
  
  ![Caixa de combinação&#47;descartar&#45;para baixo do botão desabilitada](../../extensibility/ux-guidelines/media/0303-040-comboboxdropdownbuttondisabled.png "0303 040_ComboBoxDropdownButtonDisabled")  
  
  **Botão suspenso**  
  
  Informações preliminares  
  
  Nenhum  
  
  Em primeiro plano (glifo)  
  
  `Environment.ComboBoxDisabledGlyph`  
  
####  <a name="BKMK_CommandDropDown"></a> Lista suspensa  
  
> [!IMPORTANT]
>  Menus suspensos são semelhantes às caixas de combinação, mas não têm regiões de texto editável. Se o menu suspenso inclui uma região de texto editável, usar os tokens de cor encontrados em [caixa de combinação](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandComboBox).  
  
 ![Remova&#45;corte de funcionários para baixo](../../extensibility/ux-guidelines/media/0303-042-dropdownredline.png "0303 042_DropdownRedline")  
  
 Use...  
 Quando você estiver criando controles personalizados na lista suspensa.  
  
 Não use...  
 -   para qualquer coisa que não é semelhante a uma lista suspensa.  
  
- para caixas de combinação ou botões de divisão.  
  
  **Padrão**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Remova&#45;para baixo de campo de seleção](../../extensibility/ux-guidelines/media/0303-043-dropdownselectionfield.png "0303 043_DropdownSelectionField")  
  
  **Campo de seleção**  
  
  Informações preliminares  
  
  `Environment.DropDownBackground`  
  
  Em primeiro plano (texto)  
  
  `DropDownText`  
  
  Borda  
  
  `DropDownBorder`  
  
  Separador  
  
  Nenhum separador  
  
  ![Remova&#45;botão pressionado](../../extensibility/ux-guidelines/media/0303-044-dropdownbutton.png "0303 044_DropdownButton")  
  
  **Botão suspenso**  
  
  Informações preliminares  
  
  Nenhum  
  
  Em primeiro plano (glifo)  
  
  `Environment.DropDownGlyph`  
  
  ![Remova&#45;para baixo na lista](../../extensibility/ux-guidelines/media/0303-045-dropdownlist.png "0303 045_DropdownList")  
  
  **Lista suspensa**  
  
  Informações preliminares  
  
  `Environment.DropDownPopupBackgroundBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto)  
  
  `Environment.ComboBoxItemText`  
  
  Borda  
  
  `Environment.DropDownPopupBorder`  
  
  Sombra  
  
  `Environment.DropShadowBackground`  
  
  **Passe o mouse**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Remova&#45;para baixo de campo de seleção ao focalizar](../../extensibility/ux-guidelines/media/0303-046-dropdownselectionfieldhover.png "0303 046_DropdownSelectionFieldHover")  
  
  **Campo de seleção**  
  
  Informações preliminares  
  
  `Environment.DropDownMouseOverBackgroundBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto)  
  
  `Environment.DropDownMouseOverText`  
  
  Borda  
  
  `Environment.DropDownMouseOverBorder`  
  
  Separador  
  
  `Environment.DropDownButtonMouseOverSeparator`  
  
  ![Remova&#45;para baixo do botão ao passar](../../extensibility/ux-guidelines/media/0303-047-dropdownbuttonhover.png "0303 047_DropdownButtonHover")  
  
  **Botão suspenso**  
  
  Informações preliminares  
  
  `Environment.DropDownButtonMouseOverBackground`  
  
  Em primeiro plano (glifo)  
  
  `Environment.DropDownMouseOverGlyph`  
  
  ![Remova&#45;para baixo na lista ao focalizar](../../extensibility/ux-guidelines/media/0303-048-dropdownlisthover.png "0303 048_DropdownListHover")  
  
  **Lista suspensa**  
  
  Em segundo plano (item de Menu)  
  
  `Environment.ComboBoxItemMouseOverBackground`  
  
  Em primeiro plano (texto)  
  
  `Environment.ComboBoxItemMouseOverText`  
  
  Borda (item de Menu)  
  
  `Environment.ComboBoxItemMouseOverBorder`  
  
  **Pressionado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Remova&#45;para baixo de campo de seleção pressionado](../../extensibility/ux-guidelines/media/0303-049-dropdownselectionfieldpressed.png "0303 049_DropdownSelectionFieldPressed")  
  
  **Campo de seleção**  
  
  Informações preliminares  
  
  `Environment.DropDownMouseDownBackground`  
  
  Em primeiro plano (texto)  
  
  `Environment.DropDownMouseDownText`  
  
  Borda  
  
  `Environment.DropDownMouseDownBorder`  
  
  Separador  
  
  `Environment.DropDownButtonMouseDownSeparator`  
  
  ![Remova&#45;para baixo do botão foi pressionado](../../extensibility/ux-guidelines/media/0303-050-dropdownbuttonpressed.png "0303 050_DropdownButtonPressed")  
  
  **Botão suspenso**  
  
  Informações preliminares  
  
  `Environment.DropDownButtonMouseDownBackground`  
  
  Em primeiro plano (glifo)  
  
  `Environment.DropDownMouseDownGlyph`  
  
  **Desabilitado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Remova&#45;para baixo de campo de seleção desabilitado](../../extensibility/ux-guidelines/media/0303-051-dropdownselectionfielddisabled.png "0303 051_DropdownSelectionFieldDisabled")  
  
  Informações preliminares  
  
  `Environment.DropDownDisabledBackground`  
  
  Em primeiro plano (texto)  
  
  `Environment.DropDownDisabledText`  
  
  Borda  
  
  `Environment.DropDownDisabledBorder`  
  
  Separador  
  
  Nenhum separador  
  
  ![Remova&#45;para baixo do botão desabilitado](../../extensibility/ux-guidelines/media/0303-052-dropdownbuttondisabled.png "0303 052_DropdownButtonDisabled")  
  
  Informações preliminares  
  
  N/D  
  
  Em primeiro plano (glifo)  
  
  `Environment.DropDownDisabledGlyph`  
  
#### <a name="split-button"></a>Botão de divisão  
 Botões de divisão compartilham muitos nomes de token com outros controles de barra de comando, como botões, menus e texto da barra de comando. Todas as ações necessárias e nomes de token do botão suspenso são repetidos aqui para sua conveniência. Listas de lista suspensa do botão de divisão são implementações de barra de comandos [Menus](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandMenus).  
  
 ![Aplicar linhas vermelhas no botão de divisão](../../extensibility/ux-guidelines/media/0303-053-splitbuttonredline.png "0303 053_SplitButtonRedline")  
  
 Use...  
 Quando você está criando um botão de divisão personalizado.  
  
 Não use...  
 -   para outros tipos de botões.  
  
- em qualquer combinação de plano de fundo/primeiro plano diferente do especificado.  
  
  **Padrão**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Botão de divisão](../../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303 054_SplitButton")  
  
  **Botão de divisão (padrão)**  
  
  Informações preliminares  
  
  Nenhum  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextActive`  
  
  Em primeiro plano (glifo)  
  
  `Environment.CommandBarSplitButtonGlyph`  
  
  Borda  
  
  N/D  
  
  Separador  
  
  N/D  
  
  **Passe o mouse**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Botão de divisão focalizar](../../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303 055_SplitButtonHover")  
  
  **Botão de divisão (em foco)**  
  
  Informações preliminares  
  
  `Environment.CommandBarMouseOverBackgroundBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextHover`  
  
  Em primeiro plano (glifo)  
  
  `Environment.CommandBarSplitButtonMouseOverGlyph`  
  
  Borda  
  
  `Environment.CommandBarBorder`  
  
  Separador  
  
  `Environment.CommandBarSplitButtonSeparator`  
  
  **Pressionado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Botão de divisão pressionado](../../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303 056_SplitButtonPressed")  
  
  **Botão de divisão (pressionado)**  
  
  Informações preliminares  
  
  `Environment.CommandBarMouseDownBackgroundBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto)  
  
  `Environment.CommandBarTextMouseDown`  
  
  Em primeiro plano (glifo)  
  
  `Environment.CommandBarSplitButtonMouseDownGlyph`  
  
  Borda  
  
  `Environment.CommandBarBorder`  
  
  Separador  
  
  N/D  
  
  **Desabilitado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Botão de divisão desabilitada](../../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303 057_SplitButtonDisabled")  
  
  **Botão de divisão (desabilitado)**  
  
  Informações preliminares  
  
  N/D  
  
  Em primeiro plano (texto)  
  
  `Environment.ComboBoxItemTextInactive`  
  
  Em primeiro plano (glifo)  
  
  `Environment.CommandBarTextInactive`  
  
  Borda  
  
  N/D  
  
  Separador  
  
  N/D  
  
#### <a name="more-options-and-overflow-buttons"></a>'Mais opções' e 'Overflow' botões  
 O botão "Mais opções" é usado quando um grupo de barra de comandos é personalizável pelo adicionando ou removendo os botões da barra de comando relacionado. O botão de "Estouro" aparece quando uma barra de comandos é truncada devido à falta de espaço horizontal e clique mostra um menu que contém os botões da barra de comando que não podem ser exibidos. Cores desses dois botões são controladas pelo mesmo conjunto de nomes de token.  
  
 ![Mais opções de corte de funcionários](../../extensibility/ux-guidelines/media/0303-058-moreoptionsredline.png "0303 058_MoreOptionsRedline")  
  
 Use...  
 para personalizado 'mais opções' ou 'Overflow' botões.  
  
 Não use...  
 para os botões que não têm uma funcionalidade semelhante a um 'Mais opções' ou o botão de 'estouro de '.  
  
 **Padrão**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Mais opções](../../extensibility/ux-guidelines/media/0303-059-moreoptions.png "0303 059_MoreOptions")  
  
 **Mais opções**  
  
 ![Botão de estouro](../../extensibility/ux-guidelines/media/0303-060-overflow.png "0303 060_Overflow")  
  
 **estouro**  
  
 Informações preliminares  
  
 `Environment.CommandBarOptionsBackground`  
  
 Em primeiro plano (glifo)  
  
 `Environment.CommandBarOptionsGlyph`  
  
 **Passe o mouse**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Mais opções ao focalizar](../../extensibility/ux-guidelines/media/0303-061-moreoptionshover.png "0303 061_MoreOptionsHover")  
  
 **Mais opções**  
  
 ![Ao passar de estouro](../../extensibility/ux-guidelines/media/0303-062-overflowoptions.png "0303 062_OverflowOptions")  
  
 **estouro**  
  
 Informações preliminares  
  
 `Environment.CommandBarOptionsMouseOverBackgroundBegin`  
  
 Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
 Em primeiro plano (glifo)  
  
 `Environment.CommandBarOptionsMouseDownGlyph`  
  
 **Pressionado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Mais opções pressionado](../../extensibility/ux-guidelines/media/0303-063-moreoptionspressed.png "0303 063_MoreOptionsPressed")  
  
 **Mais opções**  
  
 ![Estouro pressionado](../../extensibility/ux-guidelines/media/0303-064-overflowpressed.png "0303 064_OverflowPressed")  
  
 **estouro**  
  
 Informações preliminares  
  
 `Environment.CommandBarOptionsMouseDownBackgroundBegin`  
  
 Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
 Em primeiro plano (glifo)  
  
 `Environment.CommandBarOptionsMouseDownGlyph`  
  
## <a name="document-windows"></a>Janelas de documento  
 Não é necessário para replicar as janelas de documento, porque eles são fornecidos pelo ambiente do Visual Studio. No entanto, você pode decidir o que você deseja aproveitar as cores usadas em janelas de documento para que sua interface do usuário apareça sempre consistente com essa parte do ambiente do Visual Studio.  
  
 Ao usar tokens de cor de janela de documento, você deve ter cuidado para usá-los somente para elementos semelhantes e sempre em pares. Se você não fizer isso, você terá resultados inesperados em sua interface do usuário.  
  
### <a name="document-window-frame"></a>Quadro de janela de documento  
 Janelas de documento podem ser encaixada no IDE ou flutuante como uma janela separada. Quando uma janela de documento é flutuante fora do IDE, ele ainda se encontra em um bem de documento e tem o plano de fundo, borda, texto e guia de cores que é os mesmos de quando ele é parte do IDE. No entanto, o documento se encontra dentro de um quadro que tem seu próprio plano de fundo, borda e cores do texto. Quando as janelas de ferramentas são encaixadas do poço de documento, eles herdam o comportamento e a cor de suas guias de nomes de token de janela do documento.  
  
 ![Corte de funcionários da janela do documento encaixado](../../extensibility/ux-guidelines/media/0303-065-dockeddocumentwindowredline.png "0303 065_DockedDocumentWindowRedline")  
  
 **Janela encaixada de documento**  
  
 ![Janela de documentos flutuante corte de funcionários](../../extensibility/ux-guidelines/media/0303-066-floatingdocumentwindowredline.png "0303 066_FloatingDocumentWindowRedline")  
  
 **Janela de documentos flutuante**  
  
 Use...  
 em qualquer lugar você está criando a interface do usuário que você deseja correspondência com a janela do documento.  
  
 Não use...  
 para qualquer interface do usuário que você não deseja automaticamente alterado se o shell tem uma atualização de tema.  
  
 **Padrão**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 Documento: encaixado ou flutuante  
  
 Informações preliminares  
  
 Depende do tipo de documento  
  
 Em primeiro plano (texto)  
  
 Depende do tipo de documento  
  
 Borda  
  
 `Environment.ToolWindowBorder`  
  
 ![Quadro com foco](../../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303 067_FrameFocused")  
  
 **Quadro: flutuante, com foco**  
  
 Informações preliminares  
  
 `Environment.ToolWindowFloatingFrame`  
  
 Em primeiro plano (texto)  
  
 `Environment.ToolWindowFloatingFrame`  
  
 Em primeiro plano (glifo)  
  
 `Environment.RaftedWindowButtonActiveGlyph`  
  
 Borda  
  
 `Environment.MainWindowActiveDefaultBorder`  
  
 Borda (glifo)  
  
 `Environment.RaftedWindowButtonActiveBorder`  
  
 Definido como transparente  
  
 ![Quadro sem foco](../../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303 068_FrameUnfocused")  
  
 **Quadro: flutuante, sem foco**  
  
 Informações preliminares  
  
 `Environment.ToolWindowFloatingFrameInactive`  
  
 Em primeiro plano (texto)  
  
 `Environment.ToolWindowFloatingFrameInactive`  
  
 Em primeiro plano (glifo)  
  
 `Environment.RaftedWindowButtonInactiveGlyph`  
  
 Borda  
  
 `Environment.MainWindowInactiveBorder`  
  
 Borda (glifo)  
  
 `Environment.RaftedWindowButtonInactiveBorder`  
  
 Definido como transparente  
  
 **Passe o mouse**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Quadro com foco ao passar](../../extensibility/ux-guidelines/media/0303-069-framefocusedhover.png "0303 069_FrameFocusedHover")  
  
 **Quadro: flutuante, com foco**  
  
 Em segundo plano (glifo)  
  
 `Environment.RaftedWindowButtonHoverActive`  
  
 Em primeiro plano (glifo)  
  
 `Environment.RaftedWindowButtonHoverActiveGlyph`  
  
 Borda (glifo)  
  
 `Environment.RaftedWindowButtonHoverActiveBorder`  
  
 ![Quadro sem foco ao passar](../../extensibility/ux-guidelines/media/0303-070-frameunfocusedhover.png "0303 070_FrameUnfocusedHover")  
  
 **Quadro: flutuante, sem foco**  
  
 Em segundo plano (glifo)  
  
 `EnvironmentRaftedWindowButtonHoverInactive`  
  
 Em primeiro plano (glifo)  
  
 `Environment.RaftedWindowButtonHoverInactiveGlyph`  
  
 Borda (glifo)  
  
 `Environment.RaftedWindowButtonHoverInactiveBorder`  
  
 **Pressionado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Quadro com foco pressionado](../../extensibility/ux-guidelines/media/0303-071-framefocusedpressed.png "0303 071_FrameFocusedPressed")  
  
 **Quadro: flutuante, com foco**  
  
 Em segundo plano (glifo)  
  
 `Environment.RaftedWindowButtonDown`  
  
 Em primeiro plano (glifo)  
  
 `Environment.RaftedWindowButtonDownGlyph`  
  
 Borda (glifo)  
  
 `Environment.RaftedWindowButtonDownBorder`  
  
### <a name="document-tabs"></a>Guias de documento  
 Guias do documento ficam no canal de guia para indicar quais documentos estão abertos no momento, junto com o qual é o atual selecionado ou o documento ativo. Janelas de ferramenta também podem ser encaixadas no canal de guia de documento, se o usuário coloca lá. Nessa situação, eles usam as mesmas cores do guia como janelas de documentos. Se você estiver criando interface do usuário que você deseja sempre coincidir com as cores da janela de documento (incluindo atualizações de tema ou se novos temas instalados), em seguida, fazer referência a esses tokens de cor.  
  
 ![Aplicar linhas vermelhas no guia de documento](../../extensibility/ux-guidelines/media/0303-072-documenttabredline.png "0303 072_DocumentTabRedline")  
  
 Use...  
 em qualquer lugar você está criando a interface do usuário que você deseja corresponder guias do documento e separar automaticamente atualizações do tema ou novas cores de tema.  
  
 Não use...  
 para qualquer interface do usuário que você não deseja alterar automaticamente quando o shell tem um tema de atualização.  
  
#### <a name="open-document-tabs"></a>Guias de documento aberto  
 Cada documento aberto tem uma guia no canal de guia de documento que exibe seu nome. Documentos podem ser selecionados ou abra em segundo plano, e suas guias refletem esses estados:  
  
- A guia selecionada representa o documento que está sendo exibido no documento bem. Uma guia selecionada tem uma borda de documento que estende bem em toda a borda superior do documento.  
  
- Guias de plano de fundo são guias qualquer documento que não estão na guia selecionada no momento. Quando clicado, eles tornam-se a guia selecionada e adquirem todas as cores de plano de fundo, borda e texto desses nomes de token.  
  
  ![Aplicar linhas vermelhas no guia de documento aberto](../../extensibility/ux-guidelines/media/0303-073-opendocumenttabredline.png "0303 073_OpenDocumentTabRedline")  
  
  Use...  
  Quando você estiver criando guias de documento personalizado.  
  
  Não use...  
  -   as guias de provisionados (visualização).  
  
- para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tem uma atualização de tema.  
  
#### <a name="selected-tab"></a>Guia selecionada  
 **Com foco**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Guia selecionada focado](../../extensibility/ux-guidelines/media/0303-074-selectedtabfocused.png "0303 074_SelectedTabFocused")  
  
 **Guia de documento selecionado, com foco**  
  
 Informações preliminares  
  
 `Environment.FileTabSelectedGradientTop`  
  
 Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
 Em primeiro plano (texto)  
  
 `Environment.FileTabSelectedText`  
  
 Borda  
  
 `Environment.FileTabSelectedBorder`  
  
 Defina a mesma cor do plano de fundo.  
  
 Borda de documento  
  
 `Environment.FileTabDocumentBorderBackground`  
  
 **Sem foco**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![A guia selecionada sem foco](../../extensibility/ux-guidelines/media/0303-075-selectedtabunfocused.png "0303 075_SelectedTabUnfocused")  
  
 **Guia de documento selecionado, sem foco**  
  
 Informações preliminares  
  
 `Environment.FileTabInactiveGradientTop`  
  
 Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
 Em primeiro plano (texto)  
  
 `Environment.FileTabInactiveText`  
  
 Borda  
  
 `Environment.FileTabInactiveBorder`  
  
 Defina a mesma cor do plano de fundo.  
  
 Borda de documento  
  
 `Environment.FileTabInactiveDocumentBorderBackground`  
  
#### <a name="background-tab"></a>Guia de plano de fundo  
 **Padrão**  
  
 ![Guia de plano de fundo](../../extensibility/ux-guidelines/media/0303-076-backgroundtab.png "0303 076_BackgroundTab")  
  
 **Padrão de guia de plano de fundo**  
  
 Informações preliminares  
  
 `Environment.FileTabBackground`  
  
 Em primeiro plano (texto)  
  
 `Environment.FileTabText`  
  
 Borda  
  
 `Environment.FileTabBorder`  
  
 Defina a mesma cor do plano de fundo.  
  
 **Passe o mouse**  
  
 ![Guia de plano de fundo ao focalizar](../../extensibility/ux-guidelines/media/0303-077-backgroundtabhover.png "0303 077_BackgroundTabHover")  
  
 **Guia de plano de fundo ao focalizar**  
  
 Informações preliminares  
  
 `Environment.FileTabHotGradientTop`  
  
 Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
 Em primeiro plano (texto)  
  
 `Environment.FileTabHotText`  
  
 Borda  
  
 `Environment.FileTabHotBorder`  
  
 Defina a mesma cor do plano de fundo.  
  
#### <a name="preview-tab"></a>Guia de visualização  
 Na guia Visualização aparece à direita do canal de guia de documento quando o usuário clica em um item na janela da ferramenta Gerenciador de soluções. Ele atua como uma visualização do documento e também fornece ao usuário a opção para manter o documento aberto no lado esquerdo do canal de guia de documento. Guia de apenas uma visualização aberta pode ser aberto por vez. Guias de visualização têm ambos em segundo plano e estados selecionados, como guias abertas e pode ser focalizado ou sem foco em seu estado ativo.  
  
 ![Aplicar linhas vermelhas no guia de visualização](../../extensibility/ux-guidelines/media/0303-078-previewtabredline.png "0303 078_PreviewTabRedline")  
  
 Use...  
 em qualquer lugar, você está criando o preview provisória e deseja que algum elemento para coincidir com a cor de guia de visualização atual.  
  
 Não use...  
 -   para qualquer tipo de documento ou a guia não é provisório (visualização).  
  
- para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tem uma atualização de tema.  
  
  **Guia de visualização selecionado: focalizado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Guia de visualização focado](../../extensibility/ux-guidelines/media/0303-079-previewtabfocused.png "0303 079_PreviewTabFocused")  
  
  **Guia de visualização com foco**  
  
  Informações preliminares  
  
  `Environment.FileTabProvisionalSelectedActive`  
  
  Em primeiro plano (texto)  
  
  `Environment.FileTabProvisionalSelectedActiveForeground`  
  
  Borda  
  
  `Environment.FileTabProvisionalSelectedActiveBorder`  
  
  Defina a mesma cor do plano de fundo.  
  
  Borda de documento  
  
  `Environment.FileTabProvisionalSelectedActiveBorder`  
  
  **Guia de visualização selecionado: sem foco**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Guia de visualização sem foco](../../extensibility/ux-guidelines/media/0303-080-previewtabunfocused.png "0303 080_PreviewTabUnfocused")  
  
  **Guia de visualização sem foco**  
  
  Informações preliminares  
  
  `Environment.FileTabProvisionalSelectedInactive`  
  
  Em primeiro plano (texto)  
  
  `Environment.FileTabProvisionalSelectedInactiveForeground`  
  
  Borda  
  
  `Environment.FileTabProvisionalSelectedInactiveBorder`  
  
  Borda de documento  
  
  `Environment.FileTabProvisionalSelectedInactiveBorder`  
  
  **Guia de visualização do plano de fundo: padrão**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Guia de plano de fundo de visualização](../../extensibility/ux-guidelines/media/0303-081-previewbackgroundtab.png "0303 081_PreviewBackgroundTab")  
  
  **Guia de plano de fundo do guia de visualização**  
  
  Informações preliminares  
  
  `Environment.FileTabProvisionalInactive`  
  
  Em primeiro plano (texto)  
  
  `Environment.FileTabProvisionalInactiveForeground`  
  
  Borda  
  
  `Environment.FileTabProvisionalInactiveBorder`  
  
  Defina a mesma cor do plano de fundo.  
  
  **Guia de visualização do plano de fundo: passe o mouse**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Guia de plano de fundo de visualização ao focalizar](../../extensibility/ux-guidelines/media/0303-082-previewbackgroundtabhover.png "0303 082_PreviewBackgroundTabHover")  
  
  **Guia de plano de fundo de guia de visualização ao focalizar**  
  
  Informações preliminares  
  
  `Environment.FileTabProvisionalHover`  
  
  Em primeiro plano (texto)  
  
  `Environment.FileTabProvisionalHoverForeground`  
  
  Borda  
  
  `Environment.FileTabProvisionalHoverBorder`  
  
  Defina a mesma cor do plano de fundo.  
  
#### <a name="document-overflow-button"></a>Botão de estouro de documento  
 O botão de estouro do documento está presente se há um ou mais documentos abertos, independentemente se há espaço vertical na configuração atual de acordo com todas as guias de documento. O menu suspenso de estouro de documento, que é controlado pela **CommandBarMenu** cores (consulte [Menus](../../misc/shared-colors.md#BKMK_CommandMenus)), exibe uma lista de todos os documentos abertos, visíveis e ocultos e as alterações de glifo de estouro Dependendo se todos os documentos abertos são exibidos no canal de guia.  
  
 ![Aplicar linhas vermelhas no estouro](../../extensibility/ux-guidelines/media/0303-083-overflowredline.png "0303 083_OverflowRedline")  
  
 Use...  
 Quando você estiver criando um botão de estouro do documento personalizado.  
  
 Não use...  
 -   para a interface do usuário que não é semelhante a um botão de estouro.  
  
- para botões de estouro da barra de comando.  
  
  **Padrão**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Estouro](../../extensibility/ux-guidelines/media/0303-084-overflow.png "0303 084_Overflow")  
  
  **Botão de estouro de documento**  
  
  Informações preliminares  
  
  `Environment.DocWellOverflowButtonBackground`  
  
  Em primeiro plano (glifo)  
  
  `Environment.DocWellOverflowButtonGlyph`  
  
  Borda  
  
  N/D  
  
  **Passe o mouse**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Ao passar de estouro](../../extensibility/ux-guidelines/media/0303-085-overflowhover.png "0303 085_OverflowHover")  
  
  **Botão de estouro de documento em foco**  
  
  Informações preliminares  
  
  `Environment.DocWellOverflowButtonMouseOverBackground`  
  
  Em primeiro plano (glifo)  
  
  `Environment.DocWellOverflowButtonMouseOverGlyph`  
  
  Borda  
  
  `Environment.DocWellOverflowButtonMouseOverBorder`  
  
  **Pressionado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Estouro pressionado](../../extensibility/ux-guidelines/media/0303-086-overflowpressed.png "0303 086_OverflowPressed")  
  
  **Pressionado o botão de estouro de documento**  
  
  Informações preliminares  
  
  `Environment.DocWellOverflowButtonMouseDownBackground`  
  
  Em primeiro plano (glifo)  
  
  `Environment.DocWellOverflowButtonMouseDownGlyph`  
  
  Borda  
  
  `Environment.DocWellOverflowButtonMouseDownBorder`  
  
## <a name="tool-windows"></a>Janelas de ferramentas  
 Não é necessário para replicar as janelas de ferramentas, porque eles são fornecidos pelo ambiente do Visual Studio. No entanto, você pode decidir o que você deseja aproveitar as cores usadas em janelas de ferramentas para que sua interface do usuário apareça sempre consistente com essa parte do ambiente do Visual Studio.  
  
 ![Corte de funcionários da janela de ferramenta](../../extensibility/ux-guidelines/media/0303-087-toolwindowredline.png "0303 087_ToolWindowRedline")  
  
 Use...  
 em qualquer lugar você está criando a interface do usuário que você deseja correspondência com janelas de ferramentas.  
  
 Não use...  
 para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tem uma atualização de tema.  
  
### <a name="tool-window-frame"></a>Quadro de janela de ferramenta  
 Janelas de ferramenta no Visual Studio são usadas para muitas tarefas diferentes e podem existir em um de vários estados diferentes. Se uma janela de ferramentas estiver aberta, podem ser atribuído a qualquer um dos quatro lados da área do documento. Janelas de ferramenta também podem flutuar fora do IDE, o que lhes permite ser reposicionadas em qualquer lugar na tela do usuário. Janelas flutuantes sempre ficam na parte superior do IDE. Por fim, as janelas de ferramentas podem ser encaixadas como janelas de documentos e aparecem como uma guia no documento bem. Janelas de ferramentas que foram encaixadas como janelas de documentos são coloridas em parte, usando nomes de token de janela do documento.  
  
 ![Aplicar linhas vermelhas no quadro de janela de ferramenta](../../extensibility/ux-guidelines/media/0303-088-toolwindowframeredline.png "0303 088_ToolWindowFrameRedline")  
  
 Use...  
 em qualquer lugar você está criando a interface do usuário que você deseja correspondência com janelas de ferramentas.  
  
 Não use...  
 para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tem uma atualização de tema.  
  
 **Encaixado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Janela de ferramenta encaixada](../../extensibility/ux-guidelines/media/0303-089-toolwindowdocked.png "0303 089_ToolWindowDocked")  
  
 Informações preliminares  
  
 `Environment.ToolWindowBackground`  
  
 Borda  
  
 `Environment.ToolWindowBorder`  
  
 **Flutuante: focalizado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Janela de ferramenta focada](../../extensibility/ux-guidelines/media/0303-090-toolwindowfocused.png "0303 090_ToolWindowFocused")  
  
 Informações preliminares  
  
 `Environment.ToolWindowBackground`  
  
 Borda  
  
 `Environment.MainWindowActiveDefaultBorder`  
  
 **Flutuante: sem foco**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Janela da ferramenta sem foco](../../extensibility/ux-guidelines/media/0303-091-toolwindowunfocused.png "0303 091_ToolWindowUnfocused")  
  
 Informações preliminares  
  
 `Environment.ToolWindowBackground`  
  
 Borda  
  
 `Environment.MainWindowInactiveBorder`  
  
### <a name="tool-window-title-bar"></a>Barra de título de janela de ferramenta  
 A borda da barra de título não é uma borda true, mas uma linha espessa na parte superior da barra de título. Ele não tem um nome de token para seu estado sem foco.  
  
 ![Corte de funcionários da barra de título de janela de ferramenta](../../extensibility/ux-guidelines/media/0303-092-toolwindowtitlebarredline.png "0303 092_ToolWindowTitleBarRedline")  
  
 Use...  
 em qualquer lugar você está criando a interface do usuário que você deseja correspondência com janelas de ferramentas.  
  
 Não use...  
 para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tem uma atualização de tema.  
  
 **Com foco**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Barra de título focado](../../extensibility/ux-guidelines/media/0303-093-titlebarfocused.png "0303 093_TitleBarFocused")  
  
 **Barra de título focalizado**  
  
 Informações preliminares  
  
 `Environment.TitleBarActiveGradientBegin`  
  
 Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
 Em primeiro plano (texto)  
  
 `Environment.TitleBarActiveText`  
  
 Borda  
  
 `Environment.TitleBarActiveBorder`  
  
 Defina a mesma cor do plano de fundo.  
  
 Arraste a alça  
  
 `Environment.TitleBarDragHandleActive`  
  
 **Sem foco**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Barra de título sem foco](../../extensibility/ux-guidelines/media/0303-094-titlebarunfocused.png "0303 094_TitleBarUnfocused")  
  
 **Barra de título sem foco**  
  
 Informações preliminares  
  
 `Environment.TitleBarInactiveGradientBegin`  
  
 Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
 Em primeiro plano (texto)  
  
 `Environment.TitleBarInactiveText`  
  
 Borda  
  
 N/D  
  
 Arraste a alça  
  
 `Environment.TitleBarDragHandle`  
  
#### <a name="title-bar-buttons"></a>Botões da barra de título  
 ![Aplicar linhas vermelhas no botão da barra de título](../../extensibility/ux-guidelines/media/0303-095-titlebarbuttonredline.png "0303 095_TitleBarButtonRedline")  
  
 Use...  
 para os botões que aparecem na interface do usuário que usa tokens de cor das barras de título da janela de ferramenta.  
  
 Não use...  
 -   para os botões que aparecem em outros locais.  
  
- em qualquer combinação de plano de fundo/primeiro plano diferente do especificado.  
  
  **Padrão**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Botão com foco da barra de título](../../extensibility/ux-guidelines/media/0303-096-titlebarbuttonfocused.png "0303 096_TitleBarButtonFocused")  
  
  **Com foco**  
  
  Informações preliminares  
  
  N/D  
  
  Em primeiro plano (glifo)  
  
  `Environment.ToolWindowButtonActiveGlyph`  
  
  Borda  
  
  N/D  
  
  ![Foco do botão da barra de título](../../extensibility/ux-guidelines/media/0303-097-titlebarbuttonunfocused.png "0303 097_TitleBarButtonUnfocused")  
  
  **Sem foco**  
  
  Informações preliminares  
  
  N/D  
  
  Em primeiro plano (glifo)  
  
  `Environment.ToolWindowButtonInactiveGlyph`  
  
  Borda  
  
  N/D  
  
  **Passe o mouse**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Botão da barra de título com o foco ao passar](../../extensibility/ux-guidelines/media/0303-098-titlebarbuttonfocusedhover.png "0303 098_TitleBarButtonFocusedHover")  
  
  **Com foco**  
  
  Informações preliminares  
  
  `Environment.ToolWindowButtonHoverActive`  
  
  Em primeiro plano (glifo)  
  
  `Environment.ToolWindowButtonHoverActiveGlyph`  
  
  Borda  
  
  `Environment.ToolWindowButtonHoverActiveBorder`  
  
  ![Sem foco ao passar de botão da barra de título](../../extensibility/ux-guidelines/media/0303-099-titlebarbuttonunfocusedhover.png "0303 099_TitleBarButtonUnfocusedHover")  
  
  **Sem foco**  
  
  Informações preliminares  
  
  `Environment.ToolWindowButtonHoverInactive`  
  
  Em primeiro plano (glifo)  
  
  `Environment.ToolWindowButtonHoverInactiveGlyph`  
  
  Borda  
  
  `Environment.ToolWindowButtonHoverInactiveBorder`  
  
  **Pressionado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Botão com foco e pressionado da barra de título](../../extensibility/ux-guidelines/media/0303-100-titlebarbuttonfocusedpressed.png "0303 100_TitleBarButtonFocusedPressed")  
  
  **Com foco**  
  
  Informações preliminares  
  
  `Environment.ToolWindowButtonDown`  
  
  Em primeiro plano (glifo)  
  
  `Environment.ToolWindowButtonDownActiveGlyph`  
  
  Borda  
  
  `Environment.ToolWindowButtonDownBorder`  
  
  ![Botão de barra de título sem foco e pressionado](../../extensibility/ux-guidelines/media/0303-101-titlebarbuttonunfocusedpressed.png "0303 101_TitleBarButtonUnfocusedPressed")  
  
  **Sem foco**  
  
  Informações preliminares  
  
  `Environment.ToolWindowButtonDown`  
  
  Em primeiro plano (glifo)  
  
  `Environment.ToolWindowButtonDownInactiveGlyph`  
  
  Borda  
  
  `Environment.ToolWindowButtonDownBorder`  
  
### <a name="tool-window-tabs"></a>Guias da janela de ferramenta  
 ![Aplicar linhas vermelhas no guia da janela de ferramenta](../../extensibility/ux-guidelines/media/0303-102-toolwindowtabredline.png "0303 102_ToolWindowTabRedline")  
  
 Use...  
 em qualquer lugar você está criando a interface do usuário que você deseja correspondência com janelas de ferramentas.  
  
 Não use...  
 para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tem uma atualização de tema.  
  
 **Guia selecionada**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Guia da janela de ferramenta focado](../../extensibility/ux-guidelines/media/0303-103-toolwindowtabfocused.png "0303 103_ToolWindowTabFocused")  
  
 **Guia da janela de ferramenta selecionada, com foco**  
  
 Informações preliminares  
  
 `Environment.ToolWindowTabSelectedTab`  
  
 Em primeiro plano (texto)  
  
 `Environment.ToolWindowTabSelectedActiveText`  
  
 Borda  
  
 `Environment.ToolWindowTabSelectedBorder`  
  
 Defina a mesma cor do plano de fundo.  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Guia de janela da ferramenta sem foco](../../extensibility/ux-guidelines/media/0303-104-toolwindowtabunfocused.png "0303 104_ToolWindowTabUnfocused")  
  
 **Guia da janela de ferramenta selecionada, sem foco**  
  
 Informações preliminares  
  
 `Environment.ToolWindowTabSelectedTab`  
  
 Em primeiro plano (texto)  
  
 `Environment.ToolWindowTabSelectedText`  
  
 Borda  
  
 `Environment.ToolWindowTabSelectedBorder`  
  
 Defina a mesma cor do plano de fundo.  
  
 **Guia de plano de fundo**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Guia de plano de fundo da janela de ferramenta](../../extensibility/ux-guidelines/media/0303-105-toolwindowbackgroundtab.png "0303 105_ToolWindowBackgroundTab")  
  
 **Guia de janela de ferramenta do plano de fundo**  
  
 Informações preliminares  
  
 `Environment.ToolWindowTabGradientBegin`  
  
 Marcas de gradiente definido como o mesmo valor de cor no Visual Studio 2013.  
  
 `Environment.ToolWindowTabGradientEnd`  
  
 Marcas de gradiente definido como o mesmo valor de cor no Visual Studio 2013.  
  
 Em primeiro plano (texto)  
  
 `Environment.ToolWindowTabText`  
  
 Borda  
  
 `Environment.ToolWindowTabBorder`  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Guia de plano de fundo de janela de ferramenta ao focalizar](../../extensibility/ux-guidelines/media/0303-106-toolwindowbackgroundtabhover.png "0303 106_ToolWindowBackgroundTabHover")  
  
 **Guia de janela de ferramenta do plano de fundo ao focalizar**  
  
 Informações preliminares  
  
 `Environment.ToolWindowTabMouseOverBackgroundBegin`  
  
 Marcas de gradiente definido como o mesmo valor de cor no Visual Studio 2013.  
  
 `Environment.ToolWindowTabMouseOverBackgroundEnd`  
  
 Marcas de gradiente definido como o mesmo valor de cor no Visual Studio 2013.  
  
 Em primeiro plano (texto)  
  
 `Environment.ToolWindowTabMouseOverText`  
  
 Borda  
  
 `Environment.ToolWindowTabMouseOverBorder`  
  
 Defina a mesma cor do plano de fundo.  
  
### <a name="auto-hide-tabs"></a>Guias de ocultar automaticamente  
 ![Automático&#45;aplicar linhas vermelhas no ocultar](../../extensibility/ux-guidelines/media/0303-107-autohideredline.png "0303 107_AutoHideRedline")  
  
 Use...  
 em qualquer lugar você está criando a interface do usuário que você deseja correspondência com guias da janela de ferramenta ocultos automaticamente.  
  
 Não use...  
 para qualquer interface do usuário que você não deseja alterar automaticamente se o shell tem uma atualização de tema.  
  
 **Padrão**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Automático&#45;ocultar a guia](../../extensibility/ux-guidelines/media/0303-108-autohidetab.png "0303 108_AutoHideTab")  
  
 **Guia de ocultação automática padrão**  
  
 Informações preliminares  
  
 `Environment.AutoHideTabBackgroundBegin`  
  
 Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
 Em primeiro plano (texto)  
  
 `Environment.AutoHideTabText`  
  
 Borda  
  
 `Environment.AutoHideTabBorder`  
  
 **Passe o mouse**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Automático&#45;Ocultar guia focalizar](../../extensibility/ux-guidelines/media/0303-109-autohidetabhover.png "0303 109_AutoHideTabHover")  
  
 **Guia de ocultamento automático ao focalizar**  
  
 Informações preliminares  
  
 `Environment.AutoHideTabMouseOverBackgroundBegin`  
  
 Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
 Em primeiro plano (texto)  
  
 `Environment.AutoHideTabMouseOverText`  
  
 Borda  
  
 `Environment.AutoHideTabMouseOverBorder`  
  
## <a name="common-shared-controls"></a>Controles compartilhados comuns  
 Quando você usa uma barra de comandos padrão do Visual Studio em seu recurso, você terá acesso aos controles de shell com estilo, e você deve não re-modelo desses controles comuns. No entanto, se você precisar criar uma barra de comandos personalizada, você precisa criar controles personalizados também. Nesse caso, certifique-se de usar os nomes de token corretos para cada um dos seguintes controles para que sua interface do usuário seja consistente com o restante do Visual Studio.  
  
### <a name="search-box"></a>Caixa de pesquisa  
 Sempre que possível, use o controle de pesquisa comum fornecido pelo ambiente do Visual Studio. Cores de caixa de pesquisa são encontradas na categoria "SearchControl" no **ShellColors.pkgdef** arquivo, que contém nomes de token para o campo de entrada, o botão de ação, o botão suspenso e o menu suspenso.  
  
 Uma caixa de pesquisa pode ser um dos vários estados, algumas das quais são mutuamente exclusivas:  
  
- "Concentradas" ou "sem foco" refere-se a ou não o cursor estiver na caixa de texto.  
  
- "Active" ou "inativos" refere-se de se o usuário inseriu uma consulta de pesquisa na caixa de texto.  
  
- "Passagem" significa que o usuário tem moused sobre a caixa de pesquisa com o mouse (esse estado substitui todos os outros estados).  
  
- "Desabilitada" significa que a funcionalidade de pesquisa está desativada para o contexto atual.  
  
  ![Corte de caixa de pesquisa de funcionários](../../extensibility/ux-guidelines/media/0303-110-searchboxredline.png "0303 110_SearchBoxRedline")  
  
  Use...  
  Quando você estiver criando uma caixa de pesquisa personalizada.  
  
  Não use...  
  -   para qualquer coisa que não é uma caixa de pesquisa.  
  
- para qualquer coisa que você não deseja sempre correspondem à pesquisa de caixa de interface do usuário.  
  
  **Com foco**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Campo de entrada de pesquisa focado](../../extensibility/ux-guidelines/media/0303-111-searchinputfieldfocused.png "0303 111_SearchInputFieldFocused")  
  
  **Campo de entrada**  
  
  Informações preliminares  
  
  `SearchControl.FocusedBackground`  
  
  Em primeiro plano (texto)  
  
  `SearchControl.FocusedBackground`  
  
  Borda  
  
  `SearchControl.FocusedBorder`  
  
  Separador  
  
  `SearchControl.FocusedDropDownSeparator`  
  
  ![Botão de ação de pesquisa com foco](../../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303 112_SearchActionButtonFocused")  
  
  **Botão de ação**  
  
  Informações preliminares  
  
  Nenhum  
  
  Em primeiro plano (glifo de pesquisa)  
  
  `SearchControl.SearchGlyph`  
  
  Em primeiro plano (Stop glifo)  
  
  `SearchControl.StopGlyph`  
  
  Em primeiro plano (glifo não criptografado)  
  
  `SearchControl.ClearGlyph`  
  
  Borda  
  
  N/D  
  
  ![Lista de pesquisa&#45;para baixo do botão com foco](../../extensibility/ux-guidelines/media/0303-113-searchdropdownbuttonfocused.png "0303 113_SearchDropdownButtonFocused")  
  
  **Botão suspenso**  
  
  Informações preliminares  
  
  `SearchControl.FocusedDropDownButton`  
  
  Em primeiro plano (glifo)  
  
  `SearchControl.FocusedDropDownButtonGlyph`  
  
  Borda  
  
  `SearchControl.FocusedDropDownButtonBorder`  
  
  **Sem foco**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Campo de pesquisa sem foco](../../extensibility/ux-guidelines/media/0303-114-searchinputfieldunfocused.png "0303 114_SearchInputFieldUnfocused")  
  
  **Campo de entrada ativo**  
  
  Informações preliminares  
  
  `SearchControl.SearchActiveBackground`  
  
  Em primeiro plano (texto)  
  
  `SearchControl.SearchActiveBackground`  
  
  Borda  
  
  `SearchControl.UnfocusedBorder`  
  
  Separador  
  
  `SearchControl.DropDownSeparator`  
  
  ![Campo de entrada de pesquisa sem foco e inativo](../../extensibility/ux-guidelines/media/0303-114-1-searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")  
  
  **Campo de entrada inativo**  
  
  Informações preliminares  
  
  `SearchControl.Unfocused`  
  
  Em primeiro plano (texto)  
  
  `SearchControl.Unfocused`  
  
  Borda  
  
  `SearchControl.UnfocusedBorder`  
  
  Separador  
  
  `SearchControl.DropDownSeparator`  
  
  ![Botão de ação de pesquisa sem foco](../../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303 115_SearchActionButtonUnfocused")  
  
  **Botão de ação**  
  
  Informações preliminares  
  
  N/D  
  
  Em primeiro plano (glifo de pesquisa)  
  
  `SearchControl.SearchGlyph`  
  
  Em primeiro plano (Stop glifo)  
  
  `SearchControl.StopGlyph`  
  
  Em primeiro plano (glifo não criptografado)  
  
  `SearchControl.ClearGlyph`  
  
  Borda  
  
  N/D  
  
  ![Lista de pesquisa&#45;para baixo do botão sem foco](../../extensibility/ux-guidelines/media/0303-116-searchdropdownbuttonunfocused.png "0303 116_SearchDropdownButtonUnfocused")  
  
  **Botão suspenso**  
  
  Informações preliminares  
  
  `SearchControl.UnfocusedDropDownButton`  
  
  Em primeiro plano (glifo)  
  
  `SearchControl.UnfocusedDropDownButtonGlyph`  
  
  Borda  
  
  `SearchControl.UnfocusedDropDownButtonBorder`  
  
  **Pressionado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Botão de ação de pesquisa pressionado](../../extensibility/ux-guidelines/media/0303-116-1-searchactionbuttonpressed.png "0303-116-1_SearchActionButtonPressed")  
  
  **Botão de ação**  
  
  Informações preliminares  
  
  `SearchControl.ActionButtonMouseDown`  
  
  Em primeiro plano (glifo)  
  
  `SearchControl.ActionButtonMouseDownGlyph`  
  
  Borda  
  
  `SearchControl.ActionButtonMouseDownBorder`  
  
  ![Lista de pesquisa&#45;para baixo do botão foi pressionado](../../extensibility/ux-guidelines/media/0303-116-2-searchdropdownbuttonpressed.png "0303-116-2_SearchDropdownButtonPressed")  
  
  **Botão suspenso**  
  
  Informações preliminares  
  
  `SearchControl.MouseDownDropDownButton`  
  
  Em primeiro plano (glifo)  
  
  `SearchControl.MouseDownDropDownButtonGlyph`  
  
  Borda  
  
  `SearchControl.MouseDownDropDownButtonBorder`  
  
  **(Texto realçado somente)**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Realce de campo de entrada de pesquisa](../../extensibility/ux-guidelines/media/0303-120-searchinputfieldhighlight.png "0303 120_SearchInputFieldHighlight")  
  
  **Campo de entrada com o texto realçado**  
  
  Informações preliminares  
  
  `SearchControl.Selection`  
  
  Em primeiro plano (texto)  
  
  `SearchControl.FocusedBackground`  
  
  Borda  
  
  Nenhum  
  
  Separador  
  
  `SearchControl.FocusedDropDownSeparator`  
  
  **Desabilitado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Campo de entrada de pesquisa desabilitado](../../extensibility/ux-guidelines/media/0303-121-searchinputfielddisabled.png "0303 121_SearchInputFieldDisabled")  
  
  **Campo de entrada**  
  
  Informações preliminares  
  
  `SearchControl.Disabled`  
  
  Em primeiro plano (texto)  
  
  `SearchControl.Disabled`  
  
  Borda  
  
  `SearchControl.DisabledBorder`  
  
  Separador  
  
  `SearchControl.DropDownSeparator`  
  
  ![Botão de ação de pesquisar desabilitada](../../extensibility/ux-guidelines/media/0303-122-searchactionbuttondisabled.png "0303 122_SearchActionButtonDisabled")  
  
  **Botão de ação**  
  
  Informações preliminares  
  
  Nenhum  
  
  Em primeiro plano (glifo)  
  
  `SearchControl.ActionButtonDisabledGlyph`  
  
  Borda  
  
  Nenhum  
  
  ![Lista de pesquisa&#45;para baixo do botão desabilitado](../../extensibility/ux-guidelines/media/0303-123-searchdropdownbuttondisabled.png "0303 123_SearchDropdownButtonDisabled")  
  
  **Botão suspenso**  
  
  Informações preliminares  
  
  Nenhum  
  
  Em primeiro plano (glifo)  
  
  `SearchControl.DisabledDownButtonGlyph`  
  
  Borda  
  
  Nenhum  
  
#### <a name="search-drop-down-lists"></a>Listas suspensas de pesquisa  
 Menu de lista suspensa da caixa de pesquisa tem o potencial para ser um pouco mais complexo do que outros menus suspensos no Visual Studio. As seções de "opções de pesquisa" e "pesquisas sugeridas" pode aparecer sozinha ou em conjunto no menu e cada um deles é colorido separadamente. Uma linha também separa nessas duas seções quando aparecem juntos e uma borda ao redor de menu suspenso de inteiro.  
  
 ![Lista de pesquisa&#45;corte de funcionários para baixo](../../extensibility/ux-guidelines/media/0303-124-searchdropdownredline.png "0303 124_SearchDropdownRedline")  
  
 Use...  
 -   Quando você estiver criando uma lista suspensa de pesquisa personalizada.  
  
- os nomes de token corretos para os componentes da lista correta.  
  
  Não use...  
  -   para listas suspensas, que aparecem em outros contextos.  
  
- em qualquer combinação de plano de fundo/primeiro plano diferente do especificado.  
  
  **Padrão (nenhum outro estado)**  
  
  Elemento  
  
  Nome do token: Category.color  
  
  Borda  
  
  `SearchControl.PopupBorder`  
  
  Separador  
  
  `SearchControl.PopupSectionHeaderSeparator`  
  
  Sombra  
  
  `Environment.DropShadowBackground`  
  
  **Padrão**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Pesquisa sugerida](../../extensibility/ux-guidelines/media/0303-125-searchsuggested.png "0303 125_SearchSuggested")  
  
  **Pesquisas sugeridas**  
  
  Informações preliminares  
  
  `SearchControl.PopupItemsListBackgroundGradientBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto)  
  
  `SearchControl.PopupItemText`  
  
  ![Caixa de seleção de pesquisa](../../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303 126_SearchCheckbox")  
  
  **Opções de pesquisa (caixa de seleção)**  
  
  ![Opções de pesquisa](../../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303 127_SearchOptions")  
  
  **Opções de pesquisa (link)**  
  
  Informações preliminares  
  
  `SearchControl.PopupSectionBackgroundGradientBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (caixa de texto)  
  
  `SearchControl.PopupCheckboxText`  
  
  Em primeiro plano (texto do Link)  
  
  `SearchControl.PopupButtonText`  
  
  Plano de fundo do cabeçalho  
  
  `SearchControl.PopupSectionHeaderGradientBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto do cabeçalho)  
  
  `SearchControl.PopupSectionHeaderText`  
  
  **Passe o mouse**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Pesquisa sugerida focalizar](../../extensibility/ux-guidelines/media/0303-128-searchsuggestedhover.png "0303 128_SearchSuggestedHover")  
  
  **Pesquisas sugeridas**  
  
  Informações preliminares  
  
  `SearchControl.PopupControlMouseOverBackgroundGradientBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto)  
  
  `SearchControl.PopupMouseOverItemText`  
  
  Borda  
  
  `SearchControl.PopupControlMouseOverBorder`  
  
  ![Caixa de seleção de pesquisa ao focalizar](../../extensibility/ux-guidelines/media/0303-129-searchcheckboxhover.png "0303 129_SearchCheckboxHover")  
  
  **Pesquisas sugeridas (caixa de seleção)**  
  
  ![Pesquisar opções ao focalizar](../../extensibility/ux-guidelines/media/0303-130-searchoptionshover.png "0303 130_SearchOptionsHover")  
  
  **Opções de pesquisa**  
  
  Informações preliminares  
  
  `SearchControl.PopupControlMouseOverBackgroundGradientBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (caixa de texto)  
  
  `SearchControl.PopupCheckboxMouseDownText`  
  
  Em primeiro plano (texto do Link)  
  
  `SearchControl.PopupButtonMouseDownText`  
  
  Borda  
  
  `SearchControl.PopupControlMouseOverBorder`  
  
  **Pressionado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Pesquisa sugerido pressionado](../../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303 131_SearchSuggestedPressed")  
  
  **Pesquisas sugeridas (caixa de seleção)**  
  
  ![Pesquisar opções pressionadas](../../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303 132_SearchOptionsPressed")  
  
  **Opções de pesquisa**  
  
  Plano de fundo da caixa de seleção  
  
  `SearchControl.PopupControlMouseDownBackgroundGradientBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  `SearchControl.PopupControlMouseDownBackgroundGradientEnd`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (caixa de texto)  
  
  `SearchControl.PopupCheckboxMouseDownText`  
  
  Plano de fundo do link  
  
  `SearchControl.PopupButtonMouseDownBackgroundGradientBegin`  
  
  Embora não usado na interface do usuário com tema moderna, há paradas de gradiente e valores para este plano de fundo.  
  
  Em primeiro plano (texto do Link)  
  
  `SearchControl.PopupButtonMouseDownText`  
  
### <a name="hyperlink"></a>Hiperlink  
 O hiperlink é um controle que não tem um par de primeiro e segundo plano. Em todos os casos, use a cor de hiperlink de primeiro plano, que será exibido corretamente em planos de fundo escuros, cinzas e brancos. Se você não usar o token de cor para o controle de hiperlink, você verá a cor padrão do sistema para "pressionado", "que piscará vermelho. Esse é o sinal de que o controle não está usando o token de cor de ambiente correta.  
  
 ![Aplicar linhas vermelhas no hiperlink](../../extensibility/ux-guidelines/media/0303-133-hyperlinkredline.png "0303 133_HyperlinkRedline")  
  
 Use...  
 Quando você precisa criar um hiperlink personalizado.  
  
 Não use...  
 para qualquer coisa que não é um hiperlink.  
  
 **Padrão**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Padrão de hiperlink](../../extensibility/ux-guidelines/media/0303-134-hyperlink.png "0303 134_Hyperlink")  
  
 Em primeiro plano (texto)  
  
 `Environment.PanelHyperlink`  
  
 **Passe o mouse**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Hiperlink focalizar](../../extensibility/ux-guidelines/media/0303-135-hyperlinkhover.png "0303 135_HyperlinkHover")  
  
 Em primeiro plano (texto)  
  
 `Environment.PanelHyperlinkHover`  
  
 **Pressionado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Hiperlink pressionado](../../extensibility/ux-guidelines/media/0303-136-hyperlinkpressed.png "0303 136_HyperlinkPressed")  
  
 Em primeiro plano (texto)  
  
 `Environment.PanelHyperlinkPressed`  
  
 **Desabilitado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Hiperlink desabilitada](../../extensibility/ux-guidelines/media/0303-137-hyperlinkdisabled.png "0303 137_HyperlinkDisabled")  
  
 Em primeiro plano (texto)  
  
 `Environment.PanelHyperlinkDisabled`  
  
### <a name="infobar"></a>Barra de informações  
 Infobars são usados para fornecer mais informações sobre um determinado contexto e sempre serão exibidos na parte superior de uma janela de documento ou janela de ferramentas.  
  
 ![Corte de barra de informações de funcionários](../../extensibility/ux-guidelines/media/0303-138-infobarredline.png "0303 138_InfobarRedline")  
  
 Use...  
 ao criar infobars personalizados.  
  
 Não use...  
 para elementos de interface do usuário que não são semelhantes a uma barra de informações.  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Barra de informações](../../extensibility/ux-guidelines/media/0303-139-infobar.png "0303 139_Infobar")  
  
 **Barra de informações**  
  
 Informações preliminares  
  
 `Environment.InfoBackground`  
  
 Em primeiro plano (texto)  
  
 `Environment.InfoText`  
  
 Borda  
  
 `Environment.ToolWindowBorder`  
  
### <a name="scroll-bar"></a>Barra de rolagem  
 Barras de rolagem são denominadas pelo ambiente do Visual Studio e não precisará ser o tema. No entanto, você pode decidir o que você deseja aproveitar as cores usadas nas barras de rolagem para que sua interface do usuário apareça sempre consistente com essa parte do ambiente do Visual Studio.  
  
 ![Corte de funcionários da barra de rolagem](../../extensibility/ux-guidelines/media/0303-140-scrollbarredline.png "0303 140_ScrollbarRedline")  
  
 Use...  
 Quando você estiver criando a interface do usuário que você deseja correspondência com barras de rolagem do Visual Studio.  
  
 Não use...  
 para qualquer coisa que você não deseja sempre corresponder à barra de rolagem da interface do usuário.  
  
 **Padrão**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Barra de rolagem](../../extensibility/ux-guidelines/media/0303-141-scrollbar.png "0303 141_Scrollbar")  
  
 **Barra de rolagem**  
  
 Barra de rolagem  
  
 `Environment.ScrollBarBackground`  
  
 Em primeiro plano (Thumb)  
  
 `Environment.ScrollBarThumbBackground`  
  
 ![Seta da barra de rolagem](../../extensibility/ux-guidelines/media/0303-142-scrollbararrow.png "0303 142_ScrollbarArrow")  
  
 **Seta de rolagem**  
  
 Informações preliminares  
  
 `Environment.ScrollBarArrowBackground`  
  
 Defina a mesma cor de barra de rolagem.  
  
 Em primeiro plano (glifo)  
  
 `Environment.ScrollBarArrowGlyph`  
  
 **Passe o mouse**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Barra de rolagem ao passar](../../extensibility/ux-guidelines/media/0303-143-scrollbarhover.png "0303 143_ScrollbarHover")  
  
 **Barra de rolagem**  
  
 Barra de rolagem  
  
 `Environment.ScrollBarBackground`  
  
 Em primeiro plano (Thumb)  
  
 `Environment.ScrollBarThumbMouseOverBackground`  
  
 ![Seta no foco da barra de rolagem](../../extensibility/ux-guidelines/media/0303-144-scrollbararrowhover.png "0303 144_ScrollbarArrowHover")  
  
 **Seta de rolagem**  
  
 Informações preliminares  
  
 `Environment.ScrollBarArrowMouseOverBackground`  
  
 Defina a mesma cor de barra de rolagem.  
  
 Em primeiro plano (glifo)  
  
 `Environment.ScrollBarArrowGlyphMouseOver`  
  
 **Pressionado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Barra de rolagem pressionado](../../extensibility/ux-guidelines/media/0303-145-scrollbarpressed.png "0303 145_ScrollbarPressed")  
  
 **Barra de rolagem**  
  
 Barra de rolagem  
  
 `Environment.ScrollBarBackground`  
  
 Em primeiro plano (Thumb)  
  
 `Environment.ScrollBarThumbPressedBackground`  
  
 ![Seta pressionada da barra de rolagem](../../extensibility/ux-guidelines/media/0303-146-scrollbararrowpressed.png "0303 146_ScrollbarArrowPressed")  
  
 **Seta de rolagem**  
  
 Informações preliminares  
  
 `Environment.ScrollBarArrowPressedBackground`  
  
 Defina a mesma cor de barra de rolagem.  
  
 Em primeiro plano (glifo)  
  
 `Environment.ScrollBarArrowGlyphPressed`  
  
###  <a name="BKMK_TreeView"></a> Exibição de árvore  
 Várias janelas de ferramentas, incluindo o Gerenciador de soluções, Gerenciador de servidores e modo de exibição de classe, implementam um esquema de organizacional hierárquico cujas cores são controlados por nomes de cores na categoria de TreeView. Todos os itens em uma exibição de árvore têm cores de plano de fundo e texto. Itens que tem elementos filho aninhados também têm glifos que indicam se o item é expandido ou recolhido.  
  
 ![Aplicar linhas vermelhas no modo de exibição de árvore](../../extensibility/ux-guidelines/media/0303-147-treeviewredline.png "0303 147_TreeViewRedline")  
  
 Use...  
 em qualquer lugar, você precisa implementar uma exibição hierárquica de organizacional.  
  
 Não use...  
 -   para qualquer coisa que não é semelhante a uma exibição de árvore.  
  
- em qualquer combinação de plano de fundo/primeiro plano diferente do especificado.  
  
  **Padrão**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Exibição de árvore](../../extensibility/ux-guidelines/media/0303-148-treeview.png "0303 148_TreeView")  
  
  Informações preliminares  
  
  `TreeView.Background`  
  
  Em primeiro plano (texto)  
  
  `TreeView.Background`  
  
  Em primeiro plano (glifo)  
  
  `TreeView.Glyph`  
  
  Borda  
  
  Nenhum  
  
  **Passe o mouse**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Ao passar o modo de exibição de árvore](../../extensibility/ux-guidelines/media/0303-149-treeviewhover.png "0303 149_TreeViewHover")  
  
  Informações preliminares  
  
  `TreeView.Background`  
  
  Em primeiro plano (texto)  
  
  `TreeView.Background`  
  
  Em primeiro plano (glifo)  
  
  `TreeView.GlyphMouseOver`  
  
  Borda  
  
  Nenhum  
  
  **Arrastar sobre**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Dragover do modo de exibição de árvore](../../extensibility/ux-guidelines/media/0303-150-treeviewdragover.png "0303 150_TreeViewDragOver")  
  
  Informações preliminares  
  
  `TreeView.DragOverItem`  
  
  Em primeiro plano (texto)  
  
  `TreeView.DragOverItem`  
  
  Em primeiro plano (glifo)  
  
  `TreeView.DragOverItemGlyph`  
  
  Borda  
  
  Nenhum  
  
  **Selecionado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Focadas de exibição de árvore](../../extensibility/ux-guidelines/media/0303-151-treeviewfocused.png "0303 151_TreeViewFocused")  
  
  **Com foco**  
  
  Informações preliminares  
  
  `TreeView.SelectedItemActive`  
  
  Em primeiro plano (texto)  
  
  `TreeView.SelectedItemActive`  
  
  Em primeiro plano (glifo)  
  
  `TreeView.SelectedItemActiveGlyph`  
  
  Borda  
  
  `TreeView.FocusVisualBorder`  
  
  ![Sem foco de exibição de árvore](../../extensibility/ux-guidelines/media/0303-152-treeviewunfocused.png "0303 152_TreeViewUnfocused")  
  
  **Sem foco**  
  
  Informações preliminares  
  
  `TreeView.SelectedItemInactive`  
  
  Em primeiro plano (texto)  
  
  `TreeView.SelectedItemInactive`  
  
  Em primeiro plano (glifo)  
  
  `TreeView.SelectedItemInactiveGlyph`  
  
  Borda  
  
  Nenhum  
  
  **Passe o mouse sobre selecionado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Com foco no foco de exibição de árvore](../../extensibility/ux-guidelines/media/0303-153-treeviewfocusedhover.png "0303 153_TreeViewFocusedHover")  
  
  **Com foco**  
  
  Informações preliminares  
  
  `TreeView.SelectedItemActive`  
  
  Em primeiro plano (texto)  
  
  `TreeView.SelectedItemActive`  
  
  Em primeiro plano (glifo)  
  
  `TreeView.SelectedItemActiveGlyphMouseOver`  
  
  Borda  
  
  None`TreeView.FocusVisualBorder`  
  
  ![Árvore de exibição sem foco ao passar](../../extensibility/ux-guidelines/media/0303-154-treeviewunfocusedhover.png "0303 154_TreeViewUnfocusedHover")  
  
  **Sem foco**  
  
  Informações preliminares  
  
  `TreeView.SelectedItemInactive`  
  
  Em primeiro plano (texto)  
  
  `TreeView.SelectedItemInactive`  
  
  Em primeiro plano (glifo)  
  
  `TreeView.SelectedItemActiveGlyphMouseOver`  
  
  Borda  
  
  Nenhum  
  
### <a name="button-controls"></a>Controles de botão  
 ![Aplicar linhas vermelhas no controle de botão](../../extensibility/ux-guidelines/media/0303-155-buttoncontrolredline.png "0303 155_ButtonControlRedline")  
  
 Use...  
 para botões do poço de documento que você deseja integrar com temas do Visual Studio (claro, escuro, azul ou um tema de alto contraste do sistema).  
  
 Não use...  
 para os botões que serão exibidos em um plano de fundo personalizado que não faz parte de um tema do Visual Studio.  
  
 **Padrão**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Botão](../../extensibility/ux-guidelines/media/0303-156-button.png "0303 156_Button")  
  
 Botão  
  
 `CommonControls.Button`  
  
 Borda do botão  
  
 `CommonControls.ButtonBorder`  
  
 **Desabilitado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Botão desabilitado](../../extensibility/ux-guidelines/media/0303-157-buttondisabled.png "0303 157_ButtonDisabled")  
  
 Botão  
  
 `CommonControls.ButtonDisabled`  
  
 Borda do botão  
  
 `CommonControls.ButtonBorderDisabled`  
  
 **Passe o mouse**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Botão focalizar](../../extensibility/ux-guidelines/media/0303-158-buttonhover.png "0303 158_ButtonHover")  
  
 Botão  
  
 `CommonControls.ButtonHover`  
  
 Borda do botão  
  
 `CommonControls.ButtonBorderHover`  
  
 **Pressionado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Botão pressionado](../../extensibility/ux-guidelines/media/0303-159-buttonpressed.png "0303 159_ButtonPressed")  
  
 Botão  
  
 `CommonControls.ButtonPressed`  
  
 Borda do botão  
  
 `CommonControls.ButtonBorderPressed`  
  
 **Com foco**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Botão focalizado](../../extensibility/ux-guidelines/media/0303-160-buttonfocused.png "0303 160_ButtonFocused")  
  
 Botão  
  
 `CommonControls.ButtonFocused`  
  
 Borda do botão  
  
 `CommonControls.ButtonBorderFocused`  
  
### <a name="check-box-controls"></a>Controles de caixa de seleção  
 ![Corte de funcionários da caixa de seleção](../../extensibility/ux-guidelines/media/0303-161-checkboxredline.png "0303 161_CheckboxRedline")  
  
 Use...  
 para controles de caixa de seleção contidos no documento bem.  
  
 Não use...  
 para qualquer interface do usuário que não é um controle de caixa de seleção.  
  
 **Padrão**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Caixa de seleção](../../extensibility/ux-guidelines/media/0303-162-checkbox.png "0303 162_Checkbox")  
  
 Informações preliminares  
  
 `CommonControls.CheckBoxBackground`  
  
 Borda  
  
 `CommonControls.CheckBoxBorder`  
  
 Texto  
  
 `CommonControls.CheckBoxText`  
  
 Glifo  
  
 `CommonControls.CheckBoxGlyph`  
  
 **Desabilitado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Caixa de seleção desabilitada](../../extensibility/ux-guidelines/media/0303-163-checkboxdisabled.png "0303 163_CheckboxDisabled")  
  
 Informações preliminares  
  
 `CommonControls.CheckBoxBackgroundDisabled`  
  
 Borda  
  
 `CommonControls.CheckBoxBorderDisabled`  
  
 Texto  
  
 `CommonControls.CheckBoxTextDisabled`  
  
 Glifo  
  
 `CommonControls.CheckBoxGlyphDisabled`  
  
 **Passe o mouse**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Caixa de seleção ao focalizar](../../extensibility/ux-guidelines/media/0303-164-checkboxhover.png "0303 164_CheckboxHover")  
  
 Informações preliminares  
  
 `CommonControls.CheckBoxBackgroundHover`  
  
 Borda  
  
 `CommonControls.CheckBoxBorderHover`  
  
 Texto  
  
 `CommonControls.CheckBoxTextHover`  
  
 Glifo  
  
 `CommonControls.CheckBoxGlyphHover`  
  
 **Pressionado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Caixa de seleção pressionada](../../extensibility/ux-guidelines/media/0303-165-checkboxpressed.png "0303 165_CheckboxPressed")  
  
 Informações preliminares  
  
 `CommonControls.CheckBoxBackgroundPressed`  
  
 Borda  
  
 `CommonControls.CheckBoxBorderPressed`  
  
 Texto  
  
 `CommonControls.CheckBoxTextPressed`  
  
 Glifo  
  
 `CommonControls.CheckBoxGlyphPressed`  
  
 **Com foco**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Caixa de seleção focada](../../extensibility/ux-guidelines/media/0303-166-checkboxfocused.png "0303 166_CheckboxFocused")  
  
 Informações preliminares  
  
 `CommonControls.CheckBoxBackgroundFocused`  
  
 Borda  
  
 `CommonControls.CheckBoxBorderFocused`  
  
 Texto  
  
 `CommonControls.CheckBoxTextFocused`  
  
 Glifo  
  
 `CommonControls.CheckBoxGlyphFocused`  
  
### <a name="drop-boxcombo-box-controls"></a>Soltar os controles de caixa de combinação/caixa  
 ![Remova&#45;para baixo&#47;aplicar linhas vermelhas no caixa de combinação](../../extensibility/ux-guidelines/media/0303-167-dropdowncomboboxredline.png "0303 167_DropDownComboBoxRedline")  
  
 Use...  
 para listas suspensas e combinação caixas que também são parte do documento.  
  
 Não use...  
 -   para qualquer interface do usuário que não é uma lista suspensa ou caixa de combinação.  
  
- para um [Drop-down](../../misc/shared-colors.md#BKMK_CommandDropDown) ou [caixa de combinação](../../misc/shared-colors.md#BKMK_CommandComboBox) na barra de comandos.  
  
  **Padrão**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Remova&#45;para baixo&#47;caixa de combinação](../../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303 168_DropDownComboBox")  
  
  Informações preliminares  
  
  `CommonControls.ComboBoxBackground`  
  
  Borda  
  
  `CommonControls.ComboBoxBorder`  
  
  Texto  
  
  `CommonControls.ComboBoxText`  
  
  Separador  
  
  `CommonControls.ComboBoxSeparator`  
  
  Glifo  
  
  `CommonControls.ComboBoxGlyph`  
  
  Plano de fundo de glifo  
  
  `CommonControls.ComboBoxGlyphBackground`  
  
  **Desabilitado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Remova&#45;para baixo&#47;caixa de combinação desabilitada](../../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303 169_DropDownComboBoxDisabled")  
  
  Informações preliminares  
  
  `CommonControls.ComboBoxBackgroundDisabled`  
  
  Borda  
  
  `CommonControls.ComboBoxBorderDisabled`  
  
  Texto  
  
  `CommonControls.ComboBoxTextDisabled`  
  
  Separador  
  
  `CommonControls.ComboBoxSeparatorDisabled`  
  
  Glifo  
  
  `CommonControls.ComboBoxGlyphDisabled`  
  
  Plano de fundo de glifo  
  
  `CommonControls.ComboBoxGlyphBackgroundDisabled`  
  
  **Passe o mouse**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Remova&#45;para baixo&#47;caixa de combinação em foco](../../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303 170_DropDownComboBoxHover")  
  
  Informações preliminares  
  
  `CommonControls.ComboBoxBackgroundHover`  
  
  Borda  
  
  `CommonControls.ComboBoxBorderHover`  
  
  Texto  
  
  `CommonControls.ComboBoxTextHover`  
  
  Separador  
  
  `CommonControls.ComboBoxSeparatorHover`  
  
  Glifo  
  
  `CommonControls.ComboBoxGlyphHover`  
  
  Plano de fundo de glifo  
  
  `CommonControls.ComboBoxGlyphBackgroundHover`  
  
  **Pressionado**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Remova&#45;para baixo&#47;caixa de combinação pressionada](../../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303 171_DropDownComboBoxPressed")  
  
  Informações preliminares  
  
  `CommonControls.ComboBoxBackgroundPressed`  
  
  Borda  
  
  `CommonControls.ComboBoxBorderPressed`  
  
  Texto  
  
  `CommonControls.ComboBoxTextPressed`  
  
  Separador  
  
  `CommonControls.ComboBoxSeparatorPressed`  
  
  Glifo  
  
  `CommonControls.ComboBoxGlyphPressed`  
  
  Plano de fundo de glifo  
  
  `CommonControls.ComboBoxGlyphBackgroundPressed`  
  
  **Com foco**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Remova&#45;para baixo&#47;caixa de combinação com foco](../../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303 172_DropDownComboBoxFocused")  
  
  Informações preliminares  
  
  `CommonControls.ComboBoxBackgroundFocused`  
  
  Borda  
  
  `CommonControls.ComboBoxBorderFocused`  
  
  Texto  
  
  `CommonControls.ComboBoxTextFocused`  
  
  Separador  
  
  `CommonControls.ComboBoxSeparatorFocused`  
  
  Glifo  
  
  `CommonControls.ComboBoxGlyphFocused`  
  
  Plano de fundo de glifo  
  
  `CommonControls.ComboBoxGlyphBackgroundFocused`  
  
  **Seleção de entrada de texto**  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  ![Remova&#45;para baixo&#47;entrada de texto de caixa de combinação](../../extensibility/ux-guidelines/media/0303-173-dropdowncomboboxtextinput.png "0303 173_DropDownComboBoxTextInput")  
  
  Realce  
  
  `CommonControls.ComboBoxTextInputSelection`  
  
  **Pressionado – modo de exibição de item de lista**  
  
  ![Remova&#45;para baixo&#47;exibição de lista de caixa de combinação](../../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303 174_DropDownComboBoxListView")  
  
  Informações preliminares  
  
  `CommonControls.ComboBoxListBackground`  
  
  `CommonControls.ComboBoxListBackgroundHover`  
  
  `CommonControls.ComboBoxListItemBackgroundPressed`  
  
  `CommonControls.ComboBoxListItemBackgroundFocused`  
  
  Borda  
  
  `CommonControls.ComboBoxListBorder`  
  
  `CommonControls.ComboBoxListBorderHover`  
  
  `CommonControls.ComboBoxListBorderPressed`  
  
  `CommonControls.ComboBoxListBorderFocused`  
  
  Texto do item  
  
  `CommonControls.ComboBoxListItemText`  
  
  `CommonControls.ComboBoxListItemTextHover`  
  
  `CommonControls.ComboBoxListItemTextPressed`  
  
  `CommonControls.ComboBoxListItemTextFocused`  
  
  Sombra do plano de fundo  
  
  `CommonControls.ComboBoxListBackgroundShadow`  
  
### <a name="tabular-data-grid-controls"></a>Controles de dados tabulares (grade)  
 Controles de dados de tabela, também conhecido como controles de grade, são controles comuns do Visual Studio que pode ser usado para apresentar grandes quantidades de dados em várias colunas. Controles de dados de tabela padrão podem ser encontrados em vários lugares dentro do Visual Studio: a janela de ferramentas da lista de erros, os relatórios de IntelliTrace e exibição de heap de memória, entre outros. Sempre use os controles de dados de tabela padrão fornecidos. Em alguns casos raros, talvez você não tenha acesso aos controles de dados de tabela padrão. Nessas situações, use os seguintes nomes de token para garantir que sua interface do usuário seja consistente com outros controles de dados tabulares no Visual Studio.  
  
 ![Dados tabulares &#40;controle de grade&#41; aplicar linhas vermelhas no](../../extensibility/ux-guidelines/media/0303-197-tabulardatagridcontrolredline.png "0303 197_TabularDataGridControlRedline")  
  
 Use...  
 para tabular ou controles de grade.  
  
 Não use...  
 para qualquer interface do usuário que não é um controle de tabela ou grade.  
  
#### <a name="column-headers"></a>Cabeçalhos de coluna  
 Cabeçalhos de coluna consistem em um plano de fundo, uma borda, o texto do título e um glifo opcional que geralmente usado quando uma grade é classificada pela coluna.  
  
 Estado  
  
 Elemento  
  
 Nome do token: Category.color  
  
 Padrão  
  
 Informações preliminares  
  
 `Header.Default`  
  
 Em primeiro plano (texto)  
  
 `Environment.CommandBarTextActive`  
  
 Em primeiro plano (glifo)  
  
 `Header.Glyph`  
  
 Borda  
  
 `Header.SeparatorLine`  
  
 Passe o mouse  
  
 Informações preliminares  
  
 `Header.MouseOver`  
  
 Em primeiro plano (texto)  
  
 `Environment.CommandBarTextHover`  
  
 Em primeiro plano (glifo)  
  
 `Header.MouseOverGlyph`  
  
 Borda  
  
 `Header.SeparatorLine`  
  
 Pressionado  
  
 Informações preliminares  
  
 `CommonControls.CheckBoxBackgroundPressed`  
  
 Em primeiro plano (texto)  
  
 `CommonControls.CheckBoxBorderPressed`  
  
 Em primeiro plano (glifo)  
  
 `CommonControls.CheckBoxTextPressed`  
  
 Borda  
  
 `CommonControls.CheckBoxGlyphPressed`  
  
#### <a name="list-view-items"></a>Exibir itens de lista  
 Exibir itens de lista consistem em um plano de fundo e o conteúdo. O conteúdo pode ser texto, um ícone ou ambos.  
  
 Estado  
  
 Elemento  
  
 Nome do token: Category.color  
  
 Padrão  
  
 Informações preliminares  
  
 Transparente  
  
 Em primeiro plano (texto)  
  
 `Environment.CommandBarTextActive`  
  
 Borda  
  
 Nenhum  
  
 Selecionado (ativo)  
  
 Informações preliminares  
  
 `TreeView.SelectedItemActive`  
  
 Em primeiro plano (texto)  
  
 `TreeView.SelectedItemActiveText`  
  
 Borda  
  
 Nenhum  
  
 Selecionado (inativo)  
  
 Informações preliminares  
  
 `TreeView.SelectedItemInactive`  
  
 Em primeiro plano (texto)  
  
 `TreeView.SelectedItemInactiveText`  
  
 Borda  
  
 Nenhum  
  
## <a name="manifest-designer"></a>Designer de manifesto  
 O Designer de manifesto foi projetado como uma maneira de tornar mais fácil de editar o arquivo de manifesto em projetos do Windows 8 e Windows Phone 8. Embora não haja nenhuma estrutura compartilhada disponíveis para consumo, pode ser apropriado para a correspondência entre as cores da estrutura geral e guias de navegação/orientação e o layout de design. Para obter mais informações sobre os detalhes de layout, consulte [Layout para o Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md).  
  
 ![Aplicar linhas vermelhas no Designer de manifesto](../../extensibility/ux-guidelines/media/0303-175-manifestdesignerredline.png "0303 175_ManifestDesignerRedline")  
  
 Use...  
 -   para designers que são semelhantes para o Designer de manifesto.  
  
- em vez de usar controles de guia comum na parte superior de um editor dentro do documento bem.  
  
  Não use...  
  -   Se você tiver mais de seis guias.  
  
- para qualquer interface do usuário que não é estruturado, como o Designer de manifesto.  
  
  Estado  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  Padrão (selecionado)  
  
  Tabulação  
  
  Informações preliminares  
  
  `ManifestDesigner.TabActive`  
  
  Borda  
  
  Nenhum  
  
  Painel de descrição  
  
  Informações preliminares  
  
  `ManifestDesigner.DescriptionPane`  
  
  Página de conteúdo  
  
  Informações preliminares  
  
  `ManifestDesigner.Background`  
  
  Texto do auxiliar de diálogo  
  
  `ManifestDesigner.WatermarkText`  
  
  Esse nome de token não corresponde a sua função.  
  
  Não selecionado  
  
  Tabulação  
  
  Informações preliminares  
  
  `ManifestDesigner.Tab.Inactive`  
  
  Passe o mouse  
  
  Tabulação  
  
  Informações preliminares  
  
  `ManifestDesigner.Tab.Mouseover`  
  
## <a name="tagging"></a>Marcação  
 Visual Studio dá suporte à marcação, que permite que um usuário declarar as palavras-chave pesquisável para fins de acompanhamento. Por exemplo, os desenvolvedores e gerentes de projeto podem usar o Team Foundation Server (TFS) para marcar os itens de trabalho. As tabelas a seguir dar nomes de cor para a marca em si e o glifo "ícone de fechar" que aparece nos Estados selecionados e passe o mouse.  
  
 ![Marcação de corte de funcionários](../../extensibility/ux-guidelines/media/0303-176-taggingredline.png "0303 176_TaggingRedline")  
  
 Use...  
 interface do usuário que dá suporte a marcação.  
  
 Não use...  
 para qualquer outro tipo de interface do usuário.  
  
### <a name="tag"></a>Marca  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Marca](../../extensibility/ux-guidelines/media/0303-177-tag.png "0303 177_Tag")  
  
 **Padrão**  
  
 Informações preliminares  
  
 `Tag.Background`  
  
 Em primeiro plano (texto)  
  
 `Tag.Background`  
  
 ![Marca ao focalizar](../../extensibility/ux-guidelines/media/0303-178-taghover.png "0303 178_TagHover")  
  
 **Passe o mouse**  
  
 Informações preliminares  
  
 `Tag.HoverBackground`  
  
 Em primeiro plano (texto)  
  
 `Tag.HoverBackgroundText`  
  
 ![Marca pressionada](../../extensibility/ux-guidelines/media/0303-179-tagpressed.png "0303 179_TagPressed")  
  
 **Pressionado**  
  
 Informações preliminares  
  
 `Tag.PressedBackground`  
  
 Em primeiro plano (texto)  
  
 `Tag.PressedBackgroundText`  
  
 ![Marca selecionada](../../extensibility/ux-guidelines/media/0303-180-tagselected.png "0303 180_TagSelected")  
  
 **Selecionado**  
  
 Informações preliminares  
  
 `Tag.SelectedBackground`  
  
 Em primeiro plano (texto)  
  
 `Tag.SelectedBackgroundText`  
  
### <a name="glyph-close-icon"></a>Glifo (ícone de fechar)  
 **Padrão**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Marca &#40;glifo de&#41;](../../extensibility/ux-guidelines/media/0303-181-tagglyph.png "0303 181_TagGlyph")  
  
 **Padrão (padrão de marca)**  
  
 Informações preliminares  
  
 N/D  
  
 Em primeiro plano (glifo)  
  
 `Tag.TagHoverGlyph`  
  
 **Passe o mouse**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Marca &#40;glifo de&#41; ao focalizar](../../extensibility/ux-guidelines/media/0303-182-tagglyphhover.png "0303 182_TagGlyphHover")  
  
 **Passe o mouse (padrão de marca)**  
  
 Informações preliminares  
  
 `Tag.TagHoverGlyphHoverBackground`  
  
 Em primeiro plano (glifo)  
  
 `Tag.TagHoverGlyphHover`  
  
 Borda  
  
 `Tag.TagHoverGlyphHoverBorder`  
  
 **Pressionado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Marca &#40;glifo de&#41; pressionada](../../extensibility/ux-guidelines/media/0303-183-tagglyphpressed.png "0303 183_TagGlyphPressed")  
  
 **Pressionado (padrão de marca)**  
  
 Informações preliminares  
  
 `Tag.TagHoverGlyphPressedBackground`  
  
 Em primeiro plano (glifo)  
  
 `Tag.TagHoverGlyphPressed`  
  
 Borda  
  
 `Tag.TagHoverGlyphPressedBorder`  
  
 **Marca/glifo selecionado padrão**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Marca selecionada](../../extensibility/ux-guidelines/media/0303-184-tagselected.png "0303 184_TagSelected")  
  
 **Padrão (marca selecionada)**  
  
 Informações preliminares  
  
 N/D  
  
 Em primeiro plano (glifo)  
  
 `Tag.TagSelectedGlyph`  
  
 **Passe o mouse marca/glifo selecionado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Marca selecionada ao focalizar](../../extensibility/ux-guidelines/media/0303-185-tagselectedhover.png "0303 185_TagSelectedHover")  
  
 **Passe o mouse (marca selecionado)**  
  
 Informações preliminares  
  
 `Tag.TagSelectedGlyphHoverBackground`  
  
 Em primeiro plano (glifo)  
  
 `Tag.TagSelectedGlyphHover`  
  
 Borda  
  
 `Tag.TagSelectedGlyphHoverBorder`  
  
 **Selecionado/glifo de marca pressionado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Marca selecionada pressionado](../../extensibility/ux-guidelines/media/0303-186-tagselectedpressed.png "0303 186_TagSelectedPressed")  
  
 **Pressionado (marca selecionada)**  
  
 Informações preliminares  
  
 `Tag.TagSelectedGlyphPressedBackground`  
  
 Foreground(glyph)  
  
 `Tag.TagSelectedGlyphPressed`  
  
 Borda  
  
 `Tag.TagSelectedGlyphPressedBorder`  
  
## <a name="shell"></a>Shell  
  
### <a name="background"></a>Informações preliminares  
 O plano de fundo ambiente consiste em duas camadas. A camada inferior é uma cor sólida que abrange todo o IDE. A camada superior se encaixa em prateleira de comando e entre os canais de ocultar automaticamente janela ferramenta nas bordas esquerdas e direita do IDE. A partir do Visual Studio 2013, as camadas de plano de fundo superior e inferior são definidas para a mesma cor nos temas claro e escuro.  
  
 ![Aplicar linhas vermelhas no plano de fundo do shell](../../extensibility/ux-guidelines/media/0303-187-shellbackgroundredline.png "0303 187_ShellBackgroundRedline")  
  
 Use...  
 para os locais que você deseja correspondência com o plano de fundo do ambiente do Visual Studio.  
  
 Não use...  
 -   como um preenchimento de locais que não são as superfícies de plano de fundo.  
  
- como um plano de fundo no qual você deseja colocar os elementos de primeiro plano.  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  Camada inferior  
  
  Informações preliminares  
  
  `Environment.EnvironmentBackground`  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  Camada superior  
  
  Informações preliminares  
  
  *Conjunto com o mesmo valor de cor em temas claros de 2013 do Visual Studio e escuros marcas de gradiente.*  
  
  `Environment.EnvironmentBackgroundGradientBegin`  
  
  `Environment.EnvironmentBackgroundGradientEnd`  
  
  `Environment.EnvironmentBackgroundGradientMiddle1`  
  
  `Environment.EnvironmentBackgroundGradientMiddle2`  
  
### <a name="command-shelf"></a>Prateleira de comando  
 Dois conjuntos de nomes de token são usados para os planos de fundo de prateleira do comando: um conjunto para onde fica a barra de menus e outro para onde as barras de comandos ficam. Um grupo de barra de comandos individuais tem seus próprios valores de cor do plano de fundo, que serão discutidos mais detalhadamente na seção "barra de comandos". Barra de menus de barra e comando texto é discutidos nas seções a barra menu e o comando, respectivamente.  
  
 ![Corte de funcionários de prateleira do comando](../../extensibility/ux-guidelines/media/0303-188-commandshelfredline.png "0303 188_CommandShelfRedline")  
  
 Use...  
 -   para as áreas onde você coloca menus ou barras de ferramentas.  
  
- com o plano de fundo correto /? combinação do nome do token de primeiro plano.  
  
  Não use...  
  para as áreas que não são semelhantes a uma prateleira de comando.  
  
  Componente  
  
  Elemento  
  
  Nome do token: Category.color  
  
  Barra de menus  
  
  Informações preliminares  
  
  *Conjunto com o mesmo valor de cor em temas claros de 2013 do Visual Studio e escuros marcas de gradiente.*  
  
  `Environment.CommandShelfHighlightGradientBegin`  
  
  `Environment.CommandShelfHighlightGradientMiddle`  
  
  `Environment.CommandShelfHighlightGradientEnd`  
  
  Barra de comandos  
  
  Informações preliminares  
  
  *Conjunto com o mesmo valor de cor em temas claros de 2013 do Visual Studio e escuros marcas de gradiente.*  
  
  `Environment.CommandShelfBackgroundGradientBegin`  
  
  `Environment.CommandShelfBackgroundGradientMiddle`  
  
  `Environment.CommandShelfBackgroundGradientEnd`  
  
## <a name="toolbox"></a>Caixa de Ferramentas  
 A caixa de ferramentas é uma das janelas de ferramentas comum que é usado com mais frequência no Visual Studio. Ele é essencialmente um controle de árvore com um tema especial e o estilo aplicado.  
  
 ![Corte de funcionários da caixa de ferramentas](../../extensibility/ux-guidelines/media/0303-189-toolboxredline.png "0303 189_ToolboxRedline")  
  
 Use...  
 Quando você estiver criando uma janela de ferramentas que você deseja sempre são consistentes com a caixa de ferramentas do shell.  
  
 Não use...  
 para qualquer coisa que não seja semelhante à caixa de ferramentas da interface do usuário, ou se você não tiver certeza se a interface do usuário poderão ter problemas se a caixa de ferramentas do shell de alteração de cores.  
  
 **Padrão**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Nó pai de caixa de ferramentas](../../extensibility/ux-guidelines/media/0303-190-toolboxparentnode.png "0303 190_ToolboxParentNode")  
  
 **Nó pai**  
  
 ![Nó filho de caixa de ferramentas](../../extensibility/ux-guidelines/media/0303-191-toolboxchildnode.png "0303 191_ToolboxChildNode")  
  
 **Nó filho**  
  
 Informações preliminares  
  
 `Environment.ToolboxContent`  
  
 Títulos  
  
 `Environment.ToolWindowBackground`  
  
 Itens individuais ou a janela inteira se não há controles disponíveis  
  
 Borda  
  
 Nenhum  
  
 Em primeiro plano (glifo)  
  
 `Environment.ToolboxContent`  
  
 Em primeiro plano (texto)  
  
 `Environment.ToolboxContent`  
  
 **Passe o mouse**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Nó filho de caixa de ferramentas ao focalizar](../../extensibility/ux-guidelines/media/0303-192-toolboxchildnodehover.png "0303 192_ToolboxChildNodeHover")  
  
 **Passe o mouse no nó filho da caixa de ferramentas**  
  
 Informações preliminares  
  
 `Environment.ToolboxContentMouseOver`  
  
 Somente os itens individuais  
  
 Borda  
  
 Nenhum  
  
 Em primeiro plano (texto)  
  
 `Environment.ToolboxContentMouseOver`  
  
 Somente os itens individuais  
  
 **Selecionado**  
  
 Componente  
  
 Elemento  
  
 Nome do token: Category.color  
  
 ![Nó pai de caixa de ferramentas com foco](../../extensibility/ux-guidelines/media/0303-193-toolboxparentnodefocused.png "0303 193_ToolboxParentNodeFocused")  
  
 **Nó pai focalizado**  
  
 ![Nó filho de caixa de ferramentas com foco](../../extensibility/ux-guidelines/media/0303-194-toolboxchildnodefocused.png "0303 194_ToolboxChildNodeFocused")  
  
 **Nó filho focalizado**  
  
 Informações preliminares  
  
 `TreeView.SelectedItemActive`  
  
 Partir [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) categoria  
  
 Borda  
  
 `TreeView.FocusVisualBorder`  
  
 Partir [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) categoria  
  
 Em primeiro plano (glifo)  
  
 `TreeView.SelectedItemActive`  
  
 Partir [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) categoria  
  
 Em primeiro plano (texto)  
  
 `TreeView.SelectedItemActive`  
  
 Partir [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) categoria  
  
 ![Nó pai da caixa de ferramentas sem foco](../../extensibility/ux-guidelines/media/0303-195-toolboxparentnodeunfocused.png "0303 195_ToolboxParentNodeUnfocused")  
  
 **Nó pai sem foco**  
  
 ![Nó filho da caixa de ferramentas sem foco](../../extensibility/ux-guidelines/media/0303-196-toolboxchildnodeunfocused.png "0303 196_ToolboxChildNodeUnfocused")  
  
 **Nó filho sem foco**  
  
 Informações preliminares  
  
 `TreeView.SelectedItemInactive`  
  
 Partir [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) categoria  
  
 Borda  
  
 Nenhum  
  
 Em primeiro plano (glifo)  
  
 `TreeView.SelectedItemInactive`  
  
 Partir [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) categoria  
  
 Em primeiro plano (texto)  
  
 `TreeView.SelectedItemInactive`  
  
 Partir [exibição de árvore](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) categoria

