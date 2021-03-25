---
title: Dentro do editor
description: Saiba mais sobre os subsistemas e recursos do editor. Você pode estender os recursos do editor do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - architecture
ms.assetid: 822cbb8d-7ab4-40ee-bd12-44016ebcce81
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0bd45bb0a47de7283d75c083edc46b6fc38fe7d3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079196"
---
# <a name="inside-the-editor"></a>Dentro do editor

O editor é composto por vários subsistemas diferentes, que são projetados para manter o modelo de texto do editor separado da exibição de texto e da interface do usuário.

Estas seções descrevem diferentes aspectos do editor:

- [Visão geral dos subsistemas](../extensibility/inside-the-editor.md#overview-of-the-subsystems)

- [O modelo de texto](../extensibility/inside-the-editor.md#the-text-model)

- [A exibição de texto](../extensibility/inside-the-editor.md#the-text-view)

Estas seções descrevem os recursos do editor:

- [Marcas e classificadores](../extensibility/inside-the-editor.md#tags-and-classifiers)

- [Adornos](../extensibility/inside-the-editor.md#adornments)

- [Projeção](../extensibility/inside-the-editor.md#projection)

- [Estrutura de tópicos](../extensibility/inside-the-editor.md#outlining)

- [Associações do mouse](../extensibility/inside-the-editor.md#mouse-bindings)

- [Operações do editor](../extensibility/inside-the-editor.md#editor-operations)

- [IntelliSense](../extensibility/inside-the-editor.md#intellisense)

## <a name="overview-of-the-subsystems"></a>Visão geral dos subsistemas

### <a name="text-model-subsystem"></a>Subsistema de modelo de texto

O subsistema de modelo de texto é responsável por representar o texto e habilitar sua manipulação. O subsistema de modelo de texto contém a <xref:Microsoft.VisualStudio.Text.ITextBuffer> interface, que descreve a sequência de caracteres que deve ser exibida pelo editor. Esse texto pode ser modificado, controlado e, de outra forma, manipulado de várias maneiras. O modelo de texto também fornece tipos para os seguintes aspectos:

- Um serviço que associa texto a arquivos e gerencia a leitura e a gravação no sistema de arquivos.

- Um serviço de diferenciação que localiza as diferenças mínimas entre duas sequências de objetos.

- Um sistema para descrever o texto em um buffer em termos de subconjuntos do texto em outros buffers.

O subsistema de modelo de texto é gratuito dos conceitos da interface do usuário. Por exemplo, ele não é responsável por formatação de texto ou layout de texto e não tem conhecimento de adornos visuais que possam ser associados ao texto.

Os tipos públicos do subsistema de modelo de texto estão contidos em *Microsoft.VisualStudio.Text.Data.dll* e *Microsoft.VisualStudio.CoreUtility.dll*, que dependem apenas da biblioteca de classes base .NET Framework e do Managed Extensibility Framework (MEF).

### <a name="text-view-subsystem"></a>Subsistema de exibição de texto

O subsistema de exibição de texto é responsável por Formatar e exibir texto. Os tipos nesse subsistema são divididos em duas camadas, dependendo se os tipos dependem de Windows Presentation Foundation (WPF). Os tipos mais importantes são <xref:Microsoft.VisualStudio.Text.Editor.ITextView> e <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> , que controlam o conjunto de linhas de texto que devem ser exibidas e também o acento circunflexo, a seleção e os recursos para adornar o texto usando elementos da interface do usuário do WPF. Esse subsistema também fornece margens sobre a área de exibição de texto. Essas margens podem ser estendidas e podem conter tipos diferentes de conteúdo e efeitos visuais. Exemplos de margens são exibições de número de linha e barras de rolagem.

Os tipos públicos do subsistema de exibição de texto estão contidos em *Microsoft.VisualStudio.Text.UI.dll* e *Microsoft.VisualStudio.Text.UI.Wpf.dll*. O primeiro assembly contém os elementos independentes de plataforma e o segundo contém os elementos específicos do WPF.

### <a name="classification-subsystem"></a>Subsistema de classificação

O subsistema de classificação é responsável por determinar as propriedades da fonte para o texto. Um classificador quebra o texto em diferentes classes, por exemplo, "palavra-chave" ou "comentário". O mapa de formato de classificação relaciona essas classes às propriedades de fonte reais, por exemplo, "Blue consolas 10 pt". Essas informações são usadas pela exibição de texto quando formatam e renderizam texto. A marcação, que é descrita em mais detalhes posteriormente neste tópico, permite que os dados sejam associados a intervalos de texto.

Os tipos públicos do subsistema de classificação estão contidos no Microsoft.VisualStudio.Text.Logic.dll e interagem com os aspectos visuais da classificação, que estão contidos em Microsoft.VisualStudio.Text.UI.Wpf.dll.

### <a name="operations-subsystem"></a>Subsistema de operações

O subsistema de operações define o comportamento do editor. Ele fornece a implementação para comandos do editor do Visual Studio e o sistema de desfazer.

## <a name="a-closer-look-at-the-text-model-and-the-text-view"></a>Uma análise mais detalhada do modelo de texto e da exibição de texto

### <a name="the-text-model"></a>O modelo de texto

O subsistema de modelo de texto consiste em diferentes agrupamentos de tipos de texto. Isso inclui o buffer de texto, instantâneos de texto e intervalos de texto.

#### <a name="text-buffers-and-text-snapshots"></a>Buffers de texto e instantâneos de texto

A <xref:Microsoft.VisualStudio.Text.ITextBuffer> interface representa uma sequência de caracteres Unicode que são codificados usando UTF-16, que é a codificação usada pelo `String` tipo na .NET Framework. Um buffer de texto pode ser persistido como um documento do sistema de arquivos, mas isso não é necessário.

O <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService> é usado para criar um buffer de texto vazio ou um buffer de texto que é inicializado a partir de uma cadeia de caracteres ou de <xref:System.IO.TextReader> . O buffer de texto pode ser persistido no sistema de arquivos como um <xref:Microsoft.VisualStudio.Text.ITextDocument> .

Qualquer thread pode editar o buffer de texto até que um thread assuma a propriedade do buffer de texto chamando <xref:Microsoft.VisualStudio.Text.ITextBuffer.TakeThreadOwnership%2A> . Depois disso, somente esse thread pode executar edições.

Um buffer de texto pode passar por várias versões durante seu tempo de vida. Uma nova versão é gerada toda vez que o buffer é editado e uma imutável <xref:Microsoft.VisualStudio.Text.ITextSnapshot> representa o conteúdo dessa versão do buffer. Como os instantâneos de texto são imutáveis, você pode acessar um instantâneo de texto em qualquer thread, sem restrições, mesmo que o buffer de texto que ele representa continue a ser alterado.

#### <a name="text-snapshots-and-text-snapshot-lines"></a>Instantâneos de texto e linhas de instantâneo de texto

Você pode exibir o conteúdo de um instantâneo de texto como uma sequência de caracteres ou como uma sequência de linhas. Os caracteres e as linhas são indexados a partir de zero. Um instantâneo de texto vazio contém zero caracteres e uma linha vazia. Uma linha é delimitada por qualquer sequência de caracteres de quebra de linha Unicode válida ou pelo início ou pelo fim do buffer. Os caracteres de quebra de linha são representados explicitamente no instantâneo de texto, e as quebras de linha em um instantâneo de texto nem todos precisam ser iguais.

> [!NOTE]
> Para obter mais informações sobre caracteres de quebra de linha no editor do Visual Studio, consulte [codificações e quebras de linha](../ide/encodings-and-line-breaks.md).

Uma linha de texto é representada por um <xref:Microsoft.VisualStudio.Text.ITextSnapshotLine> objeto, que pode ser obtido de um instantâneo de texto para um número de linha específico ou para uma posição de caractere específica.

#### <a name="snapshotpoints-snapshotspans-and-normalizedsnapshotspancollections"></a>SnapshotPoints, SnapshotSpans e NormalizedSnapshotSpanCollections

Um <xref:Microsoft.VisualStudio.Text.SnapshotPoint> representa uma posição de caractere em um instantâneo. A posição tem a garantia de estar entre zero e o comprimento do instantâneo. Um <xref:Microsoft.VisualStudio.Text.SnapshotSpan> representa um intervalo de texto em um instantâneo. A posição final tem a garantia de estar entre zero e o comprimento do instantâneo. O <xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection> consiste em um conjunto de <xref:Microsoft.VisualStudio.Text.SnapshotSpan> objetos do mesmo instantâneo.

#### <a name="spans-and-normalizedspancollections"></a>Spans e NormalizedSpanCollections

Um <xref:Microsoft.VisualStudio.Text.Span> representa um intervalo que pode ser aplicado a um intervalo de texto em um instantâneo de texto. As posições de instantâneos são baseadas em zero, portanto, as extensões podem começar em qualquer posição, incluindo zero. A `End` propriedade de um Span é igual à soma de sua `Start` propriedade e sua `Length` propriedade. Um não `Span` inclui o caractere que é indexado pela `End` propriedade. Por exemplo, um Span com Start = 5 e length = 3 tem end = 8 e inclui os caracteres nas posições 5, 6 e 7. A notação para esse intervalo é [5.. 8).

Dois spans se interseccionam se tiverem qualquer posição em comum, incluindo a posição final. Portanto, a interseção de [3, 5) e [2, 7) é [3, 5) e a interseção de [3, 5) e [5, 7) é [5, 5). (Observe que [5, 5) é um intervalo vazio.)

Duas estendes se sobrepõem se tiverem posições em comum, exceto para a posição final. Um Span vazio nunca sobrepõe qualquer outro span e a sobreposição de duas extensões nunca está vazia.

Um <xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection> é uma lista de Spans na ordem das propriedades iniciais das extensões. Na lista, as extensões sobrepostas ou adjacentes são mescladas. Por exemplo, considerando o conjunto de Spans [5.. 9), [0.. 1), [3.. 6) e [9.. 10), a lista normalizada de Spans é [0.. 1), [3.. 10).

#### <a name="itextedit-textversion-and-text-change-notifications"></a>Notificações de alteração de texto e ITextEdit, textversion

O conteúdo de um buffer de texto pode ser alterado usando um <xref:Microsoft.VisualStudio.Text.ITextEdit> objeto. A criação de um objeto desse tipo (usando um dos `CreateEdit()` métodos de <xref:Microsoft.VisualStudio.Text.ITextBuffer> ) inicia uma transação de texto que consiste em edições de texto. Cada edição é uma substituição de algum intervalo de texto no buffer por uma cadeia de caracteres. As coordenadas e o conteúdo de cada edição são expressos em relação ao instantâneo do buffer quando a transação foi iniciada. O <xref:Microsoft.VisualStudio.Text.ITextEdit> objeto ajusta as coordenadas das edições que são afetadas por outras edições na mesma transação.

Por exemplo, considere um buffer de texto que contém esta cadeia de caracteres:

```
abcdefghij
```

Aplique uma transação que contém duas edições, uma edição que substitui a extensão em [2.. 4) usando o caractere `X` e uma segunda edição que substitui a extensão em [6.9) usando o caractere `Y` . O resultado é esse buffer:

```
abXefYj
```

As coordenadas para a segunda edição foram computadas em relação ao conteúdo do buffer no início da transação, antes da aplicação da primeira edição.

As alterações no buffer entram em vigor quando o <xref:Microsoft.VisualStudio.Text.ITextEdit> objeto é confirmado chamando seu `Apply()` método. Se houver pelo menos uma edição não vazia, um novo <xref:Microsoft.VisualStudio.Text.ITextVersion> será criado, um novo <xref:Microsoft.VisualStudio.Text.ITextSnapshot> será criado e um `Changed` evento será gerado. Cada versão de texto tem um instantâneo de texto diferente. Um instantâneo de texto representa o estado completo do buffer de texto após uma transação de edição, mas uma versão de texto descreve apenas as alterações de um instantâneo para o próximo. Em geral, os instantâneos de texto devem ser usados uma vez e, em seguida, descartados, enquanto as versões de texto precisam permanecer ativas por algum tempo.

Uma versão de texto contém um <xref:Microsoft.VisualStudio.Text.INormalizedTextChangeCollection> . Esta coleção descreve as alterações que, quando aplicadas ao instantâneo, produzem o instantâneo subsequente. Cada <xref:Microsoft.VisualStudio.Text.ITextChange> na coleção contém a posição do caractere da alteração, a cadeia de caracteres substituída e a cadeia de caracteres de substituição. A cadeia de caracteres substituída está vazia para uma inserção básica e a cadeia de caracteres de substituição está vazia para uma exclusão básica. A coleção normalizada sempre é `null` para a versão mais recente do buffer de texto.

Somente um <xref:Microsoft.VisualStudio.Text.ITextEdit> objeto pode ser instanciado para um buffer de texto a qualquer momento, e todas as edições de texto devem ser executadas no thread que possui o buffer de texto (se a propriedade tiver sido reivindicada). Uma edição de texto pode ser abandonada chamando seu `Cancel` método ou seu `Dispose` método.

<xref:Microsoft.VisualStudio.Text.ITextBuffer> também fornece `Insert()` `Delete()` métodos, e `Replace()` que se assemelham aos encontrados na <xref:Microsoft.VisualStudio.Text.ITextEdit> interface. Chamar esses efeitos tem o mesmo efeito que criar um <xref:Microsoft.VisualStudio.Text.ITextEdit> objeto, fazer a chamada semelhante e, em seguida, aplicar a edição.

#### <a name="tracking-points-and-tracking-spans"></a>Pontos de rastreamento e spans de rastreamento

Um <xref:Microsoft.VisualStudio.Text.ITrackingPoint> representa uma posição de caractere em um buffer de texto. Se o buffer for editado de forma que faça com que a posição do caractere seja deslocada, o ponto de controle será deslocado com ele. Por exemplo, se um ponto de controle se referir à posição 10 em um buffer e cinco caracteres forem inseridos no início do buffer, o ponto de controle fará referência à posição 15. Se uma inserção ocorrer exatamente na posição denotada pelo ponto de controle, seu comportamento será determinado por seu <xref:Microsoft.VisualStudio.Text.PointTrackingMode> , que pode ser `Positive` ou `Negative` . Se o modo de controle for positivo, o ponto de controle se referirá ao mesmo caractere, que agora está no final da inserção. Se o modo de controle for negativo, o ponto de controle se referirá ao primeiro caractere inserido na posição original. Se o caractere na posição representada por um ponto de controle for excluído, o ponto de controle mudará para o primeiro caractere que segue o intervalo excluído. Por exemplo, se um ponto de controle se referir ao caractere na posição 5, e os caracteres nas posições de 3 a 6 forem excluídos, o ponto de controle se referirá ao caractere na posição 3.

Um <xref:Microsoft.VisualStudio.Text.ITrackingSpan> representa um intervalo de caracteres em vez de apenas uma posição. Seu comportamento é determinado por seu <xref:Microsoft.VisualStudio.Text.SpanTrackingMode> . Se o modo de controle de span for [SpanTrackingMode. EdgeInclusive](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeInclusive), o intervalo de acompanhamento aumentará para incorporar o texto inserido em suas bordas. Se o modo de controle de span for [SpanTrackingMode. EdgeExclusive](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeExclusive), o alcance de rastreamento não incorporará o texto inserido em suas bordas. No entanto, se o modo de controle de span for [SpanTrackingMode. EdgePositive](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgePositive), uma inserção enviará a posição atual para o início e, se o modo de controle de span for [SpanTrackingMode. EdgeNegative](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeNegative), uma inserção enviará por push a posição atual para o final.

Você pode obter a posição de um ponto de controle ou o intervalo de um trecho de controle para qualquer instantâneo do buffer de texto ao qual eles pertencem. Os pontos de rastreamento e as extensões de rastreamento podem ser referenciados com segurança de qualquer thread.

#### <a name="content-types"></a>Tipos de conteúdo

Os tipos de conteúdo são um mecanismo para definir diferentes tipos de conteúdo. Um tipo de conteúdo pode ser um tipo de arquivo, como "texto", "código" ou "binário", ou um tipo de tecnologia, como "XML", "vb" ou "c#". Por exemplo, a palavra "using" é uma palavra-chave em C# e Visual Basic, mas não em outras linguagens de programação. Portanto, a definição dessa palavra-chave seria limitada aos tipos de conteúdo "c#" e "vb".

Os tipos de conteúdo são usados como um filtro para adornos e outros elementos do editor. Muitos recursos do editor e pontos de extensão são definidos por tipo de conteúdo. Por exemplo, a coloração de texto é diferente para arquivos de texto sem formatação, arquivos XML e arquivos de código-fonte de Visual Basic. Em geral, os buffers de texto são atribuídos a um tipo de conteúdo quando eles são criados, e o tipo de conteúdo de um buffer de texto pode ser alterado.

Tipos de conteúdo podem ser múltiplos herdados de outros tipos de conteúdo. O <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> permite que você especifique vários tipos base como os pais de um determinado tipo de conteúdo.

Os desenvolvedores podem definir seus próprios tipos de conteúdo e registrá-los usando o <xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService> . Muitos recursos do editor podem ser definidos em relação a um tipo de conteúdo específico usando o <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> . Por exemplo, as margens do editor, adorners e manipuladores de mouse podem ser definidos para que se apliquem somente a editores que exibem tipos de conteúdo específicos.

### <a name="the-text-view"></a>A exibição de texto

A parte de exibição do padrão MVC (Model View Controller) define a exibição de texto, a formatação da exibição, os elementos gráficos, como a barra de rolagem e o cursor. Todos os elementos de apresentação do editor do Visual Studio são baseados no WPF.

#### <a name="text-views"></a>Exibições de texto

A <xref:Microsoft.VisualStudio.Text.Editor.ITextView> interface é uma representação independente de plataforma de uma exibição de texto. Ele é usado principalmente para exibir documentos de texto em uma janela, mas também pode ser usado para outras finalidades, por exemplo, em uma dica de ferramenta.

A exibição de texto faz referência a diferentes tipos de buffers de texto. A <xref:Microsoft.VisualStudio.Text.Editor.ITextView.TextViewModel%2A> Propriedade refere-se a um <xref:Microsoft.VisualStudio.Text.Editor.ITextViewModel> objeto que aponta para esses três buffers de texto diferentes: o buffer de dados, que é o buffer de nível de dados superior, o buffer de edição, no qual ocorre a edição e o buffer Visual, que é o buffer que é exibido na exibição de texto.

O texto é formatado com base nos classificadores que são anexados ao buffer de texto subjacente e é adornado usando os provedores de Adornment que são anexados à exibição de texto em si.

#### <a name="the-text-view-coordinate-system"></a>O sistema de coordenadas de exibição de texto

O sistema de coordenadas da exibição de texto especifica as posições na exibição de texto. Nesse sistema de coordenadas, o valor x 0,0 corresponde à borda esquerda do texto que está sendo exibido e o valor y 0,0 corresponde à borda superior do texto que está sendo exibido. A coordenada x aumenta da esquerda para a direita e a coordenada y aumenta de cima para baixo.

Um visor (a parte do texto visível na janela de texto) não pode ser rolado da mesma maneira horizontalmente, pois é rolado verticalmente. Um visor é rolado horizontalmente alterando sua coordenada à esquerda para que ele se mova em relação à superfície de desenho. No entanto, um visor pode ser rolado verticalmente apenas alterando o texto renderizado, o que faz com que um <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> evento seja gerado.

As distâncias no sistema de coordenadas correspondem a pixels lógicos. Se a superfície de renderização de texto for exibida sem uma transformação de dimensionamento, uma unidade no sistema de coordenadas de renderização de texto corresponderá a um pixel na exibição.

#### <a name="margins"></a>Margens

A <xref:Microsoft.VisualStudio.Text.Editor.ITextViewMargin> interface representa uma margem e habilita o controle da visibilidade da margem e seu tamanho. Há quatro margens predefinidas, que são nomeadas como "superior", "esquerda", "direita" e "inferior" e anexadas à borda superior, inferior, esquerda ou direita de uma exibição. Essas margens são contêineres em que outras margens podem ser colocadas. A interface define métodos que retornam o tamanho da margem e a visibilidade de uma margem. Margens são elementos visuais que fornecem informações adicionais sobre a exibição de texto à qual eles estão anexados. Por exemplo, a margem de número de linha exibe números de linha para a exibição de texto. A margem do glifo exibe elementos da interface do usuário.

A <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider> interface manipula a criação e o posicionamento de margens. As margens podem ser ordenadas em relação a outras margens. As margens de prioridade mais alta estão localizadas mais perto da exibição de texto. Por exemplo, se houver duas margens à esquerda, A margem A e A margem B, e a margem B tiver uma prioridade mais baixa do que A margem A, a margem B será exibida à esquerda da margem A.

#### <a name="the-text-view-host"></a>O host de exibição de texto

A <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> interface contém a exibição de texto e todas as decorações adjacentes que acompanham a exibição, por exemplo, barras de rolagem. O host de exibição de texto também contém margens que são anexadas a uma borda da exibição.

#### <a name="formatted-text"></a>Texto formatado

O texto que é exibido em uma exibição de texto é composto de <xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> objetos. Cada linha de exibição de texto corresponde a uma linha de texto na exibição de texto. As linhas longas no buffer de texto subjacente podem ser parcialmente obscurecidas (se a quebra automática de linha não estiver habilitada) ou dividida em várias linhas de exibição de texto. A <xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> interface contém métodos e propriedades para mapeamento entre coordenadas e caracteres e para os adornos que podem ser associados à linha.

<xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> os objetos são criados usando uma <xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource> interface. Se você estiver preocupado apenas com o texto atualmente exibido na exibição, poderá ignorar a fonte de formatação. Se você estiver interessado no formato de texto que não é exibido na exibição (por exemplo, para dar suporte a um recorte e colagem em Rich Text), você pode usar <xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource> para formatar texto em um buffer de texto.

Os formatos de exibição de texto um de <xref:Microsoft.VisualStudio.Text.ITextSnapshotLine> cada vez.

## <a name="editor-features"></a>Recursos do editor

Os recursos do editor são projetados de forma que a definição do recurso seja separada da sua implementação. O editor inclui estes recursos:

- Marcas e classificadores

- Adornos

- Projeção

- Estrutura de tópicos

- Associações de tecla e mouse

- Operações e primitivos

- IntelliSense

### <a name="tags-and-classifiers"></a>Marcas e classificadores

Marcas são marcadores associados a um intervalo de texto. Eles podem ser apresentados de maneiras diferentes, por exemplo, usando cores de texto, sublinhados, gráficos ou pop-ups. Os classificadores são um tipo de marca.

Outros tipos de marcas são <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> para realce de texto, <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag> para estrutura de tópicos e <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag> para erros de compilação.

#### <a name="classification-types"></a>Tipos de classificação

Uma <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> interface representa uma classe equivalente, que é uma categoria abstrata de texto. Os tipos de classificação podem ser múltiplos herdados de outros tipos de classificação. Por exemplo, as classificações de linguagem de programação podem incluir "palavra-chave", "comentário" e "identificador", que são herdados de "código". Os tipos de classificação de idioma natural podem incluir "substantivo", "verbo" e "adjetivo", que são herdados de "idioma natural".

#### <a name="classifications"></a>Classificações

Uma classificação é uma instância de um tipo de classificação específico, normalmente em um intervalo de texto. Um <xref:Microsoft.VisualStudio.Text.Classification.ClassificationSpan> é usado para representar uma classificação. Uma extensão de classificação pode ser considerada como um rótulo que cobre um determinado trecho de texto e informa ao sistema que esse intervalo de texto é de um tipo de classificação específico.

#### <a name="classifiers"></a>Classificadores

Um <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> é um mecanismo que quebra o texto em um conjunto de classificações. Os classificadores devem ser definidos para tipos de conteúdo específicos e instanciados para buffers de texto específicos. Os clientes devem implementar o <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> para participar da classificação de texto.

#### <a name="classifier-aggregators"></a>Agregadores de classificação

Um agregador de classificador é um mecanismo que combina todos os classificadores de um buffer de texto em apenas um conjunto de classificações. Por exemplo, um classificador C# e um classificador de idioma inglês poderiam criar classificações sobre um comentário em um arquivo C#. Considere este comentário:

```
// This method produces a classifier
```

Um classificador C# pode rotular toda a abrangência como um comentário, e o classificador de idioma Inglês pode classificar "produz" como um "verbo" e "Method" como um "substantivo". O agregador produz um conjunto de classificações não sobrepostas e o tipo do conjunto é baseado em todas as contribuições.

Um agregador de classificador também é um classificador porque quebra o texto em um conjunto de classificações. O agregador de classificador também garante que não haja classificações sobrepostas e que as classificações sejam classificadas. Classificadores individuais são livres para retornar qualquer conjunto de classificações, em qualquer ordem, e se sobrepõem de qualquer forma.

#### <a name="classification-formatting-and-text-coloring"></a>Formatação de classificação e cores de texto

A formatação de texto é um exemplo de um recurso criado na classificação de texto. Ele é usado pela camada de exibição de texto para determinar a exibição do texto em um aplicativo. A área de formatação de texto depende do WPF, mas a definição lógica de classificações não.

Um formato de classificação é um conjunto de propriedades de formatação para um tipo de classificação específico. Esses formatos herdam do formato do pai do tipo de classificação.

Um <xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap> é um mapa de um tipo de classificação para um conjunto de propriedades de formatação de texto. A implementação do mapa de formato no editor manipula todas as exportações de formatos de classificação.

### <a name="adornments"></a>Adornos

Adorners são efeitos gráficos que não estão diretamente relacionados à fonte e à cor dos caracteres na exibição de texto. Por exemplo, o sublinhado vermelho ondulado que é usado para marcar código de não compilação em muitas linguagens de programação é um Adornment incorporado, e as dicas de ferramenta são adornos pop-up. Adorners são derivados <xref:System.Windows.UIElement> e implementados <xref:Microsoft.VisualStudio.Text.Tagging.ITag> . Dois tipos especializados de marca Adornment são o <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag> , para adornos que ocupam o mesmo espaço que o texto em uma exibição e o <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag> , para o sublinhado ondulado.

Adorners inseridos são elementos gráficos que formam parte da exibição de texto formatado. Elas são organizadas em camadas de ordem Z diferentes. Há três camadas internas, da seguinte maneira: texto, o cursor e a seleção. No entanto, os desenvolvedores podem definir mais camadas e colocá-las em ordem em relação umas com as outras. Os três tipos de adornos incorporados são adorners relativos a texto (que se movem quando o texto se move e são excluídos quando o texto é excluído), além de adornos de exibição relativos (que têm que fazer com partes de não texto da exibição) e adorners controlados pelo proprietário (o desenvolvedor deve gerenciar seu posicionamento).

Adornos de pop-up são elementos gráficos que aparecem em uma pequena janela acima da exibição de texto, por exemplo, dicas de ferramenta.

### <a name="projection"></a><a name="projection"></a> Projeção

A projeção é uma técnica para construir um tipo diferente de buffer de texto que, na verdade, não armazena texto, mas combina texto de outros buffers de texto. Por exemplo, um buffer de projeção pode ser usado para concatenar o texto de dois outros buffers e apresentar o resultado como se ele estiver em apenas um buffer ou para ocultar partes do texto em um buffer. Um buffer de projeção pode atuar como um buffer de origem para outro buffer de projeção. Um conjunto de buffers relacionados por projeção pode ser construído para reorganizar o texto de várias maneiras diferentes. (Esse conjunto também é conhecido como grafo de *buffer*.) O recurso de estrutura de texto do Visual Studio é implementado usando um buffer de projeção para ocultar o texto recolhido e o editor do Visual Studio para páginas ASP.NET usa projeção para dar suporte a idiomas incorporados, como Visual Basic e C#.

Um <xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer> é criado usando o <xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService> . Um buffer de projeção é representado por uma sequência ordenada de <xref:Microsoft.VisualStudio.Text.ITrackingSpan> objetos que são conhecidos como *spans de origem*. O conteúdo dessas extensões é apresentado como uma sequência de caracteres. Os buffers de texto dos quais as extensões de origem são desenhadas são os *buffers de origem* nomeados. Os clientes de um buffer de projeção não precisam estar cientes de que diferem de um buffer de texto comum.

O buffer de projeção escuta os eventos de alteração de texto nos buffers de origem. Quando o texto em um span de origem é alterado, o buffer de projeção mapeia as coordenadas de texto alteradas para suas próprias coordenadas e gera eventos de alteração de texto apropriados. Por exemplo, considere os buffers de origem A e B que têm o conteúdo:

```
A: ABCDE
B: vwxyz
```

Se o buffer de projeção P for formado de dois intervalos de texto, um que tenha todo o buffer A e o outro que tenha todo o buffer B, o P terá o seguinte conteúdo:

```
P: ABCDEvwxyz
```

Se a subcadeia de caracteres `xy` for excluída do buffer B, o buffer P gerará um evento que indica que os caracteres nas posições 7 e 8 foram excluídos.

O buffer de projeção também pode ser editado diretamente. Ele propaga edições para os buffers de origem apropriados. Por exemplo, se uma cadeia de caracteres for inserida no buffer P na posição 6 (a posição original do caractere "v"), a inserção será propagada para o buffer B na posição 1.

Há restrições nas extensões de origem que contribuem para um buffer de projeção. As extensões de origem não podem se sobrepor; um local em um buffer de projeção não pode ser mapeado para mais de um local em qualquer buffer de origem, e um local em um buffer de origem não pode ser mapeado para mais de um local em um buffer de projeção. Nenhuma circularidade é permitida no relacionamento de buffer de origem.

Os eventos são gerados quando o conjunto de buffers de origem de um buffer de projeção é alterado e quando o conjunto de origens abrange alterações.
Um buffer corrotina é um tipo especial de buffer de projeção. Ele é usado principalmente para estruturar e para operações que expandem e recolhem blocos de texto. Um buffer corrotina é baseado em apenas um buffer de origem, e os spans no buffer corrotina devem ser ordenados da mesma forma que são ordenados no buffer de origem.

#### <a name="the-buffer-graph"></a>O grafo de buffer

A <xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph> interface habilita o mapeamento em um grafo de buffers de projeção. Todos os buffers de texto e os buffers de projeção são coletados em um grafo acíclico direcionado, assim como a árvore de sintaxe abstrata que é produzida por um compilador de linguagem. O grafo é definido pelo buffer superior, que pode ser qualquer buffer de texto. O grafo de buffer pode mapear de um ponto no buffer superior para um ponto em um buffer de origem ou de um intervalo no buffer superior para um conjunto de Spans em um buffer de origem. Da mesma forma, ele pode mapear um ponto ou um intervalo de um buffer de origem para um ponto no buffer superior. Os gráficos de buffer são criados usando o <xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService> .

#### <a name="events-and-projection-buffers"></a>Eventos e buffers de projeção

Quando um buffer de projeção é modificado, as modificações são enviadas do buffer de projeção para os buffers que dependem dele. Depois que todos os buffers são modificados, os eventos de alteração do buffer são gerados, começando com o buffer mais profundo.

### <a name="outlining"></a>Estrutura de tópicos

A estrutura de tópicos é a capacidade de expandir ou recolher diferentes blocos de texto em uma exibição de texto. A estrutura de tópicos é definida como uma espécie de <xref:Microsoft.VisualStudio.Text.Tagging.ITag> , da mesma maneira como os adornos são definidos. Um <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag> é uma marca que define uma região de texto que pode ser expandida ou recolhida. Para usar a estrutura de tópicos, você deve importar o <xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService> para obter um <xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager> . O gerente de estrutura de tópicos enumera, recolhe e expande os diferentes blocos, que são representados como <xref:Microsoft.VisualStudio.Text.Outlining.ICollapsible> objetos, e gera eventos de acordo.

### <a name="mouse-bindings"></a>Associações do mouse

As ligações do mouse vinculam os movimentos do mouse a comandos diferentes. As associações de mouse são definidas usando um <xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider> , e as associações de chave são definidas usando um <xref:Microsoft.VisualStudio.Text.Editor.IKeyProcessorProvider> . O <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> instancia automaticamente todas as associações e as conecta aos eventos do mouse na exibição.

A <xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessor> interface contém manipuladores de eventos de pré-processamento e pós-processamento para diferentes eventos de mouse. Para lidar com um dos eventos, você pode substituir alguns dos métodos no <xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase> .

### <a name="editor-operations"></a>Operações do editor

As operações do editor podem ser usadas para automatizar a interação com o editor, para scripts ou outras finalidades. Você pode importar o <xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService> para as operações de acesso em um determinado <xref:Microsoft.VisualStudio.Text.Editor.ITextView> . Você pode usar esses objetos para modificar a seleção, rolar a exibição ou mover o cursor para partes diferentes da exibição.

### <a name="intellisense"></a>IntelliSense

O IntelliSense dá suporte à conclusão de instrução, à ajuda da assinatura (também conhecida como informações de parâmetro), a informações rápidas e a lâmpadas.

A conclusão da instrução fornece listas pop-up de possíveis conclusões para nomes de métodos, elementos XML e outros elementos de codificação ou marcação. Em geral, um gesto de usuário invoca uma sessão de conclusão. A sessão exibe a lista de possíveis conclusões e o usuário pode selecionar uma ou ignorar a lista. O <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker> é responsável por criar e disparar o <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession> . O <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> computa os <xref:Microsoft.VisualStudio.Language.Intellisense.CompletionSet> itens de conclusão para a sessão.

## <a name="see-also"></a>Confira também

- [Pontos de extensão do serviço de linguagem e do editor](../extensibility/language-service-and-editor-extension-points.md)
- [Importações do editor](../extensibility/editor-imports.md)
