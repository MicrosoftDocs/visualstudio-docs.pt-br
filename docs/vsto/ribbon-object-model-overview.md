---
title: Visão geral do modelo de objeto da faixa de opções
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], object model
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 25e34dcb38685a885ae0730740c25e1cb502e15c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49910583"
---
# <a name="ribbon-object-model-overview"></a>Visão geral do modelo de objeto da faixa de opções
  O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] expõe um modelo de objeto com rigidez de tipos que você pode usar para obter e definir as propriedades de controles da faixa de opções em tempo de execução. Por exemplo, dinamicamente você pode preencher os controles de menu, ou mostrar e ocultar controles contextualmente. Você também pode adicionar guias, grupos e controles à faixa de opções, mas apenas antes que o faixa de opções é carregada pelo aplicativo do Office. Para obter informações, consulte [definir as propriedades que se tornam somente leitura](#SettingReadOnlyProperties).  
  
 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]  
  
 Esse modelo de objeto da faixa de opções consiste principalmente a [classe de faixa de opções](#RibbonClass), [eventos da faixa de opções](#RibbonEvents), e [classes de controle de faixa de opções](#RibbonControlClasses).  
  
##  <a name="RibbonClass"></a> Classe de faixa de opções  
 Quando você adiciona um novo **faixa de opções (Visual Designer)** do item a um projeto, o Visual Studio adiciona uma **faixa de opções** classe ao seu projeto. O **faixa de opções** herda o <xref:Microsoft.Office.Tools.Ribbon.RibbonBase> classe.  
  
 Essa classe é exibida como uma classe parcial que é dividida entre o arquivo de código da faixa de opções e o arquivo de código do Designer de faixa de opções.  
  
##  <a name="RibbonEvents"></a> Eventos da faixa de opções  
 O **faixa de opções** classe contém os seguintes três eventos:  
  
|evento|Descrição|  
|-----------|-----------------|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.Load>|Gerado quando o aplicativo do Office carrega a personalização da faixa de opções. O <xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.Load> manipulador de eventos é adicionado automaticamente ao arquivo de código da faixa de opções. Use esse manipulador de eventos para executar código personalizado quando a faixa de opções for carregada.|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.LoadImage>|Permite que você às imagens de cache na personalização da faixa de opções quando a faixa de opções for carregada. Se você escrever código para armazenar em cache as imagens de faixa de opções no manipulador de eventos, você pode obter um ganho de desempenho. Para obter mais informações, consulte <xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.LoadImage>.|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.Close>|Gerado quando a instância de faixa de opções é fechada.|  
  
##  <a name="RibbonControlClasses"></a> Controles da faixa de opções  
 O <xref:Microsoft.Office.Tools.Ribbon> namespace contém um tipo para cada controle que você vê o **controles de faixa de opções do Office** grupo do **caixa de ferramentas**.  
  
 A tabela a seguir mostra o tipo para cada `Ribbon` controle. Para obter uma descrição de cada controle, consulte [visão geral da faixa de opções](../vsto/ribbon-overview.md).  
  
|Nome do controle|Nome da classe|  
|------------------|----------------|  
|**Box**|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>|  
|**Button**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton>|  
|**Grupo de botões**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButtonGroup>|  
|**CheckBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox>|  
|**ComboBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>|  
|**Lista suspensa**|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>|  
|**Caixa de edição**|<xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|  
|**Gallery**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|  
|**Grupo**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|  
|**Rótulo**|<xref:Microsoft.Office.Tools.Ribbon.RibbonLabel>|  
|**Menu**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|  
|**Separador**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|  
|**Botão de divisão**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|  
|**Tab**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|  
|**ToggleButton**|<xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|  
  
 O <xref:Microsoft.Office.Tools.Ribbon> namespace usa o prefixo "Ribbon" para esses tipos para evitar uma colisão de nomes com os nomes das classes de controle no <xref:System.Windows.Forms> namespace.  
  
 Quando você adiciona um controle para o Designer de faixa de opções, o Designer de faixa de opções declara a classe para o controle como um campo no arquivo de código do Designer de faixa de opções.  
  
### <a name="common-tasks-using-the-properties-of-ribbon-controls"></a>Tarefas comuns usando as propriedades de controles da faixa de opções  
 Cada `Ribbon` controle contém propriedades que você pode usar para realizar diversas tarefas, como atribuir um rótulo a um controle, ou ocultando e mostrando controles.  
  
 Em alguns casos, as propriedades se tornar somente leitura após as cargas de faixa de opções ou após um controle é adicionado a um menu dinâmico. Para obter mais informações, consulte [definir as propriedades que se tornam somente leitura](#SettingReadOnlyProperties).  
  
 A tabela a seguir descreve algumas das tarefas que você pode executar usando `Ribbon` propriedades do controle.  
  
|Para essa tarefa:|Faça o seguinte:|  
|--------------------|--------------|  
|Ocultar ou mostrar um controle.|Use a propriedade Visible.|  
|Habilitar ou desabilitar um controle.|Use a propriedade Enabled.|  
|Defina o tamanho de um controle.|Use a propriedade ControlSize.|  
|Obter a imagem que aparece em um controle.|Use a propriedade de imagem.|  
|Altere o rótulo de um controle.|Use a propriedade do rótulo.|  
|Adicione dados definidos pelo usuário a um controle.|Use a propriedade Tag.|  
|Obter os itens uma <xref:Microsoft.Office.Tools.Ribbon.RibbonBox>, <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>, <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>, ou<br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton> controle.|Use a propriedade de itens.|  
|Adicionar itens a um <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>, <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>, ou <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> controle.|Use a propriedade de itens.|  
|Adicionar controles a um <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>.|Use a propriedade de itens.<br /><br /> Para adicionar controles para o <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu> após a faixa de opções é carregada no aplicativo do Office, você deve configurar o <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.Dynamic%2A> propriedade a ser **verdadeiro** antes que a faixa de opções é carregada no aplicativo do Office. Para obter informações, consulte [definir as propriedades que se tornam somente leitura](#SettingReadOnlyProperties).|  
|Obter o item selecionado de um <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>,<br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>, ou <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>.|Use a propriedade SelectedItem. Para um <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>, use o <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.Text%2A> propriedade.|  
|Obter os grupos um <xref:Microsoft.Office.Tools.Ribbon.RibbonTab>.|Use a propriedade <xref:Microsoft.Office.Tools.Ribbon.RibbonTab.Groups%2A>.|  
|Especifique o número de linhas e colunas que aparecem em um <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>.|Use o <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.RowCount%2A> e <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ColumnCount%2A> propriedades.|  
  
##  <a name="SettingReadOnlyProperties"></a> Definir propriedades que se tornam somente leitura  
 Algumas propriedades só podem ser definidas antes de carrega a faixa de opções. Há três locais para definir essas propriedades:  
  
- No Visual Studio **propriedades** janela.  
  
- No construtor do **faixa de opções** classe.  
  
- No `CreateRibbonExtensibilityObject` método da `ThisAddin`, `ThisWorkbook`, ou `ThisDocument` classe do seu projeto.  
  
  Menus dinâmicos fornecem algumas exceções. Você pode criar novos controles, defina suas propriedades e, em seguida, adicioná-los a um menu dinâmico no tempo de execução, mesmo depois que a fita que contém o menu é carregada.  
  
  Propriedades de controles que você adicionar a um menu dinâmico podem ser definidas a qualquer momento.  
  
  Para obter mais informações, consulte [propriedades que se tornam somente leitura](#ReadOnlyProperties).  
  
### <a name="set-properties-in-the-constructor-of-the-ribbon"></a>Definir propriedades no construtor da faixa de opções  
 Você pode definir as propriedades de um `Ribbon` controle no construtor do **faixa de opções** classe. Esse código deve aparecer após a chamada para o `InitializeComponent` método. O exemplo a seguir adiciona um novo botão a um grupo, se a hora atual for 17:00 hora do Pacífico (UTC-8) ou posterior.  
  
 Adicione o código a seguir.  
  
 [!code-csharp[Trin_Ribbon_ObjectModel#1](../vsto/codesnippet/CSharp/trin_Ribbon_objectmodel_dotnet4/Ribbon1.Designer.cs#1)]
 [!code-vb[Trin_Ribbon_ObjectModel#1](../vsto/codesnippet/VisualBasic/trin_Ribbon_objectmodel_dotnet4/Ribbon1.Designer.vb#1)]  
  
 Em projetos Visual c# que foi atualizado do Visual Studio 2008, o construtor aparece no arquivo de código da faixa de opções.  
  
 Em projetos do Visual Basic ou em projetos do Visual c# que você criou no [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)], o construtor é exibido no arquivo de código do Designer de faixa de opções. Esse arquivo é denominado *YourRibbonItem*. Designer.cs ou *YourRibbonItem*. VB. Para ver esse arquivo em projetos do Visual Basic, primeiro você deve clicar o **Show All Files** botão no Gerenciador de soluções.  
  
### <a name="set-properties-in-the-createribbonextensibilityobject-method"></a>Definir propriedades no método CreateRibbonExtensibilityObject  
 Você pode definir as propriedades de um `Ribbon` controlar quando você substitui o `CreateRibbonExtensibilityObject` método na `ThisAddin`, `ThisWorkbook`, ou `ThisDocument` classe do seu projeto. Para obter mais informações sobre o `CreateRibbonExtensibilityObject` método, consulte [visão geral da faixa de opções](../vsto/ribbon-overview.md).  
  
 O exemplo a seguir define as propriedades de faixa de opções na `CreateRibbonExtensibilityObject` método da `ThisWorkbook` classe de um projeto de pasta de trabalho do Excel.  
  
 Adicione o código a seguir.  
  
 [!code-vb[Trin_Ribbon_ObjectModel#2](../vsto/codesnippet/VisualBasic/trin_Ribbon_objectmodel_dotnet4/ThisWorkbook.vb#2)]
 [!code-csharp[Trin_Ribbon_ObjectModel#2](../vsto/codesnippet/CSharp/trin_Ribbon_objectmodel_dotnet4/ThisWorkbook.cs#2)]  
  
###  <a name="ReadOnlyProperties"></a> Propriedades que se tornam somente leitura  
 A tabela a seguir mostra as propriedades que podem ser definidas somente antes de carrega a faixa de opções.  
  
> [!NOTE]  
>  Você pode definir as propriedades de controles em menus dinâmicos a qualquer momento. Nesse caso, não se aplicam a essa tabela.  
  
|Propriedade|Classe de controle de faixa de opções|  
|--------------|--------------------------|  
|**Style**|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>|  
|**ButtonType**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|  
|**ColumnCount**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|  
|**ControlId**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|  
|**DialogLauncher**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|  
|**dinâmico**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|  
|**Global**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|  
|**Grupos**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|  
|**ImageName**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDialogLauncher><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|  
|**ItemSize**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|  
|**MaxLength**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|  
|**Nome**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComponent>|  
|**posição**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGroup><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonTab><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|  
|**RibbonType**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|  
|**Número de linhas**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|  
|**ShowItemImage**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|  
|**ShowItemLabel**|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|  
|**ShowItemSelection**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|  
|**SizeString**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|  
|**StartFromScratch**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|  
|**Guias**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|  
|**Título**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|  
  
### <a name="set-properties-for-ribbons-that-appear-in-outlook-inspectors"></a>Definir propriedades para faixas de opções que aparecem nos inspetores do Outlook  
 Uma nova instância da faixa de opções é criada sempre que um usuário abre um Inspetor em que a faixa de opções é exibida. No entanto, você pode definir as propriedades listadas na tabela acima, antes da primeira instância da faixa de opções é criada. Após a primeira instância é criada, essas propriedades se tornar somente leitura, como a primeira instância define o arquivo XML que usa o Outlook para carregar a faixa de opções.  
  
 Se você tiver a lógica condicional que define qualquer uma dessas propriedades para um valor diferente de quando outras instâncias da faixa de opções são criadas, esse código não terá nenhum efeito.  
  
> [!NOTE]  
>  Certifique-se de que o **nome** propriedade é definida para cada controle que você adicionar a uma faixa de opções do Outlook. Se você adicionar um controle a uma faixa de opções do Outlook no tempo de execução, você deve definir essa propriedade em seu código. Se você adicionar um controle a uma faixa de opções do Outlook no tempo de design, a propriedade Name é definida automaticamente.  
  
## <a name="ribbon-control-events"></a>Eventos de controle de faixa de opções  
 Cada classe de controle contém um ou mais eventos. A tabela a seguir descreve esses eventos.  
  
|evento|Descrição|  
|-----------|-----------------|  
|Clique em|Ocorre quando um controle é clicado.|  
|TextChanged|Ocorre quando o texto de uma caixa de combinação ou caixa de edição é alterado.|  
|ItemsLoading|Ocorre quando a coleção de itens do controle é solicitada pelo Office. Office armazena em cache a coleção de itens até que seu código altera as propriedades do controle ou chamar o <xref:Microsoft.Office.Core.IRibbonUI.InvalidateControl%2A> método.|  
|ButtonClick|Ocorre quando um botão em um <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> ou <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> é clicado.|  
|SelectionChanged|Ocorre quando a seleção em um <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> ou <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> alterações.|  
|DialogLauncherClick|Ocorre quando o ícone de inicializador de caixa de diálogo no canto inferior direito de um grupo é clicado.|  
  
 Os manipuladores de eventos para esses eventos têm dois parâmetros a seguir.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*Remetente*|Um <xref:System.Object> que representa o controle que acionou o evento.|  
|*e*|Um <xref:Microsoft.Office.Tools.Ribbon.RibbonControlEventArgs> que contém um <xref:Microsoft.Office.Core.IRibbonControl>. Use este controle para acessar qualquer propriedade que não está disponível no modelo de objeto da faixa de opções fornecido pelo [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)].|  
  
## <a name="see-also"></a>Consulte também  
 [Acesso a faixa de opções em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)   
 [Visão geral da faixa de opções](../vsto/ribbon-overview.md)   
 [Como: Introdução à personalização da faixa de opções](../vsto/how-to-get-started-customizing-the-ribbon.md)   
 [Designer de faixa de opções](../vsto/ribbon-designer.md)   
 [Passo a passo: Criar uma guia personalizada usando o Designer de faixa de opções](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)   
 [Explicação passo a passo: Os controles em uma faixa de opções em tempo de execução de atualização](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)   
 [Personalizar uma faixa de opções do Outlook](../vsto/customizing-a-ribbon-for-outlook.md)   
 [Como: personalizar uma guia interna](../vsto/how-to-customize-a-built-in-tab.md)   
 [Como: adicionar controles ao modo de exibição Backstage](../vsto/how-to-add-controls-to-the-backstage-view.md)   
 [Como: exportar uma faixa de opções do Designer da faixa de opções para o XML da faixa de opções](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)   
 [Como: Add-in de mostrar erros de interface do usuário](../vsto/how-to-show-add-in-user-interface-errors.md)  
 