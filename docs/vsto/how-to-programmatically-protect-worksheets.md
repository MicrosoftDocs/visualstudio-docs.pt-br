---
title: 'Como: proteger planilhas programaticamente'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- protection, adding to worksheets
- documents [Office development in Visual Studio], document protection
- document protection, adding to worksheets
- worksheets, protecting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d51a6557b2204d7b6ff3d8865c82de091f5a59d0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545893"
---
# <a name="how-to-programmatically-protect-worksheets"></a>Como: proteger planilhas programaticamente
  O recurso de proteção no Microsoft Office Excel ajuda a impedir que usuários e código modifiquem objetos em uma planilha. Por padrão, todas as células são bloqueadas depois que você ativa a proteção.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 Em personalizações em nível de documento, você pode proteger planilhas usando o designer do Excel. Você também pode proteger uma planilha programaticamente em tempo de execução em qualquer tipo de projeto.

> [!NOTE]
> Você não pode adicionar Windows Forms controles a áreas de uma planilha protegidas.

## <a name="use-the-designer"></a>Usar o designer

### <a name="to-protect-a-worksheet-in-the-designer"></a>Para proteger uma planilha no designer

1. No grupo **alterações** da guia **revisão** , clique em **proteger planilha**.

    A caixa de diálogo **proteger planilha** é exibida. Você pode definir uma senha e, opcionalmente, especificar determinadas ações que os usuários têm permissão para executar com a planilha, como formatar células ou inserir linhas.

   Você também pode permitir que os usuários editem intervalos específicos em planilhas protegidas.

### <a name="to-allow-editing-in-specific-ranges"></a>Para permitir a edição em intervalos específicos

1. No grupo **alterações** da guia **revisão** , clique em **permitir que os usuários editem intervalos**.

     A caixa de diálogo **permitir que os usuários editem intervalos** é exibida. Você pode especificar os intervalos desbloqueados usando uma senha e os usuários que podem editar intervalos sem uma senha.

## <a name="use-code-at-run-time"></a>Usar código em tempo de execução
 O código a seguir define a senha (usando a variável getPasswordFromUser, que contém uma senha obtida do usuário) e permite apenas classificação.

### <a name="to-protect-a-worksheet-by-using-code-in-a-document-level-customization"></a>Para proteger uma planilha usando código em uma personalização em nível de documento

1. Chame o <xref:Microsoft.Office.Tools.Excel.Worksheet.Protect%2A> método da planilha. Este exemplo pressupõe que você está trabalhando com uma planilha chamada `Sheet1` .

     [!code-csharp[Trin_VstcoreExcelAutomation#27](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#27)]
     [!code-vb[Trin_VstcoreExcelAutomation#27](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#27)]

### <a name="to-protect-a-worksheet-by-using-code-in-a-vsto-add-in"></a>Para proteger uma planilha usando código em um suplemento do VSTO

1. Chame o <xref:Microsoft.Office.Interop.Excel._Worksheet.Protect%2A> método da planilha ativa.

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#17](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#17)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#17](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#17)]

## <a name="see-also"></a>Confira também
- [Trabalhar com planilhas](../vsto/working-with-worksheets.md)
- [Como: remover programaticamente a proteção de planilhas](../vsto/how-to-programmatically-remove-protection-from-worksheets.md)
- [Como: proteger pastas de trabalho programaticamente](../vsto/how-to-programmatically-protect-workbooks.md)
- [Como: ocultar planilhas programaticamente](../vsto/how-to-programmatically-hide-worksheets.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Item de host de planilha](../vsto/worksheet-host-item.md)
- [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
