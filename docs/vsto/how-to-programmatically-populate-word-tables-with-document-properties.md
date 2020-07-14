---
title: Popular tabelas do Word com propriedades de documento programaticamente
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- document properties, inserting in Word tables
- documents [Office development in Visual Studio], document properties
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 92d9b38c6a1e770749849966deec7f503f9eeb5d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537807"
---
# <a name="how-to-programmatically-populate-word-tables-with-document-properties"></a>Como: preencher programaticamente tabelas do Word com propriedades do documento
  O exemplo a seguir cria uma tabela do Word Microsoft Office na parte superior do documento e a popula com as propriedades do documento host.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="populate-tables-in-a-document-level-customization"></a>Popular tabelas em uma personalização no nível do documento

### <a name="to-create-a-table-and-populate-it-with-document-properties"></a>Para criar uma tabela e preenchê-la com propriedades do documento

1. Defina o intervalo para a parte superior do documento.

    [!code-vb[Trin_VstcoreWordAutomation#90](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#90)]
    [!code-csharp[Trin_VstcoreWordAutomation#90](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#90)]

2. Insira um título para a tabela e inclua marcas de parágrafo.

    [!code-vb[Trin_VstcoreWordAutomation#91](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#91)]
    [!code-csharp[Trin_VstcoreWordAutomation#91](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#91)]

3. Adicione a tabela ao documento no intervalo.

    [!code-vb[Trin_VstcoreWordAutomation#92](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#92)]
    [!code-csharp[Trin_VstcoreWordAutomation#92](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#92)]

4. Formate a tabela e aplique um estilo.

    [!code-vb[Trin_VstcoreWordAutomation#93](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#93)]
    [!code-csharp[Trin_VstcoreWordAutomation#93](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#93)]

5. Insira as propriedades do documento em células.

    [!code-vb[Trin_VstcoreWordAutomation#94](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#94)]
    [!code-csharp[Trin_VstcoreWordAutomation#94](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#94)]

   O exemplo a seguir mostra o procedimento completo. Para usar esse código, execute-o da `ThisDocument` classe em seu projeto.

   [!code-vb[Trin_VstcoreWordAutomation#89](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#89)]
   [!code-csharp[Trin_VstcoreWordAutomation#89](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#89)]

## <a name="populate-tables-in-a-vsto-add-in"></a>Popular tabelas em um suplemento do VSTO

### <a name="to-create-a-table-and-populate-it-with-document-properties"></a>Para criar uma tabela e preenchê-la com propriedades do documento

1. Defina o intervalo para a parte superior do documento.

    [!code-vb[Trin_VstcoreWordAutomationAddIn#90](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#90)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#90](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#90)]

2. Insira um título para a tabela e inclua marcas de parágrafo.

    [!code-vb[Trin_VstcoreWordAutomationAddIn#91](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#91)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#91](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#91)]

3. Adicione a tabela ao documento no intervalo.

    [!code-vb[Trin_VstcoreWordAutomationAddIn#92](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#92)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#92](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#92)]

4. Formate a tabela e aplique um estilo.

    [!code-vb[Trin_VstcoreWordAutomationAddIn#93](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#93)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#93](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#93)]

5. Insira as propriedades do documento em células.

    [!code-vb[Trin_VstcoreWordAutomationAddIn#94](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#94)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#94](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#94)]

   O exemplo a seguir mostra o procedimento completo. Para usar esse código, execute-o da `ThisAddIn` classe em seu projeto.

   [!code-vb[Trin_VstcoreWordAutomationAddIn#89](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#89)]
   [!code-csharp[Trin_VstcoreWordAutomationAddIn#89](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#89)]

## <a name="see-also"></a>Consulte também
- [Como: criar tabelas do Word programaticamente](../vsto/how-to-programmatically-create-word-tables.md)
- [Como: adicionar texto e formatação programaticamente a células em tabelas do Word](../vsto/how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables.md)
- [Como: adicionar linhas e colunas programaticamente a tabelas do Word](../vsto/how-to-programmatically-add-rows-and-columns-to-word-tables.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
