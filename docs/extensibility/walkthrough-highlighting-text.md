---
title: 'Walkthrough: realçando texto | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - highlight text
ms.assetid: 64b772ad-4392-42e9-a237-5137f0384bf0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3bfd94a55fe207f5c20e2ed1e5630d62c73c9ba2
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904727"
---
# <a name="walkthrough-highlight-text"></a>Walkthrough: realçar texto
Você pode adicionar diferentes efeitos visuais ao editor criando partes do componente Managed Extensibility Framework (MEF). Este tutorial mostra como realçar todas as ocorrências da palavra atual em um arquivo de texto. Se uma palavra ocorrer mais de uma vez em um arquivo de texto e você posicionar o cursor em uma ocorrência, todas as ocorrências serão realçadas.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio do centro de download. Ele está incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-mef-project"></a>Criar um projeto do MEF

1. Crie um projeto VSIX em C#. (Na caixa de diálogo **novo projeto** , selecione **Visual C#/extensibilidade**e, em seguida, **projeto VSIX**.) Nomeie a solução `HighlightWordTest` .

2. Adicione um modelo de item de classificação do editor ao projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).

3. Exclua os arquivos de classe existentes.

## <a name="define-a-textmarkertag"></a>Definir um TextMarkerTag
 A primeira etapa ao realçar o texto é a subclasse <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> e definir sua aparência.

### <a name="to-define-a-textmarkertag-and-a-markerformatdefinition"></a>Para definir um TextMarkerTag e um MarkerFormatDefinition

1. Adicione um arquivo de classe e nomeie-o **HighlightWordTag**.

2. Adicione as seguintes referências:

    1. Microsoft. VisualStudio. CoreUtility

    2. Microsoft. VisualStudio. Text. Data

    3. Microsoft. VisualStudio. Text. Logic

    4. Microsoft. VisualStudio. Text. UI

    5. Microsoft. VisualStudio. Text. UI. WPF

    6. System. ComponentModel. composição

    7. Presentation. Core

    8. Presentation. Framework

