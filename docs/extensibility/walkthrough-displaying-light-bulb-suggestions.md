---
title: 'Walkthrough: exibindo sugestões de lâmpada | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 99e5566d-450e-4660-9bca-454e1c056a02
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 153eda065b9a6e845a39c35aaae34bbe1745f7a8
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905001"
---
# <a name="walkthrough-display-light-bulb-suggestions"></a>Walkthrough: Exibir sugestões de lâmpada
Lâmpadas são ícones no editor do Visual Studio que se expandem para exibir um conjunto de ações, por exemplo, correções de problemas identificados pelos analisadores de código internos ou refatoração de código.

 Nos editores do Visual C# e do Visual Basic, você também pode usar o .NET Compiler Platform ("Roslyn") para gravar e empacotar seus próprios analisadores de código com ações que exibem lâmpadas claras automaticamente. Para obter mais informações, consulte:

- [Como: escrever um diagnóstico e uma correção de código em C#](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix)

- [Como: escrever um diagnóstico de Visual Basic e correção de código](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-Visual-Basic-Analyzer-and-Code-Fix)

  Outras linguagens, como C++, também fornecem lâmpadas para algumas ações rápidas, como uma sugestão para criar uma implementação de stub dessa função.

  Esta é a aparência de uma lâmpada. Em um projeto Visual Basic ou Visual C#, um ondulado vermelho aparece sob um nome de variável quando é inválido. Se você passar o mouse sobre o identificador inválido, uma lâmpada aparecerá próximo ao cursor.

  ![lâmpada](../extensibility/media/lightbulb.png "Lâmpadas")

  Se você clicar na seta para baixo pela lâmpada, um conjunto de ações sugeridas será exibido, junto com uma visualização da ação selecionada. Nesse caso, ele mostra as alterações feitas no seu código se você executar a ação.

  ![visualização de lâmpada](../extensibility/media/lightbulbpreview.png "LightBulbPreview")

  Você pode usar lâmpadas leves para fornecer suas próprias ações sugeridas. Por exemplo, você pode fornecer ações para mover chaves de abertura para uma nova linha ou movê-las para o final da linha anterior. A instrução a seguir mostra como criar uma lâmpada que aparece na palavra atual e tem duas ações sugeridas: **converter em maiúsculas** e **converter em**minúsculas.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio do centro de download. Ele está incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-managed-extensibility-framework-mef-project"></a>Criar um projeto Managed Extensibility Framework (MEF)

1. Crie um projeto VSIX em C#. (Na caixa de diálogo **novo projeto** , selecione **Visual C#/extensibilidade**e, em seguida, **projeto VSIX**.) Nomeie a solução `LightBulbTest` .

2. Adicione um modelo de item de **classificação do editor** ao projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).

3. Exclua os arquivos de classe existentes.

4. Adicione a seguinte referência ao projeto e defina **Copy local** como `False` :

     *Microsoft. VisualStudio. Language. IntelliSense*

5. Adicione um novo arquivo de classe e nomeie-o **LightBulbTest**.

6. Adicione o seguinte usando as orientações:

    ```csharp
    using System;
    using System.Linq;
    using System.Collections.Generic;
    using System.Threading.Tasks;
    using Microsoft.VisualStudio.Language.Intellisense;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Operations;
    using Microsoft.VisualStudio.Utilities;
    using System.ComponentModel.Composition;
    using System.Threading;

    ```

## <a name="implement-the-light-bulb-source-provider"></a>Implementar o provedor de origem de lâmpada

1. No arquivo da classe *LightBulbTest.cs* , exclua a classe LightBulbTest. Adicione uma classe chamada **TestSuggestedActionsSourceProvider** que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider> . Exporte-o com um nome de **ações sugeridas de teste** e um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "texto".

    ```csharp
    [Export(typeof(ISuggestedActionsSourceProvider))]
    [Name("Test Suggested Actions")]
    [ContentType("text")]
    internal class TestSuggestedActionsSourceProvider : ISuggestedActionsSourceProvider
    ```

