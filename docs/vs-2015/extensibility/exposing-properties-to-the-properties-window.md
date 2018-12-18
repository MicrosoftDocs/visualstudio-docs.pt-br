---
title: Expondo propriedades na janela Propriedades | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- properties [Visual Studio SDK], exposing in Property Browser
- properties [Visual Studio SDK]
- Property Browser, exposing properties
ms.assetid: 47f295b5-1ca5-4e7b-bb52-7b926b136622
caps.latest.revision: 37
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 026e7de7d56cb907682be52db2dbd32782822d9f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51756903"
---
# <a name="exposing-properties-to-the-properties-window"></a>Expondo propriedades na janela Propriedades
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo expõe as propriedades públicas de um objeto para o **propriedades** janela. As alterações feitas a essas propriedades são refletidas na **propriedades** janela.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="exposing-properties-to-the-properties-window"></a>Expondo propriedades na janela Propriedades  
 Nesta seção, você cria uma janela de ferramenta personalizada e exibir as propriedades públicas do objeto no painel janela associada a **propriedades** janela.  
  
#### <a name="to-expose-properties-to-the-properties-window"></a>Para expor propriedades à janela de propriedades  
  
1.  Cada extensão do Visual Studio inicia com um projeto de implantação do VSIX que conterá os ativos de extensão. Criar uma [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto do VSIX chamado `MyObjectPropertiesExtension`. Você pode encontrar o modelo de projeto VSIX na **novo projeto** diálogo sob **Visual c# / extensibilidade**.  
  
2.  Adicionar uma janela de ferramentas, adicionando um modelo de item da janela de ferramenta personalizada denominado `MyToolWindow`. No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **Add / Novo Item**. No **caixa de diálogo Adicionar Novo Item**, acesse **itens do Visual c# / extensibilidade** e selecione **janela de ferramenta personalizada**. No **nome** campo na parte inferior da caixa de diálogo, altere o nome de arquivo para `MyToolWindow.cs`. Para obter mais informações sobre como criar uma janela de ferramentas personalizada, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).  
  
3.  Abra MyToolWindow.cs e adicione a seguinte instrução using:  
  
    ```  
    using System.Collections;  
    using System.ComponentModel;  
    using Microsoft.VisualStudio.Shell.Interop;  
    ```  
  
4.  Agora, adicione os campos a seguir para o `MyToolWindow` classe.  
  
    ```csharp  
    private ITrackSelection trackSel;  
    private SelectionContainer selContainer;  
  
    ```  
  
5.  Adicione o seguinte código à classe MyToolWindow.  
  
    ```csharp  
    private ITrackSelection TrackSelection  
    {  
        get  
        {  
            if (trackSel == null)  
                trackSel =  
                   GetService(typeof(STrackSelection)) as ITrackSelection;  
            return trackSel;  
        }  
    }  
  
    public void UpdateSelection()  
    {  
        ITrackSelection track = TrackSelection;  
        if (track != null)  
            track.OnSelectChange((ISelectionContainer)selContainer);  
    }  
  
    public void SelectList(ArrayList list)  
    {  
        selContainer = new SelectionContainer(true, false);  
        selContainer.SelectableObjects = list;  
        selContainer.SelectedObjects = list;  
        UpdateSelection();  
    }  
  
    public override void OnToolWindowCreated()  
    {  
        ArrayList listObjects = new ArrayList();  
        listObjects.Add(this);  
        SelectList(listObjects);  
    }  
    ```  
  
     O `TrackSelection` usos de propriedade `GetService` para obter uma `STrackSelection` serviço, que fornece um <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> interface. O `OnToolWindowCreated` manipulador de eventos e `SelectList` método juntos, criam uma lista de objetos selecionados que contém somente o ferramenta Painel objeto de janela em si. O `UpdateSelection` método informa o **propriedades** janela para exibir as propriedades públicas do painel de janela de ferramentas.  
  
6.  Compile o projeto e comece a depuração. A instância experimental do Visual Studio deve aparecer.  
  
7.  Se o **propriedades** janela não estiver visível, abra-o pressionando F4.  
  
8.  Abra o **MyToolWindow** janela. Você pode encontrá-lo no **exibição / Other Windows**.  
  
     A janela é aberta e as propriedades públicas do painel da janela aparecem na **propriedades** janela.  
  
9. Alterar o **legenda** propriedade no **propriedades** janela para **propriedades do meu objeto**.  
  
     A legenda da janela MyToolWindow muda de acordo.  
  
## <a name="exposing-tool-window-properties"></a>Expondo propriedades da janela de ferramenta  
 Nesta seção, você adiciona uma janela de ferramentas e expor suas propriedades. As alterações feitas às propriedades são refletidas na **propriedades** janela.  
  
#### <a name="to-expose-tool-window-properties"></a>Para expor as propriedades da janela de ferramenta  
  
1.  Abra MyToolWindow.cs e adicione a propriedade booliana pública IsChecked à classe MyToolWindow.  
  
    ```csharp  
    [Category("My Properties")]  
    [Description("MyToolWindowControl properties")]  
    public bool IsChecked  
    {  
        get {  
            if (base.Content == null)  return false;  
            return (bool)(( MyToolWindowControl) base.Content).checkBox.IsChecked;   
        }  
        set {  
            ((MyToolWindowControl) base.Content).checkBox.IsChecked = value;  
        }  
    }  
    ```  
  
     Essa propriedade obtém seu estado da caixa de seleção WPF, que você aprenderá a criar mais tarde.  
  
2.  Abra MyToolWindowControl.xaml.cs e substitua o construtor MyToolWindowControl com o código a seguir.  
  
    ```vb  
    private MyToolWindow pane;  
    public MyToolWindowControl(MyToolWindow pane)  
    {  
        InitializeComponent();  
        this.pane = pane;  
        checkBox.IsChecked = false;  
    }  
    ```  
  
     Isso proporciona `MyToolWindowControl` de acesso para o `MyToolWindow` painel.  
  
3.  No MyToolWindow.cs, altere o `MyToolWindow` construtor da seguinte maneira:  
  
    ```csharp  
    base.Content = new MyToolWindowControl(this);  
    ```  
  
4.  Altere para o modo de design de MyToolWindowControl.  
  
5.  Exclua o botão e adicione uma caixa de seleção do **caixa de ferramentas** para o canto superior esquerdo.  
  
6.  Adicione os eventos verificado e não verificado. Selecione a caixa de seleção na exibição de design. No **propriedades** janela, clique no botão de manipuladores de eventos (na parte superior direita do **propriedades** janela). Encontrar **Checked** e digite **checkbox_Checked** na caixa de texto, em seguida, localize **desmarcado** e digite **checkbox_Unchecked** na caixa de texto.  
  
7.  Adicione os manipuladores de eventos de caixa de seleção:  
  
    ```csharp  
    private void checkbox_Checked(object sender, RoutedEventArgs e)  
    {  
        pane.IsChecked = true;  
        pane.UpdateSelection();  
    }  
    private void checkbox_Unchecked(object sender, RoutedEventArgs e)  
    {  
        pane.IsChecked = false;  
        pane.UpdateSelection();  
    }  
    ```  
  
8.  Compile o projeto e comece a depuração.  
  
9. Na instância experimental, abra o **MyToolWindow** janela.  
  
     Procurar propriedades da janela na **propriedades** janela. O **IsChecked** propriedade aparece na parte inferior da janela, sob o **propriedades do meu** categoria.  
  
10. A caixa de seleção fazer check-in a **MyToolWindow** janela. **IsChecked** no **Properties** janela é alterado para **True**. Desmarque a caixa de seleção de **MyToolWindow** janela. **IsChecked** no **Properties** janela é alterado para **False**. Altere o valor de **IsChecked** na **propriedades** janela. A caixa de seleção de **MyToolWindow** alterações de janela para coincidir com o novo valor.  
  
    > [!NOTE]
    >  Se você deve descartar um objeto que é exibido na **propriedades** janela, chame `OnSelectChange` com um `null` contêiner de seleção primeiro. Depois de descartar a propriedade ou o objeto, você pode alterar para um contêiner de seleção que atualizou <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectableObjects%2A> e <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectedObjects%2A> lista.  
  
## <a name="changing-selection-lists"></a>Alterar listas de seleção  
 Nesta seção, você adiciona uma lista de seleção para uma classe de propriedade básico e usa a interface de janela de ferramenta para escolher em qual lista de seleção para exibir.  
  
#### <a name="to-change-selection-lists"></a>Para alterar a seleção de lista  
  
1.  Abra MyToolWindow.cs e adicione uma classe pública denominada `Simple`.  
  
    ```csharp  
    public class Simple  
    {  
        private string someText = "";  
  
        [Category("My Properties")]  
        [Description("Simple Properties")]  
        [DisplayName("My Text")]  
        public string SomeText  
        {  
            get { return someText; }  
            set { someText = value; }  
        }  
  
        [Category("My Properties")]  
        [Description("Read-only property")]  
        public bool ReadOnly  
        {  
            get { return false; }  
        }  
    }  
    ```  
  
2.  Adicionar uma propriedade de SimpleObject para a classe MyToolWindow, além de dois métodos para alternar a **propriedades** seleção de janela entre o painel da janela e o `Simple` objeto.  
  
    ```csharp  
    private Simple simpleObject = null;  
    public Simple SimpleObject  
    {  
        get  
        {  
            if (simpleObject == null) simpleObject = new Simple();  
            return simpleObject;  
        }  
    }  
  
    public void SelectSimpleList()  
    {  
        ArrayList listObjects = new ArrayList();  
        listObjects.Add(SimpleObject);  
        SelectList(listObjects);  
    }  
  
    public void SelectThisList()  
    {  
        ArrayList listObjects = new ArrayList();  
        listObjects.Add(this);  
        SelectList(listObjects);  
    }  
    ```  
  
3.  No MyToolWindowControl.cs, substitua os manipuladores de caixa de seleção com estas linhas de código:  
  
    ```csharp  
    private void checkbox_Checked(object sender, RoutedEventArgs e)  
     {  
        pane.IsChecked = true;  
        pane.SelectSimpleList();  
        pane.UpdateSelection();  
    }  
    private void checkbox_Unchecked(object sender, RoutedEventArgs e)  
    {  
        pane.IsChecked = false;  
        pane.SelectThisList();  
        pane.UpdateSelection();  
    }  
    ```  
  
4.  Compile o projeto e comece a depuração.  
  
5.  Na instância experimental, abra o **MyToolWindow** janela.  
  
6.  Selecione a caixa de seleção de **MyToolWindow** janela. O **propriedades** janela exibe o `Simple` propriedades do objeto **SomeText** e **ReadOnly**. Desmarque a caixa de seleção. As propriedades públicas da janela aparecem na **propriedades** janela.  
  
    > [!NOTE]
    >  O nome de exibição **SomeText** é **meu texto**.  
  
## <a name="best-practice"></a>Prática recomendada  
 Neste passo a passo, <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> é implementada de modo que a coleção do objeto selecionável e a coleção de objetos selecionados são a mesma coleção. Apenas o objeto selecionado é exibida na lista de navegador de propriedade. Para uma implementação de ISelectionContainer mais completa, consulte os exemplos de Reference.ToolWindow.  
  
 Janelas de ferramentas do Visual Studio persistem entre sessões do Visual Studio. Para obter mais informações sobre como manter o estado da janela de ferramenta, consulte <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Estender propriedades e a janela de propriedades](../extensibility/extending-properties-and-the-property-window.md)

