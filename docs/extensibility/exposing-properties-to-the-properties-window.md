---
title: Expondo propriedades à janela propriedades | Microsoft Docs
description: Saiba mais sobre as propriedades públicas de um objeto . As alterações feitas nessas propriedades são refletidas no janela Propriedades.
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
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
ms.openlocfilehash: 5f932772b031332d7df2a2487c70576f49407ba1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898731"
---
# <a name="expose-properties-to-the-properties-window"></a>Expor propriedades ao janela Propriedades

Este passo a passo expõe as propriedades públicas de um objeto para a **janela** Propriedades. As alterações feitas nessas propriedades são refletidas na **janela** Propriedades.

## <a name="prerequisites"></a>Pré-requisitos

A partir Visual Studio 2015, você não instala o SDK do Visual Studio do centro de download. Ele é incluído como um recurso opcional na Visual Studio configuração. Você também pode instalar o SDK do VS posteriormente. Para obter mais informações, [consulte Instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="expose-properties-to-the-properties-window"></a>Expor propriedades ao janela Propriedades

Nesta seção, você criará uma janela de ferramentas personalizada e exibirá as propriedades públicas do objeto do painel de janela associado na **janela** Propriedades.

### <a name="to-expose-properties-to-the-properties-window"></a>Para expor propriedades ao janela Propriedades

1. Cada Visual Studio extensão começa com um projeto de implantação do VSIX, que conterá os ativos de extensão. Crie um [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] projeto VSIX chamado `MyObjectPropertiesExtension` . Você pode encontrar o modelo de projeto VSIX na **caixa de diálogo** Novo Projeto pesquisando "vsix".

2. Adicione uma janela de ferramentas adicionando um modelo de item da Janela de Ferramentas Personalizada chamado `MyToolWindow` . No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e **selecione Adicionar**  >  **Novo Item**. Na caixa **de diálogo Adicionar Novo Item**, acesse **Extensibilidade** de Itens do Visual C# e selecione Janela de Ferramentas  >   **Personalizada**. No campo **Nome** na parte inferior da caixa de diálogo, altere o nome do arquivo para *MyToolWindow.cs.* Para obter mais informações sobre como criar uma janela de ferramentas personalizada, consulte [Criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).

3. Abra *MyToolWindow.cs* e adicione a seguinte instrução using:

   ```csharp
   using System.Collections;
   using System.ComponentModel;
   using Microsoft.VisualStudio.Shell.Interop;
   ```

4. Agora, adicione os campos a seguir à `MyToolWindow` classe .

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

    A `TrackSelection` propriedade usa para obter um `GetService` `STrackSelection` serviço, que fornece uma interface <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> . O `OnToolWindowCreated` manipulador de eventos e o método juntos criam uma lista de objetos selecionados que contém apenas o próprio objeto do painel de janela de `SelectList` ferramentas. O `UpdateSelection` método informa à janela **Propriedades** para exibir as propriedades públicas do painel da janela de ferramentas.

6. Compile o projeto e comece a depuração. A instância experimental do Visual Studio deve aparecer.

7. Se a **janela Propriedades** não estiver visível, abra-a pressionando **F4**.

8. Abra a **janela MyToolWindow.** Você pode encontrá-lo em **Exibir**  >  **Outras Janelas.**

    A janela é aberta e as propriedades públicas do painel de janela aparecem na **janela** Propriedades.

9. Altere **a propriedade Legenda** na janela **Propriedades** para Minhas Propriedades **do Objeto**.

     A legenda da janela MyToolWindow muda de acordo.

## <a name="expose-tool-window-properties"></a>Expor propriedades da janela da ferramenta

Nesta seção, você adicionará uma janela de ferramentas e exporá suas propriedades. As alterações feitas nas propriedades são refletidas na **janela** Propriedades.

### <a name="to-expose-tool-window-properties"></a>Para expor as propriedades da janela da ferramenta

1. Abra *MyToolWindow.cs* e adicione a propriedade booliana pública IsChecked à `MyToolWindow` classe .

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

     Essa propriedade obtém seu estado da caixa de seleção WPF que você criará posteriormente.

2. Abra *MyToolWindowControl.xaml.cs* e substitua o construtor MyToolWindowControl pelo código a seguir.

    ```vb
    private MyToolWindow pane;
    public MyToolWindowControl(MyToolWindow pane)
    {
        InitializeComponent();
        this.pane = pane;
        checkBox.IsChecked = false;
    }
    ```

     Isso fornece `MyToolWindowControl` acesso ao `MyToolWindow` painel.

3. Em *MyToolWindow.cs,* altere `MyToolWindow` o construtor da seguinte forma:

    ```csharp
    base.Content = new MyToolWindowControl(this);
    ```

4. Altere para a exibição de design de MyToolWindowControl.

5. Exclua o botão e adicione uma caixa de seleção da **Caixa de** Ferramentas ao canto superior esquerdo.

6. Adicione os eventos Checked e Unchecked. Marque a caixa de seleção na exibição de design. Na janela **Propriedades,** clique no botão manipuladores de eventos (na parte superior direita da **janela** Propriedades). Encontre **Checked** e digite **checkbox_Checked** na caixa de  texto e, em seguida, encontre Desmarcado e digite checkbox_Unchecked **na** caixa de texto.

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

9. Na instância experimental, abra a **janela MyToolWindow.**

     Procure as propriedades da janela na **janela** Propriedades. A **propriedade IsChecked** aparece na parte inferior da janela, na **categoria Minhas** Propriedades.

10. Marque a caixa de seleção na **janela MyToolWindow.** **IsChecked na** janela **Propriedades muda** para **True.** Des marque a caixa de **seleção na janela MyToolWindow.** **IsChecked na** janela **Propriedades muda** para **False.** Altere o valor de **IsChecked** na **janela** Propriedades. A caixa de seleção na **janela MyToolWindow** muda para corresponder ao novo valor.

    > [!NOTE]
    > Se você deve descartar um objeto que é exibido na janela **Propriedades,** chame com `OnSelectChange` um contêiner de seleção `null` primeiro. Depois de descartar a propriedade ou o objeto, você pode alterar para um contêiner de seleção que atualizou e <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectableObjects%2A> <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectedObjects%2A> lista.

## <a name="change-selection-lists"></a>Alterar listas de seleção

 Nesta seção, você adiciona uma lista de seleção para uma classe de propriedade básica e usa a interface da janela de ferramentas para escolher qual lista de seleção exibir.

### <a name="to-change-selection-lists"></a>Para alterar listas de seleção

1. Abra *MyToolWindow.cs* e adicione uma classe pública chamada `Simple` .

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

2. Adicione uma propriedade à classe , além de dois métodos para alternar a seleção da janela Propriedades entre o `SimpleObject` painel de janela e o objeto `MyToolWindow`  `Simple` .

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

3. Em *MyToolWindowControl.cs,* substitua os manipuladores de caixa de seleção por estas linhas de código:

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

5. Na instância experimental, abra a **janela MyToolWindow.**

6. Marque a caixa de seleção na **janela MyToolWindow.** A **janela** Propriedades exibe as `Simple` propriedades do objeto, **SomeText** e **ReadOnly.** Desmarque a caixa de seleção. As propriedades públicas da janela aparecem na **janela** Propriedades.

    > [!NOTE]
    > O nome de exibição **de SomeText** é **Meu Texto.**

## <a name="best-practice"></a>Melhor prática

Neste passo a passo, é implementado para que a coleção de objetos selecionáveis e a coleção de objetos <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> selecionada sejam a mesma coleção. Somente o objeto selecionado aparece na lista Navegador de Propriedades. Para obter uma implementação mais completa de ISelectionContainer, consulte os exemplos de Reference.ToolWindow.

Visual Studio de ferramentas persistem entre Visual Studio sessões. Para obter mais informações sobre como persistir o estado da janela de ferramentas, consulte <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> .

## <a name="see-also"></a>Confira também

- [Estender propriedades e a janela Propriedade](../extensibility/extending-properties-and-the-property-window.md)
