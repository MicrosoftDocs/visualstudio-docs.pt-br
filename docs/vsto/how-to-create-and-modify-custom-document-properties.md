---
title: 'Como: criar e modificar propriedades de documento personalizadas'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom document properties
- documents [Office development in Visual Studio], properties
- document properties [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: bb66d2fbd1af41cfa89fc38f7694ee3783d10f76
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35254430"
---
# <a name="how-to-create-and-modify-custom-document-properties"></a>Como: criar e modificar propriedades de documento personalizadas
  Aplicativos do Microsoft Office listados acima fornecem propriedades internas são armazenadas com documentos. Além disso, você pode criar e modificar propriedades de documento personalizadas se há informações adicionais que você deseja armazenar no documento.  
  
 [!INCLUDE[appliesto_docprops](../vsto/includes/appliesto-docprops-md.md)]  
  
 Use a propriedade CustomDocumentProperties de um documento para trabalhar com propriedades personalizadas. Por exemplo, em um projeto de nível de documento do Microsoft Office Excel, use o <xref:Microsoft.Office.Tools.Excel.Workbook.CustomDocumentProperties%2A> propriedade do `ThisWorkbook` classe. Em um projeto do suplemento do VSTO para Excel, use o <xref:Microsoft.Office.Interop.Excel._Workbook.CustomDocumentProperties%2A> propriedade de um <xref:Microsoft.Office.Interop.Excel.Workbook> objeto. Essas propriedades retornam um <xref:Microsoft.Office.Core.DocumentProperties> objeto, que é uma coleção de <xref:Microsoft.Office.Core.DocumentProperty> objetos. Você pode usar o `Item` propriedade da coleção para recuperar uma propriedade específica, por nome ou índice dentro da coleção.  
  
 O exemplo a seguir demonstra como adicionar uma propriedade personalizada em uma personalização no nível de documento para Excel e atribua um valor.  
  
 ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [como eu faço para: acesso e manipular as propriedades de documento personalizadas no Microsoft Word?](http://go.microsoft.com/fwlink/?LinkId=136772).  
  
## <a name="example"></a>Exemplo  
 [!code-vb[Trin_VstcoreProgramming#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/ThisWorkbook.vb#6)]
 [!code-csharp[Trin_VstcoreProgramming#6](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/ThisWorkbook.cs#6)]  
  
## <a name="robust-programming"></a>Programação robusta  
 Tentativa de acesso a `Value` propriedade para propriedades indefinidas gera uma exceção.  
  
## <a name="see-also"></a>Consulte também  
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Personalizações em nível de documento do programa](../vsto/programming-document-level-customizations.md)   
 [Como: leitura de e gravação às propriedades do documento](../vsto/how-to-read-from-and-write-to-document-properties.md)  
  
  