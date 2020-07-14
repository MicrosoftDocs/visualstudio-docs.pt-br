---
title: Como mapear colunas ListObject para dados
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], mapping to ListObject column
- ListObject control, mapping data
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b09c07c8b36baeed096c0049c778e431fe232458
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538158"
---
# <a name="how-to-map-listobject-columns-to-data"></a>Como mapear colunas ListObject para dados
  Ao associar um <xref:Microsoft.Office.Tools.Excel.ListObject> controle a um <xref:System.Data.DataTable> , talvez você não queira exibir todas as colunas em uma lista ou pode ter determinadas colunas que não estão associadas aos dados. Você pode mapear as colunas que deseja que apareçam no <xref:Microsoft.Office.Tools.Excel.ListObject> quando chamar o <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> método.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="map-columns"></a>Mapear colunas

### <a name="to-map-a-data-table-to-columns-in-a-list"></a>Para mapear uma tabela de dados para colunas em uma lista

1. Crie o <xref:System.Data.DataTable> no nível de classe.

     [!code-csharp[Trin_VstcoreHostControlsExcel#16](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs#16)]
     [!code-vb[Trin_VstcoreHostControlsExcel#16](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb#16)]

2. Adicione colunas de exemplo e dados no `Startup` manipulador de eventos da `Sheet1` classe (em um projeto de nível de documento) ou `ThisAddIn` classe (em um projeto de suplemento do VSTO).

     [!code-csharp[Trin_VstcoreHostControlsExcel#17](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs#17)]
     [!code-vb[Trin_VstcoreHostControlsExcel#17](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb#17)]

3. Chame o <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> método e passe os nomes de coluna na ordem em que eles devem aparecer. O objeto de lista será vinculado ao recém-criado <xref:System.Data.DataTable> , mas a ordem das colunas no objeto de lista será diferente da ordem em que aparecem no <xref:System.Data.DataTable> .

     [!code-csharp[Trin_VstcoreHostControlsExcel#18](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs#18)]
     [!code-vb[Trin_VstcoreHostControlsExcel#18](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb#18)]

## <a name="specify-unmapped-columns"></a>Especificar colunas não mapeadas
 Ao mapear colunas para um <xref:System.Data.DataTable> , você também pode especificar que determinadas colunas não devem ser vinculadas aos dados, passando uma cadeia de caracteres vazia. Uma nova coluna que não está associada a dados é adicionada ao <xref:Microsoft.Office.Tools.Excel.ListObject> controle.

### <a name="to-specify-an-unmapped-column-when-mapping-listobject-columns"></a>Para especificar uma coluna não mapeada ao mapear colunas ListObject

1. Chame o <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> método e passe os nomes de coluna na ordem em que eles devem aparecer. Use uma cadeia de caracteres vazia para indicar onde uma coluna não mapeada é adicionada; Nesse caso, entre a coluna Title e a coluna Last Name.

     [!code-csharp[Trin_VstcoreHostControlsExcel#19](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs#19)]
     [!code-vb[Trin_VstcoreHostControlsExcel#19](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb#19)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo de código pressupõe que você tenha um <xref:Microsoft.Office.Tools.Excel.ListObject> nome existente `list1` na planilha na qual esse código é exibido.

## <a name="see-also"></a>Confira também
- [Estenda documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Controles em documentos do Office](../vsto/controls-on-office-documents.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Como preencher controles ListObject com dados](../vsto/how-to-fill-listobject-controls-with-data.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Controle ListObject](../vsto/listobject-control.md)
