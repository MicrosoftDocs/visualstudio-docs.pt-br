---
title: 'Como: pesquisar programaticamente por um contato específico'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- contacts [Office development in Visual Studio], searching
- searching contacts
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8d8b2302586fc09fcfec6420d97374197eae7e67
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547063"
---
# <a name="how-to-programmatically-search-for-a-specific-contact"></a>Como: pesquisar programaticamente por um contato específico
  Este exemplo pesquisa uma pasta contatos do Outlook para um contato específico pelo nome e sobrenome. O exemplo supõe que exista um contato chamado **John Evans** na pasta Contacts.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>Exemplo
 [!code-csharp[Trin_Outlook_RL_SearchForContact#1](../vsto/codesnippet/CSharp/trin_outlook_rl_searchforcontact/thisaddin.cs#1)]
 [!code-vb[Trin_Outlook_RL_SearchForContact#1](../vsto/codesnippet/VisualBasic/trin_outlook_rl_searchforcontact/thisaddin.vb#1)]

## <a name="see-also"></a>Confira também
- [Trabalhar com itens de contato](../vsto/working-with-contact-items.md)
- [Introdução à programação de suplementos do VSTO](../vsto/getting-started-programming-vsto-add-ins.md)
