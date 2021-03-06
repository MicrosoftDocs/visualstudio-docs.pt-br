---
title: 'Como: criar uma página de aplicativo | Microsoft Docs'
description: Crie uma página da Web do ASP.NET (também conhecida como página de aplicativo) no Visual Studio para um ou mais sites do SharePoint.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application pages [SharePoint development in Visual Studio], adding
- application pages [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 74e7aab4cbc012afbf045672dbf4af248ada4c61
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99925626"
---
# <a name="how-to-create-an-application-page"></a>Como: criar uma página de aplicativo
  Você pode criar uma página da Web do ASP.NET para um ou mais sites do SharePoint. No SharePoint, essas páginas são chamadas de páginas de aplicativo. Ao contrário de uma página do site, uma página de aplicativo contém o código que é executado atrás da página. Para obter mais informações, consulte [criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md).

### <a name="to-create-an-application-page"></a>Para criar uma página de aplicativo

1. No Visual Studio, abra ou crie um projeto do SharePoint.

     Para obter mais informações, consulte [projeto do SharePoint e modelos de item de projeto](../sharepoint/sharepoint-project-and-project-item-templates.md).

2. Em **Gerenciador de soluções**, escolha o nó do projeto.

3. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

4. Na caixa de diálogo **Adicionar novo item** , expanda o nó **SharePoint** e escolha o item **2010** .

5. Na lista de modelos do SharePoint, escolha **página do aplicativo**.

6. Na caixa **nome** , especifique um nome para a página do aplicativo e, em seguida, escolha o botão **Adicionar** .

     O Visual Studio adiciona várias pastas e arquivos ao seu projeto. Para obter mais informações sobre esses arquivos, consulte [criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md).

     Na exibição de **origem** do designer do Visual Web Developer, o arquivo de página ASP.net é exibido. Você pode criar a página adicionando controles da caixa de **ferramentas** e colocando-os em espaços reservados de conteúdo. Para obter mais informações, consulte [Source View, Web page designer](/previous-versions/aspnet/ms178154\(v\=vs.100\)).

7. Se você quiser manipular eventos de controle, adicione o código ao arquivo de código para a página do aplicativo.

     O arquivo de código será exibido se você expandir o nó para o arquivo de página ASP.NET e tiver uma extensão *. cs* ou *. vb* , dependendo do idioma do projeto. Para obter um exemplo de ponta a ponta de como criar uma página de aplicativo, consulte [Walkthrough: criar uma página de aplicativo do SharePoint](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md).

## <a name="see-also"></a>Confira também
- [Criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md)
- [Walkthrough: criar uma página de aplicativo do SharePoint](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)
