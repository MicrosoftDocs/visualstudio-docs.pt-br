---
title: Expondo Propriedades à janela Propriedades | Microsoft Docs
description: Saiba mais sobre as propriedades públicas de um objeto. As alterações feitas nessas propriedades são refletidas na janela Propriedades.
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], exposing in Property Browser
- properties [Visual Studio SDK]
- Property Browser, exposing properties
ms.assetid: 47f295b5-1ca5-4e7b-bb52-7b926b136622
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b9de86e956fe6a4d7841d519d7252b75ae216229
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075244"
---
# <a name="expose-properties-to-the-properties-window"></a>Expor propriedades para o janela Propriedades

Este passo a passos expõe as propriedades públicas de um objeto para a janela **Propriedades** . As alterações feitas nessas propriedades são refletidas na janela **Propriedades** .

## <a name="prerequisites"></a>Pré-requisitos

A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="expose-properties-to-the-properties-window"></a>Expor propriedades para o janela Propriedades

Nesta seção, você cria uma janela de ferramentas personalizada e exibe as propriedades públicas do objeto painel de janela associado na janela **Propriedades** .

### <a name="to-expose-properties-to-the-properties-window"></a>Para expor propriedades para o janela Propriedades

1. Cada extensão do Visual Studio começa com um projeto de implantação VSIX, que conterá os ativos de extensão. Crie um [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] projeto VSIX denominado `MyObjectPropertiesExtension` . Você pode encontrar o modelo de projeto VSIX na caixa de diálogo **novo projeto** pesquisando por "VSIX".

2. Adicione uma janela de ferramentas adicionando um modelo de item de janela de ferramenta personalizada chamado `MyToolWindow` . Na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >  **novo item**. Na **caixa de diálogo Adicionar novo item**, vá para extensibilidade de **itens do Visual C#**  >   e selecione **janela de ferramenta personalizada**. No campo **nome** na parte inferior da caixa de diálogo, altere o nome do arquivo para *MyToolWindow. cs*. Para obter mais informações sobre como criar uma janela de ferramentas personalizada, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).

3. Abra *MyToolWindow. cs* e adicione a seguinte instrução Using:

   ```csharp
   using System.Collections;
   using System.ComponentModel;
   using Microsoft.VisualStudio.Shell.Interop;
   ```

4. Agora, adicione os campos a seguir à `MyToolWindow` classe.

   ```csharp
   private ITrackSelection trackSel;
   private SelectionContainer selContainer;

   ```

