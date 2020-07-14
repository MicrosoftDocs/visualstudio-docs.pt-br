---
title: 'Walkthrough: usando um comando do shell com uma extensão de editor | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - add a menu command
ms.assetid: 08526848-a442-4cd4-afa1-b2eac2005adb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9e9f7de69cfd969db8ae905ea65bbf868cf2c88a
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904456"
---
# <a name="walkthrough-use-a-shell-command-with-an-editor-extension"></a>Walkthrough: usar um comando do shell com uma extensão do editor
Em um VSPackage, você pode adicionar recursos como comandos de menu ao editor. Este tutorial mostra como adicionar um Adornment a uma exibição de texto no editor invocando um comando de menu.

 Este tutorial demonstra o uso de um VSPackage junto com uma parte de componente Managed Extensibility Framework (MEF). Você deve usar um VSPackage para registrar o comando de menu no Shell do Visual Studio. E, você pode usar o comando para acessar a parte do componente MEF.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio do centro de download. Ele está incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-an-extension-with-a-menu-command"></a>Criar uma extensão com um comando de menu
 Crie um VSPackage que coloque um comando de menu chamado **Add Adornment** no menu **ferramentas** .

1. Crie um projeto VSIX em C# chamado `MenuCommandTest` e adicione um nome de modelo de item de comando personalizado **addadornament**. Para obter mais informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).

2. Uma solução chamada MenuCommandTest é aberta. O arquivo MenuCommandTestPackage tem o código que cria o comando de menu e o coloca no menu **ferramentas** . Neste ponto, o comando apenas faz com que uma caixa de mensagem seja exibida. Etapas posteriores mostrarão como alterar isso para exibir o comentário Adornment.

3. Abra o arquivo *Source. Extension. vsixmanifest* no editor de manifesto do VSIX. A `Assets` guia deve ter uma linha para um Microsoft. VisualStudio. VSPackage chamado MenuCommandTest.

4. Salve e feche o arquivo *Source. Extension. vsixmanifest* .

## <a name="add-a-mef-extension-to-the-command-extension"></a>Adicionar uma extensão de MEF à extensão de comando

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nó da solução, clique em **Adicionar**e em **novo projeto**. Na caixa de diálogo **Adicionar novo projeto** , clique em **extensibilidade** em **Visual C#** e, em seguida, **projeto VSIX**. Dê ao projeto o nome de `CommentAdornmentTest`.

2. Como este projeto irá interagir com o assembly VSPackage de nome forte, você deve assinar o assembly. Você pode reutilizar o arquivo de chave já criado para o assembly VSPackage.

    1. Abra as propriedades do projeto e selecione a guia **assinatura** .

    2. Selecione **assinar o assembly**.

    3. Em **escolher um arquivo de chave de nome forte**, selecione o arquivo *Key. SNK* que foi gerado para o assembly MenuCommandTest.

## <a name="refer-to-the-mef-extension-in-the-vspackage-project"></a>Consulte a extensão do MEF no projeto VSPackage
 Como você está adicionando um componente MEF ao VSPackage, você deve especificar os dois tipos de ativos no manifesto.

> [!NOTE]
> Para obter mais informações sobre o MEF, consulte [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index).

### <a name="to-refer-to-the-mef-component-in-the-vspackage-project"></a>Para fazer referência ao componente MEF no projeto VSPackage

1. No projeto MenuCommandTest, abra o arquivo *Source. Extension. vsixmanifest* no editor de manifesto do VSIX.

2. Na guia **ativos** , clique em **novo**.

3. Na lista **tipo** , escolha **Microsoft. VisualStudio. MefComponent**.

4. Na lista **origem** , escolha **um projeto na solução atual**.

5. Na lista **projeto** , escolha **CommentAdornmentTest**.

6. Salve e feche o arquivo *Source. Extension. vsixmanifest* .

7. Certifique-se de que o projeto MenuCommandTest tenha uma referência ao projeto CommentAdornmentTest.

