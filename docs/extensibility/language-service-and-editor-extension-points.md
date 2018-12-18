---
title: Serviço de linguagem e pontos de extensão do Editor | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extension points
ms.assetid: 91a6417e-a6fe-4bc2-9d9f-5173c634a99b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 2df3de4bfba0510cf3c8a5474a363a5ec579a79f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49927743"
---
# <a name="language-service-and-editor-extension-points"></a>Pontos de extensão de editor e o serviço de linguagem
O editor fornece pontos de extensão que você pode estender como partes do componente Managed Extensibility Framework (MEF), incluindo a maioria dos recursos do serviço de linguagem. Essas são as categorias de ponto de extensão principal:  
  
-   Tipos de conteúdo  
  
-   Tipos de classificação e formatos de classificação  
  
-   Margens e barras de rolagem  
  
-   Marcas  
  
-   Adornos  
  
-   Processadores de mouse  
  
-   Manipuladores de soltar  
  
-   Opções  
  
-   IntelliSense  
  
## <a name="extend-content-types"></a>Estender os tipos de conteúdo  
 Tipos de conteúdo são as definições dos tipos de texto tratado pelo editor de, por exemplo, "text", "código" ou "CSharp". Definir um novo tipo de conteúdo, declarando uma variável do tipo <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> e dando um nome exclusivo de novo tipo de conteúdo. Para registrar o tipo de conteúdo com o editor, exportá-lo junto com os seguintes atributos:  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute> é o nome do tipo de conteúdo.  
  
- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute> é o nome do tipo de conteúdo do qual esse tipo de conteúdo é derivado. Um tipo de conteúdo pode herdar de vários outros tipos de conteúdo.  
  
  Porque o <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> classe é fechada, você pode exportá-lo sem nenhum parâmetro de tipo.  
  
  O exemplo a seguir mostra os atributos de exportação em uma definição de tipo de conteúdo.  
  
```  
[Export]  
[Name("test")]  
[BaseDefinition("code")]  
[BaseDefinition("projection")]  
internal static ContentTypeDefinition TestContentTypeDefinition;  
```  
  
 Tipos de conteúdo podem ser baseados em zero ou mais tipos de conteúdo já existentes. Estes são os tipos internos:  
  
- Qualquer: o tipo de conteúdo básico. Pai de todos os outros tipos de conteúdo.  
  
- Texto: o tipo básico para o conteúdo não projeção. Herda de "qualquer".  
  
- Texto sem formatação: para texto não são de código. Herda de "text".  
  
- Código: para o código de todos os tipos. Herda de "text".  
  
- Inerte: exclui o texto de qualquer tipo de manipulação. Texto desse tipo de conteúdo nunca terá qualquer extensão aplicado a ele.  
  
- Projeção: para o conteúdo de buffers de projeção. Herda de "qualquer".  
  
- IntelliSense: para o conteúdo do IntelliSense. Herda de "text".  
  
- Sighelp: a Ajuda da assinatura. Herda de "intellisense".  
  
- Sighelp-doc: documentação de ajuda de assinatura. Herda de "intellisense".  
  
  Estes são alguns dos tipos de conteúdo que são definidos pelo Visual Studio e alguns dos idiomas que são hospedados no Visual Studio:  
  
- Basic  
  
- C/C++  
  
- ConsoleOutput  
  
- CSharp  
  
- CSS  
  
- ENC  
  
- Localizar resultados  
  
- F#  
  
- HTML  
  
- JScript  
  
- XAML  
  
- XML  
  
  Para descobrir a lista de tipos de conteúdo disponíveis, importe o <xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>, que mantém a coleção de tipos de conteúdo para o editor. O código a seguir importa esse serviço como uma propriedade.  
  
```  
[Import]  
internal IContentTypeRegistryService ContentTypeRegistryService { get; set; }  
```  
  
 Para associar um tipo de conteúdo com uma extensão de nome de arquivo, use <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>.  
  
