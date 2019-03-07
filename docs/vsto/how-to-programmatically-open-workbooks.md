---
title: 'Como: Abrir pastas de trabalho de forma programática'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, opening
- Excel [Office development in Visual Studio], opening workbooks
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f9d8ab4be67ffd84406869c956f9046a53d6ec79
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56611887"
---
# <a name="how-to-programmatically-open-workbooks"></a>Como: Abrir pastas de trabalho de forma programática
  O <xref:Microsoft.Office.Interop.Excel.Workbooks> coleta no Microsoft Office Excel torna possível para trabalhar com todas as pastas de trabalho e para abrir pastas de trabalho.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-open-an-existing-workbook"></a>Para abrir uma pasta de trabalho existente

1.  Use o <xref:Microsoft.Office.Interop.Excel.Workbooks.Open%2A> método da <xref:Microsoft.Office.Interop.Excel.Workbooks> coleção, passando o caminho para a pasta de trabalho.

     [!code-csharp[Trin_VstcoreExcelAutomation#2](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#2)]
     [!code-vb[Trin_VstcoreExcelAutomation#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#2)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo de código requer o seguinte:

-   Uma pasta de trabalho chamada `YourWorkbook.xls` deve existir em um diretório chamado `Test` na unidade C.

## <a name="see-also"></a>Consulte também
- [Trabalhar com pastas de trabalho](../vsto/working-with-workbooks.md)
- [Como: Abrir arquivos de texto, de forma programática, como pastas de trabalho](../vsto/how-to-programmatically-open-text-files-as-workbooks.md)
- [Como: Criar novas pastas de trabalho de forma programática](../vsto/how-to-programmatically-create-new-workbooks.md)
- [Como: Salvar pastas de trabalho de forma programática](../vsto/how-to-programmatically-save-workbooks.md)
- [Como: Fechar pastas de trabalho de forma programática](../vsto/how-to-programmatically-close-workbooks.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
- [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)
