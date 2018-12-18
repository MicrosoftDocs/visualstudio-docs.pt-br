---
title: Importações do Editor | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - services
ms.assetid: 8d096de3-33b4-427a-a122-4aeff8a72da0
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8ede17217dbac62bcc0086e6f4e5afca0cf9e0a0
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39637207"
---
# <a name="editor-imports"></a>Importações do Editor
Você pode importar um número de serviços do editor, fábricas e os agentes que fornecem a sua extensão com diferentes tipos de acesso para o editor de núcleo. Por exemplo, você pode importar o <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> para dar a você um <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> para um determinado tipo de conteúdo. (Este navegador permite que executar diferentes tipos de pesquisas em um buffer de texto).  
  
 Para usar uma importação de editor, importá-lo como um campo ou propriedade de uma classe que exporta uma parte do componente de Managed Extensibility Framework.  
  
> [!NOTE]
>  Para obter mais informações sobre o Managed Extensibility Framework, consulte [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index).  
  
## <a name="import-syntax"></a>Sintaxe de importação  
 O exemplo a seguir mostra como importar o editor de serviço de fábrica de opções.  
  
```  
[Import]  
internal IEditorOptionsFactoryService EditorOptions { get; set; }  
```  
  
 Se você deseja importar o serviço como um campo e não uma propriedade, você deve defini-lo `null` na declaração para evitar os avisos do compilador sobre não atribuir a uma variável:  
  
```  
[Import]  
internal IEditorOptionsFactoryService m_editorOptions = null;  
```  
  
 Para obter mais exemplos de como usar importações, consulte as instruções a seguir:  
  
 [Passo a passo: Criar um glifo de margem](../extensibility/walkthrough-creating-a-margin-glyph.md)  
  
 [Passo a passo: Personalizar a exibição de texto](../extensibility/walkthrough-customizing-the-text-view.md)  
  
 [Passo a passo: Realçar texto](../extensibility/walkthrough-highlighting-text.md)  
  
 [Passo a passo: Dicas de ferramenta de QuickInfo vídeo](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)  
  
 [Passo a passo: Exibir a Ajuda de assinatura](../extensibility/walkthrough-displaying-signature-help.md)  
  
 [Passo a passo: exibir preenchimento de declaração](../extensibility/walkthrough-displaying-statement-completion.md)  
  
 [Passo a passo: Exibir sugestões de lâmpada](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)  
  
## <a name="import-the-service-provider"></a>O provedor de serviço de importação  
 Você também pode importar um <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> (encontrado no assembly Microsoft.VisualStudio.Shell.Immutable.10.0) da mesma maneira para obter acesso aos serviços do Visual Studio:  
  
```csharp  
[Import]  
internal SVsServiceProvider ServiceProvider = null;   
```  
  
 Ver [instruções passo a passo: acessar o objeto DTE de uma extensão do editor](../extensibility/walkthrough-accessing-the-dte-object-from-an-editor-extension.md) para obter mais informações.  
  
## <a name="services"></a>Serviços  
 Serviços do editor são geralmente única entidades que fornecem um serviço e são compartilhadas entre vários componentes.  
  
