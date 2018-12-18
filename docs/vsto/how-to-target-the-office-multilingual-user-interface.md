---
title: 'Como: destinar a interface de usuário multilíngue do Office'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- globalization [Office development in Visual Studio], user interface targeting
- MUI [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], localization
- Multilingual User Interface [Office development in Visual Studio]
- localization [Office development in Visual Studio], user interface targeting
- Office applications [Office development in Visual Studio], globalization
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 1b917479598b73f71a0f3092c874276a700717d6
ms.sourcegitcommit: 209c2c068ff0975994ed892b62aa9b834a7f6077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34262027"
---
# <a name="how-to-target-the-office-multilingual-user-interface"></a>Como: destinar a interface de usuário multilíngue do Office
  A Interface de usuário multilíngue (MUI) é um recurso do Microsoft Office que permite que o usuário final para alterar o idioma da interface do usuário (IU). Por exemplo, um usuário final trabalhando com uma interface do usuário em inglês pode alterar o idioma da interface do usuário para espanhol.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
 Se seu aplicativo será usado por pessoas que usem muitos idiomas do Office, você pode adicionar código para alterar automaticamente o idioma de suas cadeias de caracteres da interface do usuário para corresponder ao idioma que está sendo usado pelo Office no computador do usuário (se o usuário tem os recursos corretos instalados).  
  
## <a name="to-check-the-current-office-ui-setting"></a>Para verificar a configuração atual da interface do usuário do Office  
  
1.  Use o <xref:System.Threading.Thread.CurrentUICulture%2A> propriedade do thread atual. Defina o idioma de suas cadeias de caracteres da interface do usuário para corresponder ao idioma usado pela versão do Office que atualmente é executado no computador do usuário.  
  
     [!code-vb[Trin_VstcoreCreatingExcel#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb#10)]
     [!code-csharp[Trin_VstcoreCreatingExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs#10)]  
  
## <a name="see-also"></a>Consulte também  
 [Como: aplicativos do Office de destino por meio de assemblies de interoperabilidade primários](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)   
 [Associação tardia em soluções do Office](../vsto/late-binding-in-office-solutions.md)  
  
  