> [!NOTE]
>  No Visual Studio, extensões de nome de arquivo são registradas usando o <xref:Microsoft.VisualStudio.Shell.ProvideLanguageExtensionAttribute> em um pacote de serviço de linguagem. O <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> associa um tipo de conteúdo do MEF com uma extensão de nome de arquivo que tenha sido registrada dessa maneira.  
  
 Para exportar a extensão de nome de arquivo para a definição de tipo de conteúdo, você deve incluir os seguintes atributos:  
  
- <xref:Microsoft.VisualStudio.Utilities.FileExtensionAttribute>: Especifica a extensão de nome de arquivo.  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: Especifica o tipo de conteúdo.  
  
  Porque o <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> classe é fechada, você pode exportá-lo sem nenhum parâmetro de tipo.  
  
  O exemplo a seguir mostra os atributos de exportação em uma extensão de nome de arquivo a uma definição de tipo de conteúdo.  
  
```  
[Export]  
[FileExtension(".test")]  
[ContentType("test")]  
internal static FileExtensionToContentTypeDefinition TestFileExtensionDefinition;  
```  
  
 O <xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService> gerencia as associações entre extensões de nome de arquivo e tipos de conteúdo.  
  
## <a name="extend-classification-types-and-classification-formats"></a>Estender os tipos de classificação e formatos de classificação  
 Você pode usar tipos de classificação para definir os tipos de texto para o qual você deseja fornecer tratamento diferente (por exemplo, colorir o texto "palavra-chave" azul e o texto de "comentário" verde). Definir um novo tipo de classificação, declarando uma variável do tipo <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition> e dando a ele um nome exclusivo.  
  
 Para registrar o tipo de classificação com o editor, exportá-lo junto com os seguintes atributos:  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome do tipo de classificação.  
  
- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute>: o nome do tipo de classificação do qual esse tipo de classificação herdado. Herdam de todos os tipos de classificação de "text", e um tipo de classificação pode herdar de vários outros tipos de classificação.  
  
  Porque o <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition> classe é fechada, você pode exportá-lo sem nenhum parâmetro de tipo.  
  
  O exemplo a seguir mostra os atributos de exportação em uma definição de tipo de classificação.  
  
```  
[Export]  
[Name("csharp.test")]  
[BaseDefinition("test")]  
internal static ClassificationTypeDefinition CSharpTestDefinition;  
```  
  
 O <xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService> fornece acesso às classificações padrão. Tipos de classificação internas incluem:  
  
- "texto"  
  
- "idioma natural" (deriva de "text")  
  
- "linguagem formal" (deriva de "text")  
  
- "string" (deriva de "literal")  
  
- "caractere" (deriva de "literal")  
  
- "numérico" (deriva de "literal")  
  
  Um conjunto de tipos de erro diferente de herdar de <xref:Microsoft.VisualStudio.Text.Adornments.ErrorTypeDefinition>. Eles incluem os seguintes tipos de erro:  
  
- "Erro de sintaxe"  
  
- "Erro do compilador"  
  
- "outro erro"  
  
- "aviso"  
  
  Para descobrir a lista de tipos de classificação disponível, importe o <xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>, que mantém a coleção de tipos de classificação para o editor. O código a seguir importa esse serviço como uma propriedade.  
  
```  
[Import]  
internal IClassificationTypeRegistryService ClassificationTypeRegistryService { get; set; }  
```  
  
 Você pode definir uma definição de formato de classificação para o novo tipo de classificação. Derive uma classe de <xref:Microsoft.VisualStudio.Text.Classification.ClassificationFormatDefinition> e exportá-lo com o tipo <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition>, juntamente com os seguintes atributos:  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome do formato.  
  
- <xref:Microsoft.VisualStudio.Utilities.DisplayNameAttribute>: o nome de exibição do formato.  
  
- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: Especifica se o formato é exibida na **fontes e cores** página do **opções** caixa de diálogo.  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: a prioridade do formato. Valores válidos são de <xref:Microsoft.VisualStudio.Text.Classification.Priority>.  
  
- <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeAttribute>: o nome da classificação de tipo para o qual esse formato é mapeado.  
  
  O exemplo a seguir mostra os atributos de exportação em uma definição de formato de classificação.  
  
```  
[Export(typeof(EditorFormatDefinition))]  
[ClassificationType(ClassificationTypeNames = "test")]  
[Name("test")]  
[DisplayName("Test")]  
[UserVisible(true)]  
[Order(After = Priority.Default, Before = Priority.High)]  
internal sealed class TestFormat : ClassificationFormatDefinition  
```  
  
 Para descobrir a lista de formatos disponíveis, importe o <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>, que mantém a coleção de formatos para o editor. O código a seguir importa esse serviço como uma propriedade.  
  
```  
[Import]  
internal IEditorFormatMapService FormatMapService { get; set; }  
```  
  
## <a name="extend-margins-and-scrollbars"></a>Estender as margens e barras de rolagem  
 Margens e barras de rolagem são os elementos de exibição principal do editor, além da exibição de texto. Você pode fornecer qualquer número das margens, além das margens padrão que aparecem em torno a exibição de texto.  
  
 Implemente um <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMargin> interface para definir uma margem. Você também deve implementar o <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider> interface para criar a margem.  
  
 Para registrar o provedor de margem com o editor, você deve exportar o provedor junto com os seguintes atributos:  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome da margem.  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: a ordem em que a margem é exibido, em relação as outras margens.  
  
   Estas são as margens internas:  
  
  - "Barra de rolagem Horizontal do Wpf"  
  
  - "Barra de rolagem Vertical do Wpf"  
  
  - "Wpf linha número Margin"  
  
    Margens horizontais que têm um atributo de ordem de `After="Wpf Horizontal Scrollbar"` são exibidos abaixo da margem interna e margens horizontais que têm um atributo de ordem de `Before ="Wpf Horizontal Scrollbar"` são exibidas acima da margem interna. Margens verticais que têm um atributo de ordem do botão direito do mouse `After="Wpf Vertical Scrollbar"` são exibidos à direita da barra de rolagem. Deixado margens verticais que têm um atributo de ordem de `After="Wpf Line Number Margin"` aparecer à esquerda da margem de número de linha (se estiver visível).  
  
- <xref:Microsoft.VisualStudio.Text.Editor.MarginContainerAttribute>: o tipo de margem (esquerda, direita, superior ou inferior).  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: o tipo de conteúdo (por exemplo, "text" ou "code") para o qual sua margem é válida.  
  
  O exemplo a seguir mostra os atributos de exportação em um provedor de margem para a margem que aparece à direita da margem de número de linha.  
  
```  
[Export(typeof(IWpfTextViewMarginProvider))]  
[Name("TestMargin")]  
[Order(Before = "Wpf Line Number Margin")]  
[MarginContainer(PredefinedMarginNames.Left)]  
[ContentType("text")]   
```  
  
## <a name="extend-tags"></a>Estender as marcas  
 As marcas são uma maneira de associar dados a tipos diferentes de texto. Em muitos casos, os dados associados são exibidos como um efeito visual, mas não todas as marcas tem uma apresentação visual. Você pode definir seu próprio tipo de marca implementando <xref:Microsoft.VisualStudio.Text.Tagging.ITag>. Você também deve implementar <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> para fornecer as marcas para um determinado conjunto de intervalos de texto e um <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> para fornecer o marcador. Você deve exportar o provedor de marcador junto com os seguintes atributos:  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: o tipo de conteúdo (por exemplo, "text" ou "code") para o qual sua marca é válida.  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>: o tipo de marca.  
  
  O exemplo a seguir mostra os atributos de exportação em um provedor de marcador.  
  
