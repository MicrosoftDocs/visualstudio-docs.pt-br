---
title: Adicionando uma barra de ferramentas a uma janela de ferramentas | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tool windows, adding toolbars
- toolbars [Visual Studio], adding to tool windows
ms.assetid: 172f64b3-87f8-4292-9c1c-65bffa2b0970
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e5351fe6a713c217f8fca20d6740b542dc75f053
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904131"
---
# <a name="add-a-toolbar-to-a-tool-window"></a>Adicionar uma barra de ferramentas a uma janela de ferramentas
Este tutorial mostra como adicionar uma barra de ferramentas a uma janela de ferramentas.

 Uma barra de ferramentas é uma faixa horizontal ou vertical que contém botões associados a comandos. O comprimento de uma barra de ferramentas em uma janela de ferramentas é sempre igual à largura ou altura da janela de ferramentas, dependendo de onde a barra de ferramentas está encaixada.

 Ao contrário das barras de ferramentas no IDE, uma barra de ferramentas em uma janela de ferramentas deve ser encaixada e não pode ser movida ou personalizada. Se o VSPackage for escrito em código umanaged, a barra de ferramentas poderá ser encaixada em qualquer borda.

 Para obter mais informações sobre como adicionar uma barra de ferramentas, consulte [adicionando uma barra de ferramentas](../extensibility/adding-a-toolbar.md).

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-toolbar-for-a-tool-window"></a>Criar uma barra de ferramentas para uma janela de ferramentas

1. Crie um projeto VSIX chamado `TWToolbar` que tenha um comando de menu chamado **TWTestCommand** e uma janela de ferramentas chamada **TestToolWindow**. Para obter mais informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md) e [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md). Você precisa adicionar o modelo de item de comando antes de adicionar o modelo de janela de ferramentas.

2. Em *TWTestCommandPackage. vsct*, procure a seção símbolos. No nó GuidSymbol chamado guidTWTestCommandPackageCmdSet, declare uma barra de ferramentas e um grupo de barras de ferramentas, da seguinte maneira.

    ```xml
    <IDSymbol name="TWToolbar" value="0x1000" />
    <IDSymbol name="TWToolbarGroup" value="0x1050" />
    ```

3. Na parte superior da `Commands` seção, crie uma `Menus` seção. Adicione um `Menu` elemento para definir a barra de ferramentas.

    ```xml
    <Menus>
        <Menu guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" type="ToolWindowToolbar">
            <CommandFlag>DefaultDocked</CommandFlag>
            <Strings>
                <ButtonText>Test Toolbar</ButtonText>
                <CommandName>Test Toolbar</CommandName>
            </Strings>
        </Menu>
    </Menus>
    ```

     As barras de ferramentas não podem ser aninhadas como submenus. Portanto, você não precisa atribuir um pai. Além disso, você não precisa definir uma prioridade, pois o usuário pode mover barras de ferramentas. Normalmente, o posicionamento inicial de uma barra de ferramentas é definido programaticamente, mas alterações subsequentes pelo usuário são persistidas.

4. Na seção grupos, defina um grupo para conter os comandos da barra de ferramentas.

    ```xml

    <Group guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" priority="0x0000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" />
    </Group>
    ```

5. Na seção botões, altere o pai do elemento botão existente para o grupo barra de ferramentas para que a barra de ferramentas seja exibida.

    ```xml
    <Button guid="guidTWTestCommandPackageCmdSet" id="TWTestCommandId" priority="0x0100" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke TWTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     Por padrão, se uma barra de ferramentas não tiver comandos, ela não será exibida.

     Como a nova barra de ferramentas não é adicionada automaticamente à janela de ferramentas, a barra de ferramentas deve ser adicionada explicitamente. Isso é abordado na próxima seção.

## <a name="add-the-toolbar-to-the-tool-window"></a>Adicionar a barra de ferramentas à janela de ferramentas

1. Em *TWTestCommandPackageGuids.cs* , adicione as linhas a seguir.

    ```csharp
    public const string guidTWTestCommandPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const int TWToolbar = 0x1000;
    ```

2. Em *TestToolWindow.cs* , adicione a seguinte instrução using.

    ```csharp
    using System.ComponentModel.Design;
    ```

3. No Construtor TestToolWindow, adicione a linha a seguir.

    ```csharp
    this.ToolBar = new CommandID(new Guid(TWTestCommandPackageGuids.guidTWTestCommandPackageCmdSet), TWTestCommandPackageGuids.TWToolbar);
    ```

## <a name="test-the-toolbar-in-the-tool-window"></a>Testar a barra de ferramentas na janela de ferramentas

1. Compile o projeto e comece a depuração. A instância experimental do Visual Studio deve aparecer.

2. No menu **Exibir/outras janelas** , clique em **testar ToolWindow** para exibir a janela de ferramentas.

     Você deve ver uma barra de ferramentas (parece com o ícone padrão) na parte superior esquerda da janela de ferramentas, logo abaixo do título.

3. Na barra de ferramentas, clique no ícone para exibir a mensagem **TWTestCommandPackage dentro de TWToolbar. TWTestCommand. MenuItemCallback ()**.

## <a name="see-also"></a>Confira também
- [Adicionar uma barra de ferramentas](../extensibility/adding-a-toolbar.md)
