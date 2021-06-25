---
title: Pontos de extensão do Serviço de Linguagem e do Editor | Microsoft Docs
description: Saiba mais sobre os pontos de extensão no editor Visual Studio código que você pode estender, incluindo a maioria dos recursos do serviço de linguagem.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- editors [Visual Studio SDK], new - extension points
ms.assetid: 91a6417e-a6fe-4bc2-9d9f-5173c634a99b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 293851f1f3e72508a9bc119fb7551b0118ab2a9b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903141"
---
# <a name="language-service-and-editor-extension-points"></a>Pontos de extensão do serviço de linguagem e do editor
O editor fornece pontos de extensão que você pode estender como Managed Extensibility Framework componente mef (mef), incluindo a maioria dos recursos do serviço de linguagem. Estas são as principais categorias de ponto de extensão:

- Tipos de conteúdo

- Tipos de classificação e formatos de classificação

- Margens e barras de rolagem

- Marcas

- Adornos

- Processadores de mouse

- Manipuladores de soltar

- Opções

- IntelliSense

## <a name="extend-content-types"></a>Estender tipos de conteúdo
 Os tipos de conteúdo são as definições dos tipos de texto manipulados pelo editor, por exemplo, "text", "code" ou "CSharp". Você define um novo tipo de conteúdo declarando uma variável do tipo e dando ao novo tipo <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> de conteúdo um nome exclusivo. Para registrar o tipo de conteúdo com o editor, exporte-o junto com os seguintes atributos:

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute> é o nome do tipo de conteúdo.

- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute> é o nome do tipo de conteúdo do qual esse tipo de conteúdo é derivado. Um tipo de conteúdo pode herdar de vários outros tipos de conteúdo.

  Como a <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> classe é lacrada, você pode exportá-la sem nenhum parâmetro de tipo.

  O exemplo a seguir mostra os atributos de exportação em uma definição de tipo de conteúdo.

```
[Export]
[Name("test")]
[BaseDefinition("code")]
[BaseDefinition("projection")]
internal static ContentTypeDefinition TestContentTypeDefinition;
```

 Os tipos de conteúdo podem ser baseados em zero ou mais tipos de conteúdo pré-existentes. Estes são os tipos integrados:

- Qualquer: o tipo de conteúdo básico. Pai de todos os outros tipos de conteúdo.

- Texto: o tipo básico para conteúdo sem projeção. Herda de "any".

- Texto não criptografado: para texto sem código. Herda de "text".

- Código: para código de todos os tipos. Herda de "text".

- Inerte: exclui o texto de qualquer tipo de manipulação. O texto desse tipo de conteúdo nunca terá nenhuma extensão aplicada a ele.

- Projeção: para o conteúdo dos buffers de projeção. Herda de "any".

- IntelliSense: para o conteúdo do IntelliSense. Herda de "text".

- Sighelp: ajuda de assinatura. Herda de "intelliSense".

- Sighelp-doc: documentação de ajuda de assinatura. Herda de "intelliSense".

  Estes são alguns dos tipos de conteúdo definidos por Visual Studio e alguns dos idiomas hospedados no Visual Studio:

- Basic

- C/C++

- ConsoleOutput

- CSharp

- CSS

- Enc

- FindResults

- F#

- HTML

- JScript

- XAML

- XML

  Para descobrir a lista de tipos de conteúdo disponíveis, importe o , que mantém a <xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService> coleção de tipos de conteúdo para o editor. O código a seguir importa esse serviço como uma propriedade.

```
[Import]
internal IContentTypeRegistryService ContentTypeRegistryService { get; set; }
```

 Para associar um tipo de conteúdo a uma extensão de nome de arquivo, use <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> .

> [!NOTE]
> No Visual Studio, as extensões de nome de arquivo são registradas usando o <xref:Microsoft.VisualStudio.Shell.ProvideLanguageExtensionAttribute> em um pacote de serviço de linguagem. O <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> associa um tipo de conteúdo MEF a uma extensão de nome de arquivo que foi registrada dessa maneira.

 Para exportar a extensão de nome de arquivo para a definição de tipo de conteúdo, você deve incluir os seguintes atributos:

