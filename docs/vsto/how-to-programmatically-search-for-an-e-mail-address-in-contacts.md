---
title: Localizar um endereço de email nos contatos de forma programática
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- e-mail [Office development in Visual Studio], searching
- contacts [Office development in Visual Studio], searching
- searching contacts
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a4a9d52ae16b77b40461a314c6008f8cdd741bcd
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537638"
---
# <a name="how-to-programmatically-search-for-an-email-address-in-contacts"></a>Como: pesquisar programaticamente por um endereço de email nos contatos
  Este exemplo pesquisa uma pasta de contato para contatos que têm o nome de domínio **example.com** em seus endereços de email.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>Exemplo
 [!code-csharp[Trin_OL_SearchEmail#1](../vsto/codesnippet/CSharp/Trin_OL_SearchEmail/thisaddin.cs#1)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer:

- Os contatos que têm o nome de domínio **example.com** em seus endereços de email (por exemplo, `somebody@example.com` ), e que têm nomes e sobrenomes.

## <a name="see-also"></a>Consulte também
- [Trabalhar com itens de contato](../vsto/working-with-contact-items.md)
- [Como: enviar emails por meio de programação](../vsto/how-to-programmatically-send-e-mail-programmatically.md)
- [Como programaticamente acessar contatos do Outlook](../vsto/how-to-programmatically-access-outlook-contacts.md)
- [Como: adicionar programaticamente uma entrada aos contatos do Outlook](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)
