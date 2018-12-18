---
title: 'Como: copiar e colar formas em um documento do Visio de forma programática'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- shapes [Office development in Visual Studio], copying and pasting Visio shapes
- Visio [Office development in Visual Studio], copying and pasting Visio shapes
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: e0028b11899e05adde1dd1b5483b71d2c48101db
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671489"
---
# <a name="how-to-programmatically-copy-and-paste-shapes-in-a-visio-document"></a>Como: copiar e colar formas em um documento do Visio de forma programática
  Programaticamente, você pode copiar formas em uma única página de um documento e colá-los em uma nova página no mesmo documento. Você pode optar por colá-los para o local padrão (o centro da janela ativa) ou para os mesmos locais de coordenadas que tiveram na página original.  
  
## <a name="copy-and-paste-shapes"></a>Copiar e colar formas  
 Para obter detalhes sobre o modelo de objeto, consulte a documentação de referência do VBA para o [Microsoft.Office.Interop.Visio.Shape.DrawRectangle](/office/vba/api/Visio.Shape.DrawRectangle), [Microsoft.Office.Interop.Visio.Shape.DrawOval](/office/vba/api/Visio.Shape.DrawOval), [ Microsoft.Office.Interop.Visio.Shape.Copy](/office/vba/api/Visio.Shape.Copy), e [Microsoft.Office.Interop.Visio.Shape.Paste](/office/vba/api/Visio.Shape.Paste) métodos e as [ Microsoft.Office.Interop.Visio.VisCutCopyPasteCodes.visCopyPasteNormal](/office/vba/api/Visio.viscutcopypastecodes) sinalizador.  
  
### <a name="to-copy-shapes-to-the-center-of-another-page"></a>Para copiar formas para o Centro de outra página  
  
-   O exemplo a seguir demonstra como copiar as formas da primeira página e colá-los para o centro da segunda página.  
  
     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#14](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#14)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#14](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#14)]  
  
## <a name="copy-and-paste-shapes-with-the-same-positions"></a>Copiar e colar formas com as mesmas posições  
 Para obter detalhes sobre o modelo de objeto, consulte a documentação de referência do VBA para o [Microsoft.Office.Interop.Visio.Shape.DrawRectangle](/office/vba/api/Visio.Shape.DrawRectangle), [Microsoft.Office.Interop.Visio.Shape.DrawOval](/office/vba/api/Visio.Shape.DrawOval), [ Microsoft.Office.Interop.Visio.Shape.Copy](/office/vba/api/Visio.Shape.Copy), e [Microsoft.Office.Interop.Visio.Shape.Paste](/office/vba/api/Visio.Shape.Paste) métodos e as [ Microsoft.Office.Interop.Visio.VisCutCopyPasteCodes.visCopyPasteNoTranslate](/office/vba/api/Visio.viscutcopypastecodes) sinalizador.  
  
 Se você precisar controlar o formato das informações coladas e (opcionalmente) estabelecer um link para um arquivo de origem (por exemplo, um documento do Microsoft Office Word), use o método PasteSpecial.  
  
### <a name="to-copy-shapes-and-shape-locations-to-another-page"></a>Para copiar formas e locais de forma para outra página  
  
-   O exemplo a seguir demonstra como copiar as formas da primeira página e o cola na segunda página com seus locais originais de coordenadas.  
  
     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#15](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#15)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#15](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#15)]  
  
## <a name="see-also"></a>Consulte também  
 [Soluções do Visio](../vsto/visio-solutions.md)   
 [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)   
 [Trabalhar com formas do Visio](../vsto/working-with-visio-shapes.md)   
 [Como: adicionar formas a um documento do Visio programaticamente](../vsto/how-to-programmatically-add-shapes-to-a-visio-document.md)  
  
  