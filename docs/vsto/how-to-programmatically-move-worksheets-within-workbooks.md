---
title: 'Como: mover planilhas em pastas de trabalho de forma programática'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, moving
- workbooks, moving worksheets in
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 5075008e3b6b2b6f9ae087c0cfe962f2a1191f52
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669780"
---
# <a name="how-to-programmatically-move-worksheets-within-workbooks"></a>Como: mover planilhas em pastas de trabalho de forma programática
  Programaticamente, você pode alterar a posição de planilhas em relação a outras planilhas em uma pasta de trabalho. Se você não especificar um local para a folha movida, o Excel cria uma nova pasta de trabalho para contê-lo.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="to-move-a-worksheet-in-a-document-level-customization"></a>Para mover uma planilha em uma personalização no nível de documento  
  
1.  Atribuir o número total de folhas na pasta de trabalho a uma variável e, em seguida, mova a primeira planilha para que ele se torne o último deles.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#24](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#24)]
     [!code-vb[Trin_VstcoreExcelAutomation#24](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#24)]  
  
## <a name="to-move-a-worksheet-in-a-vsto-add-in"></a>Para mover uma planilha em um suplemento do VSTO  
  
1.  Atribuir o número total de folhas na pasta de trabalho a uma variável e, em seguida, mova a primeira planilha para que ele se torne o último deles.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#16](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#16)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#16](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#16)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com planilhas](../vsto/working-with-worksheets.md)   
 [Como: ocultar planilhas programaticamente](../vsto/how-to-programmatically-hide-worksheets.md)   
 [Como: excluir planilhas de pastas de trabalho de forma programática](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)   
 [Como: proteger planilhas programaticamente](../vsto/how-to-programmatically-protect-worksheets.md)   
 [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)  
  
  