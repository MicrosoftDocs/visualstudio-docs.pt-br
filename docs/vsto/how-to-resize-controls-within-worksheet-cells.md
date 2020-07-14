---
title: 'Como: redimensionar controles nas células da planilha'
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f2d22973e13ee77b66de303041f8b6a765b4b93a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545867"
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

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#5](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#5)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#5](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#5)]

     Quando você redimensiona a célula que contém o controle, o controle é redimensionado para se ajustar à célula.

## <a name="reset-control-placement"></a>Redefinir posicionamento do controle
 Você pode redefinir o posicionamento e o redimensionamento do controle definindo a `Placement` propriedade com um dos seguintes <xref:Microsoft.Office.Interop.Excel.XlPlacement> valores:

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlFreeFloating>

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlMove>

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlMoveAndSize>

### <a name="to-change-the-behavior-of-a-control-so-that-it-does-not-resize-or-move-with-the-cell"></a>Para alterar o comportamento de um controle para que ele não redimensione ou mova com a célula

1. Chame a propriedade Placement do controle e defina o valor como <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlFreeFloating> .

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#6](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#6)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#6](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#6)]

## <a name="see-also"></a>Consulte também
- [Controles em documentos do Office](../vsto/controls-on-office-documents.md)
- [Como: adicionar controles de Windows Forms a documentos do Office](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [Como: Ocultar controles em planilhas ao imprimir](../vsto/how-to-hide-controls-on-worksheets-when-printing.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Limitações de controles de Windows Forms em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
