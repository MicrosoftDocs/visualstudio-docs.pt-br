---
title: Alterar o texto de um comando de Menu | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- menus, changing text
- text, menus
- commands, changing text
ms.assetid: 5cb676a0-c6e2-47e5-bd2b-133dc8842e46
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: df943221fc2f154e8f18007bd5f7ff5454434d84
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39234819"
---
# <a name="change-the-text-of-a-menu-command"></a>Alterar o texto de um comando de menu
As etapas a seguir mostram como alterar o rótulo de texto de um comando de menu usando o <xref:System.ComponentModel.Design.IMenuCommandService> service.  
  
## <a name="changing-a-menu-command-label-with-the-imenucommandservice"></a>Alterar um rótulo de comando de menu com o IMenuCommandService  
  
1.  Crie um projeto do VSIX chamado `MenuText` com um comando de menu denominado **ChangeMenuText**. Para obter mais informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
2.  No *VSCT* do arquivo, adicione o `TextChanges` sinalizar ao seu comando de menu, conforme mostrado no exemplo a seguir.  
  
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
  
3.  No *ChangeMenuText.cs* de arquivo, crie um manipulador de eventos será chamado antes do comando de menu é exibido.  
  
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
  
     Você também pode atualizar o status do comando de menu nesse método, alterando a <xref:System.ComponentModel.Design.MenuCommand.Visible%2A>, <xref:System.ComponentModel.Design.MenuCommand.Checked%2A>, e <xref:System.ComponentModel.Design.MenuCommand.Enabled%2A> propriedades sobre o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> objeto.  
  
4.  No construtor ChangeMenuText, substitua o código de inicialização e o posicionamento de comando original pelo código que cria uma <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> (em vez de uma `MenuCommand`) que representa o comando de menu, adiciona o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> manipulador de eventos e fornece um menu comando para o serviço de comando de menu.  
  
     Aqui está o que deve se parecer com:  
  
    ```csharp  
    private ChangeMenuText(Package package)  
    {  
        if (package == null)  
        {  
            throw new ArgumentNullException(nameof(package));  
        }  
  
        this.package = package;  
  
        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
        if (commandService != null)  
        {  
            CommandID menuCommandID = new CommandID(MenuGroup, CommandId);  
            EventHandler eventHandler = this.ShowMessageBox;  
            OleMenuCommand menuItem = new OleMenuCommand(ShowMessageBox, menuCommandID);  
            menuItem.BeforeQueryStatus +=  
                new EventHandler(OnBeforeQueryStatus);  
            commandService.AddCommand(menuItem);  
        }  
    }  
    ```  
  
5.  Compile o projeto e comece a depuração. A instância experimental do Visual Studio é exibida.  
  
6.  Sobre o **ferramentas** menu, você verá um comando chamado **ChangeMenuText invocar**.  
  
7.  Clique no comando. Você deve ver a caixa de mensagem anunciando que **MenuItemCallback** foi chamado. Quando você descartar a caixa de mensagem, você deverá ver o nome do comando no menu Ferramentas agora está **novo texto**.