- <xref:Microsoft.VisualStudio.Utilities.FileExtensionAttribute>: especifica a extensão de nome de arquivo.

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: especifica o tipo de conteúdo.

  Como a <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> classe é lacrada, você pode exportá-la sem nenhum parâmetro de tipo.

  O exemplo a seguir mostra os atributos de exportação em uma extensão de nome de arquivo para uma definição de tipo de conteúdo.

```
[Export]
[FileExtension(".test")]
[ContentType("test")]
internal static FileExtensionToContentTypeDefinition TestFileExtensionDefinition;
```

 O <xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService> gerencia as associações entre extensões de nome de arquivo e tipos de conteúdo.

## <a name="extend-classification-types-and-classification-formats"></a>Estender tipos de classificação e formatos de classificação
 Você pode usar tipos de classificação para definir os tipos de texto para os quais deseja fornecer tratamentos diferentes (por exemplo, colorir o texto "palavra-chave" azul e o texto "comentário" verde). Defina um novo tipo de classificação declarando uma variável do tipo <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition> e dando a ela um nome exclusivo.

 Para registrar o tipo de classificação com o editor, exporte-o junto com os seguintes atributos:

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome do tipo de classificação.

- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute>: o nome do tipo de classificação do qual esse tipo de classificação herda. Todos os tipos de classificação herdam de "texto", e um tipo de classificação pode herdar de vários outros tipos de classificação.

  Como a <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition> classe é lacrada, você pode exportá-la sem nenhum parâmetro de tipo.

  O exemplo a seguir mostra os atributos de exportação em uma definição de tipo de classificação.

```
[Export]
[Name("csharp.test")]
[BaseDefinition("test")]
internal static ClassificationTypeDefinition CSharpTestDefinition;
```

 O <xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService> fornece acesso a classificações padrão. Os tipos de classificação integrados incluem estes:

- "texto"

- "linguagem natural" (deriva de "texto")

- "linguagem formal" (deriva de "texto")

- "string" (deriva de "literal")

- "character" (deriva de "literal")

- "numerical" (deriva de "literal")

  Um conjunto de tipos de erro diferentes herdam de <xref:Microsoft.VisualStudio.Text.Adornments.ErrorTypeDefinition> . Eles incluem os seguintes tipos de erro:

- "erro de sintaxe"

- "erro do compilador"

- "outro erro"

- "aviso"

  Para descobrir a lista de tipos de classificação disponíveis, importe o , que mantém a <xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService> coleção de tipos de classificação para o editor. O código a seguir importa esse serviço como uma propriedade.

```
[Import]
internal IClassificationTypeRegistryService ClassificationTypeRegistryService { get; set; }
```

 Você pode definir uma definição de formato de classificação para o novo tipo de classificação. Derive uma classe de <xref:Microsoft.VisualStudio.Text.Classification.ClassificationFormatDefinition> e exporte-a com o tipo <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition> , junto com os seguintes atributos:

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome do formato.

- <xref:Microsoft.VisualStudio.Utilities.DisplayNameAttribute>: o nome de exibição do formato.

- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: especifica se o formato aparece na página **Fontes** e Cores da caixa **de diálogo** Opções.

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: a prioridade do formato. Os valores válidos são de <xref:Microsoft.VisualStudio.Text.Classification.Priority> .

- <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeAttribute>: o nome do tipo de classificação para o qual esse formato é mapeado.

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

 Para descobrir a lista de formatos disponíveis, importe o <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService> , que mantém a coleção de formatos para o editor. O código a seguir importa esse serviço como uma propriedade.

```
[Import]
internal IEditorFormatMapService FormatMapService { get; set; }
```

