---
title: Adicionando uma barra de ferramentas | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- toolbars [Visual Studio], adding to IDE
- IDE, adding toolbars
ms.assetid: 17302c25-6f59-4e97-8c85-54f95336a07f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: beb97356daf3c932470bf2598e58e1f5b40ea233
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904075"
---
# <a name="add-a-toolbar"></a>Adicionar uma barra de ferramentas
Este tutorial mostra como adicionar uma barra de ferramentas ao IDE do Visual Studio.

 Uma barra de ferramentas é uma faixa horizontal ou vertical que contém botões associados a comandos. Dependendo de sua implementação, uma barra de ferramentas no IDE pode ser reposicionada, encaixada em qualquer lado da janela principal do IDE, ou feita para permanecer na frente de outras janelas.

 Além disso, os usuários podem adicionar comandos a uma barra de ferramentas ou removê-los usando a caixa de diálogo **Personalizar** . Normalmente, as barras de ferramentas no VSPackages são personalizáveis pelo usuário. O IDE trata todas as personalizações e o VSPackage responde aos comandos. O VSPackage não precisa saber onde um comando está localizado fisicamente.

 Para obter mais informações sobre menus, consulte [comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md).

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-an-extension-with-a-toolbar"></a>Criar uma extensão com uma barra de ferramentas
 Crie um projeto VSIX denominado `IDEToolbar` . Adicione um modelo de item de comando de menu chamado **ToolbarTestCommand**. Para obter informações sobre como fazer isso, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).

## <a name="create-a-toolbar-for-the-ide"></a>Criar uma barra de ferramentas para o IDE

1. Em *ToolbarTestCommandPackage. vsct*, procure a seção símbolos. No elemento GuidSymbol chamado guidToolbarTestCommandPackageCmdSet, adicione declarações para uma barra de ferramentas e um grupo de barras de ferramentas, da seguinte maneira.

    ```xml
    <IDSymbol name="Toolbar" value="0x1000" />
    <IDSymbol name="ToolbarGroup" value="0x1050" />

    ```

2. Na parte superior da seção comandos, crie uma seção menus. Adicione um elemento de menu à seção menus para definir sua barra de ferramentas.

    ```xml
    <Menus>
        <Menu guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"
            type="Toolbar" >
            <CommandFlag>DefaultDocked</CommandFlag>
            <Strings>
                <ButtonText>Test Toolbar</ButtonText>
                <CommandName>Test Toolbar</CommandName>
            </Strings>
          </Menu>
    </Menus>
    ```

     As barras de ferramentas não podem ser aninhadas como submenus. Portanto, você não precisa atribuir um grupo pai. Além disso, você não precisa definir uma prioridade, pois o usuário pode mover barras de ferramentas. Normalmente, o posicionamento inicial de uma barra de ferramentas é definido programaticamente, mas alterações subsequentes pelo usuário são persistidas.

3. Na seção [grupos](../extensibility/groups-element.md) , após a entrada de grupo existente, defina um elemento de [grupo](../extensibility/group-element.md) para conter os comandos da barra de ferramentas.

    ```xml
    <Group guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup"
          priority="0x0000">
      <Parent guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"/>
    </Group>
    ```

4. Faça com que o botão apareça na barra de ferramentas. Na seção botões, substitua o bloco pai no botão pela barra de ferramentas. O bloco de botão resultante deve ter a seguinte aparência:

    ```xml
    <Button guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarTestCommandId" priority="0x0100" type="Button">
        <Parent guid= "guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup" />
                <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke ToolbarTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     Por padrão, se uma barra de ferramentas não tiver comandos, ela não será exibida.

5. Compile o projeto e comece a depuração. A instância experimental deve aparecer.

6. Clique com o botão direito do mouse na barra de menus do Visual Studio para obter a lista de barras de ferramentas. Selecione a **barra de ferramentas de teste**.

7. Agora você deve ver sua barra de ferramentas como um ícone à direita do ícone localizar nos arquivos. Ao clicar no ícone, você deverá ver uma caixa de mensagem que diz **ToolbarTestCommandPackage. Dentro de IDEToolbar. ToolbarTestCommand. MenuItemCallback ()**.

## <a name="see-also"></a>Confira também
- [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)
