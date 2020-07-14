---
title: Adicionar partes XML personalizadas a documentos usando suplementos do VSTO
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], custom XML parts
- Office documents [Office development in Visual Studio, custom XML parts
- Word [Office development in Visual Studio], custom XML parts
- PowerPoint [Office development in Visual Studio], custom XML parts
- Excel [Office development in Visual Studio], custom XML parts
- custom XML parts [Office development in Visual Studio], adding
- documents [Office development in Visual Studio], custom XML parts
- application-level add-ins [Office development in Visual Studio], custom XML parts
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 92c00ea69069b7374f5f595cc6f198aac23d1f91
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538288"
---
# <a name="how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins"></a>Como: adicionar partes XML personalizadas a documentos usando suplementos do VSTO
  Você pode armazenar dados XML nos seguintes tipos de documentos criando uma parte XML personalizada em um suplemento do VSTO:

- Uma Microsoft Office pasta de trabalho do Excel.

- Um Microsoft Office documento do Word.

- Uma apresentação Microsoft Office PowerPoint.

  Para obter mais informações, consulte [visão geral de partes XML personalizadas](../vsto/custom-xml-parts-overview.md).

  **Aplica-se a:** As informações neste tópico se aplicam a projetos de nível de aplicativo para Excel, PowerPoint e Word. Para obter mais informações, consulte [recursos disponíveis por aplicativo do Office e tipo de projeto](../vsto/features-available-by-office-application-and-project-type.md).

## <a name="to-add-a-custom-xml-part-to-an-excel-workbook"></a>Para adicionar uma parte XML personalizada a uma pasta de trabalho do Excel

1. Adicione um novo <xref:Microsoft.Office.Core.CustomXMLPart> objeto à <xref:Microsoft.Office.Interop.Excel._Workbook.CustomXMLParts%2A> coleção na pasta de trabalho. O <xref:Microsoft.Office.Core.CustomXMLPart> contém a cadeia de caracteres XML que você deseja armazenar na pasta de trabalho.

     O exemplo de código a seguir adiciona uma parte XML personalizada a uma pasta de trabalho especificada.

     [!code-vb[Trin_AddCustomXmlPartExcelAppLevel#1](../vsto/codesnippet/VisualBasic/trin_addcustomxmlpartexcelapplevel/ThisAddIn.vb#1)]
     [!code-csharp[Trin_AddCustomXmlPartExcelAppLevel#1](../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartExcelAppLevel/ThisAddIn.cs#1)]

2. Adicione o `AddCustomXmlPartToWorkbook` método à `ThisAddIn` classe em um projeto de suplemento do VSTO para Excel.

3. Chame o método de outro código em seu projeto. Por exemplo, para criar a parte XML personalizada quando o usuário abre uma pasta de trabalho, chame o método de um manipulador de eventos para o <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookOpen> evento.

## <a name="to-add-a-custom-xml-part-to-a-word-document"></a>Para adicionar uma parte XML personalizada a um documento do Word

1. Adicione um novo <xref:Microsoft.Office.Core.CustomXMLPart> objeto à <xref:Microsoft.Office.Interop.Word._Document.CustomXMLParts%2A> coleção no documento. O <xref:Microsoft.Office.Core.CustomXMLPart> contém a cadeia de caracteres XML que você deseja armazenar no documento.

     O exemplo de código a seguir adiciona uma parte XML personalizada a um documento especificado.

     [!code-vb[Trin_AddCustomXmlPartWordAppLevel#1](../vsto/codesnippet/VisualBasic/Trin_AddCustomXmlPartWordAppLevel/ThisAddIn.vb#1)]
     [!code-csharp[Trin_AddCustomXmlPartWordAppLevel#1](../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartWordAppLevel/ThisAddIn.cs#1)]

2. Adicione o `AddCustomXmlPartToDocument` método à `ThisAddIn` classe em um projeto de suplemento do VSTO para Word.

3. Chame o método de outro código em seu projeto. Por exemplo, para criar a parte XML personalizada quando o usuário abre um documento, chame o método de um manipulador de eventos para o <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> evento.

## <a name="to-add-a-custom-xml-part-to-a-powerpoint-presentation"></a>Para adicionar uma parte XML personalizada a uma apresentação do PowerPoint

1. Adicione um novo <xref:Microsoft.Office.Core.CustomXMLPart> objeto à coleção [Microsoft. Office. Interop. PowerPoint. _Presentation. CustomXMLParts](/previous-versions/office/developer/office-2010/ff760806%28v%3doffice.14%29) na apresentação. O <xref:Microsoft.Office.Core.CustomXMLPart> contém a cadeia de caracteres XML que você deseja armazenar na apresentação.

     O exemplo de código a seguir adiciona uma parte XML personalizada a uma apresentação especificada.

     [!code-csharp[Trin_AddCustomXmlPartPowerPointAppLevel#1](../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartPowerPointAppLevel/ThisAddIn.cs#1)]
     [!code-vb[Trin_AddCustomXmlPartPowerPointAppLevel#1](../vsto/codesnippet/VisualBasic/Trin_AddCustomXmlPartPowerPointAppLevel/ThisAddIn.vb#1)]

2. Adicione o `AddCustomXmlPartToPresentation` método à `ThisAddIn` classe em um projeto de suplemento do VSTO para PowerPoint.

3. Chame o método de outro código em seu projeto. Por exemplo, para criar a parte XML personalizada quando o usuário abre uma apresentação, chame o método de um manipulador de eventos para o evento [Microsoft. Office. Interop. PowerPoint. EApplication_Event. AfterPresentationOpen](/previous-versions/office/developer/office-2010/ff762843(v=office.14)) .

## <a name="robust-programming"></a>Programação robusta
 Para simplificar, este exemplo usa uma cadeia de caracteres XML que é definida como uma variável local no método. Normalmente, você deve obter o XML de uma fonte externa, como um arquivo ou um banco de dados.

## <a name="see-also"></a>Consulte também
- [Visão geral das partes XML personalizadas](../vsto/custom-xml-parts-overview.md)
- [Como: adicionar partes XML personalizadas a personalizações em nível de documento](../vsto/how-to-add-custom-xml-parts-to-document-level-customizations.md)
