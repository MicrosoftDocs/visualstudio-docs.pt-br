---
title: Adição dinâmica de itens de Menu | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- DYNAMICITEMSTART
- menu items, adding dynamically
- menus, adding dynamic items
ms.assetid: d281e9c9-b289-4d64-8d0a-094bac6c333c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 69a6b50702f444064715e08b31a1b014f8a1028f
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39639663"
---
# <a name="dynamically-add-menu-items"></a>Adicionar dinamicamente os itens de menu
Você pode adicionar itens de menu no tempo de execução, especificando o `DynamicItemStart` comando sinalizador em uma definição de botão do espaço reservado da tabela de comando do Visual Studio (*VSCT*) arquivos, em seguida, definindo (no código), o número de itens de menu a exibir e manipulação de comando (s). Quando o VSPackage é carregado, o espaço reservado é substituído com os itens de menu dinâmico.  
  
 O Visual Studio usa as listas dinâmicas a **usados recentemente** lista (MRU), que exibe os nomes dos documentos que foram abertos recentemente, e o **Windows** lista, que exibe os nomes do windows que estão abertos no momento.   O `DynamicItemStart` sinalizador em uma definição de comando Especifica que o comando é um espaço reservado até o VSPackage é aberto. Quando o VSPackage é aberto, o espaço reservado é substituído por 0 ou mais comandos que são criados em tempo de execução e adicionados à lista dinâmica. Você não poderá ver a posição no menu de onde a lista dinâmica aparece até que o VSPackage é aberto.  Para popular a lista dinâmica, o Visual Studio solicita o VSPackage para procurar um comando com uma ID cujos primeiros caracteres são o mesmo que a ID do espaço reservado. Quando o Visual Studio encontra um comando, ele adiciona o nome do comando para a lista dinâmica. Em seguida, ele incrementa a identificação e procura por outro comando correspondente para adicionar à lista dinâmica até que não existam comandos sem mais dinâmicos.  
  
 Este passo a passo mostra como definir o projeto de inicialização em uma solução do Visual Studio com um comando para o **Gerenciador de soluções** barra de ferramentas. Ele usa um controlador de menu que tenha uma lista suspensa dinâmica dos projetos na solução ativa. Para evitar esse comando apareça quando nenhuma solução está aberta ou quando a solução aberta tem apenas um projeto, o VSPackage é carregado apenas quando uma solução tem vários projetos.  
  
 Para obter mais informações sobre *VSCT* arquivos, consulte [arquivos de tabela (. VSCT) de comando do Visual Studio](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).  
  
## <a name="create-an-extension-with-a-menu-command"></a>Criar uma extensão com um comando de menu  
  
1.  Crie um projeto do VSIX chamado `DynamicMenuItems`.  
  
2.  Quando o projeto é aberto, adicione um modelo de item de comando personalizado e denomine- **DynamicMenu**. Para obter mais informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
## <a name="setting-up-the-elements-in-the-vsct-file"></a>Como configurar os elementos na *VSCT* arquivo  
 Para criar um controlador de menu com itens de menu dinâmico em uma barra de ferramentas, você deve especificar os seguintes elementos:  
  
-   Dois grupos, um que contém o controlador de menu e outra que contém os itens de menu no menu suspenso de comando  
  
-   Elemento de um menu do tipo `MenuController`  
  
-   Dois botões, que atua como o espaço reservado para os itens de menu e outro que fornece o ícone e a dica de ferramenta na barra de ferramentas.  
  
1.  Na *DynamicMenuPackage.vsct*, defina as IDs de comando. Vá para a seção de símbolos e substituir os elementos de IDSymbol na **guidDynamicMenuPackageCmdSet** GuidSymbol bloco. Você precisa definir IDSymbol elementos para os dois grupos, o controlador de menu, o comando de espaço reservado e o comando de âncora.  
  
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
  
2.  Na seção grupos, exclua os grupos existentes e adicione os dois grupos que você acabou de definir:  
  
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
  
     Adicione o MenuController. Defina o sinalizador de comando do DynamicVisibility, já que nem sempre é visível. O ButtonText não é exibido.  
  
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
  