3. Importe os namespaces a seguir.

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using System.Linq;
    using System.Threading;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Classification;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Operations;
    using Microsoft.VisualStudio.Text.Tagging;
    using Microsoft.VisualStudio.Utilities;
    using System.Windows.Media;
    ```

4. Crie uma classe que herde de <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> e nomeie-a `HighlightWordTag` .

    ```csharp
    internal class HighlightWordTag : TextMarkerTag
    {

    }
    ```

5. Crie uma segunda classe que herde de <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition> e nomeie-a `HighlightWordFormatDefinition` . Para usar essa definição de formato para sua marca, você deve exportá-la com os seguintes atributos:

    - <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: marcações use isto para fazer referência a este formato

    - <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: isso faz com que o formato apareça na interface do usuário

    ```csharp

    [Export(typeof(EditorFormatDefinition))]
    [Name("MarkerFormatDefinition/HighlightWordFormatDefinition")]
    [UserVisible(true)]
    internal class HighlightWordFormatDefinition : MarkerFormatDefinition
    {

    }
    ```

6. No construtor para HighlightWordFormatDefinition, defina seu nome de exibição e aparência. A propriedade Background define a cor de preenchimento, enquanto a propriedade Foreground define a cor da borda.

    ```csharp
    public HighlightWordFormatDefinition()
    {
                this.BackgroundColor = Colors.LightBlue;
        this.ForegroundColor = Colors.DarkBlue;
        this.DisplayName = "Highlight Word";
        this.ZOrder = 5;
    }
    ```

7. No construtor para HighlightWordTag, passe o nome da definição de formato que você criou.

    ```
    public HighlightWordTag() : base("MarkerFormatDefinition/HighlightWordFormatDefinition") { }
    ```

## <a name="implement-an-itagger"></a>Implementar um ITagger
 A próxima etapa é implementar a <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> interface. Essa interface atribui, a um determinado buffer de texto, marcas que fornecem realce de texto e outros efeitos visuais.

### <a name="to-implement-a-tagger"></a>Para implementar um marcador

1. Crie uma classe que implemente o <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> tipo `HighlightWordTag` e nomeie-a `HighlightWordTagger` .

    ```csharp
    internal class HighlightWordTagger : ITagger<HighlightWordTag>
    {

    }
    ```

2. Adicione os seguintes campos e propriedades particulares à classe:

    - Um <xref:Microsoft.VisualStudio.Text.Editor.ITextView> , que corresponde à exibição de texto atual.

    - Um <xref:Microsoft.VisualStudio.Text.ITextBuffer> , que corresponde ao buffer de texto que está em sua exibição de texto.

    - Um <xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService> , que é usado para localizar texto.

    - Um <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> , que tem métodos para navegar em intervalos de texto.

    - A <xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection> , que contém o conjunto de palavras a ser realçado.

    - Um <xref:Microsoft.VisualStudio.Text.SnapshotSpan> , que corresponde à palavra atual.

    - Um <xref:Microsoft.VisualStudio.Text.SnapshotPoint> , que corresponde à posição atual do cursor.

    - Um objeto de bloqueio.

    ```csharp
    ITextView View { get; set; }
    ITextBuffer SourceBuffer { get; set; }
    ITextSearchService TextSearchService { get; set; }
    ITextStructureNavigator TextStructureNavigator { get; set; }
    NormalizedSnapshotSpanCollection WordSpans { get; set; }
    SnapshotSpan? CurrentWord { get; set; }
    SnapshotPoint RequestedPoint { get; set; }
    object updateLock = new object();

    ```

3. Adicione um construtor que inicializa as propriedades listadas anteriormente e <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> adiciona <xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged> manipuladores de eventos e.

    ```csharp
    public HighlightWordTagger(ITextView view, ITextBuffer sourceBuffer, ITextSearchService textSearchService,
    ITextStructureNavigator textStructureNavigator)
    {
        this.View = view;
        this.SourceBuffer = sourceBuffer;
        this.TextSearchService = textSearchService;
        this.TextStructureNavigator = textStructureNavigator;
        this.WordSpans = new NormalizedSnapshotSpanCollection();
        this.CurrentWord = null;
        this.View.Caret.PositionChanged += CaretPositionChanged;
        this.View.LayoutChanged += ViewLayoutChanged;
    }

    ```

4. Os manipuladores de eventos chamam o `UpdateAtCaretPosition` método.

    ```csharp
    void ViewLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)
    {
        // If a new snapshot wasn't generated, then skip this layout 
        if (e.NewSnapshot != e.OldSnapshot)
        {
            UpdateAtCaretPosition(View.Caret.Position);
        }
    }

    void CaretPositionChanged(object sender, CaretPositionChangedEventArgs e)
    {
        UpdateAtCaretPosition(e.NewPosition);
    }
    ```

5. Você também deve adicionar um `TagsChanged` evento chamado pelo método Update.

     [!code-csharp[VSSDKHighlightWordTest#10](../extensibility/codesnippet/CSharp/walkthrough-highlighting-text_1.cs)]
     [!code-vb[VSSDKHighlightWordTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-highlighting-text_1.vb)]

6. O `UpdateAtCaretPosition()` método localiza todas as palavras no buffer de texto que são idênticas à palavra onde o cursor está posicionado e constrói uma lista de <xref:Microsoft.VisualStudio.Text.SnapshotSpan> objetos que correspondem às ocorrências da palavra. Em seguida, ele chama `SynchronousUpdate` , que gera o `TagsChanged` evento.

    ```csharp
    void UpdateAtCaretPosition(CaretPosition caretPosition)
    {
        SnapshotPoint? point = caretPosition.Point.GetPoint(SourceBuffer, caretPosition.Affinity);

        if (!point.HasValue)
            return;

        // If the new caret position is still within the current word (and on the same snapshot), we don't need to check it 
        if (CurrentWord.HasValue
            && CurrentWord.Value.Snapshot == View.TextSnapshot
            && point.Value >= CurrentWord.Value.Start
            && point.Value <= CurrentWord.Value.End)
        {
            return;
        }

        RequestedPoint = point.Value;
        UpdateWordAdornments();
    }

    void UpdateWordAdornments()
    {
        SnapshotPoint currentRequest = RequestedPoint;
        List<SnapshotSpan> wordSpans = new List<SnapshotSpan>();
        //Find all words in the buffer like the one the caret is on
        TextExtent word = TextStructureNavigator.GetExtentOfWord(currentRequest);
        bool foundWord = true;
        //If we've selected something not worth highlighting, we might have missed a "word" by a little bit
        if (!WordExtentIsValid(currentRequest, word))
        {
            //Before we retry, make sure it is worthwhile 
            if (word.Span.Start != currentRequest
                 || currentRequest == currentRequest.GetContainingLine().Start
                 || char.IsWhiteSpace((currentRequest - 1).GetChar()))
            {
                foundWord = false;
            }
            else
            {
                // Try again, one character previous.  
                //If the caret is at the end of a word, pick up the word.
                word = TextStructureNavigator.GetExtentOfWord(currentRequest - 1);

                //If the word still isn't valid, we're done 
                if (!WordExtentIsValid(currentRequest, word))
                    foundWord = false;
            }
        }

        if (!foundWord)
        {
            //If we couldn't find a word, clear out the existing markers
            SynchronousUpdate(currentRequest, new NormalizedSnapshotSpanCollection(), null);
            return;
        }

        SnapshotSpan currentWord = word.Span;
        //If this is the current word, and the caret moved within a word, we're done. 
        if (CurrentWord.HasValue && currentWord == CurrentWord)
            return;

        //Find the new spans
        FindData findData = new FindData(currentWord.GetText(), currentWord.Snapshot);
        findData.FindOptions = FindOptions.WholeWord | FindOptions.MatchCase;

        wordSpans.AddRange(TextSearchService.FindAll(findData));

        //If another change hasn't happened, do a real update 
        if (currentRequest == RequestedPoint)
            SynchronousUpdate(currentRequest, new NormalizedSnapshotSpanCollection(wordSpans), currentWord);
    }
    static bool WordExtentIsValid(SnapshotPoint currentRequest, TextExtent word)
    {
        return word.IsSignificant
            && currentRequest.Snapshot.GetText(word.Span).Any(c => char.IsLetter(c));
    }

    ```

7. O `SynchronousUpdate` executa uma atualização síncrona nas `WordSpans` Propriedades e e `CurrentWord` gera o `TagsChanged` evento.

    ```csharp
    void SynchronousUpdate(SnapshotPoint currentRequest, NormalizedSnapshotSpanCollection newSpans, SnapshotSpan? newCurrentWord)
    {
        lock (updateLock)
        {
            if (currentRequest != RequestedPoint)
                return;

            WordSpans = newSpans;
            CurrentWord = newCurrentWord;

            var tempEvent = TagsChanged;
            if (tempEvent != null)
                tempEvent(this, new SnapshotSpanEventArgs(new SnapshotSpan(SourceBuffer.CurrentSnapshot, 0, SourceBuffer.CurrentSnapshot.Length)));
        }
    }
    ```

8. Você deve implementar o <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> método. Esse método usa uma coleção de <xref:Microsoft.VisualStudio.Text.SnapshotSpan> objetos e retorna uma enumeração de Spans de marca.

     No C#, implemente esse método como um iterador yield, que habilita a avaliação lenta (ou seja, a avaliação do conjunto somente quando itens individuais são acessados) das marcas. Em Visual Basic, adicione as marcas a uma lista e retorne a lista.

     Aqui, o método retorna um <xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601> objeto que tem um "azul" <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> , que fornece um plano de fundo azul.

    ```csharp
    public IEnumerable<ITagSpan<HighlightWordTag>> GetTags(NormalizedSnapshotSpanCollection spans)
    {
        if (CurrentWord == null)
            yield break;

        // Hold on to a "snapshot" of the word spans and current word, so that we maintain the same
        // collection throughout
        SnapshotSpan currentWord = CurrentWord.Value;
        NormalizedSnapshotSpanCollection wordSpans = WordSpans;

        if (spans.Count == 0 || wordSpans.Count == 0)
            yield break;

        // If the requested snapshot isn't the same as the one our words are on, translate our spans to the expected snapshot 
        if (spans[0].Snapshot != wordSpans[0].Snapshot)
        {
            wordSpans = new NormalizedSnapshotSpanCollection(
                wordSpans.Select(span => span.TranslateTo(spans[0].Snapshot, SpanTrackingMode.EdgeExclusive)));

            currentWord = currentWord.TranslateTo(spans[0].Snapshot, SpanTrackingMode.EdgeExclusive);
        }

        // First, yield back the word the cursor is under (if it overlaps) 
        // Note that we'll yield back the same word again in the wordspans collection; 
        // the duplication here is expected. 
        if (spans.OverlapsWith(new NormalizedSnapshotSpanCollection(currentWord)))
            yield return new TagSpan<HighlightWordTag>(currentWord, new HighlightWordTag());

        // Second, yield all the other words in the file 
        foreach (SnapshotSpan span in NormalizedSnapshotSpanCollection.Overlap(spans, wordSpans))
        {
            yield return new TagSpan<HighlightWordTag>(span, new HighlightWordTag());
        }
    }
    ```

## <a name="create-a-tagger-provider"></a>Criar um provedor de marca
 Para criar o seu marcador, você deve implementar um <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> . Essa classe é uma parte de componente do MEF, portanto, você deve definir os atributos corretos para que essa extensão seja reconhecida.

> [!NOTE]
> Para obter mais informações sobre o MEF, consulte [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index).

### <a name="to-create-a-tagger-provider"></a>Para criar um provedor de marcador

1. Crie uma classe chamada `HighlightWordTaggerProvider` que implementa <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> e exporte-a com um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "texto" e um <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> de <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> .

    ```csharp
    [Export(typeof(IViewTaggerProvider))]
    [ContentType("text")]
    [TagType(typeof(TextMarkerTag))]
    internal class HighlightWordTaggerProvider : IViewTaggerProvider
    { }
    ```

2. Você deve importar dois serviços do editor, o <xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService> e o <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> , para instanciar o marcador.

    ```csharp
    [Import]
    internal ITextSearchService TextSearchService { get; set; }

    [Import]
    internal ITextStructureNavigatorSelectorService TextStructureNavigatorSelector { get; set; }

    ```

3. Implemente o <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A> método para retornar uma instância do `HighlightWordTagger` .

    ```csharp
    public ITagger<T> CreateTagger<T>(ITextView textView, ITextBuffer buffer) where T : ITag
    {
        //provide highlighting only on the top buffer 
        if (textView.TextBuffer != buffer)
            return null;

        ITextStructureNavigator textStructureNavigator =
            TextStructureNavigatorSelector.GetTextStructureNavigator(buffer);

        return new HighlightWordTagger(textView, buffer, TextSearchService, textStructureNavigator) as ITagger<T>;
    }
    ```

## <a name="build-and-test-the-code"></a>Compilar e testar o código
 Para testar esse código, crie a solução HighlightWordTest e execute-a na instância experimental.

### <a name="to-build-and-test-the-highlightwordtest-solution"></a>Para compilar e testar a solução HighlightWordTest

1. Compile a solução.

2. Quando você executa esse projeto no depurador, uma segunda instância do Visual Studio é iniciada.

3. Crie um arquivo de texto e digite algum texto no qual as palavras sejam repetidas, por exemplo, "Olá Olá Olá".

4. Posicione o cursor em uma das ocorrências de "Olá". Cada ocorrência deve ser realçada em azul.

## <a name="see-also"></a>Confira também
- [Walkthrough: vincular um tipo de conteúdo a uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
