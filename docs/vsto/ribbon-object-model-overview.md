---
title: Visão geral do modelo de objeto Ribbon
description: Saiba como a Ferramentas do Visual Studio para o tempo de execução do Office expõe um modelo de objeto fortemente tipado que você pode usar para obter e definir as propriedades dos controles da faixa de tipos em tempo de execução.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], object model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f053e87f8cdfd2bdf87bbdf4b7d115f6d9bbec26
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107823984"
---
# <a name="ribbon-object-model-overview"></a>Visão geral do modelo de objeto Ribbon
  O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] expõe um modelo de objeto fortemente tipado que você pode usar para obter e definir as propriedades dos controles da faixa de tipos em tempo de execução. Por exemplo, você pode preencher dinamicamente controles de menu ou mostrar e ocultar os controles de forma contextual. Você também pode adicionar guias, grupos e controles a uma faixa de faixas, mas somente antes de a faixa de faixas ser carregada pelo aplicativo do Office. Para obter informações, consulte [definir propriedades que se tornam somente leitura](#SettingReadOnlyProperties).

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

 Esse modelo de objeto Ribbon consiste principalmente na [classe Ribbon](#RibbonClass), nos [eventos da faixa](#RibbonEvents)de forma e nas [classes de controle da faixa](#RibbonControlClasses)de forma.

## <a name="ribbon-class"></a><a name="RibbonClass"></a> Classe da faixa de Ribbon
 Quando você adiciona um novo item **da faixa de visualização (Visual Designer)** a um projeto, o Visual Studio adiciona uma classe de **faixa** de uma à sua projeto. A classe **Ribbon** herda da <xref:Microsoft.Office.Tools.Ribbon.RibbonBase> classe.

 Essa classe aparece como uma classe parcial que é dividida entre o arquivo de código da faixa de Ribbon e o arquivo de código do designer de faixa de Ribbon.

## <a name="ribbon-events"></a><a name="RibbonEvents"></a> Eventos da faixa de das
 A classe **da faixa** de opções contém os três eventos a seguir:

|Evento|Descrição|
|-----------|-----------------|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.Load>|Gerado quando o aplicativo do Office carrega a personalização da faixa de uma. O <xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.Load> manipulador de eventos é adicionado automaticamente ao arquivo de código da faixa de Ribbon. Use esse manipulador de eventos para executar código personalizado quando a faixa de faixas for carregada.|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.LoadImage>|Permite armazenar imagens em cache na personalização da faixa de forma quando a faixa de faixas é carregada. Você pode obter um pequeno lucro de desempenho se você escrever código para armazenar em cache as imagens da faixa de faixas nesse manipulador de eventos. Para obter mais informações, consulte <xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.LoadImage>.|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.Close>|Gerado quando a instância da faixa de Ribbon é fechada.|

## <a name="ribbon-controls"></a><a name="RibbonControlClasses"></a> Controles da faixa de faixas
 O <xref:Microsoft.Office.Tools.Ribbon> namespace contém um tipo para cada controle que você vê no grupo de **controles da faixa** de da Office da caixa de **ferramentas**.

 A tabela a seguir mostra o tipo de cada `Ribbon` controle. Para obter uma descrição de cada controle, consulte [visão geral da faixa](../vsto/ribbon-overview.md)de visualização.

|Nome do controle|Nome da classe|
|------------------|----------------|
|**Box**|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>|
|**Botão**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton>|
|**ButtonGroup**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButtonGroup>|
|**CheckBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox>|
|**ComboBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>|
|**Suspenso**|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>|
|**Edição**|<xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**Clip**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**Grupo**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|
|**Rótulo**|<xref:Microsoft.Office.Tools.Ribbon.RibbonLabel>|
|**Menu**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|
|**Separador**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|
|**SplitButton**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|**Tab**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**ToggleButton**|<xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|

 O <xref:Microsoft.Office.Tools.Ribbon> namespace usa o prefixo "Ribbon" para esses tipos para evitar uma colisão de nome com os nomes de classes de controle no <xref:System.Windows.Forms> namespace.

 Quando você adiciona um controle ao designer de faixa de faixas, o designer de faixa de faixas declara a classe desse controle como um campo no arquivo de código do designer de faixa de das.

### <a name="common-tasks-using-the-properties-of-ribbon-controls"></a>Tarefas comuns usando as propriedades de controles da faixa de faixas
 Cada `Ribbon` controle contém propriedades que você pode usar para executar várias tarefas, como atribuir um rótulo a um controle ou ocultar e mostrar controles.

 Em alguns casos, as propriedades tornam-se somente leitura depois que a faixa de faixas é carregada ou depois que um controle é adicionado a um menu dinâmico. Para obter mais informações, consulte [definir propriedades que se tornam somente leitura](#SettingReadOnlyProperties).

 A tabela a seguir descreve algumas das tarefas que você pode executar usando `Ribbon` as propriedades de controle.

|Para esta tarefa:|Faça o seguinte:|
|--------------------|--------------|
|Ocultar ou mostrar um controle.|Use a propriedade Visible.|
|Habilitar ou desabilitar um controle.|Use a propriedade Enabled.|
|Definir o tamanho de um controle.|Use a Propriedade ControlSize.|
|Obter a imagem que aparece em um controle.|Use a propriedade Image.|
|Alterar o rótulo de um controle.|Use a propriedade Label.|
|Adicionar dados definidos pelo usuário a um controle.|Use a propriedade Tag.|
|Obter os itens em um <xref:Microsoft.Office.Tools.Ribbon.RibbonBox> , <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> , <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> ou<br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton> controlo.|Use a propriedade Items.|
|Adicionar itens a um <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> controle, ou <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> .|Use a propriedade Items.|
|Adicione controles a um <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu> .|Use a propriedade Items.<br /><br /> Para adicionar controles ao <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu> depois que a faixa de faixas é carregada no aplicativo do Office, você deve definir a <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.Dynamic%2A> propriedade como **true** antes que a faixa de faixas seja carregada no aplicativo do Office. Para obter informações, consulte [definir propriedades que se tornam somente leitura](#SettingReadOnlyProperties).|
|Obter o item selecionado de um <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox> ,<br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>, ou <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> .|Use a propriedade SelectedItem. Para um <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox> , use a <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.Text%2A> propriedade.|
|Obtenha os grupos em um <xref:Microsoft.Office.Tools.Ribbon.RibbonTab> .|Use a propriedade <xref:Microsoft.Office.Tools.Ribbon.RibbonTab.Groups%2A>.|
|Especifique o número de linhas e colunas que aparecem em um <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> .|Use as <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.RowCount%2A> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ColumnCount%2A> Propriedades e.|

## <a name="set-properties-that-become-read-only"></a><a name="SettingReadOnlyProperties"></a> Definir propriedades que se tornam somente leitura
 Algumas propriedades só podem ser definidas antes que a faixa de faixas seja carregada. Há três locais para definir essas propriedades:

- Na janela **Propriedades** do Visual Studio.

- No construtor da classe **Ribbon** .

- No `CreateRibbonExtensibilityObject` método da `ThisAddin` `ThisWorkbook` classe, ou `ThisDocument` do seu projeto.

  Os menus dinâmicos fornecem algumas exceções. Você pode criar novos controles, definir suas propriedades e, em seguida, adicioná-los a um menu dinâmico em tempo de execução, mesmo depois que a faixa de faixas que contém o menu for carregada.

  As propriedades de controles que você adiciona a um menu dinâmico podem ser definidas a qualquer momento.

  Para obter mais informações, consulte [Propriedades que se tornam somente leitura](#ReadOnlyProperties).

### <a name="set-properties-in-the-constructor-of-the-ribbon"></a>Definir propriedades no construtor da faixa de faixas
 Você pode definir as propriedades de um `Ribbon` controle no construtor da classe **Ribbon** . Esse código deve aparecer após a chamada para o `InitializeComponent` método. O exemplo a seguir adiciona um novo botão a um grupo se a hora atual for 17:00 hora do Pacífico (UTC-8) ou posterior.

 Adicione o código seguinte:

 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_Ribbon_objectmodel_dotnet4/Ribbon1.Designer.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_Ribbon_objectmodel_dotnet4/Ribbon1.Designer.vb" id="Snippet1":::

 Em projetos do Visual C# que você atualizou do Visual Studio 2008, o Construtor aparece no arquivo de código da faixa de medida.

 Em projetos Visual Basic ou em projetos do Visual C# que você criou no [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] , o Construtor aparece no arquivo de código do designer de faixa de Ribbon. Esse arquivo é denominado *YourRibbonItem*. Designer. cs ou *YourRibbonItem*. Designer. vb. Para ver esse arquivo em projetos Visual Basic, primeiro você deve clicar no botão **Mostrar todos os arquivos** em Gerenciador de soluções.

### <a name="set-properties-in-the-createribbonextensibilityobject-method"></a>Definir propriedades no método CreateRibbonExtensibilityObject
 Você pode definir as propriedades de um `Ribbon` controle ao substituir o `CreateRibbonExtensibilityObject` método na `ThisAddin` `ThisWorkbook` classe, ou `ThisDocument` do seu projeto. Para obter mais informações sobre o `CreateRibbonExtensibilityObject` método, consulte [visão geral da faixa](../vsto/ribbon-overview.md)de visualização.

 O exemplo a seguir define as propriedades da faixa de opções no `CreateRibbonExtensibilityObject` método da `ThisWorkbook` classe de um projeto de pasta de trabalho do Excel.

 Adicione o código seguinte:

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_Ribbon_objectmodel_dotnet4/ThisWorkbook.vb" id="Snippet2":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_Ribbon_objectmodel_dotnet4/ThisWorkbook.cs" id="Snippet2":::

### <a name="properties-that-become-read-only"></a><a name="ReadOnlyProperties"></a> Propriedades que se tornam somente leitura
 A tabela a seguir mostra as propriedades que só podem ser definidas antes que a faixa de opções seja carregada.

> [!NOTE]
> Você pode definir as propriedades de controles em menus dinâmicos a qualquer momento. Esta tabela não se aplica nesse caso.

|Propriedade|Classe de controle da faixa de Ribbon|
|--------------|--------------------------|
|**BoxStyle**|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>|
|**ButtonType**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|**ColumnCount**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ControlId**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**DialogLauncher**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|
|**Dinâmico**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|
|**Global**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**Grupos**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**ImageName**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDialogLauncher><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|
|**ItemSize**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|**MaxLength**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**Nome**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComponent>|
|**Posição**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGroup><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonTab><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|
|**RibbonType**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**Linhas**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemImage**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemLabel**|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemSelection**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**Tamanho da**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**StartFromScratch**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**Guias**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**Título**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|

### <a name="set-properties-for-ribbons-that-appear-in-outlook-inspectors"></a>Definir propriedades para faixas de as que aparecem nos inspetores do Outlook
 Uma nova instância da faixa de faixas é criada cada vez que um usuário abre um inspetor no qual a faixa de faixas é exibida. No entanto, você pode definir as propriedades listadas na tabela acima somente antes que a primeira instância da faixa de opções seja criada. Depois que a primeira instância é criada, essas propriedades tornam-se somente leitura porque a primeira instância define o arquivo XML que o Outlook usa para carregar a faixa de uma.

 Se você tiver uma lógica condicional que defina qualquer uma dessas propriedades para um valor diferente quando outras instâncias da faixa de tipos forem criadas, esse código não terá nenhum efeito.

> [!NOTE]
> Verifique se a propriedade **Name** está definida para cada controle que você adicionar a uma faixa de faixas do Outlook. Se você adicionar um controle a uma faixa de faixas do Outlook em tempo de execução, deverá definir essa propriedade em seu código. Se você adicionar um controle a uma faixa de faixas do Outlook em tempo de design, a propriedade Name será definida automaticamente.

## <a name="ribbon-control-events"></a>Eventos de controle da faixa de Ribbon
 Cada classe de controle contém um ou mais eventos. A tabela a seguir descreve esses eventos.

|Evento|Descrição|
|-----------|-----------------|
|Clique|Ocorre quando um controle é clicado.|
|TextChanged|Ocorre quando o texto de uma caixa de edição ou caixa de combinação é alterado.|
|ItemsLoading|Ocorre quando a coleção Items do controle é solicitada pelo Office. O Office armazena em cache a coleção de itens até que seu código altere as propriedades do controle ou chame o <xref:Microsoft.Office.Core.IRibbonUI.InvalidateControl%2A> método.|
|ButtonClick|Ocorre quando um botão em um <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> ou <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> é clicado.|
|SelectionChanged|Ocorre quando a seleção é feita em uma <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> ou é <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> alterada.|
|DialogLauncherClick|Ocorre quando o ícone do inicializador de diálogo é clicado no canto inferior direito de um grupo.|

 Os manipuladores de eventos para esses eventos têm os dois parâmetros a seguir.

|Parâmetro|Descrição|
|---------------|-----------------|
|*Sender*|Um <xref:System.Object> que representa o controle que disparou o evento.|
|*Oriental*|Um <xref:Microsoft.Office.Tools.Ribbon.RibbonControlEventArgs> que contém um <xref:Microsoft.Office.Core.IRibbonControl> . Use este controle para acessar qualquer propriedade que não esteja disponível no modelo de objeto da faixa de forma fornecido pelo [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] .|

## <a name="see-also"></a>Consulte também
- [Acessar a faixa de faixas em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)
- [Visão geral da faixa de faixas](../vsto/ribbon-overview.md)
- [Como: começar a personalizar a faixa de faixas](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [Designer da faixa de opções](../vsto/ribbon-designer.md)
- [Walkthrough: criar uma guia personalizada usando o designer de faixa de faixas](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [Walkthrough: atualizar os controles em uma faixa de faixas em tempo de execução](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)
- [Personalizar uma faixa de faixas para o Outlook](../vsto/customizing-a-ribbon-for-outlook.md)
- [Como: personalizar uma guia interna](../vsto/how-to-customize-a-built-in-tab.md)
- [Como: adicionar controles ao modo de exibição de Backstage](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [Como exportar uma faixa de faixas do designer de faixa de das faixas para XML da faixa de modo](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [Como mostrar erros de interface do usuário do suplemento](../vsto/how-to-show-add-in-user-interface-errors.md)
