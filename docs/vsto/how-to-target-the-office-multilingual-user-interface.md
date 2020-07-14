---
title: 'Como: direcionar a interface do usuário multilíngüe do Office'
ms.date: 02/02/2017
ms.topic: how-to
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
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5217f2d6cf67eced00c0c84b9bacda94573c5a09
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537495"
---
# <a name="how-to-target-the-office-multilingual-user-interface"></a>Como: direcionar a interface do usuário multilíngüe do Office
  A MUI (Multilingual User interface) é um recurso Microsoft Office que dá ao usuário final a capacidade de alterar o idioma da interface do usuário. Por exemplo, um usuário final trabalhando com uma interface de usuário em inglês pode alterar o idioma da interface do usuário para espanhol.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 Se seu aplicativo for usado por pessoas que usam muitos idiomas do Office, você poderá adicionar código para alterar automaticamente o idioma das cadeias de caracteres da interface do usuário para corresponder ao idioma usado pelo Office no computador do usuário (se o usuário tiver os recursos corretos instalados).

## <a name="to-check-the-current-office-ui-setting"></a>Para verificar a configuração atual da interface do usuário do Office

1. Use a <xref:System.Threading.Thread.CurrentUICulture%2A> Propriedade do thread atual. Defina o idioma das cadeias de caracteres da interface do usuário para corresponder ao idioma usado pela versão do Office que atualmente é executada no computador do usuário.

     [!code-vb[Trin_VstcoreCreatingExcel#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb#10)]
     [!code-csharp[Trin_VstcoreCreatingExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs#10)]

## <a name="see-also"></a>Confira também
- [Como: direcionar aplicativos do Office por meio de assemblies de interoperabilidade primária](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [Associação tardia em soluções do Office](../vsto/late-binding-in-office-solutions.md)
