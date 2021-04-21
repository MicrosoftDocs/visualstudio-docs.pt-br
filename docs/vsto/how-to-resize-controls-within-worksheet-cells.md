---
title: 'Como: redimensionar controles nas células da planilha'
description: Saiba como você pode usar o Visual Studio para redimensionar controles dentro de células de planilha do Microsoft Excel em tempo de design e em tempo de execução.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- managed controls, resizing
- worksheets, resizing
- Windows Forms controls [Office development in Visual Studio], resizing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7b42c10fd82ec077b295a8bc683fa138c2eb095b
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825739"
---
# <a name="how-to-resize-controls-within-worksheet-cells"></a>Como: redimensionar controles nas células da planilha
  Quando você redimensiona colunas ou linhas em uma planilha, todos os controles de host dentro das células são redimensionados automaticamente para a altura ou largura da célula que foi redimensionada. Os controles de Windows Forms não são redimensionados automaticamente por padrão.

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 Se você adicionar os controles em tempo de design, deverá definir opções de posicionamento para cada controle.

 Se você adicionar um controle de Windows Forms programaticamente e fornecer um argumento de intervalo, o controle será redimensionado automaticamente quando uma célula dentro do intervalo for redimensionada. Para obter mais informações, consulte [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).

## <a name="resize-controls-at-design-time"></a>Redimensionar controles em tempo de design

### <a name="to-make-controls-resize-with-cells-at-design-time"></a>Para fazer com que os controles sejam redimensionados com células em tempo de design

1. Na **caixa de ferramentas**, arraste um controle de Windows Forms para uma planilha.

2. Clique com o botão direito do mouse no controle e clique em **Formatar controle**.

3. Na caixa de diálogo **Formatar controle** , clique na guia **Propriedades** .

4. Em **posicionamento do objeto**, selecione a opção **mover e dimensionar com células** e clique em **OK**.

     Quando você redimensiona a célula que contém o controle, o controle é redimensionado para se ajustar à célula.

## <a name="resize-controls-at-run-time"></a>Redimensionar controles em tempo de execução
 Se você adicionar um controle de Windows Forms em tempo de execução e passar um <xref:Microsoft.Office.Interop.Excel.Range> como o local para o controle, o controle será redimensionado automaticamente quando a célula da planilha que contém o intervalo for redimensionada.

### <a name="to-make-controls-resize-with-cells-at-run-time"></a>Para fazer com que os controles sejam redimensionados com células em tempo de execução

1. Adicione um controle ao intervalo a1.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet5":::

     Quando você redimensiona a célula que contém o controle, o controle é redimensionado para se ajustar à célula.

## <a name="reset-control-placement"></a>Redefinir posicionamento do controle
 Você pode redefinir o posicionamento e o redimensionamento do controle definindo a `Placement` propriedade com um dos seguintes <xref:Microsoft.Office.Interop.Excel.XlPlacement> valores:

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlFreeFloating>

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlMove>

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlMoveAndSize>

### <a name="to-change-the-behavior-of-a-control-so-that-it-does-not-resize-or-move-with-the-cell"></a>Para alterar o comportamento de um controle para que ele não redimensione ou mova com a célula

1. Chame a propriedade Placement do controle e defina o valor como <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlFreeFloating> .

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet6":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet6":::

## <a name="see-also"></a>Consulte também
- [Controles em documentos do Office](../vsto/controls-on-office-documents.md)
- [Como: adicionar controles de Windows Forms a documentos do Office](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [Como: Ocultar controles em planilhas ao imprimir](../vsto/how-to-hide-controls-on-worksheets-when-printing.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Limitações de controles de Windows Forms em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
