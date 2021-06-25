---
title: Adicionando dinamicamente itens de menu | Microsoft Docs
description: Saiba como usar o sinalizador de comando DynamicItemStart para adicionar itens de menu em tempo de execução. Este artigo mostra como definir o projeto de inicialização em uma solução do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- DYNAMICITEMSTART
- menu items, adding dynamically
- menus, adding dynamic items
ms.assetid: d281e9c9-b289-4d64-8d0a-094bac6c333c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6867baafa45ca794f65b4cb0cc365dbebfbd4219
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898351"
---
# <a name="dynamically-add-menu-items"></a>Adicionar dinamicamente itens de menu
Você pode adicionar itens de menu em tempo de execução especificando o `DynamicItemStart` sinalizador de comando em uma definição de botão de espaço reservado no arquivo de tabela de comandos do Visual Studio (*. vsct*) e, em seguida, definindo (no código) o número de itens de menu a serem exibidos e manipulando os comandos. Quando o VSPackage é carregado, o espaço reservado é substituído pelos itens de menu dinâmico.

 O Visual Studio usa listas dinâmicas na lista MRU ( **usada mais recentemente** ), que exibe os nomes dos documentos que foram abertos recentemente e a lista do **Windows** , que exibe os nomes das janelas que estão abertas no momento.   O `DynamicItemStart` sinalizador em uma definição de comando especifica que o comando é um espaço reservado até que o VSPackage seja aberto. Quando o VSPackage é aberto, o espaço reservado é substituído por 0 ou mais comandos que são criados em tempo de execução e adicionados à lista dinâmica. Talvez você não consiga ver a posição no menu em que a lista dinâmica aparece até que o VSPackage seja aberto.  Para preencher a lista dinâmica, o Visual Studio solicita que o VSPackage procure um comando com uma ID cujos primeiros caracteres sejam iguais aos da ID do espaço reservado. Quando o Visual Studio encontra um comando correspondente, ele adiciona o nome do comando à lista dinâmica. Em seguida, ele incrementa a ID e procura outro comando correspondente para adicionar à lista dinâmica até que não haja mais comandos dinâmicos.

 Este tutorial mostra como definir o projeto de inicialização em uma solução do Visual Studio com um comando na barra de ferramentas **Gerenciador de soluções** . Ele usa um controlador de menu que tem uma lista suspensa dinâmica dos projetos na solução ativa. Para evitar que esse comando apareça quando nenhuma solução estiver aberta ou quando a solução aberta tiver apenas um projeto, o VSPackage só será carregado quando uma solução tiver vários projetos.

 Para obter mais informações sobre arquivos *. vsct* , consulte [arquivos de tabela de comando do Visual Studio (. vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).

## <a name="create-an-extension-with-a-menu-command"></a>Criar uma extensão com um comando de menu

1. Crie um projeto VSIX denominado `DynamicMenuItems` .

2. Quando o projeto for aberto, adicione um modelo de item de comando personalizado e nomeie-o **DynamicMenu**. Para obter mais informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).

## <a name="setting-up-the-elements-in-the-vsct-file"></a>Configurando os elementos no arquivo *. vsct*
 Para criar um controlador de menu com itens de menu dinâmicos em uma barra de ferramentas, você deve especificar os seguintes elementos:

- Dois grupos de comandos, um que contém o controlador de menu e outro que contém os itens de menu na lista suspensa

- Um elemento de menu do tipo `MenuController`

- Dois botões, um que atua como o espaço reservado para os itens de menu e outro que fornece o ícone e a dica de ferramenta na barra de ferramentas.

1. Em *DynamicMenuPackage. vsct*, defina as IDs de comando. Vá para a seção símbolos e substitua os elementos IDSymbol no bloco **guidDynamicMenuPackageCmdSet** GuidSymbol. Você precisa definir elementos IDSymbol para os dois grupos, o controlador de menu, o comando de espaço reservado e o comando de âncora.

    ```xml
    <GuidSymbol name="guidDynamicMenuPackageCmdSet" value="{ your GUID here }">
        <IDSymbol name="MyToolbarItemGroup" value="0x1020" />
        <IDSymbol name="MyMenuControllerGroup" value="0x1025" />
        <IDSymbol name="MyMenuController" value ="0x1030"/>
        <IDSymbol name="cmdidMyAnchorCommand" value="0x0103" />
        <!-- NOTE: The following command expands at run time to some number of ids.
         Try not to place command ids after it (e.g. 0x0105, 0x0106).
         If you must add a command id after it, make the gap very large (e.g. 0x200) -->
        <IDSymbol name="cmdidMyDynamicStartCommand" value="0x0104" />
    </GuidSymbol>
    ```

