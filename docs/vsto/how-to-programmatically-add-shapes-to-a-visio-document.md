---
title: 'Como: adicionar formas programaticamente a um documento do Visio'
description: Saiba como você pode adicionar formas a um Microsoft Office documento do Visio recuperando os mestres de um estêncil e soltando as formas na página ativa.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visio [Office development in Visual Studio], adding Visio shapes
- shapes [Office development in Visual Studio], adding Visio shapes
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f5eabd18ac915e6cc10ff05de3d13d0263fa1eee
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828404"
---
# <a name="how-to-programmatically-add-shapes-to-a-visio-document"></a>Como: adicionar formas programaticamente a um documento do Visio
  Você pode adicionar formas a um Microsoft Office documento do Visio recuperando os mestres de um estêncil e soltando as formas na página ativa.

 Para obter mais informações, consulte a documentação de referência do VBA para o [Microsoft.Office.Interop.Visio.Documents. Adicione](/office/vba/api/Visio.Documents.Add) o método, a propriedade [Microsoft. Office. Interop. Visio. Application. ActivePage](/office/vba/api/Visio.Application.ActivePage) e [o método Microsoft. Office. Interop. Visio. Page. drop](/office/vba/api/Visio.Page.Drop) .

## <a name="add-shapes-to-a-visio-document"></a>Adicionar formas a um documento do Visio

### <a name="to-add-shapes-to-a-visio-document"></a>Para adicionar formas a um documento do Visio

- Com um documento ativo, recupere os mestres da coleção Documents. Masters e descarte as formas no documento ativo. Você pode recuperar um mestre usando o índice ou o nome mestre.

     O exemplo de código a seguir cria um documento do Visio em branco e, em seguida, abre-o com o estêncil **formas básicas** encaixado. Em seguida, o código recupera várias formas e as descarta na página ativa.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet13":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet13":::

## <a name="see-also"></a>Consulte também
- [Soluções do Visio](../vsto/visio-solutions.md)
- [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)
- [Trabalhar com formas do Visio](../vsto/working-with-visio-shapes.md)
- [Como: copiar e colar formas programaticamente em um documento do Visio](../vsto/how-to-programmatically-copy-and-paste-shapes-in-a-visio-document.md)
