---
title: Como programaticamente acessar contatos do Outlook
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- contacts [Office development in Visual Studio], searching
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2f6d64512af660392c10082e3bcd3c26b6bc6885
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520088"
---
# <a name="how-to-programmatically-access-outlook-contacts"></a>Como programaticamente acessar contatos do Outlook
  Este exemplo localiza todos os contatos cujos últimos nomes contêm uma cadeia de caracteres de pesquisa especificada.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>Exemplo
 [!code-csharp[Trin_OL_AccessContacts#1](../vsto/codesnippet/CSharp/Trin_OL_AccessContacts.trin_ol_accesscontacts/thisaddin.cs#1)]
 [!code-csharp[Trin_OL_AccessContacts#1](../vsto/codesnippet/CSharp/Trin_OL_AccessContacts.trin_ol_accesscontacts/thisaddin.cs#1)]
 [!code-vb[Trin_OL_AccessContacts#1](../vsto/codesnippet/VisualBasic/Trin_OL_AccessContacts/thisaddin.vb#1)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer:

- Contatos cujos últimos nomes contêm a cadeia de caracteres "**na"** (por exemplo, Tzipi Butnaru) na pasta de **contatos** .

## <a name="see-also"></a>Confira também
- [Trabalhar com itens de contato](../vsto/working-with-contact-items.md)
- [Como: adicionar programaticamente uma entrada aos contatos do Outlook](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)
- [Como: pesquisar programaticamente por um contato específico](../vsto/how-to-programmatically-search-for-a-specific-contact.md)
- [Como: pesquisar programaticamente por um endereço de email nos contatos](../vsto/how-to-programmatically-search-for-an-e-mail-address-in-contacts.md)
- [Como: excluir programaticamente contatos do Outlook](../vsto/how-to-programmatically-delete-outlook-contacts.md)
