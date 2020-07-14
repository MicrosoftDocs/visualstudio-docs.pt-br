---
title: Adicionando um submenu a um menu | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- context menus
- submenus, cascading
- cascading submenus
- menus, creating cascading submenus
ms.assetid: 692600cb-d052-40e2-bdae-4354ae7c6c84
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cb143a611b1fb1f4278d28fdf9423a1f6613a68d
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904173"
---
# <a name="add-a-submenu-to-a-menu"></a>Adicionar um submenu a um menu
Este tutorial se baseia na demonstração em [Adicionar um menu à barra de menus do Visual Studio](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md) , mostrando como adicionar um submenu ao menu **TestMenu** .

 Um submenu é um menu secundário que aparece em outro menu. Um submenu pode ser identificado pela seta que segue seu nome. Clicar no nome faz com que o submenu e seus comandos sejam exibidos.

 Este tutorial cria um submenu em um menu na barra de menus do Visual Studio e coloca um novo comando no submenu. O Walkthrough também implementa o novo comando.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="add-a-submenu-to-a-menu"></a>Adicionar um submenu a um menu

1. Siga as etapas em [Adicionar um menu à barra de menus do Visual Studio](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md) para criar o projeto e o item de menu. As etapas neste passo a passos pressupõem que o nome do projeto VSIX é `TopLevelMenu` .

2. Abra *TestCommandPackage. vsct*. Na `<Symbols>` seção, adicione um `<IDSymbol>` elemento para o submenu, um para o grupo de submenu e um para o comando, tudo no `<GuidSymbol>` nó chamado "guidTopLevelMenuCmdSet". Esse é o mesmo nó que contém o `<IDSymbol>` elemento para o menu de nível superior.

    ```xml
    <IDSymbol name="SubMenu" value="0x1100"/>
    <IDSymbol name="SubMenuGroup" value="0x1150"/>
    <IDSymbol name="cmdidTestSubCommand" value="0x0105"/>
    ```

3. Adicione o submenu recém-criado à `<Menus>` seção.

    ```xml
    <Menu guid="guidTestCommandPackageCmdSet" id="SubMenu" priority="0x0100" type="Menu">
        <Parent guid="guidTestCommandPackageCmdSet" id="MyMenuGroup"/>
        <Strings>
            <ButtonText>Sub Menu</ButtonText>
            <CommandName>Sub Menu</CommandName>
        </Strings>
    </Menu>
    ```

     O par GUID/ID do pai especifica o grupo de menus que foi gerado em [Adicionar um menu à barra de menus do Visual Studio](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)e é um filho do menu de nível superior.

4. Adicione o grupo de menus definido na etapa 2 à `<Groups>` seção e torne-o um filho do submenu.

    ```xml
    <Group guid="guidTestCommandPackageCmdSet" id="SubMenuGroup" priority="0x0000">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>
    ```

5. Adicione um novo `<Button>` elemento à `<Buttons>` seção para definir o comando criado na etapa 2 como um item no submenu.

    ```xml
    <Button guid="guidTestCommandPackageCmdSet" id="cmdidTestSubCommand" priority="0x0000" type="Button">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenuGroup" />
        <Icon guid="guidImages" id="bmpPic2" />
        <Strings>
           <CommandName>cmdidTestSubCommand</CommandName>
           <ButtonText>Test Sub Command</ButtonText>
        </Strings>
    </Button>
    ```

6. Compile a solução e inicie a depuração. Você deve ver a instância experimental.

7. Clique em **TestMenu** para ver um novo submenu chamado **submenu**. Clique em **submenu** para abrir o submenu e ver um novo comando, **testar subcomando**. Observe que clicar em **testar subcomando** não faz nada.

## <a name="add-a-command"></a>Adicionar um comando

1. Abra *TestCommand.cs* e adicione a seguinte ID de comando após a ID de comando existente.

    ```csharp
    public const int cmdidTestSubCmd = 0x0105;
    ```

2. Adicione o subcomando. Localize o construtor de comandos. Adicione as linhas a seguir logo após a chamada para o `AddCommand` método.

    ```csharp
    CommandID subCommandID = new CommandID(CommandSet, cmdidTestSubCmd);
    MenuCommand subItem = new MenuCommand(new EventHandler(SubItemCallback), subCommandID);
    commandService.AddCommand(subItem);
    ```

    O `SubItemCallback` manipulador de comando será definido mais tarde. O Construtor agora deve ser assim:

    ```csharp
    private TestCommand(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException("package");
        }

        this.package = package;

        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        if (commandService != null)
        {
            var menuCommandID = new CommandID(CommandSet, CommandId);
            var menuItem = new MenuCommand(this.MenuItemCallback, menuCommandID);
            commandService.AddCommand(menuItem);

            CommandID subCommandID = new CommandID(CommandSet, cmdidTestSubCmd);
            MenuCommand subItem = new MenuCommand(new EventHandler(SubItemCallback), subCommandID);
            commandService.AddCommand(subItem);
        }
    }
    ```

3. Adicione `SubItemCallback()`. Esse é o método que é chamado quando o novo comando no submenu é clicado.

    ```csharp
    private void SubItemCallback(object sender, EventArgs e)
    {
        IVsUIShell uiShell = (IVsUIShell)this.ServiceProvider.GetServiceAsync(typeof(SVsUIShell));
        Guid clsid = Guid.Empty;
        int result;
        uiShell.ShowMessageBox(
            0,
            ref clsid,
            "TestCommand",
            string.Format(CultureInfo.CurrentCulture,
            "Inside TestCommand.SubItemCallback()",
            this.ToString()),
            string.Empty,
            0,
            OLEMSGBUTTON.OLEMSGBUTTON_OK,
            OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,
            OLEMSGICON.OLEMSGICON_INFO,
            0,
            out result);
    }
    ```

4. Compile o projeto e comece a depuração. A instância experimental deve aparecer.

5. No menu **TestMenu** , clique em **sub menu** e, em seguida, clique em **testar subcomando**. Uma caixa de mensagem deve aparecer e exibir o texto "comando de teste dentro de TestCommand. SubItemCallback ()".

## <a name="see-also"></a>Confira também

- [Adicionar um menu à barra de menus do Visual Studio](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)
- [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)
