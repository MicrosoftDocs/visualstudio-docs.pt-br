---
title: Como preencher controles ListObject com dados
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- disconnecting from data sources
- ListObject control, disconnecting from a data source
- ListObject control, filling with data
- data [Office development in Visual Studio], adding to worksheets
- data binding, ListObject controls
- worksheets, populating with data
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2941022cb434198298e9d098ef562efeaba4893f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544814"
---
# <a name="how-to-fill-listobject-controls-with-data"></a>Como preencher controles ListObject com dados
  Você pode usar a associação de dados como uma maneira de adicionar rapidamente dados ao seu documento. Depois de vincular dados a um objeto de lista, você pode desconectar o objeto de lista para que ele exiba os dados, mas não esteja mais vinculado à fonte de dados.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

### <a name="to-bind-data-to-a-listobject-control"></a>Para associar dados a um controle ListObject

1. Crie um <xref:System.Data.DataTable> no nível de classe.

     [!code-csharp[Trin_VstcoreHostControlsExcel#20](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet4.cs#20)]
     [!code-vb[Trin_VstcoreHostControlsExcel#20](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet4.vb#20)]

2. Adicione colunas de exemplo e dados no `Startup` manipulador de eventos da `Sheet1` classe (em um projeto de nível de documento) ou `ThisAddIn` classe (em um projeto de nível de aplicativo).

     [!code-csharp[Trin_VstcoreHostControlsExcel#21](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet4.cs#21)]
     [!code-vb[Trin_VstcoreHostControlsExcel#21](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet4.vb#21)]

3. Chame o <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> método e passe os nomes de coluna na ordem em que eles devem aparecer. A ordem das colunas no objeto de lista pode ser diferente da ordem em que aparecem no <xref:System.Data.DataTable> .

     [!code-csharp[Trin_VstcoreHostControlsExcel#22](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet4.cs#22)]
     [!code-vb[Trin_VstcoreHostControlsExcel#22](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet4.vb#22)]

### <a name="to-disconnect-the-listobject-control-from-the-data-source"></a>Para desconectar o controle ListObject da fonte de dados

1. Chame o método <xref:Microsoft.Office.Tools.Excel.ListObject.Disconnect%2A> de `List1`.

     [!code-csharp[Trin_VstcoreHostControlsExcel#23](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet4.cs#23)]
     [!code-vb[Trin_VstcoreHostControlsExcel#23](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet4.vb#23)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo de código pressupõe que você tenha um <xref:Microsoft.Office.Tools.Excel.ListObject> nome existente `list1` na planilha na qual esse código é exibido.

## <a name="see-also"></a>Consulte também
- [Estenda documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Controles em documentos do Office](../vsto/controls-on-office-documents.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Como mapear colunas ListObject para dados](../vsto/how-to-map-listobject-columns-to-data.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Controle ListObject](../vsto/listobject-control.md)
- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Como: preencher planilhas com dados de um banco de dado](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)
- [Como: popular documentos com dados de serviços](../vsto/how-to-populate-documents-with-data-from-services.md)
