---
title: Alterando o texto de um comando de menu | Microsoft Docs
description: Saiba como alterar o rótulo de texto de um comando de menu usando o serviço IMenuCommandService examinando este exemplo de código.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- menus, changing text
- text, menus
- commands, changing text
ms.assetid: 5cb676a0-c6e2-47e5-bd2b-133dc8842e46
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 541acf1bcf448541fe6c440eb2aada687cfbe0e9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904985"
---
# <a name="change-the-text-of-a-menu-command"></a>Alterar o texto de um comando de menu
As etapas a seguir mostram como alterar o rótulo de texto de um comando de menu usando o <xref:System.ComponentModel.Design.IMenuCommandService> serviço.

## <a name="changing-a-menu-command-label-with-the-imenucommandservice"></a>Alterando um rótulo de comando de menu com o IMenuCommandService

1. Crie um projeto VSIX chamado `MenuText` com um comando de menu chamado **ChangeMenuText**. Para obter mais informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).

2. No arquivo *. vsct* , adicione o `TextChanges` sinalizador ao comando de menu, conforme mostrado no exemplo a seguir.

    ```xml
    <Button guid="guidChangeMenuTextPackageCmdSet" id="ChangeMenuTextId" priority="0x0100" type="Button">
        <Parent guid="guidChangeMenuTextPackageCmdSet" id="MyMenuGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <CommandFlag>TextChanges</CommandFlag>
        <Strings>
            <ButtonText>Invoke ChangeMenuText</ButtonText>
        </Strings>
    </Button>
    ```

3. No arquivo *ChangeMenuText. cs* , crie um manipulador de eventos que será chamado antes que o comando de menu seja exibido.

    ```csharp
    private void OnBeforeQueryStatus(object sender, EventArgs e)
    {
        var myCommand = sender as OleMenuCommand;
        if (null != myCommand)
        {
            myCommand.Text = "New Text";
        }
    }
    ```

    Você também pode atualizar o status do comando de menu nesse método alterando as <xref:System.ComponentModel.Design.MenuCommand.Visible%2A> Propriedades, <xref:System.ComponentModel.Design.MenuCommand.Checked%2A> e <xref:System.ComponentModel.Design.MenuCommand.Enabled%2A> no <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> objeto.

4. No Construtor ChangeMenuText, substitua o código original de inicialização e posicionamento do comando pelo código que cria um <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> (em vez de um `MenuCommand` ) que representa o comando de menu, adiciona o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> manipulador de eventos e fornece o comando de menu para o serviço de comando de menu.

    Aqui está o que deve ser semelhante a:

    ```csharp
    private ChangeMenuText(AsyncPackage package, OleMenuCommandService commandService)
    {
        this.package = package ?? throw new ArgumentNullException(nameof(package));
        commandService = commandService ?? throw new ArgumentNullException(nameof(commandService));
        
        var menuCommandID = new CommandID(CommandSet, CommandId);
        var menuItem = new OleMenuCommand(this.Excute, menuCommandID);
        menuItem.BeforeQueryStatus += new EventHandler(OnBeforeQueryStatus);
        commandService.AddCommand(menuItem);
    }
    ```

5. Compile o projeto e comece a depuração. A instância experimental do Visual Studio é exibida.

6. No menu **ferramentas** , você deverá ver um comando chamado **Invoke ChangeMenuText**.

7. Clique no comando. Você deve ver a caixa de mensagem anunciando que **MenuItemCallback** foi chamado. Quando você descartar a caixa de mensagem, verá que o nome do comando no menu ferramentas agora é **novo texto**.
