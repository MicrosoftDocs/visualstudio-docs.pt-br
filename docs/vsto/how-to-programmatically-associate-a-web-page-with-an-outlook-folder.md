---
title: 'Como: associar programaticamente uma página da web uma pasta do Outlook'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- folders [Office development in Visual Studio], Web pages and
- Outlook [Office development in Visual Studio], Web pages attached to folders
- Web pages [Office development in Visual Studio], Outlook folders
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 2cb1ef525917288dc44609b899611db884da9073
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35256459"
---
# <a name="how-to-programmatically-associate-a-web-page-with-an-outlook-folder"></a>Como: associar programaticamente uma página da web uma pasta do Outlook
  Este exemplo verifica uma pasta chamada `HtmlView` no Microsoft Office Outlook. Se a pasta não existir, o código cria a pasta e atribui a uma página da Web a ela. Se a pasta existir, o código exibe o conteúdo da pasta.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[Trin_OL_HTMLFolder#1](../vsto/codesnippet/CSharp/Trin_OL_HTMLFolder/thisaddin.cs#1)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com pastas](../vsto/working-with-folders.md)   
 [Como: recuperar uma pasta por nome de forma programática](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)   
 [Como: criar itens de pasta personalizados programaticamente](../vsto/how-to-programmatically-create-custom-folder-items.md)  
  
  