---
title: Visão geral do modelo de objeto do Word
description: O modelo de objeto do Word consiste em classes e interfaces que são fornecidas no assembly de interoperabilidade primário para o Word e são definidas no namespace do Word.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word object model
- Word [Office development in Visual Studio], object model
- object models [Office development in Visual Studio], Office
- object models [Office development in Visual Studio], Word
- objects [Office development in Visual Studio], Office object models
- Office object models
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3367c1ad557c647639b9fd2d2aacf7845e067660
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826623"
---
# <a name="word-object-model-overview"></a>Visão geral do modelo de objeto do Word
  Ao desenvolver soluções do Word no Visual Studio, você interage com o modelo de objeto do Word. Esse modelo de objeto consiste em classes e interfaces que são fornecidas no assembly de interoperabilidade primário para o Word e são definidas no <xref:Microsoft.Office.Interop.Word> namespace.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 Este tópico fornece uma breve visão geral do modelo de objeto do Word. Para obter recursos em que você pode aprender mais sobre o modelo de objeto do Word inteiro, consulte [usar a documentação do modelo de objeto do Word](#WordOMDocumentation).

 Para obter informações sobre como usar o modelo de objeto do Word para executar tarefas específicas, consulte os seguintes tópicos:

- [Trabalhar com documentos](../vsto/working-with-documents.md)

- [Trabalhar com texto em documentos](../vsto/working-with-text-in-documents.md)

- [Trabalhar com tabelas](../vsto/working-with-tables.md)

## <a name="understand-the-word-object-model"></a><a name="understanding"></a> Entender o modelo de objeto do Word
 O Word fornece centenas de objetos com os quais você pode interagir. Esses objetos são organizados em uma hierarquia que segue de maneira mais próxima a interface do usuário. Na parte superior da hierarquia está o <xref:Microsoft.Office.Interop.Word.Application> objeto. Esse objeto representa a instância atual do Word. O <xref:Microsoft.Office.Interop.Word.Application> objeto contém os <xref:Microsoft.Office.Interop.Word.Document> <xref:Microsoft.Office.Interop.Word.Selection> objetos,, <xref:Microsoft.Office.Interop.Word.Bookmark> e <xref:Microsoft.Office.Interop.Word.Range> . Cada um desses objetos tem muitos métodos e propriedades que você pode acessar para manipular e interagir com o objeto.

 A ilustração a seguir mostra uma exibição desses objetos na hierarquia do modelo de objeto do Word.

 ![Gráfico de modelo de objeto do Word](../vsto/media/wrwordobjectmodel.gif "Gráfico de modelo de objeto do Word")

 À primeira vista, os objetos parecem se sobrepor. Por exemplo, os <xref:Microsoft.Office.Interop.Word.Document> <xref:Microsoft.Office.Interop.Word.Selection> objetos e são ambos membros do <xref:Microsoft.Office.Interop.Word.Application> objeto, mas o <xref:Microsoft.Office.Interop.Word.Document> objeto também é um membro do <xref:Microsoft.Office.Interop.Word.Selection> objeto. Os <xref:Microsoft.Office.Interop.Word.Document> objetos e <xref:Microsoft.Office.Interop.Word.Selection> contêm <xref:Microsoft.Office.Interop.Word.Bookmark> e <xref:Microsoft.Office.Interop.Word.Range> objetos. A sobreposição existe porque há várias maneiras pelas quais você pode acessar o mesmo tipo de objeto. Por exemplo, você aplica a formatação a um <xref:Microsoft.Office.Interop.Word.Range> objeto, mas talvez queira acessar o intervalo da seleção atual, de um parágrafo específico, de uma seção ou de todo o documento.

 As seções a seguir descrevem brevemente os objetos de nível superior e como eles interagem entre si. Esses objetos incluem os seguintes cinco:

- Objeto de aplicativo

- Objeto Document

- Objeto de seleção

- Objeto de intervalo

- Objeto de indicador

  Além do modelo de objeto do Word, os projetos do Office no Visual Studio fornecem *itens de host* e *controles de host* que estendem alguns objetos no modelo de objeto do Word. Os itens de host e os controles de host se comportam como os objetos do Word que eles estendem, mas também têm funcionalidade adicional, como recursos de ligação de dados e eventos extras. Para obter mais informações, consulte Visão geral de [automação do Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md) e [itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md).

### <a name="application-object"></a>Objeto de aplicativo
 O <xref:Microsoft.Office.Interop.Word.Application> objeto representa o aplicativo do Word e é o pai de todos os outros objetos. Seus membros geralmente se aplicam ao Word como um todo. Você pode usar suas propriedades e métodos para controlar o ambiente do Word.

 Em projetos de suplemento do VSTO, você pode acessar o <xref:Microsoft.Office.Interop.Word.Application> objeto usando o `Application` campo da `ThisAddIn` classe. Para obter mais informações, consulte [programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md).

 Em projetos de nível de documento, você pode acessar o <xref:Microsoft.Office.Interop.Word.Application> objeto usando a <xref:Microsoft.Office.Tools.Word.Document.Application%2A> propriedade da `ThisDocument` classe.

### <a name="document-object"></a>Objeto Document
 O <xref:Microsoft.Office.Interop.Word.Document> objeto é central para programar o Word. Ele representa um documento e todo o seu conteúdo. Quando você abre um documento ou cria um novo documento, cria um novo <xref:Microsoft.Office.Interop.Word.Document> objeto, que é adicionado à <xref:Microsoft.Office.Interop.Word.Documents> coleção do <xref:Microsoft.Office.Interop.Word.Application> objeto. O documento que tem o foco é chamado de documento ativo. Ele é representado pela <xref:Microsoft.Office.Interop.Word._Application.ActiveDocument%2A> Propriedade do <xref:Microsoft.Office.Interop.Word.Application> objeto.

 As ferramentas de desenvolvimento do Office no Visual Studio estendem o <xref:Microsoft.Office.Interop.Word.Document> objeto fornecendo o <xref:Microsoft.Office.Tools.Word.Document> tipo. Esse tipo é um *item de host* que fornece acesso a todos os recursos de um <xref:Microsoft.Office.Interop.Word.Document> objeto e adiciona eventos adicionais e a capacidade de adicionar controles gerenciados.

 Ao criar um projeto de nível de documento, você pode acessar <xref:Microsoft.Office.Tools.Word.Document> os membros usando a `ThisDocument` classe gerada em seu projeto. Você pode acessar os membros do <xref:Microsoft.Office.Tools.Word.Document> item de host usando o **me** ou **essas** palavras-chave do código na `ThisDocument` classe ou usando o `Globals.ThisDocument` código de fora da `ThisDocument` classe. Para obter mais informações, consulte [programar personalizações em nível de documento](../vsto/programming-document-level-customizations.md). Por exemplo, para selecionar o primeiro parágrafo no documento, use o código a seguir.

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet120":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet120":::

 Em projetos de suplemento do VSTO, você pode gerar <xref:Microsoft.Office.Tools.Word.Document> itens de host em tempo de execução. Você pode usar o item de host gerado para adicionar controles ao documento associado. Para obter mais informações, consulte [estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

### <a name="selection-object"></a>Objeto de seleção
 O <xref:Microsoft.Office.Interop.Word.Selection> objeto representa a área selecionada no momento. Quando você executa uma operação na interface do usuário do Word, como texto em negrito, seleciona ou realça o texto e, em seguida, aplica a formatação. O <xref:Microsoft.Office.Interop.Word.Selection> objeto está sempre presente em um documento. Se nada estiver selecionado, ele representará o ponto de inserção. Além disso, uma seleção pode abranger vários blocos de texto que não são contíguos.

### <a name="range-object"></a>Objeto de intervalo
 O <xref:Microsoft.Office.Interop.Word.Range> objeto representa uma área contígua em um documento e é definido por uma posição de caractere inicial e uma posição de caractere final. Você não está limitado a um único <xref:Microsoft.Office.Interop.Word.Range> objeto. Você pode definir vários <xref:Microsoft.Office.Interop.Word.Range> objetos no mesmo documento. Um <xref:Microsoft.Office.Interop.Word.Range> objeto tem as seguintes características:

- Ele pode consistir apenas no ponto de inserção, em um intervalo de texto ou no documento inteiro.

- Ele inclui caracteres não imprimíveis, como espaços, caracteres de tabulação e marcas de parágrafo.

- Pode ser a área representada pela seleção atual ou pode representar uma área diferente da seleção atual.

- Ele não é visível em um documento, ao contrário de uma seleção, que está sempre visível.

- Ele não é salvo com um documento e existe somente enquanto o código está em execução.

  Quando você insere texto no final de um intervalo, o Word expande automaticamente o intervalo para incluir o texto inserido.

### <a name="content-control-objects"></a>Objetos de controle de conteúdo
 Um <xref:Microsoft.Office.Interop.Word.ContentControl> fornece uma maneira de controlar a entrada e a apresentação de texto e outros tipos de conteúdo em documentos do Word. Um <xref:Microsoft.Office.Interop.Word.ContentControl> pode exibir vários tipos diferentes de interface do usuário que são otimizados para uso em documentos do Word, como um controle de texto rico, um seletor de data ou uma caixa de combinação. Você também pode usar um <xref:Microsoft.Office.Interop.Word.ContentControl> para impedir que os usuários editem seções do documento ou modelo.

 O Visual Studio estende o <xref:Microsoft.Office.Interop.Word.ContentControl> objeto em vários controles de host diferentes. Enquanto o <xref:Microsoft.Office.Interop.Word.ContentControl> objeto pode exibir qualquer um dos diferentes tipos de interface do usuário que estão disponíveis para controles de conteúdo, o Visual Studio fornece um tipo diferente para cada controle de conteúdo. Por exemplo, você pode usar um <xref:Microsoft.Office.Tools.Word.RichTextContentControl> para criar um controle de Rich Text ou pode usar um <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> para criar um seletor de data. Esses controles de host se comportam como o nativo <xref:Microsoft.Office.Interop.Word.ContentControl> , mas têm eventos adicionais e recursos de associação de dados. Para obter mais informações, consulte [controles de conteúdo](../vsto/content-controls.md).

### <a name="bookmark-object"></a>Objeto de indicador
 O <xref:Microsoft.Office.Interop.Word.Bookmark> objeto representa uma área contígua em um documento, com uma posição inicial e uma posição final. Você pode usar indicadores para marcar um local em um documento ou como um contêiner para texto em um documento. Um <xref:Microsoft.Office.Interop.Word.Bookmark> objeto pode consistir no ponto de inserção ou ser tão grande quanto o documento inteiro. Um <xref:Microsoft.Office.Interop.Word.Bookmark> tem as seguintes características que a configuram de fora do <xref:Microsoft.Office.Interop.Word.Range> objeto:

- Você pode nomear o indicador em tempo de design.

- <xref:Microsoft.Office.Interop.Word.Bookmark> os objetos são salvos com o documento e, portanto, não são excluídos quando o código para de ser executado ou o documento é fechado.

- Os indicadores podem ser ocultados ou tornar-se visíveis definindo a <xref:Microsoft.Office.Interop.Word.View.ShowBookmarks%2A> Propriedade do <xref:Microsoft.Office.Interop.Word.View> objeto como **false** ou **true**.

  O Visual Studio estende o <xref:Microsoft.Office.Interop.Word.Bookmark> objeto fornecendo o <xref:Microsoft.Office.Tools.Word.Bookmark> controle de host. O <xref:Microsoft.Office.Tools.Word.Bookmark> controle de host se comporta como um nativo <xref:Microsoft.Office.Interop.Word.Bookmark> , mas tem eventos adicionais e recursos de associação de dados. Você pode associar dados a um controle de indicador em um documento da mesma maneira que associa dados a um controle de caixa de texto em um formulário do Windows. Para obter mais informações, consulte [controle de indicadores](../vsto/bookmark-control.md).

## <a name="use-the-word-object-model-documentation"></a><a name="WordOMDocumentation"></a> Usar a documentação do modelo de objeto do Word
 Para obter informações completas sobre o modelo de objeto do Word, você pode consultar a referência do assembly de interoperabilidade primária (PIA) do Word e a referência do modelo de objeto do Visual Basic for Applications (VBA).

### <a name="primary-interop-assembly-reference"></a>Referência de assembly de interoperabilidade primária
 A documentação de referência do PIA do Word descreve os tipos no assembly de interoperabilidade primária para o Word. Esta documentação está disponível no seguinte local: [referência de assembly de interoperabilidade primária do Word 2010](../vsto/office-primary-interop-assemblies.md).

 Para obter mais informações sobre o design do PIA do Word, como as diferenças entre classes e interfaces no PIA e como os eventos no PIA são implementados, consulte [visão geral de classes e interfaces nos assemblies de interoperabilidade primária do Office](/previous-versions/office/office-12/ms247299(v=office.12)).

### <a name="vba-object-model-reference"></a>Referência de modelo de objeto VBA
 A referência do modelo de objeto do VBA documenta o modelo de objeto do Word conforme ele é exposto ao código do VBA. Para obter mais informações, consulte [referência de modelo de objeto do Word 2010](/office/vba/api/overview/Word/object-model).

 Todos os objetos e membros na referência do modelo de objeto do VBA correspondem a tipos e membros no PIA do Word. Por exemplo, o objeto Document na referência do modelo de objeto do VBA corresponde ao <xref:Microsoft.Office.Interop.Word.Document> objeto no pia do Word. Embora a referência de modelo de objeto do VBA Forneça exemplos de código para a maioria das propriedades, métodos e eventos, você deve converter o código VBA nesta referência para Visual Basic ou Visual C# se quiser usá-los em um projeto do Word criado usando o Visual Studio.

## <a name="see-also"></a>Consulte também
- [Assemblies de interoperabilidade primária do Office](../vsto/office-primary-interop-assemblies.md)
- [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)
- [Trabalhar com documentos](../vsto/working-with-documents.md)
- [Trabalhar com texto em documentos](../vsto/working-with-text-in-documents.md)
- [Trabalhar com tabelas](../vsto/working-with-tables.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
