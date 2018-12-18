---
title: Adicionando um Submenu a um Menu | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- context menus
- submenus, cascading
- cascading submenus
- menus, creating cascading submenus
ms.assetid: 692600cb-d052-40e2-bdae-4354ae7c6c84
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3ec436383aa745ed033858724b4d4b2ff8b929c6
ms.sourcegitcommit: b6dfa1bdf4c23c2e341754454bbd4758db2218e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48863914"
---
# <a name="add-a-submenu-to-a-menu"></a>Adicionar um Submenu a um Menu
Este passo a passo se baseia a demonstração no [adicionar um Menu a barra de menus do Visual Studio](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md) , mostrando como adicionar um submenu para o **TestMenu** menu.

 Um submenu é um menu secundário que aparece em outro menu. Um submenu pode ser identificado pela seta que segue o seu nome. Clicando no nome faz com que o submenu e seus comandos a serem exibidos.

 Este passo a passo cria um submenu em um menu na barra de menus do Visual Studio e coloca um novo comando no submenu. O passo a passo também implementa o novo comando.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="add-a-submenu-to-a-menu"></a>Adicionar um Submenu a um Menu

1.  Siga as etapas em [adicionar um Menu a barra de menus do Visual Studio](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md) para criar o item de menu e de projeto. As etapas neste passo a passo presumem que o nome do projeto VSIX é `TopLevelMenu`.

2.  Abra *TestCommandPackage.vsct*. No `<Symbols>` seção, adicione uma `<IDSymbol>` elemento para o submenu, um para o grupo de submenu e outro para o comando, tudo no `<GuidSymbol>` nó chamado "guidTopLevelMenuCmdSet". Esse é o mesmo nó que contém o `<IDSymbol>` elemento para o menu de nível superior.

    ```xml
    <IDSymbol name="SubMenu" value="0x1100"/>
    <IDSymbol name="SubMenuGroup" value="0x1150"/>
    <IDSymbol name="cmdidTestSubCommand" value="0x0105"/>
    ```

3.  Adicionar submenu recém-criado para o `<Menus>` seção.

    ```xml
    <Menu guid="guidTestCommandPackageCmdSet" id="SubMenu" priority="0x0100" type="Menu">
        <Parent guid="guidTestCommandPackageCmdSet" id="MyMenuGroup"/>
        <Strings>
            <ButtonText>Sub Menu</ButtonText>
            <CommandName>Sub Menu</CommandName>
        </Strings>
    </Menu>
    ```

     O par de ID do GUID do pai Especifica o grupo de menu que foi gerado [adicionar um Menu a barra de menus do Visual Studio](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md), e é um filho do menu de nível superior.

4.  Adicione o grupo de menu definido na etapa 2 para o `<Groups>` seção e torná-lo um filho do submenu.

    ```xml
    <Group guid="guidTestCommandPackageCmdSet" id="SubMenuGroup" priority="0x0000">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>
    ```

5.  Adicione um novo `<Button>` elemento para o `<Buttons>` seção para definir o comando criado na etapa 2 como um item no submenu.

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

6.  Compile a solução e inicie a depuração. Você deve ver a instância experimental.

7.  Clique em **TestMenu** para ver um submenu novo chamado **submenu**. Clique em **submenu** para abrir o submenu e ver um novo comando, **teste subcomando**. Observe que clicar em **teste subcomando** não faz nada.

## <a name="add-a-command"></a>Adicionar um comando

1.  Abra *TestCommand.cs* e adicione a seguinte ID de comando após a ID de comando existente.

    ```csharp
    public const int cmdidTestSubCmd = 0x0105;
    ```

2.  Adicione o subcomando. Localize o construtor de comando. Adicione as seguintes linhas imediatamente após a chamada para o `AddCommand` método.

    ```csharp
    CommandID subCommandID = new CommandID(CommandSet, cmdidTestSubCmd);
    MenuCommand subItem = new MenuCommand(new EventHandler(SubItemCallback), subCommandID);
    commandService.AddCommand(subItem);
    ```

    O `SubItemCallback` manipulador de comandos será definido posteriormente. Agora, o construtor deve ser assim:

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

3.  Adicionar `SubItemCallback()`. Esse é o método que é chamado quando o comando novo no submenu é clicado.

    ```csharp
    private void SubItemCallback(object sender, EventArgs e)
    {
        IVsUIShell uiShell = (IVsUIShell)this.ServiceProvider.GetService(typeof(SVsUIShell));
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

4.  Compile o projeto e comece a depuração. A instância experimental deve aparecer.

5.  Sobre o **TestMenu** menu, clique em **submenu** e, em seguida, clique em **teste subcomando**. Uma caixa de mensagem deve aparecer e exibir o texto, "Teste comando dentro de TestCommand.SubItemCallback()".

## <a name="see-also"></a>Consulte também
 [Adicionar um menu a barra de menus do Visual Studio](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md) [comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)
