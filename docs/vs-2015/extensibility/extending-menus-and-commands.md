---
title: Estendendo os Menus e comandos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- menus, common tasks
- VSPackages, menu tasks
- .vsct files, common menu tasks
ms.assetid: 7b2be4b9-e3fe-4412-874f-ae72ebc84c4b
caps.latest.revision: 50
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 36dcc3742b745f8933f340b8df966b1f621d6998
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51793146"
---
# <a name="extending-menus-and-commands"></a>Estendendo comandos e menus
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Comandos são a maneira de adicionar ações e processos no Visual Studio. Na maioria dos casos, comandos são exibidos em menus ou barras de ferramentas. O modelo de projeto de VSPackage mostra como implementar um comando muito básico. Para uma implementação de um pouco maior, mas ainda básica, consulte [criar uma extensão com um comando de Menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
 Para obter mais informações sobre comandos, menus e barras de ferramentas do Visual Studio, consulte [comandos, Menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md).  
  
 Comandos, menus e barras de ferramentas são definidas no arquivo. VSCT que faz parte dos projetos de VSPackage. Você pode encontrar informações sobre o IDE do Visual Studio e o arquivo. VSCT na [como os VSPackages adicionar elementos Interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md).  
  
 Os tópicos a seguir explicam como adicionar tipos diferentes de comandos, menus e barras de ferramentas.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Adicionar um menu à barra de menus do Visual Studio](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)  
 Explica como adicionar um menu na parte superior a barra de menus do Visual Studio.  
  
 [Associar atalhos de teclado aos itens de menu](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)  
 Explica como adicionar um atalho de teclado (por exemplo, CTRL + 3) a um item de menu.  
  
 [Adicionar um submenu a um menu](../extensibility/adding-a-submenu-to-a-menu.md)  
 Explica como adicionar um submenu no menu superior.  
  
 [Adicionar uma lista de usados recentemente a um submenu](../extensibility/adding-a-most-recently-used-list-to-a-submenu.md)  
 Explica como adicionar uma lista de usados recentemente.  
  
 [Criar grupos reutilizáveis de botões](../extensibility/creating-reusable-groups-of-buttons.md)  
 Descreve como agrupar itens de comando para que eles possam ser incluídos em vários menus.  
  
 [Adicionar ícones a comandos de menu](../extensibility/adding-icons-to-menu-commands.md)  
 Descreve como adicionar um ícone para um comando em uma barra de ferramentas e um menu.  
  
 [Alterar o texto de um comando de menu](../extensibility/changing-the-text-of-a-menu-command.md)  
 Descreve o uso do `TextChanges` sinalizador para ativar um item de menu a ser alterado dinamicamente.  
  
 [Alterar a aparência de um comando](../extensibility/changing-the-appearance-of-a-command.md)  
 Descreve como habilitar ou desabilitar um comando.  
  
 [Atualizar a interface do usuário](../extensibility/updating-the-user-interface.md)  
 Descreve como forçar uma atualização da interface do usuário para refletir as alterações recentes.  
  
 [Localizar os comandos de menu](../extensibility/localizing-menu-commands.md)  
 Explica como localizar os comandos de menu.  
  
## <a name="related-sections"></a>Seções relacionadas

