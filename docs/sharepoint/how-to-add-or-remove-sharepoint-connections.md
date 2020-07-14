---
title: 'Como: Adicionar ou remover conexões do SharePoint | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, browsing SharePoint sites
- SharePoint development in Visual Studio, SharePoint Connections
- SharePoint Connections [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: cec1389294c8baf169db055acb87619114d7d19b
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014573"
---
# <a name="how-to-add-or-remove-sharepoint-connections"></a>Como: Adicionar ou remover conexões do SharePoint
  Gerenciador de Servidores permite que você procure sites do SharePoint, bem como conexões de dados. No entanto, antes de poder procurar o conteúdo de um site do SharePoint, você deve adicioná-lo ao nó **conexões do SharePoint** .

### <a name="to-add-a-sharepoint-site-to-the-sharepoint-connections-node"></a>Para adicionar um site do SharePoint ao nó conexões do SharePoint

1. Na barra de menus, escolha **Exibir**, **Gerenciador de servidores**.

2. Em **Gerenciador de servidores**, escolha o nó **conexões do SharePoint** e, na barra de menus, escolha **ferramentas**  >  **Adicionar conexão do SharePoint**.

3. Na caixa **Adicionar conexão do SharePoint** , insira o [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] para o site do SharePoint (por exemplo, http://testserver/sites/unittests) .

### <a name="to-delete-a-sharepoint-site-from-the-sharepoint-connections-node"></a>Para excluir um site do SharePoint do nó conexões do SharePoint

1. Na barra de menus, escolha **Exibir**, **Gerenciador de Servidores** para abrir **Gerenciador de servidores**.

2. Expanda o nó **conexões do SharePoint** para revelar o site do SharePoint que você deseja excluir do **Gerenciador de servidores**.

3. Escolha o site e, na barra de menus, escolha **Editar**  >  **excluir**.

    > [!NOTE]
    > Esta etapa não exclui o site subjacente; Ele exclui somente a conexão de **Gerenciador de servidores**.

## <a name="see-also"></a>Consulte também
- [Procurar conexões do SharePoint usando Gerenciador de Servidores](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
