---
title: Adicionar imagens e palavras-chave a documentos de forma programática
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], adding pictures
- Word documents, adding pictures
- Word documents, adding Word Art
- graphics, adding to Word documents
- WordArt, adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 621051c827b08e66d68bc348401c2a939e279bcf
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538080"
---
# <a name="how-to-programmatically-add-pictures-and-word-art-to-documents"></a>Como: adicionar imagens e arte de palavras programaticamente a documentos
  Você pode adicionar imagens e objetos de desenho a seus documentos em tempo de design ou durante o tempo de execução. O WordArt permite que você adicione texto decorativo a Microsoft Office documentos do Word. Esses efeitos de texto especiais são objetos de desenho que você pode personalizar e inserir em seu documento.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="add-a-picture-at-design-time"></a>Adicionar uma imagem em tempo de design
 Se você estiver desenvolvendo uma personalização em nível de documento, poderá adicionar uma imagem ao documento em tempo de design.

### <a name="to-add-a-picture-to-a-word-document-at-design-time"></a>Para adicionar uma imagem a um documento do Word em tempo de design

1. Coloque o cursor onde você deseja inserir a imagem no documento.

2. Clique na guia **Inserir** da faixa de faixas.

3. No grupo **ilustrações** , clique em **imagem**.

4. Na caixa de diálogo **Inserir imagem** , navegue até a imagem que deseja inserir e clique em **Inserir**.

     A imagem é adicionada ao documento no local do cursor atual.

## <a name="add-a-picture-at-run-time"></a>Adicionar uma imagem em tempo de execução
 Você pode inserir uma imagem em um documento no local do cursor atual.

### <a name="to-add-a-picture-at-the-cursor-location"></a>Para adicionar uma imagem no local do cursor

1. Chame o <xref:Microsoft.Office.Interop.Word.InlineShapes.AddPicture%2A> método da <xref:Microsoft.Office.Interop.Word.InlineShapes> coleção e passe o nome do arquivo.

     [!code-vb[Trin_VstcoreWordAutomation#108](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#108)]
     [!code-csharp[Trin_VstcoreWordAutomation#108](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#108)]

## <a name="add-wordart-at-design-time"></a>Adicionar WordArt em tempo de design
 Se você estiver desenvolvendo uma personalização em nível de documento, poderá adicionar o WordArt ao documento em tempo de design.

### <a name="to-add-wordart-to-a-word-document-at-design-time"></a>Para adicionar um WordArt a um documento do Word em tempo de design

1. Coloque o cursor onde você deseja inserir o WordArt no documento.

2. Clique na guia **Inserir** da faixa de faixas.

3. No grupo de **texto** , clique em **WordArt**e selecione um estilo de WordArt.

4. Adicione o texto que você deseja que apareça no documento à caixa de diálogo **Editar texto de WordArt** e clique em **OK**.

     O texto é adicionado ao documento com o estilo de WordArt selecionado aplicado.

## <a name="add-wordart-at-run-time"></a>Adicionar WordArt em tempo de execução
 Você pode inserir o WordArt em um documento no local do cursor atual. O procedimento é diferente para personalizações em nível de documento e suplementos do VSTO.

### <a name="to-add-wordart-at-the-cursor-location-in-a-document-level-customization"></a>Para adicionar um WordArt no local do cursor em uma personalização no nível do documento

1. Obter a posição esquerda e superior do local do cursor atual.

     [!code-vb[Trin_VstcoreWordAutomation#109](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#109)]
     [!code-csharp[Trin_VstcoreWordAutomation#109](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#109)]

2. Chame o <xref:Microsoft.Office.Interop.Word.Shapes.AddTextEffect%2A> método do <xref:Microsoft.Office.Interop.Word.Shapes> objeto no documento.

     [!code-vb[Trin_VstcoreWordAutomation#110](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#110)]
     [!code-csharp[Trin_VstcoreWordAutomation#110](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#110)]

### <a name="to-add-wordart-at-the-cursor-location-in-a-vsto-add-in"></a>Para adicionar um WordArt no local do cursor em um suplemento do VSTO

1. Obter a posição esquerda e superior do local do cursor atual.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#109](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#109)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#109](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#109)]

2. Chamar o <xref:Microsoft.Office.Interop.Word.Shapes.AddTextEffect%2A> método do <xref:Microsoft.Office.Interop.Word.Shapes> objeto do documento ativo (ou um documento diferente que você especificar).

     [!code-vb[Trin_VstcoreWordAutomationAddIn#110](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#110)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#110](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#110)]

## <a name="compile-the-code"></a>Compilar o código

- Uma imagem chamada *SamplePicture.jpg* deve existir na unidade C.

## <a name="see-also"></a>Confira também
- [Como: abrir documentos existentes programaticamente](../vsto/how-to-programmatically-open-existing-documents.md)
- [Como: inserir texto de forma programática em documentos do Word](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [Como: programaticamente restaurar seleções após pesquisas](../vsto/how-to-programmatically-restore-selections-after-searches.md)
- [Como: salvar documentos programaticamente](../vsto/how-to-programmatically-save-documents.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
