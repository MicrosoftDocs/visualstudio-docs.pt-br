---
title: Adicionar texto & formatação a células de tabela do Word programaticamente
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- cells, adding text and formatting
- text [Office development in Visual Studio], adding to Word tables
- formatting [Office development in Visual Studio]
- tables [Office development in Visual Studio], adding text and formatting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: acd43c82c6dae32ef6595b2f63c06fe61f3c6168
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538041"
---
# <a name="how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables"></a>Como: adicionar texto e formatação programaticamente a células em tabelas do Word
  Cada tabela consiste em uma coleção de células. Cada <xref:Microsoft.Office.Interop.Word.Cell> objeto individual representa uma célula na tabela. Você faz referência a cada célula por seu local na tabela. Este exemplo refere-se à célula localizada na primeira linha e à primeira coluna da tabela; adiciona texto à célula; e aplica formatação.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-add-text-and-formatting-to-cells"></a>Para adicionar texto e formatação às células

1. Consulte a célula por seu local na tabela, adicione texto à célula e aplique a formatação.

     O exemplo de código a seguir pode ser usado em uma personalização em nível de documento. Para usar este exemplo, execute-o da `ThisDocument` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomation#97](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#97)]
     [!code-csharp[Trin_VstcoreWordAutomation#97](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#97)]

     O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Este exemplo usa o documento ativo. Para usar o exemplo, execute-o da `ThisAddIn` classe em seu projeto.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#97](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#97)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#97](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#97)]

## <a name="see-also"></a>Consulte também
- [Como: criar tabelas do Word programaticamente](../vsto/how-to-programmatically-create-word-tables.md)
- [Como: adicionar linhas e colunas programaticamente a tabelas do Word](../vsto/how-to-programmatically-add-rows-and-columns-to-word-tables.md)
- [Como: preencher programaticamente tabelas do Word com propriedades do documento](../vsto/how-to-programmatically-populate-word-tables-with-document-properties.md)