2. Na seção grupos, exclua os grupos existentes e adicione os dois grupos que você acabou de definir:

    ```xml
    <Groups>
        <!-- The group that adds the MenuController on the Solution Explorer toolbar.
             The 0x4000 priority adds this group after the group that contains the
             Preview Selected Items button, which is normally at the far right of the toolbar. -->
        <Group guid="guidDynamicMenuPackageCmdSet" id="MyToolbarItemGroup" priority="0x4000" >
            <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN" />
        </Group>
        <!-- The group for the items on the MenuController drop-down. It is added to the MenuController submenu. -->
        <Group guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" priority="0x4000" >
            <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" />
        </Group>
    </Groups>
    ```

     Adicione o MenuController. Defina o sinalizador de comando DynamicVisibility, pois ele nem sempre está visível. O ButtonText não é exibido.

    ```xml
    <Menus>
        <!-- The MenuController to display on the Solution Explorer toolbar.
             Place it in the ToolbarItemGroup.-->
        <Menu guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" priority="0x1000" type="MenuController">
            <Parent guid="guidDynamicMenuPackageCmdSet" id="MyToolbarItemGroup" />
            <CommandFlag>DynamicVisibility</CommandFlag>
            <Strings>
               <ButtonText></ButtonText>
           </Strings>
        </Menu>
    </Menus>
    ```

3. Adicione dois botões, um como um espaço reservado para os itens de menu dinâmico e um como uma âncora para o MenuController.

     O pai do botão de espaço reservado é o **MyMenuControllerGroup**. Adicione os sinalizadores de comando DynamicItemStart, DynamicVisibility e textchanges ao botão de espaço reservado. O ButtonText não é exibido.

     O botão âncora contém o ícone e o texto da dica de ferramenta. O pai do botão de âncora também é o **MyMenuControllerGroup**. Você adiciona o sinalizador de comando NoShowOnMenuController para certificar-se de que o botão não aparece realmente na lista suspensa do controlador de menu e o sinalizador de comando FixMenuController para torná-lo a âncora permanente.

    ```xml
    <!-- The placeholder for the dynamic items that expand to N items at run time. -->
    <Buttons>
        <Button guid="guidDynamicMenuPackageCmdSet" id="cmdidMyDynamicStartCommand" priority="0x1000" >
          <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" />
          <CommandFlag>DynamicItemStart</CommandFlag>
          <CommandFlag>DynamicVisibility</CommandFlag>
          <CommandFlag>TextChanges</CommandFlag>
          <!-- This text does not appear. -->
          <Strings>
            <ButtonText>Project</ButtonText>
          </Strings>
        </Button>

        <!-- The anchor item to supply the icon/tooltip for the MenuController -->
        <Button guid="guidDynamicMenuPackageCmdSet" id="cmdidMyAnchorCommand" priority="0x0000" >
          <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" />
          <!-- This is the icon that appears on the Solution Explorer toolbar. -->
          <Icon guid="guidImages" id="bmpPicArrows"/>
          <!-- Do not show on the menu controller's drop down list-->
          <CommandFlag>NoShowOnMenuController</CommandFlag>
          <!-- Become the permanent anchor item for the menu controller -->
          <CommandFlag>FixMenuController</CommandFlag>
          <!-- The text that appears in the tooltip.-->
          <Strings>
            <ButtonText>Set Startup Project</ButtonText>
          </Strings>
        </Button>
    </Buttons>
    ```

4. Adicione um ícone ao projeto (na pasta de *recursos* ) e, em seguida, adicione a referência a ele no arquivo *. vsct* . Neste tutorial, usamos o ícone de setas que é incluído no modelo de projeto.

5. Adicione uma seção VisibilityConstraints fora da seção comandos logo antes da seção Symbols. (Você poderá receber um aviso se adicioná-lo após símbolos.) Esta seção garante que o controlador de menu apareça somente quando uma solução com vários projetos for carregada.

    ```xml
    <VisibilityConstraints>
         <!--Make the MenuController show up only when there is a solution with more than one project loaded-->
        <VisibilityItem guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" context="UICONTEXT_SolutionHasMultipleProjects"/>
    </VisibilityConstraints>
    ```

## <a name="implement-the-dynamic-menu-command"></a>Implementar o comando de menu dinâmico
 Você cria uma classe de comando de menu dinâmico que herda de <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> . Nessa implementação, o construtor Especifica um predicado a ser usado para comandos correspondentes. Você deve substituir o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A> método para usar esse predicado para definir a <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A> propriedade, que identifica o comando a ser invocado.

