---
title: 'Como: enviar email'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- mail items [Office development in Visual Studio], sending e-mail
- Outlook [Office development in Visual Studio], creating e-mail
- Outlook [Office development in Visual Studio], sending e-mail
- e-mail [Office development in Visual Studio], sending
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 32977852ffbc4bb1411ed699cc97bb54035fada4
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670714"
---
# <a name="how-to-programmatically-send-email"></a>Como: enviar email  
  Este exemplo envia uma mensagem de email para contatos que têm o nome de domínio **exemplo.com** em seus endereços de email.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[Trin_OL_ProgramEmail#1](../vsto/codesnippet/CSharp/Trin_OL_ProgramEMail/thisaddin.cs#1)]  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo requer:  
  
-   Contatos que têm o nome de domínio **exemplo.com** em seus endereços de email.  
  
## <a name="robust-programming"></a>Programação robusta  
 Não remova o código de filtro que procura o nome de domínio **exemplo.com**. Sua solução enviará mensagens de email para todos os seus contatos, se você remover o filtro.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com itens de email](../vsto/working-with-mail-items.md)   
 [Como: criar programaticamente um item de email](../vsto/how-to-programmatically-create-an-e-mail-item.md)   
 [Como: acessar contatos do Outlook de forma programática](../vsto/how-to-programmatically-access-outlook-contacts.md)   
 [Como: executar ações programaticamente quando uma mensagem de email é recebida](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)  
  
  