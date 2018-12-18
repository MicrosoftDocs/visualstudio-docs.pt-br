---
title: Alterar o texto de um comando de Menu | Microsoft Docs
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
- menus, changing text
- text, menus
- commands, changing text
ms.assetid: 5cb676a0-c6e2-47e5-bd2b-133dc8842e46
caps.latest.revision: 26
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 52e0319edd7d8f9563998adc18e3b00f7c12713b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51786464"
---
# <a name="changing-the-text-of-a-menu-command"></a>Alterando o texto de um comando de menu
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As etapas a seguir mostram como alterar o rótulo de texto de um comando de menu usando o <xref:System.ComponentModel.Design.IMenuCommandService> service.  
  
## <a name="changing-a-menu-command-label-with-the-imenucommandservice"></a>Alterar um rótulo de comando de menu com o IMenuCommandService  
  
1.  Crie um projeto do VSIX chamado `MenuText` com um comando de menu denominado **ChangeMenuText**. Para obter mais informações, consulte [criar uma extensão com um comando de Menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
2.  No arquivo .vstc, adicione o `TextChanges` sinalizar ao seu comando de menu, conforme mostrado no exemplo a seguir.  
  
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
  
3.  No arquivo ChangeMenuText.cs, crie um manipulador de eventos será chamado antes do comando de menu é exibido.  
  
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
  
7.  Clique no comando. Você deve ver a caixa de mensagem anunciando que MenuItemCallback foi chamado. Quando você descartar a caixa de mensagem, você deverá ver o nome do comando no menu Ferramentas agora está **novo texto**.

