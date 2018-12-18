---
title: Adicionando uma barra de ferramentas | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- toolbars [Visual Studio], adding to IDE
- IDE, adding toolbars
ms.assetid: 17302c25-6f59-4e97-8c85-54f95336a07f
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a2888ab6fade4893389af23ff456a63ffc5fbc40
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39151971"
---
# <a name="add-a-toolbar"></a>Adicionar uma barra de ferramentas
Este passo a passo mostra como adicionar uma barra de ferramentas ao IDE do Visual Studio.  
  
 Uma barra de ferramentas é uma faixa horizontal ou vertical que contém botões que estão associados aos comandos. Dependendo da sua implementação, uma barra de ferramentas no IDE pode ser reposicionada, encaixada em qualquer lado da janela principal do IDE ou feita estar na frente de outras janelas.  
  
 Além disso, os usuários podem adicionar comandos a uma barra de ferramentas ou removê-las dela usando o **personalizar** caixa de diálogo. Normalmente, as barras de ferramentas em VSPackages são personalizáveis pelo usuário. O IDE manipula toda a personalização e o VSPackage responde a comandos. O VSPackage não precisa saber em que um comando é localizado fisicamente.  
  
 Para obter mais informações sobre menus, consulte [comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="create-an-extension-with-a-toolbar"></a>Criar uma extensão com uma barra de ferramentas  
 Crie um projeto do VSIX chamado `IDEToolbar`. Adicionar um modelo de item de comando de menu chamado **ToolbarTestCommand**. Para obter informações sobre como fazer isso, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
## <a name="create-a-toolbar-for-the-ide"></a>Criar uma barra de ferramentas para o IDE  
  
1.  Na *ToolbarTestCommandPackage.vsct*, procure a seção de símbolos. No elemento GuidSymbol chamado guidToolbarTestCommandPackageCmdSet, adicione as declarações para uma barra de ferramentas e um grupo de barra de ferramentas, da seguinte maneira.  
  
    ```xml  
    <IDSymbol name="Toolbar" value="0x1000" />  
    <IDSymbol name="ToolbarGroup" value="0x1050" />  
  
    ```  
  
2.  Na parte superior da seção de comandos, crie uma seção de Menus. Adicione um elemento do Menu para a seção de Menus para definir sua barra de ferramentas.  
  
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
  
     Barras de ferramentas não podem ser aninhadas, como submenus. Portanto, não é necessário atribuir um grupo pai. Além disso, você não precisa definir uma prioridade, porque o usuário pode mover as barras de ferramentas. Normalmente, o posicionamento inicial de uma barra de ferramentas é definido por meio de programação, mas as alterações subsequentes pelo usuário são persistentes.  
  
3.  No [grupos](../extensibility/groups-element.md) seção, após a entrada de grupo existente, defina uma [grupo](../extensibility/group-element.md) elemento para conter os comandos da barra de ferramentas.  
  
    ```xml  
    <Group guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup"  
          priority="0x0000">  
      <Parent guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"/>  
    </Group>  
    ```  
  
4.  Fazer com que o botão aparecem na barra de ferramentas. Na seção de botões, substitua o bloco pai no botão à barra de ferramentas. O bloco de botão resultante deve ter esta aparência:  
  
    ```xml  
    <Button guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarTestCommandId" priority="0x0100" type="Button">  
        <Parent guid= "guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup" />  
                <Icon guid="guidImages" id="bmpPic1" />  
        <Strings>  
            <ButtonText>Invoke ToolbarTestCommand</ButtonText>  
        </Strings>  
    </Button>  
    ```  
  
     Por padrão, se uma barra de ferramentas não tem nenhum comando, ele não aparece.  
  
5.  Compile o projeto e comece a depuração. A instância experimental deve aparecer.  
  
6.  Clique com botão direito a barra de menus do Visual Studio para obter uma lista das barras de ferramentas. Selecione **barra de ferramentas de teste**.  
  
7.  Agora você deve ver sua barra de ferramentas como um ícone à direita de localizar no ícone de arquivos. Quando você clica no ícone, você verá uma caixa de mensagem que diz **ToolbarTestCommandPackage. Dentro de IDEToolbar.ToolbarTestCommand.MenuItemCallback()**.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)