8. No projeto CommentAdornmentTest, defina o projeto para produzir um assembly. Na **Gerenciador de soluções**, selecione o projeto e examine a janela **Propriedades** para a propriedade **copiar saída da compilação para OutputDirectory** e defina-a como **true**.

## <a name="define-a-comment-adornment"></a>Definir um comentário Adornment
 O comentário Adornment consiste em um <xref:Microsoft.VisualStudio.Text.ITrackingSpan> que acompanha o texto selecionado e algumas cadeias de caracteres que representam o autor e a descrição do texto.

#### <a name="to-define-a-comment-adornment"></a>Para definir um comentário Adornment

1. No projeto CommentAdornmentTest, adicione um novo arquivo de classe e nomeie-o `CommentAdornment` .

2. Adicione as seguintes referências:

    1. Microsoft. VisualStudio. CoreUtility

    2. Microsoft. VisualStudio. Text. Data

    3. Microsoft. VisualStudio. Text. Logic

    4. Microsoft. VisualStudio. Text. UI

    5. Microsoft. VisualStudio. Text. UI. WPF

    6. System. ComponentModel. composição

    7. PresentationCore

    8. PresentationFramework

    9. WindowsBase

3. Adicione a diretiva a seguir `using` .

    ```csharp
    using Microsoft.VisualStudio.Text;
    ```

4. O arquivo deve conter uma classe chamada `CommentAdornment` .

    ```csharp
    internal class CommentAdornment
    ```

5. Adicione três campos à `CommentAdornment` classe para o <xref:Microsoft.VisualStudio.Text.ITrackingSpan> , o autor e a descrição.

    ```csharp
    public readonly ITrackingSpan Span;
    public readonly string Author;
    public readonly string Text;
    ```

6. Adicione um construtor que inicializa os campos.

    ```csharp
    public CommentAdornment(SnapshotSpan span, string author, string text)
    {
        this.Span = span.Snapshot.CreateTrackingSpan(span, SpanTrackingMode.EdgeExclusive);
        this.Author = author;
        this.Text = text;
    }
    ```

## <a name="create-a-visual-element-for-the-adornment"></a>Criar um elemento visual para o Adornment
 Defina um elemento visual para seu Adornment. Para esta explicação, defina um controle que herda da classe Windows Presentation Foundation (WPF) <xref:System.Windows.Controls.Canvas> .

1. Crie uma classe no projeto CommentAdornmentTest e nomeie-a `CommentBlock` .

2. Adicione as seguintes `using` diretivas.

    ```csharp
    using Microsoft.VisualStudio.Text;
    using System;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Media;
    using System.Windows.Shapes;
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Utilities;
    ```

3. Faça a `CommentBlock` herança da classe <xref:System.Windows.Controls.Canvas> .

    ```csharp
    internal class CommentBlock : Canvas
    { }
    ```

4. Adicione alguns campos particulares para definir os aspectos visuais do Adornment.

    ```csharp
    private Geometry textGeometry;
    private Grid commentGrid;
    private static Brush brush;
    private static Pen solidPen;
    private static Pen dashPen;
    ```