## <a name="extend-margins-and-scrollbars"></a>Estender margens e barras de rolagem
 As margens e barras de rolagem são os principais elementos de exibição do editor, além da exibição de texto em si. Você pode fornecer qualquer número de margens, além das margens padrão que aparecem ao contrário da exibição de texto.

 Implemente uma <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMargin> interface para definir uma margem. Você também deve implementar a <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider> interface para criar a margem.

 Para registrar o provedor de margem no editor, você deve exportar o provedor junto com os seguintes atributos:

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome da margem.

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: a ordem na qual a margem é exibida, em relação às outras margens.

   Estas são as margens internas:

  - "Barra de rolagem horizontal do WPF"

  - "Barra de rolagem vertical do WPF"

  - "Margem do número de linha do WPF"

    As margens horizontais que têm um atributo Order de `After="Wpf Horizontal Scrollbar"` são exibidas abaixo da margem interna, e as margens horizontais que têm um atributo Order de `Before ="Wpf Horizontal Scrollbar"` são exibidas acima da margem interna. As margens verticais direita que têm um atributo de pedido de `After="Wpf Vertical Scrollbar"` são exibidas à direita da barra de rolagem. As margens verticais esquerda que têm um atributo de ordem `After="Wpf Line Number Margin"` aparecem à esquerda da margem de número de linha (se estiver visível).

- <xref:Microsoft.VisualStudio.Text.Editor.MarginContainerAttribute>: o tipo de margem (esquerda, direita, superior ou inferior).

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: o tipo de conteúdo (por exemplo, "texto" ou "código") para o qual sua margem é válida.

  O exemplo a seguir mostra os atributos de exportação em um provedor de margem para uma margem que aparece à direita da margem de número de linha.

```
[Export(typeof(IWpfTextViewMarginProvider))]
[Name("TestMargin")]
[Order(Before = "Wpf Line Number Margin")]
[MarginContainer(PredefinedMarginNames.Left)]
[ContentType("text")]
```

## <a name="extend-tags"></a>Estender marcas
 As marcas são uma maneira de associar dados com diferentes tipos de texto. Em muitos casos, os dados associados são exibidos como um efeito visual, mas nem todas as marcas têm uma apresentação visual. Você pode definir seu próprio tipo de marca implementando <xref:Microsoft.VisualStudio.Text.Tagging.ITag> . Você também deve implementar <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> o para fornecer as marcas para um determinado conjunto de intervalos de texto e um <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> para fornecer o marcador. Você deve exportar o provedor de marcação junto com os seguintes atributos:

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: o tipo de conteúdo (por exemplo, "texto" ou "código") para o qual sua marca é válida.

- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>: o tipo de marca.

  O exemplo a seguir mostra os atributos de exportação em um provedor de marca.

\<CodeContentPlaceHolder>8 </CodeContentPlaceHolder> os seguintes tipos de marca são internos:

- <xref:Microsoft.VisualStudio.Text.Tagging.ClassificationTag>: associado a um <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> .

- <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>: associado a tipos de erro.

- <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>: associado a um Adornment.

  > [!NOTE]
  > Para obter um exemplo de um <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> , consulte a definição de HighlightWordTag no [passo a passos: realçar texto](../extensibility/walkthrough-highlighting-text.md).

- <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>: associado a regiões que podem ser expandidas ou recolhidas na estrutura de tópicos.

- <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>: define o espaço que um Adornment ocupa em uma exibição de texto. Para obter mais informações sobre adornos de negociação de espaço, consulte a seção a seguir.

- <xref:Microsoft.VisualStudio.Text.Editor.IntraTextAdornmentTag>: fornece espaçamento automático e dimensionamento para o Adornment.

  Para localizar e usar marcas para buffers e exibições, importe o <xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService> ou o <xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService> , que fornece um <xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601> tipo solicitado. O código a seguir importa esse serviço como uma propriedade.

```
[Import]
internal IViewTagAggregatorFactoryService ViewTagAggregatorFactoryService { get; set; }
```

#### <a name="tags-and-markerformatdefinitions"></a>Marcas e MarkerFormatDefinitions
 Você pode estender a <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition> classe para definir a aparência de uma marca. Você deve exportar sua classe (como um <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition> ) com os seguintes atributos:

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome usado para fazer referência a este formato

- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: isso faz com que o formato apareça na interface do usuário

  No construtor, você define o nome de exibição e a aparência da marca. <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.BackgroundColor%2A> define a cor de preenchimento e <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.ForegroundColor%2A> define a cor da borda. O <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.DisplayName%2A> é o nome localizável da definição de formato.

  Veja a seguir um exemplo de uma definição de formato:

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

 Para aplicar essa definição de formato a uma marca, referencie o nome que você definiu no atributo Name da classe (não o nome de exibição).

> [!NOTE]
> Para obter um exemplo de um <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition> , consulte a classe HighlightWordFormatDefinition em [Walkthrough: realçando texto](../extensibility/walkthrough-highlighting-text.md).

## <a name="extend-adornments"></a>Estender adornos
 Adorners definem efeitos visuais que podem ser adicionados ao texto exibido em uma exibição de texto ou à própria exibição de texto. Você pode definir seu próprio Adornment como qualquer tipo de <xref:System.Windows.UIElement> .

 Em sua classe Adornment, você deve declarar um <xref:Microsoft.VisualStudio.Text.Editor.AdornmentLayerDefinition> . Para registrar sua camada do Adornment, exporte-a junto com os seguintes atributos:

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome do Adornment.

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: a ordenação do Adornment em relação a outras camadas de Adornment. A classe <xref:Microsoft.VisualStudio.Text.Editor.PredefinedAdornmentLayers> define quatro camadas padrão: seleção, estrutura de tópicos, cursor e texto.

  O exemplo a seguir mostra os atributos de exportação em uma definição de camada Adornment.

```
[Export]
[Name("TestEmbeddedAdornment")]
[Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
internal AdornmentLayerDefinition testLayerDefinition;
```

 Você deve criar uma segunda classe que implemente <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> e manipule seu <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> evento ao instanciar o Adornment. Você deve exportar essa classe junto com os seguintes atributos:

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: o tipo de conteúdo (por exemplo, "texto" ou "código") para o qual o Adornment é válido.

- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>: o tipo de exibição de texto para o qual este Adornment é válido. A classe <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles> tem o conjunto de funções de exibição de texto predefinidas. Por exemplo, <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document> é usado principalmente para exibições de texto de arquivos. <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> é usado para exibições de texto que um usuário pode editar ou navegar usando um mouse e um teclado. Exemplos de <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> exibições são a exibição de texto do editor e a janela **saída** .

  O exemplo a seguir mostra os atributos de exportação no provedor Adornment.

```
[Export(typeof(IWpfTextViewCreationListener))]
[ContentType("csharp")]
[TextViewRole(PredefinedTextViewRoles.Document)]
internal sealed class TestAdornmentProvider : IWpfTextViewCreationListener
```

 Um Adornment de negociação de espaço é aquele que ocupa espaço no mesmo nível do texto. Para criar esse tipo de Adornment, você deve definir uma classe de marca que herda de <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag> , que define a quantidade de espaço ocupada pelo Adornment.

 Assim como em todos os adornos, você deve exportar a definição de camada Adornment.

```
[Export]
[Name("TestAdornment")]
[Order(After = DefaultAdornmentLayers.Text)]
internal AdornmentLayerDefinition testAdornmentLayer;
```

 Para instanciar a Adornment de negociação de espaço, você deve criar uma classe que implementa <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> , além da classe que implementa <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> (como com outros tipos de adornos).

 Para registrar o provedor de marcador, você deve exportá-lo junto com os seguintes atributos:

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: o tipo de conteúdo (por exemplo, "texto" ou "código") para o qual seu Adornment é válido.

- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>: o tipo de exibição de texto para o qual esta marca ou Adornment é válida. A classe <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles> tem o conjunto de funções de exibição de texto predefinidas. Por exemplo, <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document> é usado principalmente para exibições de texto de arquivos. <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> é usado para exibições de texto que um usuário pode editar ou navegar usando um mouse e um teclado. Exemplos de <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> exibições são a exibição de texto do editor e a janela **saída** .

- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>: o tipo de marca ou Adornment que você definiu. Você deve adicionar um segundo <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> para <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag> .

  O exemplo a seguir mostra os atributos de exportação no provedor do marcador para uma marca Adornment de negociação de espaço.

