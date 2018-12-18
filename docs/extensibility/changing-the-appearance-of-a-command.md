---
title: Alterando a aparência de um comando | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, changing appearance
- menu commands, changing appearance
- menus, changing command appearance
ms.assetid: da2474fa-f92d-4e9e-b8bf-67c61bf249c2
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 61ba39bc8a312fb06499bed7ca94e33dc5e7153e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49825979"
---
# <a name="change-the-appearance-of-a-command"></a>Alterar a aparência de um comando
Você pode fornecer comentários ao usuário, alterando a aparência de um comando. Por exemplo, convém um comando para uma aparência diferente quando ele não estiver disponível. Você pode tornar os comandos disponíveis ou não disponíveis, ocultar ou mostrá-los, ou marque ou desmarque-os no menu.  
  
 Para alterar a aparência de um comando, execute uma destas ações:  
  
- Especifica os sinalizadores adequados na definição de comando no arquivo de comando de tabela.  
  
- Use o <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> service.  
  
- Implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> de interface e modificar os objetos de comando bruto.  
  
  As etapas a seguir mostram como localizar e atualizar a aparência de um comando usando a estrutura de pacote gerenciado (MPF).  
  
### <a name="to-change-the-appearance-of-a-menu-command"></a>Para alterar a aparência de um comando de menu  
  
1.  Siga as instruções em [alterar o texto de um comando de menu](../extensibility/changing-the-text-of-a-menu-command.md) para criar um item de menu chamado `New Text`.  
  
2.  No *ChangeMenuText.cs* de arquivo, adicione a seguinte instrução using:  
  
    ```csharp  
    using System.Security.Permissions;  
    ```  
  
3.  No *ChangeMenuTextPackageGuids.cs* arquivo, adicione a seguinte linha:  
  
    ```csharp  
    public const string guidChangeMenuTextPackageCmdSet= "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file  
    ```  
  
4.  No *ChangeMenuText.cs* de arquivo, substitua o código no método ShowMessageBox com o seguinte:  
  
    ```csharp  
    private void ShowMessageBox(object sender, EventArgs e)  
    {  
        var command = sender as OleMenuCommand;  
        if (command.Text == "New Text")  
            ChangeMyCommand(command.CommandID.ID, false);
    }  
    ```  
  
5.  Obter o comando que você deseja atualizar a partir de <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> do objeto e, em seguida, defina as propriedades apropriadas no objeto de comando. Por exemplo, o método a seguir faz o comando especificado a partir de um comando de VSPackage conjunto disponível ou não está disponível. O código a seguir faz com que o item de menu chamado `New Text` indisponível após ser clicado.  
  
    ```csharp  
    public bool ChangeMyCommand(int cmdID, bool enableCmd)  
    {  
        bool cmdUpdated = false;  
        var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService))  
            as OleMenuCommandService;  
        var newCmdID = new CommandID(new Guid(ChangeMenuTextPackageGuids.guidChangeMenuTextPackageCmdSet), cmdID);  
        MenuCommand mc = mcs.FindCommand(newCmdID);  
        if (mc != null)  
        {  
            mc.Enabled = enableCmd;  
            cmdUpdated = true;  
        }  
        return cmdUpdated;
    }  
    ```  
  
6.  Compile o projeto e comece a depuração. A instância experimental do Visual Studio deve aparecer.  
  
7.  Sobre o **ferramentas** menu, clique no **ChangeMenuText invocar** comando. Neste ponto é o nome do comando **invocar ChangeMenuText**, portanto, o manipulador de comandos não chama **ChangeMyCommand()**.  
  
8.  Sobre o **ferramentas** menu, agora você deve ver **novo texto**. Clique em **novo texto**. O comando agora deveriam ser esmaecido.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)   
 [Como os VSPackages adicionam elementos da interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [Ampliar menus e comandos](../extensibility/extending-menus-and-commands.md)   
 [Tabela de comando do Visual Studio (. Arquivos de VSCT)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
