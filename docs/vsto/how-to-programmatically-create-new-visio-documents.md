---
title: Como criar programaticamente novos documentos do Visio
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visio [Office development in Visual Studio], creating Visio documents
- documents [Office development in Visual Studio], creating Visio documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 171ad93caf6b5c13d000073a0d7f7e82282b9b4a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541525"
---
# <a name="how-to-programmatically-create-new-visio-documents"></a>Como criar programaticamente novos documentos do Visio
  Ao criar um novo documento de desenho Microsoft Office do Visio, você o adiciona à `Microsoft.Office.Interop.Visio.Documents` coleção de documentos abertos do Visio. Consequentemente, o `Microsoft.Office.Interop.Visio.Documents.Add` método cria um novo documento de desenho do Visio. Para obter mais informações, consulte a documentação de referência do VBA para o [Microsoft.Office.Interop.Visio.Documents. Adicionar](/office/vba/api/Visio.Documents.Add) método.

## <a name="create-new-blank-documents"></a>Criar novos documentos em branco

### <a name="to-create-a-new-document"></a>Para criar um novo documento

- Use o `Microsoft.Office.Interop.Visio.Documents.Add` método para criar um novo documento em branco que não seja baseado em um modelo.

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#1](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#1)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#1](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#1)]

## <a name="create-documents-copied-from-existing-documents"></a>Criar documentos copiados de documentos existentes
 O `Microsoft.Office.Interop.Visio.Documents.Add` método pode criar um novo documento que seja uma cópia de um documento existente do Visio. Você deve fornecer o nome do arquivo e o caminho totalmente qualificado do diagrama.

### <a name="to-create-a-new-document-that-is-copied-from-an-existing-document"></a>Para criar um novo documento que é copiado de um documento existente

- Chame o `Microsoft.Office.Interop.Visio.Documents.Add` método e especifique o caminho do diagrama do Visio.

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#2](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#2)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#2](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#2)]

## <a name="create-stencils-copied-from-existing-stencils"></a>Criar estênceis copiados de estênceis existentes
 O [Microsoft.Office.Interop.Visio.Documents. ](/office/vba/api/Visio.Documents.Add)O método Add pode criar um novo estêncil que é uma cópia de um estêncil existente do Visio. Você deve fornecer o nome do arquivo e o caminho totalmente qualificado do estêncil.

### <a name="to-create-a-new-stencil-that-is-copied-from-an-existing-stencil"></a>Para criar um novo estêncil que é copiado de um estêncil existente

- Chame o `Microsoft.Office.Interop.Visio.Documents.Add` método e especifique o caminho do estêncil.

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#3](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#3)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#3](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#3)]

## <a name="create-documents-based-on-existing-templates"></a>Criar documentos com base em modelos existentes
 O `Microsoft.Office.Interop.Visio.Documents.Add` método pode criar um novo documento (um arquivo *. vsd* ) baseado em um modelo existente do Visio (um arquivo *. VST* ). Esse método copia os estênceis, estilos e configurações que fazem parte do espaço de trabalho de modelo. Você deve fornecer o nome do arquivo e o caminho totalmente qualificado do modelo.

### <a name="to-create-a-new-document-that-is-based-on-an-existing-template"></a>Para criar um novo documento baseado em um modelo existente

- Chame o `Microsoft.Office.Interop.Visio.Documents.Add` método e especifique o caminho do modelo.

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#4](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#4)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#4](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#4)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo de código requer o seguinte:

- Um documento do Visio chamado `myDrawing.vsd` deve estar localizado em um diretório chamado `Test` na pasta *meus documentos* (para o Windows XP e versões anteriores) ou a pasta *documentos* (para o Windows Vista).

- Um documento do Visio chamado `myStencil.vss` deve estar localizado em um diretório chamado `Test` na pasta *meus documentos* (para o Windows XP e versões anteriores) ou a pasta *documentos* (para o Windows Vista).

- Um documento do Visio chamado `myTemplate.vst` deve estar localizado em um diretório chamado `Test` na pasta *meus documentos* (para o Windows XP e versões anteriores) ou a pasta *documentos* (para o Windows Vista).

## <a name="see-also"></a>Confira também
- [Soluções do Visio](../vsto/visio-solutions.md)
- [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)
- [Como: abrir documentos do Visio programaticamente](../vsto/how-to-programmatically-open-visio-documents.md)
- [Como: fechar documentos do Visio por meio de programação](../vsto/how-to-programmatically-close-visio-documents.md)
- [Como: salvar documentos do Visio programaticamente](../vsto/how-to-programmatically-save-visio-documents.md)
- [Como: imprimir documentos do Visio programaticamente](../vsto/how-to-programmatically-print-visio-documents.md)