5. Adicione um construtor que defina o comentário Adornment e adicione o texto relevante.

    ```csharp
    public CommentBlock(double textRightEdge, double viewRightEdge,
            Geometry newTextGeometry, string author, string body)
    {
        if (brush == null)
        {
            brush = new SolidColorBrush(Color.FromArgb(0x20, 0x00, 0xff, 0x00));
            brush.Freeze();
            Brush penBrush = new SolidColorBrush(Colors.Green);
            penBrush.Freeze();
            solidPen = new Pen(penBrush, 0.5);
            solidPen.Freeze();
            dashPen = new Pen(penBrush, 0.5);
            dashPen.DashStyle = DashStyles.Dash;
            dashPen.Freeze();
        }

        this.textGeometry = newTextGeometry;

        TextBlock tb1 = new TextBlock();
        tb1.Text = author;
        TextBlock tb2 = new TextBlock();
        tb2.Text = body;

        const int MarginWidth = 8;
        this.commentGrid = new Grid();
        this.commentGrid.RowDefinitions.Add(new RowDefinition());
        this.commentGrid.RowDefinitions.Add(new RowDefinition());
        ColumnDefinition cEdge = new ColumnDefinition();
        cEdge.Width = new GridLength(MarginWidth);
        ColumnDefinition cEdge2 = new ColumnDefinition();
        cEdge2.Width = new GridLength(MarginWidth);
        this.commentGrid.ColumnDefinitions.Add(cEdge);
        this.commentGrid.ColumnDefinitions.Add(new ColumnDefinition());
        this.commentGrid.ColumnDefinitions.Add(cEdge2);

        System.Windows.Shapes.Rectangle rect = new System.Windows.Shapes.Rectangle();
        rect.RadiusX = 6;
        rect.RadiusY = 3;
        rect.Fill = brush;
        rect.Stroke = Brushes.Green;

            Size inf = new Size(double.PositiveInfinity, double.PositiveInfinity);
            tb1.Measure(inf);
            tb2.Measure(inf);
            double middleWidth = Math.Max(tb1.DesiredSize.Width, tb2.DesiredSize.Width);
            this.commentGrid.Width = middleWidth + 2 * MarginWidth;

        Grid.SetColumn(rect, 0);
        Grid.SetRow(rect, 0);
        Grid.SetRowSpan(rect, 2);
        Grid.SetColumnSpan(rect, 3);
        Grid.SetRow(tb1, 0);
        Grid.SetColumn(tb1, 1);
        Grid.SetRow(tb2, 1);
        Grid.SetColumn(tb2, 1);
        this.commentGrid.Children.Add(rect);
        this.commentGrid.Children.Add(tb1);
        this.commentGrid.Children.Add(tb2);

        Canvas.SetLeft(this.commentGrid, Math.Max(viewRightEdge - this.commentGrid.Width - 20.0, textRightEdge + 20.0));
        Canvas.SetTop(this.commentGrid, textGeometry.GetRenderBounds(solidPen).Top);

        this.Children.Add(this.commentGrid);
    }
    ```

6. Implemente também um <xref:System.Windows.Controls.Panel.OnRender%2A> manipulador de eventos que desenha o Adornment.

    ```csharp
    protected override void OnRender(DrawingContext dc)
    {
        base.OnRender(dc);
        if (this.textGeometry != null)
        {
            dc.DrawGeometry(brush, solidPen, this.textGeometry);
            Rect textBounds = this.textGeometry.GetRenderBounds(solidPen);
            Point p1 = new Point(textBounds.Right, textBounds.Bottom);
            Point p2 = new Point(Math.Max(Canvas.GetLeft(this.commentGrid) - 20.0, p1.X), p1.Y);
            Point p3 = new Point(Math.Max(Canvas.GetLeft(this.commentGrid), p1.X), (Canvas.GetTop(this.commentGrid) + p1.Y) * 0.5);
            dc.DrawLine(dashPen, p1, p2);
            dc.DrawLine(dashPen, p2, p3);
        }
    }
    ```

## <a name="add-an-iwpftextviewcreationlistener"></a>Adicionar um IWpfTextViewCreationListener
 O <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> é uma parte de componente do MEF que você pode usar para escutar a exibição de eventos de criação.

1. Adicione um arquivo de classe ao projeto CommentAdornmentTest e nomeie-o `Connector` .

2. Adicione as seguintes `using` diretivas.

    ```csharp
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Utilities;
    ```