1. Crie um novo arquivo de classe C# chamado *DynamicItemMenuCommand. cs* e adicione uma classe chamada **DynamicItemMenuCommand** que herde de <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> :

    ```csharp
    class DynamicItemMenuCommand : OleMenuCommand
    {

    }

    ```

2. Adicione o seguinte usando as orientações:

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.Shell.Interop;
    using System.ComponentModel.Design;
    ```

3. Adicione um campo particular para armazenar o predicado de correspondência:

    ```csharp
    private Predicate<int> matches;

    ```

4. Adicione um construtor que herde do <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> Construtor e especifique um manipulador de comandos e um <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> manipulador. Adicione um predicado para corresponder ao comando:

    ```csharp
    public DynamicItemMenuCommand(CommandID rootId, Predicate<int> matches, EventHandler invokeHandler, EventHandler beforeQueryStatusHandler)
        : base(invokeHandler, null /*changeHandler*/, beforeQueryStatusHandler, rootId)
    {
        if (matches == null)
        {
            throw new ArgumentNullException("matches");
        }

        this.matches = matches;
    }
    ```

5. Substitua o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A> método para que ele chame o predicado de correspondências e defina a <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A> Propriedade:

    ```csharp
    public override bool DynamicItemMatch(int cmdId)
    {
        // Call the supplied predicate to test whether the given cmdId is a match.
        // If it is, store the command id in MatchedCommandid
        // for use by any BeforeQueryStatus handlers, and then return that it is a match.
        // Otherwise clear any previously stored matched cmdId and return that it is not a match.
        if (this.matches(cmdId))
        {
            this.MatchedCommandId = cmdId;
            return true;
        }

        this.MatchedCommandId = 0;
        return false;
    }
    ```

## <a name="add-the-command"></a>Adicionar o comando
 O Construtor DynamicMenu é onde você configura comandos de menu, incluindo menus dinâmicos e itens de menu.

1. Em *DynamicMenuPackage. cs*, adicione o GUID do conjunto de comandos e a ID do comando:

    ```csharp
    public const string guidDynamicMenuPackageCmdSet = "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file
    public const uint cmdidMyCommand = 0x104;
    ```

2. No arquivo *DynamicMenu. cs* , adicione as seguintes diretivas using:

    ```csharp
    using EnvDTE;
    using EnvDTE80;
    using System.ComponentModel.Design;
    ```

3. Na `DynamicMenu` classe, adicione um campo privado **DTE2**.

    ```csharp
    private DTE2 dte2;
    ```

4. Adicione um campo rootItemId particular:

    ```csharp
    private int rootItemId = 0;
    ```

5. No Construtor DynamicMenu, adicione o comando de menu. Na próxima seção, vamos definir o manipulador de comandos, o `BeforeQueryStatus` manipulador de eventos e o predicado Match.

    ```csharp
    private DynamicMenu(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException(nameof(package));
        }

        this.package = package;

        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        if (commandService != null)
        {
            // Add the DynamicItemMenuCommand for the expansion of the root item into N items at run time.
            CommandID dynamicItemRootId = new CommandID(new Guid(DynamicMenuPackageGuids.guidDynamicMenuPackageCmdSet), (int)DynamicMenuPackageGuids.cmdidMyCommand);
            DynamicItemMenuCommand dynamicMenuCommand = new DynamicItemMenuCommand(dynamicItemRootId,
                IsValidDynamicItem,
                OnInvokedDynamicItem,
                OnBeforeQueryStatusDynamicItem);
                commandService.AddCommand(dynamicMenuCommand);
                }

        dte2 = (DTE2)this.ServiceProvider.GetService(typeof(DTE));
    }
    ```

## <a name="implement-the-handlers"></a>Implementar os manipuladores
 Para implementar itens de menu dinâmico em um controlador de menu, você deve manipular o comando quando um item dinâmico é clicado. Você também deve implementar a lógica que define o estado do item de menu. Adicione os manipuladores à `DynamicMenu` classe.

1. Para implementar o comando **set StartUp Project** , adicione o manipulador de eventos **OnInvokedDynamicItem** . Ele procura o projeto cujo nome é o mesmo que o texto do comando que foi invocado e o define como o projeto de inicialização definindo seu caminho absoluto na <xref:EnvDTE.SolutionBuild.StartupProjects%2A> propriedade.

    ```csharp
    private void OnInvokedDynamicItem(object sender, EventArgs args)
    {
        DynamicItemMenuCommand invokedCommand = (DynamicItemMenuCommand)sender;
        // If the command is already checked, we don't need to do anything
        if (invokedCommand.Checked)
            return;

        // Find the project that corresponds to the command text and set it as the startup project
        var projects = dte2.Solution.Projects;
        foreach (Project proj in projects)
        {
            if (invokedCommand.Text.Equals(proj.Name))
            {
                dte2.Solution.SolutionBuild.StartupProjects = proj.FullName;
                return;
            }
        }
    }
    ```

2. Adicione o `OnBeforeQueryStatusDynamicItem` manipulador de eventos. Este é o manipulador chamado antes de um `QueryStatus` evento. Ele determina se o item de menu é um item "real", ou seja, não o item de espaço reservado e se o item já está marcado (o que significa que o projeto já está definido como o projeto de inicialização).

    ```csharp
    private void OnBeforeQueryStatusDynamicItem(object sender, EventArgs args)
    {
        DynamicItemMenuCommand matchedCommand = (DynamicItemMenuCommand)sender;
        matchedCommand.Enabled = true;
        matchedCommand.Visible = true;

        // Find out whether the command ID is 0, which is the ID of the root item.
        // If it is the root item, it matches the constructed DynamicItemMenuCommand,
         // and IsValidDynamicItem won't be called.
        bool isRootItem = (matchedCommand.MatchedCommandId == 0);

        // The index is set to 1 rather than 0 because the Solution.Projects collection is 1-based.
        int indexForDisplay = (isRootItem ? 1 : (matchedCommand.MatchedCommandId - (int) DynamicMenuPackageGuids.cmdidMyCommand) + 1);

        matchedCommand.Text = dte2.Solution.Projects.Item(indexForDisplay).Name;

        Array startupProjects = (Array)dte2.Solution.SolutionBuild.StartupProjects;
        string startupProject = System.IO.Path.GetFileNameWithoutExtension((string)startupProjects.GetValue(0));

        // Check the command if it isn't checked already selected
        matchedCommand.Checked = (matchedCommand.Text == startupProject);

        // Clear the ID because we are done with this item.
        matchedCommand.MatchedCommandId = 0;
    }
    ```

## <a name="implement-the-command-id-match-predicate"></a>Implementar o predicado de correspondência de ID de comando

Agora implemente o predicado Match. Precisamos determinar duas coisas: primeiro, se a ID de comando é válida (é maior ou igual à ID de comando declarada) e segundo, se ela especifica um projeto possível (é menor do que o número de projetos na solução).

```csharp
private bool IsValidDynamicItem(int commandId)
{
    // The match is valid if the command ID is >= the id of our root dynamic start item
    // and the command ID minus the ID of our root dynamic start item
    // is less than or equal to the number of projects in the solution.
    return (commandId >= (int)DynamicMenuPackageGuids.cmdidMyCommand) && ((commandId - (int)DynamicMenuPackageGuids.cmdidMyCommand) < dte2.Solution.Projects.Count);
}
```

## <a name="set-the-vspackage-to-load-only-when-a-solution-has-multiple-projects"></a>Definir o VSPackage para carregar somente quando uma solução tiver vários projetos
 Como o comando **set StartUp Project** não faz sentido, a menos que a solução ativa tenha mais de um projeto, você pode definir seu VSPackage para carregar automaticamente somente nesse caso. Você usa <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> junto com o contexto da interface do usuário <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids.SolutionHasMultipleProjects> . No arquivo *DynamicMenuPackage. cs* , adicione os seguintes atributos à classe DynamicMenuPackage:

```csharp
[PackageRegistration(UseManagedResourcesOnly = true)]
[InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
[ProvideMenuResource("Menus.ctmenu", 1)]
[ProvideAutoLoad(UIContextGuids.SolutionHasMultipleProjects)]
[Guid(DynamicMenuPackage.PackageGuidString)]
public sealed class DynamicMenuItemsPackage : Package
{}
```

## <a name="test-the-set-startup-project-command"></a>Testar o comando Set StartUp Project
 Agora você pode testar seu código.

1. Compile o projeto e comece a depuração. A instância experimental deve aparecer.

2. Na instância experimental, abra uma solução que tenha mais de um projeto.

     Você deve ver o ícone de seta na barra de ferramentas **Gerenciador de soluções** . Quando você o expande, os itens de menu que representam os diferentes projetos na solução devem aparecer.

3. Quando você marca um dos projetos, ele se torna o projeto de inicialização.

4. Quando você fecha a solução ou abre uma solução que tem apenas um projeto, o ícone da barra de ferramentas deve desaparecer.

## <a name="see-also"></a>Confira também
- [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)
- [Como VSPackages adicionar elementos da interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