<CodeContentPlaceHolder>8</CodeContentPlaceHolder>  
 Os seguintes tipos de marca são internos:  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.ClassificationTag>: associado com um <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType>.  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>: associadas aos tipos de erro.  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>: associado com um adorno.  
  
  > [!NOTE]
  >  Para obter um exemplo de uma <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>, consulte a definição de HighlightWordTag na [passo a passo: realce de texto](../extensibility/walkthrough-highlighting-text.md).  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>: associados a regiões que podem ser expandidos ou recolhidos na estrutura de tópicos.  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>: define o espaço que ocupa um adorno em uma exibição de texto. Para obter mais informações sobre adornos de negociação de espaço, consulte a seção a seguir.  
  
- <xref:Microsoft.VisualStudio.Text.Editor.IntraTextAdornmentTag>: fornece espaçamento automático e dimensionamento para o adorno.  
  
  Para localizar e usar marcas de buffers e modos de exibição, importe as <xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService> ou o <xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService>, que lhe dão uma <xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601> do tipo solicitado. O código a seguir importa esse serviço como uma propriedade.  
  
```  
[Import]  
internal IViewTagAggregatorFactoryService ViewTagAggregatorFactoryService { get; set; }  
```  
  
#### <a name="tags-and-markerformatdefinitions"></a>Marcas e MarkerFormatDefinitions  
 Você pode estender o <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition> classe para definir a aparência de uma marca. Você deve exportar sua classe (como um <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition>) com os seguintes atributos:  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome usado para fazer referência a esse formato  
  
- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: isso faz com que o formato a ser exibido na interface do usuário  
  
  No construtor, você pode definir o nome de exibição e a aparência da marca. <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.BackgroundColor%2A> Define a cor de preenchimento, e <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.ForegroundColor%2A> define a cor da borda. O <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.DisplayName%2A> é o nome localizável da definição de formato.  
  
  Este é um exemplo de uma definição de formato:  
  
```  
[Export(typeof(EditorFormatDefinition))]  
[Name("MarkerFormatDefinition/HighlightWordFormatDefinition")]  
[UserVisible(true)]  
internal class HighlightWordFormatDefinition : MarkerFormatDefinition  
{  
    public HighlightWordFormatDefinition()  
    {  
        this.BackgroundColor = Colors.LightBlue;  
        this.ForegroundColor = Colors.DarkBlue;  
        this.DisplayName = "Highlight Word";   
        this.ZOrder = 5;  
    }  
}  
  
```  
  
 Para aplicar essa definição de formato para uma marca, fazer referência ao nome definido no atributo de nome da classe (não o nome de exibição).  
  
> [!NOTE]
>  Para obter um exemplo de uma <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition>, consulte a classe HighlightWordFormatDefinition [passo a passo: realce de texto](../extensibility/walkthrough-highlighting-text.md).  
  
## <a name="extend-adornments"></a>Estender adornos  
 Adornos definem os efeitos visuais que podem ser adicionados ao texto que é exibido em uma exibição de texto ou ao texto a exibir em si. Você pode definir seu próprio adornos como qualquer tipo de <xref:System.Windows.UIElement>.  
  
 Em sua classe de adorno, você deve declarar um <xref:Microsoft.VisualStudio.Text.Editor.AdornmentLayerDefinition>. Para registrar sua camada de adorno, exportá-lo junto com os seguintes atributos:  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome do adorno.  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: a ordenação do adorno em relação a outras camadas de adorno. A classe <xref:Microsoft.VisualStudio.Text.Editor.PredefinedAdornmentLayers> define quatro camadas de padrão: estrutura de tópicos, seleção, cursor e texto.  
  
  O exemplo a seguir mostra os atributos de exportação em uma definição de camada de adorno.  
  