```
[Export(typeof(ITaggerProvider))]
[ContentType("text")]
[TextViewRole(PredefinedTextViewRoles.Document)]
[TagType(typeof(SpaceNegotiatingAdornmentTag))]
[TagType(typeof(TestSpaceNegotiatingTag))]
internal sealed class TestTaggerProvider : ITaggerProvider
```

## <a name="extending-mouse-processors"></a>Estendendo processadores do mouse
 Você pode adicionar tratamento especial para entrada do mouse. Crie uma classe que herda de <xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase> e substitua os eventos do mouse para a entrada que você deseja manipular. Você também deve implementar <xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider> em uma segunda classe e exportá-la junto com o <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> que especifica o tipo de conteúdo (por exemplo, "texto" ou "código") para o qual o manipulador do mouse é válido.

 O exemplo a seguir mostra os atributos de exportação em um provedor de processador do mouse.

```
[Export(typeof(IMouseProcessorProvider))]
[Name("test mouse processor")]
[ContentType("text")]
[TextViewRole(PredefinedTextViewRoles.Interactive)]
internal sealed class TestMouseProcessorProvider : IMouseProcessorProvider
```

## <a name="extend-drop-handlers"></a>Estender manipuladores de descarte
 Você pode personalizar o comportamento de drop handlers para tipos específicos de texto criando uma classe que implementa <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandler> e uma segunda classe que implementa <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandlerProvider> para criar o manipulador drop. Você deve exportar o manipulador drop junto com os seguintes atributos:

- <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.DropFormatAttribute>: o formato de texto para o qual esse manipulador de drop é válido. Os seguintes formatos são tratados em ordem de prioridade do mais alto para o mais baixo:

  1. Qualquer formato personalizado

  2. FileDrop

  3. EnhancedMetafile

  4. WaveAudio

  5. Metálica

  6. Diferencial

  7. Local

  8. Paleta

  9. PenData

  10. Serializável

  11. SymbolicLink

  12. XAML

  13. XamlPackage

  14. Tiff

  15. Bitmap

  16. DIB

  17. MetafilePicture

  18. CSV

  19. System.String

  20. Formato HTML

  21. UnicodeText

  22. OEMText

  23. Texto

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome do manipulador de remoção.

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: a ordenação do manipulador drop antes ou depois do manipulador de posicionamento padrão. O manipulador de posicionamento padrão para o Visual Studio é denominado "DefaultFileDropHandler".

  O exemplo a seguir mostra os atributos de exportação em um provedor de manipulador de descarte.

```
[Export(typeof(IDropHandlerProvider))]
[DropFormat("Text")]
[Name("TestDropHandler")]
[Order(Before="DefaultFileDropHandler")]
internal class TestDropHandlerProvider : IDropHandlerProvider
```

## <a name="extending-editor-options"></a>Estendendo opções do editor
 Você pode definir opções para serem válidas somente em um determinado escopo, por exemplo, em uma exibição de texto. O Editor fornece esse conjunto de opções predefinidas: opções do editor, opções de exibição e opções de exibição de Windows Presentation Foundation (WPF). Essas opções podem ser encontradas em <xref:Microsoft.VisualStudio.Text.Editor.DefaultOptions> , <xref:Microsoft.VisualStudio.Text.Editor.DefaultTextViewOptions> e <xref:Microsoft.VisualStudio.Text.Editor.DefaultWpfViewOptions> .

 Para adicionar uma nova opção, derive uma classe de uma destas classes de definição de opção:

- <xref:Microsoft.VisualStudio.Text.Editor.EditorOptionDefinition%601>

- <xref:Microsoft.VisualStudio.Text.Editor.ViewOptionDefinition%601>

- <xref:Microsoft.VisualStudio.Text.Editor.WpfViewOptionDefinition%601>

  O exemplo a seguir mostra como exportar uma definição de opção que tem um valor booliano.

```
[Export(typeof(EditorOptionDefinition))]
internal sealed class TestOption : EditorOptionDefinition<bool>
```

