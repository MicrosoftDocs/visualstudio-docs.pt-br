---
title: Estendendo menus e comandos | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus, common tasks
- VSPackages, menu tasks
- .vsct files, common menu tasks
ms.assetid: 7b2be4b9-e3fe-4412-874f-ae72ebc84c4b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c344d996c70012ef1516fa2bebe52394739bea35
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768584"
---
# <a name="extend-menus-and-commands"></a>Estender menus e comandos
Os comandos são a maneira como você adiciona ações e processos ao Visual Studio. Na maioria dos casos, os comandos são exibidos em menus ou barras de ferramentas. O modelo de projeto VSPackage mostra como implementar um comando muito básico. Para uma implementação um pouco mais longa, mas ainda básica, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).

 Para obter mais informações sobre comandos, menus e barras de ferramentas do Visual Studio, consulte [comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md).

 Os comandos, menus e barras de ferramentas são definidos no arquivo *. vsct* que faz parte de projetos VSPackage. Você pode encontrar informações sobre o IDE do Visual Studio e o arquivo *. vsct* em [como VSPackages adicionar elementos da interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md).

 Os tópicos a seguir explicam como adicionar diferentes tipos de comandos, menus e barras de ferramentas.

## <a name="in-this-section"></a>Nesta seção
- [Adicionar um menu à barra de menus do Visual Studio](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md) Explica como adicionar um menu à barra de menus superior do Visual Studio.

- [Associar atalhos de teclado a itens de menu](../extensibility/binding-keyboard-shortcuts-to-menu-items.md) Explica como adicionar um atalho de teclado (como CTRL + 3) a um item de menu.

- [Adicionar um submenu a um menu](../extensibility/adding-a-submenu-to-a-menu.md) Explica como adicionar um submenu ao menu superior.

- [Adicionar uma lista usada mais recentemente a um submenu](../extensibility/adding-a-most-recently-used-list-to-a-submenu.md) Explica como adicionar uma lista usada mais recentemente.

- [Criar grupos de botões reutilizáveis](../extensibility/creating-reusable-groups-of-buttons.md) Descreve como agrupar itens de comando para que eles possam ser incluídos em vários menus.

- [Adicionar ícones a comandos de menu](../extensibility/adding-icons-to-menu-commands.md) Descreve como adicionar um ícone a um comando em uma barra de ferramentas e em um menu.

- [Alterar o texto de um comando de menu](../extensibility/changing-the-text-of-a-menu-command.md) Descreve o uso do `TextChanges` sinalizador para permitir que um item de menu seja alterado dinamicamente.

- [Alterar a aparência de um comando](../extensibility/changing-the-appearance-of-a-command.md) Descreve como habilitar ou desabilitar um comando dinamicamente.

- [Atualizar a interface do usuário](../extensibility/updating-the-user-interface.md) Descreve como forçar uma atualização da interface do usuário para refletir as alterações recentes.

- [Comandos do menu localizar](../extensibility/localizing-menu-commands.md) Explica como localizar comandos de menu.
