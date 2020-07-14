---
title: 'Como: ler e gravar nas propriedades do documento'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], document properties
- documents [Office development in Visual Studio], properties
- document properties [Office development in Visual Studio]
- Excel [Office development in Visual Studio], document properties
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: adad9ec70290f426ce7c3c59ad13ff8636a69463
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541317"
---
# <a name="how-to-read-from-and-write-to-document-properties"></a>Como: ler e gravar nas propriedades do documento
  Você pode armazenar as propriedades do documento junto com um documento. Os aplicativos do Office fornecem várias propriedades internas, como autor, título e assunto. Este tópico mostra como definir propriedades de documento no Microsoft Office Excel e Microsoft Office Word.

 [!INCLUDE[appliesto_docprops](../vsto/includes/appliesto-docprops-md.md)]

## <a name="set-document-properties-in-excel"></a>Definir propriedades de documento no Excel
 Para trabalhar com propriedades internas no Excel, use as seguintes propriedades:

- Em um projeto de nível de documento, use a <xref:Microsoft.Office.Tools.Excel.Workbook.BuiltinDocumentProperties%2A> propriedade da `ThisWorkbook` classe.

- Em um projeto de suplemento do VSTO, use a <xref:Microsoft.Office.Interop.Excel._Workbook.BuiltinDocumentProperties%2A> propriedade de um <xref:Microsoft.Office.Interop.Excel.Workbook> objeto.

  Essas propriedades retornam um <xref:Microsoft.Office.Core.DocumentProperties> objeto, que é uma coleção de <xref:Microsoft.Office.Core.DocumentProperty> objetos. Você pode usar a `Item` propriedade da coleção para recuperar uma propriedade específica, seja por nome ou por índice dentro da coleção.

  O exemplo de código a seguir mostra como alterar a propriedade de **número de revisão** interna em um projeto de nível de documento.

### <a name="to-change-the-revision-number-property-in-excel"></a>Para alterar a propriedade número de revisão no Excel

1. Atribua as propriedades do documento interno a uma variável.

     [!code-vb[Trin_VstcoreProgramming#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/ThisWorkbook.vb#7)]
     [!code-csharp[Trin_VstcoreProgramming#7](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/ThisWorkbook.cs#7)]

2. Incrementar a `Revision Number` Propriedade por uma.

     [!code-vb[Trin_VstcoreProgramming#8](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/ThisWorkbook.vb#8)]
     [!code-csharp[Trin_VstcoreProgramming#8](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/ThisWorkbook.cs#8)]

## <a name="set-document-properties-in-word"></a>Definir propriedades de documento no Word
 Para trabalhar com propriedades internas no Word, use as seguintes propriedades:

- Em um projeto de nível de documento, use a <xref:Microsoft.Office.Tools.Word.Document.BuiltInDocumentProperties%2A> propriedade da `ThisDocument` classe.

- Em um projeto de suplemento do VSTO, use a <xref:Microsoft.Office.Interop.Word._Document.BuiltInDocumentProperties%2A> propriedade de um <xref:Microsoft.Office.Interop.Word.Document> objeto.

  Essas propriedades retornam um <xref:Microsoft.Office.Core.DocumentProperties> objeto, que é uma coleção de <xref:Microsoft.Office.Core.DocumentProperty> objetos. Você pode usar a `Item` propriedade da coleção para recuperar uma propriedade específica, seja por nome ou por índice dentro da coleção.

  O exemplo de código a seguir mostra como alterar a propriedade de **entidade** interna em um projeto de nível de documento.

### <a name="to-change-the-subject-property"></a>Para alterar a propriedade Subject

1. Atribua as propriedades do documento interno a uma variável.

     [!code-csharp[Trin_VstcoreProgrammingWord#1](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingWordCS/ThisDocument.cs#1)]
     [!code-vb[Trin_VstcoreProgrammingWord#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingWordVB/ThisDocument.vb#1)]

2. Altere a `Subject` propriedade para "White Paper".

     [!code-csharp[Trin_VstcoreProgrammingWord#2](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingWordCS/ThisDocument.cs#2)]
     [!code-vb[Trin_VstcoreProgrammingWord#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingWordVB/ThisDocument.vb#2)]

## <a name="robust-programming"></a>Programação robusta
 Os exemplos pressupõem que você escreveu o código na `ThisWorkbook` classe em um projeto de nível de documento para Excel e a `ThisDocument` classe em um projeto de nível de documento para o Word.

 Embora você esteja trabalhando com o Word e o Excel e seus objetos, Microsoft Office fornece a lista de propriedades de documento internas disponíveis. A tentativa de acessar uma propriedade indefinida gera uma exceção.

## <a name="see-also"></a>Consulte também
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
- [Programar personalizações em nível de documento](../vsto/programming-document-level-customizations.md)
- [Como: criar e modificar propriedades de documento personalizadas](../vsto/how-to-create-and-modify-custom-document-properties.md)
