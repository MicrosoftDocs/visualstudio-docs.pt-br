---
title: Adicionando um controlador de menu a uma barra de ferramentas | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- toolbars [Visual Studio], adding menu controllers
- menus, adding menu controllers to toolbars
- menu controllers, adding to toolbars
ms.assetid: 6af9b0b4-037f-404c-bb40-aaa1970768ea
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 32cbbbc7784c112b33b5f720b306b8c93269bb82
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903533"
---
# <a name="add-a-menu-controller-to-a-toolbar"></a>Adicionar um controlador de menu a uma barra de ferramentas
Este tutorial se baseia na guia [Adicionar uma barra de ferramentas a uma janela](../extensibility/adding-a-toolbar-to-a-tool-window.md) de ferramentas e mostra como adicionar um controlador de menu à barra de ferramentas da janela de ferramentas. As etapas mostradas aqui também podem ser aplicadas à barra de ferramentas criada na guia [Adicionar uma barra de ferramentas](../extensibility/adding-a-toolbar.md) .

Um controlador de menu é um controle de divisão. O lado esquerdo do controlador de menu mostra o último comando usado, e você pode executá-lo clicando nele. O lado direito do controlador de menu é uma seta que, quando clicada, abre uma lista de comandos adicionais. Quando você clica em um comando na lista, o comando é executado e substitui o comando no lado esquerdo do controlador de menu. Dessa forma, o controlador de menu Opera como um botão de comando que sempre mostra o último comando usado de uma lista.

Os controladores de menu podem aparecer em menus, mas são usados com mais frequência em barras de ferramentas.

## <a name="prerequisites"></a>Pré-requisitos
A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-menu-controller"></a>Criar um controlador de menu

1. Siga os procedimentos descritos em [Adicionar uma barra de ferramentas a uma janela de ferramentas](../extensibility/adding-a-toolbar-to-a-tool-window.md) para criar uma janela de ferramentas que tenha uma barra de ferramentas.

2. Em *TWTestCommandPackage. vsct*, vá para a seção símbolos. No elemento GuidSymbol chamado **guidTWTestCommandPackageCmdSet**, declare o controlador de menu, o grupo de controlador de menu e os três itens de menu.

    ```xml
    <IDSymbol name="TestMenuController" value="0x1300" /><IDSymbol name="TestMenuControllerGroup" value="0x1060" /><IDSymbol name="cmdidMCItem1" value="0x0130" /><IDSymbol name="cmdidMCItem2" value="0x0131" /><IDSymbol name="cmdidMCItem3" value="0x0132" />
    ```

3. Na seção menus, após a última entrada de menu, defina o controlador de menu como um menu.

    ```xml
    <Menu guid="guidTWTestCommandPackageCmdSet" id="TestMenuController" priority="0x0100" type="MenuController">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" />
        <CommandFlag>IconAndText</CommandFlag>
        <CommandFlag>TextChanges</CommandFlag>
        <CommandFlag>TextIsAnchorCommand</CommandFlag>
        <Strings>
            <ButtonText>Test Menu Controller</ButtonText>
            <CommandName>Test Menu Controller</CommandName>
        </Strings>
    </Menu>
    ```

    Os `TextChanges` `TextIsAnchorCommand` sinalizadores e devem ser incluídos para permitir que o controlador de menu reflita o último comando selecionado.

4. Na seção grupos, após a entrada do último grupo, adicione o grupo do controlador de menu.

    ```xml
    <Group guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" priority="0x000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuController" />
    </Group>
    ```

    Ao definir o controlador de menu como o pai, todos os comandos colocados nesse grupo aparecerão no controlador de menu. O `priority` atributo é omitido, o que o define como o valor padrão de 0, porque ele é o único grupo no controlador de menu.

5. Na seção botões, após a entrada do último botão, adicione um elemento de botão para cada um dos itens de menu.

    ```xml
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem1" priority="0x0000" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 1</ButtonText>
            <CommandName>MC Item 1</CommandName>
        </Strings>
    </Button>
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem2" priority="0x0100" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPic2" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 2</ButtonText>
            <CommandName>MC Item 2</CommandName>
        </Strings>
    </Button>
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem3" priority="0x0200" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPicSearch" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 3</ButtonText>
            <CommandName>MC Item 3</CommandName>
        </Strings>
    </Button>
    ```

6. Neste ponto, você pode examinar o controlador de menu. Compile o projeto e comece a depuração. Você deve ver a instância experimental.

   1. No menu **Exibir/outras janelas** , abra **testar ToolWindow**.

   2. O controlador de menu aparece na barra de ferramentas na janela de ferramentas.

   3. Clique na seta no lado direito do controlador de menu para ver os três comandos possíveis.

      Observe que, quando você clica em um comando, o título do controlador de menu é alterado para exibir esse comando. Na próxima seção, adicionaremos o código para ativar esses comandos.

