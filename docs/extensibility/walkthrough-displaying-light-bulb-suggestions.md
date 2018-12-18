---
title: 'Passo a passo: Exibir sugestões de lâmpada | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 99e5566d-450e-4660-9bca-454e1c056a02
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 16b9d56daab6eda1ef1cd9c31d8cc4d720f9a08e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49875886"
---
# <a name="walkthrough-display-light-bulb-suggestions"></a>Passo a passo: Exibir sugestões de lâmpada
As lâmpadas são ícones que expandem para exibir um conjunto de ações, por exemplo, correções para problemas identificados pelo analisadores de código internos ou refatoração de código no editor do Visual Studio.  
  
 Nos editores do Visual c# e Visual Basic, você também pode usar o .NET Compiler Platform ("Roslyn") para gravar e empacotar seus próprios analisadores de código com as ações que exibem as lâmpadas automaticamente. Para obter mais informações, consulte:  
  
- [Como Gravar um c# diagnóstico e correção de código](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix)  
  
- [Como Gravar um diagnóstico do Visual Basic e correção de código](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-Visual-Basic-Analyzer-and-Code-Fix)  
  
  Outras linguagens como C++ também fornecem as lâmpadas para algumas ações rápidas, por exemplo, uma sugestão para criar uma implementação de stub dessa função.  
  
  Uma lâmpada é semelhante ao seguinte. Em um projeto do Visual Basic ou Visual c#, uma linha ondulada vermelha aparece sob um nome de variável quando ela é inválida. Se você passar o mouse sobre o identificador inválido, uma lâmpada aparece perto do cursor.  
  
  ![lâmpada](../extensibility/media/lightbulb.png "lâmpada")  
  
  Se você clicar na seta para baixo, a lâmpada, um conjunto de ações sugeridas que é exibido junto com uma visualização da ação selecionada. Nesse caso, ele mostra as alterações feitas em seu código se você executar a ação.  
  
  ![visualização da lâmpada](../extensibility/media/lightbulbpreview.png "LightBulbPreview")  
  
  Você pode usar as lâmpadas para fornecer suas próprias ações sugeridas. Por exemplo, você pode fornecer ações para mover as chaves para uma nova linha de abertura ou movê-los ao final da linha anterior. A instrução a seguir mostra como criar uma lâmpada que aparece na palavra atual e tem duas ações sugeridas: **convertida em letras maiusculas** e **converter em letras minúsculas**.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ela está incluída como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="create-a-managed-extensibility-framework-mef-project"></a>Criar um projeto de Managed Extensibility Framework (MEF)  
  
1.  Crie um projeto de VSIX em C#. (Na **novo projeto** caixa de diálogo, selecione **Visual c# / extensibilidade**, em seguida, **projeto VSIX**.) Nomeie a solução `LightBulbTest`.  
  
2.  Adicionar um **classificador de Editor** modelo de item ao projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de item editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
3.  Exclua os arquivos de classe existentes.  
  
4.  Adicione a seguinte referência ao projeto e defina **Copy Local** para `False`:  
  
     *Microsoft.VisualStudio.Language.Intellisense*  
  
5.  Adicione um novo arquivo de classe e denomine **LightBulbTest**.  
  
6.  Adicione as seguintes instruções using:  
  
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
  
## <a name="implement-the-light-bulb-source-provider"></a>Implementar o provedor de código-fonte da lâmpada  
  
1.  No *LightBulbTest.cs* arquivo de classe, excluir a classe LightBulbTest. Adicione uma classe chamada **TestSuggestedActionsSourceProvider** que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>. Exportá-lo com um nome de **ações sugeridas de teste** e um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "text".  
  
    ```csharp  
    [Export(typeof(ISuggestedActionsSourceProvider))]  
    [Name("Test Suggested Actions")]  
    [ContentType("text")]  
    internal class TestSuggestedActionsSourceProvider : ISuggestedActionsSourceProvider  
    ```  
  
2.  Dentro da classe de provedor de código-fonte, importe o <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> e adicioná-lo como uma propriedade.  
  
    ```csharp  
    [Import(typeof(ITextStructureNavigatorSelectorService))]  
    internal ITextStructureNavigatorSelectorService NavigatorService { get; set; }  
    ```  
  
3.  Implemente a <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider.CreateSuggestedActionsSource%2A> método para retornar um <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> objeto. A fonte é abordada na próxima seção.  
  
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
 A origem da ação sugerida é responsável por coletar o conjunto de ações sugeridas e adicioná-los no contexto certo. Nesse caso, o contexto é a palavra atual e são as ações sugeridas **UpperCaseSuggestedAction** e **LowerCaseSuggestedAction**, que é discutido na seção a seguir.  
  
1.  Adicione uma classe **TestSuggestedActionsSource** que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>.  
  
    ```csharp  
    internal class TestSuggestedActionsSource : ISuggestedActionsSource  
    ```  
  
2.  Adicione campos privados, somente leitura para o provedor de origem da ação sugerida, o buffer de texto e a exibição de texto.  
  
    ```csharp  
    private readonly TestSuggestedActionsSourceProvider m_factory;  
    private readonly ITextBuffer m_textBuffer;  
    private readonly ITextView m_textView;  
    ```  
  
3.  Adicione um construtor que define os campos particulares.  
  
    ```csharp  
    public TestSuggestedActionsSource(TestSuggestedActionsSourceProvider testSuggestedActionsSourceProvider, ITextView textView, ITextBuffer textBuffer)  
    {  
        m_factory = testSuggestedActionsSourceProvider;  
        m_textBuffer = textBuffer;  
        m_textView = textView;  
    }  
    ```  
  
4.  Adicione um método particular que retorna a palavra que está atualmente sob o cursor. O método a seguir examina o local atual do cursor e solicita que o navegador de estrutura de texto para a extensão da palavra. Se o cursor estiver sobre uma palavra, o <xref:Microsoft.VisualStudio.Text.Operations.TextExtent> é retornado no parâmetro de saída; caso contrário, o `out` parâmetro é `null` e o método retornará `false`.  
  
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
  
5.  Implementar o método de <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.HasSuggestedActionsAsync%2A> . O editor chama esse método para descobrir se deve exibir a lâmpada. Essa chamada é feita com frequência, por exemplo, sempre que o cursor se move de uma linha para outra, ou quando o mouse passa sobre um rabisco de erro. Ele é assíncrono para permitir que outras operações de interface do usuário executar enquanto esse método está funcionando. Na maioria dos casos, esse método precisa executar alguma análise e a análise da linha atual, portanto, o processamento pode levar algum tempo.  
  
     Nessa implementação, ele obtém de maneira assíncrona o <xref:Microsoft.VisualStudio.Text.Operations.TextExtent> e determina se a extensão é significativa, por exemplo, se ele tem algum texto que não seja espaço em branco.  
  
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
  
6.  Implemente a <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.GetSuggestedActions%2A> método, que retorna uma matriz de <xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet> objetos que contêm diferentes <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction> objetos. Esse método é chamado quando a lâmpada é expandida.  
  
    > [!WARNING]
    >  Assegure-se de que as implementações de `HasSuggestedActionsAsync()` e `GetSuggestedActions()` are consistente; que é, se `HasSuggestedActionsAsync()` retorna `true`, em seguida, `GetSuggestedActions()` deve ter algumas ações para exibir. Em muitos casos, `HasSuggestedActionsAsync()` é chamado antes `GetSuggestedActions()`, mas isso não é sempre o caso. Por exemplo, se o usuário invoca as ações de lâmpada pressionando (**CTRL +** .) só `GetSuggestedActions()` é chamado.  
  
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
  
7.  Definir um `SuggestedActionsChanged` eventos.  
  
    ```csharp  
    public event EventHandler<EventArgs> SuggestedActionsChanged;  
    ```  
  
8.  Para concluir a implementação, adicione as implementações para o `Dispose()` e `TryGetTelemetryId()` métodos. Você não quiser fazer a telemetria, portanto, apenas retornar `false` e defina o GUID para `Empty`.  
  
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
  
## <a name="implement-light-bulb-actions"></a>Implementar lâmpada de ações  
  
1.  No projeto, adicione uma referência ao *Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime.dll* e defina **Copy Local** para `False`.  
  
2.  Crie duas classes, a primeira chamada `UpperCaseSuggestedAction` e a segunda chamada `LowerCaseSuggestedAction`. Ambas as classes implementam <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction>.  
  
    ```csharp  
    internal class UpperCaseSuggestedAction : ISuggestedAction   
    internal class LowerCaseSuggestedAction : ISuggestedAction  
    ```  
  
     Ambas as classes são semelhantes, exceto que um chama <xref:System.String.ToUpper%2A> e as outras chamadas <xref:System.String.ToLower%2A>. As etapas a seguir abrangem apenas a classe de ação em maiusculas, mas você deve implementar as duas classes. Use as etapas para implementar a ação de letras maiusculas como um padrão para implementar a ação em minúsculas.  
  
3.  Adicione o seguinte usando instruções para essas classes:  
  
    ```csharp  
    using Microsoft.VisualStudio.Imaging.Interop;  
    using System.Windows;  
    using System.Windows.Controls;  
    using System.Windows.Documents;  
    using System.Windows.Media;  
  
    ```  
  
4.  Declare um conjunto de campos particulares.  
  
    ```csharp  
    private ITrackingSpan m_span;  
    private string m_upper;  
    private string m_display;  
    private ITextSnapshot m_snapshot;  
    ```  
  
5.  Adicione um construtor que define os campos.  
  
    ```csharp  
    public UpperCaseSuggestedAction(ITrackingSpan span)  
    {  
        m_span = span;  
        m_snapshot = span.TextBuffer.CurrentSnapshot;  
        m_upper = span.GetText(m_snapshot).ToUpper();  
        m_display = string.Format("Convert '{0}' to upper case", span.GetText(m_snapshot));  
    }  
    ```  
  
6.  Implementar o <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetPreviewAsync%2A> , de modo que ele exibe a visualização de ação.  
  
    ```csharp  
    public Task<object> GetPreviewAsync(CancellationToken cancellationToken)  
    {  
        var textBlock = new TextBlock();  
        textBlock.Padding = new Thickness(5);  
        textBlock.Inlines.Add(new Run() { Text = m_upper });  
        return Task.FromResult<object>(textBlock);  
    }  
    ```  
  
7.  Implemente a <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetActionSetsAsync%2A> método para que ele retorne um vazio <xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet> enumeração.  
  
    ```csharp  
    public Task<IEnumerable<SuggestedActionSet>> GetActionSetsAsync(CancellationToken cancellationToken)  
    {  
        return Task.FromResult<IEnumerable<SuggestedActionSet>>(null);  
    }  
    ```  
  
8.  Implemente as propriedades da seguinte maneira.  
  
    ```csharp  
    public bool HasActionSets  
    {  
        get { return false; }  
    }  
    public string DisplayText  
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
  
9. Implementar o <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.Invoke%2A> método, substituindo o texto no trecho com seu equivalente em maiusculas.  
  
    ```csharp  
    public void Invoke(CancellationToken cancellationToken)  
    {  
        m_span.TextBuffer.Replace(m_span.GetSpan(m_snapshot), m_upper);  
    }  
    ```  
  
    > [!WARNING]
    >  A ação de lâmpada **Invoke** método não é esperado para mostrar a interface do usuário. Se a ação de abrir nova interface do usuário (por exemplo, um diálogo Visualização ou a seleção), não exibem a interface do usuário diretamente de dentro do **Invoke** método, mas em vez disso, agendar para exibir sua interface do usuário depois de retornar do **Invoke**.  
  
10. Para concluir a implementação, adicione a `Dispose()` e `TryGetTelemetryId()` métodos.  
  
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
  
11. Não se esqueça de fazer a mesma coisa `LowerCaseSuggestedAction` alterando o texto de exibição para "converter '{0}' para letras minúsculas" e a chamada <xref:System.String.ToUpper%2A> para <xref:System.String.ToLower%2A>.  
  
## <a name="build-and-test-the-code"></a>Compilar e testar o código  
 Para testar esse código, compile a solução LightBulbTest e executá-lo na instância Experimental.  
  
1.  Compile a solução.  
  
2.  Quando você executar esse projeto no depurador, uma segunda instância do Visual Studio é iniciada.  
  
3.  Crie um arquivo de texto e digite algum texto. Você deve ver uma lâmpada à esquerda do texto.  
  
     ![testar a lâmpada](../extensibility/media/testlightbulb.png "TestLIghtBulb")  
  
4.  Apontar para a lâmpada. Você deve ver uma seta para baixo.  
  
5.  Quando você clicar na lâmpada, devem exibir duas ações sugeridas, juntamente com a visualização da ação selecionada.  
  
     ![testar a lâmpada expandida](../extensibility/media/testlightbulbexpanded.gif "TestLIghtBulbExpanded")  
  
6.  Se você clicar na primeira ação, todo o texto da palavra atual deve ser convertido em letras maiusculas. Se você clicar na segunda ação, todo o texto deve ser convertido em minúsculas.  
  
