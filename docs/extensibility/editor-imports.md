---
title: Importações do editor | Microsoft Docs
description: Saiba como importar serviços, fábricas e agente do editor que fornecem à sua extensão diferentes tipos de acesso ao editor principal.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- editors [Visual Studio SDK], new - services
ms.assetid: 8d096de3-33b4-427a-a122-4aeff8a72da0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7f2fa91b41017512b3f38ad61b800b293e0abaa1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898338"
---
# <a name="editor-imports"></a>Importações do editor
Você pode importar vários serviços de editor, fábricas e agente que fornecem à sua extensão diferentes tipos de acesso ao editor principal. Por exemplo, você pode importar o <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> para fornecer um para um determinado tipo de <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> conteúdo. (Esse navegador permite que você execute diferentes tipos de pesquisas em um buffer de texto.)

 Para usar uma importação de editor, importe-a como um campo ou propriedade de uma classe que exporta uma parte Managed Extensibility Framework componente.

> [!NOTE]
> Para obter mais informações sobre Managed Extensibility Framework, [consulte Managed Extensibility Framework (MEF).](/dotnet/framework/mef/index)

## <a name="import-syntax"></a>Sintaxe de importação
 O exemplo a seguir mostra como importar o serviço de fábrica de opções do editor.

```
[Import]
internal IEditorOptionsFactoryService EditorOptions { get; set; }
```

 Se você quiser importar o serviço como um campo e não uma propriedade, deverá defini-lo como na declaração para evitar os avisos do compilador sobre não atribuir a uma `null` variável:

```
[Import]
internal IEditorOptionsFactoryService m_editorOptions = null;
```

 Para obter mais exemplos de como usar importações, consulte os seguintes passo a passo:

- [Passo a passo: criar um glifo de margem](../extensibility/walkthrough-creating-a-margin-glyph.md)

- [Passo a passo: personalizar a exibição de texto](../extensibility/walkthrough-customizing-the-text-view.md)

- [Passo a passo: realça o texto](../extensibility/walkthrough-highlighting-text.md)

- [Passo a passo: exibir dicas de ferramenta QuickInfo](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)

- [Passo a passo: Exibir Ajuda de Assinatura](../extensibility/walkthrough-displaying-signature-help.md)

- [Passo a passo: exibir preenchimento de declaração](../extensibility/walkthrough-displaying-statement-completion.md)

- [Passo a passo: exibir sugestões de lâmpada](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)

## <a name="import-the-service-provider"></a>Importar o provedor de serviços
 Você também pode importar um (encontrado no <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> assembly Microsoft.VisualStudio.Shell.Immutable.10.0) da mesma maneira para obter acesso aos serviços Visual Studio:

```csharp
[Import]
internal SVsServiceProvider ServiceProvider = null;
```

 Consulte [Passo a passo: acessar o objeto DTE de uma extensão do editor](../extensibility/walkthrough-accessing-the-dte-object-from-an-editor-extension.md) para obter mais informações.

## <a name="services"></a>Serviços
 Os serviços do editor geralmente são entidades individuais que fornecem um serviço e são compartilhados entre vários componentes.

|Importação|Fornece o|
|------------|--------------|
|<xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService>|A relação entre extensões de arquivo e <xref:Microsoft.VisualStudio.Utilities.IContentType> objetos.|
|<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>|A coleção de objetos <xref:Microsoft.VisualStudio.Utilities.IContentType>.|
|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformationService>|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformation> Objetos.|
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>|Muitos objetos de adaptador de editor:<br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|
|<xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearchFactoryService>|Um <xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearch> objeto para uma exibição de texto determinada.|
|<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>|Um <xref:Microsoft.VisualStudio.Text.ITextBuffer>.|
|<xref:Microsoft.VisualStudio.Text.ITextDocumentFactoryService>|Um <xref:Microsoft.VisualStudio.Text.ITextDocument>.|
|<xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceService>|Um <xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceCollection%601> de diferenças.|
|<xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalStringDifferenceService>|Um <xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalDifferenceCollection> de diferenças.|
|<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService>|Um <xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer> ou um <xref:Microsoft.VisualStudio.Text.Projection.IElisionBuffer> .|
|<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService>|Um <xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph> para um conjunto de objetos <xref:Microsoft.VisualStudio.Text.ITextBuffer> .|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService>|Um <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> para um <xref:Microsoft.VisualStudio.Text.ITextBuffer> .|
|<xref:Microsoft.VisualStudio.Text.Classification.IViewClassifierAggregatorService>|Um <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView> .|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMapService>|Um <xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView> .|
|<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>|Um <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView> .|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>|Mantém a coleção de <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> objetos .|
|<xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService>|Um <xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601> para um buffer de texto.|
|<xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService>|Um <xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601> para uma exibição de texto.|
|<xref:Microsoft.VisualStudio.Text.Editor.IEditorOptionsFactoryService>|O <xref:Microsoft.VisualStudio.Text.Editor.IEditorOptions> para o escopo especificado.|
|<xref:Microsoft.VisualStudio.Text.Editor.IScrollMapFactoryService>|Um <xref:Microsoft.VisualStudio.Text.Editor.IScrollMap> para uma exibição de texto.|
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|Um <xref:Microsoft.VisualStudio.Text.Editor.ISmartIndent> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView> .|
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|Obtém o recuo automático por meio dos <xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentProvider> objetos .|
|<xref:Microsoft.VisualStudio.Text.Editor.ITextEditorFactoryService>|Gerencia o <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> para um <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> .|
|<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedTextSourceFactoryService>|Um <xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource>.|
|<xref:Microsoft.VisualStudio.Text.Formatting.IRtfBuilderService>|Gera texto formatado em RTF de um conjunto de intervalos de instantâneos.|
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencerFactoryService>|Um <xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencer> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView> .|
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextParagraphPropertiesFactoryService>|Um <xref:System.Windows.Media.TextFormatting.TextParagraphProperties> para formatação de linhas de texto em uma exibição.|
|<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService>|Um <xref:Microsoft.VisualStudio.Text.Operations.IEditorOperations> objeto para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView> .|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>|Pesquisa um instantâneo de texto.|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>|Um <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> para um por <xref:Microsoft.VisualStudio.Text.ITextBuffer> <xref:Microsoft.VisualStudio.Utilities.IContentType> .|
|<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService>|Um <xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager> para uma exibição de texto.|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IGlyphService>|Um conjunto padrão de glifos.|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStackMapService>|Um <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStack> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView> .|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IWpfKeyboardTrackingService>|Rastreia a manipulação de teclado.|
|<xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService>|Objetos <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> padrão.|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistoryRegistry>|Mantém a relação entre buffers de texto e  <xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistory> objetos.|

## <a name="other-imports"></a>Outras importações
 Fábricas de provedores e agente geralmente são entidades que podem ter várias instâncias em vários componentes.

|Importação|Fornece o|
|------------|--------------|
|<xref:Microsoft.VisualStudio.Text.Adornments.IErrorProviderFactory>|Um <xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601> do tipo ) para o buffer <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag> determinado.|
|<xref:Microsoft.VisualStudio.Text.Adornments.ITextMarkerProviderFactory>|Um tagger de marcador de texto <xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601> (um do tipo <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> ).|
|<xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProviderFactory>|Um <xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProvider> para um determinado <xref:Microsoft.VisualStudio.Text.Editor.ITextView> .|
|<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>|Um <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession>.|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker>|Um <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSession>.|
|<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>|Um <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSession>.|

## <a name="see-also"></a>Confira também
- [Pontos de extensão do serviço de linguagem e do editor](../extensibility/language-service-and-editor-extension-points.md)
