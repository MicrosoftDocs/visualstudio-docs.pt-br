---
title: 'Como: aplicar estilos a intervalos em pastas de trabalho programaticamente'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, styles
- styles, workbook ranges
- workbooks, styles
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: d19c886a7b3ae1a1976ab2a47fe139ba830a4ea5
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669966"
---
# <a name="how-to-programmatically-apply-styles-to-ranges-in-workbooks"></a>Como: aplicar estilos a intervalos em pastas de trabalho programaticamente
  Você pode aplicar estilos nomeados para regiões em pastas de trabalho. Excel fornece um número de estilos predefinidos.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
 O **Formatar células** caixa de diálogo exibe todas as opções que você pode usar para formatar células, e cada uma dessas opções está disponível a partir do código. Para exibir essa caixa de diálogo no Excel, clique em **células** sobre o **formato** menu.  
  
## <a name="to-apply-a-style-to-a-named-range-in-a-document-level-customization"></a>Para aplicar um estilo a um intervalo nomeado em uma personalização no nível de documento  
  
1.  Crie um novo estilo e defina seus atributos.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#53](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#53)]
     [!code-vb[Trin_VstcoreExcelAutomation#53](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#53)]  
  
2.  Criar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controlar, atribuir texto a ele e, em seguida, aplicar o novo estilo. Esse código deve ser colocado em uma classe de folha, não no `ThisWorkbook` classe.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#54](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#54)]
     [!code-vb[Trin_VstcoreExcelAutomation#54](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#54)]  
  
## <a name="to-clear-a-style-from-a-named-range-in-a-document-level-customization"></a>Para limpar um estilo de um intervalo nomeado em uma personalização no nível de documento  
  
1.  Aplica o estilo Normal para o intervalo. Esse código deve ser colocado em uma classe de folha, não no `ThisWorkbook` classe.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#55](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#55)]
     [!code-vb[Trin_VstcoreExcelAutomation#55](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#55)]  
  
## <a name="to-apply-a-style-to-a-named-range-in-a-vsto-add-in"></a>Para aplicar um estilo a um intervalo nomeado em um suplemento do VSTO  
  
1.  Crie um novo estilo e defina seus atributos.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#28](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#28)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#28](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#28)]  
  
2.  Criar um <xref:Microsoft.Office.Interop.Excel.Range>, atribuir texto a ele e, em seguida, aplicar o novo estilo.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#29](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#29)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#29](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#29)]  
  
## <a name="to-clear-a-style-from-a-named-range-in-a-vsto-add-in"></a>Para limpar um estilo de um intervalo nomeado em um suplemento do VSTO  
  
1.  Aplica o estilo Normal para o intervalo.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#56](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#56)]
     [!code-vb[Trin_VstcoreExcelAutomation#56](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#56)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com intervalos](../vsto/working-with-ranges.md)   
 [Controle NamedRange](../vsto/namedrange-control.md)   
 [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  