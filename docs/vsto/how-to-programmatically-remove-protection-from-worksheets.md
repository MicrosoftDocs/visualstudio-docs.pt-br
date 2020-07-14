---
title: 'Como: remover programaticamente a proteção de planilhas'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, unprotecting
- documents [Office development in Visual Studio], document protection
- document protection, removing from worksheets
- Unprotect method
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 72448f9d1e5c24c917459b8c2c59e317190e0a11
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85519867"
---
# <a name="how-to-programmatically-remove-protection-from-worksheets"></a>Como: remover programaticamente a proteção de planilhas
  Você pode remover programaticamente a proteção de uma planilha Microsoft Office Excel.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 O exemplo a seguir usa a variável `getPasswordFromUser` , que contém uma senha obtida do usuário.

## <a name="to-unprotect-a-worksheet-in-a-document-level-customization"></a>Para desproteger uma planilha em uma personalização em nível de documento

1. Chame o <xref:Microsoft.Office.Tools.Excel.Worksheet.Unprotect%2A> método da planilha e passe a senha, se necessário. Este exemplo pressupõe que você está trabalhando com uma planilha chamada `Sheet1` .

     [!code-csharp[Trin_VstcoreExcelAutomation#28](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#28)]
     [!code-vb[Trin_VstcoreExcelAutomation#28](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#28)]

## <a name="to-unprotect-a-worksheet-in-a-vsto-add-in"></a>Para desproteger uma planilha em um suplemento do VSTO

1. Chame o <xref:Microsoft.Office.Interop.Excel._Worksheet.Unprotect%2A> método da planilha ativa e passe a senha, se necessário.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#18](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#18)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#18](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#18)]

## <a name="see-also"></a>Confira também
- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Como: proteger planilhas programaticamente](../vsto/how-to-programmatically-protect-worksheets.md)
- [Como: proteger pastas de trabalho programaticamente](../vsto/how-to-programmatically-protect-workbooks.md)
- [Como: ocultar planilhas programaticamente](../vsto/how-to-programmatically-hide-worksheets.md)
- [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)
