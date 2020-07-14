---
title: Criar controle de usuário para página de aplicativo do SharePoint ou Web Part
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- user controls [SharePoint development in Visual Studio], creating
- user controls [SharePoint development in Visual Studio], adding
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2fbf1b646ae9e7fb697fcab93adfb8661a4372c6
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016978"
---
# <a name="how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part"></a>Como: criar um controle de usuário para uma página de aplicativo do SharePoint ou Web Part
  Você pode criar controles de usuário personalizados que fornecem funcionalidade personalizada para sua solução do SharePoint e pode reutilizar essa funcionalidade em seu projeto. Você pode incluir os controles de usuário em uma página da Web Part ou do aplicativo, adicionar outros controles ASP.NET e controles do SharePoint e definir propriedades e métodos para o controle. Para obter mais informações sobre controles de usuário, consulte [criar controles reutilizáveis para Web Parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md) e controles de [usuário e controles de servidor no SharePoint](https://blogs.msdn.microsoft.com/kaevans/2011/04/28/user-controls-and-server-controls-in-sharepoint/).

### <a name="to-create-a-user-control-for-sharepoint"></a>Para criar um controle de usuário para o SharePoint

1. No Visual Studio, abra ou crie um projeto do SharePoint.

     Consulte [projeto do SharePoint e modelos de item de projeto](../sharepoint/sharepoint-project-and-project-item-templates.md).

2. Em **Gerenciador de soluções**, escolha o nó do projeto.

3. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

     A caixa de diálogo **Adicionar Novo Item** é aberta.

4. No painel **instalado** , escolha o nó **Office/SharePoint** .

5. Na lista de modelos do SharePoint, escolha **controle de usuário (somente solução de farm)**.

    > [!NOTE]
    > Os controles de usuário só funcionam em soluções de farm.

6. Na caixa **nome** , especifique um nome para o controle de usuário e, em seguida, escolha o botão **Adicionar** .

     O Visual Studio adiciona várias pastas e arquivos ao seu projeto. Para obter mais informações sobre esses arquivos, consulte [criar controles reutilizáveis para Web Parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md).

     Por padrão, o arquivo de controle de usuário aparece na exibição de **origem** do designer do Visual Web Developer. Nessa exibição, você pode editar a marcação XML do controle. Você pode alternar para o modo de exibição de **design** se quiser criar o controle visualmente arrastando controles da **caixa de ferramentas**. Consulte [exibição de design, designer de página da Web](/previous-versions/aspnet/ms178149\(v\=vs.100\)).

7. Se você quiser manipular eventos que ocorrem no controle, adicione o código ao arquivo de código do controle de usuário.

     Esse arquivo aparece em **Gerenciador de soluções** no arquivo de controle de usuário e tem uma extensão *. cs* ou *. vb* , dependendo do idioma do projeto.

## <a name="see-also"></a>Consulte também
- [Criar controles reutilizáveis para Web Parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
- [Criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md)
- [Criar Web Parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md)
