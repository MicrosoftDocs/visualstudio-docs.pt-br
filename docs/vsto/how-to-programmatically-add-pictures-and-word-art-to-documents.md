---
title: 'Como: adicionar programaticamente imagens e Word Art a documentos'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], adding pictures
- Word documents, adding pictures
- Word documents, adding Word Art
- graphics, adding to Word documents
- WordArt, adding to documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 61399df32ef0f22d1d0aacf23dea45c1357c7579
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35255100"
---
# <a name="how-to-programmatically-add-pictures-and-word-art-to-documents"></a>Como: adicionar programaticamente imagens e Word Art a documentos
  Você pode adicionar imagens e objetos de desenho para seus documentos em tempo de design ou tempo de execução. WordArt permite que você adicione texto decorativo para documentos do Microsoft Office Word. Esses efeitos especiais de texto são objetos que você pode personalizar e inserir no documento de desenho.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="add-a-picture-at-design-time"></a>Adicionar uma imagem em tempo de design  
 Se você estiver desenvolvendo uma personalização no nível de documento, você pode adicionar uma imagem ao documento em tempo de design.  
  
### <a name="to-add-a-picture-to-a-word-document-at-design-time"></a>Para adicionar uma imagem a um documento do Word em tempo de design  
  
1.  Coloque o cursor onde você deseja inserir a imagem no documento.  
  
2.  Clique o **inserir** guia da faixa de opções.  
  
3.  No **ilustrações** , clique em **imagem**.  
  
4.  No **Insert Picture** caixa de diálogo, navegue até a imagem que você deseja inserir e clique em **inserir**.  
  
     A imagem é adicionada ao documento no local atual do cursor.  
  
## <a name="add-a-picture-at-runtime"></a>Adicionar uma imagem em tempo de execução  
 Você pode inserir uma imagem em um documento no local atual do cursor.  
  
### <a name="to-add-a-picture-at-the-cursor-location"></a>Para adicionar uma imagem no local do cursor  
  
1.  Chame o <xref:Microsoft.Office.Interop.Word.InlineShapes.AddPicture%2A> método da <xref:Microsoft.Office.Interop.Word.InlineShapes> coleta e passe no nome do arquivo.  
  
     [!code-vb[Trin_VstcoreWordAutomation#108](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#108)]
     [!code-csharp[Trin_VstcoreWordAutomation#108](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#108)]  
  
## <a name="add-wordart-at-design-time"></a>Adicionar WordArt no tempo de design  
 Se você estiver desenvolvendo uma personalização no nível de documento, você pode adicionar WordArt ao documento em tempo de design.  
  
### <a name="to-add-wordart-to-a-word-document-at-design-time"></a>Para adicionar o WordArt a um documento do Word em tempo de design  
  
1.  Coloque o cursor onde você deseja inserir a WordArt no documento.  
  
2.  Clique o **inserir** guia da faixa de opções.  
  
3.  No **texto** , clique em **WordArt**e, em seguida, selecione um estilo de WordArt.  
  
4.  Adicione o texto que você deseja que apareça no documento para o **editar texto de WordArt** caixa de diálogo e clique em **Okey**.  
  
     O texto é adicionado ao seu documento com o estilo selecionado do WordArt aplicado.  
  
## <a name="add-wordart-at-runtime"></a>Adicionar WordArt no tempo de execução  
 Você pode inserir o WordArt em um documento no local atual do cursor. O procedimento é diferente para personalizações no nível de documento e suplementos do VSTO.  
  
### <a name="to-add-wordart-at-the-cursor-location-in-a-document-level-customization"></a>Para adicionar o WordArt no local do cursor em uma personalização no nível de documento  
  
1.  Obtenha a posição esquerda e superior do local atual do cursor.  
  
     [!code-vb[Trin_VstcoreWordAutomation#109](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#109)]
     [!code-csharp[Trin_VstcoreWordAutomation#109](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#109)]  
  
2.  Chame o <xref:Microsoft.Office.Interop.Word.Shapes.AddTextEffect%2A> método da <xref:Microsoft.Office.Interop.Word.Shapes> objeto no documento.  
  
     [!code-vb[Trin_VstcoreWordAutomation#110](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#110)]
     [!code-csharp[Trin_VstcoreWordAutomation#110](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#110)]  
  
### <a name="to-add-wordart-at-the-cursor-location-in-a-vsto-add-in"></a>Para adicionar o WordArt no local do cursor em um suplemento do VSTO  
  
1.  Obtenha a posição esquerda e superior do local atual do cursor.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#109](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#109)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#109](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#109)]  
  
2.  Chame o <xref:Microsoft.Office.Interop.Word.Shapes.AddTextEffect%2A> método da <xref:Microsoft.Office.Interop.Word.Shapes> objeto do documento ativo (ou outro documento que você especificar).  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#110](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#110)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#110](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#110)]  
  
## <a name="compile-the-code"></a>Compilar o código  
  
-   Uma imagem denominada *SamplePicture.jpg* deve existir na unidade C.  
  
## <a name="see-also"></a>Consulte também  
 [Como: abrir documentos existentes programaticamente](../vsto/how-to-programmatically-open-existing-documents.md)   
 [Como: programaticamente, inserir texto em documentos do Word](../vsto/how-to-programmatically-insert-text-into-word-documents.md)   
 [Como: programaticamente restaurar seleções após pesquisas](../vsto/how-to-programmatically-restore-selections-after-searches.md)   
 [Como: salvar documentos programaticamente](../vsto/how-to-programmatically-save-documents.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  