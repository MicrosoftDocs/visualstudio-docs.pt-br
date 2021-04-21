---
title: Como programaticamente acessar contatos do Outlook
description: Saiba como você pode acessar os contatos do Outlook programaticamente. Este exemplo localiza todos os contatos cujos últimos nomes contêm uma cadeia de caracteres de pesquisa especificada.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- contacts [Office development in Visual Studio], searching
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 08e9d9ea69985a26a9688152f5c3b028caf75300
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828898"
---
# <a name="how-to-programmatically-access-outlook-contacts"></a>Como programaticamente acessar contatos do Outlook
  Este exemplo localiza todos os contatos cujos últimos nomes contêm uma cadeia de caracteres de pesquisa especificada.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>Exemplo
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_AccessContacts.trin_ol_accesscontacts/thisaddin.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OL_AccessContacts/thisaddin.vb" id="Snippet1":::


## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer:

- Contatos cujos últimos nomes contêm a cadeia de caracteres "**na"** (por exemplo, Tzipi Butnaru) na pasta de **contatos** .

## <a name="see-also"></a>Consulte também
- [Trabalhar com itens de contato](../vsto/working-with-contact-items.md)
- [Como: adicionar programaticamente uma entrada aos contatos do Outlook](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)
- [Como: pesquisar programaticamente por um contato específico](../vsto/how-to-programmatically-search-for-a-specific-contact.md)
- [Como: pesquisar programaticamente por um endereço de email nos contatos](../vsto/how-to-programmatically-search-for-an-e-mail-address-in-contacts.md)
- [Como: excluir programaticamente contatos do Outlook](../vsto/how-to-programmatically-delete-outlook-contacts.md)
