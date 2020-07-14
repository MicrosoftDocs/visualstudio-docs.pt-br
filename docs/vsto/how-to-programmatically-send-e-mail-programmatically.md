---
title: 'Como: enviar emails por meio de programação'
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- mail items [Office development in Visual Studio], sending e-mail
- Outlook [Office development in Visual Studio], creating e-mail
- Outlook [Office development in Visual Studio], sending e-mail
- e-mail [Office development in Visual Studio], sending
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c56527f18857ad3c4ac82060ffd5794b72ac017c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543254"
---
# <a name="how-to-programmatically-send-email"></a>Como: enviar emails por meio de programação
  Este exemplo envia uma mensagem de email para contatos que têm o nome de domínio **example.com** em seus endereços de email.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="example"></a>Exemplo
 [!code-csharp[Trin_OL_ProgramEmail#1](../vsto/codesnippet/CSharp/Trin_OL_ProgramEMail/thisaddin.cs#1)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer:

- Contatos que têm o nome de domínio **example.com** em seus endereços de email.

## <a name="robust-programming"></a>Programação robusta
 Não remova o código de filtro que procura o nome de domínio **example.com**. Sua solução enviará mensagens de email para todos os seus contatos se você remover o filtro.

## <a name="see-also"></a>Confira também
- [Trabalhar com itens de email](../vsto/working-with-mail-items.md)
- [Como: criar programaticamente um item de email](../vsto/how-to-programmatically-create-an-e-mail-item.md)
- [Como programaticamente acessar contatos do Outlook](../vsto/how-to-programmatically-access-outlook-contacts.md)
- [Como executar programaticamente ações quando uma mensagem de email é recebida](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
