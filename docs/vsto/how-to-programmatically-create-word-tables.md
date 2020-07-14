---
title: 'Como: criar tabelas do Word programaticamente'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], adding tables
- tables [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a1bc20b277df90ae963d257137373457a0196e72
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544749"
---
# <a name="how-to-programmatically-create-word-tables"></a>Como: criar tabelas do Word programaticamente
  A <xref:Microsoft.Office.Interop.Word.Tables> coleção é um membro das <xref:Microsoft.Office.Interop.Word.Document> classes, <xref:Microsoft.Office.Tools.Word.Document> , <xref:Microsoft.Office.Interop.Word.Selection> e <xref:Microsoft.Office.Interop.Word.Range> , o que significa que você pode criar uma tabela em qualquer um desses contextos. Você usa o <xref:Microsoft.Office.Interop.Word.Tables.Add%2A> método da <xref:Microsoft.Office.Interop.Word.Tables> coleção para adicionar uma tabela no intervalo especificado.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="create-tables-in-document-level-customizations"></a>Criar tabelas em personalizações em nível de documento

### <a name="to-add-a-table-to-a-document"></a>Para adicionar uma tabela a um documento

- Use o <xref:Microsoft.Office.Interop.Word.Tables.Add%2A> método para adicionar uma tabela que consiste em três linhas e quatro colunas no início do documento.

   Para usar o exemplo de código a seguir, execute-o da `ThisDocument` classe em seu projeto.

   [!code-vb[Trin_VstcoreWordAutomation#86](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#86)]
   [!code-csharp[Trin_VstcoreWordAutomation#86](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#86)]

  Quando você cria uma tabela, ela é automaticamente adicionada à <xref:Microsoft.Office.Interop.Word.Tables> coleção do item de <xref:Microsoft.Office.Tools.Word.Document> host. Em seguida, você pode consultar a tabela por seu número de item usando a <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> propriedade, conforme mostrado no código a seguir.

### <a name="to-refer-to-a-table-by-item-number"></a>Para fazer referência a uma tabela por número de item

1. Use a <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> propriedade e forneça o número de item da tabela que você deseja fazer referência.

    Para usar o exemplo de código a seguir, execute-o da `ThisDocument` classe em seu projeto.

    [!code-vb[Trin_VstcoreWordAutomation#87](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#87)]
    [!code-csharp[Trin_VstcoreWordAutomation#87](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#87)]

   Cada <xref:Microsoft.Office.Interop.Word.Table> objeto também tem uma <xref:Microsoft.Office.Interop.Word.Table.Range%2A> propriedade que permite definir atributos de formatação.

### <a name="to-apply-a-style-to-a-table"></a>Para aplicar um estilo a uma tabela

1. Use a <xref:Microsoft.Office.Interop.Word.Table.Style%2A> propriedade para aplicar um dos estilos internos da palavra a uma tabela.

     Para usar o exemplo de código a seguir, execute-o da `ThisDocument` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#88](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#88)]
     [!code-csharp[Trin_VstcoreWordAutomation#88](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#88)]

## <a name="create-tables-in-vsto-add-ins"></a>Criar tabelas em suplementos do VSTO

### <a name="to-add-a-table-to-a-document"></a>Para adicionar uma tabela a um documento

- Use o <xref:Microsoft.Office.Interop.Word.Tables.Add%2A> método para adicionar uma tabela que consiste em três linhas e quatro colunas no início do documento.

   O exemplo de código a seguir adiciona uma tabela ao documento ativo. Para usar este exemplo, execute-o da `ThisAddIn` classe em seu projeto.

   [!code-vb[Trin_VstcoreWordAutomationAddIn#86](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#86)]
   [!code-csharp[Trin_VstcoreWordAutomationAddIn#86](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#86)]

  Quando você cria uma tabela, ela é automaticamente adicionada à <xref:Microsoft.Office.Interop.Word.Tables> coleção do <xref:Microsoft.Office.Interop.Word.Document> . Em seguida, você pode consultar a tabela por seu número de item usando a <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> propriedade, conforme mostrado no código a seguir.

### <a name="to-refer-to-a-table-by-item-number"></a>Para fazer referência a uma tabela por número de item

1. Use a <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> propriedade e forneça o número de item da tabela que você deseja fazer referência.

    O exemplo de código a seguir usa o documento ativo. Para usar este exemplo, execute-o da `ThisAddIn` classe em seu projeto.

    [!code-vb[Trin_VstcoreWordAutomationAddIn#87](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#87)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#87](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#87)]

   Cada <xref:Microsoft.Office.Interop.Word.Table> objeto também tem uma <xref:Microsoft.Office.Interop.Word.Table.Range%2A> propriedade que permite definir atributos de formatação.

### <a name="to-apply-a-style-to-a-table"></a>Para aplicar um estilo a uma tabela

1. Use a <xref:Microsoft.Office.Interop.Word.Table.Style%2A> propriedade para aplicar um dos estilos internos da palavra a uma tabela.

     O exemplo de código a seguir usa o documento ativo. Para usar este exemplo, execute-o da `ThisAddIn` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#88](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#88)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#88](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#88)]

## <a name="see-also"></a>Consulte também
- [Como: adicionar texto e formatação programaticamente a células em tabelas do Word](../vsto/how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables.md)
- [Como: adicionar linhas e colunas programaticamente a tabelas do Word](../vsto/how-to-programmatically-add-rows-and-columns-to-word-tables.md)
- [Como: preencher programaticamente tabelas do Word com propriedades do documento](../vsto/how-to-programmatically-populate-word-tables-with-document-properties.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