3. Declare uma classe que implementa e <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> exporte-a com um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "texto" e um <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> de <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document> . O atributo Content Type Especifica o tipo de conteúdo ao qual o componente se aplica. O tipo de texto é o tipo base para todos os tipos de arquivo não binários. Portanto, quase todas as exibições de texto criadas serão desse tipo. O atributo função de exibição de texto especifica o tipo de exibição de texto ao qual o componente se aplica. As funções de exibição de texto de documento geralmente mostram o texto composto de linhas e é armazenado em um arquivo.

     [!code-vb[VSSDKMenuCommandTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-using-a-shell-command-with-an-editor-extension_1.vb)]
     [!code-csharp[VSSDKMenuCommandTest#11](../extensibility/codesnippet/CSharp/walkthrough-using-a-shell-command-with-an-editor-extension_1.cs)]

4. Implemente o <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> método para que ele chame o `Create()` evento estático do `CommentAdornmentManager` .

    ```csharp
    public void TextViewCreated(IWpfTextView textView)
    {
        CommentAdornmentManager.Create(textView);
    }
    ```

5. Adicione um método que você pode usar para executar o comando.

    ```csharp
    static public void Execute(IWpfTextViewHost host)
    {
        IWpfTextView view = host.TextView;
        //Add a comment on the selected text. 
        if (!view.Selection.IsEmpty)
        {
            //Get the provider for the comment adornments in the property bag of the view.
            CommentAdornmentProvider provider = view.Properties.GetProperty<CommentAdornmentProvider>(typeof(CommentAdornmentProvider));

            //Add some arbitrary author and comment text. 
            string author = System.Security.Principal.WindowsIdentity.GetCurrent().Name;
            string comment = "Four score....";

            //Add the comment adornment using the provider.
            provider.Add(view.Selection.SelectedSpans[0], author, comment);
        }
    }
    ```

## <a name="define-an-adornment-layer"></a>Definir uma camada Adornment
 Para adicionar um novo Adornment, você deve definir uma camada Adornment.

### <a name="to-define-an-adornment-layer"></a>Para definir uma camada de Adornment

1. Na `Connector` classe, declare um campo público do tipo <xref:Microsoft.VisualStudio.Text.Editor.AdornmentLayerDefinition> e exporte-o com um <xref:Microsoft.VisualStudio.Utilities.NameAttribute> que especifica um nome exclusivo para a camada Adornment e um <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> que define a relação de ordem Z dessa camada Adornment para as outras camadas de exibição de texto (texto, cursor e seleção).

    ```csharp
    [Export(typeof(AdornmentLayerDefinition))]
    [Name("CommentAdornmentLayer")]
    [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
    public AdornmentLayerDefinition commentLayerDefinition;

    ```

## <a name="provide-comment-adornments"></a>Fornecer adornos de comentário
 Ao definir um Adornment, implemente também um provedor Adornment de comentário e um comentário Adornment Manager. O provedor Adornment de comentários mantém uma lista de adornos de comentário, ouve <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> eventos no buffer de texto subjacente e exclui adorners de comentário quando o texto subjacente é excluído.

1. Adicione um novo arquivo de classe ao projeto CommentAdornmentTest e nomeie-o `CommentAdornmentProvider` .

2. Adicione as seguintes `using` diretivas.

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Collections.ObjectModel;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Editor;
    ```

3. Adicione uma classe chamada `CommentAdornmentProvider`.

    ```csharp
    internal class CommentAdornmentProvider
    {
    }
    ```

4. Adicione campos particulares para o buffer de texto e a lista de adornos de comentário relacionados ao buffer.

    ```csharp
    private ITextBuffer buffer;
    private IList<CommentAdornment> comments = new List<CommentAdornment>();

    ```

5. Adicione um construtor para `CommentAdornmentProvider` . Esse construtor deve ter acesso privado porque o provedor é instanciado pelo `Create()` método. O construtor adiciona o `OnBufferChanged` manipulador de eventos ao <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> evento.

    ```csharp
    private CommentAdornmentProvider(ITextBuffer buffer)
    {
        this.buffer = buffer;
        //listen to the Changed event so we can react to deletions. 
        this.buffer.Changed += OnBufferChanged;
    }

    ```

6. Adicione o método `Create()`.

    ```csharp
    public static CommentAdornmentProvider Create(IWpfTextView view)
    {
        return view.Properties.GetOrCreateSingletonProperty<CommentAdornmentProvider>(delegate { return new CommentAdornmentProvider(view.TextBuffer); });
    }

    ```

7. Adicione o método `Detach()`.

    ```csharp
    public void Detach()
    {
        if (this.buffer != null)
        {
            //remove the Changed listener 
            this.buffer.Changed -= OnBufferChanged;
            this.buffer = null;
        }
    }
    ```

8. Adicione o `OnBufferChanged` manipulador de eventos.

     [!code-csharp[VSSDKMenuCommandTest#21](../extensibility/codesnippet/CSharp/walkthrough-using-a-shell-command-with-an-editor-extension_2.cs)]
     [!code-vb[VSSDKMenuCommandTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-using-a-shell-command-with-an-editor-extension_2.vb)]

9. Adicione uma declaração para um `CommentsChanged` evento.

    ```csharp
    public event EventHandler<CommentsChangedEventArgs> CommentsChanged;
    ```

10. Crie um `Add()` método para adicionar o Adornment.

    ```csharp
    public void Add(SnapshotSpan span, string author, string text)
    {
        if (span.Length == 0)
            throw new ArgumentOutOfRangeException("span");
        if (author == null)
            throw new ArgumentNullException("author");
        if (text == null)
            throw new ArgumentNullException("text");

        //Create a comment adornment given the span, author and text.
        CommentAdornment comment = new CommentAdornment(span, author, text);

        //Add it to the list of comments. 
        this.comments.Add(comment);

        //Raise the changed event.
        EventHandler<CommentsChangedEventArgs> commentsChanged = this.CommentsChanged;
        if (commentsChanged != null)
            commentsChanged(this, new CommentsChangedEventArgs(comment, null));
    }

    ```

11. Adicione um `RemoveComments()` método.

    ```csharp
    public void RemoveComments(SnapshotSpan span)
    {
        EventHandler<CommentsChangedEventArgs> commentsChanged = this.CommentsChanged;

        //Get a list of all the comments that are being kept
        IList<CommentAdornment> keptComments = new List<CommentAdornment>(this.comments.Count);

        foreach (CommentAdornment comment in this.comments)
        {
            //find out if the given span overlaps with the comment text span. If two spans are adjacent, they do not overlap. To consider adjacent spans, use IntersectsWith. 
            if (comment.Span.GetSpan(span.Snapshot).OverlapsWith(span))
            {
                //Raise the change event to delete this comment. 
                if (commentsChanged != null)
                    commentsChanged(this, new CommentsChangedEventArgs(null, comment));
            }
            else
                keptComments.Add(comment);
        }

        this.comments = keptComments;
    }
    ```

12. Adicione um `GetComments()` método que retorna todos os comentários em um determinado span de instantâneo.

    ```csharp
    public Collection<CommentAdornment> GetComments(SnapshotSpan span)
    {
        IList<CommentAdornment> overlappingComments = new List<CommentAdornment>();
        foreach (CommentAdornment comment in this.comments)
        {
            if (comment.Span.GetSpan(span.Snapshot).OverlapsWith(span))
                overlappingComments.Add(comment);
        }

        return new Collection<CommentAdornment>(overlappingComments);
    }
    ```

13. Adicione uma classe chamada `CommentsChangedEventArgs` , da seguinte maneira.

    ```csharp
    internal class CommentsChangedEventArgs : EventArgs
    {
        public readonly CommentAdornment CommentAdded;

        public readonly CommentAdornment CommentRemoved;

        public CommentsChangedEventArgs(CommentAdornment added, CommentAdornment removed)
        {
            this.CommentAdded = added;
            this.CommentRemoved = removed;
        }
    }
    ```

## <a name="manage-comment-adornments"></a>Gerenciar adornos de comentário
 O comentário Adornment Manager cria o Adornment e o adiciona à camada Adornment. Ele escuta os <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> <xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed> eventos e para que ele possa mover ou excluir o Adornment. Ele também escuta o `CommentsChanged` evento que é disparado pelo provedor de comentário Adornment quando comentários são adicionados ou removidos.

1. Adicione um arquivo de classe ao projeto CommentAdornmentTest e nomeie-o `CommentAdornmentManager` .

2. Adicione as seguintes `using` diretivas.

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Windows.Media;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Formatting;
    ```

3. Adicione uma classe chamada `CommentAdornmentManager`.

    ```csharp
    internal class CommentAdornmentManager
        {
        }
    ```

4. Adicione alguns campos particulares.

    ```csharp
    private readonly IWpfTextView view;
    private readonly IAdornmentLayer layer;
    private readonly CommentAdornmentProvider provider;
    ```

5. Adicione um construtor que assina o gerente aos <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> eventos e e <xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed> também ao `CommentsChanged` evento. O construtor é privado porque o gerente é instanciado pelo método estático `Create()` .

    ```csharp
    private CommentAdornmentManager(IWpfTextView view)
    {
        this.view = view;
        this.view.LayoutChanged += OnLayoutChanged;
        this.view.Closed += OnClosed;

        this.layer = view.GetAdornmentLayer("CommentAdornmentLayer");

        this.provider = CommentAdornmentProvider.Create(view);
        this.provider.CommentsChanged += OnCommentsChanged;
    }
    ```

6. Adicione o `Create()` método que obtém um provedor ou cria um, se necessário.

    ```csharp
    public static CommentAdornmentManager Create(IWpfTextView view)
    {
        return view.Properties.GetOrCreateSingletonProperty<CommentAdornmentManager>(delegate { return new CommentAdornmentManager(view); });
    }
    ```

7. Adicione o `CommentsChanged` manipulador.

    ```csharp
    private void OnCommentsChanged(object sender, CommentsChangedEventArgs e)
    {
        //Remove the comment (when the adornment was added, the comment adornment was used as the tag). 
        if (e.CommentRemoved != null)
            this.layer.RemoveAdornmentsByTag(e.CommentRemoved);

        //Draw the newly added comment (this will appear immediately: the view does not need to do a layout). 
        if (e.CommentAdded != null)
            this.DrawComment(e.CommentAdded);
    }
    ```

8. Adicione o <xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed> manipulador.

    ```csharp
    private void OnClosed(object sender, EventArgs e)
    {
        this.provider.Detach();
        this.view.LayoutChanged -= OnLayoutChanged;
        this.view.Closed -= OnClosed;
    }
    ```

9. Adicione o <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> manipulador.

    ```csharp
    private void OnLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)
    {
        //Get all of the comments that intersect any of the new or reformatted lines of text.
        List<CommentAdornment> newComments = new List<CommentAdornment>();

        //The event args contain a list of modified lines and a NormalizedSpanCollection of the spans of the modified lines.  
        //Use the latter to find the comments that intersect the new or reformatted lines of text. 
        foreach (Span span in e.NewOrReformattedSpans)
        {
            newComments.AddRange(this.provider.GetComments(new SnapshotSpan(this.view.TextSnapshot, span)));
        }

        //It is possible to get duplicates in this list if a comment spanned 3 lines, and the first and last lines were modified but the middle line was not. 
        //Sort the list and skip duplicates.
        newComments.Sort(delegate(CommentAdornment a, CommentAdornment b) { return a.GetHashCode().CompareTo(b.GetHashCode()); });

        CommentAdornment lastComment = null;
        foreach (CommentAdornment comment in newComments)
        {
            if (comment != lastComment)
            {
                lastComment = comment;
                this.DrawComment(comment);
            }
        }
    }
    ```

10. Adicione o método particular que desenha o comentário.

     [!code-csharp[VSSDKMenuCommandTest#35](../extensibility/codesnippet/CSharp/walkthrough-using-a-shell-command-with-an-editor-extension_3.cs)]
     [!code-vb[VSSDKMenuCommandTest#35](../extensibility/codesnippet/VisualBasic/walkthrough-using-a-shell-command-with-an-editor-extension_3.vb)]

## <a name="use-the-menu-command-to-add-the-comment-adornment"></a>Use o comando de menu para adicionar o comentário Adornment
 Você pode usar o comando de menu para criar um comentário Adornment implementando o `MenuItemCallback` método de VSPackage.

1. Adicione as seguintes referências ao projeto MenuCommandTest:

    - Microsoft. VisualStudio. Textmanager. Interop

    - Microsoft. VisualStudio. editor

    - Microsoft. VisualStudio. Text. UI. WPF

2. Abra o arquivo *AddAdornment.cs* e adicione as seguintes `using` diretivas.

    ```csharp
    using Microsoft.VisualStudio.TextManager.Interop;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Editor;
    using CommentAdornmentTest;
    ```

3. Exclua o `Execute()` método e adicione o manipulador de comando a seguir.

    ```csharp
    private async void AddAdornmentHandler(object sender, EventArgs e)
    {
    }
    ```

4. Adicione o código para obter o modo de exibição ativo. Você deve obter o `SVsTextManager` do shell do Visual Studio para obter o ativo `IVsTextView` .

    ```csharp
    private async void AddAdornmentHandler(object sender, EventArgs e)
    {
        IVsTextManager txtMgr = (IVsTextManager) await ServiceProvider.GetServiceAsync(typeof(SVsTextManager));
        IVsTextView vTextView = null;
        int mustHaveFocus = 1;
        txtMgr.GetActiveView(mustHaveFocus, null, out vTextView);
    }
    ```

5. Se essa exibição de texto for uma instância de uma exibição de texto de editor, você poderá convertê-la na <xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData> interface e, em seguida, obter o <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> e seu associado <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> . Use o <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> para chamar o `Connector.Execute()` método, que obtém o comentário Adornment Provider e adiciona o Adornment. O manipulador de comandos agora deve se parecer com este código:

    ```csharp
    private async void AddAdornmentHandler(object sender, EventArgs e)
    {
        IVsTextManager txtMgr = (IVsTextManager) await ServiceProvider.GetServiceAsync(typeof(SVsTextManager));
        IVsTextView vTextView = null;
        int mustHaveFocus = 1;
        txtMgr.GetActiveView(mustHaveFocus, null, out vTextView);
        IVsUserData userData = vTextView as IVsUserData;
         if (userData == null)
        {
            Console.WriteLine("No text view is currently open");
            return;
        }
        IWpfTextViewHost viewHost;
        object holder;
        Guid guidViewHost = DefGuidList.guidIWpfTextViewHost;
        userData.GetData(ref guidViewHost, out holder);
        viewHost = (IWpfTextViewHost)holder;
        Connector.Execute(viewHost);
    }
    ```

6. Defina o método AddAdornmentHandler como o manipulador para o comando addadornation no Construtor addadornation.

    ```csharp
    private AddAdornment(AsyncPackage package, OleMenuCommandService commandService)
    {
        this.package = package ?? throw new ArgumentNullException(nameof(package));
        commandService = commandService ?? throw new ArgumentNullException(nameof(commandService));

        var menuCommandID = new CommandID(CommandSet, CommandId);
        var menuItem = new MenuCommand(this.AddAdornmentHandler, menuCommandID);
        commandService.AddCommand(menuItem);
    }
    ```

## <a name="build-and-test-the-code"></a>Compilar e testar o código

1. Compile a solução e inicie a depuração. A instância experimental deve aparecer.

2. Crie um arquivo de texto. Digite algum texto e, em seguida, selecione-o.

3. No menu **ferramentas** , clique em **invocar adicionar Adornment**. Um balão deve ser exibido no lado direito da janela de texto e deve conter texto que se assemelha ao texto a seguir.

     Seunomedeusuário

     Fourscore...

## <a name="see-also"></a>Confira também
- [Walkthrough: vincular um tipo de conteúdo a uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
