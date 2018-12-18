---
title: 'Como: colunas de mapa ListObject para dados'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], mapping to ListObject column
- ListObject control, mapping data
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: b77d33b8d30ed7f581e27e1cbe07d0c90715ff04
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670190"
---
# <a name="how-to-map-listobject-columns-to-data"></a>Como: colunas de mapa ListObject para dados
  Quando você associa um <xref:Microsoft.Office.Tools.Excel.ListObject> o controle para um <xref:System.Data.DataTable>, talvez você não queira exibir todas as colunas em uma lista ou você pode ter determinadas colunas que não estão associadas aos dados. Você pode mapear as colunas que você deseja que apareça na <xref:Microsoft.Office.Tools.Excel.ListObject> quando você chama o <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> método.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
 ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [How do i: criar uma lista no Excel que está conectado a uma lista do SharePoint?](http://go.microsoft.com/fwlink/?LinkID=130263).  
  
## <a name="map-columns"></a>Mapear colunas  
  
### <a name="to-map-a-data-table-to-columns-in-a-list"></a>Para mapear uma tabela de dados para colunas em uma lista  
  
1.  Criar o <xref:System.Data.DataTable> no nível de classe.  
  
     [!code-csharp[Trin_VstcoreHostControlsExcel#16](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs#16)]
     [!code-vb[Trin_VstcoreHostControlsExcel#16](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb#16)]  
  
2.  Adicionar colunas de amostra e dados na `Startup` manipulador de eventos do `Sheet1` classe (em um projeto de nível de documento) ou `ThisAddIn` classe (em um projeto de suplemento do VSTO).  
  
     [!code-csharp[Trin_VstcoreHostControlsExcel#17](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs#17)]
     [!code-vb[Trin_VstcoreHostControlsExcel#17](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb#17)]  
  
3.  Chamar o <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> método e passar os nomes de coluna na ordem em que elas devem aparecer. O objeto de lista será associado ao recém-criado <xref:System.Data.DataTable>, mas a ordem das colunas no objeto da lista será diferente da ordem em que aparecem no <xref:System.Data.DataTable>.  
  
     [!code-csharp[Trin_VstcoreHostControlsExcel#18](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs#18)]
     [!code-vb[Trin_VstcoreHostControlsExcel#18](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb#18)]  
  
## <a name="specify-unmapped-columns"></a>Especifique as colunas não mapeadas  
 Quando você mapear colunas para um <xref:System.Data.DataTable>, você também pode especificar que determinadas colunas não devem ser associadas a dados, passando uma cadeia de caracteres vazia. Uma nova coluna que não está associada a dados é adicionada ao <xref:Microsoft.Office.Tools.Excel.ListObject> controle.  
  
### <a name="to-specify-an-unmapped-column-when-mapping-listobject-columns"></a>Para especificar uma coluna não mapeada ao mapear colunas ListObject  
  
1.  Chamar o <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> método e passar os nomes de coluna na ordem em que elas devem aparecer. Use uma cadeia de caracteres vazia para indicar onde uma coluna não mapeada é adicionada; Nesse caso, entre a coluna de título e a última coluna de nome.  
  
     [!code-csharp[Trin_VstcoreHostControlsExcel#19](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs#19)]
     [!code-vb[Trin_VstcoreHostControlsExcel#19](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb#19)]  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo de código pressupõe que você tiver uma <xref:Microsoft.Office.Tools.Excel.ListObject> chamado `list1` na planilha em que esse código é exibida.  
  
## <a name="see-also"></a>Consulte também  
 [Estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)   
 [Controles em documentos do Office](../vsto/controls-on-office-documents.md)   
 [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)   
 [Como: controla o preenchimento ListObject com dados](../vsto/how-to-fill-listobject-controls-with-data.md)   
 [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)   
 [Controle ListObject](../vsto/listobject-control.md)  
  
  