```  
[Export]  
[Name("TestEmbeddedAdornment")]  
[Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]  
internal AdornmentLayerDefinition testLayerDefinition;  
```  
  
 Você deve criar uma segunda classe que implementa <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> e manipula seu <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> evento instanciando o adorno. Você deve exportar essa classe junto com os seguintes atributos:  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: o tipo de conteúdo (por exemplo, "text" ou "code") para o qual o adorno é válido.  
  
- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>: o tipo de exibição de texto para o qual este adorno é válido. A classe <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles> tem o conjunto de funções do modo de exibição de texto predefinido. Por exemplo, <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document> é usado principalmente para modos de exibição de texto de arquivos. <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> é usado para modos de exibição de texto que um usuário pode editar ou navegar usando um mouse e teclado. Exemplos de <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> modos de exibição são o modo de exibição de texto do editor e o **saída** janela.  
  
  O exemplo a seguir mostra os atributos de exportação no provedor de adorno.  
  
```  
[Export(typeof(IWpfTextViewCreationListener))]  
[ContentType("csharp")]  
[TextViewRole(PredefinedTextViewRoles.Document)]  
internal sealed class TestAdornmentProvider : IWpfTextViewCreationListener  
```  
  
 Um adorno de negociação de espaço é aquele que ocupa espaço no mesmo nível como o texto. Para criar esse tipo de adorno, você deve definir uma classe de marca que herda de <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>, que define a quantidade de espaço que ocupa o adorno.  
  
 Assim como acontece com todos os adornos, você deve exportar a definição da camada de adorno.  
  
```  
[Export]  
[Name("TestAdornment")]  
[Order(After = DefaultAdornmentLayers.Text)]  
internal AdornmentLayerDefinition testAdornmentLayer;  
```  
  
 Para instanciar o adorno de negociação de espaço, você deve criar uma classe que implementa <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider>, além da classe que implementa <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> (assim como acontece com outros tipos de adornos).  
  
 Para registrar o provedor de marcador, você deve exportá-lo junto com os seguintes atributos:  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: o tipo de conteúdo (por exemplo, "text" ou "code") para o qual o adorno é válido.  
  
- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>: o tipo de exibição de texto para o qual o adorno ou a marca é válido. A classe <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles> tem o conjunto de funções do modo de exibição de texto predefinido. Por exemplo, <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document> é usado principalmente para modos de exibição de texto de arquivos. <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> é usado para modos de exibição de texto que um usuário pode editar ou navegar usando um mouse e teclado. Exemplos de <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> modos de exibição são o modo de exibição de texto do editor e o **saída** janela.  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>: o tipo de marca ou adorno que você definiu. Você deve adicionar um segundo <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> para <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>.  
  
  O exemplo a seguir mostra os atributos de exportação no provedor de marcador para uma marca de adorno negociação de espaço.  
  
```  
[Export(typeof(ITaggerProvider))]  
[ContentType("text")]  
[TextViewRole(PredefinedTextViewRoles.Document)]  
[TagType(typeof(SpaceNegotiatingAdornmentTag))]  
[TagType(typeof(TestSpaceNegotiatingTag))]  
internal sealed class TestTaggerProvider : ITaggerProvider  
```  
  
## <a name="extending-mouse-processors"></a>Estendendo os processadores de Mouse  
 Você pode adicionar um tratamento especial para a entrada do mouse. Criar uma classe que herda de <xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase> e substituir os eventos de mouse para a entrada que você deseja manipular. Você também deve implementar <xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider> em uma segunda classe e exportá-lo junto com o <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> que especifica o tipo de conteúdo (por exemplo, "text" ou "code") para o qual o manipulador de mouse é válido.  
  
 O exemplo a seguir mostra os atributos de exportação em um provedor de processador de mouse.  
  
```  
[Export(typeof(IMouseProcessorProvider))]  
[Name("test mouse processor")]  
[ContentType("text")]  
[TextViewRole(PredefinedTextViewRoles.Interactive)]   
internal sealed class TestMouseProcessorProvider : IMouseProcessorProvider  
```  
  
