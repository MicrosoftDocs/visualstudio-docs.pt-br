---
title: Como armazenar dados em cache em um documento protegido por senha
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], protected documents
- datasets [Office development in Visual Studio], caching
- data [Office development in Visual Studio], caching
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 12b04b985d54161343d26cdd32178b67bd6e6b91
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547232"
---
# <a name="how-to-cache-data-in-a-password-protected-document"></a>Como armazenar dados em cache em um documento protegido por senha
  Se você adicionar dados ao cache de dados em um documento ou pasta de trabalho protegido por uma senha, as alterações nos dados armazenados em cache não serão salvas automaticamente. Você pode salvar as alterações nos dados armazenados em cache substituindo dois métodos em seu projeto.

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="caching-in-word-documents"></a>Cache em documentos do Word

### <a name="to-cache-data-in-a-word-document-that-is-protected-with-a-password"></a>Para armazenar em cache dados em um documento do Word protegido por uma senha

1. Na `ThisDocument` classe, marque um campo público ou propriedade a ser armazenada em cache. Para obter mais informações, consulte [armazenar dados em cache](../vsto/caching-data.md).

2. Substitua o <xref:Microsoft.Office.Tools.Word.DocumentBase.UnprotectDocument%2A> método na `ThisDocument` classe e remova a proteção do documento.

     Quando o documento é salvo, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] chama esse método para lhe dar a oportunidade de desproteger o documento. Isso permite que as alterações feitas nos dados armazenados em cache sejam salvas.

3. Substitua o <xref:Microsoft.Office.Tools.Word.DocumentBase.ProtectDocument%2A> método na `ThisDocument` classe e reaplique a proteção ao documento.

     Depois que o documento é salvo, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] chama esse método para lhe dar a oportunidade de reaplicar a proteção ao documento.

### <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como armazenar em cache dados em um documento do Word protegido com uma senha. Antes que o código remova a proteção no <xref:Microsoft.Office.Tools.Word.DocumentBase.UnprotectDocument%2A> método, ele salva o <xref:Microsoft.Office.Tools.Word.Document.ProtectionType%2A> valor atual, para que o mesmo tipo de proteção possa ser reaplicado no <xref:Microsoft.Office.Tools.Word.DocumentBase.ProtectDocument%2A> método.

 [!code-csharp[Trin_CachedDataProtectedDocument#1](../vsto/codesnippet/CSharp/Trin_CachedDataProtectedDocument/ThisDocument.cs#1)]
 [!code-vb[Trin_CachedDataProtectedDocument#1](../vsto/codesnippet/VisualBasic/Trin_CachedDataProtectedDocument/ThisDocument.vb#1)]

### <a name="compile-the-code"></a>Compilar o código
 Adicione este código à `ThisDocument` classe em seu projeto. Esse código pressupõe que a senha seja armazenada em um campo chamado `securelyStoredPassword` .

## <a name="cache-in-excel-workbooks"></a>Cache em pastas de trabalho do Excel
 Em projetos do Excel, esse procedimento é necessário apenas quando você protege toda a pasta de trabalho com uma senha usando o <xref:Microsoft.Office.Tools.Excel.Workbook.Protect%2A> método. Esse procedimento não será necessário se você proteger apenas uma planilha específica com uma senha usando o <xref:Microsoft.Office.Tools.Excel.Worksheet.Protect%2A> método.

### <a name="to-cache-data-in-an-excel-workbook-that-is-protected-with-a-password"></a>Para armazenar em cache dados em uma pasta de trabalho do Excel protegida por uma senha

1. Na `ThisWorkbook` classe ou em uma das classes `Sheet` *n* , marque um campo público ou uma propriedade a ser armazenada em cache. Para obter mais informações, consulte [armazenar dados em cache](../vsto/caching-data.md).

2. Substitua o <xref:Microsoft.Office.Tools.Excel.WorkbookBase.UnprotectDocument%2A> método na `ThisWorkbook` classe e remova a proteção da pasta de trabalho.

     Quando a pasta de trabalho é salva, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] chama esse método para lhe dar a oportunidade de desproteger a pasta de trabalho. Isso permite que as alterações feitas nos dados armazenados em cache sejam salvas.

3. Substitua o <xref:Microsoft.Office.Tools.Excel.WorkbookBase.ProtectDocument%2A> método na `ThisWorkbook` classe e reaplique a proteção ao documento.

     Depois que a pasta de trabalho é salva, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] chama esse método para lhe dar a oportunidade de reaplicar a proteção à pasta de trabalho.

### <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como armazenar em cache dados em uma pasta de trabalho do Excel protegida por uma senha. Antes que o código remova a proteção no <xref:Microsoft.Office.Tools.Excel.WorkbookBase.UnprotectDocument%2A> método, ele salva o atual <xref:Microsoft.Office.Tools.Excel.Workbook.ProtectStructure%2A> e os <xref:Microsoft.Office.Tools.Excel.Workbook.ProtectWindows%2A> valores, para que o mesmo tipo de proteção possa ser reaplicado no <xref:Microsoft.Office.Tools.Excel.WorkbookBase.ProtectDocument%2A> método.

 [!code-vb[Trin_CachedDataProtectedWorkbook#1](../vsto/codesnippet/VisualBasic/Trin_CachedDataProtectedWorkbook/ThisWorkbook.vb#1)]
 [!code-csharp[Trin_CachedDataProtectedWorkbook#1](../vsto/codesnippet/CSharp/Trin_CachedDataProtectedWorkbook/ThisWorkbook.cs#1)]

### <a name="compile-the-code"></a>Compilar o código
 Adicione este código à `ThisWorkbook` classe em seu projeto. Esse código pressupõe que a senha seja armazenada em um campo chamado `securelyStoredPassword` .

## <a name="see-also"></a>Confira também
- [Dados de cache](../vsto/caching-data.md)
- [Como armazenar em cache dados para uso offline ou em um servidor](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [Como: armazenar em cache uma fonte de dados programaticamente em um documento do Office](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
