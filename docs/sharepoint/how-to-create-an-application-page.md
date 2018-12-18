---
title: 'Como: criar uma página de aplicativo | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- application pages [SharePoint development in Visual Studio], adding
- application pages [SharePoint development in Visual Studio], creating
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9f390ddf14925b43f1aa1d9e79db05e2aa64f234
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51296197"
---
# <a name="how-to-create-an-application-page"></a>Como: criar uma página de aplicativo
  Você pode criar uma página da web para um ou mais sites do SharePoint. No SharePoint, essas páginas são chamadas de páginas do aplicativo. Ao contrário de uma página do site, uma página de aplicativo contém código que é executado por trás da página. Para obter mais informações, consulte [criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md).  
  
### <a name="to-create-an-application-page"></a>Para criar uma página de aplicativo  
  
1.  No Visual Studio, abra ou crie um projeto do SharePoint.  
  
     Para obter mais informações, consulte [SharePoint modelos de item de projeto e projeto](../sharepoint/sharepoint-project-and-project-item-templates.md).  
  
2.  Na **Gerenciador de soluções**, escolha o nó do projeto.  
  
3.  Na barra de menus, escolha **Projeto** > **Adicionar Novo Item**.  
  
4.  No **Adicionar Novo Item** diálogo caixa, expanda o **SharePoint** nó e, em seguida, escolha o **2010** item.  
  
5.  Na lista de modelos do SharePoint, escolha **página de aplicativo**.  
  
6.  No **nome** caixa, especifique um nome para a página do aplicativo e, em seguida, escolha o **Add** botão.  
  
     Visual Studio adiciona várias pastas e arquivos ao seu projeto. Para obter mais informações sobre esses arquivos, consulte [criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md).  
  
     No **origem** exibição do designer Visual Web Developer, o arquivo de página ASP.NET é exibida. Você pode criar a página, adicionando controles a partir de **caixa de ferramentas** e colocando-os em espaços reservados de conteúdo. Para obter mais informações, consulte [exibição da fonte, o Designer de página da Web](/previous-versions/aspnet/ms178154\(v\=vs.100\)).  
  
7.  Se você quiser manipular eventos de controle, adicione código ao arquivo de código para a página de aplicativo.  
  
     O arquivo de código será exibida se você expandir o nó para o arquivo de página ASP.NET e tem um *. CS* ou *. vb* extensão, dependendo do idioma do projeto. Para obter um exemplo de ponta a ponta de como criar uma página de aplicativo, consulte [instruções passo a passo: criar uma página de aplicativo do SharePoint](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md).  
  
## <a name="see-also"></a>Consulte também
 [Criar páginas de aplicativo do SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md)   
 [Passo a passo: Criar uma página de aplicativo do SharePoint](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)  
  
