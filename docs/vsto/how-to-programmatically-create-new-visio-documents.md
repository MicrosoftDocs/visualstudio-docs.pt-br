---
title: 'Como: criar novos documentos do Visio programaticamente'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visio [Office development in Visual Studio], creating Visio documents
- documents [Office development in Visual Studio], creating Visio documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 4142ebe86ea69fbb0a74f25c2a7053a60c527cdb
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671554"
---
# <a name="how-to-programmatically-create-new-visio-documents"></a>Como: criar novos documentos do Visio programaticamente
  Quando você cria um novo Microsoft Office Visio desenhando o documento, você adicioná-lo para o `Microsoft.Office.Interop.Visio.Documents` coleção de documentos do Visio abertos. Consequentemente, o `Microsoft.Office.Interop.Visio.Documents.Add` método cria um novo documento de desenho do Visio. Para obter mais informações, consulte a documentação de referência do VBA para o [Microsoft.Office.Interop.Visio.Documents.Add](/office/vba/api/Visio.Documents.Add) método.  
  
## <a name="create-new-blank-documents"></a>Criar novos documentos em branco  
  
### <a name="to-create-a-new-document"></a>Para criar um novo documento  
  
-   Use o `Microsoft.Office.Interop.Visio.Documents.Add` método para criar um novo documento em branco que não se baseia em um modelo.  
  
     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#1](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#1)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#1](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#1)]  
  
## <a name="create-documents-copied-from-existing-documents"></a>Criar documentos copiados de documentos existentes  
 O `Microsoft.Office.Interop.Visio.Documents.Add` método pode criar um novo documento que é uma cópia de um documento existente do Visio. Você deve fornecer o nome do arquivo e o caminho totalmente qualificado do diagrama.  
  
### <a name="to-create-a-new-document-that-is-copied-from-an-existing-document"></a>Para criar um novo documento que é copiado de um documento existente  
  
-   Chamar o `Microsoft.Office.Interop.Visio.Documents.Add` método e especifique o caminho do diagrama do Visio.  
  
     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#2](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#2)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#2](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#2)]  
  
## <a name="create-stencils-copied-from-existing-stencils"></a>Criar estênceis copiados de estênceis existentes  
 O [Microsoft.Office.Interop.Visio.Documents.Add](/office/vba/api/Visio.Documents.Add) método pode criar um novo estêncil é uma cópia de um estêncil do Visio existente. Você deve fornecer o nome do arquivo e o caminho totalmente qualificado do estêncil.  
  
### <a name="to-create-a-new-stencil-that-is-copied-from-an-existing-stencil"></a>Para criar um novo estêncil que é copiado de um estêncil existente  
  
-   Chamar o `Microsoft.Office.Interop.Visio.Documents.Add` método e especifique o caminho do estêncil.  
  
     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#3](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#3)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#3](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#3)]  
  
## <a name="create-documents-based-on-existing-templates"></a>Criar documentos com base em modelos existentes  
 O `Microsoft.Office.Interop.Visio.Documents.Add` método pode criar um novo documento (um *. vsd* arquivo) que se baseia em um modelo existente do Visio (um *. vst* arquivo). Esse método copia os estênceis, estilos e configurações que fazem parte do espaço de trabalho modelo. Você deve fornecer o nome de arquivo e o caminho totalmente qualificado do modelo.  
  
### <a name="to-create-a-new-document-that-is-based-on-an-existing-template"></a>Para criar um novo documento com base em um modelo existente  
  
-   Chamar o `Microsoft.Office.Interop.Visio.Documents.Add` método e especifique o caminho do modelo.  
  
     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#4](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#4)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#4](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#4)]  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo de código requer o seguinte:  
  
-   Um documento do Visio chamado `myDrawing.vsd` devem estar localizados em um diretório chamado `Test` na *Meus documentos* pasta (para o Windows XP e versões anteriores) ou o *documentos* pasta (para Windows Vista).  
  
-   Um documento do Visio chamado `myStencil.vss` devem estar localizados em um diretório chamado `Test` na *Meus documentos* pasta (para o Windows XP e versões anteriores) ou o *documentos* pasta (para Windows Vista).  
  
-   Um documento do Visio chamado `myTemplate.vst` devem estar localizados em um diretório chamado `Test` na *Meus documentos* pasta (para o Windows XP e versões anteriores) ou o *documentos* pasta (para Windows Vista).  
  
## <a name="see-also"></a>Consulte também  
 [Soluções do Visio](../vsto/visio-solutions.md)   
 [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)   
 [Como: abrir documentos do Visio de forma programática](../vsto/how-to-programmatically-open-visio-documents.md)   
 [Como: fechar documentos do Visio programaticamente](../vsto/how-to-programmatically-close-visio-documents.md)   
 [Como: salvar documentos do Visio programaticamente](../vsto/how-to-programmatically-save-visio-documents.md)   
 [Como: imprimir documentos do Visio de forma programática](../vsto/how-to-programmatically-print-visio-documents.md)  
  
  