3.  Adicione dois botões, um como um espaço reservado para os itens de menu dinâmico e outro como uma âncora para o MenuController.  
  
     O pai do botão de espaço reservado é a **MyMenuControllerGroup**. Adicione os sinalizadores de comando DynamicItemStart, DynamicVisibility e textoAltera ao botão de espaço reservado. O ButtonText não é exibido.  
  
     O botão de âncora contém o ícone e o texto de dica de ferramenta. O pai do botão âncora é também o **MyMenuControllerGroup**. Adicione o sinalizador de comando NoShowOnMenuController para garantir que o botão, na verdade, não aparece no menu suspenso de controlador e o sinalizador de comando FixMenuController para torná-lo a âncora permanente.  
  
    ```xml  
    <!-- The placeholder for the dynamic items that expand to N items at runtime. -->  
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
  
4.  Adicionar um ícone para o projeto (na *recursos* pasta) e, em seguida, adicione a referência a ele na *VSCT* arquivo. Neste passo a passo, usamos o ícone de setas que está incluído no modelo de projeto.  
  
5.  Adicione uma seção VisibilityConstraints fora da seção de comandos apenas antes da seção de símbolos. (Você pode receber um aviso se você adicioná-lo depois de símbolos). Esta seção garante que o controlador de menu aparece somente quando uma solução com vários projetos é carregada.  
  
    ```xml  
    <VisibilityConstraints>  
         <!--Make the MenuController show up only when there is a solution with more than one project loaded-->  
        <VisibilityItem guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" context="UICONTEXT_SolutionHasMultipleProjects"/>  
    </VisibilityConstraints>  
    ```  
  
## <a name="implement-the-dynamic-menu-command"></a>Implementar o comando de menu dinâmico  
 Você cria uma classe de comando de menu dinâmico que herda de <xref:Microsoft.VisualStudio.Shell.OleMenuCommand>. Nessa implementação, o construtor Especifica um predicado a ser usado para correspondência de comandos. Você deve substituir a <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A> método para usar esse predicado para definir o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A> propriedade, que identifica o comando a ser invocado.  
  
1.  Criar um nova classe arquivo c# chamado *DynamicItemMenuCommand.cs*, e adicione uma classe chamada **DynamicItemMenuCommand** que herda de <xref:Microsoft.VisualStudio.Shell.OleMenuCommand>:  
  
    ```csharp  
    class DynamicItemMenuCommand : OleMenuCommand  
    {  
  
    }  
  
    ```  
  
2.  Adicione as seguintes instruções using:  
  
    ```csharp  
    using Microsoft.VisualStudio.Shell;  
    using Microsoft.VisualStudio.Shell.Interop;  
    using System.ComponentModel.Design;  
    ```  
  
3.  Adicione um campo particular para armazenar o predicado de correspondência:  
  
    ```csharp  
    private Predicate<int> matches;  
  
    ```  
  
4.  Adicione um construtor que herda de <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> construtor e especifica um manipulador de comandos e um <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> manipulador. Adicione um predicado para o comando de correspondência:  
  
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
  
5.  Substituir a <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A> , de modo que ele chama as correspondências de predicado e conjuntos de <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A> propriedade:  
  
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
  
## <a name="add-the-command"></a>Adicione o comando  
 O construtor de DynamicMenu é onde você configurar os comandos de menu, incluindo menus dinâmicos e itens de menu.  
  
1.  Na *DynamicMenuPackage.cs*, adicione o GUID do conjunto de comandos e a ID de comando:  
  
    ```csharp  
    public const string guidDynamicMenuPackageCmdSet = "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file  
    public const uint cmdidMyCommand = 0x104;  
    ```  
  
2.  No *DynamicMenu.cs* arquivo, adicione as seguintes instruções using:  
  
    ```csharp  
    using EnvDTE;  
    using EnvDTE80;  
    using System.ComponentModel.Design;  
    ```  
  
3.  No `DynamicMenu` classe, adicione um campo particular **dte2**.  
  
    ```csharp  
    private DTE2 dte2;  
    ```  
  
4.  Adicione um campo particular rootItemId:  
  
    ```csharp  
    private int rootItemId = 0;  
    ```  
  
5.  No construtor de DynamicMenu, adicione o comando de menu. Na próxima seção, definiremos o manipulador de comando, o `BeforeQueryStatus` manipulador de eventos e o predicado de correspondência.  
  
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
  
## <a name="implement-the-handlers"></a>Implemente os manipuladores  
 Para implementar itens de menu dinâmico em um controlador de menu, você deve tratar o comando quando um item dinâmico é clicado. Você também deve implementar a lógica que define o estado do item de menu. Adicione os manipuladores para o `DynamicMenu` classe.  
  
1.  Para implementar o **defina o projeto de inicialização** de comando, adicione o **OnInvokedDynamicItem** manipulador de eventos. Ele procura o projeto cujo nome é o mesmo que o texto do comando que foi invocado e o define como o projeto de inicialização, definindo seu caminho absoluto no <xref:EnvDTE.SolutionBuild.StartupProjects%2A> propriedade.  
  
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
  
2.  Adicionar o `OnBeforeQueryStatusDynamicItem` manipulador de eventos. Isso é chamado antes do manipulador de um `QueryStatus` eventos. Ele determina se o item de menu é um item "real", ou seja, não o item do espaço reservado, e se o item já está marcado (o que significa que o projeto já está definido como o projeto de inicialização).  
  
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
  
Agora, implemente o predicado de correspondência. Precisamos determinar duas coisas: primeiro, se a ID de comando é válida (ele é maior que ou igual à ID do comando declarado) e o segundo, se ele especifica um projeto possíveis (ele é menor que o número de projetos na solução).
  
    ```csharp  
    private bool IsValidDynamicItem(int commandId)  
    {  
        // The match is valid if the command ID is >= the id of our root dynamic start item   
        // and the command ID minus the ID of our root dynamic start item  
        // is less than or equal to the number of projects in the solution.  
        return (commandId >= (int)DynamicMenuPackageGuids.cmdidMyCommand) && ((commandId - (int)DynamicMenuPackageGuids.cmdidMyCommand) < dte2.Solution.Projects.Count);  
    }  
    ```  
  
## <a name="set-the-vspackage-to-load-only-when-a-solution-has-multiple-projects"></a>Defina o VSPackage sejam carregadas somente quando uma solução tem vários projetos  
 Porque o **projeto de inicialização definido** comando não faz sentido, a menos que a solução ativa tem mais de um projeto, você pode definir o VSPackage para carregar automaticamente somente nesse caso. Você usa <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> junto com o contexto de interface do usuário <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids.SolutionHasMultipleProjects>. No *DynamicMenuPackage.cs* arquivo adicione os seguintes atributos à classe DynamicMenuPackage:  
  
```csharp  
[PackageRegistration(UseManagedResourcesOnly = true)]  
[InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]  
[ProvideMenuResource("Menus.ctmenu", 1)]  
[ProvideAutoLoad(UIContextGuids.SolutionHasMultipleProjects)]  
[Guid(DynamicMenuPackage.PackageGuidString)]  
public sealed class DynamicMenuItemsPackage : Package  
{}  
```  
  
## <a name="test-the-set-startup-project-command"></a>O comando de projeto de inicialização do conjunto de teste  
 Agora você pode testar seu código.  
  
1.  Compile o projeto e comece a depuração. A instância experimental deve aparecer.  
  
2.  Na instância experimental, abra uma solução que tem mais de um projeto.  
  
     Você verá o ícone de seta para a **Gerenciador de soluções** barra de ferramentas. Ao expandir, itens de menu que representam os diferentes projetos na solução devem aparecer.  
  
3.  Quando você marca um dos projetos, torna-se o projeto de inicialização.  
  
4.  Quando você fecha a solução ou abre uma solução que tem apenas um projeto, o ícone de barra de ferramentas deve desaparecer.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)   
 [Como os VSPackages adicionam elementos da interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md)