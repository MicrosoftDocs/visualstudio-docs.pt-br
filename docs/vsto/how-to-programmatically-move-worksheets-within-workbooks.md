---
title: 'Como: mover planilhas programaticamente dentro de pastas de trabalho'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, moving
- workbooks, moving worksheets in
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4594395eb887a950c9ff0ba41cd8d3c625d35dc3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85519815"
---
# <a name="how-to-programmatically-move-worksheets-within-workbooks"></a>Como: mover planilhas programaticamente dentro de pastas de trabalho
  Você pode alterar programaticamente a posição das planilhas em relação a outras planilhas em uma pasta de trabalho. Se você não especificar um local para a planilha movida, o Excel criará uma nova pasta de trabalho para contê-la.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-move-a-worksheet-in-a-document-level-customization"></a>Para mover uma planilha em uma personalização no nível do documento

1. Atribua o número total de planilhas na pasta de trabalho a uma variável e, em seguida, mova a primeira planilha para que ela se torne a última.

     [!code-csharp[Trin_VstcoreExcelAutomation#24](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#24)]
     [!code-vb[Trin_VstcoreExcelAutomation#24](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#24)]

## <a name="to-move-a-worksheet-in-a-vsto-add-in"></a>Para mover uma planilha em um suplemento do VSTO

1. Atribua o número total de planilhas na pasta de trabalho a uma variável e, em seguida, mova a primeira planilha para que ela se torne a última.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#16](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#16)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#16](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#16)]

## <a name="see-also"></a>Confira também
- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Como: ocultar planilhas programaticamente](../vsto/how-to-programmatically-hide-worksheets.md)
- [Como: excluir programaticamente planilhas de pastas de trabalho](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [Como: proteger planilhas programaticamente](../vsto/how-to-programmatically-protect-worksheets.md)
- [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)
