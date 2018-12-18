---
title: 'Como: determinar o item atual do Outlook de forma programática'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- mail items [Office development in Visual Studio], current
- e-mail [Office development in Visual Studio], current item
- SelectionChange event
- Outlook [Office development in Visual Studio], current item
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 519fd1572b3ebb1faf8cc7adc6d5a9ba2773d67b
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35257032"
---
# <a name="how-to-programmatically-determine-the-current-outlook-item"></a>Como: determinar o item atual do Outlook de forma programática
  Este exemplo usa o `Explorer.SelectionChange` evento para exibir o nome da pasta atual e algumas informações sobre o item selecionado. O código, em seguida, exibe o item selecionado.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
## <a name="example"></a>Exemplo  
 [!code-vb[Trin_OL_CurrentItem#1](../vsto/codesnippet/VisualBasic/Trin_OL_CurrentItem/thisaddin.vb#1)]
 [!code-csharp[Trin_OL_CurrentItem#1](../vsto/codesnippet/CSharp/Trin_OL_CurrentItem/thisaddin.cs#1)]  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo requer:  
  
-   Compromisso, contatos e itens de email no Microsoft Office Outlook.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de modelo de objeto do Outlook](../vsto/outlook-object-model-overview.md)   
 [Como: recuperar uma pasta por nome de forma programática](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)   
 [Como: pesquisar um contato específico de forma programática](../vsto/how-to-programmatically-search-for-a-specific-contact.md)  
  
  