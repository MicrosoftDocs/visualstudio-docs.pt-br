---
title: Visão geral dos controles de host e de itens de host
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- host controls [Office development in Visual Studio], adding
- Office documents [Office development in Visual Studio, host controls
- host items [Office development in Visual Studio]
- application development [Office development in Visual Studio], host items
- Office applications [Office development in Visual Studio], host items
- host controls [Office development in Visual Studio], listed
- Excel [Office development in Visual Studio], host items
- host controls [Office Development in Visual Stuio], naming
- host controls [Office development in Visual Studio]
- host controls [Office development in Visual Studio], about host controls
- document-level customizations [Office development in Visual Studio], host controls
- Office applications [Office development in Visual Studio], host controls
- documents [Office development in Visual Studio], host controls
- controls [Office development in Visual Studio], host controls
- application development [Office development in Visual Studio], host controls
- Excel [Office development in Visual Studio], host controls
- host items [Office development in Visual Studio], about host items
- host items [Office development in Visual Studio], listed
- documents [Office development in Visual Studio], host items
- data binding [Office development in Visual Studio], host controls
- Office documents [Office development in Visual Studio, host items
- Word [Office development in Visual Studio], host items
- document-level customizations [Office development in Visual Studio], host items
- Word [Office development in Visual Studio], host controls
- host controls [Office development in Visual Studio], deleting
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 48ce311a767d68ce1402961d2ddf4cf8b673637c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49937493"
---
# <a name="host-items-and-host-controls-overview"></a>Visão geral dos controles de host e de itens de host
  Itens de host e controles de host são tipos que ajudam a fornecer o modelo de programação para soluções do Office que são criadas usando as ferramentas de desenvolvimento do Office no Visual Studio. Itens de host e controles de host fazem da interação com os modelos de objeto do Microsoft Office Word e Microsoft Office Excel, que são baseados em COM, mais como interagir com os objetos gerenciados, como controles de formulários do Windows.  
  
 [!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]  
  
## <a name="host-items"></a>Itens de host  
 Itens de host são tipos que estão na parte superior de hierarquias de modelo de objeto em projetos do Office. O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] define os seguintes itens de host para soluções do Word e Excel:  
  
- <xref:Microsoft.Office.Tools.Word.Document>  
  
- <xref:Microsoft.Office.Tools.Excel.Workbook>  
  
- <xref:Microsoft.Office.Tools.Excel.Worksheet>  
  
- <xref:Microsoft.Office.Tools.Excel.ChartSheet>  
  
  Cada um desses tipos estende um objeto que existe nativamente no modelo de objeto do Word ou Excel, chamado de um *objeto nativo do Office*. Por exemplo, o <xref:Microsoft.Office.Tools.Word.Document> estende o item de host a <xref:Microsoft.Office.Interop.Word.Document> objeto, que é definido no assembly de interoperabilidade primário para o Word.  
  
  Itens de host geralmente têm a mesma funcionalidade de base como objetos do Office correspondentes, mas são aprimorados com os seguintes recursos:  
  
- A capacidade de hospedar controles gerenciados, incluindo controles de host e controles de formulários do Windows.  
  
- Modelos de evento mais avançados. Alguns eventos de documento, a pasta de trabalho e a planilha em que os modelos de objeto do Word e Excel nativos são acionados apenas no nível do aplicativo. Itens de host fornecem esses eventos no nível do documento, para que ele seja mais fácil de manipular os eventos para um documento específico.  
  
### <a name="understand-host-items-in-document-level-projects"></a>Entender os itens de host nos projetos em nível de documento  
 Em projetos de nível de documento, itens de host fornecem um ponto de entrada para seu código e têm designers que ajudam a desenvolver sua solução.  
  
 O <xref:Microsoft.Office.Tools.Word.Document> e <xref:Microsoft.Office.Tools.Excel.Worksheet> itens de host associou designers que são a representação visual do documento ou planilha, como um designer de formulários do Windows. Você pode usar esse designer para modificar o conteúdo do documento ou planilha diretamente no Word ou Excel e arrastar os controles na superfície de design. Para obter mais informações, consulte [item de host do documento](../vsto/document-host-item.md) e [item de host da planilha](../vsto/worksheet-host-item.md).  
  
 O <xref:Microsoft.Office.Tools.Excel.Workbook> item de host não age como um contêiner para controles que têm uma interface do usuário. Em vez disso, o designer para este item de host de funções como uma bandeja de componentes, que permite que você arrasta um componente, como um <xref:System.Data.DataSet>, para sua superfície de design. Para obter mais informações, consulte [item de host da pasta de trabalho](../vsto/workbook-host-item.md).  
  
 Não não possível criar itens de host por meio de programação em projetos de nível de documento. Em vez disso, use o `ThisDocument`, `ThisWorkbook`, ou `Sheet` *n* classes que gera automaticamente em seu projeto do Visual Studio em tempo de design. Essas classes geradas derivam os itens de host e eles fornecem um ponto de entrada para seu código. Para obter mais informações, consulte [limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md).  
  
### <a name="understand-host-items-in-vsto-add-in-projects"></a>Entender os itens de host em projetos de suplemento do VSTO  
 Quando você cria um suplemento do VSTO, você não tem acesso a qualquer item de host por padrão. No entanto, você pode gerar <xref:Microsoft.Office.Tools.Word.Document>, <xref:Microsoft.Office.Tools.Excel.Workbook>, e <xref:Microsoft.Office.Tools.Excel.Worksheet> hospedar itens no Word e suplementos do VSTO do Excel em tempo de execução.  
  
 Depois de gerar um item de host, você pode executar tarefas como adicionar controles a documentos. Para obter mais informações, consulte [documentos de estender o Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
## <a name="host-controls"></a>Controles de host  
 Controles de host estendem a vários objetos de (UI) de interface do usuário em modelos de objeto do Word e Excel, como `Microsoft.Office.Interop.Word.ContentControl` e <xref:Microsoft.Office.Interop.Excel.Range> objetos.  
  
 Os seguintes controles de host estão disponíveis para projetos do Excel:  
  
- [Controle de gráfico](../vsto/chart-control.md)  
  
- [Controle ListObject](../vsto/listobject-control.md)  
  
- [Controle NamedRange](../vsto/namedrange-control.md)  
  
- [Controle XmlMappedRange](../vsto/xmlmappedrange-control.md)  
  
  Os seguintes controles de host estão disponíveis para projetos do Word:  
  
- [Controle de indicador](../vsto/bookmark-control.md)  
  
- [Controles de conteúdo](../vsto/content-controls.md)  
  
- [Controle XMLNode](../vsto/xmlnode-control.md)  
  
- [Controle XMLNodes](../vsto/xmlnodes-control.md)  
  
  Controles de host que são adicionados aos documentos do Office se comportam como os objetos nativos do Office; No entanto, os controles de host têm funcionalidades adicionais, incluindo os eventos e recursos de ligação de dados. Por exemplo, quando você deseja capturar os eventos de um nativo <xref:Microsoft.Office.Interop.Excel.Range> do objeto no Excel, primeiro você deve tratar o evento de alteração da planilha. Em seguida, você deve determinar se a alteração ocorreu dentro do <xref:Microsoft.Office.Interop.Excel.Range>. Em contraste, o <xref:Microsoft.Office.Tools.Excel.NamedRange> controle de host tem um <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> eventos que você pode manipular diretamente.  
  
  A relação entre um item de host e controles de host é semelhante à relação entre os controles de formulário do Windows e Windows Forms. Assim como você colocaria um controle de caixa de texto em um formulário do Windows, você coloca um <xref:Microsoft.Office.Tools.Excel.NamedRange> control em um <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host. A ilustração a seguir mostra a relação entre itens de host e controles de host.  
  
  ![Relação entre itens de host e controles de host](../vsto/media/hostitemscontrols.png "relação entre itens de host e controles de host")  
  
  Você também pode usar controles de formulários do Windows em suas soluções Office adicionando-os diretamente para a superfície de documento do Word e Excel. Para obter mais informações, consulte [controles de formulários do Windows de visão geral de documentos do Office](../vsto/windows-forms-controls-on-office-documents-overview.md).  
  
> [!NOTE]  
>  Não há suporte para a adição de controles de host ou controles dos Windows Forms a um subdocumento de palavra.  
  
### <a name="add-host-controls-to-your-documents"></a>Adicionar controles de host para seus documentos  
 Em projetos de nível de documento, você pode adicionar controles de host para seus documentos do Word ou planilhas do Excel em tempo de design das seguintes maneiras:  
  
- Adicionar controles de host para o documento em tempo de design da mesma maneira, você adicionaria um objeto nativo.  
  
- Arraste os controles de host dos **caixa de ferramentas** em seus documentos e planilhas. Controles de host do Excel estão disponíveis na **controles do Excel** guia em projetos do Excel e os controles estão disponíveis no host do Word a **controles do Word** guia em projetos do Word.  
  
- Arraste os controles de host dos **fontes de dados** janela para os seus documentos e planilhas. Isso permite que você adicionar controles que já estão associados a dados. Para obter mais informações, consulte [ligar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md).  
  
  No nível de documento e projetos de suplemento do VSTO, você também pode adicionar alguns controles de host para documentos em tempo de execução. Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
  Para obter mais informações sobre como adicionar controles de host a documentos, consulte os tópicos a seguir:  
  
- [Como: adicionar controles Chart a planilhas](../vsto/how-to-add-chart-controls-to-worksheets.md)  
  
- [Como: adicionar controles ListObject a planilhas](../vsto/how-to-add-listobject-controls-to-worksheets.md)  
  
- [Como: adicionar controles NamedRange a planilhas](../vsto/how-to-add-namedrange-controls-to-worksheets.md)  
  
- [Como: adicionar controles XMLMappedRange a planilhas](../vsto/how-to-add-xmlmappedrange-controls-to-worksheets.md)  
  
- [Como: adicionar controles de indicador a documentos do Word](../vsto/how-to-add-bookmark-controls-to-word-documents.md)  
  
- [Como: adicionar conteúdo controles a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md)  
  
- [Como: adicionar controles XMLNode a documentos do Word](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)  
  
- [Como: adicionar controles XMLNodes a documentos do Word](../vsto/how-to-add-xmlnodes-controls-to-word-documents.md)  
  
### <a name="name-host-controls"></a>Controles de host do nome  
 Quando você arrasta um controle de host do **caixa de ferramentas** ao seu documento, o controle automaticamente é chamado usando o tipo de controle com um número incremental no final. Por exemplo, os indicadores são nomeados **bookmark1**, **bookmark2**e assim por diante. Se você usar a funcionalidade nativa do Word ou Excel para adicionar o controle, você pode atribuir um nome específico no momento em que você criá-lo. Você também pode renomear os controles, alterando o valor da **nome** propriedade no **propriedades** janela.  
  
> [!NOTE]  
>  É possível usar palavras reservadas para nomear os controles de host. Por exemplo, se você adicionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> o controle para uma planilha e altere o nome para **sistema**, erros ocorrem quando você compila o projeto.  
  
### <a name="delete-host-controls"></a>Excluir os controles de host  
 Em projetos de nível de documento, você pode excluir os controles de host em tempo de design, selecionando o controle no documento do Word ou planilha do Excel e pressionando a **excluir** chave. No entanto, você deve usar o **definir nome** caixa de diálogo no Excel para excluir <xref:Microsoft.Office.Tools.Excel.NamedRange> controles.  
  
 Se você adicionar um controle de host para um documento em tempo de design, você não deve removê-lo por meio de programação em tempo de execução porque na próxima vez que tentar usar o controle no código, uma exceção será lançada. O `Delete` método de um controle de host remove somente os controles de host que são adicionados ao documento em tempo de execução. Se você chamar o `Delete` método de um controle de host que foi criado em tempo de design, uma exceção será lançada.  
  
 Por exemplo, o <xref:Microsoft.Office.Tools.Excel.NamedRange.Delete%2A> método de um <xref:Microsoft.Office.Tools.Excel.NamedRange> exclui somente com êxito o <xref:Microsoft.Office.Tools.Excel.NamedRange> se ele foi adicionado por meio de programação a planilha, que é conhecido como criar controles de host dinamicamente. Controles de host criado dinamicamente também podem ser removidos, passando o nome do controle para o `Remove` método da <xref:Microsoft.Office.Tools.Excel.Worksheet.Controls%2A> ou <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> propriedade. Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
 Se os usuários finais excluir um controle de host do documento em tempo de execução, a solução poderá falhar de maneiras inesperadas. Você pode usar os recursos de proteção de documento no Word e Excel para proteger os controles de host sejam excluídas. Para obter mais informações, consulte [exemplos de desenvolvimento do Office e instruções passo a passo](../vsto/office-development-samples-and-walkthroughs.md).  
  
> [!NOTE]  
>  Não remover programaticamente os controles durante o `Shutdown` manipulador de eventos do documento ou planilha. Os elementos de interface do usuário não estão mais disponíveis quando o `Shutdown` evento ocorre. Se você quiser remover os controles antes de fecha o aplicativo, adicione seu código para outro manipulador de eventos, como `BeforeClose` ou `BeforeSave`.  
  
### <a name="program-against-host-control-events"></a>Programe em eventos de controle de host  
 Uma maneira que os controles de host estendem objetos do Office é com a adição de eventos. Por exemplo, o <xref:Microsoft.Office.Interop.Excel.Range> objeto no Excel e <xref:Microsoft.Office.Interop.Word.Bookmark> objeto no Word não tem eventos, mas o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] estende esses objetos, adicionando eventos programáveis. Você pode acessar e codificar esses eventos, a mesma maneira como você acessa os eventos de controles nos Windows Forms: por meio da lista suspensa de evento no Visual Basic e a página de propriedades de evento em c#. Para obter mais informações, consulte [instruções passo a passo: programa contra eventos de um controle NamedRange](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md).  
  
> [!NOTE]  
>  Você não deve definir a <xref:Microsoft.Office.Interop.Excel._Application.EnableEvents%2A> propriedade do <xref:Microsoft.Office.Interop.Excel.Application> objeto no Excel para **falso**. Definir essa propriedade como **falsos** impede que o Excel da geração de todos os eventos, incluindo os eventos de controles de host.  
  
## <a name="see-also"></a>Consulte também  
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Personalizações em nível de documento do programa](../vsto/programming-document-level-customizations.md)   
 [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)   
 [Controles em documentos do Office](../vsto/controls-on-office-documents.md)   
 [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)  
  