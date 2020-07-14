---
title: Cores compartilhadas | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
ms.assetid: 9d3186f3-07d2-441f-b33e-435e95d8a0b8
caps.latest.revision: 11
ms.author: brgeorge
ms.openlocfilehash: 76c04680b63eb362e02fdf26d817660d671b3b52
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548350"
---
# <a name="shared-colors"></a>Cores compartilhadas
Inserir introdução aqui.  
  
## <a name="shared-colors"></a>Cores compartilhadas  
 Quando você está projetando a interface do usuário que usa elementos do shell do Visual Studio comuns ou deseja que seu elemento de interface seja consistente com recursos semelhantes, use nomes de token existentes em arquivos de definição de pacote para escolher e atribuir cores. Isso garante que sua interface do usuário permaneça consistente com o ambiente do Visual Studio geral e que seja atualizada automaticamente quando os temas forem adicionados ou atualizados.  
  
 Este artigo descreve os elementos comuns da interface do usuário e os nomes de token que eles usam, que você pode referenciar ao criar uma interface do usuário semelhante. Para obter informações específicas sobre como acessar esses tokens de cor, consulte [o serviço VSColor](../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService).  
  
 Certifique-se de usar os nomes de token corretamente:  
  
- **Use nomes de token com base na função, não na própria cor.** As cores compartilhadas comuns são associadas a elementos de interface específicos e devem ser usadas apenas para os mesmos ou recursos semelhantes. Por exemplo, não reutilize a cor de uma caixa de combinação pressionada para uma animação de progresso girando apenas porque você gosta da cor. As funções da caixa de combinação e da animação são diferentes e, se a cor associada à caixa de combinação for alterada, ela poderá não ser mais uma cor apropriada para o elemento de animação. O uso consistente da cor ajuda a orientar seus usuários e a evitar confusão.  
  
- **Use cores de plano de fundo e texto na combinação correta.** As cores de plano de fundo que devem ser usadas com texto terão uma cor de texto associada. Não use cores de texto diferentes das especificadas para esse plano de fundo. Se não houver uma cor de texto associada, não use essa cor de plano de fundo para qualquer superfície em que você espera exibir texto. Outras combinações de cores de texto e de plano de fundo podem resultar em uma interface ilegível.  
  
- **Use cores de controle apropriadas para seu local.** Em determinados Estados, alguns controles do Visual Studio não têm cores de borda e de plano de fundo separadas. Em vez disso, eles pegam essas cores nas superfícies por trás delas. Certifique-se de sempre usar os nomes de token apropriados para o local onde você está colocando o controle.  
  
> [!IMPORTANT]
> Não use tokens encontrados nas categorias "página inicial" ou "Cider"!  
  
### <a name="command-structures"></a>Estruturas de comando  
  
#### <a name="menus"></a><a name="BKMK_CommandMenus"></a>Completos  
 Os menus podem ocorrer em vários locais dentro do Visual Studio 2013: a barra de menus principal, inserida em janelas de documentos ou ferramentas, ou clique com o botão direito do mouse em vários locais em todo o IDE. Implementações de menus associados a outros elementos da interface do usuário são discutidas na seção para o respectivo elemento. Você sempre deve usar a implementação de menu padrão fornecida pelo ambiente do Visual Studio. No entanto, em algumas instâncias raras, talvez você não tenha acesso aos menus padrão do Visual Studio. Nessas situações, use os nomes de token a seguir para garantir que sua interface do usuário seja consistente com outros menus do Visual Studio.  
  
 ![Redline de menus](../extensibility/ux-guidelines/media/0303-000-menuredline.png "0303-000_MenuRedline")  
  
Usar...  
- sempre que você precisar criar um menu personalizado.  
  
- Quando você tem um novo componente de interface do usuário que deseja corresponder aos menus do Visual Studio.  
  
Não use...  
apenas a cor do plano de fundo. Sempre use a combinação de plano de fundo/primeiro plano como especificado.  
  
##### <a name="menu-title"></a>Título do menu  
 Os títulos de menu consistem em um plano de fundo, uma borda e o texto do título, bem como um glifo opcional, geralmente quando o menu é encontrado em uma barra de comandos.  
  
 ![Título do menu Redline](../extensibility/ux-guidelines/media/0303-001-menutitleredline.png "0303-001_MenuTitleRedline")  
  
Usar...  
sempre que você estiver criando um título de menu personalizado.  
  
Não use...  
- para qualquer coisa que você não queira que corresponda sempre ao título do menu.  
  
- em qualquer combinação de plano de fundo/primeiro plano diferente de especificada.  
  
  **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Padrão de título do menu](../extensibility/ux-guidelines/media/0303-002-menutitledefault.png "0303-002_MenuTitleDefault")<br /><br /> **Título do menu**|Segundo plano|Nenhum|  
|![Padrão de título do menu](../extensibility/ux-guidelines/media/0303-002-menutitledefault.png "0303-002_MenuTitleDefault")<br /><br /> **Título do menu**|Primeiro plano (texto)|`Environment.CommandBarTextActive`|  
|![Título do menu com o padrão de glifo](../extensibility/ux-guidelines/media/0303-003-menutitlewithglyphdefault.png "0303-003_MenuTitleWithGlyphDefault")<br /><br /> **Título do menu com glifo**|Primeiro plano (glifo)|`Environment.CommandBarMenuGlyph`|  
|![Título do menu com o padrão de glifo](../extensibility/ux-guidelines/media/0303-003-menutitlewithglyphdefault.png "0303-003_MenuTitleWithGlyphDefault")<br /><br /> **Título do menu com glifo**|Borda|Nenhum|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Título do menu ao focalizar](../extensibility/ux-guidelines/media/0303-004-menutitlehover.png "0303-004_MenuTitleHover")<br /><br /> **Título do menu**|Segundo plano|`Environment.CommandBarMouseOverBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Título do menu ao focalizar](../extensibility/ux-guidelines/media/0303-004-menutitlehover.png "0303-004_MenuTitleHover")<br /><br /> **Título do menu**|Primeiro plano (texto)|`Environment.CommandBarTextHover`|  
|![Título do menu com glifo ao focalizar](../extensibility/ux-guidelines/media/0303-005-menutitlewithglyphhover.png "0303-005_MenuTitleWithGlyphHover")<br /><br /> **Título do menu com glifo**|Primeiro plano (glifo)|`Environment.CommandBarMenuMouseOverGlyph`|  
|![Título do menu com glifo ao focalizar](../extensibility/ux-guidelines/media/0303-005-menutitlewithglyphhover.png "0303-005_MenuTitleWithGlyphHover")<br /><br /> **Título do menu com glifo**|Borda|`Environment.CommandBarBorder`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Título do menu pressionado](../extensibility/ux-guidelines/media/0303-006-menutitlepressed.png "0303-006_MenuTitlePressed")<br /><br /> **Título do menu**|Segundo plano|`Environment.CommandBarMenuBackgroundGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Título do menu pressionado](../extensibility/ux-guidelines/media/0303-006-menutitlepressed.png "0303-006_MenuTitlePressed")<br /><br /> **Título do menu**|Primeiro plano (texto)|`Environment.CommandBarTextActive`|  
|![Título do menu com glifo pressionado](../extensibility/ux-guidelines/media/0303-007-menutitlewithglyphpressed.png "0303-007_MenuTitleWithGlyphPressed")<br /><br /> **Título do menu com glifo**|Primeiro plano (glifo)|`Environment.CommandBarMenuMouseDownGlyph`|  
|![Título do menu com glifo pressionado](../extensibility/ux-guidelines/media/0303-007-menutitlewithglyphpressed.png "0303-007_MenuTitleWithGlyphPressed")<br /><br /> **Título do menu com glifo**|Borda|`Environment.CommandBarMenuBorder`<br /><br /> Somente os lados esquerdo, superior e direito.|  
  
 **Desabilitado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Título do menu com glifo desabilitado](../extensibility/ux-guidelines/media/0303-008-menutitlewithglyphdisabled.png "0303-008_MenuTitleWithGlyphDisabled")<br /><br /> **Título do menu com glifo**|Segundo plano|Nenhum|  
|![Título do menu com glifo desabilitado](../extensibility/ux-guidelines/media/0303-008-menutitlewithglyphdisabled.png "0303-008_MenuTitleWithGlyphDisabled")<br /><br /> **Título do menu com glifo**|Primeiro plano (texto)|`Environment.CommandBarTextInactive`|  
|![Título do menu com glifo desabilitado](../extensibility/ux-guidelines/media/0303-008-menutitlewithglyphdisabled.png "0303-008_MenuTitleWithGlyphDisabled")<br /><br /> **Título do menu com glifo**|Primeiro plano (glifo)|`Environment.CommandBarTextInactive`|  
|![Título do menu com glifo desabilitado](../extensibility/ux-guidelines/media/0303-008-menutitlewithglyphdisabled.png "0303-008_MenuTitleWithGlyphDisabled")<br /><br /> **Título do menu com glifo**|Borda|Nenhum|  
  
##### <a name="menu"></a>Menu  
 Um item de menu individual consiste no texto do menu e em um ícone opcional, caixa de seleção ou glifo de submenu. Sua cor de plano de fundo e de texto é alterada ao focalizar. Esse token de cor é um par de plano de fundo/primeiro plano.  
  
 ![Itens de menu Redline](../extensibility/ux-guidelines/media/0303-009-menuitemredline.png "0303-009_MenuItemRedline")  
  
 Usar...  
 para qualquer lista suspensa iniciada em uma barra de menus ou barra de comandos.  
  
Não use...  
- para qualquer lista suspensa que ocorra em outro contexto.  

- em qualquer combinação de plano de fundo/primeiro plano diferente de especificada.  
  
  **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Menu padrão](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303-010_MenuDefault")<br /><br /> **Menu**|Segundo plano|`Environment.CommandBarMenuBackgroundGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Menu padrão](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303-010_MenuDefault")<br /><br /> **Menu**|Primeiro plano (texto)|`Environment.CommandBarTextActive`|  
