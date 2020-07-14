---
title: Adicionando uma lista usada mais recentemente a um submenu | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- MRU lists
- menus, creating MRU list
- most recently used
ms.assetid: 27d4bbcf-99b1-498f-8b66-40002e3db0f8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3f73f948befc7665ecc3a40f816389bfaae8e4fd
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904200"
---
# <a name="add-a-most-recently-used-list-to-a-submenu"></a>Adicionar uma lista usada mais recentemente a um submenu
Este tutorial se baseia nas demonstrações em [Adicionar um submenu a um menu](../extensibility/adding-a-submenu-to-a-menu.md)e mostra como adicionar uma lista dinâmica a um submenu. A lista dinâmica forma a base para a criação de uma lista MRU (usada mais recentemente).

Uma lista dinâmica de menus começa com um espaço reservado em um menu. Sempre que o menu é mostrado, o IDE (ambiente de desenvolvimento integrado) do Visual Studio solicita a VSPackage de todos os comandos que devem ser mostrados no espaço reservado. Uma lista dinâmica pode ocorrer em qualquer lugar em um menu. No entanto, as listas dinâmicas são normalmente armazenadas e exibidas por conta própria em submenus ou na parte inferior dos menus. Usando esses padrões de design, você permite que a lista dinâmica de comandos seja expandida e contratada sem afetar a posição de outros comandos no menu. Neste tutorial, a lista de MRU dinâmica é exibida na parte inferior de um submenu existente, separados do restante do submenu por uma linha.

Tecnicamente, uma lista dinâmica também pode ser aplicada a uma barra de ferramentas. No entanto, desencorajamos o uso porque uma barra de ferramentas deve permanecer inalterada, a menos que o usuário precise de etapas específicas para alterá-la.

Este tutorial cria uma lista MRU de quatro itens que alteram a ordem toda vez que um deles é selecionado (o item selecionado é movido para o topo da lista).

Para obter mais informações sobre menus e arquivos *. vsct* , consulte [comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md).

## <a name="prerequisites"></a>Pré-requisitos
Para seguir este passo a passos, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [Visual Studio SDK](../extensibility/visual-studio-sdk.md).

## <a name="create-an-extension"></a>Criar uma extensão

- Siga os procedimentos em [adicionando um submenu a um menu](../extensibility/adding-a-submenu-to-a-menu.md) para criar o submenu que é modificado nos procedimentos a seguir.

  Os procedimentos neste passo a passos pressupõem que o nome do VSPackage é `TestCommand` , que é o nome usado em [Adicionar um menu à barra de menus do Visual Studio](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md).

## <a name="create-a-dynamic-item-list-command"></a>Criar um comando de lista de itens dinâmicos

1. Abra *TestCommandPackage. vsct*.

2. Na `Symbols` seção, no `GuidSymbol` nó chamado guidTestCommandPackageCmdSet, adicione o símbolo para o `MRUListGroup` grupo e o `cmdidMRUList` comando, da seguinte maneira.

    ```xml
    <IDSymbol name="MRUListGroup" value="0x1200"/>
    <IDSymbol name="cmdidMRUList" value="0x0200"/>
    ```

3. Na `Groups` seção, adicione o grupo declarado após as entradas de grupo existentes.

    ```xml
    <Group guid="guidTestCommandPackageCmdSet" id="MRUListGroup"
            priority="0x0100">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>
    ```

4. Na `Buttons` seção, adicione um nó para representar o comando declarado recentemente, após as entradas do botão existente.

    ```xml
    <Button guid="guidTestCommandPackageCmdSet" id="cmdidMRUList"
        type="Button" priority="0x0100">
        <Parent guid="guidTestCommandPackageCmdSet" id="MRUListGroup" />
        <CommandFlag>DynamicItemStart</CommandFlag>
        <Strings>
            <CommandName>cmdidMRUList</CommandName>
            <ButtonText>MRU Placeholder</ButtonText>
        </Strings>
    </Button>
    ```

    O `DynamicItemStart` sinalizador permite que o comando seja gerado dinamicamente.

5. Compile o projeto e inicie a depuração para testar a exibição do novo comando.

    No menu **TestMenu** , clique no novo submenu, **sub menu**, para exibir o novo comando, **espaço reservado para MRU**. Depois que uma lista de comandos MRU dinâmicos for implementada no próximo procedimento, esse rótulo de comando será substituído por essa lista toda vez que o submenu for aberto.

## <a name="filling-the-mru-list"></a>Preenchendo a lista MRU

1. No *TestCommandPackageGuids.cs*, adicione as seguintes linhas após as IDs de comando existentes na `TestCommandPackageGuids` definição de classe.

    ```csharp
    public const string guidTestCommandPackageCmdSet = "00000000-0000-0000-0000-00000000"; // get the GUID from the .vsct file
    public const uint cmdidMRUList = 0x200;
    ```

2. Em *TestCommand.cs* , adicione a seguinte instrução using.

    ```csharp
    using System.Collections;
    ```

