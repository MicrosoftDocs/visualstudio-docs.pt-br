---
title: 'Como: criar tabelas do Word programaticamente'
description: Saiba como usar o método Add da coleção Tables para adicionar uma tabela no intervalo especificado em um documento do Microsoft Word.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 5651487e280d7fb9912734b919b00fab28a702db
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827377"
---
# <a name="how-to-programmatically-create-word-tables"></a>Como: criar tabelas do Word programaticamente
  A <xref:Microsoft.Office.Interop.Word.Tables> coleção é um membro das <xref:Microsoft.Office.Interop.Word.Document> classes, <xref:Microsoft.Office.Tools.Word.Document> , <xref:Microsoft.Office.Interop.Word.Selection> e <xref:Microsoft.Office.Interop.Word.Range> , o que significa que você pode criar uma tabela em qualquer um desses contextos. Você usa o <xref:Microsoft.Office.Interop.Word.Tables.Add%2A> método da <xref:Microsoft.Office.Interop.Word.Tables> coleção para adicionar uma tabela no intervalo especificado.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="create-tables-in-document-level-customizations"></a>Criar tabelas em personalizações em nível de documento

### <a name="to-add-a-table-to-a-document"></a>Para adicionar uma tabela a um documento

- Use o <xref:Microsoft.Office.Interop.Word.Tables.Add%2A> método para adicionar uma tabela que consiste em três linhas e quatro colunas no início do documento.

   Para usar o exemplo de código a seguir, execute-o da `ThisDocument` classe em seu projeto.

   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet86":::
   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet86":::

  Quando você cria uma tabela, ela é automaticamente adicionada à <xref:Microsoft.Office.Interop.Word.Tables> coleção do item de <xref:Microsoft.Office.Tools.Word.Document> host. Em seguida, você pode consultar a tabela por seu número de item usando a <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> propriedade, conforme mostrado no código a seguir.

### <a name="to-refer-to-a-table-by-item-number"></a>Para fazer referência a uma tabela por número de item

1. Use a <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> propriedade e forneça o número de item da tabela que você deseja fazer referência.

    Para usar o exemplo de código a seguir, execute-o da `ThisDocument` classe em seu projeto.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet87":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet87":::

   Cada <xref:Microsoft.Office.Interop.Word.Table> objeto também tem uma <xref:Microsoft.Office.Interop.Word.Table.Range%2A> propriedade que permite definir atributos de formatação.

### <a name="to-apply-a-style-to-a-table"></a>Para aplicar um estilo a uma tabela

1. Use a <xref:Microsoft.Office.Interop.Word.Table.Style%2A> propriedade para aplicar um dos estilos internos da palavra a uma tabela.

     Para usar o exemplo de código a seguir, execute-o da `ThisDocument` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet88":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet88":::

## <a name="create-tables-in-vsto-add-ins"></a>Criar tabelas em suplementos do VSTO

### <a name="to-add-a-table-to-a-document"></a>Para adicionar uma tabela a um documento

- Use o <xref:Microsoft.Office.Interop.Word.Tables.Add%2A> método para adicionar uma tabela que consiste em três linhas e quatro colunas no início do documento.

   O exemplo de código a seguir adiciona uma tabela ao documento ativo. Para usar este exemplo, execute-o da `ThisAddIn` classe em seu projeto.

   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet86":::
   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet86":::

  Quando você cria uma tabela, ela é automaticamente adicionada à <xref:Microsoft.Office.Interop.Word.Tables> coleção do <xref:Microsoft.Office.Interop.Word.Document> . Em seguida, você pode consultar a tabela por seu número de item usando a <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> propriedade, conforme mostrado no código a seguir.

### <a name="to-refer-to-a-table-by-item-number"></a>Para fazer referência a uma tabela por número de item

1. Use a <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> propriedade e forneça o número de item da tabela que você deseja fazer referência.

    O exemplo de código a seguir usa o documento ativo. Para usar este exemplo, execute-o da `ThisAddIn` classe em seu projeto.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet87":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet87":::

   Cada <xref:Microsoft.Office.Interop.Word.Table> objeto também tem uma <xref:Microsoft.Office.Interop.Word.Table.Range%2A> propriedade que permite definir atributos de formatação.

### <a name="to-apply-a-style-to-a-table"></a>Para aplicar um estilo a uma tabela

1. Use a <xref:Microsoft.Office.Interop.Word.Table.Style%2A> propriedade para aplicar um dos estilos internos da palavra a uma tabela.

     O exemplo de código a seguir usa o documento ativo. Para usar este exemplo, execute-o da `ThisAddIn` classe em seu projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet88":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet88":::

## <a name="see-also"></a>Consulte também
- [Como: adicionar texto e formatação programaticamente a células em tabelas do Word](../vsto/how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables.md)
- [Como: adicionar linhas e colunas programaticamente a tabelas do Word](../vsto/how-to-programmatically-add-rows-and-columns-to-word-tables.md)
- [Como: preencher programaticamente tabelas do Word com propriedades do documento](../vsto/how-to-programmatically-populate-word-tables-with-document-properties.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