## <a name="extend-intellisense"></a>Estender o IntelliSense
 O IntelliSense é um termo geral para um grupo de recursos que fornecem informações sobre o texto estruturado e a conclusão da instrução para ele. Esses recursos incluem conclusão de instrução, ajuda de assinatura, informações rápidas e lâmpadas. A conclusão da instrução ajuda os usuários a digitarem corretamente um nome de palavra-chave ou de membro. A ajuda da assinatura exibe a assinatura ou as assinaturas para o método que o usuário acabou de digitar. Informações rápidas exibe uma assinatura completa para um nome de tipo ou membro quando o mouse é colocado sobre ele. A lâmpada fornece ações adicionais para determinados identificadores em determinados contextos, por exemplo, renomeando todas as ocorrências de uma variável depois que uma ocorrência for renomeada.

 O design de um recurso do IntelliSense é muito semelhante em todos os casos:

- Um *agente do* IntelliSense é responsável pelo processo geral.

- Uma *sessão* do IntelliSense representa a sequência de eventos entre o gatilho do apresentador e a confirmação ou cancelamento da seleção. A sessão é normalmente disparada por algum gesto do usuário.

- Um *controlador* IntelliSense é responsável por decidir quando a sessão deve começar e terminar. Ele também decide quando as informações devem ser confirmadas e quando a sessão deve ser cancelada.

- Uma *fonte* do IntelliSense fornece o conteúdo e decide a melhor correspondência.

- Um *apresentador* do IntelliSense é responsável por exibir o conteúdo.

  Na maioria dos casos, recomendamos que você forneça pelo menos uma origem e um controlador. Você também pode fornecer um apresentador se desejar personalizar a exibição.

### <a name="implement-an-intellisense-source"></a>Implementar uma fonte do IntelliSense
 Para personalizar uma fonte, você deve implementar uma (ou mais) das seguintes interfaces de origem:

- <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>

> [!IMPORTANT]
> <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSource> foi preterido em favor do <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> .

 Além disso, você deve implementar um provedor do mesmo tipo:

- <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>

> [!IMPORTANT]
> <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSourceProvider> foi preterido em favor do <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider> .

 Você deve exportar o provedor junto com os seguintes atributos:

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome da origem.

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: o tipo de conteúdo (por exemplo, "texto" ou "código") ao qual a origem se aplica.

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: a ordem na qual a origem deve aparecer (em relação a outras fontes).

- O exemplo a seguir mostra os atributos de exportação em um provedor de origem de conclusão.

```
Export(typeof(ICompletionSourceProvider))]
[Name(" Test Statement Completion Provider")]
[Order(Before = "default")]
[ContentType("text")]
internal class TestCompletionSourceProvider : ICompletionSourceProvider
```

 Para obter mais informações sobre como implementar fontes do IntelliSense, consulte as instruções a seguir:

- [Walkthrough: Exibir dicas de ferramenta QuickInfo](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)

- [Walkthrough: exibir a ajuda da assinatura](../extensibility/walkthrough-displaying-signature-help.md)

- [Passo a passo: exibir preenchimento de declaração](../extensibility/walkthrough-displaying-statement-completion.md)

### <a name="implement-an-intellisense-controller"></a>Implementar um controlador do IntelliSense
 Para personalizar um controlador, você deve implementar a <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController> interface. Além disso, você deve implementar um provedor de controlador junto com os seguintes atributos:

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: o nome do controlador.

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: o tipo de conteúdo (por exemplo, "texto" ou "código") ao qual o controlador se aplica.

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: a ordem na qual o controlador deve aparecer (com relação a outros controladores).

  O exemplo a seguir mostra atributos de exportação em um provedor de controlador de conclusão.

```
Export(typeof(IIntellisenseControllerProvider))]
[Name(" Test Controller Provider")]
[Order(Before = "default")]
[ContentType("text")]
internal class TestIntellisenseControllerProvider : IIntellisenseControllerProvider
```

 Para obter mais informações sobre como usar os controladores do IntelliSense, consulte as instruções a seguir:

- [Walkthrough: Exibir dicas de ferramenta QuickInfo](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)
