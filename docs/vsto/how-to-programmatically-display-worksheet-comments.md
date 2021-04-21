---
title: Como exibir programaticamente comentários de planilha
description: Saiba como você pode mostrar e ocultar de forma programática os comentários em uma planilha do Microsoft Excel no nível de documento ou no nível do aplicativo.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, comments
- comments, worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: af327a6756189c73f80f624205451274abf19264
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828664"
---
# <a name="how-to-programmatically-display-worksheet-comments"></a>Como exibir programaticamente comentários de planilha
  Você pode mostrar e ocultar de forma programática comentários em planilhas Microsoft Office Excel.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-display-all-comments-on-a-worksheet-in-a-document-level-customization"></a>Para exibir todos os comentários em uma planilha em uma personalização no nível do documento

1. Defina a <xref:Microsoft.Office.Interop.Excel.Comment.Visible%2A> propriedade como **true** se desejar mostrar comentários; caso contrário, **false**. Esse código deve ser colocado em uma classe de planilha, não na `ThisWorkbook` classe.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet31":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet31":::

## <a name="to-display-all-comments-on-a-worksheet-in-an-application-level-vsto-add-in"></a>Para exibir todos os comentários em uma planilha em um suplemento do VSTO em nível de aplicativo

1. Defina a <xref:Microsoft.Office.Interop.Excel.Comment.Visible%2A> propriedade como **true** se desejar mostrar comentários; caso contrário, **false**.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet21":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet21":::

## <a name="see-also"></a>Consulte também
- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Como: Adicionar e excluir de forma programática comentários da planilha](../vsto/how-to-programmatically-add-and-delete-worksheet-comments.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