## <a name="extend-drop-handlers"></a>Estender os manipuladores de soltar  
 Você pode personalizar o comportamento de manipuladores de soltar para tipos específicos de texto, criando uma classe que implementa <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandler> e uma segunda classe que implementa <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandlerProvider> para criar o manipulador de soltar. Você deve exportar o manipulador de soltar junto com os seguintes atributos:  
  
- <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.DropFormatAttribute>: o formato de texto para o qual este manipulador de soltar é válido. Os seguintes formatos são tratados em ordem de prioridade do mais alto ao mais baixo:  
  
  1.  Qualquer formato personalizado  
  
  2.  FileDrop  
  
  3.  EnhancedMetafile  
  
  4.  WaveAudio  
  
  5.  RIFF  
  
  6.  DIF  
  
  7.  Localidade  
  
  8.  Paleta  
  
  9. PenData  
  
  10. Serializável  
  
  11. SymbolicLink  
  
  12. XAML  
  
  13. XamlPackage  
  
  14. TIFF  
  
  15. Bitmap  
  
  16. DIB  
  
  17. MetafilePicture  
  
  18. CSV  
  
  19. System.String  
  
  20. Formato HTML  
  
  21. UnicodeText  
  
  22. OEMText  
  
  23. Texto  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome do manipulador de soltar.  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: a ordenação do manipulador de soltar antes ou depois do manipulador de menu padrão. O manipulador de menu padrão para o Visual Studio é chamado de "DefaultFileDropHandler".  
  
  O exemplo a seguir mostra os atributos de exportação em um provedor de manipulador de soltar.  
  
```  
[Export(typeof(IDropHandlerProvider))]  
[DropFormat("Text")]   
[Name("TestDropHandler")]  
[Order(Before="DefaultFileDropHandler")]   
internal class TestDropHandlerProvider : IDropHandlerProvider  
```  
  
## <a name="extending-editor-options"></a>Estendendo as opções do Editor  
 Você pode definir opções para ser válida somente em um determinado escopo, por exemplo, em uma exibição de texto. O editor fornece esse conjunto de opções predefinidas: opções de exibição do Windows Presentation Foundation (WPF), opções de exibição e as opções do editor. Essas opções podem ser encontradas no <xref:Microsoft.VisualStudio.Text.Editor.DefaultOptions>, <xref:Microsoft.VisualStudio.Text.Editor.DefaultTextViewOptions>, e <xref:Microsoft.VisualStudio.Text.Editor.DefaultWpfViewOptions>.  
  
 Para adicionar uma nova opção, derive uma classe de uma dessas classes de definição de opção:  
  
- <xref:Microsoft.VisualStudio.Text.Editor.EditorOptionDefinition%601>  
  
- <xref:Microsoft.VisualStudio.Text.Editor.ViewOptionDefinition%601>  
  
- <xref:Microsoft.VisualStudio.Text.Editor.WpfViewOptionDefinition%601>  
  
  O exemplo a seguir mostra como exportar uma definição de opção que tem um valor booliano.  
  
```  
[Export(typeof(EditorOptionDefinition))]  
internal sealed class TestOption : EditorOptionDefinition<bool>  
```  
  
## <a name="extend-intellisense"></a>Estender o IntelliSense  
 O IntelliSense é um termo geral para um grupo de recursos que fornecem informações sobre o texto estruturado e preenchimento de declaração para ele. Esses recursos incluem preenchimento de declaração, a Ajuda da assinatura, informações rápidas e lâmpadas. Preenchimento de declaração ajuda os usuários a digitar um nome de membro ou a palavra-chave de idioma corretamente. Ajuda da assinatura exibe a assinatura ou assinaturas para o método que o usuário digitou apenas. Informação rápida exibe uma assinatura completa para um nome de tipo ou membro quando o mouse é posicionado sobre ele. Lâmpada fornecer ações adicionais para determinadas identificadores em determinados contextos, por exemplo, a renomeação de todas as ocorrências de uma variável após uma ocorrência foi renomeada.  
  
 O design de um recurso do IntelliSense é muito semelhante em todos os casos:  
  
