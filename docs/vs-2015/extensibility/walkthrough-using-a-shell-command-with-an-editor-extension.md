---
title: 'Passo a passo: Usando um comando de Shell com uma extensão do Editor | Microsoft Docs'
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
- editors [Visual Studio SDK], new - add a menu command
ms.assetid: 08526848-a442-4cd4-afa1-b2eac2005adb
caps.latest.revision: 47
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e64d50dcd56f1421e4ffe1ab33b5396c436eeeda
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51773035"
---
# <a name="walkthrough-using-a-shell-command-with-an-editor-extension"></a>Passo a passo: usando um comando do shell com uma extensão do editor
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

De um VSPackage, você pode adicionar recursos, como comandos de menu para o editor. Este passo a passo mostra como adicionar um adorno a um modo de exibição de texto no editor, invocando um comando de menu.  
  
 Este passo a passo demonstra o uso de um VSPackage junto com uma parte do componente de Managed Extensibility Framework (MEF). Você deve usar um VSPackage para registrar o comando de menu com o shell do Visual Studio, e você pode usar o comando para acessar a parte do componente MEF.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-an-extension-with-a-menu-command"></a>Criando uma extensão com um comando de menu  
 Crie um VSPackage que coloca um comando de menu chamado **adicionar adorno** sobre o **ferramentas** menu.  
  
1.  Crie um projeto de VSIX em C# chamado `MenuCommandTest`e adicione um nome de modelo de item de comando personalizado **AddAdornment**. Para obter mais informações, consulte [criar uma extensão com um comando de Menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
2.  Uma solução chamada MenuCommandTest é aberta. O arquivo de MenuCommandTestPackage tem o código que cria o comando de menu e coloca-o a **ferramentas** menu. Neste ponto, o comando fará com apenas uma caixa de mensagem a ser exibido. Etapas posteriores mostram como alterar essa opção para exibir o adorno de comentário.  
  
3.  Abra o arquivo de vsixmanifest no Editor de manifesto do VSIX. O `Assets` guia deve ter uma linha para um VSPackage nomeado MenuCommandTest.  
  
4.  Salve e feche o arquivo vsixmanifest.  
  
## <a name="adding-a-mef-extension-to-the-command-extension"></a>Adicionando uma extensão do MEF para a extensão de comando  
  
1.  Na **Gerenciador de soluções**, clique com botão direito no nó da solução, clique em **Add**e, em seguida, clique em **novo projeto**. No **adicionar novo projeto** caixa de diálogo, clique em **extensibilidade** sob **Visual c#**, em seguida, **projeto VSIX**. Nomeie o projeto `CommentAdornmentTest`.  
  
2.  Porque este projeto irá interagir com o assembly de nome forte de VSPackage, você deve assinar o assembly. Você pode reutilizar o arquivo de chave já criado para o assembly de VSPackage.  
  
    1.  Abra as propriedades do projeto e selecione o **Signing** guia.  
  
    2.  Selecione **assinar o assembly**.  
  
    3.  Sob **escolher um arquivo de chave de nome forte**, selecione o arquivo snk que foi gerado para o assembly MenuCommandTest.  
  
## <a name="referring-to-the-mef-extension-in-the-vspackage-project"></a>Referindo-se para a extensão do MEF no projeto de VSPackage  
 Como você está adicionando um componente de MEF para o VSPackage, você deve especificar ambos os tipos de ativos no manifesto.  
  