2. Dentro da classe do provedor de origem, importe o <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> e adicione-o como uma propriedade.

    ```csharp
    [Import(typeof(ITextStructureNavigatorSelectorService))]
    internal ITextStructureNavigatorSelectorService NavigatorService { get; set; }
    ```

3. Implemente o <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider.CreateSuggestedActionsSource%2A> método para retornar um <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> objeto. A fonte é discutida na próxima seção.

    ```csharp
    public ISuggestedActionsSource CreateSuggestedActionsSource(ITextView textView, ITextBuffer textBuffer)
    {
        if (textBuffer == null || textView == null)
        {
            return null;
        }
        return new TestSuggestedActionsSource(this, textView, textBuffer);
    }
    ```

## <a name="implement-the-isuggestedactionsource"></a>Implementar o ISuggestedActionSource
 A origem da ação sugerida é responsável por coletar o conjunto de ações sugeridas e adicioná-las no contexto certo. Nesse caso, o contexto é a palavra atual e as ações sugeridas são **UpperCaseSuggestedAction** e **LowerCaseSuggestedAction**, que é discutido na seção a seguir.

1. Adicione uma classe **TestSuggestedActionsSource** que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> .

    ```csharp
    internal class TestSuggestedActionsSource : ISuggestedActionsSource
    ```

2. Adicione campos particulares e somente leitura para o provedor de origem de ação sugerido, o buffer de texto e a exibição de texto.

    ```csharp
    private readonly TestSuggestedActionsSourceProvider m_factory;
    private readonly ITextBuffer m_textBuffer;
    private readonly ITextView m_textView;
    ```

3. Adicione um construtor que define os campos particulares.

    ```csharp
    public TestSuggestedActionsSource(TestSuggestedActionsSourceProvider testSuggestedActionsSourceProvider, ITextView textView, ITextBuffer textBuffer)
    {
        m_factory = testSuggestedActionsSourceProvider;
        m_textBuffer = textBuffer;
        m_textView = textView;
    }
    ```

4. Adicione um método particular que retorne a palavra que está no cursor no momento. O método a seguir examina o local atual do cursor e solicita ao navegador de estrutura de texto a extensão da palavra. Se o cursor estiver em uma palavra, o <xref:Microsoft.VisualStudio.Text.Operations.TextExtent> será retornado no parâmetro out; caso contrário, o `out` parâmetro será `null` e o método retornará `false` .

    ```csharp
    private bool TryGetWordUnderCaret(out TextExtent wordExtent)
    {
        ITextCaret caret = m_textView.Caret;
        SnapshotPoint point;

        if (caret.Position.BufferPosition > 0)
        {
            point = caret.Position.BufferPosition - 1;
        }
        else
        {
            wordExtent = default(TextExtent);
            return false;
        }

        ITextStructureNavigator navigator = m_factory.NavigatorService.GetTextStructureNavigator(m_textBuffer);

        wordExtent = navigator.GetExtentOfWord(point);
        return true;
    }
    ```

5. Implementar o método de <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.HasSuggestedActionsAsync%2A> . O editor chama esse método para descobrir se deseja exibir a lâmpada. Essa chamada é feita com frequência, por exemplo, sempre que o cursor se move de uma linha para outra ou quando o mouse passa sobre um erro rabiscado. É assíncrono para permitir que outras operações de interface do usuário sejam executadas enquanto esse método está funcionando. Na maioria dos casos, esse método precisa executar alguma análise e análise da linha atual, para que o processamento possa levar algum tempo.

     Nessa implementação, ele obtém de forma assíncrona o <xref:Microsoft.VisualStudio.Text.Operations.TextExtent> e determina se a extensão é significativa, como em, se ela tem algum texto diferente de espaço em branco.

    ```csharp
    public Task<bool> HasSuggestedActionsAsync(ISuggestedActionCategorySet requestedActionCategories, SnapshotSpan range, CancellationToken cancellationToken)
    {
        return Task.Factory.StartNew(() =>
        {
            TextExtent extent;
            if (TryGetWordUnderCaret(out extent))
            {
                // don't display the action if the extent has whitespace
                return extent.IsSignificant;
              }
            return false;
        });
    }
    ```