- Um IntelliSense *broker* é responsável por processo geral.  
  
- Um IntelliSense *sessão* representa a sequência de eventos entre o disparo do apresentador e o envio ou cancelamento da seleção. Normalmente, a sessão é disparada por alguns gesto do usuário.  
  
- Um IntelliSense *controlador* é responsável por decidir quando a sessão deve começar e terminar. Ele também decide quando as informações devem ser confirmadas e quando a sessão deve ser cancelada.  
  
- Um IntelliSense *origem* fornece o conteúdo e decide a melhor correspondência.  
  
- Um IntelliSense *apresentador* é responsável por exibir o conteúdo.  
  
  Na maioria dos casos, é recomendável que você forneça pelo menos uma origem e um controlador. Você também pode fornecer um apresentador, se você quiser personalizar a exibição.  
  
### <a name="implement-an-intellisense-source"></a>Implementar uma fonte do IntelliSense  
 Para personalizar uma fonte, você deve implementar um (ou mais) das interfaces de origem a seguir:  
  
-   <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>  
  
-   <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>  
  
-   <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>  
  
-   <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>  
  
> [!IMPORTANT]
>  <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSource> foi preterido em favor do <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>.  
  
 Além disso, você deve implementar um provedor do mesmo tipo:  
  
-   <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>  
  
-   <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider>  
  
-   <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>  
  
-   <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>  
  
> [!IMPORTANT]
>  <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSourceProvider> foi preterido em favor do <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>.  
  
 Você deve exportar o provedor junto com os seguintes atributos:  
  
-   <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome da origem.  
  
-   <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: o tipo de conteúdo (por exemplo, "text" ou "code") ao qual a fonte se aplica.  
  
-   <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: a ordem na qual a origem deve aparecer (em relação a outras fontes).  
  
-   O exemplo a seguir mostra os atributos de exportação em um provedor de fonte de conclusão.  
  
```  
Export(typeof(ICompletionSourceProvider))]  
[Name(" Test Statement Completion Provider")]  
[Order(Before = "default")]  
[ContentType("text")]  
internal class TestCompletionSourceProvider : ICompletionSourceProvider  
```  
  
 Para obter mais informações sobre a implementação de fontes do IntelliSense, consulte as instruções a seguir:  
  
 [Passo a passo: Dicas de ferramenta de QuickInfo vídeo](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)  
  
 [Passo a passo: Exibir a Ajuda de assinatura](../extensibility/walkthrough-displaying-signature-help.md)  
  
 [Passo a passo: exibir preenchimento de declaração](../extensibility/walkthrough-displaying-statement-completion.md)  
  
### <a name="implement-an-intellisense-controller"></a>Implementar um controlador do IntelliSense  
 Para personalizar um controlador, você deve implementar o <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController> interface. Além disso, você deve implementar um provedor de controlador junto com os seguintes atributos:  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome do controlador.  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: o tipo de conteúdo (por exemplo, "text" ou "code") ao qual o controlador se aplica.  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: a ordem na qual o controlador deve aparecer (em relação a outros controladores).  
  
  O exemplo a seguir mostra os atributos de exportação em um provedor de controlador de conclusão.  
  
```  
Export(typeof(IIntellisenseControllerProvider))]  
[Name(" Test Controller Provider")]  
[Order(Before = "default")]  
[ContentType("text")]  
internal class TestIntellisenseControllerProvider : IIntellisenseControllerProvider  
```  
  
 Para obter mais informações sobre como usar controladores de IntelliSense, consulte as instruções a seguir:  
  
 [Passo a passo: Dicas de ferramenta de QuickInfo vídeo](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)