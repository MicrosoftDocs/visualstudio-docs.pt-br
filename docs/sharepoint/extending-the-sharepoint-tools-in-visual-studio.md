---
title: Estendendo as ferramentas do SharePoint no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio, extending tools
- extensibility [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, extending tools
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f360982f26cf2eb9ffe26678743bb514d9606ae7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49890667"
---
# <a name="extend-the-sharepoint-tools-in-visual-studio"></a>Estender as ferramentas do SharePoint no Visual Studio
  As ferramentas do SharePoint no Visual Studio atender os requisitos de muitos cenários de desenvolvimento de aplicativo. No entanto, talvez você descubra os casos em que eles não fornecem a funcionalidade que você ou outros desenvolvedores exigem. Nesses casos, você pode estender as ferramentas do SharePoint para criar a funcionalidade que você precisa.

## <a name="how-to-extend-the-sharepoint-tools"></a>Como estender as ferramentas do SharePoint
 Você pode estender o sistema de projeto do SharePoint e o **conexões do SharePoint** nó na **Server Explorer** janela.

### <a name="extend-the-sharepoint-project-system"></a>Estender o sistema de projeto do SharePoint
 Visual Studio inclui um conjunto de modelos de projeto e modelos de item que você pode usar para criar soluções do SharePoint. Por exemplo, há modelos para receptores de evento, as definições de lista, fluxos de trabalho e Web Parts. No entanto, você também pode definir seus próprios tipos de itens de projeto do SharePoint para a criação de componentes do SharePoint, como campos ou ações personalizadas. Você também pode criar extensões para tipos de item de projeto do SharePoint que já estão instaladas no Visual Studio, e você pode criar extensões para projetos do SharePoint.

 Para obter mais informações, consulte [estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md).

### <a name="extend-the-sharepoint-connections-node-in-server-explorer"></a>Estender o nó de conexões do SharePoint no Gerenciador de servidores
 No Visual Studio, você pode usar o **conexões do SharePoint** nó na **Server Explorer** janela para exibir muitos dos componentes de um ou mais sites locais do SharePoint em uma exibição de árvore hierárquica. Você também pode estender a **conexões do SharePoint** nó das seguintes maneiras:

- Adicionando seus próprios nós. Isso é útil se você quiser exibir componentes de sites do SharePoint que não são exibidos por padrão.

- Estendendo nós existentes. Por exemplo, você pode adicionar um novo nó filho a um nó existente, ou você pode adicionar um item de menu de atalho a um nó e executar tarefas quando um desenvolvedor clica no item de menu.

  Para obter mais informações, consulte [estender o nó de conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md).

## <a name="development-computer-requirements"></a>Requisitos do computador de desenvolvimento
 Para criar extensões para as ferramentas do SharePoint, seu computador de desenvolvimento deve atender os mesmos requisitos para a criação de soluções do SharePoint no Visual Studio.

 Também recomendamos que você instale o [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]. O SDK inclui ferramentas que você pode usar para estender o Visual Studio e modelos de projeto. Em particular, o SDK inclui um modelo de projeto, que você pode usar para criar facilmente um pacote de extensão VSIX (Visual Studio). Pacotes VSIX são a maneira preferencial para implantar as extensões do Visual Studio no Visual Studio. Todas as extensões de ferramentas do SharePoint devem ser implantadas usando pacotes VSIX. Todas a instruções passo a passo nesta documentação pressupõem que você tenha o [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)] instalado.

 Para instalar o SDK do Visual Studio, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md). Para obter mais informações sobre extensões do Visual Studio, consulte [começando a desenvolver extensões do Visual Studio](../extensibility/starting-to-develop-visual-studio-extensions.md).

## <a name="see-also"></a>Consulte também

- [Extensões de ferramentas de visão geral do modelo de programação do SharePoint](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
- [Estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md)
- [Estender o nó de conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [Conceitos de programação e recursos para extensões de ferramentas do SharePoint](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
- [Referência de &#40;extensibilidade de ferramentas do SharePoint&#41;](../sharepoint/reference-sharepoint-tools-extensibility.md)
- [Depurar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)
- [Implantar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)