## <a name="implement-the-menu-controller-commands"></a>Implementar os comandos do controlador de menu

1. No *TWTestCommandPackageGuids.cs*, adicione IDs de comando para os três itens de menu após as IDs de comando existentes.

    ```csharp
    public const int cmdidMCItem1 = 0x130;
    public const int cmdidMCItem2 = 0x131;
    public const int cmdidMCItem3 = 0x132;
    ```

2. No *TWTestCommand.cs*, adicione o código a seguir na parte superior da `TWTestCommand` classe.

    ```csharp
    private int currentMCCommand; // The currently selected menu controller command
    ```

3. No Construtor TWTestCommand, após a última chamada para o `AddCommand` método, adicione o código para rotear os eventos para cada comando por meio dos mesmos manipuladores.

    ```csharp
    for (int i = TWTestCommandPackageGuids.cmdidMCItem1; i <=
        TWTestCommandPackageGuids.cmdidMCItem3; i++)
    {
        CommandID cmdID = new
        CommandID(new Guid(TWTestCommandPackageGuids.guidTWTestCommandPackageCmdSet), i);
        OleMenuCommand mc = new OleMenuCommand(new
          EventHandler(OnMCItemClicked), cmdID);
        mc.BeforeQueryStatus += new EventHandler(OnMCItemQueryStatus);
        commandService.AddCommand(mc);
        // The first item is, by default, checked. 
        if (TWTestCommandPackageGuids.cmdidMCItem1 == i)
        {
            mc.Checked = true;
            this.currentMCCommand = i;
        }
    }
    ```

4. Adicione um manipulador de eventos à classe **TWTestCommand** para marcar o comando selecionado como marcado.

    ```csharp
    private void OnMCItemQueryStatus(object sender, EventArgs e)
    {
        OleMenuCommand mc = sender as OleMenuCommand;
        if (null != mc)
        {
            mc.Checked = (mc.CommandID.ID == this.currentMCCommand);
        }
    }
    ```

5. Adicione um manipulador de eventos que exibe uma MessageBox quando o usuário seleciona um comando no controlador de menu:

    ```csharp
    private void OnMCItemClicked(object sender, EventArgs e)
    {
        OleMenuCommand mc = sender as OleMenuCommand;
        if (null != mc)
        {
            string selection;
            switch (mc.CommandID.ID)
            {
                case c.cmdidMCItem1:
                    selection = "Menu controller Item 1";
                    break;

                case TWTestCommandPackageGuids.cmdidMCItem2:
                    selection = "Menu controller Item 2";
                    break;

                case TWTestCommandPackageGuids.cmdidMCItem3:
                    selection = "Menu controller Item 3";
                    break;

                default:
                    selection = "Unknown command";
                    break;
            }
            this.currentMCCommand = mc.CommandID.ID;

            IVsUIShell uiShell =
              (IVsUIShell) ServiceProvider.GetService(typeof(SVsUIShell));
            Guid clsid = Guid.Empty;
            int result;
            uiShell.ShowMessageBox(
                    0,
                    ref clsid,
                    "Test Tool Window Toolbar Package",
                    string.Format(CultureInfo.CurrentCulture,
                                 "You selected {0}", selection),
                    string.Empty,
                    0,
                    OLEMSGBUTTON.OLEMSGBUTTON_OK,
                    OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,
                    OLEMSGICON.OLEMSGICON_INFO,
                    0,
                    out result);
        }
    }
    ```

## <a name="testing-the-menu-controller"></a>Testando o controlador de menu

1. Compile o projeto e comece a depuração. Você deve ver a instância experimental.

2. Abra o **ToolWindow de teste** no menu **Exibir/outras janelas** .

    O controlador de menu aparece na barra de ferramentas na janela de ferramentas e exibe o **Item 1 do MC**.

3. Clique no botão controlador de menu à esquerda da seta.

    Você deve ver três itens, o primeiro deles é selecionado e tem uma caixa de realce ao seu ícone. Clique em **MC item 3**.

    Uma caixa de diálogo é exibida com a mensagem **que você selecionou item do controlador de menu 3**. Observe que a mensagem corresponde ao texto no botão controlador do menu. O botão controlador de menu agora exibe o **item 3 do MC**.

## <a name="see-also"></a>Confira também
- [Adicionando uma barra de ferramentas a uma janela de ferramentas](../extensibility/adding-a-toolbar-to-a-tool-window.md)
- [Adicionando uma barra de ferramentas](../extensibility/adding-a-toolbar.md)
