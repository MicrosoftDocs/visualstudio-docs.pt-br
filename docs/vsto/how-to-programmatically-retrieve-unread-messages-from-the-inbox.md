---
title: Obter mensagens não lidas da caixa de entrada programaticamente
description: Saiba como você pode usar o Visual Studio para recuperar programaticamente mensagens não lidas da sua caixa de entrada no Microsoft Outlook.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- e-mail [Office development in Visual Studio], unread mail
- Outlook [Office development in Visual Studio], unread mail
- unread e-mail
- mail items [Office development in Visual Studio], unread mail
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 82bd595b76a03ee730995e546fd9c4e827c95a53
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99953845"
---
# <a name="how-to-programmatically-retrieve-unread-messages-from-the-inbox"></a>Como: recuperar programaticamente mensagens não lidas da caixa de entrada
  Este exemplo recupera mensagens de email não lidas da **caixa de entrada** do Outlook e exibe o número de itens.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>Exemplo
 [!code-vb[Trin_Outlook_RL_UnreadItems#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_RL_UnreadItems/thisaddin.vb#1)]
 [!code-csharp[Trin_Outlook_RL_UnreadItems#1](../vsto/codesnippet/CSharp/Trin_Outlook_RL_UnreadItems/thisaddin.cs#1)]

## <a name="see-also"></a>Confira também
- [Trabalhar com itens de email](../vsto/working-with-mail-items.md)
- [Introdução à programação de suplementos do VSTO](../vsto/getting-started-programming-vsto-add-ins.md)
- [Como: criar programaticamente um item de email](../vsto/how-to-programmatically-create-an-e-mail-item.md)
- [Como: enviar emails por meio de programação](../vsto/how-to-programmatically-send-e-mail-programmatically.md)
- [Como executar programaticamente ações quando uma mensagem de email é recebida](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
