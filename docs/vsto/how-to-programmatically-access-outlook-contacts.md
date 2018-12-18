---
title: 'Como: acessar contatos do Outlook de forma programática'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- contacts [Office development in Visual Studio], searching
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 6ee09e0d0a51675bc00b19aedd0508276cb0cb09
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35255935"
---
# <a name="how-to-programmatically-access-outlook-contacts"></a>Como: acessar contatos do Outlook de forma programática
  Este exemplo localiza todos os contatos cujos sobrenomes contêm uma cadeia de caracteres de pesquisa especificado.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[Trin_OL_AccessContacts#1](../vsto/codesnippet/CSharp/Trin_OL_AccessContacts.trin_ol_accesscontacts/thisaddin.cs#1)]
 [!code-csharp[Trin_OL_AccessContacts#1](../vsto/codesnippet/CSharp/Trin_OL_AccessContacts.trin_ol_accesscontacts/thisaddin.cs#1)]
 [!code-vb[Trin_OL_AccessContacts#1](../vsto/codesnippet/VisualBasic/Trin_OL_AccessContacts/thisaddin.vb#1)]  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo requer:  
  
-   Contatos cujos sobrenomes contêm a cadeia de caracteres "**Na"** (por exemplo, Tzipi Butnaru) na **contatos** pasta.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com itens de contato](../vsto/working-with-contact-items.md)   
 [Como: adicionar uma entrada a contatos do Outlook de forma programática](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)   
 [Como: pesquisar um contato específico de forma programática](../vsto/how-to-programmatically-search-for-a-specific-contact.md)   
 [Como: procurar um endereço de email em contatos programaticamente](../vsto/how-to-programmatically-search-for-an-e-mail-address-in-contacts.md)   
 [Como: excluir contatos do Outlook de forma programática](../vsto/how-to-programmatically-delete-outlook-contacts.md)  
  
  