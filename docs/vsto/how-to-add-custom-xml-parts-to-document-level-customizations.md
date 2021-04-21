---
title: 'Como: adicionar partes XML personalizadas a personalizações em nível de documento'
description: Saiba como você pode armazenar dados XML em uma Microsoft Office pasta de trabalho do Excel ou Microsoft Office documento do Word criando uma parte XML personalizada em uma personalização no nível do documento.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
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
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 99374a2daded3c4b49b60053a69cd1ff7c4dffe8
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827676"
---
# <a name="how-to-add-custom-xml-parts-to-document-level-customizations"></a>Como: adicionar partes XML personalizadas a personalizações em nível de documento
  Você pode armazenar dados XML em uma Microsoft Office pasta de trabalho do Excel ou Microsoft Office documento do Word criando uma parte XML personalizada em uma personalização no nível do documento. Para obter mais informações, consulte [visão geral de partes XML personalizadas](../vsto/custom-xml-parts-overview.md).

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

> [!NOTE]
> O Visual Studio não fornece projetos de nível de documento para Microsoft Office PowerPoint. Para obter informações sobre como adicionar uma parte XML personalizada a uma apresentação do PowerPoint usando um suplemento do VSTO, consulte [como: adicionar partes XML personalizadas a documentos usando suplementos do VSTO](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md).

### <a name="to-add-a-custom-xml-part-to-an-excel-workbook"></a>Para adicionar uma parte XML personalizada a uma pasta de trabalho do Excel

1. Adicione um novo <xref:Microsoft.Office.Core.CustomXMLPart> objeto à <xref:Microsoft.Office.Core.CustomXMLParts> coleção na pasta de trabalho. O <xref:Microsoft.Office.Core.CustomXMLPart> contém a cadeia de caracteres XML que você deseja armazenar na pasta de trabalho.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartExcelDocLevel/ThisWorkbook.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddCustomXmlPartExcelDocLevel/ThisWorkbook.vb" id="Snippet1":::

2. Adicione o `AddCustomXmlPartToWorkbook` método à `ThisWorkbook` classe em um projeto de nível de documento para o Excel.

3. Chame o método de outro código em seu projeto. Por exemplo, para criar a parte XML personalizada quando o usuário abrir a pasta de trabalho, chame o método do `ThisWorkbook_Startup` manipulador de eventos.

### <a name="to-add-a-custom-xml-part-to-a-word-document"></a>Para adicionar uma parte XML personalizada a um documento do Word

1. Adicione um novo <xref:Microsoft.Office.Core.CustomXMLPart> objeto à <xref:Microsoft.Office.Core.CustomXMLParts> coleção no documento. O <xref:Microsoft.Office.Core.CustomXMLPart> contém a cadeia de caracteres XML que você deseja armazenar no documento.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddCustomXmlPartWordDocLevel/ThisDocument.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartWordDocLevel/ThisDocument.cs" id="Snippet1":::

2. Adicione o `AddCustomXmlPartToDocument` método à `ThisDocument` classe em um projeto de nível de documento para o Word.

3. Chame o método de outro código em seu projeto. Por exemplo, para criar a parte XML personalizada quando o usuário abrir o documento, chame o método do `ThisDocument_Startup` manipulador de eventos.

## <a name="robust-programming"></a>Programação robusta
 Para simplificar, este exemplo usa uma cadeia de caracteres XML que é definida como uma variável local no método. Normalmente, você deve obter o XML de uma fonte externa, como um arquivo ou um banco de dados.

## <a name="see-also"></a>Consulte também
- [Visão geral das partes XML personalizadas](../vsto/custom-xml-parts-overview.md)
- [Como: adicionar partes XML personalizadas a documentos usando suplementos do VSTO](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md)