|![Menu padrão](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303-010_MenuDefault")<br /><br /> **Menu**|Primeiro plano (glifo do submenu)|`Environment.CommandBarMenuSubmenuGlyph`|  
|![Menu padrão](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303-010_MenuDefault")<br /><br /> **Menu**|Borda|`Environment.CommandBarMenuBorder`|  
|![Menu padrão](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303-010_MenuDefault")<br /><br /> **Menu**|Plano de fundo do canal de ícone|`Environment.CommandBarMenuIconBackground`|  
|![Menu padrão](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303-010_MenuDefault")<br /><br /> **Menu**|Separador|`Environment.CommandBarMenuSeparator`|  
|![Menu padrão](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303-010_MenuDefault")<br /><br /> **Menu**|Shadow|`Environment.DropShadowBackground`|  
|![Menu marcado](../extensibility/ux-guidelines/media/0303-011-menuchecked.png "0303-011_MenuChecked")<br /><br /> **Check**|Marca de seleção|`Environment.CommandBarCheckBox`|  
|![Menu marcado](../extensibility/ux-guidelines/media/0303-011-menuchecked.png "0303-011_MenuChecked")<br /><br /> **Check**|Plano de fundo de marca de seleção|`Environment.CommandBarSelectedIcon`|  
|![Menu selecionado](../extensibility/ux-guidelines/media/0303-012-menuselected.png "0303-012_MenuSelected")<br /><br /> **Selected**|Plano de fundo do ícone|`Environment.CommandBarSelected`|  
|![Menu selecionado](../extensibility/ux-guidelines/media/0303-012-menuselected.png "0303-012_MenuSelected")<br /><br /> **Selected**|Borda do ícone|`Environment.CommandBarSelectedBorder`|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Focalização do menu](../extensibility/ux-guidelines/media/0303-013-menuhover.png "0303-013_MenuHover")<br /><br /> **Item de menu**|Segundo plano|`Environment.CommandBarMenuItemMouseOver`|  
|![Focalização do menu](../extensibility/ux-guidelines/media/0303-013-menuhover.png "0303-013_MenuHover")<br /><br /> **Item de menu**|Primeiro plano (texto)|`Environment.CommandBarMenuItemMouseOver`|  
|![Focalização do menu](../extensibility/ux-guidelines/media/0303-013-menuhover.png "0303-013_MenuHover")<br /><br /> **Item de menu**|Primeiro plano (glifo do submenu)|`Environment.CommandBarMenuMouseOverSubmenuGlyph`|  
|![Foco do menu verificado](../extensibility/ux-guidelines/media/0303-014-menuhoverchecked.png "0303-014_MenuHoverChecked")<br /><br /> **Check**|Marca de seleção|`Environment.CommandBarCheckBoxMouseOver`|  
|![Foco do menu verificado](../extensibility/ux-guidelines/media/0303-014-menuhoverchecked.png "0303-014_MenuHoverChecked")<br /><br /> **Check**|Plano de fundo de marca de seleção|`Environment.CommandBarHoverOverSelectedIcon`|  
|![Menu focalizado selecionado](../extensibility/ux-guidelines/media/0303-015-menuhoverselected.png "0303-015_MenuHoverSelected")<br /><br /> **Selected**|Plano de fundo do ícone|`Environment.CommandBarHoverOverSelected`|  
|![Menu focalizado selecionado](../extensibility/ux-guidelines/media/0303-015-menuhoverselected.png "0303-015_MenuHoverSelected")<br /><br /> **Selected**|Borda do ícone|`Environment.CommandBarHoverOverSelectedIconBorder`|  
  
 **Desabilitado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Menu desabilitado](../extensibility/ux-guidelines/media/0303-016-menudisabled.png "0303-016_MenuDisabled")<br /><br /> Item de menu|Primeiro plano (texto)|`Environment.CommandBarTextInactive`|  
|![Menu desabilitado](../extensibility/ux-guidelines/media/0303-016-menudisabled.png "0303-016_MenuDisabled")<br /><br /> Item de menu|Primeiro plano (glifo do submenu)|`Environment.CommandBarMenuSubmenuGlyph`|  
|![Menu desabilitado marcado](../extensibility/ux-guidelines/media/0303-017-menudisabledchecked.png "0303-017_MenuDisabledChecked")<br /><br /> Verificado|Marca de seleção|`Environment.CommandBarCheckBoxDisabled`|  
|![Menu desabilitado marcado](../extensibility/ux-guidelines/media/0303-017-menudisabledchecked.png "0303-017_MenuDisabledChecked")<br /><br /> Verificado|Plano de fundo de marca de seleção|`Environment.CommandBarSelectedIconDisabled`|  
  
#### <a name="command-bar"></a>Barra de comandos  
 A barra de comandos pode aparecer em vários locais no IDE do Visual Studio, mais notavelmente a prateleira de comandos e incorporada em janelas de ferramentas ou documentos.  
  
 Em geral, sempre use a implementação da barra de comandos padrão fornecida pelo ambiente do Visual Studio. O uso do mecanismo padrão garante que todos os detalhes visuais apareçam corretamente e que os elementos interativos se comportem de forma consistente com outros controles de barra de comandos do Visual Studio. No entanto, se for necessário que você crie sua própria barra de comandos, certifique-se de estilizar corretamente usando os nomes de token a seguir.  
  
 ![Redline da barra de comandos](../extensibility/ux-guidelines/media/0303-018-commandbarredline.png "0303-018_CommandBarRedline")  
  
 ![Botão de estouro Redline](../extensibility/ux-guidelines/media/0303-019-overflowbuttonredline.png "0303-019_OverflowButtonRedline")  
  
 Usar...  
 em locais onde você precisa de uma barra de comandos inserida, mas não é possível usar a implementação padrão da barra de comandos do Visual Studio.  
  
Não use...  
- para elementos de interface do usuário que não são semelhantes a uma barra de comandos.  

- para componentes da barra de comandos diferentes daqueles para os quais os nomes de token são especificados.  
  
##### <a name="command-bar-group"></a>Grupo de barras de comando  
 Um grupo de barras de comando consiste em um conjunto relacionado de controles de barra de comandos e pode conter qualquer número de botões, botões de divisão, menus suspensos, caixas de combinação ou menus. As cores desses controles são regulamentadas por nomes de token separados e são discutidas individualmente em outro lugar neste guia. Uma linha separadora é usada para dividir um grupo de barras de comandos em subgrupos relacionados.  
  
 ![Grupo de barras de comandos Redline](../extensibility/ux-guidelines/media/0303-020-commandbargroupredline.png "0303-020_CommandBarGroupRedline")  
  
 Usar...  
 em locais onde você precisa de uma barra de comandos inserida, mas não é possível usar a implementação padrão da barra de comandos do Visual Studio.  
  
Não use...  
- para elementos de interface do usuário que não são semelhantes a uma barra de comandos.  

- para componentes da barra de comandos diferentes daqueles para os quais os nomes de token são especificados.  
  
  **Padrão** (nenhum outro Estado)  
  
|Elemento|Nome do token: categoria. cor|  
|-------------|--------------------------------|  
|Segundo plano|`Environment.CommandBarGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|Borda|`Environment.CommandBarToolBarBorder`|  
|Identificador de arrastar|`Environment.CommandBarDragHandle`|  
|Separador|`Environment.CommandBarToolBarSeparator`<br /><br /> `Environment.CommandBarToolBarSeparatorHighlight`|  
  
##### <a name="command-icons"></a>Ícones de comando  
 ![Ícone de comando Redline](../extensibility/ux-guidelines/media/0303-021-commandiconredline1.png "0303-021_CommandIconRedline1")  
  
 ![Ícone de comando Redline](../extensibility/ux-guidelines/media/0303-022-commandiconredline2.png "0303-022_CommandIconRedline2")  
  
 Usar...  
 para todos os botões que serão colocados em uma barra de comandos.  
  
Não use...  
- para controles que têm seus próprios nomes de token.  

- em qualquer combinação de plano de fundo/primeiro plano diferente de especificada.  
  
  **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Ícone de comando padrão](../extensibility/ux-guidelines/media/0303-023-commandicondefault.png "0303-023_CommandIconDefault")<br /><br /> **Default**|Segundo plano|N/A (herda do plano de fundo da barra de comandos)|  
|![Ícone de comando padrão](../extensibility/ux-guidelines/media/0303-023-commandicondefault.png "0303-023_CommandIconDefault")<br /><br /> **Default**|Primeiro plano (texto)|`Environment.CommandBarTextActive`|  
|![Ícone de comando padrão](../extensibility/ux-guidelines/media/0303-023-commandicondefault.png "0303-023_CommandIconDefault")<br /><br /> **Default**|Borda|N/D|  
|![Ícone de comando padrão selecionado](../extensibility/ux-guidelines/media/0303-024-commandicondefaultselected.png "0303-024_CommandIconDefaultSelected")<br /><br /> **Selected**|Segundo plano|`Environment.CommandBarSelected`|  
|![Ícone de comando padrão selecionado](../extensibility/ux-guidelines/media/0303-024-commandicondefaultselected.png "0303-024_CommandIconDefaultSelected")<br /><br /> **Selected**|Primeiro plano (texto)|`Environment.CommandBarTextSelected`|  
|![Ícone de comando padrão selecionado](../extensibility/ux-guidelines/media/0303-024-commandicondefaultselected.png "0303-024_CommandIconDefaultSelected")<br /><br /> **Selected**|Borda|`Environment.CommandBarSelectedBorder`|  
  
 **Foco e teclado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Ícone de comando focalizado](../extensibility/ux-guidelines/media/0303-025-commandiconhover.png "0303-025_CommandIconHover")<br /><br /> **Padrão ao focalizar**|Segundo plano|`Environment.CommandBarMouseOverBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Ícone de comando focalizado](../extensibility/ux-guidelines/media/0303-025-commandiconhover.png "0303-025_CommandIconHover")<br /><br /> **Padrão ao focalizar**|Primeiro plano (texto)|`Environment.CommandBarTextHover`|  
|![Ícone de comando focalizado](../extensibility/ux-guidelines/media/0303-025-commandiconhover.png "0303-025_CommandIconHover")<br /><br /> **Padrão ao focalizar**|Borda|`Environment.CommandBarBorder`|  
|![Ícone de comando com foco selecionado](../extensibility/ux-guidelines/media/0303-026-commandiconhoverselected.png "0303-026_CommandIconHoverSelected")<br /><br /> **Selecionado ao focalizar**|Segundo plano|`Environment.CommandBarHoverOverSelected`|  
|![Ícone de comando com foco selecionado](../extensibility/ux-guidelines/media/0303-026-commandiconhoverselected.png "0303-026_CommandIconHoverSelected")<br /><br /> **Selecionado ao focalizar**|Primeiro plano (texto)|`Environment.CommandBarTextHoverOverSelected`|  
|![Ícone de comando com foco selecionado](../extensibility/ux-guidelines/media/0303-026-commandiconhoverselected.png "0303-026_CommandIconHoverSelected")<br /><br /> **Selecionado ao focalizar**|Borda|`Environment.CommandBarHoverOverSelectedIconBorder`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Ícone de comando pressionado](../extensibility/ux-guidelines/media/0303-027-commandiconpressed.png "0303-027_CommandIconPressed")<br /><br /> **Ícone de comando pressionado**|Segundo plano|`Environment.CommandBarMouseDownBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Ícone de comando pressionado](../extensibility/ux-guidelines/media/0303-027-commandiconpressed.png "0303-027_CommandIconPressed")<br /><br /> **Ícone de comando pressionado**|Primeiro plano (texto)|`Environment.CommandBarTextMouseDown`|  
|![Ícone de comando pressionado](../extensibility/ux-guidelines/media/0303-027-commandiconpressed.png "0303-027_CommandIconPressed")<br /><br /> **Ícone de comando pressionado**|Borda|`Environment.CommandBarBorder`|  
  
 **Desabilitado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Ícone de comando desabilitado](../extensibility/ux-guidelines/media/0303-028-commandicondisabled.png "0303-028_CommandIconDisabled")<br /><br /> **Ícone de comando desabilitado**|Segundo plano|N/A (herda do plano de fundo da barra de comandos)|  
|![Ícone de comando desabilitado](../extensibility/ux-guidelines/media/0303-028-commandicondisabled.png "0303-028_CommandIconDisabled")<br /><br /> **Ícone de comando desabilitado**|Primeiro plano (texto)|`Environment.CommandBarTextInactive`|  
|![Ícone de comando desabilitado](../extensibility/ux-guidelines/media/0303-028-commandicondisabled.png "0303-028_CommandIconDisabled")<br /><br /> **Ícone de comando desabilitado**|Borda|N/D|  
  
##### <a name="combo-box"></a><a name="BKMK_CommandComboBox"></a>Caixa de combinação  
  
> [!IMPORTANT]
> As caixas de combinação são semelhantes a menus suspensos, mas incluem uma região de texto editável. Se o menu suspenso não incluir uma região de texto editável, use os tokens de cor encontrados na [lista](../misc/shared-colors.md#BKMK_CommandDropDown)suspensa.  
  
 ![Redline da caixa de combinação](../extensibility/ux-guidelines/media/0303-029-comboboxredline.png "0303-029_ComboBoxRedline")  
  
Usar...  
- ao criar caixas de combinação personalizadas.  

- ao criar um controle da barra de comandos semelhante a uma caixa de combinação.  

Não use...  
- para tudo o que você não quer que corresponda sempre à interface do usuário da barra de comandos.  

- Quando você tem acesso a uma caixa de combinação com estilo.  
  
  **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Campo de entrada da caixa de combinação](../extensibility/ux-guidelines/media/0303-030-comboboxinputfield.png "0303-030_ComboBoxInputField")<br /><br /> **Campo de entrada**|Segundo plano|`Environment.ComboBoxBackground`|  
|![Campo de entrada da caixa de combinação](../extensibility/ux-guidelines/media/0303-030-comboboxinputfield.png "0303-030_ComboBoxInputField")<br /><br /> **Campo de entrada**|Primeiro plano (texto)|`Environment.ComboBoxText`|  
|![Campo de entrada da caixa de combinação](../extensibility/ux-guidelines/media/0303-030-comboboxinputfield.png "0303-030_ComboBoxInputField")<br /><br /> **Campo de entrada**|Borda|`Environment.ComboBoxBorder`|  
|![Campo de entrada da caixa de combinação](../extensibility/ux-guidelines/media/0303-030-comboboxinputfield.png "0303-030_ComboBoxInputField")<br /><br /> **Campo de entrada**|Separador|Sem separador|  
|![Botão de remoção de&#45;caixa de combinação](../extensibility/ux-guidelines/media/0303-031-comboboxdropdownbutton.png "0303-031_ComboBoxDropdownButton")<br /><br /> **Botão suspenso**|Segundo plano|N/A (herda)|  
|![Botão de remoção de&#45;caixa de combinação](../extensibility/ux-guidelines/media/0303-031-comboboxdropdownbutton.png "0303-031_ComboBoxDropdownButton")<br /><br /> **Botão suspenso**|Primeiro plano (glifo)|`Environment.ComboBoxGlyph`|  
|![Caixa de combinação&#47;drop&#45;lista suspensa](../extensibility/ux-guidelines/media/0303-032-comboboxdropdownlist.png "0303-032_ComboBoxDropdownList")<br /><br /> **Lista suspensa**|Segundo plano|`Environment.ComboBoxPopupBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Caixa de combinação&#47;drop&#45;lista suspensa](../extensibility/ux-guidelines/media/0303-032-comboboxdropdownlist.png "0303-032_ComboBoxDropdownList")<br /><br /> **Lista suspensa**|Primeiro plano (texto)|`Environment.ComboBoxItemText`|  
|![Caixa de combinação&#47;drop&#45;lista suspensa](../extensibility/ux-guidelines/media/0303-032-comboboxdropdownlist.png "0303-032_ComboBoxDropdownList")<br /><br /> **Lista suspensa**|Borda|`Environment.ComboBoxPopupBorder`|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Campo de entrada da caixa de combinação ao focalizar](../extensibility/ux-guidelines/media/0303-033-comboboxinputfieldhover.png "0303-033_ComboBoxInputFieldHover")<br /><br /> **Campo de entrada**|Segundo plano|`Environment.ComboBoxMouseOverBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Campo de entrada da caixa de combinação ao focalizar](../extensibility/ux-guidelines/media/0303-033-comboboxinputfieldhover.png "0303-033_ComboBoxInputFieldHover")<br /><br /> **Campo de entrada**|Primeiro plano (texto)|`Environment.ComboBoxMouseOverText`|  
|![Campo de entrada da caixa de combinação ao focalizar](../extensibility/ux-guidelines/media/0303-033-comboboxinputfieldhover.png "0303-033_ComboBoxInputFieldHover")<br /><br /> **Campo de entrada**|Borda|`Environment.ComboBoxMouseOverBorder`|  
|![Campo de entrada da caixa de combinação ao focalizar](../extensibility/ux-guidelines/media/0303-033-comboboxinputfieldhover.png "0303-033_ComboBoxInputFieldHover")<br /><br /> **Campo de entrada**|Separador|`Environment.ComboBoxMouseOverSeparator`|  
|![Caixa de combinação&#47;soltar&#45;botão para baixo ao focalizar](../extensibility/ux-guidelines/media/0303-034-comboboxdropdownbuttonhover.png "0303-034_ComboBoxDropdownButtonHover")<br /><br /> **Botão suspenso**|Segundo plano|`Environment.ComboBoxButtonMouseOverBackground`|  
|![Caixa de combinação&#47;soltar&#45;botão para baixo ao focalizar](../extensibility/ux-guidelines/media/0303-034-comboboxdropdownbuttonhover.png "0303-034_ComboBoxDropdownButtonHover")<br /><br /> **Botão suspenso**|Primeiro plano (glifo)|`Environment.ComboBoxMouseOverGlyph`|  
|![Caixa de combinação&#47;drop&#45;lista suspensa ao focalizar](../extensibility/ux-guidelines/media/0303-035-comboboxdropdownlisthover.png "0303-035_ComboBoxDropdownListHover")<br /><br /> **Lista suspensa**|Plano de fundo (item de menu)|`Environment.ComboBoxItemMouseOverBackground`|  
|![Caixa de combinação&#47;drop&#45;lista suspensa ao focalizar](../extensibility/ux-guidelines/media/0303-035-comboboxdropdownlisthover.png "0303-035_ComboBoxDropdownListHover")<br /><br /> **Lista suspensa**|Primeiro plano (texto)|`Environment.ComboBoxItemMouseOverText`|  
|![Caixa de combinação&#47;drop&#45;lista suspensa ao focalizar](../extensibility/ux-guidelines/media/0303-035-comboboxdropdownlisthover.png "0303-035_ComboBoxDropdownListHover")<br /><br /> **Lista suspensa**|Border (item de menu)|`Environment.ComboBoxItemMouseOverBorder`|  
  
 **Focused**  
  
|Componente|Elemento|Nome do token: Color. Category|  
|---------------|-------------|--------------------------------|  
|![Foco no campo de entrada da caixa de combinação](../extensibility/ux-guidelines/media/0303-036-comboboxinputfieldfocused.png "0303-036_ComboBoxInputFieldFocused")<br /><br /> **Campo de entrada**|Segundo plano|`Environment.ComboBoxFocusedBackground`|  
|![Foco no campo de entrada da caixa de combinação](../extensibility/ux-guidelines/media/0303-036-comboboxinputfieldfocused.png "0303-036_ComboBoxInputFieldFocused")<br /><br /> **Campo de entrada**|Primeiro plano (texto)|`Environment.ComboBoxFocusedText`|  
|![Foco no campo de entrada da caixa de combinação](../extensibility/ux-guidelines/media/0303-036-comboboxinputfieldfocused.png "0303-036_ComboBoxInputFieldFocused")<br /><br /> **Campo de entrada**|Borda|`Environment.ComboBoxFocusedBorder`|  
|![Foco no campo de entrada da caixa de combinação](../extensibility/ux-guidelines/media/0303-036-comboboxinputfieldfocused.png "0303-036_ComboBoxInputFieldFocused")<br /><br /> **Campo de entrada**|Separador|`Environment.ComboBoxFocusedButtonSeparator`|  
|![Caixa de combinação&#47;botão de soltar&#45;com foco](../extensibility/ux-guidelines/media/0303-037-comboboxdropdownbuttonfocused.png "0303-037_ComboBoxDropdownButtonFocused")<br /><br /> **Botão suspenso**|Segundo plano|`Environment.ComboBoxFocusedButtonBackground`|  
|![Caixa de combinação&#47;botão de soltar&#45;com foco](../extensibility/ux-guidelines/media/0303-037-comboboxdropdownbuttonfocused.png "0303-037_ComboBoxDropdownButtonFocused")<br /><br /> **Botão suspenso**|Primeiro plano (glifo)|`Environment.ComboBoxFocusedGlyph`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: Color. Category|  
|---------------|-------------|--------------------------------|  
|![Campo de entrada da caixa de combinação pressionado](../extensibility/ux-guidelines/media/0303-038-comboboxinputfieldpressed.png "0303-038_ComboBoxInputFieldPressed")<br /><br /> **Campo de entrada**|Segundo plano|`Environment.ComboBoxMouseDownBackground`|  
|![Campo de entrada da caixa de combinação pressionado](../extensibility/ux-guidelines/media/0303-038-comboboxinputfieldpressed.png "0303-038_ComboBoxInputFieldPressed")<br /><br /> **Campo de entrada**|Primeiro plano (texto)|`Environment.ComboBoxMouseDownText`|  
|![Campo de entrada da caixa de combinação pressionado](../extensibility/ux-guidelines/media/0303-038-comboboxinputfieldpressed.png "0303-038_ComboBoxInputFieldPressed")<br /><br /> **Campo de entrada**|Borda|`Environment.ComboBoxMouseDownBorder`|  
|![Campo de entrada da caixa de combinação pressionado](../extensibility/ux-guidelines/media/0303-038-comboboxinputfieldpressed.png "0303-038_ComboBoxInputFieldPressed")<br /><br /> **Campo de entrada**|Separador|`Environment.ComboBoxMouseDownSeparator`|  
|![Caixa de combinação&#47;soltar&#45;botão pressionado](../extensibility/ux-guidelines/media/0303-039-comboboxdropdownbuttonpressed.png "0303-039_ComboBoxDropdownButtonPressed")<br /><br /> **Botão suspenso**|Segundo plano|`Environment.ComboBoxButtonMouseDownBackground`|  
|![Caixa de combinação&#47;soltar&#45;botão pressionado](../extensibility/ux-guidelines/media/0303-039-comboboxdropdownbuttonpressed.png "0303-039_ComboBoxDropdownButtonPressed")<br /><br /> **Botão suspenso**|Primeiro plano (glifo)|`Environment.ComboBoxMouseDownGlyph`|  
  
 **Desabilitado**  
  
|Componente|Elemento|Nome do token: Color. Category|  
|---------------|-------------|--------------------------------|  
|![Campo de entrada da caixa de combinação desabilitado](../extensibility/ux-guidelines/media/0303-041-comboboxinputfielddisabled.png "0303-041_ComboBoxInputFieldDisabled")<br /><br /> **Campo de entrada**|Segundo plano|`Environment.ComboBoxDisabledBackground`|  
|![Campo de entrada da caixa de combinação desabilitado](../extensibility/ux-guidelines/media/0303-041-comboboxinputfielddisabled.png "0303-041_ComboBoxInputFieldDisabled")<br /><br /> **Campo de entrada**|Primeiro plano (texto)|`Environment.ComboBoxDisabledText`|  
|![Campo de entrada da caixa de combinação desabilitado](../extensibility/ux-guidelines/media/0303-041-comboboxinputfielddisabled.png "0303-041_ComboBoxInputFieldDisabled")<br /><br /> **Campo de entrada**|Borda|`Environment.ComboBoxDisabledBorder`|  
|![Campo de entrada da caixa de combinação desabilitado](../extensibility/ux-guidelines/media/0303-041-comboboxinputfielddisabled.png "0303-041_ComboBoxInputFieldDisabled")<br /><br /> **Campo de entrada**|Separador|Sem separador|  
|![Caixa de combinação&#47;soltar&#45;botão para baixo desabilitado](../extensibility/ux-guidelines/media/0303-040-comboboxdropdownbuttondisabled.png "0303-040_ComboBoxDropdownButtonDisabled")<br /><br /> **Botão suspenso**|Segundo plano|Nenhum|  
|![Caixa de combinação&#47;soltar&#45;botão para baixo desabilitado](../extensibility/ux-guidelines/media/0303-040-comboboxdropdownbuttondisabled.png "0303-040_ComboBoxDropdownButtonDisabled")<br /><br /> **Botão suspenso**|Primeiro plano (glifo)|`Environment.ComboBoxDisabledGlyph`|  
  
##### <a name="drop-down"></a><a name="BKMK_CommandDropDown"></a>Lista suspensa  
  
> [!IMPORTANT]
> Os menus suspensos são semelhantes às caixas de combinação, mas não têm regiões de texto editáveis. Se a lista suspensa incluir uma região de texto editável, use os tokens de cor encontrados na [caixa de combinação](../misc/shared-colors.md#BKMK_CommandComboBox).  
  
 ![Soltar&#45;Redline para baixo](../extensibility/ux-guidelines/media/0303-042-dropdownredline.png "0303-042_DropdownRedline")  
  
 Usar...  
 Quando você estiver criando controles de lista suspensa personalizados.  
  
Não use...  
- para qualquer coisa que não seja semelhante a uma lista suspensa.  

- para caixas de combinação ou botões de divisão.  
  
  **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Descartar&#45;campo de seleção para baixo](../extensibility/ux-guidelines/media/0303-043-dropdownselectionfield.png "0303-043_DropdownSelectionField")<br /><br /> **Campo de seleção**|Segundo plano|`Environment.DropDownBackground`|  
|![Descartar&#45;campo de seleção para baixo](../extensibility/ux-guidelines/media/0303-043-dropdownselectionfield.png "0303-043_DropdownSelectionField")<br /><br /> **Campo de seleção**|Primeiro plano (texto)|`DropDownText`|  
|![Descartar&#45;campo de seleção para baixo](../extensibility/ux-guidelines/media/0303-043-dropdownselectionfield.png "0303-043_DropdownSelectionField")<br /><br /> **Campo de seleção**|Borda|`DropDownBorder`|  
|![Descartar&#45;campo de seleção para baixo](../extensibility/ux-guidelines/media/0303-043-dropdownselectionfield.png "0303-043_DropdownSelectionField")<br /><br /> **Campo de seleção**|Separador|Sem separador|  
|![Botão de soltar&#45;para baixo](../extensibility/ux-guidelines/media/0303-044-dropdownbutton.png "0303-044_DropdownButton")<br /><br /> **Botão suspenso**|Segundo plano|Nenhum|  
|![Botão de soltar&#45;para baixo](../extensibility/ux-guidelines/media/0303-044-dropdownbutton.png "0303-044_DropdownButton")<br /><br /> **Botão suspenso**|Primeiro plano (glifo)|`Environment.DropDownGlyph`|  
|![&#45;lista suspensa](../extensibility/ux-guidelines/media/0303-045-dropdownlist.png "0303-045_DropdownList")<br /><br /> **Lista suspensa**|Segundo plano|`Environment.DropDownPopupBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![&#45;lista suspensa](../extensibility/ux-guidelines/media/0303-045-dropdownlist.png "0303-045_DropdownList")<br /><br /> **Lista suspensa**|Primeiro plano (texto)|`Environment.ComboBoxItemText`|  
|![&#45;lista suspensa](../extensibility/ux-guidelines/media/0303-045-dropdownlist.png "0303-045_DropdownList")<br /><br /> **Lista suspensa**|Borda|`Environment.DropDownPopupBorder`|  
|![&#45;lista suspensa](../extensibility/ux-guidelines/media/0303-045-dropdownlist.png "0303-045_DropdownList")<br /><br /> **Lista suspensa**|Shadow|`Environment.DropShadowBackground`|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Descartar&#45;campo de seleção para baixo ao focalizar](../extensibility/ux-guidelines/media/0303-046-dropdownselectionfieldhover.png "0303-046_DropdownSelectionFieldHover")<br /><br /> **Campo de seleção**|Segundo plano|`Environment.DropDownMouseOverBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Descartar&#45;campo de seleção para baixo ao focalizar](../extensibility/ux-guidelines/media/0303-046-dropdownselectionfieldhover.png "0303-046_DropdownSelectionFieldHover")<br /><br /> **Campo de seleção**|Primeiro plano (texto)|`Environment.DropDownMouseOverText`|  
|![Descartar&#45;campo de seleção para baixo ao focalizar](../extensibility/ux-guidelines/media/0303-046-dropdownselectionfieldhover.png "0303-046_DropdownSelectionFieldHover")<br /><br /> **Campo de seleção**|Borda|`Environment.DropDownMouseOverBorder`|  
|![Descartar&#45;campo de seleção para baixo ao focalizar](../extensibility/ux-guidelines/media/0303-046-dropdownselectionfieldhover.png "0303-046_DropdownSelectionFieldHover")<br /><br /> **Campo de seleção**|Separador|`Environment.DropDownButtonMouseOverSeparator`|  
|![Botão de soltar&#45;para baixo ao focalizar](../extensibility/ux-guidelines/media/0303-047-dropdownbuttonhover.png "0303-047_DropdownButtonHover")<br /><br /> **Botão suspenso**|Segundo plano|`Environment.DropDownButtonMouseOverBackground`|  
|![Botão de soltar&#45;para baixo ao focalizar](../extensibility/ux-guidelines/media/0303-047-dropdownbuttonhover.png "0303-047_DropdownButtonHover")<br /><br /> **Botão suspenso**|Primeiro plano (glifo)|`Environment.DropDownMouseOverGlyph`|  
|![Soltar&#45;lista suspensa ao focalizar](../extensibility/ux-guidelines/media/0303-048-dropdownlisthover.png "0303-048_DropdownListHover")<br /><br /> **Lista suspensa**|Plano de fundo (item de menu)|`Environment.ComboBoxItemMouseOverBackground`|  
|![Soltar&#45;lista suspensa ao focalizar](../extensibility/ux-guidelines/media/0303-048-dropdownlisthover.png "0303-048_DropdownListHover")<br /><br /> **Lista suspensa**|Primeiro plano (texto)|`Environment.ComboBoxItemMouseOverText`|  
|![Soltar&#45;lista suspensa ao focalizar](../extensibility/ux-guidelines/media/0303-048-dropdownlisthover.png "0303-048_DropdownListHover")<br /><br /> **Lista suspensa**|Border (item de menu)|`Environment.ComboBoxItemMouseOverBorder`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Descartar&#45;campo de seleção pressionado](../extensibility/ux-guidelines/media/0303-049-dropdownselectionfieldpressed.png "0303-049_DropdownSelectionFieldPressed")<br /><br /> **Campo de seleção**|Segundo plano|`Environment.DropDownMouseDownBackground`|  
|![Descartar&#45;campo de seleção pressionado](../extensibility/ux-guidelines/media/0303-049-dropdownselectionfieldpressed.png "0303-049_DropdownSelectionFieldPressed")<br /><br /> **Campo de seleção**|Primeiro plano (texto)|`Environment.DropDownMouseDownText`|  
|![Descartar&#45;campo de seleção pressionado](../extensibility/ux-guidelines/media/0303-049-dropdownselectionfieldpressed.png "0303-049_DropdownSelectionFieldPressed")<br /><br /> **Campo de seleção**|Borda|`Environment.DropDownMouseDownBorder`|  
|![Descartar&#45;campo de seleção pressionado](../extensibility/ux-guidelines/media/0303-049-dropdownselectionfieldpressed.png "0303-049_DropdownSelectionFieldPressed")<br /><br /> **Campo de seleção**|Separador|`Environment.DropDownButtonMouseDownSeparator`|  
|![Botão de soltar&#45;pressionado](../extensibility/ux-guidelines/media/0303-050-dropdownbuttonpressed.png "0303-050_DropdownButtonPressed")<br /><br /> **Botão suspenso**|Segundo plano|`Environment.DropDownButtonMouseDownBackground`|  
|![Botão de soltar&#45;pressionado](../extensibility/ux-guidelines/media/0303-050-dropdownbuttonpressed.png "0303-050_DropdownButtonPressed")<br /><br /> **Botão suspenso**|Primeiro plano (glifo)|`Environment.DropDownMouseDownGlyph`|  
  
 **Desabilitado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Descartar&#45;campo de seleção desativado](../extensibility/ux-guidelines/media/0303-051-dropdownselectionfielddisabled.png "0303-051_DropdownSelectionFieldDisabled")|Segundo plano|`Environment.DropDownDisabledBackground`|  
|![Descartar&#45;campo de seleção desativado](../extensibility/ux-guidelines/media/0303-051-dropdownselectionfielddisabled.png "0303-051_DropdownSelectionFieldDisabled")|Primeiro plano (texto)|`Environment.DropDownDisabledText`|  
|![Descartar&#45;campo de seleção desativado](../extensibility/ux-guidelines/media/0303-051-dropdownselectionfielddisabled.png "0303-051_DropdownSelectionFieldDisabled")|Borda|`Environment.DropDownDisabledBorder`|  
|![Descartar&#45;campo de seleção desativado](../extensibility/ux-guidelines/media/0303-051-dropdownselectionfielddisabled.png "0303-051_DropdownSelectionFieldDisabled")|Separador|Sem separador|  
|![Botão de soltar&#45;desativado](../extensibility/ux-guidelines/media/0303-052-dropdownbuttondisabled.png "0303-052_DropdownButtonDisabled")|Segundo plano|N/D|  
|![Botão de soltar&#45;desativado](../extensibility/ux-guidelines/media/0303-052-dropdownbuttondisabled.png "0303-052_DropdownButtonDisabled")|Primeiro plano (glifo)|`Environment.DropDownDisabledGlyph`|  
  
##### <a name="split-button"></a>Botão de divisão  
 Os botões de divisão compartilham vários nomes de token com outros controles de barra de comandos, como botões, menus e texto da barra de comandos. Todos os nomes de token de ações e botões suspensos necessários são repetidos aqui para sua conveniência. As listas suspensas do botão de divisão são implementações dos [menus](../misc/shared-colors.md#BKMK_CommandMenus)da barra de comandos.  
  
 ![Botão de divisão Redline](../extensibility/ux-guidelines/media/0303-053-splitbuttonredline.png "0303-053_SplitButtonRedline")  
  
 Usar...  
 Quando você estiver criando um botão de divisão personalizado.  
  
Não use...  
- para outros tipos de botões.  

- em qualquer combinação de plano de fundo/primeiro plano diferente de especificada.  
  
  **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Botão de divisão](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303-054_SplitButton")<br /><br /> **Botão de divisão (padrão)**|Segundo plano|Nenhum|  
|![Botão de divisão](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303-054_SplitButton")<br /><br /> **Botão de divisão (padrão)**|Primeiro plano (texto)|`Environment.CommandBarTextActive`|  
|![Botão de divisão](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303-054_SplitButton")<br /><br /> **Botão de divisão (padrão)**|Primeiro plano (glifo)|`Environment.CommandBarSplitButtonGlyph`|  
|![Botão de divisão](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303-054_SplitButton")<br /><br /> **Botão de divisão (padrão)**|Borda|N/D|  
|![Botão de divisão](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303-054_SplitButton")<br /><br /> **Botão de divisão (padrão)**|Separador|N/D|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Botão de divisão em foco](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303-055_SplitButtonHover")<br /><br /> **Botão de divisão (ao focalizar)**|Segundo plano|`Environment.CommandBarMouseOverBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Botão de divisão em foco](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303-055_SplitButtonHover")<br /><br /> **Botão de divisão (ao focalizar)**|Primeiro plano (texto)|`Environment.CommandBarTextHover`|  
|![Botão de divisão em foco](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303-055_SplitButtonHover")<br /><br /> **Botão de divisão (ao focalizar)**|Primeiro plano (glifo)|`Environment.CommandBarSplitButtonMouseOverGlyph`|  
|![Botão de divisão em foco](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303-055_SplitButtonHover")<br /><br /> **Botão de divisão (ao focalizar)**|Borda|`Environment.CommandBarBorder`|  
|![Botão de divisão em foco](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303-055_SplitButtonHover")<br /><br /> **Botão de divisão (ao focalizar)**|Separador|`Environment.CommandBarSplitButtonSeparator`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Botão de divisão pressionado](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303-056_SplitButtonPressed")<br /><br /> **Botão de divisão (pressionado)**|Segundo plano|`Environment.CommandBarMouseDownBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Botão de divisão pressionado](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303-056_SplitButtonPressed")<br /><br /> **Botão de divisão (pressionado)**|Primeiro plano (texto)|`Environment.CommandBarTextMouseDown`|  
|![Botão de divisão pressionado](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303-056_SplitButtonPressed")<br /><br /> **Botão de divisão (pressionado)**|Primeiro plano (glifo)|`Environment.CommandBarSplitButtonMouseDownGlyph`|  
|![Botão de divisão pressionado](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303-056_SplitButtonPressed")<br /><br /> **Botão de divisão (pressionado)**|Borda|`Environment.CommandBarBorder`|  
|![Botão de divisão pressionado](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303-056_SplitButtonPressed")<br /><br /> **Botão de divisão (pressionado)**|Separador|N/D|  
  
 **Desabilitado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Botão de divisão desabilitado](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br /><br /> **Botão de divisão (desabilitado)**|Segundo plano|N/D|  
|![Botão de divisão desabilitado](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br /><br /> **Botão de divisão (desabilitado)**|Primeiro plano (texto)|`Environment.ComboBoxItemTextInactive`|  
|![Botão de divisão desabilitado](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br /><br /> **Botão de divisão (desabilitado)**|Primeiro plano (glifo)|`Environment.CommandBarTextInactive`|  
|![Botão de divisão desabilitado](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br /><br /> **Botão de divisão (desabilitado)**|Borda|N/D|  
|![Botão de divisão desabilitado](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br /><br /> **Botão de divisão (desabilitado)**|Separador|N/D|  
  
##### <a name="more-options-and-overflow-buttons"></a>Botões ' mais opções ' e ' estouro '  
 O botão "mais opções" é usado quando um grupo de barras de comandos é personalizável com a adição ou remoção de botões de barra de comandos relacionados. O botão "estouro" é exibido quando uma barra de comandos é truncada devido à falta de espaço horizontal e, ao clicar, mostra um menu contendo os botões da barra de comandos que não podem ser exibidos. As cores desses dois botões são controladas pelo mesmo conjunto de nomes de token.  
  
 ![Mais opções Redline](../extensibility/ux-guidelines/media/0303-058-moreoptionsredline.png "0303-058_MoreOptionsRedline")  
  
 Usar...  
 para os botões ' mais opções ' ou ' estouro ' personalizados.  
  
 Não use...  
 para botões que não têm funcionalidade semelhante a um botão ' mais opções ' ou ' estouro '.  
  
 **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Mais opções](../extensibility/ux-guidelines/media/0303-059-moreoptions.png "0303-059_MoreOptions")<br /><br /> **Mais opções**|Segundo plano|`Environment.CommandBarOptionsBackground`|  
|![Mais opções](../extensibility/ux-guidelines/media/0303-059-moreoptions.png "0303-059_MoreOptions")<br /><br /> **Mais opções**|Primeiro plano (glifo)|`Environment.CommandBarOptionsGlyph`|  
|![Botão de estouro](../extensibility/ux-guidelines/media/0303-060-overflow.png "0303-060_Overflow")<br /><br /> **Contra**|Segundo plano|`Environment.CommandBarOptionsBackground`|  
|![Botão de estouro](../extensibility/ux-guidelines/media/0303-060-overflow.png "0303-060_Overflow")<br /><br /> **Contra**|Primeiro plano (glifo)|`Environment.CommandBarOptionsGlyph`|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Mais opções ao focalizar](../extensibility/ux-guidelines/media/0303-061-moreoptionshover.png "0303-061_MoreOptionsHover")<br /><br /> **Mais opções**|Segundo plano|`Environment.CommandBarOptionsMouseOverBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Mais opções ao focalizar](../extensibility/ux-guidelines/media/0303-061-moreoptionshover.png "0303-061_MoreOptionsHover")<br /><br /> **Mais opções**|Primeiro plano (glifo)|`Environment.CommandBarOptionsMouseDownGlyph`|  
|![Estouro no foco](../extensibility/ux-guidelines/media/0303-062-overflowoptions.png "0303-062_OverflowOptions")<br /><br /> **Contra**|Segundo plano|`Environment.CommandBarOptionsMouseOverBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Estouro no foco](../extensibility/ux-guidelines/media/0303-062-overflowoptions.png "0303-062_OverflowOptions")<br /><br /> **Contra**|Primeiro plano (glifo)|`Environment.CommandBarOptionsMouseDownGlyph`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Mais opções pressionadas](../extensibility/ux-guidelines/media/0303-063-moreoptionspressed.png "0303-063_MoreOptionsPressed")<br /><br /> **Mais opções**|Segundo plano|`Environment.CommandBarOptionsMouseDownBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Mais opções pressionadas](../extensibility/ux-guidelines/media/0303-063-moreoptionspressed.png "0303-063_MoreOptionsPressed")<br /><br /> **Mais opções**|Primeiro plano (glifo)|`Environment.CommandBarOptionsMouseDownGlyph`|  
|![Estouro pressionado](../extensibility/ux-guidelines/media/0303-064-overflowpressed.png "0303-064_OverflowPressed")<br /><br /> **Contra**|Segundo plano|`Environment.CommandBarOptionsMouseDownBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Estouro pressionado](../extensibility/ux-guidelines/media/0303-064-overflowpressed.png "0303-064_OverflowPressed")<br /><br /> **Contra**|Primeiro plano (glifo)|`Environment.CommandBarOptionsMouseDownGlyph`|  
  
### <a name="document-windows"></a>Janelas de documentos  
 Não é necessário replicar as janelas de documentos, pois elas são fornecidas pelo ambiente do Visual Studio. No entanto, você pode decidir que deseja aproveitar as cores usadas em janelas de documentos para que sua interface do usuário sempre pareça consistente com essa parte do ambiente do Visual Studio.  
  
 Ao usar os tokens de cor da janela do documento, você deve ter cuidado para usá-los somente para elementos semelhantes e sempre em pares. Se você não fizer isso, terá resultados inesperados em sua interface do usuário.  
  
#### <a name="document-window-frame"></a>Quadro da janela do documento  
 As janelas de documentos podem ser encaixadas no IDE ou flutuantes como uma janela separada. Quando uma janela de documento está flutuante fora do IDE, ela ainda fica em um bom documento e tem cores de plano de fundo, borda, texto e tabulação que são iguais a quando ele faz parte do IDE. No entanto, o documento fica dentro de um quadro que tem suas próprias cores de plano de fundo, borda e texto. Quando janelas de ferramentas são encaixadas no documento bem, elas herdam o comportamento e a cor de suas guias dos nomes de token da janela do documento.  
  
 ![Janela de documento encaixada Redline](../extensibility/ux-guidelines/media/0303-065-dockeddocumentwindowredline.png "0303-065_DockedDocumentWindowRedline")  
  
 **Janela de documento encaixado**  
  
 ![Janela de documento flutuante Redline](../extensibility/ux-guidelines/media/0303-066-floatingdocumentwindowredline.png "0303-066_FloatingDocumentWindowRedline")  
  
 **Janela de documento flutuante**  
  
 Usar...  
 em qualquer lugar, você está criando a interface do usuário que deseja corresponder à janela do documento.  
  
 Não use...  
 para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema.  
  
 **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|Documento: encaixado ou flutuante|Segundo plano|Depende do tipo de documento|  
|Documento: encaixado ou flutuante|Primeiro plano (texto)|Depende do tipo de documento|  
|Documento: encaixado ou flutuante|Borda|`Environment.ToolWindowBorder`|  
|![Quadro focado](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303-067_FrameFocused")<br /><br /> **Quadro: flutuante, focado**|Segundo plano|`Environment.ToolWindowFloatingFrame`|  
|![Quadro focado](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303-067_FrameFocused")<br /><br /> **Quadro: flutuante, focado**|Primeiro plano (texto)|`Environment.ToolWindowFloatingFrame`|  
|![Quadro focado](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303-067_FrameFocused")<br /><br /> **Quadro: flutuante, focado**|Primeiro plano (glifo)|`Environment.RaftedWindowButtonActiveGlyph`|  
|![Quadro focado](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303-067_FrameFocused")<br /><br /> **Quadro: flutuante, focado**|Borda|`Environment.MainWindowActiveDefaultBorder`|  
|![Quadro focado](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303-067_FrameFocused")<br /><br /> **Quadro: flutuante, focado**|Borda (glifo)|`Environment.RaftedWindowButtonActiveBorder`<br /><br /> Definir como transparente|  
|![Quadro não focalizado](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303-068_FrameUnfocused")<br /><br /> **Quadro: flutuante, não focalizado**|Segundo plano|`Environment.ToolWindowFloatingFrameInactive`|  
|![Quadro não focalizado](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303-068_FrameUnfocused")<br /><br /> **Quadro: flutuante, não focalizado**|Primeiro plano (texto)|`Environment.ToolWindowFloatingFrameInactive`|  
|![Quadro não focalizado](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303-068_FrameUnfocused")<br /><br /> **Quadro: flutuante, não focalizado**|Primeiro plano (glifo)|`Environment.RaftedWindowButtonInactiveGlyph`|  
|![Quadro não focalizado](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303-068_FrameUnfocused")<br /><br /> **Quadro: flutuante, não focalizado**|Borda|`Environment.MainWindowInactiveBorder`|  
|![Quadro não focalizado](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303-068_FrameUnfocused")<br /><br /> **Quadro: flutuante, não focalizado**|Borda (glifo)|`Environment.RaftedWindowButtonInactiveBorder`<br /><br /> Definir como transparente|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Quadro com foco no foco](../extensibility/ux-guidelines/media/0303-069-framefocusedhover.png "0303-069_FrameFocusedHover")<br /><br /> **Quadro: flutuante, focado**|Plano de fundo (glifo)|`Environment.RaftedWindowButtonHoverActive`|  
|![Quadro com foco no foco](../extensibility/ux-guidelines/media/0303-069-framefocusedhover.png "0303-069_FrameFocusedHover")<br /><br /> **Quadro: flutuante, focado**|Primeiro plano (glifo)|`Environment.RaftedWindowButtonHoverActiveGlyph`|  
|![Quadro com foco no foco](../extensibility/ux-guidelines/media/0303-069-framefocusedhover.png "0303-069_FrameFocusedHover")<br /><br /> **Quadro: flutuante, focado**|Borda (glifo)|`Environment.RaftedWindowButtonHoverActiveBorder`|  
|![Quadro desfocado ao focalizar](../extensibility/ux-guidelines/media/0303-070-frameunfocusedhover.png "0303-070_FrameUnfocusedHover")<br /><br /> **Quadro: flutuante, não focalizado**|Plano de fundo (glifo)|`EnvironmentRaftedWindowButtonHoverInactive`|  
|![Quadro desfocado ao focalizar](../extensibility/ux-guidelines/media/0303-070-frameunfocusedhover.png "0303-070_FrameUnfocusedHover")<br /><br /> **Quadro: flutuante, não focalizado**|Primeiro plano (glifo)|`Environment.RaftedWindowButtonHoverInactiveGlyph`|  
|![Quadro desfocado ao focalizar](../extensibility/ux-guidelines/media/0303-070-frameunfocusedhover.png "0303-070_FrameUnfocusedHover")<br /><br /> **Quadro: flutuante, não focalizado**|Borda (glifo)|`Environment.RaftedWindowButtonHoverInactiveBorder`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Quadro com foco pressionado](../extensibility/ux-guidelines/media/0303-071-framefocusedpressed.png "0303-071_FrameFocusedPressed")<br /><br /> **Quadro: flutuante, focado**|Plano de fundo (glifo)|`Environment.RaftedWindowButtonDown`|  
|![Quadro com foco pressionado](../extensibility/ux-guidelines/media/0303-071-framefocusedpressed.png "0303-071_FrameFocusedPressed")<br /><br /> **Quadro: flutuante, focado**|Primeiro plano (glifo)|`Environment.RaftedWindowButtonDownGlyph`|  
|![Quadro com foco pressionado](../extensibility/ux-guidelines/media/0303-071-framefocusedpressed.png "0303-071_FrameFocusedPressed")<br /><br /> **Quadro: flutuante, focado**|Borda (glifo)|`Environment.RaftedWindowButtonDownBorder`|  
  
#### <a name="document-tabs"></a>Guias de documento  
 As guias de documento ficam no canal de guia para indicar quais documentos estão abertos no momento, juntamente com qual deles é o documento atual selecionado ou ativo. As janelas de ferramentas também podem ser encaixadas no canal da guia do documento se o usuário as colocar lá. Nessa situação, eles usam as mesmas cores de guia que as janelas de documentos. Se você estiver criando a interface do usuário que deseja sempre corresponder às cores da janela do documento (incluindo atualizações de tema ou se novos temas estiverem instalados), faça referência a esses tokens de cor.  
  
 ![Guia do documento Redline](../extensibility/ux-guidelines/media/0303-072-documenttabredline.png "0303-072_DocumentTabRedline")  
  
 Usar...  
 em qualquer lugar em que você estiver criando a interface do usuário que deseja corresponder às guias de documentos e selecionar automaticamente as atualizações de tema ou novas cores de tema.  
  
 Não use...  
 para qualquer interface do usuário que você não deseja alterar automaticamente quando o Shell tem uma atualização de tema.  
  
##### <a name="open-document-tabs"></a>Abrir guias de documento  
 Cada documento aberto tem uma guia no canal da guia do documento que exibe seu nome. Os documentos podem ser selecionados ou abertos em segundo plano, e suas guias refletem esses Estados:  
  
- A guia selecionada representa o documento que está atualmente exibido no documento. Uma guia selecionada tem uma borda de documento que se estende pela borda superior do documento bem.  
  
- As guias de segundo plano são guias de documentos que não são a guia selecionada no momento. Depois de clicados, eles se tornam a guia selecionada e adquirem todas as cores de plano de fundo, borda e texto desses nomes de token.  
  
  ![Abrir guia do documento Redline](../extensibility/ux-guidelines/media/0303-073-opendocumenttabredline.png "0303-073_OpenDocumentTabRedline")  
  
  Usar...  
  ao criar guias de documento personalizado.  
  
  Não use...  
  - para obter as guias provisórios (visualização).  
  
- para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema.  
  
##### <a name="selected-tab"></a>Guia selecionada  
 **Focused**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Guia selecionada com foco](../extensibility/ux-guidelines/media/0303-074-selectedtabfocused.png "0303-074_SelectedTabFocused")<br /><br /> **Guia documento selecionado, com foco**|Segundo plano|`Environment.FileTabSelectedGradientTop`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Guia selecionada com foco](../extensibility/ux-guidelines/media/0303-074-selectedtabfocused.png "0303-074_SelectedTabFocused")<br /><br /> **Guia documento selecionado, com foco**|Primeiro plano (texto)|`Environment.FileTabSelectedText`|  
|![Guia selecionada com foco](../extensibility/ux-guidelines/media/0303-074-selectedtabfocused.png "0303-074_SelectedTabFocused")<br /><br /> **Guia documento selecionado, com foco**|Borda|`Environment.FileTabSelectedBorder`<br /><br /> Defina para a mesma cor que o plano de fundo.|  
|![Guia selecionada com foco](../extensibility/ux-guidelines/media/0303-074-selectedtabfocused.png "0303-074_SelectedTabFocused")<br /><br /> **Guia documento selecionado, com foco**|Borda do documento|`Environment.FileTabDocumentBorderBackground`|  
  
 **Sem foco**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Guia selecionada desfocada](../extensibility/ux-guidelines/media/0303-075-selectedtabunfocused.png "0303-075_SelectedTabUnfocused")<br /><br /> **Guia documento selecionado, não focalizado**|Segundo plano|`Environment.FileTabInactiveGradientTop`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Guia selecionada desfocada](../extensibility/ux-guidelines/media/0303-075-selectedtabunfocused.png "0303-075_SelectedTabUnfocused")<br /><br /> **Guia documento selecionado, não focalizado**|Primeiro plano (texto)|`Environment.FileTabInactiveText`|  
|![Guia selecionada desfocada](../extensibility/ux-guidelines/media/0303-075-selectedtabunfocused.png "0303-075_SelectedTabUnfocused")<br /><br /> **Guia documento selecionado, não focalizado**|Borda|`Environment.FileTabInactiveBorder`<br /><br /> Defina para a mesma cor que o plano de fundo.|  
|![Guia selecionada desfocada](../extensibility/ux-guidelines/media/0303-075-selectedtabunfocused.png "0303-075_SelectedTabUnfocused")<br /><br /> **Guia documento selecionado, não focalizado**|Borda do documento|`Environment.FileTabInactiveDocumentBorderBackground`|  
  
##### <a name="background-tab"></a>Guia de segundo plano  
 **Default**  
  
|Componente|Elemento|Nome do token: Color. Category|  
|---------------|-------------|--------------------------------|  
|![Guia de segundo plano](../extensibility/ux-guidelines/media/0303-076-backgroundtab.png "0303-076_BackgroundTab")<br /><br /> **Padrão da guia de segundo plano**|Segundo plano|`Environment.FileTabBackground`|  
|![Guia de segundo plano](../extensibility/ux-guidelines/media/0303-076-backgroundtab.png "0303-076_BackgroundTab")<br /><br /> **Padrão da guia de segundo plano**|Primeiro plano (texto)|`Environment.FileTabText`|  
|![Guia de segundo plano](../extensibility/ux-guidelines/media/0303-076-backgroundtab.png "0303-076_BackgroundTab")<br /><br /> **Padrão da guia de segundo plano**|Borda|`Environment.FileTabBorder`<br /><br /> Defina para a mesma cor que o plano de fundo.|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: Color. Category|  
|---------------|-------------|--------------------------------|  
|![Guia em segundo plano ao focalizar](../extensibility/ux-guidelines/media/0303-077-backgroundtabhover.png "0303-077_BackgroundTabHover")<br /><br /> **Guia em segundo plano ao focalizar**|Segundo plano|`Environment.FileTabHotGradientTop`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Guia em segundo plano ao focalizar](../extensibility/ux-guidelines/media/0303-077-backgroundtabhover.png "0303-077_BackgroundTabHover")<br /><br /> **Guia em segundo plano ao focalizar**|Primeiro plano (texto)|`Environment.FileTabHotText`|  
|![Guia em segundo plano ao focalizar](../extensibility/ux-guidelines/media/0303-077-backgroundtabhover.png "0303-077_BackgroundTabHover")<br /><br /> **Guia em segundo plano ao focalizar**|Borda|`Environment.FileTabHotBorder`<br /><br /> Defina para a mesma cor que o plano de fundo.|  
  
##### <a name="preview-tab"></a>Guia de visualização  
 A guia Visualização é exibida no lado direito do canal da guia do documento quando o usuário clica em um item na janela de ferramentas do Gerenciador de Soluções. Ele atua como uma visualização do documento e também dá ao usuário a opção de manter o documento aberto no lado esquerdo do canal da guia do documento. Somente uma guia de visualização aberta pode ser aberta por vez. As guias de visualização têm os Estados de segundo plano e selecionados, como guias abertas e podem ser focadas ou desfocadas em seu estado ativo.  
  
 ![Guia de visualização Redline](../extensibility/ux-guidelines/media/0303-078-previewtabredline.png "0303-078_PreviewTabRedline")  
  
 Usar...  
 em qualquer lugar que você esteja criando a visualização provisória e queira que algum elemento corresponda à cor da guia de visualização atual.  
  
Não use...  
- para qualquer tipo de documento ou guia que não seja provisório (versão prévia).  

- para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema.  
  
  **Guia de visualização selecionada: focada**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Guia de visualização focada](../extensibility/ux-guidelines/media/0303-079-previewtabfocused.png "0303-079_PreviewTabFocused")<br /><br /> **Guia de visualização focada**|Segundo plano|`Environment.FileTabProvisionalSelectedActive`|  
|![Guia de visualização focada](../extensibility/ux-guidelines/media/0303-079-previewtabfocused.png "0303-079_PreviewTabFocused")<br /><br /> **Guia de visualização focada**|Primeiro plano (texto)|`Environment.FileTabProvisionalSelectedActiveForeground`|  
|![Guia de visualização focada](../extensibility/ux-guidelines/media/0303-079-previewtabfocused.png "0303-079_PreviewTabFocused")<br /><br /> **Guia de visualização focada**|Borda|`Environment.FileTabProvisionalSelectedActiveBorder`<br /><br /> Defina para a mesma cor que o plano de fundo.|  
|![Guia de visualização focada](../extensibility/ux-guidelines/media/0303-079-previewtabfocused.png "0303-079_PreviewTabFocused")<br /><br /> **Guia de visualização focada**|Borda do documento|`Environment.FileTabProvisionalSelectedActiveBorder`|  
  
 **Guia de visualização selecionada: desfocada**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Guia de visualização desfocada](../extensibility/ux-guidelines/media/0303-080-previewtabunfocused.png "0303-080_PreviewTabUnfocused")<br /><br /> **Guia de visualização não focalizada**|Segundo plano|`Environment.FileTabProvisionalSelectedInactive`|  
|![Guia de visualização desfocada](../extensibility/ux-guidelines/media/0303-080-previewtabunfocused.png "0303-080_PreviewTabUnfocused")<br /><br /> **Guia de visualização não focalizada**|Primeiro plano (texto)|`Environment.FileTabProvisionalSelectedInactiveForeground`|  
|![Guia de visualização desfocada](../extensibility/ux-guidelines/media/0303-080-previewtabunfocused.png "0303-080_PreviewTabUnfocused")<br /><br /> **Guia de visualização não focalizada**|Borda|`Environment.FileTabProvisionalSelectedInactiveBorder`|  
|![Guia de visualização desfocada](../extensibility/ux-guidelines/media/0303-080-previewtabunfocused.png "0303-080_PreviewTabUnfocused")<br /><br /> **Guia de visualização não focalizada**|Borda do documento|`Environment.FileTabProvisionalSelectedInactiveBorder`|  
  
 **Guia de visualização em segundo plano: padrão**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Guia de plano de fundo da visualização](../extensibility/ux-guidelines/media/0303-081-previewbackgroundtab.png "0303-081_PreviewBackgroundTab")<br /><br /> **Guia de plano de fundo da guia Visualizar**|Segundo plano|`Environment.FileTabProvisionalInactive`|  
|![Guia de plano de fundo da visualização](../extensibility/ux-guidelines/media/0303-081-previewbackgroundtab.png "0303-081_PreviewBackgroundTab")<br /><br /> **Guia de plano de fundo da guia Visualizar**|Primeiro plano (texto)|`Environment.FileTabProvisionalInactiveForeground`|  
|![Guia de plano de fundo da visualização](../extensibility/ux-guidelines/media/0303-081-previewbackgroundtab.png "0303-081_PreviewBackgroundTab")<br /><br /> **Guia de plano de fundo da guia Visualizar**|Borda|`Environment.FileTabProvisionalInactiveBorder`<br /><br /> Defina para a mesma cor que o plano de fundo.|  
  
 **Guia de visualização em segundo plano: focalizar**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Visualizar guia de segundo plano ao focalizar](../extensibility/ux-guidelines/media/0303-082-previewbackgroundtabhover.png "0303-082_PreviewBackgroundTabHover")<br /><br /> **Guia de plano de fundo da guia Visualizar ao focalizar**|Segundo plano|`Environment.FileTabProvisionalHover`|  
|![Visualizar guia de segundo plano ao focalizar](../extensibility/ux-guidelines/media/0303-082-previewbackgroundtabhover.png "0303-082_PreviewBackgroundTabHover")<br /><br /> **Guia de plano de fundo da guia Visualizar ao focalizar**|Primeiro plano (texto)|`Environment.FileTabProvisionalHoverForeground`|  
|![Visualizar guia de segundo plano ao focalizar](../extensibility/ux-guidelines/media/0303-082-previewbackgroundtabhover.png "0303-082_PreviewBackgroundTabHover")<br /><br /> **Guia de plano de fundo da guia Visualizar ao focalizar**|Borda|`Environment.FileTabProvisionalHoverBorder`<br /><br /> Defina para a mesma cor que o plano de fundo.|  
  
##### <a name="document-overflow-button"></a>Botão de estouro de documento  
 O botão de estouro de documento estará presente se houver um ou mais documentos abertos, independentemente de haver espaço vertical na configuração atual para ajustar todas as guias do documento. O menu suspenso de estouro de documento, que é controlado pelas cores **CommandBarMenu** (consulte [menus](../misc/shared-colors.md#BKMK_CommandMenus)), exibe uma lista de todos os documentos abertos, visíveis e ocultos, e as alterações de glifo de estouro, dependendo se todos os documentos abertos são exibidos no canal de guia.  
  
 ![Redline de estouro](../extensibility/ux-guidelines/media/0303-083-overflowredline.png "0303-083_OverflowRedline")  
  
Usar...  
ao criar um botão de estouro de documento personalizado.  

Não use...  
- para a interface do usuário que não é semelhante a um botão de estouro.  

- para botões de estouro da barra de comandos.  
  
  **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Contra](../extensibility/ux-guidelines/media/0303-084-overflow.png "0303-084_Overflow")<br /><br /> **Botão de estouro de documento**|Segundo plano|`Environment.DocWellOverflowButtonBackground`|  
|![Contra](../extensibility/ux-guidelines/media/0303-084-overflow.png "0303-084_Overflow")<br /><br /> **Botão de estouro de documento**|Primeiro plano (glifo)|`Environment.DocWellOverflowButtonGlyph`|  
|![Contra](../extensibility/ux-guidelines/media/0303-084-overflow.png "0303-084_Overflow")<br /><br /> **Botão de estouro de documento**|Borda|N/D|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Estouro no foco](../extensibility/ux-guidelines/media/0303-085-overflowhover.png "0303-085_OverflowHover")<br /><br /> **Botão de estouro de documento ao focalizar**|Segundo plano|`Environment.DocWellOverflowButtonMouseOverBackground`|  
|![Estouro no foco](../extensibility/ux-guidelines/media/0303-085-overflowhover.png "0303-085_OverflowHover")<br /><br /> **Botão de estouro de documento ao focalizar**|Primeiro plano (glifo)|`Environment.DocWellOverflowButtonMouseOverGlyph`|  
|![Estouro no foco](../extensibility/ux-guidelines/media/0303-085-overflowhover.png "0303-085_OverflowHover")<br /><br /> **Botão de estouro de documento ao focalizar**|Borda|`Environment.DocWellOverflowButtonMouseOverBorder`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Estouro pressionado](../extensibility/ux-guidelines/media/0303-086-overflowpressed.png "0303-086_OverflowPressed")<br /><br /> **Botão de estouro de documento pressionado**|Segundo plano|`Environment.DocWellOverflowButtonMouseDownBackground`|  
|![Estouro pressionado](../extensibility/ux-guidelines/media/0303-086-overflowpressed.png "0303-086_OverflowPressed")<br /><br /> **Botão de estouro de documento pressionado**|Primeiro plano (glifo)|`Environment.DocWellOverflowButtonMouseDownGlyph`|  
|![Estouro pressionado](../extensibility/ux-guidelines/media/0303-086-overflowpressed.png "0303-086_OverflowPressed")<br /><br /> **Botão de estouro de documento pressionado**|Borda|`Environment.DocWellOverflowButtonMouseDownBorder`|  
  
### <a name="tool-windows"></a>Janelas da ferramenta  
 Não é necessário replicar janelas de ferramentas, pois elas são fornecidas pelo ambiente do Visual Studio. No entanto, você pode decidir que deseja aproveitar as cores usadas nas janelas de ferramentas para que sua interface do usuário sempre pareça consistente com essa parte do ambiente do Visual Studio.  
  
 ![Janela de ferramentas Redline](../extensibility/ux-guidelines/media/0303-087-toolwindowredline.png "0303-087_ToolWindowRedline")  
  
 Usar...  
 em qualquer lugar, você está criando a interface do usuário que deseja corresponder às janelas de ferramentas.  
  
 Não use...  
 para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema.  
  
#### <a name="tool-window-frame"></a>Quadro da janela de ferramentas  
 Janelas de ferramentas no Visual Studio são usadas para várias tarefas diferentes e podem existir em um de vários Estados diferentes. Se uma janela de ferramenta estiver aberta, ela poderá ser atribuída a qualquer um dos quatro lados da área do documento. As janelas de ferramentas também podem flutuar fora do IDE, o que permite que elas sejam reposicionadas em qualquer lugar na tela do usuário. Janelas flutuantes sempre ficam na parte superior do IDE. Por fim, as janelas de ferramentas podem ser encaixadas como janelas de documentos e exibidas também como uma guia no documento. Janelas de ferramentas que foram encaixadas como janelas de documentos são coloridas em parte usando nomes de token de janela de documento.  
  
 ![Quadro da janela de ferramentas Redline](../extensibility/ux-guidelines/media/0303-088-toolwindowframeredline.png "0303-088_ToolWindowFrameRedline")  
  
 Usar...  
 em qualquer lugar, você está criando a interface do usuário que deseja corresponder às janelas de ferramentas.  
  
 Não use...  
 para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema.  
  
 **Encaixado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Janela de ferramentas encaixada](../extensibility/ux-guidelines/media/0303-089-toolwindowdocked.png "0303-089_ToolWindowDocked")|Segundo plano|`Environment.ToolWindowBackground`|  
|![Janela de ferramentas encaixada](../extensibility/ux-guidelines/media/0303-089-toolwindowdocked.png "0303-089_ToolWindowDocked")|Borda|`Environment.ToolWindowBorder`|  
  
 **Flutuante: focado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Janela de ferramentas focada](../extensibility/ux-guidelines/media/0303-090-toolwindowfocused.png "0303-090_ToolWindowFocused")|Segundo plano|`Environment.ToolWindowBackground`|  
|![Janela de ferramentas focada](../extensibility/ux-guidelines/media/0303-090-toolwindowfocused.png "0303-090_ToolWindowFocused")|Borda|`Environment.MainWindowActiveDefaultBorder`|  
  
 **Flutuante: não focalizado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Janela de ferramentas desfocada](../extensibility/ux-guidelines/media/0303-091-toolwindowunfocused.png "0303-091_ToolWindowUnfocused")|Segundo plano|`Environment.ToolWindowBackground`|  
|![Janela de ferramentas desfocada](../extensibility/ux-guidelines/media/0303-091-toolwindowunfocused.png "0303-091_ToolWindowUnfocused")|Borda|`Environment.MainWindowInactiveBorder`|  
  
#### <a name="tool-window-title-bar"></a>Barra de título da janela de ferramentas  
 A borda da barra de título não é uma borda verdadeira, mas uma linha espessa na parte superior da barra de título. Ele não tem um nome de token para seu estado sem foco.  
  
 ![Barra de título da janela de ferramentas Redline](../extensibility/ux-guidelines/media/0303-092-toolwindowtitlebarredline.png "0303-092_ToolWindowTitleBarRedline")  
  
 Usar...  
 em qualquer lugar, você está criando a interface do usuário que deseja corresponder às janelas de ferramentas.  
  
 Não use...  
 para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema.  
  
 **Focused**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Barra de título focada](../extensibility/ux-guidelines/media/0303-093-titlebarfocused.png "0303-093_TitleBarFocused")<br /><br /> **Barra de título focalizada**|Segundo plano|`Environment.TitleBarActiveGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Barra de título focada](../extensibility/ux-guidelines/media/0303-093-titlebarfocused.png "0303-093_TitleBarFocused")<br /><br /> **Barra de título focalizada**|Primeiro plano (texto)|`Environment.TitleBarActiveText`|  
|![Barra de título focada](../extensibility/ux-guidelines/media/0303-093-titlebarfocused.png "0303-093_TitleBarFocused")<br /><br /> **Barra de título focalizada**|Borda|`Environment.TitleBarActiveBorder`<br /><br /> Defina para a mesma cor que o plano de fundo.|  
|![Barra de título focada](../extensibility/ux-guidelines/media/0303-093-titlebarfocused.png "0303-093_TitleBarFocused")<br /><br /> **Barra de título focalizada**|Identificador de arrastar|`Environment.TitleBarDragHandleActive`|  
  
 **Sem foco**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Barra de título desfocada](../extensibility/ux-guidelines/media/0303-094-titlebarunfocused.png "0303-094_TitleBarUnfocused")<br /><br /> **Barra de título sem foco**|Segundo plano|`Environment.TitleBarInactiveGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Barra de título desfocada](../extensibility/ux-guidelines/media/0303-094-titlebarunfocused.png "0303-094_TitleBarUnfocused")<br /><br /> **Barra de título sem foco**|Primeiro plano (texto)|`Environment.TitleBarInactiveText`|  
|![Barra de título desfocada](../extensibility/ux-guidelines/media/0303-094-titlebarunfocused.png "0303-094_TitleBarUnfocused")<br /><br /> **Barra de título sem foco**|Borda|N/D|  
|![Barra de título desfocada](../extensibility/ux-guidelines/media/0303-094-titlebarunfocused.png "0303-094_TitleBarUnfocused")<br /><br /> **Barra de título sem foco**|Identificador de arrastar|`Environment.TitleBarDragHandle`|  
  
##### <a name="title-bar-buttons"></a>Botões da barra de título  
 ![Botão da barra de título Redline](../extensibility/ux-guidelines/media/0303-095-titlebarbuttonredline.png "0303-095_TitleBarButtonRedline")  
  
 Usar...  
 para botões que aparecem na interface do usuário que usa tokens de cor das barras de título da janela de ferramentas.  
  
Não use...  
- para botões que aparecem em outros locais.  

- em qualquer combinação de plano de fundo/primeiro plano diferente de especificada.  
  
  **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Foco no botão da barra de título](../extensibility/ux-guidelines/media/0303-096-titlebarbuttonfocused.png "0303-096_TitleBarButtonFocused")<br /><br /> **Focused**|Segundo plano|N/D|  
|![Foco no botão da barra de título](../extensibility/ux-guidelines/media/0303-096-titlebarbuttonfocused.png "0303-096_TitleBarButtonFocused")<br /><br /> **Focused**|Primeiro plano (glifo)|`Environment.ToolWindowButtonActiveGlyph`|  
|![Foco no botão da barra de título](../extensibility/ux-guidelines/media/0303-096-titlebarbuttonfocused.png "0303-096_TitleBarButtonFocused")<br /><br /> **Focused**|Borda|N/D|  
|![Botão da barra de título sem foco](../extensibility/ux-guidelines/media/0303-097-titlebarbuttonunfocused.png "0303-097_TitleBarButtonUnfocused")<br /><br /> **Sem foco**|Segundo plano|N/D|  
|![Botão da barra de título sem foco](../extensibility/ux-guidelines/media/0303-097-titlebarbuttonunfocused.png "0303-097_TitleBarButtonUnfocused")<br /><br /> **Sem foco**|Primeiro plano (glifo)|`Environment.ToolWindowButtonInactiveGlyph`|  
|![Botão da barra de título sem foco](../extensibility/ux-guidelines/media/0303-097-titlebarbuttonunfocused.png "0303-097_TitleBarButtonUnfocused")<br /><br /> **Sem foco**|Borda|N/D|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Botão da barra de título focado no foco](../extensibility/ux-guidelines/media/0303-098-titlebarbuttonfocusedhover.png "0303-098_TitleBarButtonFocusedHover")<br /><br /> **Focused**|Segundo plano|`Environment.ToolWindowButtonHoverActive`|  
|![Botão da barra de título focado no foco](../extensibility/ux-guidelines/media/0303-098-titlebarbuttonfocusedhover.png "0303-098_TitleBarButtonFocusedHover")<br /><br /> **Focused**|Primeiro plano (glifo)|`Environment.ToolWindowButtonHoverActiveGlyph`|  
|![Botão da barra de título focado no foco](../extensibility/ux-guidelines/media/0303-098-titlebarbuttonfocusedhover.png "0303-098_TitleBarButtonFocusedHover")<br /><br /> **Focused**|Borda|`Environment.ToolWindowButtonHoverActiveBorder`|  
|![Botão da barra de título sem foco ao focalizar](../extensibility/ux-guidelines/media/0303-099-titlebarbuttonunfocusedhover.png "0303-099_TitleBarButtonUnfocusedHover")<br /><br /> **Sem foco**|Segundo plano|`Environment.ToolWindowButtonHoverInactive`|  
|![Botão da barra de título sem foco ao focalizar](../extensibility/ux-guidelines/media/0303-099-titlebarbuttonunfocusedhover.png "0303-099_TitleBarButtonUnfocusedHover")<br /><br /> **Sem foco**|Primeiro plano (glifo)|`Environment.ToolWindowButtonHoverInactiveGlyph`|  
|![Botão da barra de título sem foco ao focalizar](../extensibility/ux-guidelines/media/0303-099-titlebarbuttonunfocusedhover.png "0303-099_TitleBarButtonUnfocusedHover")<br /><br /> **Sem foco**|Borda|`Environment.ToolWindowButtonHoverInactiveBorder`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Botão da barra de título focalizado e pressionado](../extensibility/ux-guidelines/media/0303-100-titlebarbuttonfocusedpressed.png "0303-100_TitleBarButtonFocusedPressed")<br /><br /> **Focused**|Segundo plano|`Environment.ToolWindowButtonDown`|  
|![Botão da barra de título focalizado e pressionado](../extensibility/ux-guidelines/media/0303-100-titlebarbuttonfocusedpressed.png "0303-100_TitleBarButtonFocusedPressed")<br /><br /> **Focused**|Primeiro plano (glifo)|`Environment.ToolWindowButtonDownActiveGlyph`|  
|![Botão da barra de título focalizado e pressionado](../extensibility/ux-guidelines/media/0303-100-titlebarbuttonfocusedpressed.png "0303-100_TitleBarButtonFocusedPressed")<br /><br /> **Focused**|Borda|`Environment.ToolWindowButtonDownBorder`|  
|![Botão da barra de título sem foco e pressionado](../extensibility/ux-guidelines/media/0303-101-titlebarbuttonunfocusedpressed.png "0303-101_TitleBarButtonUnfocusedPressed")<br /><br /> **Sem foco**|Segundo plano|`Environment.ToolWindowButtonDown`|  
|![Botão da barra de título sem foco e pressionado](../extensibility/ux-guidelines/media/0303-101-titlebarbuttonunfocusedpressed.png "0303-101_TitleBarButtonUnfocusedPressed")<br /><br /> **Sem foco**|Primeiro plano (glifo)|`Environment.ToolWindowButtonDownInactiveGlyph`|  
|![Botão da barra de título sem foco e pressionado](../extensibility/ux-guidelines/media/0303-101-titlebarbuttonunfocusedpressed.png "0303-101_TitleBarButtonUnfocusedPressed")<br /><br /> **Sem foco**|Borda|`Environment.ToolWindowButtonDownBorder`|  
  
#### <a name="tool-window-tabs"></a>Guias da janela de ferramentas  
 ![Guia da janela de ferramentas Redline](../extensibility/ux-guidelines/media/0303-102-toolwindowtabredline.png "0303-102_ToolWindowTabRedline")  
  
 Usar...  
 em qualquer lugar, você está criando a interface do usuário que deseja corresponder às janelas de ferramentas.  
  
 Não use...  
 para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema.  
  
 **Guia selecionada**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Guia da janela da ferramenta focada](../extensibility/ux-guidelines/media/0303-103-toolwindowtabfocused.png "0303-103_ToolWindowTabFocused")<br /><br /> **Guia da janela de ferramentas focalizada selecionada**|Segundo plano|`Environment.ToolWindowTabSelectedTab`|  
|![Guia da janela da ferramenta focada](../extensibility/ux-guidelines/media/0303-103-toolwindowtabfocused.png "0303-103_ToolWindowTabFocused")<br /><br /> **Guia da janela de ferramentas focalizada selecionada**|Primeiro plano (texto)|`Environment.ToolWindowTabSelectedActiveText`|  
|![Guia da janela da ferramenta focada](../extensibility/ux-guidelines/media/0303-103-toolwindowtabfocused.png "0303-103_ToolWindowTabFocused")<br /><br /> **Guia da janela de ferramentas focalizada selecionada**|Borda|`Environment.ToolWindowTabSelectedBorder`<br /><br /> Defina para a mesma cor que o plano de fundo.|  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Guia da janela de ferramentas desfocada](../extensibility/ux-guidelines/media/0303-104-toolwindowtabunfocused.png "0303-104_ToolWindowTabUnfocused")<br /><br /> **Selecionada, guia de janela de ferramentas não focalizada**|Segundo plano|`Environment.ToolWindowTabSelectedTab`|  
|![Guia da janela de ferramentas desfocada](../extensibility/ux-guidelines/media/0303-104-toolwindowtabunfocused.png "0303-104_ToolWindowTabUnfocused")<br /><br /> **Selecionada, guia de janela de ferramentas não focalizada**|Primeiro plano (texto)|`Environment.ToolWindowTabSelectedText`|  
|![Guia da janela de ferramentas desfocada](../extensibility/ux-guidelines/media/0303-104-toolwindowtabunfocused.png "0303-104_ToolWindowTabUnfocused")<br /><br /> **Selecionada, guia de janela de ferramentas não focalizada**|Borda|`Environment.ToolWindowTabSelectedBorder`<br /><br /> Defina para a mesma cor que o plano de fundo.|  
  
 **Guia de segundo plano**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Guia de plano de fundo da janela de ferramentas](../extensibility/ux-guidelines/media/0303-105-toolwindowbackgroundtab.png "0303-105_ToolWindowBackgroundTab")<br /><br /> **Guia da janela da ferramenta de segundo plano**|Segundo plano|`Environment.ToolWindowTabGradientBegin`<br /><br /> As interrupções de gradiente são definidas com o mesmo valor de cor em Visual Studio 2013.<br /><br /> `Environment.ToolWindowTabGradientEnd`<br /><br /> As interrupções de gradiente são definidas com o mesmo valor de cor em Visual Studio 2013.|  
|![Guia de plano de fundo da janela de ferramentas](../extensibility/ux-guidelines/media/0303-105-toolwindowbackgroundtab.png "0303-105_ToolWindowBackgroundTab")<br /><br /> **Guia da janela da ferramenta de segundo plano**|Primeiro plano (texto)|`Environment.ToolWindowTabText`|  
|![Guia de plano de fundo da janela de ferramentas](../extensibility/ux-guidelines/media/0303-105-toolwindowbackgroundtab.png "0303-105_ToolWindowBackgroundTab")<br /><br /> **Guia da janela da ferramenta de segundo plano**|Borda|`Environment.ToolWindowTabBorder`|  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Guia de plano de fundo da janela de ferramentas ao focalizar](../extensibility/ux-guidelines/media/0303-106-toolwindowbackgroundtabhover.png "0303-106_ToolWindowBackgroundTabHover")<br /><br /> **Guia da janela da ferramenta de segundo plano ao focalizar**|Segundo plano|`Environment.ToolWindowTabMouseOverBackgroundBegin`<br /><br /> As interrupções de gradiente são definidas com o mesmo valor de cor em Visual Studio 2013.<br /><br /> `Environment.ToolWindowTabMouseOverBackgroundEnd`<br /><br /> As interrupções de gradiente são definidas com o mesmo valor de cor em Visual Studio 2013.|  
|![Guia de plano de fundo da janela de ferramentas ao focalizar](../extensibility/ux-guidelines/media/0303-106-toolwindowbackgroundtabhover.png "0303-106_ToolWindowBackgroundTabHover")<br /><br /> **Guia da janela da ferramenta de segundo plano ao focalizar**|Primeiro plano (texto)|`Environment.ToolWindowTabMouseOverText`|  
|![Guia de plano de fundo da janela de ferramentas ao focalizar](../extensibility/ux-guidelines/media/0303-106-toolwindowbackgroundtabhover.png "0303-106_ToolWindowBackgroundTabHover")<br /><br /> **Guia da janela da ferramenta de segundo plano ao focalizar**|Borda|`Environment.ToolWindowTabMouseOverBorder`<br /><br /> Defina para a mesma cor que o plano de fundo.|  
  
#### <a name="auto-hide-tabs"></a>Ocultar guias automaticamente  
 ![&#45;automaticamente ocultar Redline](../extensibility/ux-guidelines/media/0303-107-autohideredline.png "0303-107_AutoHideRedline")  
  
 Usar...  
 em qualquer lugar, você está criando a interface do usuário que deseja corresponder às guias da janela de ferramentas ocultas automaticamente.  
  
 Não use...  
 para qualquer interface do usuário que você não deseja alterar automaticamente se o Shell tiver uma atualização de tema.  
  
 **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Guia ocultar&#45;automaticamente](../extensibility/ux-guidelines/media/0303-108-autohidetab.png "0303-108_AutoHideTab")<br /><br /> **Guia ocultar automaticamente padrão**|Segundo plano|`Environment.AutoHideTabBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Guia ocultar&#45;automaticamente](../extensibility/ux-guidelines/media/0303-108-autohidetab.png "0303-108_AutoHideTab")<br /><br /> **Guia ocultar automaticamente padrão**|Primeiro plano (texto)|`Environment.AutoHideTabText`|  
|![Guia ocultar&#45;automaticamente](../extensibility/ux-guidelines/media/0303-108-autohidetab.png "0303-108_AutoHideTab")<br /><br /> **Guia ocultar automaticamente padrão**|Borda|`Environment.AutoHideTabBorder`|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![&#45;automaticamente a guia ocultar ao focalizar](../extensibility/ux-guidelines/media/0303-109-autohidetabhover.png "0303-109_AutoHideTabHover")<br /><br /> **Ocultar guia automaticamente ao focalizar**|Segundo plano|`Environment.AutoHideTabMouseOverBackgroundBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![&#45;automaticamente a guia ocultar ao focalizar](../extensibility/ux-guidelines/media/0303-109-autohidetabhover.png "0303-109_AutoHideTabHover")<br /><br /> **Ocultar guia automaticamente ao focalizar**|Primeiro plano (texto)|`Environment.AutoHideTabMouseOverText`|  
|![&#45;automaticamente a guia ocultar ao focalizar](../extensibility/ux-guidelines/media/0303-109-autohidetabhover.png "0303-109_AutoHideTabHover")<br /><br /> **Ocultar guia automaticamente ao focalizar**|Borda|`Environment.AutoHideTabMouseOverBorder`|  
  
### <a name="common-shared-controls"></a>Controles compartilhados comuns  
 Ao usar uma barra de comandos padrão do Visual Studio em seu recurso, você terá acesso aos controles de shell com estilo e não deverá modelar esses controles comuns. No entanto, se você precisar criar uma barra de comandos personalizada, talvez seja necessário também criar controles personalizados. Nesse caso, certifique-se de usar os nomes de token corretos para cada um dos controles a seguir para que sua interface do usuário seja consistente com o restante do Visual Studio.  
  
#### <a name="search-box"></a>Caixa de pesquisa  
 Sempre que possível, use o controle de pesquisa comum fornecido pelo ambiente do Visual Studio. As cores da caixa de pesquisa são encontradas na categoria "SearchControl" no arquivo **ShellColors. pkgdef** , que contém nomes de token para o campo de entrada, botão de ação, botão suspenso e menu suspenso.  
  
 Uma caixa de pesquisa pode ser um dos vários Estados, algumas das quais são mutuamente exclusivas:  
  
- "Focalizado" ou "sem foco" refere-se a se o cursor está ou não na caixa de texto.  
  
- "Ativo" ou "inativo" refere-se a se o usuário tem entrada em uma consulta de pesquisa na caixa de texto.  
  
- "Hover" significa que o usuário fez o mouse sobre a caixa de pesquisa com o mouse (esse estado substitui todos os outros Estados).  
  
- "Disabled" significa que a funcionalidade de pesquisa está desativada para o contexto atual.  
  
  ![Caixa de pesquisa Redline](../extensibility/ux-guidelines/media/0303-110-searchboxredline.png "0303-110_SearchBoxRedline")  
  
  Usar...  
  Quando você está criando uma caixa de pesquisa personalizada.  
  
  Não use...  
  - para qualquer coisa que não seja uma caixa de pesquisa.  
  
- para qualquer coisa que você não queira sempre corresponder à interface do usuário da caixa de pesquisa.  
  
  **Focused**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Foco no campo de entrada de pesquisa](../extensibility/ux-guidelines/media/0303-111-searchinputfieldfocused.png "0303-111_SearchInputFieldFocused")<br /><br /> **Campo de entrada**|Segundo plano|`SearchControl.FocusedBackground`|  
|![Foco no campo de entrada de pesquisa](../extensibility/ux-guidelines/media/0303-111-searchinputfieldfocused.png "0303-111_SearchInputFieldFocused")<br /><br /> **Campo de entrada**|Primeiro plano (texto)|`SearchControl.FocusedBackground`|  
|![Foco no campo de entrada de pesquisa](../extensibility/ux-guidelines/media/0303-111-searchinputfieldfocused.png "0303-111_SearchInputFieldFocused")<br /><br /> **Campo de entrada**|Borda|`SearchControl.FocusedBorder`|  
|![Foco no campo de entrada de pesquisa](../extensibility/ux-guidelines/media/0303-111-searchinputfieldfocused.png "0303-111_SearchInputFieldFocused")<br /><br /> **Campo de entrada**|Separador|`SearchControl.FocusedDropDownSeparator`|  
|![Foco no botão de ação de pesquisa](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br /><br /> **Botão de ação**|Segundo plano|Nenhum|  
|![Foco no botão de ação de pesquisa](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br /><br /> **Botão de ação**|Primeiro plano (glifo de pesquisa)|`SearchControl.SearchGlyph`|  
|![Foco no botão de ação de pesquisa](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br /><br /> **Botão de ação**|Primeiro plano (glifo de parada)|`SearchControl.StopGlyph`|  
|![Foco no botão de ação de pesquisa](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br /><br /> **Botão de ação**|Primeiro plano (limpar glifo)|`SearchControl.ClearGlyph`|  
|![Foco no botão de ação de pesquisa](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br /><br /> **Botão de ação**|Borda|N/D|  
|![Botão para soltar&#45;de pesquisa com foco](../extensibility/ux-guidelines/media/0303-113-searchdropdownbuttonfocused.png "0303-113_SearchDropdownButtonFocused")<br /><br /> **Botão suspenso**|Segundo plano|`SearchControl.FocusedDropDownButton`|  
|![Botão para soltar&#45;de pesquisa com foco](../extensibility/ux-guidelines/media/0303-113-searchdropdownbuttonfocused.png "0303-113_SearchDropdownButtonFocused")<br /><br /> **Botão suspenso**|Primeiro plano (glifo)|`SearchControl.FocusedDropDownButtonGlyph`|  
|![Botão para soltar&#45;de pesquisa com foco](../extensibility/ux-guidelines/media/0303-113-searchdropdownbuttonfocused.png "0303-113_SearchDropdownButtonFocused")<br /><br /> **Botão suspenso**|Borda|`SearchControl.FocusedDropDownButtonBorder`|  
  
 **Sem foco**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Campo de entrada de pesquisa não focalizado](../extensibility/ux-guidelines/media/0303-114-searchinputfieldunfocused.png "0303-114_SearchInputFieldUnfocused")<br /><br /> **Campo de entrada ativo**|Segundo plano|`SearchControl.SearchActiveBackground`|  
|![Campo de entrada de pesquisa não focalizado](../extensibility/ux-guidelines/media/0303-114-searchinputfieldunfocused.png "0303-114_SearchInputFieldUnfocused")<br /><br /> **Campo de entrada ativo**|Primeiro plano (texto)|`SearchControl.SearchActiveBackground`|  
|![Campo de entrada de pesquisa não focalizado](../extensibility/ux-guidelines/media/0303-114-searchinputfieldunfocused.png "0303-114_SearchInputFieldUnfocused")<br /><br /> **Campo de entrada ativo**|Borda|`SearchControl.UnfocusedBorder`|  
|![Campo de entrada de pesquisa não focalizado](../extensibility/ux-guidelines/media/0303-114-searchinputfieldunfocused.png "0303-114_SearchInputFieldUnfocused")<br /><br /> **Campo de entrada ativo**|Separador|`SearchControl.DropDownSeparator`|  
|![Campo de entrada de pesquisa não focalizado e inativo](../extensibility/ux-guidelines/media/0303-114-1-searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")<br /><br /> **Campo de entrada inativo**|Segundo plano|`SearchControl.Unfocused`|  
|![Campo de entrada de pesquisa não focalizado e inativo](../extensibility/ux-guidelines/media/0303-114-1-searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")<br /><br /> **Campo de entrada inativo**|Primeiro plano (texto)|`SearchControl.Unfocused`|  
|![Campo de entrada de pesquisa não focalizado e inativo](../extensibility/ux-guidelines/media/0303-114-1-searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")<br /><br /> **Campo de entrada inativo**|Borda|`SearchControl.UnfocusedBorder`|  
|![Campo de entrada de pesquisa não focalizado e inativo](../extensibility/ux-guidelines/media/0303-114-1-searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")<br /><br /> **Campo de entrada inativo**|Separador|`SearchControl.DropDownSeparator`|  
|![Botão de ação de pesquisa não focalizado](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br /><br /> **Botão de ação**|Segundo plano|N/D|  
|![Botão de ação de pesquisa não focalizado](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br /><br /> **Botão de ação**|Primeiro plano (glifo de pesquisa)|`SearchControl.SearchGlyph`|  
|![Botão de ação de pesquisa não focalizado](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br /><br /> **Botão de ação**|Primeiro plano (glifo de parada)|`SearchControl.StopGlyph`|  
|![Botão de ação de pesquisa não focalizado](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br /><br /> **Botão de ação**|Primeiro plano (limpar glifo)|`SearchControl.ClearGlyph`|  
|![Botão de ação de pesquisa não focalizado](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br /><br /> **Botão de ação**|Borda|N/D|  
|![Botão para soltar&#45;de pesquisa desfocado](../extensibility/ux-guidelines/media/0303-116-searchdropdownbuttonunfocused.png "0303-116_SearchDropdownButtonUnfocused")<br /><br /> **Botão suspenso**|Segundo plano|`SearchControl.UnfocusedDropDownButton`|  
|![Botão para soltar&#45;de pesquisa desfocado](../extensibility/ux-guidelines/media/0303-116-searchdropdownbuttonunfocused.png "0303-116_SearchDropdownButtonUnfocused")<br /><br /> **Botão suspenso**|Primeiro plano (glifo)|`SearchControl.UnfocusedDropDownButtonGlyph`|  
|![Botão para soltar&#45;de pesquisa desfocado](../extensibility/ux-guidelines/media/0303-116-searchdropdownbuttonunfocused.png "0303-116_SearchDropdownButtonUnfocused")<br /><br /> **Botão suspenso**|Borda|`SearchControl.UnfocusedDropDownButtonBorder`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Botão de ação de pesquisa pressionado](../extensibility/ux-guidelines/media/0303-116-1-searchactionbuttonpressed.png "0303-116-1_SearchActionButtonPressed")<br /><br /> **Botão de ação**|Segundo plano|`SearchControl.ActionButtonMouseDown`|  
|![Botão de ação de pesquisa pressionado](../extensibility/ux-guidelines/media/0303-116-1-searchactionbuttonpressed.png "0303-116-1_SearchActionButtonPressed")<br /><br /> **Botão de ação**|Primeiro plano (glifo)|`SearchControl.ActionButtonMouseDownGlyph`|  
|![Botão de ação de pesquisa pressionado](../extensibility/ux-guidelines/media/0303-116-1-searchactionbuttonpressed.png "0303-116-1_SearchActionButtonPressed")<br /><br /> **Botão de ação**|Borda|`SearchControl.ActionButtonMouseDownBorder`|  
|![Botão de pesquisa soltar&#45;pressionado](../extensibility/ux-guidelines/media/0303-116-2-searchdropdownbuttonpressed.png "0303-116-2_SearchDropdownButtonPressed")<br /><br /> **Botão suspenso**|Segundo plano|`SearchControl.MouseDownDropDownButton`|  
|![Botão de pesquisa soltar&#45;pressionado](../extensibility/ux-guidelines/media/0303-116-2-searchdropdownbuttonpressed.png "0303-116-2_SearchDropdownButtonPressed")<br /><br /> **Botão suspenso**|Primeiro plano (glifo)|`SearchControl.MouseDownDropDownButtonGlyph`|  
|![Botão de pesquisa soltar&#45;pressionado](../extensibility/ux-guidelines/media/0303-116-2-searchdropdownbuttonpressed.png "0303-116-2_SearchDropdownButtonPressed")<br /><br /> **Botão suspenso**|Borda|`SearchControl.MouseDownDropDownButtonBorder`|  
  
 **Realçado (somente texto)**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Realce do campo de entrada de pesquisa](../extensibility/ux-guidelines/media/0303-120-searchinputfieldhighlight.png "0303-120_SearchInputFieldHighlight")<br /><br /> **Campo de entrada com texto realçado**|Segundo plano|`SearchControl.Selection`|  
|![Realce do campo de entrada de pesquisa](../extensibility/ux-guidelines/media/0303-120-searchinputfieldhighlight.png "0303-120_SearchInputFieldHighlight")<br /><br /> **Campo de entrada com texto realçado**|Primeiro plano (texto)|`SearchControl.FocusedBackground`|  
|![Realce do campo de entrada de pesquisa](../extensibility/ux-guidelines/media/0303-120-searchinputfieldhighlight.png "0303-120_SearchInputFieldHighlight")<br /><br /> **Campo de entrada com texto realçado**|Borda|Nenhum|  
|![Realce do campo de entrada de pesquisa](../extensibility/ux-guidelines/media/0303-120-searchinputfieldhighlight.png "0303-120_SearchInputFieldHighlight")<br /><br /> **Campo de entrada com texto realçado**|Separador|`SearchControl.FocusedDropDownSeparator`|  
  
 **Desabilitado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Campo de entrada de pesquisa desabilitado](../extensibility/ux-guidelines/media/0303-121-searchinputfielddisabled.png "0303-121_SearchInputFieldDisabled")<br /><br /> **Campo de entrada**|Segundo plano|`SearchControl.Disabled`|  
|![Campo de entrada de pesquisa desabilitado](../extensibility/ux-guidelines/media/0303-121-searchinputfielddisabled.png "0303-121_SearchInputFieldDisabled")<br /><br /> **Campo de entrada**|Primeiro plano (texto)|`SearchControl.Disabled`|  
|![Campo de entrada de pesquisa desabilitado](../extensibility/ux-guidelines/media/0303-121-searchinputfielddisabled.png "0303-121_SearchInputFieldDisabled")<br /><br /> **Campo de entrada**|Borda|`SearchControl.DisabledBorder`|  
|![Campo de entrada de pesquisa desabilitado](../extensibility/ux-guidelines/media/0303-121-searchinputfielddisabled.png "0303-121_SearchInputFieldDisabled")<br /><br /> **Campo de entrada**|Separador|`SearchControl.DropDownSeparator`|  
|![Botão de ação de pesquisa desabilitado](../extensibility/ux-guidelines/media/0303-122-searchactionbuttondisabled.png "0303-122_SearchActionButtonDisabled")<br /><br /> **Botão de ação**|Segundo plano|Nenhum|  
|![Botão de ação de pesquisa desabilitado](../extensibility/ux-guidelines/media/0303-122-searchactionbuttondisabled.png "0303-122_SearchActionButtonDisabled")<br /><br /> **Botão de ação**|Primeiro plano (glifo)|`SearchControl.ActionButtonDisabledGlyph`|  
|![Botão de ação de pesquisa desabilitado](../extensibility/ux-guidelines/media/0303-122-searchactionbuttondisabled.png "0303-122_SearchActionButtonDisabled")<br /><br /> **Botão de ação**|Borda|Nenhum|  
|![Botão de descartar pesquisa&#45;desabilitado](../extensibility/ux-guidelines/media/0303-123-searchdropdownbuttondisabled.png "0303-123_SearchDropdownButtonDisabled")<br /><br /> **Botão suspenso**|Segundo plano|Nenhum|  
|![Botão de descartar pesquisa&#45;desabilitado](../extensibility/ux-guidelines/media/0303-123-searchdropdownbuttondisabled.png "0303-123_SearchDropdownButtonDisabled")<br /><br /> **Botão suspenso**|Primeiro plano (glifo)|`SearchControl.DisabledDownButtonGlyph`|  
|![Botão de descartar pesquisa&#45;desabilitado](../extensibility/ux-guidelines/media/0303-123-searchdropdownbuttondisabled.png "0303-123_SearchDropdownButtonDisabled")<br /><br /> **Botão suspenso**|Borda|Nenhum|  
  
##### <a name="search-drop-down-lists"></a>Listas suspensas de pesquisa  
 O menu suspenso da caixa de pesquisa tem o potencial de ser um pouco mais complexo do que outros menus suspensos no Visual Studio. As seções "pesquisas sugeridas" e "opções de pesquisa" podem aparecer sozinhas ou juntas no menu e cada uma é colorida separadamente. Uma linha também separa essas duas seções quando elas aparecem juntas e uma borda circunda todo o menu suspenso.  
  
 ![Pesquisar&#45;Redline para baixo](../extensibility/ux-guidelines/media/0303-124-searchdropdownredline.png "0303-124_SearchDropdownRedline")  
  
Usar...  
- Quando você estiver criando uma lista suspensa de pesquisa personalizada.  

- os nomes de token corretos para os componentes de lista corretos.  

Não use...  
- para listas suspensas que aparecem em outros contextos.  

- em qualquer combinação de plano de fundo/primeiro plano diferente de especificada.  
  
  **Padrão (nenhum outro Estado)**  
  
|Elemento|Nome do token: categoria. cor|  
|-------------|--------------------------------|  
|Borda|`SearchControl.PopupBorder`|  
|Separador|`SearchControl.PopupSectionHeaderSeparator`|  
|Shadow|`Environment.DropShadowBackground`|  
  
 **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Pesquisa sugerida](../extensibility/ux-guidelines/media/0303-125-searchsuggested.png "0303-125_SearchSuggested")<br /><br /> **Pesquisas sugeridas**|Segundo plano|`SearchControl.PopupItemsListBackgroundGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Pesquisa sugerida](../extensibility/ux-guidelines/media/0303-125-searchsuggested.png "0303-125_SearchSuggested")<br /><br /> **Pesquisas sugeridas**|Primeiro plano (texto)|`SearchControl.PopupItemText`|  
|![Caixa de seleção Pesquisar](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303-126_SearchCheckbox")<br /><br /> **Opções de pesquisa (caixa de seleção)**|Segundo plano|`SearchControl.PopupSectionBackgroundGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Opções de pesquisa](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303-127_SearchOptions")<br /><br /> **Opções de pesquisa (link)**|Segundo plano|`SearchControl.PopupSectionBackgroundGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Caixa de seleção Pesquisar](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303-126_SearchCheckbox")<br /><br /> **Opções de pesquisa (caixa de seleção)**|Primeiro plano (texto da caixa de seleção)|`SearchControl.PopupCheckboxText`|  
|![Opções de pesquisa](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303-127_SearchOptions")<br /><br /> **Opções de pesquisa (link)**|Primeiro plano (texto da caixa de seleção)|`SearchControl.PopupCheckboxText`|  
|![Caixa de seleção Pesquisar](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303-126_SearchCheckbox")<br /><br /> **Opções de pesquisa (caixa de seleção)**|Primeiro plano (texto do link)|`SearchControl.PopupButtonText`|  
|![Opções de pesquisa](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303-127_SearchOptions")<br /><br /> **Opções de pesquisa (link)**|Primeiro plano (texto do link)|`SearchControl.PopupButtonText`|  
|![Caixa de seleção Pesquisar](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303-126_SearchCheckbox")<br /><br /> **Opções de pesquisa (caixa de seleção)**|Plano de fundo do cabeçalho|`SearchControl.PopupSectionHeaderGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Opções de pesquisa](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303-127_SearchOptions")<br /><br /> **Opções de pesquisa (link)**|Plano de fundo do cabeçalho|`SearchControl.PopupSectionHeaderGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Caixa de seleção Pesquisar](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303-126_SearchCheckbox")<br /><br /> **Opções de pesquisa (caixa de seleção)**|Primeiro plano (texto do cabeçalho)|`SearchControl.PopupSectionHeaderText`|  
|![Opções de pesquisa](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303-127_SearchOptions")<br /><br /> **Opções de pesquisa (link)**|Primeiro plano (texto do cabeçalho)|`SearchControl.PopupSectionHeaderText`|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Pesquisa sugerida ao focalizar](../extensibility/ux-guidelines/media/0303-128-searchsuggestedhover.png "0303-128_SearchSuggestedHover")<br /><br /> **Pesquisas sugeridas**|Segundo plano|`SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Pesquisa sugerida ao focalizar](../extensibility/ux-guidelines/media/0303-128-searchsuggestedhover.png "0303-128_SearchSuggestedHover")<br /><br /> **Pesquisas sugeridas**|Primeiro plano (texto)|`SearchControl.PopupMouseOverItemText`|  
|![Pesquisa sugerida ao focalizar](../extensibility/ux-guidelines/media/0303-128-searchsuggestedhover.png "0303-128_SearchSuggestedHover")<br /><br /> **Pesquisas sugeridas**|Borda|`SearchControl.PopupControlMouseOverBorder`|  
|![Caixa de seleção de pesquisa ao focalizar](../extensibility/ux-guidelines/media/0303-129-searchcheckboxhover.png "0303-129_SearchCheckboxHover")<br /><br /> **Pesquisas sugeridas (caixa de seleção)**|Segundo plano|`SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Opções de pesquisa ao focalizar](../extensibility/ux-guidelines/media/0303-130-searchoptionshover.png "0303-130_SearchOptionsHover")<br /><br /> **Opções de pesquisa**|Segundo plano|`SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Caixa de seleção de pesquisa ao focalizar](../extensibility/ux-guidelines/media/0303-129-searchcheckboxhover.png "0303-129_SearchCheckboxHover")<br /><br /> **Pesquisas sugeridas (caixa de seleção)**|Primeiro plano (texto da caixa de seleção)|`SearchControl.PopupCheckboxMouseDownText`|  
|![Opções de pesquisa ao focalizar](../extensibility/ux-guidelines/media/0303-130-searchoptionshover.png "0303-130_SearchOptionsHover")<br /><br /> **Opções de pesquisa**|Primeiro plano (texto da caixa de seleção)|`SearchControl.PopupCheckboxMouseDownText`|  
|![Caixa de seleção de pesquisa ao focalizar](../extensibility/ux-guidelines/media/0303-129-searchcheckboxhover.png "0303-129_SearchCheckboxHover")<br /><br /> **Pesquisas sugeridas (caixa de seleção)**|Primeiro plano (texto do link)|`SearchControl.PopupButtonMouseDownText`|  
|![Opções de pesquisa ao focalizar](../extensibility/ux-guidelines/media/0303-130-searchoptionshover.png "0303-130_SearchOptionsHover")<br /><br /> **Opções de pesquisa**|Primeiro plano (texto do link)|`SearchControl.PopupButtonMouseDownText`|  
|![Caixa de seleção de pesquisa ao focalizar](../extensibility/ux-guidelines/media/0303-129-searchcheckboxhover.png "0303-129_SearchCheckboxHover")<br /><br /> **Pesquisas sugeridas (caixa de seleção)**|Borda|`SearchControl.PopupControlMouseOverBorder`|  
|![Opções de pesquisa ao focalizar](../extensibility/ux-guidelines/media/0303-130-searchoptionshover.png "0303-130_SearchOptionsHover")<br /><br /> **Opções de pesquisa**|Borda|`SearchControl.PopupControlMouseOverBorder`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Pesquisa sugerida pressionada](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br /><br /> **Pesquisas sugeridas (caixa de seleção)**|Plano de fundo da caixa de seleção|`SearchControl.PopupControlMouseDownBackgroundGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Opções de pesquisa pressionadas](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303-132_SearchOptionsPressed")<br /><br /> **Opções de pesquisa**|Plano de fundo da caixa de seleção|`SearchControl.PopupControlMouseDownBackgroundGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Pesquisa sugerida pressionada](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br /><br /> **Pesquisas sugeridas (caixa de seleção)**|Plano de fundo da caixa de seleção|`SearchControl.PopupControlMouseDownBackgroundGradientEnd`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Opções de pesquisa pressionadas](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303-132_SearchOptionsPressed")<br /><br /> **Opções de pesquisa**|Plano de fundo da caixa de seleção|`SearchControl.PopupControlMouseDownBackgroundGradientEnd`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Pesquisa sugerida pressionada](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br /><br /> **Pesquisas sugeridas (caixa de seleção)**|Primeiro plano (texto da caixa de seleção)|`SearchControl.PopupCheckboxMouseDownText`|  
|![Opções de pesquisa pressionadas](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303-132_SearchOptionsPressed")<br /><br /> **Opções de pesquisa**|Primeiro plano (texto da caixa de seleção)|`SearchControl.PopupCheckboxMouseDownText`|  
|![Pesquisa sugerida pressionada](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br /><br /> **Pesquisas sugeridas (caixa de seleção)**|Vincular plano de fundo|`SearchControl.PopupButtonMouseDownBackgroundGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Opções de pesquisa pressionadas](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303-132_SearchOptionsPressed")<br /><br /> **Opções de pesquisa**|Vincular plano de fundo|`SearchControl.PopupButtonMouseDownBackgroundGradientBegin`<br /><br /> Embora não seja usado em uma interface do usuário com tema moderno, há interrupções de gradiente e valores para esse plano de fundo.|  
|![Pesquisa sugerida pressionada](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br /><br /> **Pesquisas sugeridas (caixa de seleção)**|Primeiro plano (texto do link)|`SearchControl.PopupButtonMouseDownText`|  
|![Opções de pesquisa pressionadas](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303-132_SearchOptionsPressed")<br /><br /> **Opções de pesquisa**|Primeiro plano (texto do link)|`SearchControl.PopupButtonMouseDownText`|  
  
#### <a name="hyperlink"></a>Hyperlink  
 O hiperlink é um controle que não tem um par de primeiro plano/segundo plano. Em todos os casos, use a cor do hiperlink de primeiro plano, que será exibida corretamente em planos de fundo escuros, cinzas e brancos. Se você não usar o token de cor para o controle HyperLink, verá a cor padrão do sistema para "pressionado", que piscará vermelho. Esse é o sinal de que o controle não está usando o token de cor de ambiente correto.  
  
 ![Redline de hiperlink](../extensibility/ux-guidelines/media/0303-133-hyperlinkredline.png "0303-133_HyperlinkRedline")  
  
 Usar...  
 Quando você precisar criar um hiperlink personalizado.  
  
 Não use...  
 para qualquer coisa que não seja um hiperlink.  
  
 **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Hiperlink padrão](../extensibility/ux-guidelines/media/0303-134-hyperlink.png "0303-134_Hyperlink")|Primeiro plano (texto)|`Environment.PanelHyperlink`|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Hiperlink ao focalizar](../extensibility/ux-guidelines/media/0303-135-hyperlinkhover.png "0303-135_HyperlinkHover")|Primeiro plano (texto)|`Environment.PanelHyperlinkHover`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Hiperlink pressionado](../extensibility/ux-guidelines/media/0303-136-hyperlinkpressed.png "0303-136_HyperlinkPressed")|Primeiro plano (texto)|`Environment.PanelHyperlinkPressed`|  
  
 **Desabilitado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Hiperlink desabilitado](../extensibility/ux-guidelines/media/0303-137-hyperlinkdisabled.png "0303-137_HyperlinkDisabled")|Primeiro plano (texto)|`Environment.PanelHyperlinkDisabled`|  
  
#### <a name="infobar"></a>Barra  
 Infobars são usados para fornecer mais informações sobre um determinado contexto e sempre aparecem na parte superior de uma janela de documento ou janela de ferramentas.  
  
 ![Redline da barra de a](../extensibility/ux-guidelines/media/0303-138-infobarredline.png "0303-138_InfobarRedline")  
  
 Usar...  
 ao criar infobars personalizado.  
  
 Não use...  
 para elementos de interface do usuário que não são semelhantes a uma barra de lista.  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Barra](../extensibility/ux-guidelines/media/0303-139-infobar.png "0303-139_Infobar")<br /><br /> **Barra**|Segundo plano|`Environment.InfoBackground`|  
|![Barra](../extensibility/ux-guidelines/media/0303-139-infobar.png "0303-139_Infobar")<br /><br /> **Barra**|Primeiro plano (texto)|`Environment.InfoText`|  
|![Barra](../extensibility/ux-guidelines/media/0303-139-infobar.png "0303-139_Infobar")<br /><br /> **Barra**|Borda|`Environment.ToolWindowBorder`|  
  
#### <a name="scroll-bar"></a>Barra de rolagem  
 As barras de rolagem são estilizadas pelo ambiente do Visual Studio e não precisarão ser configuradas. No entanto, você pode decidir que deseja aproveitar as cores usadas nas barras de rolagem para que sua interface do usuário sempre pareça consistente com essa parte do ambiente do Visual Studio.  
  
 ![Barra de rolagem Redline](../extensibility/ux-guidelines/media/0303-140-scrollbarredline.png "0303-140_ScrollbarRedline")  
  
 Usar...  
 ao criar a interface do usuário que você deseja corresponder às barras de rolagem do Visual Studio.  
  
 Não use...  
 para qualquer coisa que você não queira sempre corresponder à interface do usuário da barra de rolagem.  
  
 **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Barra de rolagem](../extensibility/ux-guidelines/media/0303-141-scrollbar.png "0303-141_Scrollbar")<br /><br /> **Rolagem**|Rolagem|`Environment.ScrollBarBackground`|  
|![Barra de rolagem](../extensibility/ux-guidelines/media/0303-141-scrollbar.png "0303-141_Scrollbar")<br /><br /> **Rolagem**|Primeiro plano (Thumb)|`Environment.ScrollBarThumbBackground`|  
|![Seta da barra de rolagem](../extensibility/ux-guidelines/media/0303-142-scrollbararrow.png "0303-142_ScrollbarArrow")<br /><br /> **Seta de rolagem**|Segundo plano|`Environment.ScrollBarArrowBackground`<br /><br /> Defina para a mesma cor que a barra de rolagem.|  
|![Seta da barra de rolagem](../extensibility/ux-guidelines/media/0303-142-scrollbararrow.png "0303-142_ScrollbarArrow")<br /><br /> **Seta de rolagem**|Primeiro plano (glifo)|`Environment.ScrollBarArrowGlyph`|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Barra de rolagem ao focalizar](../extensibility/ux-guidelines/media/0303-143-scrollbarhover.png "0303-143_ScrollbarHover")<br /><br /> **Rolagem**|Rolagem|`Environment.ScrollBarBackground`|  
|![Barra de rolagem ao focalizar](../extensibility/ux-guidelines/media/0303-143-scrollbarhover.png "0303-143_ScrollbarHover")<br /><br /> **Rolagem**|Primeiro plano (Thumb)|`Environment.ScrollBarThumbMouseOverBackground`|  
|![Seta da barra de rolagem ao focalizar](../extensibility/ux-guidelines/media/0303-144-scrollbararrowhover.png "0303-144_ScrollbarArrowHover")<br /><br /> **Seta de rolagem**|Segundo plano|`Environment.ScrollBarArrowMouseOverBackground`<br /><br /> Defina para a mesma cor que a barra de rolagem.|  
|![Seta da barra de rolagem ao focalizar](../extensibility/ux-guidelines/media/0303-144-scrollbararrowhover.png "0303-144_ScrollbarArrowHover")<br /><br /> **Seta de rolagem**|Primeiro plano (glifo)|`Environment.ScrollBarArrowGlyphMouseOver`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Barra de rolagem pressionada](../extensibility/ux-guidelines/media/0303-145-scrollbarpressed.png "0303-145_ScrollbarPressed")<br /><br /> **Rolagem**|Rolagem|`Environment.ScrollBarBackground`|  
|![Barra de rolagem pressionada](../extensibility/ux-guidelines/media/0303-145-scrollbarpressed.png "0303-145_ScrollbarPressed")<br /><br /> **Rolagem**|Primeiro plano (Thumb)|`Environment.ScrollBarThumbPressedBackground`|  
|![Seta da barra de rolagem pressionada](../extensibility/ux-guidelines/media/0303-146-scrollbararrowpressed.png "0303-146_ScrollbarArrowPressed")<br /><br /> **Seta de rolagem**|Segundo plano|`Environment.ScrollBarArrowPressedBackground`<br /><br /> Defina para a mesma cor que a barra de rolagem.|  
|![Seta da barra de rolagem pressionada](../extensibility/ux-guidelines/media/0303-146-scrollbararrowpressed.png "0303-146_ScrollbarArrowPressed")<br /><br /> **Seta de rolagem**|Primeiro plano (glifo)|`Environment.ScrollBarArrowGlyphPressed`|  
  
#### <a name="tree-view"></a><a name="BKMK_TreeView"></a>Exibição de árvore  
 Várias janelas de ferramentas, incluindo a Gerenciador de Soluções, Gerenciador de Servidores e Modo de Exibição de Classe, implementam um esquema organizacional hierárquico cujas cores são controladas por nomes de cores na categoria de TreeView. Todos os itens em um modo de exibição de árvore têm cores de texto e em segundo plano. Os itens que têm elementos filho aninhados também têm glifos que indicam se o item está expandido ou recolhido.  
  
 ![Redline de exibição de árvore](../extensibility/ux-guidelines/media/0303-147-treeviewredline.png "0303-147_TreeViewRedline")  
  
 Usar...  
 em qualquer lugar, você precisa implementar uma exibição organizacional hierárquica.  
  
Não use...  
- para qualquer coisa que não seja semelhante a uma exibição de árvore.  

- em qualquer combinação de plano de fundo/primeiro plano diferente de especificada.  
  
  **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Modo de exibição de árvore](../extensibility/ux-guidelines/media/0303-148-treeview.png "0303-148_TreeView")|Segundo plano|`TreeView.Background`|  
|![Modo de exibição de árvore](../extensibility/ux-guidelines/media/0303-148-treeview.png "0303-148_TreeView")|Primeiro plano (texto)|`TreeView.Background`|  
|![Modo de exibição de árvore](../extensibility/ux-guidelines/media/0303-148-treeview.png "0303-148_TreeView")|Primeiro plano (glifo)|`TreeView.Glyph`|  
|![Modo de exibição de árvore](../extensibility/ux-guidelines/media/0303-148-treeview.png "0303-148_TreeView")|Borda|Nenhum|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Modo de exibição de árvore em foco](../extensibility/ux-guidelines/media/0303-149-treeviewhover.png "0303-149_TreeViewHover")|Segundo plano|`TreeView.Background`|  
|![Modo de exibição de árvore em foco](../extensibility/ux-guidelines/media/0303-149-treeviewhover.png "0303-149_TreeViewHover")|Primeiro plano (texto)|`TreeView.Background`|  
|![Modo de exibição de árvore em foco](../extensibility/ux-guidelines/media/0303-149-treeviewhover.png "0303-149_TreeViewHover")|Primeiro plano (glifo)|`TreeView.GlyphMouseOver`|  
|![Modo de exibição de árvore em foco](../extensibility/ux-guidelines/media/0303-149-treeviewhover.png "0303-149_TreeViewHover")|Borda|Nenhum|  
  
 **Arrastar sobre**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![DragOver de exibição de árvore](../extensibility/ux-guidelines/media/0303-150-treeviewdragover.png "0303-150_TreeViewDragOver")|Segundo plano|`TreeView.DragOverItem`|  
|![DragOver de exibição de árvore](../extensibility/ux-guidelines/media/0303-150-treeviewdragover.png "0303-150_TreeViewDragOver")|Primeiro plano (texto)|`TreeView.DragOverItem`|  
|![DragOver de exibição de árvore](../extensibility/ux-guidelines/media/0303-150-treeviewdragover.png "0303-150_TreeViewDragOver")|Primeiro plano (glifo)|`TreeView.DragOverItemGlyph`|  
|![DragOver de exibição de árvore](../extensibility/ux-guidelines/media/0303-150-treeviewdragover.png "0303-150_TreeViewDragOver")|Borda|Nenhum|  
  
 **Selected**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Modo de exibição de árvore focado](../extensibility/ux-guidelines/media/0303-151-treeviewfocused.png "0303-151_TreeViewFocused")<br /><br /> **Focused**|Segundo plano|`TreeView.SelectedItemActive`|  
|![Modo de exibição de árvore focado](../extensibility/ux-guidelines/media/0303-151-treeviewfocused.png "0303-151_TreeViewFocused")<br /><br /> **Focused**|Primeiro plano (texto)|`TreeView.SelectedItemActive`|  
|![Modo de exibição de árvore focado](../extensibility/ux-guidelines/media/0303-151-treeviewfocused.png "0303-151_TreeViewFocused")<br /><br /> **Focused**|Primeiro plano (glifo)|`TreeView.SelectedItemActiveGlyph`|  
|![Modo de exibição de árvore focado](../extensibility/ux-guidelines/media/0303-151-treeviewfocused.png "0303-151_TreeViewFocused")<br /><br /> **Focused**|Borda|`TreeView.FocusVisualBorder`|  
|![Modo de exibição de árvore não focalizado](../extensibility/ux-guidelines/media/0303-152-treeviewunfocused.png "0303-152_TreeViewUnfocused")<br /><br /> **Sem foco**|Segundo plano|`TreeView.SelectedItemInactive`|  
|![Modo de exibição de árvore não focalizado](../extensibility/ux-guidelines/media/0303-152-treeviewunfocused.png "0303-152_TreeViewUnfocused")<br /><br /> **Sem foco**|Primeiro plano (texto)|`TreeView.SelectedItemInactive`|  
|![Modo de exibição de árvore não focalizado](../extensibility/ux-guidelines/media/0303-152-treeviewunfocused.png "0303-152_TreeViewUnfocused")<br /><br /> **Sem foco**|Primeiro plano (glifo)|`TreeView.SelectedItemInactiveGlyph`|  
|![Modo de exibição de árvore não focalizado](../extensibility/ux-guidelines/media/0303-152-treeviewunfocused.png "0303-152_TreeViewUnfocused")<br /><br /> **Sem foco**|Borda|Nenhum|  
  
 **Focalizar selecionado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Exibição de árvore focada no foco](../extensibility/ux-guidelines/media/0303-153-treeviewfocusedhover.png "0303-153_TreeViewFocusedHover")<br /><br /> **Focused**|Segundo plano|`TreeView.SelectedItemActive`|  
|![Exibição de árvore focada no foco](../extensibility/ux-guidelines/media/0303-153-treeviewfocusedhover.png "0303-153_TreeViewFocusedHover")<br /><br /> **Focused**|Primeiro plano (texto)|`TreeView.SelectedItemActive`|  
|![Exibição de árvore focada no foco](../extensibility/ux-guidelines/media/0303-153-treeviewfocusedhover.png "0303-153_TreeViewFocusedHover")<br /><br /> **Focused**|Primeiro plano (glifo)|`TreeView.SelectedItemActiveGlyphMouseOver`|  
|![Exibição de árvore focada no foco](../extensibility/ux-guidelines/media/0303-153-treeviewfocusedhover.png "0303-153_TreeViewFocusedHover")<br /><br /> **Focused**|Borda|Nenhum`TreeView.FocusVisualBorder`|  
|![Modo de exibição de árvore não focalizado ao focalizar](../extensibility/ux-guidelines/media/0303-154-treeviewunfocusedhover.png "0303-154_TreeViewUnfocusedHover")<br /><br /> **Sem foco**|Segundo plano|`TreeView.SelectedItemInactive`|  
|![Modo de exibição de árvore não focalizado ao focalizar](../extensibility/ux-guidelines/media/0303-154-treeviewunfocusedhover.png "0303-154_TreeViewUnfocusedHover")<br /><br /> **Sem foco**|Primeiro plano (texto)|`TreeView.SelectedItemInactive`|  
|![Modo de exibição de árvore não focalizado ao focalizar](../extensibility/ux-guidelines/media/0303-154-treeviewunfocusedhover.png "0303-154_TreeViewUnfocusedHover")<br /><br /> **Sem foco**|Primeiro plano (glifo)|`TreeView.SelectedItemActiveGlyphMouseOver`|  
|![Modo de exibição de árvore não focalizado ao focalizar](../extensibility/ux-guidelines/media/0303-154-treeviewunfocusedhover.png "0303-154_TreeViewUnfocusedHover")<br /><br /> **Sem foco**|Borda|Nenhum|  
  
#### <a name="button-controls"></a>Controles de botão  
 ![Redline de controle de botão](../extensibility/ux-guidelines/media/0303-155-buttoncontrolredline.png "0303-155_ButtonControlRedline")  
  
 Usar...  
 para os botões no documento bem que você deseja integrar com temas do Visual Studio (claro, escuro, azul ou um tema de Alto Contraste do sistema).  
  
 Não use...  
 para botões que serão exibidos em um plano de fundo personalizado que não faz parte de um tema do Visual Studio.  
  
 **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Botão](../extensibility/ux-guidelines/media/0303-156-button.png "0303-156_Button")|Botão|`CommonControls.Button`|  
|![Botão](../extensibility/ux-guidelines/media/0303-156-button.png "0303-156_Button")|Borda do botão|`CommonControls.ButtonBorder`|  
  
 **Desabilitado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Botão desabilitado](../extensibility/ux-guidelines/media/0303-157-buttondisabled.png "0303-157_ButtonDisabled")|Botão|`CommonControls.ButtonDisabled`|  
|![Botão desabilitado](../extensibility/ux-guidelines/media/0303-157-buttondisabled.png "0303-157_ButtonDisabled")|Borda do botão|`CommonControls.ButtonBorderDisabled`|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Botão ao focalizar](../extensibility/ux-guidelines/media/0303-158-buttonhover.png "0303-158_ButtonHover")|Botão|`CommonControls.ButtonHover`|  
|![Botão ao focalizar](../extensibility/ux-guidelines/media/0303-158-buttonhover.png "0303-158_ButtonHover")|Borda do botão|`CommonControls.ButtonBorderHover`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Botão pressionado](../extensibility/ux-guidelines/media/0303-159-buttonpressed.png "0303-159_ButtonPressed")|Botão|`CommonControls.ButtonPressed`|  
|![Botão pressionado](../extensibility/ux-guidelines/media/0303-159-buttonpressed.png "0303-159_ButtonPressed")|Borda do botão|`CommonControls.ButtonBorderPressed`|  
  
 **Focused**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Foco no botão](../extensibility/ux-guidelines/media/0303-160-buttonfocused.png "0303-160_ButtonFocused")|Botão|`CommonControls.ButtonFocused`|  
|![Foco no botão](../extensibility/ux-guidelines/media/0303-160-buttonfocused.png "0303-160_ButtonFocused")|Borda do botão|`CommonControls.ButtonBorderFocused`|  
  
#### <a name="check-box-controls"></a>Controles da caixa de seleção  
 ![Caixa de seleção Redline](../extensibility/ux-guidelines/media/0303-161-checkboxredline.png "0303-161_CheckboxRedline")  
  
 Usar...  
 para controles de caixa de seleção contidos no documento bem.  
  
 Não use...  
 para qualquer interface do usuário que não seja um controle de caixa de seleção.  
  
 **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Caixa de seleção](../extensibility/ux-guidelines/media/0303-162-checkbox.png "0303-162_Checkbox")|Segundo plano|`CommonControls.CheckBoxBackground`|  
|![Caixa de seleção](../extensibility/ux-guidelines/media/0303-162-checkbox.png "0303-162_Checkbox")|Borda|`CommonControls.CheckBoxBorder`|  
|![Caixa de seleção](../extensibility/ux-guidelines/media/0303-162-checkbox.png "0303-162_Checkbox")|Texto|`CommonControls.CheckBoxText`|  
|![Caixa de seleção](../extensibility/ux-guidelines/media/0303-162-checkbox.png "0303-162_Checkbox")|Glifo|`CommonControls.CheckBoxGlyph`|  
  
 **Desabilitado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Caixa de seleção desabilitada](../extensibility/ux-guidelines/media/0303-163-checkboxdisabled.png "0303-163_CheckboxDisabled")|Segundo plano|`CommonControls.CheckBoxBackgroundDisabled`|  
|![Caixa de seleção desabilitada](../extensibility/ux-guidelines/media/0303-163-checkboxdisabled.png "0303-163_CheckboxDisabled")|Borda|`CommonControls.CheckBoxBorderDisabled`|  
|![Caixa de seleção desabilitada](../extensibility/ux-guidelines/media/0303-163-checkboxdisabled.png "0303-163_CheckboxDisabled")|Texto|`CommonControls.CheckBoxTextDisabled`|  
|![Caixa de seleção desabilitada](../extensibility/ux-guidelines/media/0303-163-checkboxdisabled.png "0303-163_CheckboxDisabled")|Glifo|`CommonControls.CheckBoxGlyphDisabled`|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Caixa de seleção ao focalizar](../extensibility/ux-guidelines/media/0303-164-checkboxhover.png "0303-164_CheckboxHover")|Segundo plano|`CommonControls.CheckBoxBackgroundHover`|  
|![Caixa de seleção ao focalizar](../extensibility/ux-guidelines/media/0303-164-checkboxhover.png "0303-164_CheckboxHover")|Borda|`CommonControls.CheckBoxBorderHover`|  
|![Caixa de seleção ao focalizar](../extensibility/ux-guidelines/media/0303-164-checkboxhover.png "0303-164_CheckboxHover")|Texto|`CommonControls.CheckBoxTextHover`|  
|![Caixa de seleção ao focalizar](../extensibility/ux-guidelines/media/0303-164-checkboxhover.png "0303-164_CheckboxHover")|Glifo|`CommonControls.CheckBoxGlyphHover`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Caixa de seleção pressionada](../extensibility/ux-guidelines/media/0303-165-checkboxpressed.png "0303-165_CheckboxPressed")|Segundo plano|`CommonControls.CheckBoxBackgroundPressed`|  
|![Caixa de seleção pressionada](../extensibility/ux-guidelines/media/0303-165-checkboxpressed.png "0303-165_CheckboxPressed")|Borda|`CommonControls.CheckBoxBorderPressed`|  
|![Caixa de seleção pressionada](../extensibility/ux-guidelines/media/0303-165-checkboxpressed.png "0303-165_CheckboxPressed")|Texto|`CommonControls.CheckBoxTextPressed`|  
|![Caixa de seleção pressionada](../extensibility/ux-guidelines/media/0303-165-checkboxpressed.png "0303-165_CheckboxPressed")|Glifo|`CommonControls.CheckBoxGlyphPressed`|  
  
 **Focused**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Caixa de seleção focada](../extensibility/ux-guidelines/media/0303-166-checkboxfocused.png "0303-166_CheckboxFocused")|Segundo plano|`CommonControls.CheckBoxBackgroundFocused`|  
|![Caixa de seleção focada](../extensibility/ux-guidelines/media/0303-166-checkboxfocused.png "0303-166_CheckboxFocused")|Borda|`CommonControls.CheckBoxBorderFocused`|  
|![Caixa de seleção focada](../extensibility/ux-guidelines/media/0303-166-checkboxfocused.png "0303-166_CheckboxFocused")|Texto|`CommonControls.CheckBoxTextFocused`|  
|![Caixa de seleção focada](../extensibility/ux-guidelines/media/0303-166-checkboxfocused.png "0303-166_CheckboxFocused")|Glifo|`CommonControls.CheckBoxGlyphFocused`|  
  
#### <a name="drop-boxcombo-box-controls"></a>Controles da caixa de combinação/caixa suspensa  
 ![Soltar&#45;&#47;caixa de combinação Redline](../extensibility/ux-guidelines/media/0303-167-dropdowncomboboxredline.png "0303-167_DropDownComboBoxRedline")  
  
Usar...  
para menus suspensos e caixas de combinação que fazem parte do bem do documento.  

Não use...  
- para qualquer interface do usuário que não seja uma lista suspensa ou uma caixa de combinação.  

- para uma [lista](../misc/shared-colors.md#BKMK_CommandDropDown) suspensa ou uma [caixa de combinação](../misc/shared-colors.md#BKMK_CommandComboBox) na barra de comandos.  
  
  **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![&#45;caixa de combinação de&#47;suspensa](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|Segundo plano|`CommonControls.ComboBoxBackground`|  
|![&#45;caixa de combinação de&#47;suspensa](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|Borda|`CommonControls.ComboBoxBorder`|  
|![&#45;caixa de combinação de&#47;suspensa](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|Texto|`CommonControls.ComboBoxText`|  
|![&#45;caixa de combinação de&#47;suspensa](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|Separador|`CommonControls.ComboBoxSeparator`|  
|![&#45;caixa de combinação de&#47;suspensa](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|Glifo|`CommonControls.ComboBoxGlyph`|  
|![&#45;caixa de combinação de&#47;suspensa](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|Plano de fundo do glifo|`CommonControls.ComboBoxGlyphBackground`|  
  
 **Desabilitado**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![&#45;descartar&#47;caixa de combinação desabilitada](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")|Segundo plano|`CommonControls.ComboBoxBackgroundDisabled`|  
|![&#45;descartar&#47;caixa de combinação desabilitada](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")|Borda|`CommonControls.ComboBoxBorderDisabled`|  
|![&#45;descartar&#47;caixa de combinação desabilitada](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")|Texto|`CommonControls.ComboBoxTextDisabled`|  
|![&#45;descartar&#47;caixa de combinação desabilitada](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")|Separador|`CommonControls.ComboBoxSeparatorDisabled`|  
|![&#45;descartar&#47;caixa de combinação desabilitada](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")|Glifo|`CommonControls.ComboBoxGlyphDisabled`|  
|![&#45;descartar&#47;caixa de combinação desabilitada](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")|Plano de fundo do glifo|`CommonControls.ComboBoxGlyphBackgroundDisabled`|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Soltar&#45;&#47;caixa de combinação ao focalizar](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")|Segundo plano|`CommonControls.ComboBoxBackgroundHover`|  
|![Soltar&#45;&#47;caixa de combinação ao focalizar](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")|Borda|`CommonControls.ComboBoxBorderHover`|  
|![Soltar&#45;&#47;caixa de combinação ao focalizar](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")|Texto|`CommonControls.ComboBoxTextHover`|  
|![Soltar&#45;&#47;caixa de combinação ao focalizar](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")|Separador|`CommonControls.ComboBoxSeparatorHover`|  
|![Soltar&#45;&#47;caixa de combinação ao focalizar](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")|Glifo|`CommonControls.ComboBoxGlyphHover`|  
|![Soltar&#45;&#47;caixa de combinação ao focalizar](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")|Plano de fundo do glifo|`CommonControls.ComboBoxGlyphBackgroundHover`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Soltar&#45;&#47;caixa de combinação pressionada](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")|Segundo plano|`CommonControls.ComboBoxBackgroundPressed`|  
|![Soltar&#45;&#47;caixa de combinação pressionada](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")|Borda|`CommonControls.ComboBoxBorderPressed`|  
|![Soltar&#45;&#47;caixa de combinação pressionada](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")|Texto|`CommonControls.ComboBoxTextPressed`|  
|![Soltar&#45;&#47;caixa de combinação pressionada](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")|Separador|`CommonControls.ComboBoxSeparatorPressed`|  
|![Soltar&#45;&#47;caixa de combinação pressionada](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")|Glifo|`CommonControls.ComboBoxGlyphPressed`|  
|![Soltar&#45;&#47;caixa de combinação pressionada](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")|Plano de fundo do glifo|`CommonControls.ComboBoxGlyphBackgroundPressed`|  
  
 **Focused**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Descartar&#45;&#47;caixa de combinação focada](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")|Segundo plano|`CommonControls.ComboBoxBackgroundFocused`|  
|![Descartar&#45;&#47;caixa de combinação focada](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")|Borda|`CommonControls.ComboBoxBorderFocused`|  
|![Descartar&#45;&#47;caixa de combinação focada](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")|Texto|`CommonControls.ComboBoxTextFocused`|  
|![Descartar&#45;&#47;caixa de combinação focada](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")|Separador|`CommonControls.ComboBoxSeparatorFocused`|  
|![Descartar&#45;&#47;caixa de combinação focada](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")|Glifo|`CommonControls.ComboBoxGlyphFocused`|  
|![Descartar&#45;&#47;caixa de combinação focada](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")|Plano de fundo do glifo|`CommonControls.ComboBoxGlyphBackgroundFocused`|  
  
 **Seleção de entrada de texto**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Soltar&#45;&#47;entrada de texto da caixa de combinação](../extensibility/ux-guidelines/media/0303-173-dropdowncomboboxtextinput.png "0303-173_DropDownComboBoxTextInput")|Realce|`CommonControls.ComboBoxTextInputSelection`|  
  
 **Pressionado – exibição de item de lista**  
  
|Componente|Elemento|Nome do token: Color. Category|  
|---------------|-------------|--------------------------------|  
|![Soltar&#45;para baixo&#47;exibição de lista da caixa de combinação](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|Segundo plano|`CommonControls.ComboBoxListBackground`|  
|![Soltar&#45;para baixo&#47;exibição de lista da caixa de combinação](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|Segundo plano|`CommonControls.ComboBoxListBackgroundHover`|  
|![Soltar&#45;para baixo&#47;exibição de lista da caixa de combinação](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|Segundo plano|`CommonControls.ComboBoxListItemBackgroundPressed`|  
|![Soltar&#45;para baixo&#47;exibição de lista da caixa de combinação](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|Segundo plano|`CommonControls.ComboBoxListItemBackgroundFocused`|  
|![Soltar&#45;para baixo&#47;exibição de lista da caixa de combinação](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|Borda|`CommonControls.ComboBoxListBorder`|  
|![Soltar&#45;para baixo&#47;exibição de lista da caixa de combinação](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|Borda|`CommonControls.ComboBoxListBorderHover`|  
|![Soltar&#45;para baixo&#47;exibição de lista da caixa de combinação](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|Borda|`CommonControls.ComboBoxListBorderPressed`|  
|![Soltar&#45;para baixo&#47;exibição de lista da caixa de combinação](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|Borda|`CommonControls.ComboBoxListBorderFocused`|  
|![Soltar&#45;para baixo&#47;exibição de lista da caixa de combinação](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|Texto do item|`CommonControls.ComboBoxListItemText`|  
|![Soltar&#45;para baixo&#47;exibição de lista da caixa de combinação](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|Texto do item|`CommonControls.ComboBoxListItemTextHover`|  
|![Soltar&#45;para baixo&#47;exibição de lista da caixa de combinação](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|Texto do item|`CommonControls.ComboBoxListItemTextPressed`|  
|![Soltar&#45;para baixo&#47;exibição de lista da caixa de combinação](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|Texto do item|`CommonControls.ComboBoxListItemTextFocused`|  
|![Soltar&#45;para baixo&#47;exibição de lista da caixa de combinação](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|Sombra em segundo plano|`CommonControls.ComboBoxListBackgroundShadow`|  
  
#### <a name="tabular-data-grid-controls"></a>Controles de dados tabulares (grade)  
 Controles de dados tabulares, também conhecidos como controles de grade, são controles comuns para o Visual Studio que podem ser usados para apresentar grandes quantidades de dados em várias colunas. Os controles de dados de tabela padrão podem ser encontrados em vários locais no Visual Studio: a janela de ferramentas Lista de Erros, os relatórios do IntelliTrace e a exibição de heap de memória, entre outros. Sempre use os controles de dados tabulares padrão fornecidos. Em algumas instâncias raras, talvez você não tenha acesso aos controles de dados tabulares padrão. Nessas situações, use os nomes de token a seguir para garantir que sua interface do usuário seja consistente com outros controles de dados de tabela no Visual Studio.  
  
 ![Dados tabulares &#40;controle de grade&#41; Redline](../extensibility/ux-guidelines/media/0303-197-tabulardatagridcontrolredline.png "0303-197_TabularDataGridControlRedline")  
  
 Usar...  
 para controles de tabela ou de grade.  
  
 Não use...  
 para qualquer interface do usuário que não seja um controle de tabela ou de grade.  
  
##### <a name="column-headers"></a>Cabeçalhos da coluna  
 Os cabeçalhos de coluna consistem em um plano de fundo, uma borda, o texto do título e um glifo opcional geralmente usado quando uma grade é classificada por essa coluna.  
  
|Estado|Elemento|Nome do token: categoria. cor|  
|-----------|-------------|--------------------------------|  
|Padrão|Segundo plano|`Header.Default`|  
|Padrão|Primeiro plano (texto)|`Environment.CommandBarTextActive`|  
|Padrão|Primeiro plano (glifo)|`Header.Glyph`|  
|Padrão|Borda|`Header.SeparatorLine`|  
|Passar o mouse|Segundo plano|`Header.MouseOver`|  
|Passar o mouse|Primeiro plano (texto)|`Environment.CommandBarTextHover`|  
|Passar o mouse|Primeiro plano (glifo)|`Header.MouseOverGlyph`|  
|Passar o mouse|Borda|`Header.SeparatorLine`|  
|Pressionado|Segundo plano|`CommonControls.CheckBoxBackgroundPressed`|  
|Pressionado|Primeiro plano (texto)|`CommonControls.CheckBoxBorderPressed`|  
|Pressionado|Primeiro plano (glifo)|`CommonControls.CheckBoxTextPressed`|  
|Pressionado|Borda|`CommonControls.CheckBoxGlyphPressed`|  
  
##### <a name="list-view-items"></a>Listar itens de exibição  
 Os itens de exibição de lista consistem em um plano de fundo e o conteúdo. O conteúdo pode ser texto, um ícone ou ambos.  
  
|Estado|Elemento|Nome do token: categoria. cor|  
|-----------|-------------|--------------------------------|  
|Padrão|Segundo plano|Transparente|  
|Padrão|Primeiro plano (texto)|`Environment.CommandBarTextActive`|  
|Padrão|Borda|Nenhum|  
|Selecionado (ativo)|Segundo plano|`TreeView.SelectedItemActive`|  
|Selecionado (ativo)|Primeiro plano (texto)|`TreeView.SelectedItemActiveText`|  
|Selecionado (ativo)|Borda|Nenhum|  
|Selecionado (inativo)|Segundo plano|`TreeView.SelectedItemInactive`|  
|Selecionado (inativo)|Primeiro plano (texto)|`TreeView.SelectedItemInactiveText`|  
|Selecionado (inativo)|Borda|Nenhum|  
  
### <a name="manifest-designer"></a>Designer de manifesto  
 O designer de manifesto foi projetado como uma maneira de facilitar a edição do arquivo de manifesto nos projetos do Windows 8 e do Windows Phone 8. Embora não haja nenhuma estrutura compartilhada disponível para consumo, pode ser apropriado que você corresponda ao layout de design e às cores das guias de orientação/navegação e da estrutura geral. Para obter mais informações sobre detalhes de layout, consulte [layout para Visual Studio](../extensibility/ux-guidelines/layout-for-visual-studio.md).  
  
 ![Designer de manifesto Redline](../extensibility/ux-guidelines/media/0303-175-manifestdesignerredline.png "0303-175_ManifestDesignerRedline")  
  
Usar...  
- para designers semelhantes ao designer de manifesto.  

- em vez de usar os controles de guia comuns na parte superior de um editor dentro do bem do documento.  

Não use...  
- Se você tiver mais de seis guias.  

- para qualquer interface do usuário que não seja estruturada como o designer de manifesto.  
  
|Estado|Componente|Elemento|Nome do token: categoria. cor|  
|-----------|---------------|-------------|--------------------------------|  
|Padrão (selecionado)|Tab|Segundo plano|`ManifestDesigner.TabActive`|  
|Padrão (selecionado)|Tab|Borda|Nenhum|  
|Padrão (selecionado)|Painel de descrição|Segundo plano|`ManifestDesigner.DescriptionPane`|  
|Padrão (selecionado)|Página de conteúdo|Segundo plano|`ManifestDesigner.Background`|  
|Padrão (selecionado)|Página de conteúdo|Texto auxiliar de diálogo|`ManifestDesigner.WatermarkText`<br /><br /> Esse nome de token não corresponde à sua função.|  
|Não selecionado|Tab|Segundo plano|`ManifestDesigner.Tab.Inactive`|  
|Passar o mouse|Tab|Segundo plano|`ManifestDesigner.Tab.Mouseover`|  
  
### <a name="tagging"></a>Marcação  
 O Visual Studio dá suporte à marcação, que permite que um usuário declare palavras-chave pesquisáveis para fins de acompanhamento. Por exemplo, gerentes de projeto e desenvolvedores podem usar Team Foundation Server (TFS) para marcar itens de trabalho. As tabelas a seguir fornecem nomes de cor para a marca em si e o glifo "ícone de fechamento" que aparece nos Estados de focalizar e selecionados.  
  
 ![Marcando Redline](../extensibility/ux-guidelines/media/0303-176-taggingredline.png "0303-176_TaggingRedline")  
  
 Usar...  
 para a interface do usuário que dá suporte à marcação.  
  
 Não use...  
 para qualquer outro tipo de interface do usuário.  
  
#### <a name="tag"></a>Marca  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Tag](../extensibility/ux-guidelines/media/0303-177-tag.png "0303-177_Tag")<br /><br /> **Default**|Segundo plano|`Tag.Background`|  
|![Tag](../extensibility/ux-guidelines/media/0303-177-tag.png "0303-177_Tag")<br /><br /> **Default**|Primeiro plano (texto)|`Tag.Background`|  
|![Marca ao focalizar](../extensibility/ux-guidelines/media/0303-178-taghover.png "0303-178_TagHover")<br /><br /> **Passar o mouse**|Segundo plano|`Tag.HoverBackground`|  
|![Marca ao focalizar](../extensibility/ux-guidelines/media/0303-178-taghover.png "0303-178_TagHover")<br /><br /> **Passar o mouse**|Primeiro plano (texto)|`Tag.HoverBackgroundText`|  
|![Marca pressionada](../extensibility/ux-guidelines/media/0303-179-tagpressed.png "0303-179_TagPressed")<br /><br /> **Pressed**|Segundo plano|`Tag.PressedBackground`|  
|![Marca pressionada](../extensibility/ux-guidelines/media/0303-179-tagpressed.png "0303-179_TagPressed")<br /><br /> **Pressed**|Primeiro plano (texto)|`Tag.PressedBackgroundText`|  
|![Marca selecionada](../extensibility/ux-guidelines/media/0303-180-tagselected.png "0303-180_TagSelected")<br /><br /> **Selected**|Segundo plano|`Tag.SelectedBackground`|  
|![Marca selecionada](../extensibility/ux-guidelines/media/0303-180-tagselected.png "0303-180_TagSelected")<br /><br /> **Selected**|Primeiro plano (texto)|`Tag.SelectedBackgroundText`|  
  
#### <a name="glyph-close-icon"></a>Glifo (ícone de fechamento)  
 **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Marca de &#40;glifo&#41;](../extensibility/ux-guidelines/media/0303-181-tagglyph.png "0303-181_TagGlyph")<br /><br /> **Padrão (marca padrão)**|Segundo plano|N/D|  
|![Marca de &#40;glifo&#41;](../extensibility/ux-guidelines/media/0303-181-tagglyph.png "0303-181_TagGlyph")<br /><br /> **Padrão (marca padrão)**|Primeiro plano (glifo)|`Tag.TagHoverGlyph`|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Marcação &#40;glifo&#41; ao focalizar](../extensibility/ux-guidelines/media/0303-182-tagglyphhover.png "0303-182_TagGlyphHover")<br /><br /> **Hover (marca padrão)**|Segundo plano|`Tag.TagHoverGlyphHoverBackground`|  
|![Marcação &#40;glifo&#41; ao focalizar](../extensibility/ux-guidelines/media/0303-182-tagglyphhover.png "0303-182_TagGlyphHover")<br /><br /> **Hover (marca padrão)**|Primeiro plano (glifo)|`Tag.TagHoverGlyphHover`|  
|![Marcação &#40;glifo&#41; ao focalizar](../extensibility/ux-guidelines/media/0303-182-tagglyphhover.png "0303-182_TagGlyphHover")<br /><br /> **Hover (marca padrão)**|Borda|`Tag.TagHoverGlyphHoverBorder`|  
  
 **Pressed**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Marca &#40;glifo&#41; pressionado](../extensibility/ux-guidelines/media/0303-183-tagglyphpressed.png "0303-183_TagGlyphPressed")<br /><br /> **Pressionado (marca padrão)**|Segundo plano|`Tag.TagHoverGlyphPressedBackground`|  
|![Marca &#40;glifo&#41; pressionado](../extensibility/ux-guidelines/media/0303-183-tagglyphpressed.png "0303-183_TagGlyphPressed")<br /><br /> **Pressionado (marca padrão)**|Primeiro plano (glifo)|`Tag.TagHoverGlyphPressed`|  
|![Marca &#40;glifo&#41; pressionado](../extensibility/ux-guidelines/media/0303-183-tagglyphpressed.png "0303-183_TagGlyphPressed")<br /><br /> **Pressionado (marca padrão)**|Borda|`Tag.TagHoverGlyphPressedBorder`|  
  
 **Marca de seleção/padrão de glifo**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Marca selecionada](../extensibility/ux-guidelines/media/0303-184-tagselected.png "0303-184_TagSelected")<br /><br /> **Padrão (marca selecionada)**|Segundo plano|N/D|  
|![Marca selecionada](../extensibility/ux-guidelines/media/0303-184-tagselected.png "0303-184_TagSelected")<br /><br /> **Padrão (marca selecionada)**|Primeiro plano (glifo)|`Tag.TagSelectedGlyph`|  
  
 **Marca de foco selecionado/glifo**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Marca selecionada ao focalizar](../extensibility/ux-guidelines/media/0303-185-tagselectedhover.png "0303-185_TagSelectedHover")<br /><br /> **Hover (marca selecionada)**|Segundo plano|`Tag.TagSelectedGlyphHoverBackground`|  
|![Marca selecionada ao focalizar](../extensibility/ux-guidelines/media/0303-185-tagselectedhover.png "0303-185_TagSelectedHover")<br /><br /> **Hover (marca selecionada)**|Primeiro plano (glifo)|`Tag.TagSelectedGlyphHover`|  
|![Marca selecionada ao focalizar](../extensibility/ux-guidelines/media/0303-185-tagselectedhover.png "0303-185_TagSelectedHover")<br /><br /> **Hover (marca selecionada)**|Borda|`Tag.TagSelectedGlyphHoverBorder`|  
  
 **Marca selecionada/glifo pressionada**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Marca selecionada pressionada](../extensibility/ux-guidelines/media/0303-186-tagselectedpressed.png "0303-186_TagSelectedPressed")<br /><br /> **Pressionado (marca selecionada)**|Segundo plano|`Tag.TagSelectedGlyphPressedBackground`|  
|![Marca selecionada pressionada](../extensibility/ux-guidelines/media/0303-186-tagselectedpressed.png "0303-186_TagSelectedPressed")<br /><br /> **Pressionado (marca selecionada)**|Primeiro plano (glifo)|`Tag.TagSelectedGlyphPressed`|  
|![Marca selecionada pressionada](../extensibility/ux-guidelines/media/0303-186-tagselectedpressed.png "0303-186_TagSelectedPressed")<br /><br /> **Pressionado (marca selecionada)**|Borda|`Tag.TagSelectedGlyphPressedBorder`|  
  
### <a name="shell"></a>Shell  
  
#### <a name="background"></a>Segundo plano  
 O plano de fundo do ambiente consiste em duas camadas. A camada inferior é uma cor sólida que cobre todo o IDE. A camada superior se ajusta na prateleira de comando e entre a janela de ferramentas oculta automaticamente os canais nas bordas esquerda e direita do IDE. A partir de Visual Studio 2013, as camadas de plano de fundo superior e inferior são definidas com a mesma cor nos temas claro e escuro.  
  
 ![Redline em segundo plano do Shell](../extensibility/ux-guidelines/media/0303-187-shellbackgroundredline.png "0303-187_ShellBackgroundRedline")  
  
 Usar...  
 para locais que você deseja corresponder ao plano de fundo do ambiente do Visual Studio.  
  
Não use...  
- como um preenchimento para lugares que não são superfícies de segundo plano.  

- como um plano de fundo no qual você deseja inserir elementos de primeiro plano.  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|Camada inferior|Segundo plano|`Environment.EnvironmentBackground`|  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|Camada superior|Segundo plano<br /><br /> *As interrupções de gradiente são definidas com o mesmo valor de cor nos temas Visual Studio 2013 claro e escuro.*|`Environment.EnvironmentBackgroundGradientBegin`|  
|Camada superior|Segundo plano<br /><br /> *As interrupções de gradiente são definidas com o mesmo valor de cor nos temas Visual Studio 2013 claro e escuro.*|`Environment.EnvironmentBackgroundGradientEnd`|  
|Camada superior|Segundo plano<br /><br /> *As interrupções de gradiente são definidas com o mesmo valor de cor nos temas Visual Studio 2013 claro e escuro.*|`Environment.EnvironmentBackgroundGradientMiddle1`|  
|Camada superior|Segundo plano<br /><br /> *As interrupções de gradiente são definidas com o mesmo valor de cor nos temas Visual Studio 2013 claro e escuro.*|`Environment.EnvironmentBackgroundGradientMiddle2`|  
  
#### <a name="command-shelf"></a>Prateleira de comando  
 Dois conjuntos de nomes de token são usados para os planos de fundo de prateleira de comando: um conjunto para o local em que a barra de menus reside e um para onde as barras de comando ficam. Um grupo de barras de comando individual tem seus próprios valores de cor de plano de fundo, que são discutidos com mais detalhes na seção "barra de comandos". A barra de menus e o texto da barra de comandos são discutidos nas seções do menu e da barra de comandos, respectivamente.  
  
 ![Redline de prateleira de comando](../extensibility/ux-guidelines/media/0303-188-commandshelfredline.png "0303-188_CommandShelfRedline")  
  
Usar...  
- para áreas em que você coloca menus ou barras de ferramentas.  

- com a combinação correta de nome de token de segundo plano/primeiro plano.  
  
  Não use...  
  para áreas que não são semelhantes a uma prateleira de comando.  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|Barra de menus|Segundo plano<br /><br /> *As interrupções de gradiente são definidas com o mesmo valor de cor nos temas Visual Studio 2013 claro e escuro.*|`Environment.CommandShelfHighlightGradientBegin`|  
|Barra de menus|Segundo plano<br /><br /> *As interrupções de gradiente são definidas com o mesmo valor de cor nos temas Visual Studio 2013 claro e escuro.*|`Environment.CommandShelfHighlightGradientMiddle`|  
|Barra de menus|Segundo plano<br /><br /> *As interrupções de gradiente são definidas com o mesmo valor de cor nos temas Visual Studio 2013 claro e escuro.*|`Environment.CommandShelfHighlightGradientEnd`|  
|Barra de comandos|Segundo plano<br /><br /> *As interrupções de gradiente são definidas com o mesmo valor de cor nos temas Visual Studio 2013 claro e escuro.*|`Environment.CommandShelfBackgroundGradientBegin`|  
|Barra de comandos|Segundo plano<br /><br /> *As interrupções de gradiente são definidas com o mesmo valor de cor nos temas Visual Studio 2013 claro e escuro.*|`Environment.CommandShelfBackgroundGradientMiddle`|  
|Barra de comandos|Segundo plano<br /><br /> *As interrupções de gradiente são definidas com o mesmo valor de cor nos temas Visual Studio 2013 claro e escuro.*|`Environment.CommandShelfBackgroundGradientEnd`|  
  
### <a name="toolbox"></a>Caixa de Ferramentas  
 A caixa de ferramentas é uma das janelas de ferramentas comuns que é usada com mais frequência no Visual Studio. Ele é essencialmente um controle de árvore com um tema e estilo especiais aplicados.  
  
 ![Caixa de ferramentas Redline](../extensibility/ux-guidelines/media/0303-189-toolboxredline.png "0303-189_ToolboxRedline")  
  
 Usar...  
 ao criar uma janela de ferramenta que você deseja que seja sempre consistente com a caixa de ferramentas do Shell.  
  
 Não use...  
 para qualquer coisa que não seja semelhante à interface do usuário da caixa de ferramentas, ou se você não tiver certeza se a sua interface do usuário terá problemas se as cores da caixa de ferramentas do Shell forem alteradas.  
  
 **Default**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Nó pai da caixa de ferramentas](../extensibility/ux-guidelines/media/0303-190-toolboxparentnode.png "0303-190_ToolboxParentNode")<br /><br /> **Nó pai**|Segundo plano|`Environment.ToolboxContent`<br /><br /> Títulos<br /><br /> `Environment.ToolWindowBackground`<br /><br /> Itens individuais ou janela inteira se não houver controles disponíveis|  
|![Nó filho da caixa de ferramentas](../extensibility/ux-guidelines/media/0303-191-toolboxchildnode.png "0303-191_ToolboxChildNode")<br /><br /> **Nó filho**|Segundo plano|`Environment.ToolboxContent`<br /><br /> Títulos<br /><br /> `Environment.ToolWindowBackground`<br /><br /> Itens individuais ou janela inteira se não houver controles disponíveis|  
|![Nó pai da caixa de ferramentas](../extensibility/ux-guidelines/media/0303-190-toolboxparentnode.png "0303-190_ToolboxParentNode")<br /><br /> **Nó pai**|Borda|Nenhum|  
|![Nó filho da caixa de ferramentas](../extensibility/ux-guidelines/media/0303-191-toolboxchildnode.png "0303-191_ToolboxChildNode")<br /><br /> **Nó filho**|Borda|Nenhum|  
|![Nó pai da caixa de ferramentas](../extensibility/ux-guidelines/media/0303-190-toolboxparentnode.png "0303-190_ToolboxParentNode")<br /><br /> **Nó pai**|Primeiro plano (glifo)|`Environment.ToolboxContent`|  
|![Nó filho da caixa de ferramentas](../extensibility/ux-guidelines/media/0303-191-toolboxchildnode.png "0303-191_ToolboxChildNode")<br /><br /> **Nó filho**|Primeiro plano (glifo)|`Environment.ToolboxContent`|  
|![Nó pai da caixa de ferramentas](../extensibility/ux-guidelines/media/0303-190-toolboxparentnode.png "0303-190_ToolboxParentNode")<br /><br /> **Nó pai**|Primeiro plano (texto)|`Environment.ToolboxContent`|  
|![Nó filho da caixa de ferramentas](../extensibility/ux-guidelines/media/0303-191-toolboxchildnode.png "0303-191_ToolboxChildNode")<br /><br /> **Nó filho**|Primeiro plano (texto)|`Environment.ToolboxContent`|  
  
 **Passar o mouse**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Nó filho da caixa de ferramentas ao focalizar](../extensibility/ux-guidelines/media/0303-192-toolboxchildnodehover.png "0303-192_ToolboxChildNodeHover")<br /><br /> **Foco da caixa de ferramentas no nó filho**|Segundo plano|`Environment.ToolboxContentMouseOver`<br /><br /> Somente itens individuais|  
|![Nó filho da caixa de ferramentas ao focalizar](../extensibility/ux-guidelines/media/0303-192-toolboxchildnodehover.png "0303-192_ToolboxChildNodeHover")<br /><br /> **Foco da caixa de ferramentas no nó filho**|Borda|Nenhum|  
|![Nó filho da caixa de ferramentas ao focalizar](../extensibility/ux-guidelines/media/0303-192-toolboxchildnodehover.png "0303-192_ToolboxChildNodeHover")<br /><br /> **Foco da caixa de ferramentas no nó filho**|Primeiro plano (texto)|`Environment.ToolboxContentMouseOver`<br /><br /> Somente itens individuais|  
  
 **Selected**  
  
|Componente|Elemento|Nome do token: categoria. cor|  
|---------------|-------------|--------------------------------|  
|![Foco no nó pai da caixa de ferramentas](../extensibility/ux-guidelines/media/0303-193-toolboxparentnodefocused.png "0303-193_ToolboxParentNodeFocused")<br /><br /> **Nó pai focado**|Segundo plano|`TreeView.SelectedItemActive`<br /><br /> Categoria da [exibição de árvore](../misc/shared-colors.md#BKMK_TreeView)|  
|![Nó filho da caixa de ferramentas focado](../extensibility/ux-guidelines/media/0303-194-toolboxchildnodefocused.png "0303-194_ToolboxChildNodeFocused")<br /><br /> **Nó filho focado**|Segundo plano|`TreeView.SelectedItemActive`<br /><br /> Categoria da [exibição de árvore](../misc/shared-colors.md#BKMK_TreeView)|  
|![Foco no nó pai da caixa de ferramentas](../extensibility/ux-guidelines/media/0303-193-toolboxparentnodefocused.png "0303-193_ToolboxParentNodeFocused")<br /><br /> **Nó pai focado**|Borda|`TreeView.FocusVisualBorder`<br /><br /> Categoria da [exibição de árvore](../misc/shared-colors.md#BKMK_TreeView)|  
|![Nó filho da caixa de ferramentas focado](../extensibility/ux-guidelines/media/0303-194-toolboxchildnodefocused.png "0303-194_ToolboxChildNodeFocused")<br /><br /> **Nó filho focado**|Borda|`TreeView.FocusVisualBorder`<br /><br /> Categoria da [exibição de árvore](../misc/shared-colors.md#BKMK_TreeView)|  
|![Foco no nó pai da caixa de ferramentas](../extensibility/ux-guidelines/media/0303-193-toolboxparentnodefocused.png "0303-193_ToolboxParentNodeFocused")<br /><br /> **Nó pai focado**|Primeiro plano (glifo)|`TreeView.SelectedItemActive`<br /><br /> Categoria da [exibição de árvore](../misc/shared-colors.md#BKMK_TreeView)|  
|![Nó filho da caixa de ferramentas focado](../extensibility/ux-guidelines/media/0303-194-toolboxchildnodefocused.png "0303-194_ToolboxChildNodeFocused")<br /><br /> **Nó filho focado**|Primeiro plano (glifo)|`TreeView.SelectedItemActive`<br /><br /> Categoria da [exibição de árvore](../misc/shared-colors.md#BKMK_TreeView)|  
|![Foco no nó pai da caixa de ferramentas](../extensibility/ux-guidelines/media/0303-193-toolboxparentnodefocused.png "0303-193_ToolboxParentNodeFocused")<br /><br /> **Nó pai focado**|Primeiro plano (texto)|`TreeView.SelectedItemActive`<br /><br /> Categoria da [exibição de árvore](../misc/shared-colors.md#BKMK_TreeView)|  
|![Nó filho da caixa de ferramentas focado](../extensibility/ux-guidelines/media/0303-194-toolboxchildnodefocused.png "0303-194_ToolboxChildNodeFocused")<br /><br /> **Nó filho focado**|Primeiro plano (texto)|`TreeView.SelectedItemActive`<br /><br /> Categoria da [exibição de árvore](../misc/shared-colors.md#BKMK_TreeView)|  
|![Nó pai da caixa de ferramentas desfocado](../extensibility/ux-guidelines/media/0303-195-toolboxparentnodeunfocused.png "0303-195_ToolboxParentNodeUnfocused")<br /><br /> **Nó pai não focalizado**|Segundo plano|`TreeView.SelectedItemInactive`<br /><br /> Categoria da [exibição de árvore](../misc/shared-colors.md#BKMK_TreeView)|  
|![Nó filho da caixa de ferramentas desfocado](../extensibility/ux-guidelines/media/0303-196-toolboxchildnodeunfocused.png "0303-196_ToolboxChildNodeUnfocused")<br /><br /> **Nó filho não focalizado**|Segundo plano|`TreeView.SelectedItemInactive`<br /><br /> Categoria da [exibição de árvore](../misc/shared-colors.md#BKMK_TreeView)|  
|![Nó pai da caixa de ferramentas desfocado](../extensibility/ux-guidelines/media/0303-195-toolboxparentnodeunfocused.png "0303-195_ToolboxParentNodeUnfocused")<br /><br /> **Nó pai não focalizado**|Borda|Nenhum|  
|![Nó filho da caixa de ferramentas desfocado](../extensibility/ux-guidelines/media/0303-196-toolboxchildnodeunfocused.png "0303-196_ToolboxChildNodeUnfocused")<br /><br /> **Nó filho não focalizado**|Borda|Nenhum|  
|![Nó pai da caixa de ferramentas desfocado](../extensibility/ux-guidelines/media/0303-195-toolboxparentnodeunfocused.png "0303-195_ToolboxParentNodeUnfocused")<br /><br /> **Nó pai não focalizado**|Primeiro plano (glifo)|`TreeView.SelectedItemInactive`<br /><br /> Categoria da [exibição de árvore](../misc/shared-colors.md#BKMK_TreeView)|  
|![Nó filho da caixa de ferramentas desfocado](../extensibility/ux-guidelines/media/0303-196-toolboxchildnodeunfocused.png "0303-196_ToolboxChildNodeUnfocused")<br /><br /> **Nó filho não focalizado**|Primeiro plano (glifo)|`TreeView.SelectedItemInactive`<br /><br /> Categoria da [exibição de árvore](../misc/shared-colors.md#BKMK_TreeView)|  
|![Nó pai da caixa de ferramentas desfocado](../extensibility/ux-guidelines/media/0303-195-toolboxparentnodeunfocused.png "0303-195_ToolboxParentNodeUnfocused")<br /><br /> **Nó pai não focalizado**|Primeiro plano (texto)|`TreeView.SelectedItemInactive`<br /><br /> Categoria da [exibição de árvore](../misc/shared-colors.md#BKMK_TreeView)|  
|![Nó filho da caixa de ferramentas desfocado](../extensibility/ux-guidelines/media/0303-196-toolboxchildnodeunfocused.png "0303-196_ToolboxChildNodeUnfocused")<br /><br /> **Nó filho não focalizado**|Primeiro plano (texto)|`TreeView.SelectedItemInactive`<br /><br /> Categoria da [exibição de árvore](../misc/shared-colors.md#BKMK_TreeView)|  
  
## <a name="color-value-reference"></a>Referência de valor de cor  
  
|Componente|Parte|Elemento|Estado|Leve|Escuro|Azul|Alto Contraste|
|---------|----|-------|-----|-----|----|----|----|  
|Linhas divisórias|||Padrão|FFEEEEF2|FF2D2D30|FFEEEEF2|ControlDark|  
|Glifo de expansor||Primeiro plano|Padrão|||||  
|Glifo de expansor||Primeiro plano|Passar o mouse|||||  
|Glifo de expansor||Segundo plano|Padrão|||||  
|Glifo de expansor||Segundo plano|Passar o mouse|||||  
|Glifo de expansor||Borda|Padrão|||||  
|Glifo de expansor||Borda|Passar o mouse|||||