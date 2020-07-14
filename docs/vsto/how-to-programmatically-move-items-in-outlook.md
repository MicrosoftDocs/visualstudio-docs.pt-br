---
title: 'Como: mover itens programaticamente no Outlook'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook folders [Office development in Visual Studio], moving items
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 97f686a47d18fa91909de489f12f9c7a8c1306d1
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85519906"
---
# <a name="how-to-programmatically-move-items-in-outlook"></a>Como: mover itens programaticamente no Outlook
  Este exemplo move as mensagens de email não lidas da **caixa de entrada** para uma pasta chamada **Test**. O exemplo move apenas as mensagens que têm a palavra **Test** no `Subject` campo.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>Exemplo
 [!code-csharp[Trin_OL_MoveItems#1](../vsto/codesnippet/CSharp/Trin_OL_MoveItems/thisaddin.cs#1)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer:

- Uma pasta de email do Outlook chamada **Test**.

- Uma mensagem de email que chega com a palavra **Test** no `Subject` campo.

## <a name="see-also"></a>Confira também
- [Trabalhar com pastas](../vsto/working-with-folders.md)
- [Como: recuperar programaticamente uma pasta por nome](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [Como: pesquisar programaticamente em uma pasta específica](../vsto/how-to-programmatically-search-within-a-specific-folder.md)
- [Como executar programaticamente ações quando uma mensagem de email é recebida](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