5. Adicione o código a seguir à classe `MyToolWindow` .

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

   public void UpdateSelection()
   {
       ITrackSelection track = TrackSelection;
       if (track != null)
           track.OnSelectChange((ISelectionContainer)selContainer);
   }

   public void SelectList(ArrayList list)
   {
       selContainer = new SelectionContainer(true, false);
       selContainer.SelectableObjects = list;
       selContainer.SelectedObjects = list;
       UpdateSelection();
   }

   public override void OnToolWindowCreated()
   {
       ArrayList listObjects = new ArrayList();
       listObjects.Add(this);
       SelectList(listObjects);
   }
   ```

    A `TrackSelection` propriedade usa `GetService` para obter um `STrackSelection` serviço, que fornece uma <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> interface. O `OnToolWindowCreated` manipulador de eventos e o `SelectList` método juntos criam uma lista de objetos selecionados que contém apenas o próprio objeto de painel da janela de ferramentas. O `UpdateSelection` método informa à janela **Propriedades** para exibir as propriedades públicas do painel janela da ferramenta.

6. Compile o projeto e comece a depuração. A instância experimental do Visual Studio deve aparecer.

7. Se a janela **Propriedades** não estiver visível, abra-a pressionando **F4**.

8. Abra a janela **MyToolWindow** . Você pode encontrá-lo em **Exibir**  >  **outras janelas**.

    A janela é aberta e as propriedades públicas do painel janela são exibidas na janela **Propriedades** .

9. Altere a propriedade **legenda** na janela **Propriedades** para **minhas propriedades de objeto**.

     A legenda da janela MyToolWindow é alterada de acordo.

## <a name="expose-tool-window-properties"></a>Expor propriedades da janela de ferramentas

Nesta seção, você adiciona uma janela de ferramentas e expõe suas propriedades. As alterações feitas nas propriedades são refletidas na janela **Propriedades** .

### <a name="to-expose-tool-window-properties"></a>Para expor propriedades da janela de ferramentas

1. Abra *MyToolWindow. cs* e adicione a propriedade Public booliana IsChecked à `MyToolWindow` classe.

    ```csharp
    [Category("My Properties")]
    [Description("MyToolWindowControl properties")]
    public bool IsChecked
    {
        get {
            if (base.Content == null)  return false;
            return (bool)(( MyToolWindowControl) base.Content).checkBox.IsChecked;
        }
        set {
            ((MyToolWindowControl) base.Content).checkBox.IsChecked = value;
        }
    }
    ```

     Essa propriedade obtém seu estado na caixa de seleção do WPF que você criará posteriormente.

2. Abra *MyToolWindowControl. XAML. cs* e substitua o Construtor MyToolWindowControl pelo código a seguir.

    ```vb
    private MyToolWindow pane;
    public MyToolWindowControl(MyToolWindow pane)
    {
        InitializeComponent();
        this.pane = pane;
        checkBox.IsChecked = false;
    }
    ```

     Isso dá `MyToolWindowControl` acesso ao `MyToolWindow` painel.

3. No *MyToolWindow. cs*, altere o `MyToolWindow` Construtor da seguinte maneira:

    ```csharp
    base.Content = new MyToolWindowControl(this);
    ```

4. Altere para o modo de exibição de design de MyToolWindowControl.

5. Exclua o botão e adicione uma caixa de seleção do **Toolbox** no canto superior esquerdo.

6. Adicione os eventos marcados e desmarcados. Marque a caixa de seleção na exibição Design. Na janela **Propriedades** , clique no botão manipuladores de eventos (no canto superior direito da janela **Propriedades** ). Localize **selecionado** e digite **checkbox_Checked** na caixa de texto e, em seguida, localize **desmarcado** e digite **checkbox_Unchecked** na caixa de texto.

7. Adicione os manipuladores de eventos da caixa de seleção:

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

8. Compile o projeto e comece a depuração.

9. Na instância experimental, abra a janela **MyToolWindow** .

     Procure as propriedades da janela na janela **Propriedades** . A propriedade **IsChecked** aparece na parte inferior da janela, na categoria **minhas propriedades** .

10. Marque a caixa de seleção na janela **MyToolWindow** . **IsChecked** na janela **Propriedades** muda para **true**. Desmarque a caixa de seleção na janela **MyToolWindow** . **IsChecked** na janela **Propriedades** é alterado para **false**. Altere o valor de **IsChecked** na janela **Propriedades** . A caixa de seleção na janela **MyToolWindow** é alterada para corresponder ao novo valor.

    > [!NOTE]
    > Se for necessário descartar um objeto que é exibido na janela **Propriedades** , chame `OnSelectChange` primeiro um `null` contêiner de seleção. Depois de descartar a propriedade ou o objeto, você pode alterar para um contêiner de seleção que tenha atualizado <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectableObjects%2A> e <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectedObjects%2A> listas.

## <a name="change-selection-lists"></a>Alterar listas de seleção

 Nesta seção, você adiciona uma lista de seleção para uma classe de propriedade básica e usa a interface da janela de ferramentas para escolher a lista de seleção a ser exibida.

### <a name="to-change-selection-lists"></a>Para alterar as listas de seleção

1. Abra *MyToolWindow. cs* e adicione uma classe pública denominada `Simple` .

    ```csharp
    public class Simple
    {
        private string someText = "";

        [Category("My Properties")]
        [Description("Simple Properties")]
        [DisplayName("My Text")]
        public string SomeText
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

2. Adicione uma `SimpleObject` Propriedade à `MyToolWindow` classe, além de dois métodos para alternar a seleção da janela **Propriedades** entre o painel janela e o `Simple` objeto.

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

3. No *MyToolWindowControl. cs*, substitua os manipuladores de caixa de seleção por estas linhas de código:

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

4. Compile o projeto e comece a depuração.

5. Na instância experimental, abra a janela **MyToolWindow** .

6. Marque a caixa de seleção na janela **MyToolWindow** . A janela **Propriedades** exibe as `Simple` Propriedades do objeto, **SomeText** e **ReadOnly**. Desmarque a caixa de seleção. As propriedades públicas da janela são exibidas na janela **Propriedades** .

    > [!NOTE]
    > O nome de exibição de **SomeText** é o **meu texto**.

## <a name="best-practice"></a>Melhor prática

Neste passo a passo, <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> é implementado para que a coleção de objetos selecionáveis e a coleção de objetos selecionada sejam a mesma coleção. Somente o objeto selecionado aparece na lista navegador de propriedades. Para obter uma implementação ISelectionContainer mais completa, consulte os exemplos Reference. ToolWindow.

As janelas de ferramentas do Visual Studio persistem entre as sessões do Visual Studio. Para obter mais informações sobre como persistir o estado da janela de ferramentas, consulte <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> .

## <a name="see-also"></a>Confira também

- [Estender Propriedades e a janela de propriedades](../extensibility/extending-properties-and-the-property-window.md)
