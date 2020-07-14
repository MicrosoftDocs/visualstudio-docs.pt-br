---
title: Salvar anexos de itens de email do Outlook programaticamente
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], attachments
- e-mail [Office development in Visual Studio], attachments
- saving e-mail attachments
- mail items [Office development in Visual Studio], attachments
- attachments [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9fbe6099a8928397a7d885ac72c4f34da2da6af0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545880"
---
# <a name="how-to-programmatically-save-attachments-from-outlook-email-items"></a>Como: salvar com programação anexos de itens de email do Outlook

Este exemplo salva anexos de email em uma pasta especificada quando o email é recebido na caixa de entrada.

> [!IMPORTANT]
> Este exemplo só funcionará se você adicionar uma pasta chamada **TestFileSave** na raiz do diretório C.

[!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>Exemplo

[!code-csharp[Trin_OL_SaveAttachments#1](../vsto/codesnippet/CSharp/Trin_OL_SaveAttachments/thisaddin.cs#1)]

## <a name="see-also"></a>Confira também

- [Trabalhar com itens de email](../vsto/working-with-mail-items.md)
- [Como: recuperar programaticamente uma pasta por nome](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [Como executar programaticamente ações quando uma mensagem de email é recebida](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
- [Como: pesquisar programaticamente em uma pasta específica](../vsto/how-to-programmatically-search-within-a-specific-folder.md)
