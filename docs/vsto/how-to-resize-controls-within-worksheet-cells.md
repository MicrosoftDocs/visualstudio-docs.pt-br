---
title: 'Como: redimensionar controles dentro de células da planilha'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- managed controls, resizing
- worksheets, resizing
- Windows Forms controls [Office development in Visual Studio], resizing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 91a7e66e085408b35f0ce1d8f7d4783e0c4715a8
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670106"
---
# <a name="how-to-resize-controls-within-worksheet-cells"></a>Como: redimensionar controles dentro de células da planilha
  Quando você redimensiona as colunas ou linhas em uma planilha, todos os controles dentro das células host será redimensionada automaticamente para a altura ou largura da célula que foi redimensionada. Controles dos Windows Forms não são redimensionados automaticamente por padrão.  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
 Se você adicionar os controles em tempo de design, você deve definir opções de posicionamento para cada controle.  
  
 Se você adicionar um controle dos Windows Forms programaticamente e fornece um argumento de intervalo, o controle é redimensionado automaticamente quando uma célula dentro do intervalo é redimensionada. Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
## <a name="resize-controls-at-design-time"></a>Redimensionar controles no tempo de design  
  
### <a name="to-make-controls-resize-with-cells-at-design-time"></a>Para fazer com que controles redimensionar com células em tempo de design  
  
1.  Dos **caixa de ferramentas**, arraste um controle dos Windows Forms a uma planilha.  
  
2.  O controle com o botão direito e, em seguida, clique em **Formatar controle**.  
  
3.  No **controle de formato** caixa de diálogo, clique o **propriedades** guia.  
  
4.  Sob **posicionamento do objeto**, selecione o **mover e dimensionar com células** opção e, em seguida, clique em **Okey**.  
  
     Quando você redimensiona a célula que contém o controle, o controle é redimensionado para caber na célula.  
  
## <a name="resize-controls-at-runtime"></a>Redimensionar controles no tempo de execução  
 Se você adicionar um controle dos Windows Forms em tempo de execução e passar um <xref:Microsoft.Office.Interop.Excel.Range> como o local para o controle, o controle será redimensionado automaticamente quando a célula da planilha que contém o intervalo é redimensionada.  
  
### <a name="to-make-controls-resize-with-cells-at-run-time"></a>Para fazer com que controles redimensionar com células em tempo de execução  
  
1.  Adicione um controle ao intervalo A1.  
  
     [!code-vb[Trin_VstcoreProgrammingControlsExcel#5](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#5)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#5](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#5)]  
  
     Quando você redimensiona a célula que contém o controle, o controle é redimensionado para caber na célula.  
  
## <a name="reset-control-placement"></a>Redefinir o posicionamento de controle  
 Você pode redefinir o posicionamento e redimensionamento do controle definindo a `Placement` propriedade para um dos seguintes <xref:Microsoft.Office.Interop.Excel.XlPlacement> valores:  
  
-   <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlFreeFloating>  
  
-   <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlMove>  
  
-   <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlMoveAndSize>  
  
### <a name="to-change-the-behavior-of-a-control-so-that-it-does-not-resize-or-move-with-the-cell"></a>Para alterar o comportamento de um controle para que ele não redimensionar ou mover com a célula  
  
1.  Chame a propriedade de posicionamento do controle e defina o valor para <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlFreeFloating>.  
  
     [!code-vb[Trin_VstcoreProgrammingControlsExcel#6](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#6)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#6](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#6)]  
  
## <a name="see-also"></a>Consulte também  
 [Controles em documentos do Office](../vsto/controls-on-office-documents.md)   
 [Como: adicionar controles dos Windows Forms a documentos do Office](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)   
 [Como: ocultar controles em planilhas durante a impressão](../vsto/how-to-hide-controls-on-worksheets-when-printing.md)   
 [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)   
 [Limitações de controles de Windows Forms em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)  
  