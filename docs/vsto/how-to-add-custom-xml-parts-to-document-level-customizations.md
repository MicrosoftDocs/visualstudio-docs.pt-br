---
title: 'Como: adicionar partes XML personalizadas a personalizações no nível do documento'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- document-level customizations [Office development in Visual Studio], custom XML parts
- Office documents [Office development in Visual Studio, custom XML parts
- Word [Office development in Visual Studio], custom XML parts
- Excel [Office development in Visual Studio], custom XML parts
- custom XML parts [Office development in Visual Studio], adding
- documents [Office development in Visual Studio], custom XML parts
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 0472ad001dee595f1f8edb77d7a70f1eefb0c024
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50744854"
---
# <a name="how-to-add-custom-xml-parts-to-document-level-customizations"></a>Como: adicionar partes XML personalizadas a personalizações no nível do documento
  Você pode armazenar dados XML em uma pasta de trabalho do Microsoft Office Excel ou um documento do Microsoft Office Word, criando uma parte XML personalizada em uma personalização no nível de documento. Para obter mais informações, consulte [visão geral de partes XML personalizadas](../vsto/custom-xml-parts-overview.md).  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
> [!NOTE]  
>  Visual Studio não fornece os projetos de nível de documento para o Microsoft Office PowerPoint. Para obter informações sobre como adicionar uma parte XML personalizada a uma apresentação do PowerPoint usando um suplemento do VSTO, consulte [como: adicionar partes XML personalizadas aos documentos usando suplementos VSTO](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md).  
  
### <a name="to-add-a-custom-xml-part-to-an-excel-workbook"></a>Para adicionar uma parte XML personalizada a uma pasta de trabalho do Excel  
  
1.  Adicione um novo <xref:Microsoft.Office.Core.CustomXMLPart> do objeto para o <xref:Microsoft.Office.Core.CustomXMLParts> coleção na pasta de trabalho. O <xref:Microsoft.Office.Core.CustomXMLPart> contém a cadeia de caracteres XML que você deseja armazenar na pasta de trabalho.  
  
     [!code-csharp[Trin_AddCustomXmlPartExcelDocLevel#1](../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartExcelDocLevel/ThisWorkbook.cs#1)]
     [!code-vb[Trin_AddCustomXmlPartExcelDocLevel#1](../vsto/codesnippet/VisualBasic/Trin_AddCustomXmlPartExcelDocLevel/ThisWorkbook.vb#1)]  
  
2.  Adicione a `AddCustomXmlPartToWorkbook` método para o `ThisWorkbook` classe em um projeto de nível de documento para Excel.  
  
3.  Chame o método de outro código no seu projeto. Por exemplo, para criar a parte XML personalizada quando o usuário abre a pasta de trabalho, chame o método da `ThisWorkbook_Startup` manipulador de eventos.  
  
### <a name="to-add-a-custom-xml-part-to-a-word-document"></a>Para adicionar uma parte XML personalizada a um documento do Word  
  
1.  Adicione um novo <xref:Microsoft.Office.Core.CustomXMLPart> do objeto para o <xref:Microsoft.Office.Core.CustomXMLParts> coleta no documento. O <xref:Microsoft.Office.Core.CustomXMLPart> contém a cadeia de caracteres XML que você deseja armazenar no documento.  
  
     [!code-vb[Trin_AddCustomXmlPartWordDocLevel#1](../vsto/codesnippet/VisualBasic/Trin_AddCustomXmlPartWordDocLevel/ThisDocument.vb#1)]
     [!code-csharp[Trin_AddCustomXmlPartWordDocLevel#1](../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartWordDocLevel/ThisDocument.cs#1)]  
  
2.  Adicione a `AddCustomXmlPartToDocument` método para o `ThisDocument` classe em um projeto de nível de documento para Word.  
  
3.  Chame o método de outro código no seu projeto. Por exemplo, para criar a parte XML personalizada quando o usuário abre o documento, chame o método da `ThisDocument_Startup` manipulador de eventos.  
  
## <a name="robust-programming"></a>Programação robusta  
 Para simplificar, este exemplo usa uma cadeia de caracteres XML que é definida como uma variável local no método. Normalmente, você deverá obter o XML de uma fonte externa, como um arquivo ou um banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de partes XML personalizado](../vsto/custom-xml-parts-overview.md)   
 [Como: adicionar partes XML personalizadas aos documentos usando suplementos VSTO](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md)  
  