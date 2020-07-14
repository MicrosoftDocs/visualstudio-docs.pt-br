---
title: 'Como: criar e modificar propriedades de documento personalizadas'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom document properties
- documents [Office development in Visual Studio], properties
- document properties [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6dd4f4ada36be4ef7b70f4f32d659abb10c8a62a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547206"
---
# <a name="how-to-create-and-modify-custom-document-properties"></a>Como: criar e modificar propriedades de documento personalizadas
  Os aplicativos Microsoft Office listados acima fornecem propriedades internas que são armazenadas com documentos. Além disso, você pode criar e modificar propriedades de documento personalizadas se houver informações adicionais que você deseja armazenar com o documento.

 [!INCLUDE[appliesto_docprops](../vsto/includes/appliesto-docprops-md.md)]

 Use a propriedade CustomDocumentProperties de um documento para trabalhar com propriedades personalizadas. Por exemplo, em um projeto de nível de documento para Microsoft Office Excel, use a <xref:Microsoft.Office.Tools.Excel.Workbook.CustomDocumentProperties%2A> propriedade da `ThisWorkbook` classe. Em um projeto de suplemento do VSTO para Excel, use a <xref:Microsoft.Office.Interop.Excel._Workbook.CustomDocumentProperties%2A> propriedade de um <xref:Microsoft.Office.Interop.Excel.Workbook> objeto. Essas propriedades retornam um <xref:Microsoft.Office.Core.DocumentProperties> objeto, que é uma coleção de <xref:Microsoft.Office.Core.DocumentProperty> objetos. Você pode usar a `Item` propriedade da coleção para recuperar uma propriedade específica, seja por nome ou por índice dentro da coleção.

 O exemplo a seguir demonstra como adicionar uma propriedade personalizada em uma personalização no nível do documento para o Excel e atribuir um valor a ela.

## <a name="example"></a>Exemplo
 [!code-vb[Trin_VstcoreProgramming#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/ThisWorkbook.vb#6)]
 [!code-csharp[Trin_VstcoreProgramming#6](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/ThisWorkbook.cs#6)]

## <a name="robust-programming"></a>Programação robusta
 A tentativa de acessar a `Value` propriedade para propriedades indefinidas gera uma exceção.

## <a name="see-also"></a>Confira também
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
- [Programar personalizações em nível de documento](../vsto/programming-document-level-customizations.md)
- [Como: ler e gravar nas propriedades do documento](../vsto/how-to-read-from-and-write-to-document-properties.md)
