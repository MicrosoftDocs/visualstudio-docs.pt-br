---
title: 'Como: armazenar em Cache os dados em um documento protegido por senha'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], protected documents
- datasets [Office development in Visual Studio], caching
- data [Office development in Visual Studio], caching
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: c15d3fee1728118df2701cc940dc288ae500942d
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35255337"
---
# <a name="how-to-cache-data-in-a-password-protected-document"></a>Como: armazenar em Cache os dados em um documento protegido por senha
  Se você adicionar dados ao cache de dados em um documento ou pasta de trabalho protegida com uma senha, as alterações nos dados armazenados em cache não são salvas automaticamente. Você pode salvar as alterações aos dados armazenados em cache por substituir dois métodos em seu projeto.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
## <a name="caching-in-word-documents"></a>Armazenamento em cache em documentos do Word  
  
### <a name="to-cache-data-in-a-word-document-that-is-protected-with-a-password"></a>Os dados em cache em um documento do Word que está protegido com uma senha  
  
1.  No `ThisDocument` de classe, marcar um campo ou propriedade pública a ser armazenado em cache. Para obter mais informações, consulte [armazenar em Cache dados](../vsto/caching-data.md).  
  
2.  Substituir a <xref:Microsoft.Office.Tools.Word.DocumentBase.UnprotectDocument%2A> método no `ThisDocument` de classe e remover a proteção do documento.  
  
     Quando o documento é salvo, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] chama esse método para dar a você uma oportunidade para desproteger o documento. Isso permite que as alterações feitas nos dados armazenados em cache sejam salvas.  
  
3.  Substituir a <xref:Microsoft.Office.Tools.Word.DocumentBase.ProtectDocument%2A> método no `ThisDocument` de classe e reaplicar a proteção para o documento.  
  
     Depois que o documento é salvo, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] chama esse método para lhe dar uma oportunidade de reaplicar proteção por documento.  
  
### <a name="example"></a>Exemplo  
 O exemplo de código a seguir demonstra como armazenar em cache os dados em um documento do Word que está protegido com uma senha. Antes do código remove a proteção contra o <xref:Microsoft.Office.Tools.Word.DocumentBase.UnprotectDocument%2A> método, ele salva o atual <xref:Microsoft.Office.Tools.Word.Document.ProtectionType%2A> de valor, para que o mesmo tipo de proteção pode ser reaplicado no <xref:Microsoft.Office.Tools.Word.DocumentBase.ProtectDocument%2A> método.  
  
 [!code-csharp[Trin_CachedDataProtectedDocument#1](../vsto/codesnippet/CSharp/Trin_CachedDataProtectedDocument/ThisDocument.cs#1)]
 [!code-vb[Trin_CachedDataProtectedDocument#1](../vsto/codesnippet/VisualBasic/Trin_CachedDataProtectedDocument/ThisDocument.vb#1)]  
  
### <a name="compile-the-code"></a>Compilar o código  
 Adicione este código para o `ThisDocument` classe em seu projeto. Esse código supõe que a senha é armazenada em um campo chamado `securelyStoredPassword`.  
  
## <a name="cache-in-excel-workbooks"></a>Armazenar em cache em pastas de trabalho do Excel  
 Em projetos do Excel, esse procedimento é necessário somente quando você protege toda a pasta de trabalho com uma senha usando o <xref:Microsoft.Office.Tools.Excel.Workbook.Protect%2A> método. Esse procedimento não será necessário se você proteger apenas uma planilha específica com uma senha usando o <xref:Microsoft.Office.Tools.Excel.Worksheet.Protect%2A> método.  
  
### <a name="to-cache-data-in-an-excel-workbook-that-is-protected-with-a-password"></a>Os dados em cache em uma pasta de trabalho do Excel que é protegida por senha  
  
1.  No `ThisWorkbook` classe ou uma da `Sheet` *n* classes, marcar um campo ou propriedade pública a ser armazenado em cache. Para obter mais informações, consulte [armazenar em Cache dados](../vsto/caching-data.md).  
  
2.  Substituir a <xref:Microsoft.Office.Tools.Excel.WorkbookBase.UnprotectDocument%2A> método no `ThisWorkbook` de classe e remover a proteção da pasta de trabalho.  
  
     Quando a pasta de trabalho é salvo, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] chama esse método para dar a você uma oportunidade para desproteger a pasta de trabalho. Isso permite que as alterações feitas nos dados armazenados em cache sejam salvas.  
  
3.  Substituir a <xref:Microsoft.Office.Tools.Excel.WorkbookBase.ProtectDocument%2A> método no `ThisWorkbook` de classe e reaplicar a proteção para o documento.  
  
     Depois que a pasta de trabalho é salvo, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] chama esse método para lhe dar uma oportunidade de reaplicar a proteção para a pasta de trabalho.  
  
### <a name="example"></a>Exemplo  
 O exemplo de código a seguir demonstra como armazenar em cache os dados em uma pasta de trabalho do Excel que é protegida por senha. Antes do código remove a proteção contra o <xref:Microsoft.Office.Tools.Excel.WorkbookBase.UnprotectDocument%2A> método, ele salva o atual <xref:Microsoft.Office.Tools.Excel.Workbook.ProtectStructure%2A> e <xref:Microsoft.Office.Tools.Excel.Workbook.ProtectWindows%2A> valores, para que o mesmo tipo de proteção pode ser reaplicado no <xref:Microsoft.Office.Tools.Excel.WorkbookBase.ProtectDocument%2A> método.  
  
 [!code-vb[Trin_CachedDataProtectedWorkbook#1](../vsto/codesnippet/VisualBasic/Trin_CachedDataProtectedWorkbook/ThisWorkbook.vb#1)]
 [!code-csharp[Trin_CachedDataProtectedWorkbook#1](../vsto/codesnippet/CSharp/Trin_CachedDataProtectedWorkbook/ThisWorkbook.cs#1)]  
  
### <a name="compile-the-code"></a>Compilar o código  
 Adicione este código para o `ThisWorkbook` classe em seu projeto. Esse código supõe que a senha é armazenada em um campo chamado `securelyStoredPassword`.  
  
## <a name="see-also"></a>Consulte também  
 [Dados de cache](../vsto/caching-data.md)   
 [Como: armazenar em Cache dados para uso offline ou em um servidor](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)   
 [Como: armazenar em cache programaticamente uma fonte de dados em um documento do Office](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)  
  
  