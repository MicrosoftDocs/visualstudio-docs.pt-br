---
title: Localizar um endereço de email nos contatos de forma programática
description: Saiba como você pode usar o Visual Studio para encontrar programaticamente um endereço de email nos contatos do Microsoft Outlook.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 43baafee82cf38dfd346ebe50e9b348857a3fdc4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99920464"
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