6. Implemente o <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.GetSuggestedActions%2A> método, que retorna uma matriz de <xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet> objetos que contêm os diferentes <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction> objetos. Esse método é chamado quando a lâmpada é expandida.

    > [!WARNING]
    > Você deve certificar-se de que as implementações do `HasSuggestedActionsAsync()` e `GetSuggestedActions()` são consistentes; ou seja, se `HasSuggestedActionsAsync()` retorna `true` , `GetSuggestedActions()` deve ter algumas ações para exibir. Em muitos casos, `HasSuggestedActionsAsync()` é chamado pouco antes `GetSuggestedActions()` , mas esse não é sempre o caso. Por exemplo, se o usuário invocar as ações de lâmpada, pressionar (**Ctrl +** .) somente `GetSuggestedActions()` é chamado.

    ```csharp
    public IEnumerable<SuggestedActionSet> GetSuggestedActions(ISuggestedActionCategorySet requestedActionCategories, SnapshotSpan range, CancellationToken cancellationToken)
    {
        TextExtent extent;
        if (TryGetWordUnderCaret(out extent) && extent.IsSignificant)
        {
            ITrackingSpan trackingSpan = range.Snapshot.CreateTrackingSpan(extent.Span, SpanTrackingMode.EdgeInclusive);
            var upperAction = new UpperCaseSuggestedAction(trackingSpan);
            var lowerAction = new LowerCaseSuggestedAction(trackingSpan);
            return new SuggestedActionSet[] { new SuggestedActionSet(new ISuggestedAction[] { upperAction, lowerAction }) };
        }
        return Enumerable.Empty<SuggestedActionSet>();
    }
    ```

7. Defina um `SuggestedActionsChanged` evento.

    ```csharp
    public event EventHandler<EventArgs> SuggestedActionsChanged;
    ```

8. Para concluir a implementação, adicione implementações para `Dispose()` os `TryGetTelemetryId()` métodos e. Você não quer fazer telemetria, portanto, basta retornar `false` e definir o GUID como `Empty` .

    ```csharp
    public void Dispose()
    {
    }

    public bool TryGetTelemetryId(out Guid telemetryId)
    {
        // This is a sample provider and doesn't participate in LightBulb telemetry
        telemetryId = Guid.Empty;
        return false;
    }
    ```

## <a name="implement-light-bulb-actions"></a>Implementar ações de lâmpada

1. No projeto, adicione uma referência a *Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime.dll* e defina **Copiar local** como `False` .

2. Crie duas classes, o primeiro nome `UpperCaseSuggestedAction` e o segundo nomeado `LowerCaseSuggestedAction` . Ambas as classes implementam <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction> .

    ```csharp
    internal class UpperCaseSuggestedAction : ISuggestedAction
    internal class LowerCaseSuggestedAction : ISuggestedAction
    ```

     Ambas as classes são semelhantes, exceto que uma chamada <xref:System.String.ToUpper%2A> e as outras chamadas <xref:System.String.ToLower%2A> . As etapas a seguir abrangem apenas a classe de ação de letras maiúsculas, mas você deve implementar ambas as classes. Use as etapas para implementar a ação em maiúsculas como um padrão para implementar a ação em minúsculas.

3. Adicione as seguintes diretivas using para essas classes:

    ```csharp
    using Microsoft.VisualStudio.Imaging.Interop;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Documents;
    using System.Windows.Media;

    ```

4. Declare um conjunto de campos privados.

    ```csharp
    private ITrackingSpan m_span;
    private string m_upper;
    private string m_display;
    private ITextSnapshot m_snapshot;
    ```

