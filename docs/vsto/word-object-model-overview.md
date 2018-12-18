---
title: Visão geral do modelo de objeto do Word
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 75a5f8e79bbd6dd34b046cbff6d59844a977efb3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49878005"
---
# <a name="word-object-model-overview"></a>Visão geral do modelo de objeto do Word
  Ao desenvolver soluções do Word no Visual Studio, você interage com o modelo de objeto do Word. Esse modelo de objeto consiste em classes e interfaces que são fornecidos no assembly de interoperabilidade primário para o Word e são definidos na <xref:Microsoft.Office.Interop.Word> namespace.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 Este tópico fornece uma visão geral do modelo de objeto do Word. Para obter recursos onde você pode aprender mais sobre todo o modelo de objeto do Word, consulte [Use a documentação do modelo de objeto Word](#WordOMDocumentation).  
  
 Para obter informações sobre como usar o modelo de objeto do Word para executar tarefas específicas, consulte os tópicos a seguir:  
  
-   [Trabalhar com documentos](../vsto/working-with-documents.md)  
  
-   [Trabalhar com texto em documentos](../vsto/working-with-text-in-documents.md)  
  
-   [Trabalhar com tabelas](../vsto/working-with-tables.md)  
  
##  <a name="understanding"></a> Entender o modelo de objeto do Word  
 O Word fornece centenas de objetos com os quais você pode interagir. Esses objetos são organizados em uma hierarquia que segue rigorosamente a interface do usuário. Na parte superior da hierarquia é o <xref:Microsoft.Office.Interop.Word.Application> objeto. Este objeto representa a instância atual do Word. O <xref:Microsoft.Office.Interop.Word.Application> objeto contém o <xref:Microsoft.Office.Interop.Word.Document>, <xref:Microsoft.Office.Interop.Word.Selection>, <xref:Microsoft.Office.Interop.Word.Bookmark>, e <xref:Microsoft.Office.Interop.Word.Range> objetos. Cada um desses objetos tem vários métodos e propriedades que você pode acessar para manipular e interagir com o objeto.  
  
 A ilustração a seguir mostra uma exibição desses objetos na hierarquia de modelo de objeto do Word.  
  
 ![Gráfico de modelo de objeto do Word](../vsto/media/wrwordobjectmodel.gif "gráfico do modelo de objeto do Word")  
  
 À primeira vista, os objetos aparecem se sobreponham. Por exemplo, o <xref:Microsoft.Office.Interop.Word.Document> e <xref:Microsoft.Office.Interop.Word.Selection> objetos são os dois membros da <xref:Microsoft.Office.Interop.Word.Application> objeto, mas o <xref:Microsoft.Office.Interop.Word.Document> objeto também é um membro do <xref:Microsoft.Office.Interop.Word.Selection> objeto. Tanto a <xref:Microsoft.Office.Interop.Word.Document> e <xref:Microsoft.Office.Interop.Word.Selection> objetos contêm <xref:Microsoft.Office.Interop.Word.Bookmark> e <xref:Microsoft.Office.Interop.Word.Range> objetos. A sobreposição existe porque há várias maneiras que você pode acessar o mesmo tipo de objeto. Por exemplo, aplicar formatação a uma <xref:Microsoft.Office.Interop.Word.Range> objeto; mas você talvez queira acessar o intervalo da seleção atual, de um determinado parágrafo, de uma seção ou de todo o documento.  
  
 As seções a seguir descrevem brevemente os objetos de nível superior e como eles interagem entre si. Esses objetos incluem os cinco seguintes:  
  
- Objeto de aplicativo  
  
- Objeto de documento  
  
- Objeto Selection  
  
- Objeto de intervalo  
  
- Objeto de indicador  
  
  Além do modelo de objeto do Word, os projetos do Office no Visual Studio fornecem *hospedar itens* e *hospedar controles* que estendem alguns objetos no modelo de objeto do Word. Itens de host e controles de host se comportam como eles estendem os objetos do Word, mas eles também têm funcionalidade adicional, como recursos de vinculação de dados e eventos adicionais. Para obter mais informações, consulte [automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md) e [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md).  
  
### <a name="application-object"></a>Objeto de aplicativo  
 O <xref:Microsoft.Office.Interop.Word.Application> objeto representa o aplicativo Word e é o pai de todos os outros objetos. Seus membros geralmente se aplicam ao Word como um todo. Você pode usar suas propriedades e métodos para controlar o ambiente do Word.  
  
 Em projetos de suplemento do VSTO, você pode acessar o <xref:Microsoft.Office.Interop.Word.Application> objeto usando o `Application` campo do `ThisAddIn` classe. Para obter mais informações, consulte [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md).  
  
 Em projetos de nível de documento, você pode acessar o <xref:Microsoft.Office.Interop.Word.Application> objeto usando o <xref:Microsoft.Office.Tools.Word.Document.Application%2A> propriedade do `ThisDocument` classe.  
  
### <a name="document-object"></a>Objeto de documento  
 O <xref:Microsoft.Office.Interop.Word.Document> objeto é fundamental para programação do Word. Representa um documento e todo seu conteúdo. Quando você abre um documento ou cria um novo documento, você cria um novo <xref:Microsoft.Office.Interop.Word.Document> objeto, que é adicionado para o <xref:Microsoft.Office.Interop.Word.Documents> coleção do <xref:Microsoft.Office.Interop.Word.Application> objeto. O documento que tem o foco é chamado o documento ativo. Ele é representado pela <xref:Microsoft.Office.Interop.Word._Application.ActiveDocument%2A> propriedade do <xref:Microsoft.Office.Interop.Word.Application> objeto.  
  
 As ferramentas de desenvolvimento do Office no Visual Studio estendem o <xref:Microsoft.Office.Interop.Word.Document> objeto, fornecendo o <xref:Microsoft.Office.Tools.Word.Document> tipo. Esse tipo é um *item de host* que fornece acesso a todos os recursos de um <xref:Microsoft.Office.Interop.Word.Document> de objeto e adiciona eventos adicionais e a capacidade de adicionar controles gerenciados.  
  
 Quando você cria um projeto de nível de documento, você pode acessar <xref:Microsoft.Office.Tools.Word.Document> membros usando gerado `ThisDocument` classe em seu projeto. Você pode acessar membros do <xref:Microsoft.Office.Tools.Word.Document> item de host usando o **Me** ou **isso** palavras-chave a partir do código no `ThisDocument` classe, ou usando `Globals.ThisDocument` do código fora o `ThisDocument` classe. Para obter mais informações, consulte [personalizações no nível de documento do programa](../vsto/programming-document-level-customizations.md). Por exemplo, para selecionar o primeiro parágrafo no documento, use o código a seguir.  
  
 [!code-vb[Trin_VstcoreWordAutomation#120](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#120)]
 [!code-csharp[Trin_VstcoreWordAutomation#120](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#120)]  
  
 Em projetos de suplemento do VSTO, você pode gerar <xref:Microsoft.Office.Tools.Word.Document> hospedar itens em tempo de execução. Você pode usar o item de host gerados para adicionar controles para o documento associado. Para obter mais informações, consulte [documentos de estender o Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
### <a name="selection-object"></a>Objeto Selection  
 O <xref:Microsoft.Office.Interop.Word.Selection> objeto representa a área que está selecionada no momento. Quando você executa uma operação na interface do usuário de palavra, como texto em negrito, selecione, ou realce o texto e, em seguida, aplicar a formatação. O <xref:Microsoft.Office.Interop.Word.Selection> objeto está sempre presente em um documento. Se nada estiver selecionado, ele representa o ponto de inserção. Além disso, uma seleção pode abranger vários blocos de texto que não são contíguos.  
  
### <a name="range-object"></a>Objeto de intervalo  
 O <xref:Microsoft.Office.Interop.Word.Range> objeto representa uma área contígua em um documento e é definido por uma posição de caractere inicial e uma posição do caractere final. Você não está limitado a um único <xref:Microsoft.Office.Interop.Word.Range> objeto. É possível definir diversos <xref:Microsoft.Office.Interop.Word.Range> objetos no mesmo documento. Um <xref:Microsoft.Office.Interop.Word.Range> objeto tem as seguintes características:  
  
- Ele pode consistir de apenas o ponto de inserção, um intervalo de texto ou o documento inteiro.  
  
- Ele inclui caracteres não imprimíveis como espaços, caracteres de tabulação e marcas de parágrafo.  
  
- É a área representada pela seleção atual ou pode representar uma área diferente da seleção atual.  
  
- Não é visível em um documento, ao contrário de uma seleção, que está sempre visível.  
  
- Ele não será salvo com um documento e existe somente enquanto o código está em execução.  
  
  Quando você insere o texto no final de um intervalo, o Word automaticamente expande o intervalo para incluir o texto inserido.  
  
### <a name="content-control-objects"></a>Objetos de controle de conteúdo  
 Um <xref:Microsoft.Office.Interop.Word.ContentControl> fornece uma maneira de controlar a entrada e a apresentação de texto e outros tipos de conteúdo em documentos do Word. Um <xref:Microsoft.Office.Interop.Word.ContentControl> pode exibir vários tipos diferentes de interface do usuário que são otimizados para uso em documentos do Word, como um controle rich text, um seletor de data ou uma caixa de combinação. Você também pode usar um <xref:Microsoft.Office.Interop.Word.ContentControl> para impedir que usuários editem seções do documento ou modelo.  
  
 O Visual Studio estende o <xref:Microsoft.Office.Interop.Word.ContentControl> objeto em vários controles de host diferente. Enquanto o <xref:Microsoft.Office.Interop.Word.ContentControl> objeto pode exibir qualquer um dos diferentes tipos de interface do usuário que estão disponíveis para controles de conteúdo, o Visual Studio fornece um tipo diferente para cada controle de conteúdo. Por exemplo, você pode usar um <xref:Microsoft.Office.Tools.Word.RichTextContentControl> criar um controle rich text, ou você pode usar um <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> para criar um seletor de data. Esses controles de host se comportam como nativo <xref:Microsoft.Office.Interop.Word.ContentControl>, mas têm eventos adicionais e recursos de ligação de dados. Para obter mais informações, consulte [controles de conteúdo](../vsto/content-controls.md).  
  
### <a name="bookmark-object"></a>Objeto de indicador  
 O <xref:Microsoft.Office.Interop.Word.Bookmark> objeto representa uma área contígua em um documento, com uma posição inicial e uma posição final. Você pode usar indicadores para marcar um local em um documento, ou como um contêiner para texto em um documento. Um <xref:Microsoft.Office.Interop.Word.Bookmark> objeto pode conter o ponto de inserção ou ser tão grande quanto o documento inteiro. Um <xref:Microsoft.Office.Interop.Word.Bookmark> tem as seguintes características que defini-lo, além do <xref:Microsoft.Office.Interop.Word.Range> objeto:  
  
- Você pode nomear o indicador em tempo de design.  
  
- <xref:Microsoft.Office.Interop.Word.Bookmark> objetos são salvos com o documento e, portanto, não são excluídos quando o código será interrompido ou o documento é fechado.  
  
- Indicadores podem ser ocultos ou ficam visíveis definindo a <xref:Microsoft.Office.Interop.Word.View.ShowBookmarks%2A> propriedade do <xref:Microsoft.Office.Interop.Word.View> do objeto para **false** ou **true**.  
  
  Visual Studio estende o <xref:Microsoft.Office.Interop.Word.Bookmark> objeto, fornecendo o <xref:Microsoft.Office.Tools.Word.Bookmark> controle de host. O <xref:Microsoft.Office.Tools.Word.Bookmark> controle de host se comporta como um nativo <xref:Microsoft.Office.Interop.Word.Bookmark>, mas tem eventos adicionais e recursos de vinculação de dados. Você pode associar dados a um controle de indicador em um documento da mesma forma que você associe dados a um controle de caixa de texto em um formulário do Windows. Para obter mais informações, consulte [controle de indicador](../vsto/bookmark-control.md).  
  
##  <a name="WordOMDocumentation"></a> Use a documentação de modelo de objeto do Word  
 Para obter informações completas sobre o modelo de objeto do Word, você pode consultar a referência de assembly de interoperabilidade primária (PIA) do Word e do Visual Basic para referência de modelo de objeto Applications (VBA).  
  
### <a name="primary-interop-assembly-reference"></a>Referência de assembly de interoperabilidade primário  
 A documentação de referência de PIA Word descreve os tipos no assembly de interoperabilidade primário para o Word. Esta documentação está disponível no seguinte local: [referência de assembly de interoperabilidade primária do Word 2010](http://go.microsoft.com/fwlink/?LinkId=189588).  
  
 Para obter mais informações sobre o design de PIA o Word, como as diferenças entre classes e interfaces no PIA e como os eventos no PIA são implementados, consulte [visão geral das classes e interfaces no Office assemblies de interoperabilidade primários](http://go.microsoft.com/fwlink/?LinkId=189592).  
  
### <a name="vba-object-model-reference"></a>Referência de modelo de objeto do VBA  
 A referência de modelo de objeto VBA documenta o modelo de objeto do Word, conforme ele é exposto ao código do VBA. Para obter mais informações, consulte [referência de modelo de objeto do Word 2010](http://go.microsoft.com/fwlink/?LinkId=199772).  
  
 Todos os objetos e membros na referência de modelo de objeto do VBA correspondem aos tipos e membros no PIA do Word. Por exemplo, o objeto de documento na referência de modelo de objeto do VBA corresponde à <xref:Microsoft.Office.Interop.Word.Document> objeto no PIA do Word. Embora a referência de modelo de objeto VBA fornece exemplos de código para a maioria das propriedades, métodos e eventos, você deve converter o código VBA essa referência para o Visual Basic ou Visual c# se você quiser usá-los em uma palavra de projeto que você cria usando o Visual Studio.  
  
## <a name="see-also"></a>Consulte também  
 [Assemblies de interoperabilidade primários do Office](../vsto/office-primary-interop-assemblies.md)   
 [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Trabalhar com documentos](../vsto/working-with-documents.md)   
 [Trabalhar com texto em documentos](../vsto/working-with-text-in-documents.md)   
 [Trabalhar com tabelas](../vsto/working-with-tables.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  