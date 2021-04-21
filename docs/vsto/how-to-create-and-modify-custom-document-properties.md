---
title: 'Como: criar e modificar propriedades de documento personalizadas'
description: Saiba como você pode criar e modificar propriedades de documento personalizadas se houver informações adicionais que você deseja armazenar com o documento.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cd89cb1e2991f48fefd9984eaa6d5894d9b506c1
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826571"
---
# <a name="how-to-create-and-modify-custom-document-properties"></a>Como: criar e modificar propriedades de documento personalizadas
  Os aplicativos Microsoft Office listados acima fornecem propriedades internas que são armazenadas com documentos. Além disso, você pode criar e modificar propriedades de documento personalizadas se houver informações adicionais que você deseja armazenar com o documento.

 [!INCLUDE[appliesto_docprops](../vsto/includes/appliesto-docprops-md.md)]

 Use a propriedade CustomDocumentProperties de um documento para trabalhar com propriedades personalizadas. Por exemplo, em um projeto de nível de documento para Microsoft Office Excel, use a <xref:Microsoft.Office.Tools.Excel.Workbook.CustomDocumentProperties%2A> propriedade da `ThisWorkbook` classe. Em um projeto de suplemento do VSTO para Excel, use a <xref:Microsoft.Office.Interop.Excel._Workbook.CustomDocumentProperties%2A> propriedade de um <xref:Microsoft.Office.Interop.Excel.Workbook> objeto. Essas propriedades retornam um <xref:Microsoft.Office.Core.DocumentProperties> objeto, que é uma coleção de <xref:Microsoft.Office.Core.DocumentProperty> objetos. Você pode usar a `Item` propriedade da coleção para recuperar uma propriedade específica, seja por nome ou por índice dentro da coleção.

 O exemplo a seguir demonstra como adicionar uma propriedade personalizada em uma personalização no nível do documento para o Excel e atribuir um valor a ela.

## <a name="example"></a>Exemplo
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/ThisWorkbook.vb" id="Snippet6":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/ThisWorkbook.cs" id="Snippet6":::

## <a name="robust-programming"></a>Programação robusta
 A tentativa de acessar a `Value` propriedade para propriedades indefinidas gera uma exceção.

## <a name="see-also"></a>Consulte também
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
- [Programar personalizações em nível de documento](../vsto/programming-document-level-customizations.md)
- [Como: ler e gravar nas propriedades do documento](../vsto/how-to-read-from-and-write-to-document-properties.md)
