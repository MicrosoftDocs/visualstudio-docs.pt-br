---
title: Limitações programáticas de itens de host e controles de host
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, host controls
- application development [Office development in Visual Studio], host items
- Office applications [Office development in Visual Studio], host items
- host items [Office development in Visual Studio], programmatic limitations
- Excel [Office development in Visual Studio], host items
- host controls [Office development in Visual Studio], creating
- document-level customizations [Office development in Visual Studio], host controls
- Office applications [Office development in Visual Studio], host controls
- documents [Office development in Visual Studio], host controls
- controls [Office development in Visual Studio], host controls
- host controls [Office development in Visual Studio], passing to methods and properties
- application development [Office development in Visual Studio], host controls
- Excel [Office development in Visual Studio], host controls
- host controls [Office development in Visual Studio], programmatic limitations
- documents [Office development in Visual Studio], host items
- Office documents [Office development in Visual Studio, host items
- Word [Office development in Visual Studio], host items
- document-level customizations [Office development in Visual Studio], host items
- Word [Office development in Visual Studio], host controls
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 0b7e45ed9ba8e9fcd42d57a1cc6aaf34ce3e3711
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34693377"
---
# <a name="programmatic-limitations-of-host-items-and-host-controls"></a>Limitações programáticas de itens de host e controles de host
  Cada item de host e o controle de host foi projetado para se comportar como um correspondente nativo Microsoft Office Word ou o Microsoft Office Excel, com funcionalidade adicional. No entanto, há algumas diferenças fundamentais entre o comportamento de itens de host e controles de host e os objetos nativos do Office em tempo de execução.  
  
 Para obter informações gerais sobre itens de host e controles de host, consulte [itens de Host e visão geral dos controles de host](../vsto/host-items-and-host-controls-overview.md).  
  
 [!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]  
  
## <a name="programmatically-create-host-items"></a>Criar itens de host de forma programática  
 Quando você programaticamente cria ou abre um documento, a pasta de trabalho ou a planilha em tempo de execução usando o modelo de objeto do Word ou Excel, o item não é um item de host. Em vez disso, o novo objeto é um objeto nativo do Office. Por exemplo, se você usar o <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> método para criar um novo documento do Word em tempo de execução, ele será um nativo <xref:Microsoft.Office.Interop.Word.Document> objeto em vez de <xref:Microsoft.Office.Tools.Word.Document> item de host. Da mesma forma, quando você cria uma nova planilha em tempo de execução usando o <xref:Microsoft.Office.Interop.Excel.Worksheets.Add%2A> método, você obtém um nativo <xref:Microsoft.Office.Interop.Excel.Worksheet> objeto em vez de <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host.  
  
 Em projetos de nível de documento, você não pode criar itens de host em tempo de execução. Itens de host podem ser criados apenas em tempo de design em projetos de nível de documento. Para obter mais informações, consulte [item de host do documento](../vsto/document-host-item.md), [item de host de pasta de trabalho](../vsto/workbook-host-item.md), e [item de host de planilha](../vsto/worksheet-host-item.md).  
  
 Em projetos de suplemento do VSTO, você pode criar <xref:Microsoft.Office.Tools.Word.Document>, <xref:Microsoft.Office.Tools.Excel.Workbook>, ou <xref:Microsoft.Office.Tools.Excel.Worksheet> hospedar itens em tempo de execução. Para obter mais informações, consulte [documentos de estender o Word e pastas de trabalho do Excel no suplemento do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
## <a name="programmatically-create-host-controls"></a>Criar controles de host de forma programática  
 Você pode adicionar programaticamente os controles de host para um <xref:Microsoft.Office.Tools.Word.Document> ou <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host em tempo de execução. Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
 Você não pode adicionar controles de host para um nativo <xref:Microsoft.Office.Interop.Word.Document> ou <xref:Microsoft.Office.Interop.Excel.Worksheet>.  
  
> [!NOTE]  
>  Os seguintes controles de host não podem ser adicionados por meio de programação para planilhas ou documentos: <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>, <xref:Microsoft.Office.Tools.Word.XMLNode>, e <xref:Microsoft.Office.Tools.Word.XMLNodes>.  
  
## <a name="understand-type-differences-between-host-items-host-controls-and-native-office-objects"></a>Entender as diferenças de tipo entre itens de host, controles de host e objetos nativos do Office  
 Para cada item de host e o controle de host, há um objeto Microsoft Office Word ou o Microsoft Office Excel nativo subjacente. Você pode acessar o objeto subjacente usando a propriedade InnerObject do item de host ou controle de host. No entanto, não é possível converter um objeto nativo do Office para o item de host correspondente ou controle de host. Se você tentar converter um objeto nativo do Office para o tipo de um item de host ou o controle de host, um <xref:System.InvalidCastException> é gerada.  
  
 Há várias situações em que as diferenças entre os tipos de itens de host e controles de host e os objetos do Office nativo subjacentes podem afetar seu código.  
  
### <a name="pass-host-controls-to-methods-and-properties"></a>Controles de host de passagem para métodos e propriedades  
 No Word, você não pode passar um controle de host para um método ou propriedade que requer um objeto do Word nativo como um parâmetro. Você deve usar a propriedade InnerObject do controle de host para retornar o objeto do Word nativo subjacente. Por exemplo, você pode passar um <xref:Microsoft.Office.Interop.Word.Bookmark> objeto para um método, passando o <xref:Microsoft.Office.Tools.Word.Bookmark.InnerObject%2A> propriedade o <xref:Microsoft.Office.Tools.Word.Bookmark> controle para o método de host.  
  
 No Excel, você deve usar a propriedade InnerObject do controle de host para passar o controle de host para um método ou propriedade quando o método ou propriedade espera o objeto subjacente do Excel.  
  
 O exemplo a seguir cria um <xref:Microsoft.Office.Tools.Excel.NamedRange> de controle e o transmite para o <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> método. O código usa o <xref:Microsoft.Office.Tools.Excel.NamedRange.InnerObject%2A> propriedade do intervalo nomeado para retornar o escritório base <xref:Microsoft.Office.Interop.Excel.Range> que é exigido pelo <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> método.  
  
 [!code-csharp[Trin_VstcoreHostControlsExcel#28](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#28)]
 [!code-vb[Trin_VstcoreHostControlsExcel#28](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#28)]  
  
### <a name="return-types-of-native-office-methods-and-properties"></a>Retornar tipos de propriedades e métodos nativos do Office  
 A maioria dos métodos e propriedades de itens de host de retornam o objeto de Office nativo subjacente no qual o item de host é baseado. Por exemplo, o <xref:Microsoft.Office.Tools.Excel.NamedRange.Parent%2A> propriedade de um <xref:Microsoft.Office.Tools.Excel.NamedRange> hospedar em Excel retorna um <xref:Microsoft.Office.Interop.Excel.Worksheet> objeto em vez de <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host. Da mesma forma, o <xref:Microsoft.Office.Tools.Word.RichTextContentControl.Parent%2A> propriedade de um <xref:Microsoft.Office.Tools.Word.RichTextContentControl> hospedar em retorna Word um <xref:Microsoft.Office.Interop.Word.Document> objeto em vez de <xref:Microsoft.Office.Tools.Word.Document> item de host.  
  
### <a name="access-collections-of-host-controls"></a>Coleções de acesso de controles de host  
 O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] não fornece coleções individuais para cada tipo de controle de host. Em vez disso, use a propriedade de controles de um item de host para iterar por todos os controles gerenciados (controles de host e controles de formulários do Windows) no documento ou planilha e, em seguida, procure itens que correspondem ao tipo de controle de host que você está interessado. O exemplo de código a seguir examina cada controle em um documento do Word e determina se o controle é um <xref:Microsoft.Office.Tools.Word.Bookmark>.  
  
 [!code-csharp[Trin_VstcoreHostControlsWord#10](../vsto/codesnippet/CSharp/trin_vstcorehostcontrolsword/ThisDocument.cs#10)]
 [!code-vb[Trin_VstcoreHostControlsWord#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsWordVB/ThisDocument.vb#10)]  
  
 Para obter mais informações sobre a propriedade de controles de itens de host, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
 Os modelos de objeto do Word e Excel incluem propriedades que expõem as coleções de controles nativos em documentos e planilhas. Você não pode acessar controles gerenciados usando essas propriedades. Por exemplo, não é possível enumerar cada <xref:Microsoft.Office.Tools.Word.Bookmark> hospedar em um documento usando o <xref:Microsoft.Office.Interop.Word._Document.Bookmarks%2A> propriedade de um <xref:Microsoft.Office.Interop.Word.Document> ou <xref:Microsoft.Office.Tools.Word.Document.Bookmarks%2A> propriedade de um <xref:Microsoft.Office.Tools.Word.Document>. Essas propriedades incluem apenas o <xref:Microsoft.Office.Interop.Word.Bookmark> controles no documento; eles não contêm o <xref:Microsoft.Office.Tools.Word.Bookmark> hospedar controles no documento.  
  
## <a name="see-also"></a>Consulte também  
 [Itens de host e visão geral dos controles de host](../vsto/host-items-and-host-controls-overview.md)   
 [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)   
 [Item de host de planilha](../vsto/worksheet-host-item.md)   
 [Item de host de pasta de trabalho](../vsto/workbook-host-item.md)   
 [Item de host do documento](../vsto/document-host-item.md)  
  
  