|Importar|Fornece|  
|------------|--------------|  
|<xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService>|A relação entre as extensões de arquivo e <xref:Microsoft.VisualStudio.Utilities.IContentType> objetos.|  
|<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>|A coleção de objetos <xref:Microsoft.VisualStudio.Utilities.IContentType>.|  
|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformationService>|Objetos <xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformation>.|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>|Muitos objetos de adaptador do editor:<br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|  
|<xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearchFactoryService>|Um <xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearch> objeto para um modo de exibição de texto especificado.|  
|<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>|Um <xref:Microsoft.VisualStudio.Text.ITextBuffer>.|  
|<xref:Microsoft.VisualStudio.Text.ITextDocumentFactoryService>|Um <xref:Microsoft.VisualStudio.Text.ITextDocument>.|  
|<xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceService>|Um <xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceCollection%601> das diferenças.|  
|<xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalStringDifferenceService>|Um <xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalDifferenceCollection> das diferenças.|  
|<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService>|Uma <xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer> ou um <xref:Microsoft.VisualStudio.Text.Projection.IElisionBuffer>.|  
|<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService>|Uma <xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph> para um conjunto de <xref:Microsoft.VisualStudio.Text.ITextBuffer> objetos.|  
|<xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService>|Uma <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> para um <xref:Microsoft.VisualStudio.Text.ITextBuffer>.|  
|<xref:Microsoft.VisualStudio.Text.Classification.IViewClassifierAggregatorService>|Uma <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView>.|  
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMapService>|Uma <xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView>.|  
|<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>|Uma <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView>.|  
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>|Mantém a coleção de <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> objetos.|  
|<xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService>|Um <xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601> para um buffer de texto.|  
|<xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService>|Um <xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601> para uma exibição de texto.|  
|<xref:Microsoft.VisualStudio.Text.Editor.IEditorOptionsFactoryService>|O <xref:Microsoft.VisualStudio.Text.Editor.IEditorOptions> para o escopo especificado.|  
|<xref:Microsoft.VisualStudio.Text.Editor.IScrollMapFactoryService>|Um <xref:Microsoft.VisualStudio.Text.Editor.IScrollMap> para uma exibição de texto.|  
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|Uma <xref:Microsoft.VisualStudio.Text.Editor.ISmartIndent> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView>.|  
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|Obtém o recuo automático por meio de <xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentProvider> objetos.|  
|<xref:Microsoft.VisualStudio.Text.Editor.ITextEditorFactoryService>|Gerencia o <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> para um <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>.|  
|<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedTextSourceFactoryService>|Um <xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource>.|  
|<xref:Microsoft.VisualStudio.Text.Formatting.IRtfBuilderService>|Gera texto formatado em RTF de um conjunto de intervalos de instantâneo.|  
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencerFactoryService>|Uma <xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencer> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView>.|  
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextParagraphPropertiesFactoryService>|Um <xref:System.Windows.Media.TextFormatting.TextParagraphProperties> para formatação de linhas de texto em uma exibição.|  
|<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService>|Um <xref:Microsoft.VisualStudio.Text.Operations.IEditorOperations> do objeto para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView>.|  
|<xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>|Pesquisa um instantâneo de texto.|  
|<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>|Uma <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> para um <xref:Microsoft.VisualStudio.Text.ITextBuffer> por <xref:Microsoft.VisualStudio.Utilities.IContentType>.|  
|<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService>|Um <xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager> para uma exibição de texto.|  
|<xref:Microsoft.VisualStudio.Language.Intellisense.IGlyphService>|Um conjunto padrão de glifos.|  
|<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStackMapService>|Uma <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStack> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView>.|  
|<xref:Microsoft.VisualStudio.Language.Intellisense.IWpfKeyboardTrackingService>|Faixas de manipulação de teclado.|  
|<xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService>|Padrão <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> objetos.|  
|<xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistoryRegistry>|Mantém a relação entre os buffers de texto e <xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistory> objetos.|  
  
## <a name="other-imports"></a>Outras importações  
 Agentes e fábricas de provedor geralmente são entidades que podem ter várias instâncias em vários componentes.  
  
|Importar|Fornece|  
|------------|--------------|  
|<xref:Microsoft.VisualStudio.Text.Adornments.IErrorProviderFactory>|Uma <xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601> do tipo <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>) para o buffer fornecido.|  
|<xref:Microsoft.VisualStudio.Text.Adornments.ITextMarkerProviderFactory>|Um marcador de marcador de texto (um <xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601> do tipo <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>).|  
|<xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProviderFactory>|Uma <xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProvider> para um determinado <xref:Microsoft.VisualStudio.Text.Editor.ITextView>.|  
|<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>|Um <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession>.|  
|<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker>|Um <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSession>.|  
|<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>|Um <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSession>.|  
  
## <a name="see-also"></a>Consulte também  
 [Pontos de extensão de editor e o serviço de linguagem](../extensibility/language-service-and-editor-extension-points.md)
