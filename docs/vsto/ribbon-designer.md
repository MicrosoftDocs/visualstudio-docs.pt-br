---
title: Designer da faixa de opções
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- Designer_Microsoft.VisualStudio.Tools.Office.Ribbon.Design.RibbonDesigner
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, about Ribbon Designer
- controls [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], controls
- customizing the Ribbon, about Ribbon Designer
- Ribbon [Office development in Visual Studio], visual designer
- customizing the Ribbon
- custom Ribbon
- designers [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], customizing
- Ribbon [Office development in Visual Studio], common tasks
- Ribbon Designer [Office development in Visual Studio]
- read-only properties
- Ribbon [Office development in Visual Studio], shortcut keys
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: b85347b6bda0d42f7350d145baf2c824aa92a71c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49820610"
---
# <a name="ribbon-designer"></a>Designer da faixa de opções
  O Designer de faixa de opções é uma tela de design visual. Use o Designer de faixa de opções para adicionar guias personalizadas, grupos e controles à faixa de opções de um aplicativo do Microsoft Office.  
  
 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]  
  
 Para abrir o Designer de faixa de opções, adicione uma **faixa de opções (Visual Designer)** item ao seu projeto. Em seguida, você pode usar as ferramentas de design para as seguintes tarefas:  
  
-   [Criar o layout de faixa de opções](#DesigningRibbonLayout)  
  
-   [Manipular eventos e definir propriedades de controle](#HandleEventsSetProperties)  
  
-   [Adicionar controles ao modo de exibição Backstage](#CustomizingMicrosoftOfficeButton)  
  
> [!NOTE]  
>  Há algumas tarefas que você não pode realizar usando o Designer de faixa de opções. Para obter mais informações sobre essas tarefas e como realizá-las, consulte [visão geral da faixa de opções](../vsto/ribbon-overview.md).  
  
 ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [How do i: Use o Designer de faixa de opções para personalizar a faixa de opções no Outlook?](http://go.microsoft.com/fwlink/?LinkID=130312).  
  
## <a name="add-a-ribbon-visual-designer-item-to-a-project"></a>Adicionar um item da faixa de opções (Visual Designer) a um projeto  
 Para usar o Designer de faixa de opções, adicione um novo **faixa de opções (Visual Designer)** item ao seu projeto. Para obter mais informações, consulte [como: Introdução à personalização da faixa de opções](../vsto/how-to-get-started-customizing-the-ribbon.md).  
  
 Quando você adiciona um novo **faixa de opções (Visual Designer)** item, o Visual Studio adiciona automaticamente os arquivos a seguir ao seu projeto:  
  
- Um arquivo de código da faixa de opções. Este arquivo tem o nome que você especificar para o **faixa de opções (Visual Designer)** item o **Adicionar Novo Item** caixa de diálogo. Adicione código para manipular eventos da faixa de opções para esse arquivo.  
  
- Um arquivo de código do Designer de faixa de opções. Esse arquivo contém o código gerado pelo Designer de faixa de opções e não deve ser editado diretamente.  
  
- Um arquivo de recurso. Esse arquivo contém os valores de propriedade de cada controle na faixa de opções.  
  
  Se você já tiver um **faixa de opções (Visual Designer)** item de outro projeto, você pode reutilizá-lo em seu projeto atual usando o **Add Existing Item** caixa de diálogo.  
  
##  <a name="DesigningRibbonLayout"></a> Uma faixa de opções de design  
 Há três maneiras de abrir o Designer de faixa de opções:  
  
- Na **Gerenciador de soluções**, clique duas vezes no arquivo de código da faixa de opções.  
  
- Na **Gerenciador de soluções**, clique no arquivo de código da faixa de opções e, em seguida, clique em **View Designer**.  
  
- Na **Gerenciador de soluções**, selecione o arquivo de código da faixa de opções e, em seguida, clique em **Designer** sobre o **exibição** menu.  
  
  O Designer de faixa de opções contém um guia padrão e um grupo. Você pode remover a guia padrão e o grupo da faixa de opções. Para remover o grupo padrão, clique com botão direito **Group1**e, em seguida, clique em **excluir**. Para remover a guia padrão, uma área vazia da superfície de design com o botão direito e, em seguida, clique em **remover a guia de faixa de opções**.  
  
  Você também pode adicionar guias personalizadas, grupos e controles para o Designer de faixa de opções. Você pode encontrar esses controles na **caixa de ferramentas**, no **controles de faixa de opções do Office** grupo. Há três maneiras de adicionar controles a partir de **controles de faixa de opções do Office** grupo para o Designer de faixa de opções:  
  
- Arraste um controle para uma área apropriada no Designer de faixa de opções.  
  
- Clique em um controle e, em seguida, clique em uma área apropriada no Designer de faixa de opções.  
  
- Selecione uma área apropriada no designer e, em seguida, clique duas vezes em um controle na **caixa de ferramentas**.  
  
### <a name="ribbon-design-workflow"></a>Fluxo de trabalho de design de faixa de opções  
 Siga estas etapas básicas para criar o layout de faixa de opções:  
  
1. [Adicionar uma guia personalizada à faixa de opções](#AddTabToRibbon).  
  
2. [Adicionar grupos à guia](#AddGroupsToTab).  
  
3. [Adicionar controles aos grupos](#AddControlsToGroups).  
  
   Controles podem ser ignorados somente em grupos; Você não pode arrastar um controle diretamente a uma guia ou a faixa de opções. Grupos podem ser ignorados somente em guias; Você não pode arrastar um grupo diretamente para uma faixa de opções.  
  
   Organize os controles arrastando-os para as posições corretas. Você pode definir as propriedades de um controle usando o **propriedades** janela.  
  
   Você não pode arrastar controles de uma guia para outra na faixa de opções. Se você quiser mover um controle para outra guia, você deve usar o **Recortar** comando para remover o controle de uma guia e, em seguida, cole o controle em outra guia. Se você cortar o controle e colá-lo, o manipulador de eventos para de funcionar. Você pode reconectar o manipulador de eventos de **propriedades** janela. Para obter mais informações, consulte [janela de propriedades](/visualstudio/ide/reference/properties-window).  
  
###  <a name="AddTabToRibbon"></a> Adicionar guias personalizadas à faixa de opções  
 Há três maneiras de adicionar uma guia personalizada à faixa de opções:  
  
- Adicionar uma guia entre a **caixa de ferramentas**.  
  
- O Designer de faixa de opções com o botão direito e, em seguida, clique em **guia de faixa de opções adicionar**.  
  
- Abra o **guia Editor de coleção**e, em seguida, clique em **Add**.  
  
   Para abrir o **guia Editor de coleção**, no **propriedades** janela, selecione o **guias** propriedade e, em seguida, clique no botão de reticências ![ASP.NET para dispositivos móveis Elipse de Designer](../sharepoint/media/mwellipsis.gif "elipse do Designer de dispositivo móvel do ASP.NET").  
  
  Depois de adicionar uma guia, você pode adicionar grupos para conter controles.  
  
#### <a name="remove-custom-tabs-from-the-ribbon"></a>Remover guias personalizadas da faixa de opções  
 Há três maneiras de remover uma guia personalizada na faixa de opções:  
  
-   O designer com o botão direito e, em seguida, clique em **remover a guia de faixa de opções**.  
  
-   No **comandos** painel da **propriedades** janela, clique em **remover a guia de faixa de opções**.  
  
-   Abra o **guia Editor de coleção**, selecione a guia e, em seguida, clique em **remover**.  
  
#### <a name="change-the-position-of-a-tab-on-the-ribbon"></a>Alterar a posição de uma guia na faixa de opções  
 Você pode alterar a ordem das guias personalizadas em uma faixa de opções. Você também pode posicionar guias personalizadas antes ou depois de uma guia interna na faixa de opções. Para obter mais informações, consulte [como: alterar a posição de uma guia na faixa de opções](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md).  
  
#### <a name="customize-built-in-tabs-on-the-ribbon"></a>Personalizar as guias internas da faixa de opções  
 Uma guia interna é uma guia que já está na faixa de opções de um aplicativo do Microsoft Office. Por exemplo, o **dados** guia é uma guia interna no Excel.  
  
 Você pode adicionar grupos e controles a uma guia interna. Por padrão, um grupo personalizado aparece como o último grupo em uma guia interna, embora você possa movê-lo antes ou depois de qualquer grupo interno na guia.  
  
 É possível remover grupos internos.  
  
 Para obter detalhes sobre como personalizar uma guia interna, consulte [como: personalizar uma guia interna](../vsto/how-to-customize-a-built-in-tab.md).  
  
###  <a name="AddGroupsToTab"></a> Adicionar grupos a uma guia  
 Os grupos organizam logicamente os controles na faixa de opções. Adicione grupos às guias. Adicione todos os outros controles ao grupo.  
  
###  <a name="AddControlsToGroups"></a> Adicionar controles aos grupos  
 Adicione um ou mais controles a um grupo. A tabela a seguir descreve cada controle.  
  
|Controle|Descrição|  
|-------------|-----------------|  
|**Box**|Um contêiner que organiza controles em um grupo. Você pode adicionar qualquer controle a uma caixa exceto um separador, um grupo ou uma guia. Uma caixa pode ser horizontal ou vertical.|  
|**Button**|Um botão que inicia uma ação. Você pode adicionar um botão para um grupo, um grupo de botões, uma lista suspensa, uma galeria, um menu ou um botão de divisão.|  
|**Grupo de botões**|Um grupo que contém um ou mais botões, botões de alternância, menus, botões de divisão e galerias. Você pode adicionar um grupo de botões a um grupo ou um menu.|  
|**CheckBox**|Uma caixa que é marcada ou desmarcada para ativar ou desativar uma opção.|  
|**ComboBox**|Uma caixa de edição com uma caixa de listagem anexada. Usuários podem digitar ou selecionar sua escolha. A caixa exibe a seleção atual. Use o <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.Items%2A> propriedade para adicionar e remover itens em tempo de execução antes ou depois que a faixa de opções é carregada no aplicativo do Office.|  
|**Lista suspensa**|Uma lista de itens que o usuário pode selecionar. O usuário não é possível digitar um novo item em uma lista suspensa.<br /><br /> Use o <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.Items%2A> propriedade para adicionar itens à lista. Você pode adicionar e remover itens em tempo de execução.<br /><br /> Use o <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.Buttons%2A> propriedade para adicionar botões à lista. No entanto, você não pode adicionar e remover botões em tempo de execução depois que a faixa de opções é carregada no aplicativo do Office.|  
|**Caixa de edição**|Uma caixa em que o usuário pode digitar texto.|  
|**Gallery**|Um menu que apresenta uma matriz ou grade de opções visuais da qual os usuários podem selecionar. Você pode controlar o layout das seleções no menu. Use o <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ColumnCount%2A> e o <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.RowCount%2A> propriedades para especificar o número de linhas e colunas que exibição os itens e botões de galeria.|  
|**Rótulo**|Texto que você pode usar para identificar os controles na faixa de opções.|  
|**Menu**|Uma lista suspensa que pode conter qualquer um dos seguintes controles:<br /><br /> -Botão<br />-Caixa de seleção<br />-Galeria<br />-Menu<br />-Botão de divisão<br />-Botão de alternância<br />-Separador<br /><br /> Para adicionar um controle a um menu no Designer de faixa de opções, clique na seta para baixo no menu para expor a superfície de design de menu. Em seguida, você pode arrastar controles da faixa de opções do **caixa de ferramentas** para o menu. Para organizar controles, arraste-os para as posições desejadas.<br /><br /> Para adicionar controles para o <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu> após a faixa de opções é carregada no aplicativo do Office, você deve configurar o <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.Dynamic%2A> propriedade a ser **true** antes que a faixa de opções é carregada. Para obter informações sobre como fazer isso, consulte [visão geral do modelo de objeto da faixa de opções](../vsto/ribbon-object-model-overview.md).|  
|**Separador**|Uma barra fina usada para separar itens em uma lista. Quando adicionado a um grupo, a barra é vertical. Quando adicionado a um menu, a barra é horizontal.|  
|**Botão de divisão**|Um botão com um menu anexado. Um botão de divisão pode conter qualquer um dos seguintes controles:<br /><br /> -Botão<br />-Caixa de seleção<br />-Galeria<br />-Menu<br />-Botão de divisão<br />-Botão de alternância<br />-Separador<br /><br /> Como o menu, o botão de divisão tem sua própria superfície de design. No entanto, ao contrário de um menu, só é possível atualizar os itens em um botão de divisão antes que a faixa de opções é carregada no aplicativo do Office. Para obter informações sobre como atualizar os itens em um botão de divisão, consulte [visão geral do modelo de objeto da faixa de opções](../vsto/ribbon-object-model-overview.md).|  
|**ToggleButton**|Um botão que aparece pressionado ou não pressionado.|  
  
##  <a name="HandleEventsSetProperties"></a> Tratar eventos e propriedades de configuração  
 O Designer de faixa de opções permite que você defina as propriedades de controle em tempo de design usando o **propriedades** janela. Além disso, a faixa de opções expõe um modelo de objeto com rigidez de tipos que você pode usar para obter e definir as propriedades de controles da faixa de opções em tempo de execução.  
  
 Clique duas vezes em qualquer controle no designer para abrir um manipulador de eventos para o evento padrão do controle. Você pode criar manipuladores de eventos para todos os outros eventos de controle usando o **propriedades** janela.  
  
 Propriedades e eventos da faixa de opções estão localizadas no <xref:Microsoft.Office.Tools.Ribbon> namespace. O **faixa de opções (Visual Designer)** item automaticamente adiciona uma referência a esse assembly no projeto e insere apropriado **usando** ou **importações** instrução na parte superior o faixa de opções do arquivo de código.  
  
 Para obter informações sobre a manipulação de eventos da faixa de opções e definindo as propriedades de controles da faixa de opções em tempo de execução, consulte [visão geral do modelo de objeto da faixa de opções](../vsto/ribbon-object-model-overview.md).  
  
##  <a name="CustomizingMicrosoftOfficeButton"></a> Personalizar o modo de exibição Backstage  
 Você pode usar o Designer de faixa de opções para adicionar controles ao menu que é aberta quando você clica o **arquivo** guia. Esse menu é chamado de modo de exibição Backstage.  
  
 Você não pode posicionar controles antes ou depois de controles internos usando o designer de faixa de opções. Um controle interno é um controle que já aparece no modo de exibição Backstage. Se você desejar posicionar controles antes ou depois de controles internos, você deve usar o XML da faixa de opções. Para obter mais informações sobre **da faixa de opções (XML)**, consulte [XML da faixa de opções](../vsto/ribbon-xml.md). Para obter mais informações sobre como personalizar o modo de exibição Backstage, consulte [Introdução ao modo de exibição Backstage do Office 2010 para desenvolvedores](http://go.microsoft.com/fwlink/?LinkId=182189) e [personalizar o modo de exibição Backstage do Office 2010 para desenvolvedores](http://go.microsoft.com/fwlink/?LinkId=182188).  
  
 [!INCLUDE[appliesto_ribbon_2010](../vsto/includes/appliesto-ribbon-2010-md.md)]  
  
 Para obter informações sobre como adicionar controles à exibição do Backstage, consulte [como: adicionar controles ao modo de exibição Backstage](../vsto/how-to-add-controls-to-the-backstage-view.md).  
  
##  <a name="Accessibility"></a> Acessibilidade no Designer de faixa de opções  
 Você pode usar atalhos de teclado para mover os controles no Designer de faixa de opções. Alguns atalhos de teclado se aplicam a todos os controles e alguns se aplicam somente a controles que têm menus.  
  
 Os atalhos de teclado que se aplicam a todos os controles são mostrados na tabela a seguir.  
  
|Ação|Atalho de teclado|  
|------------|-----------------------|  
|Mova um controle antes do controle anterior na lista.|**CTRL**+**backup**<br /><br /> **CTRL**+**esquerda**|  
|Mova um controle depois do próximo controle na lista.|**CTRL**+**para baixo**<br /><br /> **CTRL**+**direita**|  
|Mova a seleção de um controle para outro no mesmo grupo. Para um painel suspenso, mova entre o controle pai e os controles no painel de lista suspensa.|**Para cima**<br /><br /> **Para baixo**|  
|Itere para frente por todos os controles.|**Tab**|  
|Itere para o reverso por todos os controles.|**Shift**+**Tab**|  
|Exclua o controle selecionado ou conjunto de controles.|**Excluir**|  
|Copie os controles selecionados.|**Ctrl**+**C**|  
|Recorte os controles selecionados.|**Ctrl**+**X**|  
|Cole controles da área de transferência.|**Ctrl**+**V**|  
|Selecione o **caixa de ferramentas**.|**CTRL**+**Alt**+**X**|  
|Selecione o componente pai.|**Esc**|  
  
 Os atalhos de teclado que se aplicam somente ao Menu do Microsoft Office <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>, e <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton> são mostrados na tabela a seguir.  
  
|Ação|Atalho de teclado|  
|------------|-----------------------|  
|Se o painel de lista suspensa é aberto e não há um controle selecionado no painel de lista suspensa, selecione o controle pai.|**Esquerda**|  
|Feche o painel suspenso se o painel de lista suspensa é aberto e o controle pai estiver selecionado.|**Esquerda**|  
|Abra o painel de lista suspensa.|**Direita**|  
|Se o painel de lista suspensa é aberto, selecione o primeiro controle no painel de lista suspensa.|**Direita**|  
|Feche um painel de lista suspensa.|**Esc**|  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral da faixa de opções](../vsto/ribbon-overview.md)   
 [XML da faixa de opções](../vsto/ribbon-xml.md)   
 [Passo a passo: Criar uma guia personalizada usando o Designer de faixa de opções](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)   
 [Como: exportar uma faixa de opções do Designer da faixa de opções para o XML da faixa de opções](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)   
 [Como: Introdução à personalização da faixa de opções](../vsto/how-to-get-started-customizing-the-ribbon.md)   
 [Acesso a faixa de opções em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)  
  
  