> [!NOTE]
>  Para obter mais informações sobre o MEF, consulte [Managed Extensibility Framework (MEF)](http://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde).  
  
#### <a name="to-refer-to-the-mef-component-in-the-vspackage-project"></a>Para fazer referência ao componente de MEF, no projeto de VSPackage  
  
1.  No projeto MenuCommandTest, abra o arquivo de vsixmanifest no Editor de manifesto do VSIX.  
  
2.  Sobre o **ativos** , clique em **New**.  
  
3.  No **tipo** , escolha **mefcomponent**.  
  
4.  No **fonte** , escolha **um projeto na solução atual**.  
  
5.  No **Project** , escolha **CommentAdornmentTest**.  
  
6.  Salve e feche o arquivo vsixmanifest.  
  
7.  Certifique-se de que o projeto MenuCommandTest tem uma referência ao projeto CommentAdornmentTest.  
  
8.  No projeto CommentAdornmentTest, defina o projeto para produzir um assembly. No **Gerenciador de soluções**, selecione o projeto e examinar o **propriedades** janela para o **copiar saída do Build para OutputDirectory** propriedade e defina-o como **verdadeiro**.  
  
## <a name="defining-a-comment-adornment"></a>Definindo um adorno de comentário  
 O adorno de comentário em si consiste em um <xref:Microsoft.VisualStudio.Text.ITrackingSpan> que controla o texto selecionado e algumas cadeias de caracteres que representam o autor e a descrição do texto.  
  
#### <a name="to-define-a-comment-adornment"></a>Para definir um adorno de comentário  
  
1.  No projeto CommentAdornmentTest, adicione um novo arquivo de classe e nomeie- `CommentAdornment`.  
  
2.  Adicione as seguintes referências:  
  
    1.  Microsoft.VisualStudio.CoreUtility  
  
    2.  Microsoft.VisualStudio.Text.Data  
  
    3.  Microsoft.VisualStudio.Text.Logic  
  
    4.  Microsoft.VisualStudio.Text.UI  
  
    5.  Microsoft.VisualStudio.Text.UI.Wpf  
  
    6.  System.ComponentModel.Composition  
  
    7.  PresentationCore  
  
    8.  PresentationFramework  
  
    9. WindowsBase  
  
3.  Adicione o seguinte `using` instrução.  
  
    ```vb  
    using Microsoft.VisualStudio.Text;  
    ```  
  
4.  O arquivo deve conter uma classe chamada `CommentAdornment`.  
  
    ```  
    internal class CommentAdornment  
    ```  
  
5.  Adicionar três campos para o `CommentAdornment` de classe para o <xref:Microsoft.VisualStudio.Text.ITrackingSpan>, o autor e a descrição.  
  
    ```csharp  
    public readonly ITrackingSpan Span;  
    public readonly string Author;  
    public readonly string Text;  
    ```  
  
6.  Adicione um construtor que inicializa os campos.  
  
    ```csharp  
    public CommentAdornment(SnapshotSpan span, string author, string text)  
    {  
        this.Span = span.Snapshot.CreateTrackingSpan(span, SpanTrackingMode.EdgeExclusive);  
        this.Author = author;  
        this.Text = text;  
    }  
    ```  
  
## <a name="creating-a-visual-element-for-the-adornment"></a>Criação de um elemento Visual para o adorno  
 Você também deve definir um elemento visual para o adorno. Para este passo a passo, definir um controle que herda a classe do Windows Presentation Foundation (WPF) <xref:System.Windows.Controls.Canvas>.  
  
1.  Crie uma classe no projeto CommentAdornmentTest e nomeie- `CommentBlock`.  
  
2.  Adicione o seguinte `using` instruções.  
  
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
  
3.  Verifique as `CommentBlock` classe herdar de <xref:System.Windows.Controls.Canvas>.  
  
    ```csharp  
    internal class CommentBlock : Canvas  
    { }  
    ```  
  
4.  Adicione alguns campos particulares para definir os aspectos visuais do adorno.  
  
    ```csharp  
    private Geometry textGeometry;  
    private Grid commentGrid;  
    private static Brush brush;  
    private static Pen solidPen;  
    private static Pen dashPen;  
    ```  
  
5.  Adicione um construtor que define o adorno de comentário e adiciona o texto relevante.  
  
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
  
6.  Também implementam um <xref:System.Windows.Controls.Panel.OnRender%2A> manipulador de eventos que desenha o adorno.  
  
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
  
## <a name="adding-an-iwpftextviewcreationlistener"></a>Adicionando um IWpfTextViewCreationListener  
 O <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> é uma parte do componente MEF que você pode usar para escutar para exibir eventos de criação.  
  
1.  Adicione um arquivo de classe ao projeto CommentAdornmentTest e nomeie- `Connector`.  
  
2.  Adicione o seguinte `using` instruções.  
  
    ```csharp  
    using System.ComponentModel.Composition;  
    using Microsoft.VisualStudio.Text.Editor;  
    using Microsoft.VisualStudio.Utilities;  
    ```  
  
3.  Declarar uma classe que implementa <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>e exportá-lo com um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "text" e um <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> de <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document>. O atributo de tipo de conteúdo especifica o tipo de conteúdo ao qual o componente se aplica. O tipo de texto é o tipo base para todos os tipos de arquivo não binários. Portanto, quase cada exibição de texto que é criada será desse tipo. O atributo de função do modo de exibição de texto Especifica o tipo de exibição de texto ao qual o componente se aplica. Funções de exibição de texto do documento geralmente mostram o texto que é composto de linhas e é armazenado em um arquivo.  
  
     [!code-csharp[VSSDKMenuCommandTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdkmenucommandtest/cs/commentadornmenttest/connector.cs#11)]
     [!code-vb[VSSDKMenuCommandTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkmenucommandtest/vb/commentadornmenttest/connector.vb#11)]  
  
4.  Implemente a <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> , de modo que ele chama estático `Create()` evento do `CommentAdornmentManager`.  
  
    ```csharp  
    public void TextViewCreated(IWpfTextView textView)  
    {  
        CommentAdornmentManager.Create(textView);  
    }  
    ```  
  
5.  Adicione um método que você pode usar para executar o comando.  
  
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
  
## <a name="defining-an-adornment-layer"></a>Definindo uma camada de adorno  
 Para adicionar um adorno de novo, você deve definir uma camada de adorno.  
  
#### <a name="to-define-an-adornment-layer"></a>Para definir uma camada de adorno  
  
1.  No `Connector` classe, declare um campo público do tipo <xref:Microsoft.VisualStudio.Text.Editor.AdornmentLayerDefinition>e exportá-lo com um <xref:Microsoft.VisualStudio.Utilities.NameAttribute> que especifica um nome exclusivo para a camada de adorno e um <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> que define a relação de ordem Z dessa camada de adorno para o outro texto Exibir camadas (texto, cursor e seleção).  
  
    ```csharp  
    [Export(typeof(AdornmentLayerDefinition))]  
    [Name("CommentAdornmentLayer")]  
    [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]  
    public AdornmentLayerDefinition commentLayerDefinition;  
  
    ```  
  
## <a name="providing-comment-adornments"></a>Fornecendo adornos de comentário  
 Quando você define um adorno, também implemente um provedor de adorno de comentário e um Gerenciador de adorno do comentário. O provedor de adorno do comentário mantém uma lista de adornos de comentário, escuta <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> eventos no buffer de texto subjacente e exclusões adornos de comentário quando o texto subjacente é excluído.  
  
1.  Adicione um novo arquivo de classe ao projeto CommentAdornmentTest e nomeie- `CommentAdornmentProvider`.  
  
2.  Adicione o seguinte `using` instruções.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Collections.ObjectModel;  
    using Microsoft.VisualStudio.Text;  
    using Microsoft.VisualStudio.Text.Editor;  
    ```  
  
3.  Adicione uma classe chamada `CommentAdornmentProvider`.  
  
    ```csharp  
    internal class CommentAdornmentProvider  
    {  
    }  
    ```  
  
4.  Adicione campos privados para o buffer de texto e a lista de adornos comentário relacionado ao buffer.  
  
    ```csharp  
    private ITextBuffer buffer;  
    private IList<CommentAdornment> comments = new List<CommentAdornment>();  
  
    ```  
  
5.  Adicione um construtor para `CommentAdornmentProvider`. Este construtor deve ter acesso privado porque o provedor for instanciado pelo `Create()` método. O construtor adiciona os `OnBufferChanged` manipulador de eventos para o <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> eventos.  
  
    ```csharp  
    private CommentAdornmentProvider(ITextBuffer buffer)  
    {  
        this.buffer = buffer;  
        //listen to the Changed event so we can react to deletions.   
        this.buffer.Changed += OnBufferChanged;  
    }  
  
    ```  
  
6.  Adicione o método `Create()`.  
  
    ```csharp  
    public static CommentAdornmentProvider Create(IWpfTextView view)  
    {  
        return view.Properties.GetOrCreateSingletonProperty<CommentAdornmentProvider>(delegate { return new CommentAdornmentProvider(view.TextBuffer); });  
    }  
  
    ```  
  
7.  Adicione o método `Detach()`.  
  
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
  
8.  Adicionar o `OnBufferChanged` manipulador de eventos.  
  
    ```csharp  
    private void OnBufferChanged(object sender, TextContentChangedEventArgs e)  
    {  
        //Make a list of all comments that have a span of at least one character after applying the change. There is no need to raise a changed event for the deleted adornments. The adornments are deleted only if a text change would cause the view to reformat the line and discard the adornments.  
        IList<CommentAdornment> keptComments = new List<CommentAdornment>(this.comments.Count);  
  
        foreach (CommentAdornment comment in this.comments)  
        {  
            Span span = comment.Span.GetSpan(e.After);  
            //if a comment does not span at least one character, its text was deleted.   
            if (span.Length != 0)  
            {  
                keptComments.Add(comment);  
            }  
        }  
  
        this.comments = keptComments;  
    }  
  
    ```  
  
     [!code-csharp[VSSDKMenuCommandTest#21](../snippets/csharp/VS_Snippets_VSSDK/vssdkmenucommandtest/cs/commentadornmenttest/commentadornmentprovider.cs#21)]
     [!code-vb[VSSDKMenuCommandTest#21](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkmenucommandtest/vb/commentadornmenttest/commentadornmentprovider.vb#21)]  
  
9. Adicionar uma declaração para um `CommentsChanged` eventos.  
  
    ```csharp  
    public event EventHandler<CommentsChangedEventArgs> CommentsChanged;  
    ```  
  
10. Criar um `Add()` método para adicionar o adorno.  
  
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
  
11. Adicionar um `RemoveComments()` método.  
  
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
  
12. Adicionar um `GetComments()` método que retorna todos os comentários em um período de instantâneo específico.  
  
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
  
13. Adicione uma classe chamada `CommentsChangedEventArgs`, da seguinte maneira.  
  
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
  
## <a name="managing-comment-adornments"></a>Gerenciando os adornos de comentário  
 O Gerenciador de adorno comentário cria o adorno e adiciona-o para a camada de adorno. Ele escuta para o <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> e <xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed> eventos de forma que ele pode mover ou excluir o adorno. Ele também escuta para o `CommentsChanged` evento que é acionado pelo provedor do adorno de comentário quando os comentários são adicionados ou removidos.  
  
1.  Adicione um arquivo de classe ao projeto CommentAdornmentTest e nomeie- `CommentAdornmentManager`.  
  
2.  Adicione o seguinte `using` instruções.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Windows.Media;  
    using Microsoft.VisualStudio.Text;  
    using Microsoft.VisualStudio.Text.Editor;  
    using Microsoft.VisualStudio.Text.Formatting;  
    ```  
  
3.  Adicione uma classe chamada `CommentAdornmentManager`.  
  
    ```csharp  
    internal class CommentAdornmentManager  
        {  
        }  
    ```  
  
4.  Adicione alguns campos particulares.  
  
    ```csharp  
    private readonly IWpfTextView view;  
    private readonly IAdornmentLayer layer;  
    private readonly CommentAdornmentProvider provider;  
    ```  
  
5.  Adicione um construtor que assina o Gerenciador do <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> e <xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed> eventos e também o `CommentsChanged` eventos. O construtor é particular porque o Gerenciador é instanciado pelo estático `Create()` método.  
  
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
  
6.  Adicionar o `Create()` método que obtém um provedor ou cria um, se necessário.  
  
    ```csharp  
    public static CommentAdornmentManager Create(IWpfTextView view)  
    {  
        return view.Properties.GetOrCreateSingletonProperty<CommentAdornmentManager>(delegate { return new CommentAdornmentManager(view); });  
    }  
    ```  
  
7.  Adicionar o `CommentsChanged` manipulador.  
  
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
  
8.  Adicionar o <xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed> manipulador.  
  
    ```csharp  
    private void OnClosed(object sender, EventArgs e)  
    {  
        this.provider.Detach();  
        this.view.LayoutChanged -= OnLayoutChanged;  
        this.view.Closed -= OnClosed;  
    }  
    ```  
  
9. Adicionar o <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> manipulador.  
  
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
  
     [!code-csharp[VSSDKMenuCommandTest#35](../snippets/csharp/VS_Snippets_VSSDK/vssdkmenucommandtest/cs/commentadornmenttest/commentadornmentmanager.cs#35)]
     [!code-vb[VSSDKMenuCommandTest#35](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkmenucommandtest/vb/commentadornmenttest/commentadornmentmanager.vb#35)]  
  
## <a name="using-the-menu-command-to-add-the-comment-adornment"></a>Usando o comando de Menu para adicionar o adorno de comentário  
 Você pode usar o comando de menu para criar um adorno de comentário Implementando o `MenuItemCallback` método do VSPackage.  
  
1.  Adicione as seguintes referências ao projeto MenuCommandTest:  
  
    -   Microsoft.VisualStudio.TextManager.Interop  
  
    -   Microsoft.VisualStudio.Editor  
  
    -   Microsoft.VisualStudio.Text.UI.Wpf  
  
2.  Abra o arquivo AddAdornment.cs e adicione o seguinte `using` instruções.  
  
    ```csharp  
    using Microsoft.VisualStudio.TextManager.Interop;  
    using Microsoft.VisualStudio.Text.Editor;  
    using Microsoft.VisualStudio.Editor;  
    using CommentAdornmentTest;  
    ```  
  
3.  Exclua o método ShowMessageBox() e adicione o seguinte manipulador de comando.  
  
    ```csharp  
    private void AddAdornmentHandler(object sender, EventArgs e)  
    {  
    }  
    ```  
  
4.  Adicione código para obter a exibição ativa. Você deve obter o `SVsTextManager` do shell do Visual Studio para obter o ativo `IVsTextView`.  
  
    ```csharp  
    private void AddAdornmentHandler(object sender, EventArgs e)  
    {  
        IVsTextManager txtMgr = (IVsTextManager)ServiceProvider.GetService(typeof(SVsTextManager));  
        IVsTextView vTextView = null;  
        int mustHaveFocus = 1;  
        txtMgr.GetActiveView(mustHaveFocus, null, out vTextView);  
    }  
    ```  
  
5.  Se este modo de exibição de texto for uma instância de uma exibição de texto do editor, você pode convertê-lo para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData> da interface e, em seguida, obtenha a <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> e seus respectivos <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>. Use o <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> para chamar o `Connector.Execute()` método, que obtém o provedor do adorno de comentário e adiciona o adorno. Agora, o manipulador de comandos deve ser assim:  
  
    ```csharp  
    private void AddAdornmentHandler(object sender, EventArgs e)  
    {  
        IVsTextManager txtMgr = (IVsTextManager)ServiceProvider.GetService(typeof(SVsTextManager));  
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
  
6.  Defina o método de AddAdornmentHandler como o manipulador para o comando AddAdornment no construtor AddAdornment.  
  
    ```csharp  
    private AddAdornment(Package package)  
    {  
        if (package == null)  
        {  
            throw new ArgumentNullException(nameof(package));  
        }  
  
        this.package = package;  
  
        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
        if (commandService != null)  
        {  
            CommandID menuCommandID = new CommandID(MenuGroup, CommandId);  
            EventHandler eventHandler = this.AddAdornmentHandler;  
            MenuCommand menuItem = new MenuCommand(eventHandler, menuCommandID);  
            commandService.AddCommand(menuItem);  
        }  
    }  
    ```  
  
## <a name="building-and-testing-the-code"></a>Compilar e testar o código  
  
1.  Compile a solução e inicie a depuração. A instância experimental deve aparecer.  
  
2.  Crie um arquivo de texto. Digite algum texto e, em seguida, selecioná-lo.  
  
3.  Sobre o **ferramentas** menu, clique em **invocar adorno adicionar**. Um balão deve ser exibido no lado direito da janela de texto e deve conter o texto que se parece com o texto a seguir.  
  
     Seu nome de usuário  
  
     Fourscore...  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Vincular um tipo de conteúdo a uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

