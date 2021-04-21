---
title: Copiar e colar formas no documento do Visio programaticamente
description: Saiba como você pode copiar formas programaticamente em uma página de um documento e colá-las em uma nova página no mesmo documento.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- shapes [Office development in Visual Studio], copying and pasting Visio shapes
- Visio [Office development in Visual Studio], copying and pasting Visio shapes
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b7cda46330967ef2b2b08db2109a030bbef8cace
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828547"
---
# <a name="how-to-programmatically-copy-and-paste-shapes-in-a-visio-document"></a>Como: copiar e colar formas programaticamente em um documento do Visio
  Você pode copiar formas programaticamente em uma página de um documento e colá-las em uma nova página no mesmo documento. Você pode optar por colá-los no local padrão (o centro da janela ativa) ou nos mesmos locais de coordenadas que tinham na página original.

## <a name="copy-and-paste-shapes"></a>Copiar e colar formas
 Para obter detalhes sobre o modelo de objeto, consulte a documentação de referência do VBA para o [Microsoft. Office. Interop. Visio. Shape. DrawRectangle](/office/vba/api/Visio.Shape.DrawRectangle), [Microsoft. Office. Interop. Visio. Shape. DrawOval](/office/vba/api/Visio.Shape.DrawOval), os métodos Microsoft. Office [. Interop. Visio. Shape. Copy](/office/vba/api/Visio.Shape.Copy)e [Microsoft. Office. Interop. Visio. Shape. Paste](/office/vba/api/Visio.Shape.Paste) e o sinalizador [Microsoft. Office. Interop. Visio. VisCutCopyPasteCodes](/office/vba/api/Visio.viscutcopypastecodes)

### <a name="to-copy-shapes-to-the-center-of-another-page"></a>Para copiar formas para o centro de outra página

- O exemplo a seguir demonstra como copiar as formas da primeira página e colá-las no centro da segunda página.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet14":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet14":::

## <a name="copy-and-paste-shapes-with-the-same-positions"></a>Copiar e colar formas com as mesmas posições
 Para obter detalhes sobre o modelo de objeto, consulte a documentação de referência do VBA para o [Microsoft. Office. Interop. Visio. Shape. DrawRectangle](/office/vba/api/Visio.Shape.DrawRectangle), [Microsoft. Office. Interop. Visio. Shape. DrawOval](/office/vba/api/Visio.Shape.DrawOval), os métodos Microsoft. Office [. Interop. Visio. Shape. Copy](/office/vba/api/Visio.Shape.Copy)e [Microsoft. Office. Interop. Visio. Shape. Paste](/office/vba/api/Visio.Shape.Paste) e o sinalizador [Microsoft. Office. Interop. Visio. VisCutCopyPasteCodes](/office/vba/api/Visio.viscutcopypastecodes)

 Se você precisar controlar o formato das informações coladas e (opcionalmente) estabelecer um link para um arquivo de origem (por exemplo, um Microsoft Office documento do Word), use o método PasteSpecial.

### <a name="to-copy-shapes-and-shape-locations-to-another-page"></a>Para copiar formas e locais de forma para outra página

- O exemplo a seguir demonstra como copiar as formas da primeira página e colá-las na segunda página com seus locais de coordenadas originais.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet15":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet15":::

## <a name="see-also"></a>Consulte também
- [Soluções do Visio](../vsto/visio-solutions.md)
- [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)
- [Trabalhar com formas do Visio](../vsto/working-with-visio-shapes.md)
- [Como: adicionar formas programaticamente a um documento do Visio](../vsto/how-to-programmatically-add-shapes-to-a-visio-document.md)
