---
title: Estendendo as ferramentas do SharePoint no Visual Studio | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio, extending tools
- extensibility [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, extending tools
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7dc0cc0d0af73d032d870629877b62c94e6b347b
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016038"
---
# <a name="extend-the-sharepoint-tools-in-visual-studio"></a>Estenda as ferramentas do SharePoint no Visual Studio
  As ferramentas do SharePoint no Visual Studio atendem aos requisitos de muitos cenários de desenvolvimento de aplicativos. No entanto, você pode descobrir casos em que eles não fornecem funcionalidade que você ou outros desenvolvedores precisam. Nesses casos, você pode estender as ferramentas do SharePoint para criar a funcionalidade de que precisa.

## <a name="how-to-extend-the-sharepoint-tools"></a>Como estender as ferramentas do SharePoint
 Você pode estender o sistema de projeto do SharePoint e o nó **conexões do SharePoint** na janela **Gerenciador de servidores** .

### <a name="extend-the-sharepoint-project-system"></a>Estender o sistema de projeto do SharePoint
 O Visual Studio inclui um conjunto de modelos de projeto e modelos de item que você pode usar para criar soluções do SharePoint. Por exemplo, há modelos para receptores de eventos, definições de lista, fluxos de trabalho e Web Parts. No entanto, você também pode definir seus próprios tipos de itens de projeto do SharePoint para criar componentes do SharePoint, como campos ou ações personalizadas. Você também pode criar extensões para os tipos de item de projeto do SharePoint que já estão instalados no Visual Studio e pode criar extensões para projetos do SharePoint.

 Para obter mais informações, consulte [estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md).

### <a name="extend-the-sharepoint-connections-node-in-server-explorer"></a>Estenda o nó conexões do SharePoint no Gerenciador de Servidores
 No Visual Studio, você pode usar o nó **conexões do SharePoint** na janela **Gerenciador de servidores** para exibir muitos dos componentes de um ou mais sites locais do SharePoint em um modo de exibição de árvore hierárquica. Você também pode estender o nó **conexões do SharePoint** das seguintes maneiras:

- Adicionando seus próprios nós. Isso será útil se você quiser exibir componentes de sites do SharePoint que não são exibidos por padrão.

- Estendendo os nós existentes. Por exemplo, você pode adicionar um novo nó filho a um nó existente ou pode adicionar um item de menu de atalho a um nó e executar tarefas quando um desenvolvedor clicar no item de menu.

  Para obter mais informações, consulte [estender o nó conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md).

## <a name="development-computer-requirements"></a>Requisitos do computador de desenvolvimento
 Para criar extensões para as ferramentas do SharePoint, seu computador de desenvolvimento deve atender aos mesmos requisitos para criar soluções do SharePoint no Visual Studio.

 Também recomendamos que você instale o [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)] . O SDK inclui modelos e ferramentas de projeto que você pode usar para estender o Visual Studio. Em particular, o SDK inclui um modelo de projeto que você pode usar para criar facilmente um pacote de VSIX (Visual Studio Extension). Os pacotes VSIX são a maneira preferida de implantar extensões do Visual Studio no Visual Studio. Todas as extensões de ferramentas do SharePoint devem ser implantadas usando pacotes VSIX. Todos os passo a passos nesta documentação pressupõem que você tenha o [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)] instalado.

 Para instalar o SDK do Visual Studio, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md). Para obter mais informações sobre extensões do Visual Studio, consulte [iniciando o desenvolvimento de extensões do Visual Studio](../extensibility/starting-to-develop-visual-studio-extensions.md).

## <a name="see-also"></a>Consulte também

- [Visão geral do modelo de programação das extensões de ferramentas do SharePoint](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
- [Estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md)
- [Estenda o nó conexões do SharePoint no Gerenciador de Servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [Conceitos e recursos de programação para extensões de ferramentas do SharePoint](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
- [Referência &#40;extensibilidade de ferramentas do SharePoint&#41;](../sharepoint/reference-sharepoint-tools-extensibility.md)
- [Extensões de depuração para as ferramentas do SharePoint no Visual Studio](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)
- [Implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)