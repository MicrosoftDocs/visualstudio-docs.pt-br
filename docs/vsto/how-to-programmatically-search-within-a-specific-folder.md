---
title: 'Como: pesquisar programaticamente em uma pasta específica'
description: Saiba como você pode usar o Visual Studio para pesquisar programaticamente em uma pasta específica do Microsoft Outlook.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook folders [Office development in Visual Studio], searching
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b25880420e23b82f6f63ab28ef5f1f93429bdd8c
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824751"
---
# <a name="how-to-programmatically-search-within-a-specific-folder"></a>Como: pesquisar programaticamente em uma pasta específica
  Este exemplo de código usa `Find` os `FindNext` métodos e para Pesquisar texto no campo assunto das mensagens de email que estão na **caixa de entrada**. Esse método usa um filtro de cadeia de caracteres para verificar a letra T como a letra inicial do `Subject` texto.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>Exemplo
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_SearchFolder/thisaddin.cs" id="Snippet1":::

## <a name="see-also"></a>Consulte também
- [Trabalhar com pastas](../vsto/working-with-folders.md)
- [Visão geral do modelo de objeto do Outlook](../vsto/outlook-object-model-overview.md)
- [Como: recuperar programaticamente uma pasta por nome](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
