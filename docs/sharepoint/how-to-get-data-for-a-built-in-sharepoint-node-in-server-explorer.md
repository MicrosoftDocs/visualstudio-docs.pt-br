---
title: Obter dados para o nó interno do SharePoint no Gerenciador de Servidores
titleSuffix: ''
description: Obtenha dados para o componente subjacente do SharePoint de um nó interno do SharePoint na janela Gerenciador de Servidores do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c58de345400c7b724a755839cb8baa1afc3cfce2
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217184"
---
# <a name="how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer"></a>Como: obter dados para um nó interno do SharePoint no Gerenciador de Servidores
  Para cada nó interno do SharePoint no **Gerenciador de servidores**, você pode obter dados para o componente subjacente do SharePoint que o nó representa. Para obter mais informações, consulte [estender o nó conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md).

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como obter dados para a lista do SharePoint subjacente que um nó de lista representa em **Gerenciador de servidores**. Por padrão, os nós da lista têm um **modo de exibição no item de** menu de contexto do navegador, no qual você pode clicar para abrir as listas em um navegador da Web. Este exemplo estende os nós da lista adicionando um **modo de exibição no** item de menu de contexto do Visual Studio que abre as listas diretamente no Visual Studio. O código acessa os dados da lista para o nó para obter a URL da lista a ser aberta no Visual Studio.

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextensionnodeinfo.vb" id="Snippet10":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextensionnodeinfo.cs" id="Snippet10":::

 Este exemplo usa o serviço de projeto do SharePoint para obter o <xref:EnvDTE.DTE> objeto usado para abrir listas no Visual Studio. Para obter mais informações sobre o serviço de projeto do SharePoint, consulte [usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md).

 Para obter mais informações sobre as tarefas básicas para criar uma extensão para um nó do SharePoint, consulte [como: estender um nó do SharePoint no Gerenciador de servidores](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md).

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer referências aos seguintes assemblies:

- EnvDTE

- Microsoft. VisualStudio. SharePoint

- Microsoft. VisualStudio. SharePoint. Explorer. Extensions

- System. ComponentModel. composição

## <a name="deploy-the-extension"></a>Implantar a extensão
 Para implantar a extensão de **Gerenciador de servidores** , crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly e quaisquer outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Confira também
- [Estenda o nó conexões do SharePoint no Gerenciador de Servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [Como: estender um nó do SharePoint no Gerenciador de Servidores](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [Usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md)
- [Implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
