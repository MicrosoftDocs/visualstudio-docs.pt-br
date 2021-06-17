---
title: Como criar uma Web Part do SharePoint usando um designer | Microsoft Docs
titleSuffix: ''
description: Crie uma web part adicionando um item de web part visual a um projeto do SharePoint, que abre o designer do Desenvolvedor da Web Visual no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], designer
- Web Parts [SharePoint development in Visual Studio], adding
- Web Parts [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cbbb290af0029329910a23a71f68024ee0e5e5f4
ms.sourcegitcommit: 1f27f33852112702ee35fbc0c02fba37899e4cf5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2021
ms.locfileid: "112112379"
---
# <a name="how-to-create-a-sharepoint-web-part-by-using-a-designer"></a>Como criar uma Web Part do SharePoint usando um designer

  Você pode criar uma web part adicionando um item **do Visual Web Part** a qualquer projeto do SharePoint. Isso abre o designer do Desenvolvedor da Web Visual Visual Studio em que você pode adicionar controles e código à web part. As web parts visuais funcionam da mesma maneira que as web parts. A única diferença é que você projeta web parts visuais no designer do Visual Web Developer.

## <a name="to-create-a-project-for-visual-web-parts"></a>Para criar um projeto para web parts visuais

1. Na barra de menus, escolha **Arquivo**  > **Novo**  >  **Projeto**.
::: moniker range="=vs-2017"

2. Na caixa **de diálogo** Novo Projeto, em **Visual C#** ou **Visual Basic**, expanda o nó **Office/SharePoint** e escolha a **categoria Soluções do SharePoint.**

3. Na lista de modelos de projeto, escolha **SharePoint 2013 – Visual Web Part** e, em seguida, escolha o botão **OK.**

     O **Assistente de Personalização do SharePoint** é exibido.
::: moniker-end
::: moniker range=">=vs-2019"
2. Na caixa **de diálogo Criar um Novo Projeto,** selecione o Visual Web Part do *SharePoint** para a versão específica do SharePoint instalada. Por exemplo, se você tiver instalado o SharePoint 2019, selecione o **modelo SharePoint 2019 – Visual Web Part.**
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

3. Altere o nome do projeto se quiser e escolha o **botão** Criar.

::: moniker-end
4. Na página **Especificar o site** e o nível de segurança para depuração, especifique a URL de um site do SharePoint que está no computador local e escolha o **botão** Concluir.

     No **Gerenciador de Soluções**, uma web part é exibida. Depois de criar a web part no designer do Visual Web Developer, você a testará no site especificado.

### <a name="to-add-a-visual-web-part-to-an-existing-sharepoint-project"></a>Para adicionar uma web part visual a um projeto existente do SharePoint

1. Na barra de menus, escolha **Projeto**  >  **Adicionar Novo Item**.

2. Na caixa **de diálogo Adicionar Novo Item,** escolha o nó **Office/SharePoint.**

3. Na lista de modelos de projeto, escolha **Visual Web Part**, nomee escolha o **botão** Adicionar.

     No **Gerenciador de Soluções**, sua web part é exibida. Depois de criar a web part no designer do Visual Web Developer, você a testará no site especificado.

## <a name="see-also"></a>Confira também

- [Criar web parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md)
- [Como criar uma web part do SharePoint](../sharepoint/how-to-create-a-sharepoint-web-part.md)
- [Passo a passo: criar uma web part para SharePoint](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
- [Passo a passo: criar uma web part para SharePoint usando um designer](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