3. Adicione o código a seguir no Construtor TestCommand após a última chamada AddCommand. O `InitMRUMenu` será definido mais tarde

    ```csharp
    this.InitMRUMenu(commandService);
    ```

4. Adicione o seguinte código à classe TestCommand. Esse código inicializa a lista de cadeias de caracteres que representam os itens a serem mostrados na lista MRU.

    ```csharp
    private int numMRUItems = 4;
    private int baseMRUID = (int)TestCommandPackageGuids.cmdidMRUList;
    private ArrayList mruList;

    private void InitializeMRUList()
    {
        if (null == this.mruList)
        {
            this.mruList = new ArrayList();
            if (null != this.mruList)
            {
                for (int i = 0; i < this.numMRUItems; i++)
                {
                    this.mruList.Add(string.Format(CultureInfo.CurrentCulture,
                        "Item {0}", i + 1));
                }
            }
        }
    }
    ```

5. Depois do `InitializeMRUList` método, adicione o `InitMRUMenu` método. Isso inicializa os comandos do menu da lista MRU.

    ```csharp
    private void InitMRUMenu(OleMenuCommandService mcs)
    {
        InitializeMRUList();
        for (int i = 0; i < this.numMRUItems; i++)
        {
            var cmdID = new CommandID(
                new Guid(TestCommandPackageGuids.guidTestCommandPackageCmdSet), this.baseMRUID + i);
            var mc = new OleMenuCommand(
                new EventHandler(OnMRUExec), cmdID);
            mc.BeforeQueryStatus += new EventHandler(OnMRUQueryStatus);
            mcs.AddCommand(mc);
        }
    }
    ```

    Você deve criar um objeto de comando de menu para cada item possível na lista MRU. O IDE chama o `OnMRUQueryStatus` método para cada item na lista MRU até que não haja mais itens. No código gerenciado, a única maneira para o IDE saber que não há mais nenhum item é criar todos os itens possíveis primeiro. Se desejar, você pode marcar itens adicionais como não visíveis primeiro usando `mc.Visible = false;` depois que o comando de menu for criado. Esses itens podem então ser visíveis mais tarde, usando `mc.Visible = true;` o no `OnMRUQueryStatus` método.

6. Depois do `InitMRUMenu` método, adicione o método a seguir `OnMRUQueryStatus` . Esse é o manipulador que define o texto para cada item MRU.

    ```csharp
    private void OnMRUQueryStatus(object sender, EventArgs e)
    {
        OleMenuCommand menuCommand = sender as OleMenuCommand;
        if (null != menuCommand)
        {
            int MRUItemIndex = menuCommand.CommandID.ID - this.baseMRUID;
            if (MRUItemIndex >= 0 && MRUItemIndex < this.mruList.Count)
            {
                menuCommand.Text = this.mruList[MRUItemIndex] as string;
            }
        }
    }
    ```

7. Depois do `OnMRUQueryStatus` método, adicione o método a seguir `OnMRUExec` . Este é o manipulador para selecionar um item MRU. Esse método move o item selecionado para a parte superior da lista e, em seguida, exibe o item selecionado em uma caixa de mensagem.

    ```csharp
    private void OnMRUExec(object sender, EventArgs e)
    {
        var menuCommand = sender as OleMenuCommand;
        if (null != menuCommand)
        {
            int MRUItemIndex = menuCommand.CommandID.ID - this.baseMRUID;
            if (MRUItemIndex >= 0 && MRUItemIndex < this.mruList.Count)
            {
                string selection = this.mruList[MRUItemIndex] as string;
                for (int i = MRUItemIndex; i > 0; i--)
                {
                    this.mruList[i] = this.mruList[i - 1];
                }
                this.mruList[0] = selection;
                System.Windows.Forms.MessageBox.Show(
                    string.Format(CultureInfo.CurrentCulture,
                                  "Selected {0}", selection));
            }
        }
    }
    ```

## <a name="testing-the-mru-list"></a>Testando a lista MRU

1. Compile o projeto e comece a depuração.

2. No menu **TestMenu** , clique em **invocar TestCommand**. Isso exibe uma caixa de mensagem que indica que o comando foi selecionado.

    > [!NOTE]
    > Essa etapa é necessária para forçar o VSPackage a carregar e exibir corretamente a lista MRU. Se você ignorar essa etapa, a lista MRU não será exibida.

3. No menu de **menu de teste** , clique em **submenu**. Uma lista de quatro itens é exibida no final do submenu, abaixo de um separador. Quando você clica no **item 3**, uma caixa de mensagem deve aparecer e exibir o texto, **item 3 selecionado**. (Se a lista de quatro itens não for exibida, verifique se você seguiu as instruções na etapa anterior.)

4. Abra o submenu novamente. Observe que o **item 3** agora está na parte superior da lista e os outros itens foram empurrados uma posição para baixo. Clique no **item 3** novamente e observe que a caixa de mensagem ainda exibe o **item 3 selecionado**, que indica que o texto foi movido corretamente para a nova posição junto com o rótulo de comando.

## <a name="see-also"></a>Confira também
- [Adicionando dinamicamente itens de menu](../extensibility/dynamically-adding-menu-items.md)
