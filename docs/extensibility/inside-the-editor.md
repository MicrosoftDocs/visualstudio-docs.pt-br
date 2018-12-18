---
title: Dentro do Editor | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - architecture
ms.assetid: 822cbb8d-7ab4-40ee-bd12-44016ebcce81
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 18587516298fa58e8a5e783ffb1f7c37d5a6b497
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49859675"
---
# <a name="inside-the-editor"></a>Dentro do editor
O editor é composto de um número de diferentes subsistemas, que são projetados para impedir que o editor de texto separado de modelo a exibição de texto e a interface do usuário.  
  
 Estas seções descrevem diferentes aspectos do editor:  
  
- [Visão geral dos subsistemas](../extensibility/inside-the-editor.md#overview-of-the-subsystems)  
  
- [O modelo de texto](../extensibility/inside-the-editor.md#the-text-model)  
  
- [A exibição de texto](../extensibility/inside-the-editor.md#the-text-view)  
  
  Estas seções descrevem os recursos do editor:  
  
- [Classificadores e marcas](../extensibility/inside-the-editor.md#tags-and-classifiers)  
  
- [Adornos](../extensibility/inside-the-editor.md#adornments)  
  
- [Projeção](../extensibility/inside-the-editor.md#projection)  
  
- [Estrutura de tópicos](../extensibility/inside-the-editor.md#outlining)  
  
- [Associações de mouse](../extensibility/inside-the-editor.md#mousebindings)  
  
- [Operações de editor](../extensibility/inside-the-editor.md#editoroperations)  
  
- [IntelliSense](../extensibility/inside-the-editor.md#intellisense)  
  
## <a name="overview-of-the-subsystems"></a>Visão geral dos subsistemas  
  
### <a name="text-model-subsystem"></a>Subsistema de modelo de texto  
 O subsistema de modelo de texto é responsável por representação de texto e habilitar sua manipulação. O subsistema de modelo de texto contém o <xref:Microsoft.VisualStudio.Text.ITextBuffer> interface, que descreve a sequência de caracteres a ser exibido pelo editor. Esse texto pode ser modificado, controlado e manipulado de várias maneiras. O modelo de texto também fornece tipos para os seguintes aspectos:  
  
- Um serviço que associa a arquivos de texto e gerencia lendo e gravando-os no sistema de arquivos.  
  
- Um serviço diferencial que localiza as diferenças mínimas entre duas sequências de objetos.  
  
- Um sistema para descrever o texto em um buffer em termos de subconjuntos do texto em outros buffers.  
  
  O subsistema de modelo de texto é livre de conceitos (UI) de interface do usuário. Por exemplo, não é responsável pela formatação de texto ou o layout de texto, e ele não tem conhecimento de adornos visual que pode ser associado com o texto.  
  
  Os tipos públicos do subsistema de modelo de texto estão contidos em *Microsoft.VisualStudio.Text.Data.dll* e *Microsoft.VisualStudio.CoreUtility.dll*, que depende de apenas a base do .NET Framework biblioteca de classes e a estrutura de MEF (Managed Extensibility).  
  
### <a name="text-view-subsystem"></a>Subsistema de modo de exibição de texto  
 O subsistema de modo de exibição de texto é responsável por formatar e exibir texto. Os tipos nesse subsistema são divididos em duas camadas, dependendo se os tipos se baseiam no Windows Presentation Foundation (WPF). Os tipos mais importantes são <xref:Microsoft.VisualStudio.Text.Editor.ITextView> e <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>, que controlam o conjunto de linhas de texto que devem ser exibidas e também o cursor, a seleção e os recursos para o adorno de texto por meio de elementos de UI do WPF. Esse subsistema fornece também a área de exibição de margens ao redor do texto. Dessas margens podem ser estendidas e podem conter diferentes tipos de efeitos de conteúdo e o visuais. Exemplos de margens são linha número exibe e barras de rolagem.  
  
 Os tipos públicos do subsistema de modo de exibição de texto estão contidos em *Microsoft.VisualStudio.Text.UI.dll* e *Microsoft.VisualStudio.Text.UI.Wpf.dll*. O primeiro conjunto contém os elementos de independente de plataforma e o segundo contém os elementos do WPF específicos.  
  
### <a name="classification-subsystem"></a>Subsistema de classificação  
 O subsistema de classificação é responsável por determinar propriedades de fonte para texto. Um classificador quebra o texto em classes diferentes, por exemplo, "palavra-chave" ou "comment". O mapa de formatação de classificação se relaciona essas classes com propriedades de fonte real, por exemplo, "azul Consolas 10 pt". Essas informações são usadas pelo modo de exibição de texto quando ele formata e renderiza o texto. Marcação, que é descrito em mais detalhes mais adiante neste tópico, permite que os dados a serem associados com intervalos de texto.  
  
 Os tipos públicos do subsistema de classificação estão contidos em Microsoft.VisualStudio.Text.Logic.dll, e eles interagem com os aspectos visuais de classificação, que estão contidos em Microsoft.VisualStudio.Text.UI.Wpf.dll.  
  
### <a name="operations-subsystem"></a>Subsistema de operações  
 O subsistema de operações define o comportamento do editor. Ele fornece a implementação de comandos de editor do Visual Studio e o sistema de desfazer.  
  
## <a name="a-closer-look-at-the-text-model-and-the-text-view"></a>Examinar mais detalhadamente o modelo de texto e a exibição de texto  
  
### <a name="the-text-model"></a>O modelo de texto  
 O subsistema de modelo de texto consiste em diferentes grupos de tipos de texto. Isso inclui o buffer de texto, os instantâneos de texto e os intervalos de texto.  
  
#### <a name="text-buffers-and-text-snapshots"></a>Buffers de texto e os instantâneos de texto  
 O <xref:Microsoft.VisualStudio.Text.ITextBuffer> interface representa uma sequência de caracteres Unicode que são codificados usando UTF-16, que é a codificação usada pelo `String` tipo no .NET Framework. Um buffer de texto pode ser mantido como um documento do sistema de arquivos, mas isso não é necessário.  
  
 O <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService> é usado para criar um buffer de texto vazio ou um buffer de texto que é inicializado a partir de uma cadeia de caracteres ou <xref:System.IO.TextReader>. O buffer de texto pode ser transferido para o sistema de arquivos como um <xref:Microsoft.VisualStudio.Text.ITextDocument>.  
  
 O buffer de texto pode ser editado por qualquer thread até que um thread se apropria de buffer de texto chamando <xref:Microsoft.VisualStudio.Text.ITextBuffer.TakeThreadOwnership%2A>. Depois disso, somente esse thread pode executar as edições.  
  
 Um buffer de texto pode passar por várias versões durante seu ciclo de vida. Uma nova versão é gerada sempre que o buffer é editado e um imutável <xref:Microsoft.VisualStudio.Text.ITextSnapshot> representa o conteúdo dessa versão do buffer. Como os instantâneos de texto são imutáveis, você pode acessar um instantâneo de texto em qualquer thread, sem restrições, mesmo se ele representa o buffer de texto continua a mudar.  
  
#### <a name="text-snapshots-and-text-snapshot-lines"></a>Instantâneos de texto e linhas de instantâneo de texto  
 Você pode exibir o conteúdo de um instantâneo de texto como uma sequência de caracteres ou como uma sequência de linhas. Caracteres e as linhas são que ambas indexados começando com zero. Um instantâneo de texto vazio contém zero caracteres e uma linha vazia. Uma linha é delimitada por qualquer sequência válida de caracteres de quebra de linha Unicode ou pelo início ou no final do buffer. Caracteres de quebra de linha explicitamente são representados no instantâneo de texto e as quebras de linha em um instantâneo de texto não tiverem o mesmo.  
  
> [!NOTE]
>  Para obter mais informações sobre caracteres de quebra de linha no editor do Visual Studio, consulte [codificações e quebras de linha](../ide/encodings-and-line-breaks.md).  
  
 Uma linha de texto é representada por um <xref:Microsoft.VisualStudio.Text.ITextSnapshotLine> objeto, que pode ser obtido de um instantâneo de texto para um número de linha específico ou para uma posição de caractere específico.  
  
#### <a name="snapshotpoints-snapshotspans-and-normalizedsnapshotspancollections"></a>SnapshotPoints, SnapshotSpans e NormalizedSnapshotSpanCollections  
 Um <xref:Microsoft.VisualStudio.Text.SnapshotPoint> representa uma posição de caractere em um instantâneo. A posição é garantido que se encontram entre zero e o tamanho do instantâneo. Um <xref:Microsoft.VisualStudio.Text.SnapshotSpan> representa um intervalo de texto em um instantâneo. Sua posição final é garantido que se encontram entre zero e o tamanho do instantâneo. O <xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection> consiste em um conjunto de <xref:Microsoft.VisualStudio.Text.SnapshotSpan> objetos do mesmo instantâneo.  
  
#### <a name="spans-and-normalizedspancollections"></a>Intervalos e NormalizedSpanCollections  
 Um <xref:Microsoft.VisualStudio.Text.Span> representa um intervalo que pode ser aplicado a um intervalo de texto em um instantâneo de texto. Posições de instantâneo são baseados em zero, então spans podem começar em qualquer posição incluindo zero. O `End` propriedade de uma extensão é igual à soma dos seus `Start` propriedade e seu `Length` propriedade. Um `Span` não inclui o caractere que é indexado pelo `End` propriedade. Por exemplo, um intervalo que tem início = 5 e comprimento = 3 tem fim = 8, e inclui os caracteres nas posições 5, 6 e 7. A notação para este alcance é 5..8).  
  
 Dois intervalos de interseção se eles tiverem qualquer posições em comum, incluindo a posição final. Portanto, a interseção de [3, 5) e [2, 7) é [3, 5) e a interseção de [3, 5) e [5, 7) é [5, 5). (Observe que [5, 5) é um intervalo vazio.)  
  
 Dois intervalos sobreponham, se eles têm em comum, posições, exceto para a posição final. Um intervalo vazio nunca se sobrepõe a qualquer outro intervalo e a sobreposição das duas extensões nunca está vazia.  
  
 Um <xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection> é uma lista de extensões na ordem as propriedades de início dos intervalos. Na lista de intervalos sobrepostos ou adjacentes são mesclados. Por exemplo, dado o conjunto de intervalos [5..9), [0..1), [3..6), e [9..10), a lista normalizada de spans é [0..1), [3..10).  
  
#### <a name="itextedit-textversion-and-text-change-notifications"></a>As notificações de alteração ITextEdit, TextVersion e texto  
 O conteúdo de um buffer de texto pode ser alterado usando um <xref:Microsoft.VisualStudio.Text.ITextEdit> objeto. Criação de tal objeto (usando um dos `CreateEdit()` métodos de <xref:Microsoft.VisualStudio.Text.ITextBuffer>) inicia uma transação de texto que consiste em edições de texto. Cada edição é um substituto de algum intervalo de texto no buffer por uma cadeia de caracteres. O conteúdo de cada edição e as coordenadas são expressas em relação ao instantâneo do buffer, quando a transação foi iniciada. O <xref:Microsoft.VisualStudio.Text.ITextEdit> objeto ajusta as coordenadas de edições que são afetadas por outras edições na mesma transação.  
  
 Por exemplo, considere um buffer de texto que contém essa cadeia de caracteres:  
  
```  
abcdefghij  
```  
  
 Aplicar uma transação que contém as duas edições, uma edição que substitui o alcance em [2..4) usando o caractere `X` e uma segunda edição que substitui o alcance em [6..9) usando o caractere `Y`. O resultado é esse buffer:  
  
```  
abXefYj  
```  
  
 As coordenadas para a segunda edição foram calculadas em relação ao conteúdo do buffer no início da transação, antes da primeira edição foi aplicada.  
  
 As alterações no buffer em vigor quando o <xref:Microsoft.VisualStudio.Text.ITextEdit> objeto é confirmado, chamando seu `Apply()` método. Se houver pelo menos uma edição de não vazio, um novo <xref:Microsoft.VisualStudio.Text.ITextVersion> é criado, um novo <xref:Microsoft.VisualStudio.Text.ITextSnapshot> é criado e um `Changed` é gerado. Cada versão de texto tem outro instantâneo do texto. Um instantâneo de texto representa o estado do buffer de texto completo após uma transação de edição, mas uma versão de texto descreve somente as alterações de um instantâneo para a próxima. Em geral, os instantâneos de texto são deve ser usado uma vez e depois são descartados, enquanto as versões de texto devem permanecer ativos por algum tempo.  
  
 Uma versão de texto contém uma <xref:Microsoft.VisualStudio.Text.INormalizedTextChangeCollection>. Esta coleção descreve as alterações que, quando aplicada ao instantâneo, produzirá o instantâneo subsequente. Cada <xref:Microsoft.VisualStudio.Text.ITextChange> na coleção contém a posição do caractere da alteração, a cadeia de caracteres substituída e a cadeia de caracteres de substituição. A cadeia de caracteres substituída está vazia para uma inserção básica e a cadeia de caracteres de substituição está vazia para uma exclusão básica. A coleção normalizada é sempre `null` para a versão mais recente do buffer de texto.  
  
 Apenas um <xref:Microsoft.VisualStudio.Text.ITextEdit> objeto pode ser instanciado para um buffer de texto a qualquer momento, e todas as edições de texto devem ser executadas no thread que possui o buffer de texto (se a propriedade tiver sido declarada). Uma edição de texto pode ser abandonada chamando seus `Cancel` método ou seus `Dispose` método.  
  
 <xref:Microsoft.VisualStudio.Text.ITextBuffer> também fornece `Insert()`, `Delete()`, e `Replace()` métodos semelhantes aos encontrados no <xref:Microsoft.VisualStudio.Text.ITextEdit> interface. Chamando essas tem o mesmo efeito que a criação de um <xref:Microsoft.VisualStudio.Text.ITextEdit> objeto, fazendo a chamada semelhante e, em seguida, aplicando a edição.  
  
#### <a name="tracking-points-and-tracking-spans"></a>Pontos de controle e rastreamento spans  
 Um <xref:Microsoft.VisualStudio.Text.ITrackingPoint> representa uma posição de caractere em um buffer de texto. Se o buffer é editado de forma que faz com que a posição do caractere para deslocar, o ponto de controle se desloca com ele. Por exemplo, se um ponto de controle se refere à posição 10 em um buffer e cinco caracteres serão inseridos no início do buffer, o ponto de controle, em seguida, refere-se à posição 15. Se uma inserção ocorrer precisamente a posição indicada pelo ponto de controle, seu comportamento é determinado pelo seu <xref:Microsoft.VisualStudio.Text.PointTrackingMode>, que poderá ser `Positive` ou `Negative`. Se o modo de controle for positivo, que o ponto de controle refere-se para o mesmo caractere, que agora está no final da inserção; Se o modo de controle for negativo, o ponto de controle refere-se para o primeiro caractere inserido na posição original. Se o caractere na posição em que é representado por um ponto de acompanhamento for excluído, o ponto de controle é deslocado para o primeiro caractere que segue o intervalo de exclusão. Por exemplo, se um ponto de controle refere-se para o caractere na posição 5 e os caracteres nas posições de 3 a 6 são excluídos, o ponto de controle refere-se para o caractere na posição 3.  
  
 Um <xref:Microsoft.VisualStudio.Text.ITrackingSpan> representa um intervalo de caracteres em vez de apenas uma posição. Seu comportamento é determinado pela sua <xref:Microsoft.VisualStudio.Text.SpanTrackingMode>. Se for o modo de controle de span <xref:Microsoft.VisualStudio.Text.SpanTrackingMode>, o alcance de acompanhamento cresce para incorporar o texto inserido em suas bordas; se o modo de controle de alcance é <xref:Microsoft.VisualStudio.Text.SpanTrackingMode>, o alcance de acompanhamento não incorpora o texto inserido em suas bordas. No entanto, se for o modo de controle de span <xref:Microsoft.VisualStudio.Text.SpanTrackingMode>, uma inserção envia por push a posição atual até o início e se o modo de controle de span <xref:Microsoft.VisualStudio.Text.SpanTrackingMode>, uma inserção envia por push a posição atual na direção do final.  
  
 Você pode obter a posição de um ponto de controle ou o alcance de uma extensão de rastreamento para qualquer instantâneo de buffer de texto ao qual pertencem. Pontos de controle e rastreamento spans podem ser consultados com segurança de qualquer thread.  
  
#### <a name="content-types"></a>Tipos de conteúdo  
 Tipos de conteúdo são um mecanismo para definir diferentes tipos de conteúdo. Um tipo de conteúdo pode ser um tipo de arquivo, como "text", "código" ou "binary" ou um tipo de tecnologia, como "xml", "vb" ou "c#". Por exemplo, a palavra "using" é uma palavra-chave em c# e Visual Basic, mas não em outras linguagens de programação. Portanto, a definição da palavra-chave this poderia ser limitada aos tipos de conteúdo "c#" e "vb".  
  
 Tipos de conteúdo são usados como um filtro de adornos e outros elementos do editor. Muitos recursos do editor e pontos de extensão são definidos por tipo de conteúdo. Por exemplo, cores de texto é diferente para os arquivos de texto sem formatação, arquivos XML e arquivos de código de origem do Visual Basic. Buffers de texto geralmente são atribuídos a um tipo de conteúdo quando eles são criados, e o tipo de conteúdo de um buffer de texto pode ser alterado.  
  
 Tipos de conteúdo podem herdar várias de outros tipos de conteúdo. O <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> permite que você especifique vários tipos de base como pais de um determinado tipo de conteúdo.  
  
 Os desenvolvedores podem definir seus próprios tipos de conteúdo e registrá-los usando o <xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>. Vários recursos do editor podem ser definidos em relação a um tipo específico de conteúdo usando o <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>. Por exemplo, margens do editor, adornos e manipuladores de mouse podem ser definidos para que eles se aplicam somente a editores que exibem tipos específicos de conteúdo.  
  
###  <a name="the-text-view"></a>A exibição de texto  
 A parte de modo de exibição do padrão de controller (MVC) de modo de exibição de modelo define o modo de exibição de texto, a formatação da exibição, elementos gráficos, como a barra de rolagem e o cursor. Todos os elementos de apresentação do editor do Visual Studio baseiam-se no WPF.  
  
#### <a name="text-views"></a>Modos de exibição de texto  
 O <xref:Microsoft.VisualStudio.Text.Editor.ITextView> interface é uma representação independente de plataforma de uma exibição de texto. Ele é usado principalmente para exibir documentos de texto em uma janela, mas ele pode também ser usado para outras finalidades, por exemplo, em uma dica de ferramenta.  
  
 A exibição de texto faz referência a tipos diferentes de buffers de texto. O <xref:Microsoft.VisualStudio.Text.Editor.ITextView.TextViewModel%2A> propriedade se refere a um <xref:Microsoft.VisualStudio.Text.Editor.ITextViewModel> objeto que aponta para esses três buffers de texto diferente: o buffer de dados, que é o buffer de dados de nível superior, buffer de edição, em que a edição ocorre e o buffer de visual, que é o buffer que é exibido no modo de exibição de texto.  
  
 O texto é formatado com base em dos classificadores que estão anexados ao buffer de texto subjacente e é adornado por meio de provedores de adorno que estão anexados à exibição de texto em si.  
  
#### <a name="the-text-view-coordinate-system"></a>O sistema de coordenadas do modo de exibição de texto  
 O sistema de coordenadas do modo de exibição de texto Especifica posições na exibição de texto. Nesse sistema de coordenadas, o valor de x 0.0 corresponde à borda esquerda do texto que está sendo exibido, e o valor de y 0.0 corresponde até a borda superior do texto que está sendo exibido. A coordenada x aumenta da esquerda para a direita e a coordenada y aumenta de cima para baixo.  
  
 Um visor (a parte do texto visível na janela de texto) não pode ser rolado da mesma maneira horizontalmente conforme ele é rolado verticalmente. Um visor é rolado horizontalmente alterando sua coordenada esquerda para que ele se mova em relação à superfície de desenho. No entanto, um visor pode ser rolado verticalmente alterando o texto renderizado, o que faz com que um <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> evento seja acionado.  
  
 Distâncias no sistema de coordenadas correspondem aos pixels lógicos. Se a superfície de renderização de texto é exibida sem uma transformação de escala, uma unidade no sistema de coordenadas de renderização de texto corresponde a um pixel na exibição.  
  
#### <a name="margins"></a>Margens  
 O <xref:Microsoft.VisualStudio.Text.Editor.ITextViewMargin> interface representa uma margem e habilita o controle da visibilidade da margem e seu tamanho. Há quatro margens predefinidas, que são nomeadas "Top", "Esquerda", "Direita" e "Inferior" e anexadas à parte superior, inferior, esquerda ou borda direita de uma exibição. Dessas margens são contêineres no qual outras margens podem ser colocadas. A interface define os métodos que retornam o tamanho da margem e a visibilidade de uma margem. As margens são elementos visuais que fornecem informações adicionais sobre o modo de exibição de texto para o qual eles estão conectados. Por exemplo, a margem de número de linha exibe números de linha para a exibição de texto. A margem do ícone exibe elementos de interface do usuário.  
  
 O <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider> interface manipula a criação e o posicionamento das margens. Margens podem ser ordenadas em relação à outra margem. Margens de prioridade mais alta são mais próximo a exibição de texto. Por exemplo, se houver margens esquerdas, margem A e B de margem e margem B tem uma prioridade menor que a margem A, B de margem aparece à esquerda da margem A.  
  
#### <a name="the-text-view-host"></a>O host do modo de exibição de texto  
 O <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> interface contém a exibição de texto e qualquer decorações adjacentes que acompanham o modo de exibição, por exemplo, as barras de rolagem. O host do modo de exibição de texto também contém as margens que estão anexadas a uma borda do modo de exibição.  
  
#### <a name="formatted-text"></a>Texto formatado  
 O texto que é exibido em uma exibição de texto é composto de <xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> objetos. Cada linha da exibição de texto corresponde a uma linha de texto no modo de exibição de texto. Longas linhas no buffer de texto subjacente podem ser parcialmente obscurecidas (se a quebra de texto não estiver habilitada) ou divididas em várias linhas de exibição de texto. O <xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> interface contém métodos e propriedades para o mapeamento entre as coordenadas e caracteres e para os adornos que podem ser associados com a linha.  
  
 <xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> objetos são criados usando um <xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource> interface. Se você estiver preocupado apenas com o texto que é exibido atualmente no modo de exibição, você pode ignorar a origem da formatação. Se você estiver interessado no formato de texto que não é exibido no modo de exibição (por exemplo, para dar suporte a um RTF recortar e colar), você pode usar <xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource> para formatar o texto em um buffer de texto.  
  
 A exibição de texto formata um <xref:Microsoft.VisualStudio.Text.ITextSnapshotLine> por vez.  
  
## <a name="editor-features"></a>Recursos do editor  
 Os recursos do editor são projetados para que a definição do recurso é separada da sua implementação. O editor inclui os seguintes recursos:  
  
-   Classificadores e marcas  
  
-   Adornos  
  
-   Projeção  
  
-   Estrutura de tópicos  
  
-   Associações de mouse e a chave  
  
-   Operações e os primitivos  
  
-   IntelliSense  
  
### <a name="tags-and-classifiers"></a>Classificadores e marcas  
 As marcas são marcadores que estão associados um intervalo de texto. Podem ser apresentados de maneiras diferentes, por exemplo, usando cores de texto, sublinhados, gráficos ou pop-ups. Classificadores são um tipo de marca.  
  
 Outros tipos de marcas são <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> para o realce de texto <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag> para a estrutura de tópicos, e <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag> para erros de compilação.  
  
#### <a name="classification-types"></a>Tipos de classificação  
 Um <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> interface representa uma classe de equivalência, que é uma categoria abstrata de texto. Tipos de classificação podem herdar várias de outros tipos de classificação. Por exemplo, a classificações de linguagem de programação pode incluir "palavra-chave", "comment" e "identificador", que herda de "código". Tipos de classificação de linguagem natural podem incluir "substantivo", "verbo" e "adjetivo", que herdam de "idioma natural".  
  
#### <a name="classifications"></a>Classificações  
 Uma classificação é uma instância de um tipo específico de classificação, geralmente ao longo de um intervalo de texto. Um <xref:Microsoft.VisualStudio.Text.Classification.ClassificationSpan> é usado para representar uma classificação. Um intervalo de classificação pode ser pensado como um rótulo que abrange um intervalo específico de texto e informa ao sistema que este trecho de texto é de um tipo de classificação específica.  
  
#### <a name="classifiers"></a>Classificadores  
 Um <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> é um mecanismo que quebra o texto em um conjunto de classificações. Classificadores devem ser definidos para tipos específicos de conteúdo e instanciadas para buffers de texto específico. Os clientes devem implementar <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> para participar de classificação de texto.  
  
#### <a name="classifier-aggregators"></a>Agregadores de classificador  
 Um agregador de classificador é um mecanismo que combina todos os classificadores de buffer de texto de uma em apenas um conjunto de classificações. Por exemplo, um classificador do c# e um classificador de idioma inglês podem criar classificações sobre um comentário em um arquivo c#. Considere este comentário:  
  
```  
// This method produces a classifier  
```  
  
 Um classificador de c# pode rotular o período inteiro como um comentário e a classificação do idioma inglês pode classificar "produz" como "verbo" e "método" como um "substantivo". O agregador produz um conjunto de classificações não sobrepostos e o tipo do conjunto se baseia em todas as contribuições.  
  
 Um agregador de classificador também é um classificador porque ele quebra o texto em um conjunto de classificações. O agregador de classificador também garante que não há nenhuma sobreposição classificações e que as classificações são classificadas. Classificadores individuais são livres para retornar qualquer conjunto de classificações, em qualquer ordem e sobrepostos de qualquer forma.  
  
#### <a name="classification-formatting-and-text-coloring"></a>Formatação de classificação e a coloração de texto  
 Formatação de texto é um exemplo de um recurso que se baseia a classificação de texto. Ela é usada pela camada de exibição de texto para determinar a exibição do texto em um aplicativo. Depende da área de formatação de texto no WPF, mas a definição de lógica de classificações não é.  
  
 Um formato de classificação é um conjunto de propriedades para um tipo de classificação específica de formatação. Esses formatos herdam o formato do pai do tipo de classificação.  
  
 Um <xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap> é um mapa de um tipo de classificação para um conjunto de propriedades de formatação de texto. A implementação do mapa no editor de formato manipula todas as exportações de formatos de classificação.  
  
###   <a name="adornments"></a>Adornos  
 Adornos são efeitos gráficos que não estão diretamente relacionados a fonte e cor dos caracteres na exibição de texto. Por exemplo, o sublinhado de uma linha ondulada vermelha que é usado para marcar o código não compilar em várias linguagens de programação é um adorno incorporado e dicas de ferramenta são adornos pop-up. Adornos são derivados <xref:System.Windows.UIElement> e implementar <xref:Microsoft.VisualStudio.Text.Tagging.ITag>. Dois tipos especializados de marca de adorno são as <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>, para adornos que ocupam o mesmo espaço que o texto em uma exibição, e o <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>, para o sublinhado Rabisco.  
  
 Adornos incorporados são gráficos que fazem parte do modo de exibição de texto formatado. Eles são organizados em camadas diferentes da ordem Z. Há três camadas internas, da seguinte maneira: texto, o cursor e a seleção. No entanto, os desenvolvedores podem definir mais camadas e colocá-los na ordem em relação a uma da outra. Os três tipos de adornos incorporados são adornos de texto relativo (que se move quando move o texto e são excluídos quando o texto será excluído), adornos relativo do modo de exibição (que tem a ver com partes não são de texto da exibição) e controlado pelo proprietário adornos (os desenvolvedor deve gerenciar seu posicionamento).  
  
 Pop-up adornos são gráficos que aparecem em uma pequena janela acima da exibição de texto, por exemplo, as dicas de ferramenta.  
  
###  <a name="projection"></a> Projeção  
 Projeção é uma técnica para a criação de um tipo diferente de buffer de texto que não armazena texto, mas em vez disso, combina texto dos outros buffers de texto. Por exemplo, um buffer de projeção pode ser usado para concatenar o texto de dois outros buffers e apresentará o resultado como se estivesse em apenas um buffer ou ocultar partes do texto em um buffer. Um buffer de projeção pode agir como um buffer de origem para outro buffer de projeção. Um conjunto de buffers que são relacionados por projeção pode ser construído para reorganizar o texto de várias maneiras diferentes. (Esse conjunto também é conhecido como um *grafo de buffer*.) O recurso de estrutura de tópicos de texto do Visual Studio é implementado por meio de um buffer de projeção para ocultar o texto recolhido e editor do Visual Studio para as páginas ASP.NET usa a projeção para oferecer suporte a idiomas incorporados como Visual Basic e c#.  
  
 Uma <xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer> é criado usando <xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService>. Um buffer de projeção é representado por uma sequência ordenada de <xref:Microsoft.VisualStudio.Text.ITrackingSpan> objetos que são conhecidos como *intervalos de origem*. O conteúdo de um desses intervalos é apresentado como uma sequência de caracteres. Os buffers de texto do qual os intervalos de origem são desenhados são nomeados *buffers de fonte*. Os clientes de um buffer de projeção é preciso estar ciente de que ele difere de um buffer de texto comum.  
  
 O buffer de projeção escuta para eventos de alteração de texto em buffers de fonte. Quando o texto em uma fonte abrangem as alterações, o buffer de projeção mapeia as coordenadas de texto alterado para seus próprio coordenadas e gera eventos de alteração de texto apropriado. Por exemplo, considere os buffers de origem A e B com esses conteúdos:  
  
```  
A: ABCDE  
B: vwxyz  
```  
  
 Se o buffer de projeção P é formado por dois intervalos de texto, um que tenha todos do buffer de e outros que tem todos os buffers B, P tem o seguinte conteúdo:  
  
```  
P: ABCDEvwxyz  
```  
  
 Se a subcadeia de caracteres `xy` é excluído do buffer de B, em seguida, o buffer P gera um evento que indica que os caracteres nas posições 7 e 8 foram excluídos.  
  
 O buffer de projeção também pode ser editado diretamente. Ele propaga edições para os buffers de fonte apropriada. Por exemplo, se uma cadeia de caracteres é inserida no buffer P na posição 6 (a posição original do caractere "v"), a inserção é propagada para o buffer B na posição 1.  
  
 Há restrições sobre os intervalos de origem que contribuem para um buffer de projeção. Não podem se sobrepor a intervalos de origem; um local em um buffer de projeção não é possível mapear a mais de um local em qualquer buffer de origem e um local em um buffer de origem não é possível mapear a mais de um local em um buffer de projeção. Nenhum circularities são permitidas na relação de buffer de origem.  
  
 Eventos são gerados quando o conjunto de código-fonte armazena em buffer para um alterações de buffer de projeção e quando o conjunto de código-fonte abrange as alterações.  
  
 Um buffer de elisão é um tipo especial de buffer de projeção. Ele é usado principalmente para a estrutura de tópicos e para operações que expandir e recolher blocos de texto. Um buffer de elisão baseia-se apenas um buffer de origem e os intervalos no buffer de elisão devem ordenados da mesma maneira como eles serão ordenados no buffer de origem.  
  
#### <a name="the-buffer-graph"></a>O gráfico de buffer  
 O <xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph> interface habilita o mapeamento entre um gráfico de buffers de projeção. Todos os buffers de texto e buffers de projeção são coletados em um grafo acíclico direcionado, assim como a árvore de sintaxe abstrata que é produzido por um compilador de linguagem. O gráfico é definido pelo buffer superior, que pode ser qualquer buffer de texto. O gráfico de buffer pode mapear a partir de um ponto no buffer superior a um ponto em um buffer de origem ou um intervalo no buffer superior a um conjunto de extensões em um buffer de origem. Da mesma forma, ele pode mapear um ponto ou variam de um buffer de origem para um ponto no buffer superior. Gráficos de buffer são criados usando o <xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService>.  
  
#### <a name="events-and-projection-buffers"></a>Eventos e buffers de projeção  
 Quando um buffer de projeção é modificado, as modificações são enviadas do buffer de projeção para os buffers que dependem dele. Depois que todos os buffers são modificados, são gerados eventos de alteração de buffer, começando com o buffer mais profundo.  
  
###  <a name="outlining"></a> Estrutura de tópicos  
 Estrutura de tópicos é a capacidade de expandir ou recolher blocos de texto em uma exibição de texto diferentes. Estrutura de tópicos é definida como um tipo de <xref:Microsoft.VisualStudio.Text.Tagging.ITag>, da mesma maneira que adornos são definidos. Um <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag> é uma marca que define uma região de texto que pode ser expandida ou recolhida. Para usar a estrutura de tópicos, você deve importar o <xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService> para obter um <xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager>. Enumera o Gerenciador de estrutura de tópicos, recolhe e expande os blocos diferentes, que são representados como <xref:Microsoft.VisualStudio.Text.Outlining.ICollapsible> objetos e gera eventos adequadamente.  
  
###  <a name="mousebindings"></a> Associações de mouse  
 Associações de mouse vincular movimentos do mouse a comandos diferentes. Associações de mouse são definidas usando um <xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider>, e as associações de teclas são definidas usando um <xref:Microsoft.VisualStudio.Text.Editor.IKeyProcessorProvider>. O <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> automaticamente cria uma instância de todas as associações e conecta-se para eventos de mouse no modo de exibição.  
  
 O <xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessor> interface contém manipuladores de eventos de pré-processar e pós-processamento para eventos de mouse diferente. A alça de um dos eventos, você pode substituir alguns dos métodos em <xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase>.  
  
###  <a name="editoroperations"></a> Operações de editor  
 Operações do Editor podem ser usadas para automatizar a interação com o editor, para scripts ou outras finalidades. Você pode importar o <xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService> para operações de acesso em um determinado <xref:Microsoft.VisualStudio.Text.Editor.ITextView>. Em seguida, você pode usar esses objetos para modificar a seleção, role para a exibição ou mover o cursor para diferentes partes da exibição.  
  
###  <a name="intellisense"></a> IntelliSense  
 Dá suporte ao IntelliSense, preenchimento de declaração, a Ajuda da assinatura (também conhecido como informações de parâmetro), informações rápidas e lâmpadas.  
  
 Preenchimento de declaração fornece listas pop-up de possíveis conclusões para nomes de método, os elementos XML e outros elementos de código ou marcação. Em geral, um gesto do usuário invoca uma sessão de conclusão. A sessão exibe a lista de possíveis conclusões e o usuário pode selecionar um ou descartar a lista. O <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker> é responsável por criar e disparar o <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession>. O <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> calcula o <xref:Microsoft.VisualStudio.Language.Intellisense.CompletionSet> de itens de conclusão para a sessão.  
  
## <a name="see-also"></a>Consulte também  
 [Pontos de extensão de editor e o serviço de linguagem](../extensibility/language-service-and-editor-extension-points.md)   
 [Importações do Editor](../extensibility/editor-imports.md)
