---
title: Como mapear colunas ListObject para dados
description: Saiba como você pode mapear quais colunas você deseja que apareçam no ListObject ao chamar o método SetDataBinding.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 68cb12503d0f8ad59de92f965c0ed51fbc0d7f40
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827452"
---
# <a name="how-to-map-listobject-columns-to-data"></a>Como mapear colunas ListObject para dados
  Ao associar um <xref:Microsoft.Office.Tools.Excel.ListObject> controle a um <xref:System.Data.DataTable> , talvez você não queira exibir todas as colunas em uma lista ou pode ter determinadas colunas que não estão associadas aos dados. Você pode mapear as colunas que deseja que apareçam no <xref:Microsoft.Office.Tools.Excel.ListObject> quando chamar o <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> método.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="map-columns"></a>Mapear colunas

### <a name="to-map-a-data-table-to-columns-in-a-list"></a>Para mapear uma tabela de dados para colunas em uma lista

1. Crie o <xref:System.Data.DataTable> no nível de classe.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs" id="Snippet16":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb" id="Snippet16":::

2. Adicione colunas de exemplo e dados no `Startup` manipulador de eventos da `Sheet1` classe (em um projeto de nível de documento) ou `ThisAddIn` classe (em um projeto de suplemento do VSTO).

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs" id="Snippet17":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb" id="Snippet17":::

3. Chame o <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> método e passe os nomes de coluna na ordem em que eles devem aparecer. O objeto de lista será vinculado ao recém-criado <xref:System.Data.DataTable> , mas a ordem das colunas no objeto de lista será diferente da ordem em que aparecem no <xref:System.Data.DataTable> .

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs" id="Snippet18":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb" id="Snippet18":::

## <a name="specify-unmapped-columns"></a>Especificar colunas não mapeadas
 Ao mapear colunas para um <xref:System.Data.DataTable> , você também pode especificar que determinadas colunas não devem ser vinculadas aos dados, passando uma cadeia de caracteres vazia. Uma nova coluna que não está associada a dados é adicionada ao <xref:Microsoft.Office.Tools.Excel.ListObject> controle.

### <a name="to-specify-an-unmapped-column-when-mapping-listobject-columns"></a>Para especificar uma coluna não mapeada ao mapear colunas ListObject

1. Chame o <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> método e passe os nomes de coluna na ordem em que eles devem aparecer. Use uma cadeia de caracteres vazia para indicar onde uma coluna não mapeada é adicionada; Nesse caso, entre a coluna Title e a coluna Last Name.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs" id="Snippet19":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb" id="Snippet19":::

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo de código pressupõe que você tenha um <xref:Microsoft.Office.Tools.Excel.ListObject> nome existente `list1` na planilha na qual esse código é exibido.

## <a name="see-also"></a>Consulte também
- [Estenda documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Controles em documentos do Office](../vsto/controls-on-office-documents.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Como preencher controles ListObject com dados](../vsto/how-to-fill-listobject-controls-with-data.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Controle ListObject](../vsto/listobject-control.md)
