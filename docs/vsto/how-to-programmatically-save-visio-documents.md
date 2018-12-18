---
title: 'Como: salvar documentos do Visio programaticamente'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], saving Visio documents
- Visio [Office development in Visual Studio], saving Visio documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: a9f065a32fc26d372b97a31eb70836451b31fa00
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50670722"
---
# <a name="how-to-programmatically-save-visio-documents"></a>Como: salvar documentos do Visio programaticamente
  Há várias maneiras de salvar documentos do Microsoft Office Visio:  
  
- Salve alterações em um documento existente.  
  
- Salvar um novo documento, ou salvar um documento com um novo nome.  
  
- Salve um documento com os argumentos especificados.  
  
  Para obter mais informações, consulte a documentação de referência do VBA para o [Microsoft.Office.Interop.Visio.Document.Save](/office/vba/api/Visio.Document.Save) método, [Microsoft.Office.Interop.Visio.Document.SaveAs](/office/vba/api/Visio.Document.SaveAs) emétodo[ Microsoft.Office.Interop.Visio.Document.SaveAsEx](/office/vba/api/Visio.Document.SaveAsEx) método.  
  
## <a name="save-an-existing-document"></a>Salvar um documento existente  
  
### <a name="to-save-a-document"></a>Para salvar um documento  
  
-   Chame o `Microsoft.Office.Interop.Visio.Document.Save` método da `Microsoft.Office.Tools.Visio.Document` classe de um documento que foi salvo anteriormente.  
  
     Para usar este exemplo de código, executá-la na `ThisAddIn` classe em seu projeto.  
  
    > [!NOTE]  
    >  O `Microsoft.Office.Interop.Visio.Document.Save` método lança uma exceção se um novo documento do Visio ainda não foi salvo.  
  
     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#11](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#11)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#11](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#11)]  
  
## <a name="save-a-document-with-a-new-name"></a>Salvar um documento com um novo nome  
 Use o `Microsoft.Office.Interop.Visio.Document.SaveAs` método para salvar um novo documento ou um documento que tem um novo nome. Esse método requer que você especifique o novo nome de arquivo.  
  
### <a name="to-save-the-active-visio-document-with-a-new-name"></a>Para salvar o documento ativo do Visio com um novo nome  
  
-   Chame o `Microsoft.Office.Interop.Visio.Document.SaveAs` método da `Microsoft.Office.Tools.Visio.Document` que você deseja salvar, usando um caminho totalmente qualificado, incluindo um nome de arquivo. Se um arquivo com esse nome já existe nessa pasta, ele será substituído silenciosamente.  
  
     Para usar este exemplo de código, executá-la na `ThisAddIn` classe em seu projeto.  
  
     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#10](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#10)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#10](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#10)]  
  
## <a name="save-a-document-with-a-new-name-and-specified-arguments"></a>Salvar um documento com um novo nome e os argumentos especificados  
 Use o `Microsoft.Office.Interop.Visio.Document.SaveAsEx` método para salvar um documento com um novo nome e especifique quaisquer argumentos aplicáveis para aplicar ao documento.  
  
### <a name="to-save-document-with-a-new-name-and-specified-arguments"></a>Para salvar o documento com um novo nome e os argumentos especificados  
  
-   Chame o `Microsoft.Office.Interop.Visio.Document.SaveAsEx` método da `Microsoft.Office.Tools.Visio.Document` que você deseja salvar, usando um caminho totalmente qualificado, incluindo um nome de arquivo. Se um arquivo com esse nome já existe nessa pasta, uma exceção é lançada.  
  
     O exemplo de código a seguir salva o documento ativo com um novo nome, marca o documento como somente leitura e mostra o documento na lista de documentos usados recentemente. Para usar este exemplo de código, executá-la na `ThisAddIn` classe em seu projeto.  
  
     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#12](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#12)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#12](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#12)]  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo de código requer o seguinte:  
  
-   Para salvar um documento que tem um novo nome, um diretório chamado `Test` devem estar localizados em de *Meus documentos* pasta (para o Windows XP e versões anteriores) ou o *documentos* pasta (para Windows Vista).  
  
## <a name="see-also"></a>Consulte também  
 [Soluções do Visio](../vsto/visio-solutions.md)   
 [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)   
 [Como: criar novos documentos do Visio programaticamente](../vsto/how-to-programmatically-create-new-visio-documents.md)   
 [Como: abrir documentos do Visio de forma programática](../vsto/how-to-programmatically-open-visio-documents.md)   
 [Como: fechar documentos do Visio programaticamente](../vsto/how-to-programmatically-close-visio-documents.md)   
 [Como: imprimir documentos do Visio de forma programática](../vsto/how-to-programmatically-print-visio-documents.md)  
  
  