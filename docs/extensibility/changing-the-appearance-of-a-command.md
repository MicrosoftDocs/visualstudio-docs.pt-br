---
title: Alterando a aparência de um comando | Microsoft Docs
description: Saiba como fornecer comentários alterando a aparência de um comando, como disponibilizar/não disponível comandos, ocultos/mostrados ou marcados/desmarcados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- commands, changing appearance
- menu commands, changing appearance
- menus, changing command appearance
ms.assetid: da2474fa-f92d-4e9e-b8bf-67c61bf249c2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ddeed08d7bc33b9a9ae5405876f3b28459d4eaf2
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905027"
---
# <a name="change-the-appearance-of-a-command"></a>Alterar a aparência de um comando
Você pode fornecer comentários ao usuário alterando a aparência de um comando. Por exemplo, talvez você queira que um comando tenha uma aparência diferente quando ele não estiver disponível. Você pode disponibilizar comandos ou não disponível, ocultar ou mostrar ou verificar ou desmarque-os no menu.

Para alterar a aparência de um comando, execute uma destas ações:

- Especifique os sinalizadores apropriados na definição de comando no arquivo da tabela de comandos.

- Use o <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> serviço .

- Implemente <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> a interface e modifique os objetos de comando brutos.

  As etapas a seguir mostram como encontrar e atualizar a aparência de um comando usando o MPF (Managed Package Framework).

### <a name="to-change-the-appearance-of-a-menu-command"></a>Para alterar a aparência de um comando de menu

1. Siga as instruções em [Alterar o texto de um comando de menu](../extensibility/changing-the-text-of-a-menu-command.md) para criar um item de menu chamado `New Text` .

2. No arquivo *ChangeMenuText.cs,* adicione a seguinte instrução using:

    ```csharp
    using System.Security.Permissions;
    ```

3. No arquivo *ChangeMenuTextPackageGuids.cs,* adicione a seguinte linha:

    ```csharp
    public const string guidChangeMenuTextPackageCmdSet= "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file
    ```

4. No arquivo *ChangeMenuText.cs,* substitua o código no método ShowMessageBox pelo seguinte:

    ```csharp
    private void Execute(object sender, EventArgs e)
    {
        ThreadHelper.ThrowIfNotOnUIThread();
        var command = sender as OleMenuCommand;
        if (command.Text == "New Text")
            ChangeMyCommand(command.CommandID.ID, false);
    }
    ```

5. Obtenha o comando que você deseja atualizar do objeto <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> e, em seguida, de definir as propriedades apropriadas no objeto de comando. Por exemplo, o método a seguir torna o comando especificado de um conjunto de comandos VSPackage disponível ou indisponível. O código a seguir torna o item de menu chamado `New Text` indisponível depois que ele foi clicado.

    ```csharp
    public bool ChangeMyCommand(int cmdID, bool enableCmd)
    {
        bool cmdUpdated = false;
        var mcs = this.package.GetService<IMenuCommandService, OleMenuCommandService>();
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

6. Compile o projeto e comece a depuração. A instância experimental do Visual Studio deve aparecer.

7. No menu **Ferramentas,** clique no **comando Invocar ChangeMenuText.** Neste ponto, o nome do comando é **Invoke ChangeMenuText**, para que o manipulador de comandos não chame **ChangeMyCommand().**

8. No menu **Ferramentas,** agora você deve ver **Novo Texto.** Clique **em Novo Texto.** O comando agora deve estar es cinza.

## <a name="see-also"></a>Confira também
- [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)
- [Como o VSPackages adiciona elementos de interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Estendendo menus e comandos](../extensibility/extending-menus-and-commands.md)
- [Visual Studio de comando (. Vsct) Arquivos](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
