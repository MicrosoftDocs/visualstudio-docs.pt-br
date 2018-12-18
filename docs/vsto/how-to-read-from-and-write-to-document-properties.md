---
title: 'Como: leitura de e gravação às propriedades do documento'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], document properties
- documents [Office development in Visual Studio], properties
- document properties [Office development in Visual Studio]
- Excel [Office development in Visual Studio], document properties
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: de9ae85156f9d272901893c74c5d2c9729a0a3dd
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49924220"
---
# <a name="how-to-read-from-and-write-to-document-properties"></a>Como: leitura de e gravação às propriedades do documento
  Você pode armazenar as propriedades do documento, juntamente com um documento. Aplicativos do Office fornecem uma série de propriedades internas, como autor, título e assunto. Este tópico mostra como definir propriedades de documento no Microsoft Office Excel e Microsoft Office Word.  
  
 ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [como eu faço para: acesso e manipular as propriedades de documento personalizadas no Microsoft Word?](http://go.microsoft.com/fwlink/?LinkId=136772).  
  
 [!INCLUDE[appliesto_docprops](../vsto/includes/appliesto-docprops-md.md)]  
  
## <a name="set-document-properties-in-excel"></a>Definir propriedades de documento no Excel  
 Para trabalhar com propriedades internas no Excel, use as seguintes propriedades:  
  
- Em um projeto de nível de documento, use o <xref:Microsoft.Office.Tools.Excel.Workbook.BuiltinDocumentProperties%2A> propriedade do `ThisWorkbook` classe.  
  
- Em um projeto de suplemento do VSTO, use o <xref:Microsoft.Office.Interop.Excel._Workbook.BuiltinDocumentProperties%2A> propriedade de um <xref:Microsoft.Office.Interop.Excel.Workbook> objeto.  
  
  Essas propriedades retornam um <xref:Microsoft.Office.Core.DocumentProperties> objeto, que é uma coleção de <xref:Microsoft.Office.Core.DocumentProperty> objetos. Você pode usar o `Item` propriedade da coleção para recuperar uma propriedade específica, por nome ou índice dentro da coleção.  
  
  O exemplo de código a seguir mostra como alterar o interno **número de revisão** propriedade em um projeto de nível de documento.  
  
### <a name="to-change-the-revision-number-property-in-excel"></a>Para alterar a propriedade de número de revisão no Excel  
  
1.  Atribua propriedades internas do documento a uma variável.  
  
     [!code-vb[Trin_VstcoreProgramming#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/ThisWorkbook.vb#7)]
     [!code-csharp[Trin_VstcoreProgramming#7](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/ThisWorkbook.cs#7)]  
  
2.  Incremento de `Revision Number` propriedade por um.  
  
     [!code-vb[Trin_VstcoreProgramming#8](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/ThisWorkbook.vb#8)]
     [!code-csharp[Trin_VstcoreProgramming#8](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/ThisWorkbook.cs#8)]  
  
## <a name="set-document-properties-in-word"></a>Definir propriedades de documento no Word  
 Para trabalhar com propriedades internas no Word, use as seguintes propriedades:  
  
- Em um projeto de nível de documento, use o <xref:Microsoft.Office.Tools.Word.Document.BuiltInDocumentProperties%2A> propriedade do `ThisDocument` classe.  
  
- Em um projeto de suplemento do VSTO, use o <xref:Microsoft.Office.Interop.Word._Document.BuiltInDocumentProperties%2A> propriedade de um <xref:Microsoft.Office.Interop.Word.Document> objeto.  
  
  Essas propriedades retornam um <xref:Microsoft.Office.Core.DocumentProperties> objeto, que é uma coleção de <xref:Microsoft.Office.Core.DocumentProperty> objetos. Você pode usar o `Item` propriedade da coleção para recuperar uma propriedade específica, por nome ou índice dentro da coleção.  
  
  O exemplo de código a seguir mostra como alterar o interno **assunto** propriedade em um projeto de nível de documento.  
  
### <a name="to-change-the-subject-property"></a>Para alterar a propriedade Subject  
  
1.  Atribua propriedades internas do documento a uma variável.  
  
     [!code-csharp[Trin_VstcoreProgrammingWord#1](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingWordCS/ThisDocument.cs#1)]
     [!code-vb[Trin_VstcoreProgrammingWord#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingWordVB/ThisDocument.vb#1)]  
  
2.  Alterar o `Subject` propriedade como "White paper".  
  
     [!code-csharp[Trin_VstcoreProgrammingWord#2](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingWordCS/ThisDocument.cs#2)]
     [!code-vb[Trin_VstcoreProgrammingWord#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingWordVB/ThisDocument.vb#2)]  
  
## <a name="robust-programming"></a>Programação robusta  
 Os exemplos pressupõem que você tenha escrito o código `ThisWorkbook` classe em um projeto de nível de documento para Excel e o `ThisDocument` classe em um projeto de nível de documento para Word.  
  
 Embora você estiver trabalhando com o Word e Excel e seus objetos, o Microsoft Office fornece a lista de propriedades do documento internas disponíveis. A tentativa de acessar uma propriedade indefinida gerará uma exceção.  
  
## <a name="see-also"></a>Consulte também  
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Personalizações em nível de documento do programa](../vsto/programming-document-level-customizations.md)   
 [Como: criar e modificar propriedades de documento personalizadas](../vsto/how-to-create-and-modify-custom-document-properties.md)  
  
  