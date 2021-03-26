---
title: Alterando a aparência de um comando | Microsoft Docs
description: Saiba como fornecer comentários alterando a aparência de um comando, como tornar os comandos disponíveis/não disponíveis, ocultos/mostrados ou marcados/desmarcados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 8b6911d865b253ff82ffcc6c4911e0989f109f28
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089817"
---
# <a name="change-the-appearance-of-a-command"></a>Alterar a aparência de um comando
Você pode fornecer comentários para o usuário alterando a aparência de um comando. Por exemplo, você pode desejar que um comando pareça diferente quando não estiver disponível. Você pode tornar os comandos disponíveis ou indisponíveis, ocultá-los ou exibi-los, ou marque ou desmarque-os no menu.

Para alterar a aparência de um comando, execute uma destas ações:

- Especifique os sinalizadores apropriados na definição de comando no arquivo de tabela de comando.

- Use o <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> serviço.

- Implemente a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface e modifique os objetos de comando brutos.

  As etapas a seguir mostram como localizar e atualizar a aparência de um comando usando o MPF (estrutura de pacote gerenciada).

### <a name="to-change-the-appearance-of-a-menu-command"></a>Para alterar a aparência de um comando de menu

1. Siga as instruções em [alterar o texto de um comando de menu](../extensibility/changing-the-text-of-a-menu-command.md) para criar um item de menu chamado `New Text` .

2. No arquivo *ChangeMenuText. cs* , adicione a seguinte instrução Using:

    ```csharp
    using System.Security.Permissions;
    ```

3. No arquivo *ChangeMenuTextPackageGuids. cs* , adicione a seguinte linha:

    ```csharp
    public const string guidChangeMenuTextPackageCmdSet= "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file
    ```

4. No arquivo *ChangeMenuText. cs* , substitua o código no método de a MessageBox pelo seguinte:

    ```csharp
    private void Execute(object sender, EventArgs e)
    {
        ThreadHelper.ThrowIfNotOnUIThread();
        var command = sender as OleMenuCommand;
        if (command.Text == "New Text")
            ChangeMyCommand(command.CommandID.ID, false);
    }
    ```

5. Obtenha o comando que você deseja atualizar do <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> objeto e, em seguida, defina as propriedades apropriadas no objeto de comando. Por exemplo, o método a seguir torna o comando especificado de um conjunto de comandos VSPackage disponível ou indisponível. O código a seguir torna o item de menu chamado `New Text` indisponível depois de ter sido clicado.

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

7. No menu **ferramentas** , clique no comando **invocar ChangeMenuText** . Neste ponto, o nome do comando é **invocar ChangeMenuText**, portanto, o manipulador de comandos não chama **ChangeMyCommand ()**.

8. No menu **ferramentas** , agora você deve ver o **novo texto**. Clique em **novo texto**. O comando agora deve estar esmaecido.

## <a name="see-also"></a>Confira também
- [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)
- [Como VSPackages adicionar elementos da interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Estendendo menus e comandos](../extensibility/extending-menus-and-commands.md)
- [Tabela de comandos do Visual Studio (. Arquivos de vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