5. Adicione um construtor que defina os campos.

    ```csharp
    public UpperCaseSuggestedAction(ITrackingSpan span)
    {
        m_span = span;
        m_snapshot = span.TextBuffer.CurrentSnapshot;
        m_upper = span.GetText(m_snapshot).ToUpper();
        m_display = string.Format("Convert '{0}' to upper case", span.GetText(m_snapshot));
    }
    ```

6. Implemente o <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetPreviewAsync%2A> método para que ele exiba a visualização da ação.

    ```csharp
    public Task<object> GetPreviewAsync(CancellationToken cancellationToken)
    {
        var textBlock = new TextBlock();
        textBlock.Padding = new Thickness(5);
        textBlock.Inlines.Add(new Run() { Text = m_upper });
        return Task.FromResult<object>(textBlock);
    }
    ```

7. Implemente o <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetActionSetsAsync%2A> método para que ele retorne uma <xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet> Enumeração vazia.

    ```csharp
    public Task<IEnumerable<SuggestedActionSet>> GetActionSetsAsync(CancellationToken cancellationToken)
    {
        return Task.FromResult<IEnumerable<SuggestedActionSet>>(null);
    }
    ```

8. Implemente as propriedades da seguinte maneira.

    ```csharp
    public bool HasActionSets
    {
        get { return false; }
    }
    public string DisplayText
    {
        get { return m_display; }
    }
    public ImageMoniker IconMoniker
    {
       get { return default(ImageMoniker); }
    }
    public string IconAutomationText
    {
        get
        {
            return null;
        }
    }
    public string InputGestureText
    {
        get
        {
            return null;
        }
    }
    public bool HasPreview
    {
        get { return true; }
    }
    ```

9. Implemente o <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.Invoke%2A> método substituindo o texto no span por seu equivalente em maiúsculas.

    ```csharp
    public void Invoke(CancellationToken cancellationToken)
    {
        m_span.TextBuffer.Replace(m_span.GetSpan(m_snapshot), m_upper);
    }
    ```

    > [!WARNING]
    > O método **Invoke** da ação de lâmpada não é esperado para mostrar a interface do usuário. Se a ação abrir a nova interface do usuário (por exemplo, uma caixa de diálogo de visualização ou seleção), não exiba a interface do usuário diretamente de dentro do método **Invoke** , mas, em vez disso, agende para exibir a interface do usuário depois de retornar de **Invoke**.

10. Para concluir a implementação, adicione os `Dispose()` `TryGetTelemetryId()` métodos e.

    ```csharp
    public void Dispose()
    {
    }

    public bool TryGetTelemetryId(out Guid telemetryId)
    {
        // This is a sample action and doesn't participate in LightBulb telemetry
        telemetryId = Guid.Empty;
        return false;
    }
    ```

11. Não se esqueça de fazer a mesma coisa para `LowerCaseSuggestedAction` alterar o texto de exibição para "converter" {0} em letras minúsculas "e a chamada <xref:System.String.ToUpper%2A> para <xref:System.String.ToLower%2A> .

## <a name="build-and-test-the-code"></a>Compilar e testar o código
 Para testar esse código, crie a solução LightBulbTest e execute-a na instância experimental.

1. Compile a solução.

2. Quando você executa esse projeto no depurador, uma segunda instância do Visual Studio é iniciada.

3. Crie um arquivo de texto e digite algum texto. Você deve ver uma lâmpada à esquerda do texto.

     ![testar a lâmpada](../extensibility/media/testlightbulb.png "TestLIghtBulb")

4. Aponte para a lâmpada. Você deve ver uma seta para baixo.

5. Quando você clica na lâmpada, duas ações sugeridas devem ser exibidas, juntamente com a visualização da ação selecionada.

     ![lâmpada de teste, expandida](../extensibility/media/testlightbulbexpanded.gif "TestLIghtBulbExpanded")

6. Se você clicar na primeira ação, todo o texto na palavra atual deverá ser convertido em letras maiúsculas. Se você clicar na segunda ação, todo o texto deverá ser convertido em letras minúsculas.
