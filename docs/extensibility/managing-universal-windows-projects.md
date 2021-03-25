---
title: Gerenciando projetos universais do Windows | Microsoft Docs
description: Para dar suporte a aplicativos universais do Windows, as extensões do Visual Studio que gerenciam projetos devem estar cientes da estrutura do projeto de aplicativo universal do Windows.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 47926aa1-3b41-410d-bca8-f77fc950cbe7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8af418d8ffcaad18aca4497078f4e24f9bb679fd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090636"
---
# <a name="manage-universal-windows-projects"></a>Gerenciar projetos universais do Windows

Aplicativos universais do Windows são aplicativos direcionados Windows 8.1 e Windows Phone 8,1, permitindo que os desenvolvedores usem código e outros ativos em ambas as plataformas. O código compartilhado e os recursos são mantidos em um projeto compartilhado, enquanto o código e os recursos específicos da plataforma são mantidos em projetos separados, um para o Windows e outro para Windows Phone. Para obter mais informações sobre aplicativos universais do Windows, consulte [aplicativos universais do Windows](/windows/uwp/get-started/create-uwp-apps). As extensões do Visual Studio que gerenciam projetos devem estar cientes de que os projetos de aplicativos universais do Windows têm uma estrutura que difere dos aplicativos de plataforma única. Este tutorial mostra como navegar no projeto compartilhado e gerenciar os itens compartilhados.

## <a name="prerequisites"></a>Pré-requisitos

A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele está incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

### <a name="navigate-the-shared-project"></a>Navegar no projeto compartilhado

1. Crie um projeto VSIX em C# chamado **TestUniversalProject**. (**Arquivo**  >  **Novo**  >  **Projeto** e, em seguida, extensibilidade **C#**  >    >  **pacote do Visual Studio**). Adicione um modelo de item de projeto de **comando personalizado** (na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >  **novo item** e vá para **extensibilidade**). Nomeie o arquivo **TestUniversalProject**.

2. Adicione uma referência a *Microsoft.VisualStudio.Shell.Interop.12.1.DesignTime.dll* e *Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll* (na seção **extensões** ).

3. Abra *TestUniversalProject. cs* e adicione as seguintes `using` diretivas:

    ```csharp
    using EnvDTE;
    using EnvDTE80;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.PlatformUI;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    using System.Collections.Generic;
    using System.IO;
    using System.Windows.Forms;
    ```

4. Na `TestUniversalProject` classe, adicione um campo privado apontando para a janela **saída** .

    ```csharp
    public sealed class TestUniversalProject
    {
        IVsOutputWindowPane output;
    . . .
    }
    ```

5. Defina a referência ao painel de saída dentro do Construtor TestUniversalProject:

    ```csharp
    private TestUniversalProject(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException("package");
        }

        this.package = package;

        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        if (commandService != null)
        {
            CommandID menuCommandID = new CommandID(MenuGroup, CommandId);
            EventHandler eventHandler = this.ShowMessageBox;
            MenuCommand menuItem = new MenuCommand(eventHandler, menuCommandID);
            commandService.AddCommand(menuItem);
        }

        // get a reference to the Output window
        output = (IVsOutputWindowPane)ServiceProvider.GetService(typeof(SVsGeneralOutputWindowPane));
    }
    ```

6. Remova o código existente do `ShowMessageBox` método:

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
    }
    ```

7. Obtenha o objeto DTE, que usaremos para várias finalidades diferentes neste passo a passos. Além disso, certifique-se de que uma solução seja carregada quando o botão de menu for clicado.

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        var dte = (EnvDTE.DTE)this.ServiceProvider.GetService(typeof(EnvDTE.DTE));
        if (dte.Solution != null)
        {
            . . .
        }
        else
        {
            MessageBox.Show("No solution is open");
            return;
        }
    }
    ```

8. Localize o projeto compartilhado. O projeto compartilhado é um contêiner puro; Ele não cria ou produz saídas. O método a seguir localiza o primeiro projeto compartilhado na solução procurando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> objeto que tem o recurso de projeto compartilhado.

    ```csharp
    private IVsHierarchy FindSharedProject()
    {
        var sln = (IVsSolution)this.ServiceProvider.GetService(typeof(SVsSolution));
        Guid empty = Guid.Empty;
        IEnumHierarchies enumHiers;

        //get all the projects in the solution
        ErrorHandler.ThrowOnFailure(sln.GetProjectEnum((uint)__VSENUMPROJFLAGS.EPF_LOADEDINSOLUTION, ref empty, out enumHiers));
        foreach (IVsHierarchy hier in ComUtilities.EnumerableFrom(enumHiers))
        {
            if (PackageUtilities.IsCapabilityMatch(hier, "SharedAssetsProject"))
            {
                return hier;
            }
        }
        return null;
    }
    ```

9. No `ShowMessageBox` método, gere a legenda (o nome do projeto que aparece na **Gerenciador de soluções**) do projeto compartilhado.

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        var dte = (DTE)this.ServiceProvider.GetService(typeof(DTE));

        if (dte.Solution != null)
        {
            var sharedHier = this.FindSharedProject();
            if (sharedHier != null)
            {
                string sharedCaption = HierarchyUtilities.GetHierarchyProperty<string>(sharedHier, (uint)VSConstants.VSITEMID.Root,
                     (int)__VSHPROPID.VSHPROPID_Caption);
                output.OutputStringThreadSafe(string.Format("Found shared project: {0}\n", sharedCaption));
            }
            else
            {
                MessageBox.Show("Solution has no shared project");
                return;
            }
        }
        else
        {
            MessageBox.Show("No solution is open");
            return;
        }
    }
    ```

10. Obtenha o projeto da plataforma ativa. Os projetos de plataforma são os projetos que contêm código e recursos específicos da plataforma. O método a seguir usa o novo campo <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy> para obter o projeto da plataforma ativa.

    ```csharp
    private IVsHierarchy GetActiveProjectContext(IVsHierarchy hierarchy)
    {
        IVsHierarchy activeProjectContext;
        if (HierarchyUtilities.TryGetHierarchyProperty(hierarchy, (uint)VSConstants.VSITEMID.Root,
             (int)__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy, out activeProjectContext))
        {
            return activeProjectContext;
        }
        else
        {
            return null;
        }
    }
    ```

11. No `ShowMessageBox` método, gere a legenda do projeto da plataforma ativa.

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        var dte = (DTE)this.ServiceProvider.GetService(typeof(DTE));

        if (dte.Solution != null)
        {
            var sharedHier = this.FindSharedProject();
            if (sharedHier != null)
            {
                string sharedCaption = HierarchyUtilities.GetHierarchyProperty<string>(sharedHier, (uint)VSConstants.VSITEMID.Root,
                     (int)__VSHPROPID.VSHPROPID_Caption);
                output.OutputStringThreadSafe(string.Format("Shared project: {0}\n", sharedCaption));

                var activePlatformHier = this.GetActiveProjectContext(sharedHier);
                if (activePlatformHier != null)
                {
                    string activeCaption = HierarchyUtilities.GetHierarchyProperty<string>(activePlatformHier,
                         (uint)VSConstants.VSITEMID.Root, (int)__VSHPROPID.VSHPROPID_Caption);
                    output.OutputStringThreadSafe(string.Format("Active platform project: {0}\n", activeCaption));
                }
                else
                {
                    MessageBox.Show("Shared project has no active platform project");
                }
            }
            else
            {
                MessageBox.Show("Solution has no shared project");
            }
        }
        else
        {
            MessageBox.Show("No solution is open");
        }
    }
    ```

12. Itere pelos projetos da plataforma. O método a seguir obtém todos os projetos de importação (plataforma) do projeto compartilhado.

    ```csharp
    private IEnumerable<IVsHierarchy> EnumImportingProjects(IVsHierarchy hierarchy)
    {
        IVsSharedAssetsProject sharedAssetsProject;
        if (HierarchyUtilities.TryGetHierarchyProperty(hierarchy, (uint)VSConstants.VSITEMID.Root,
            (int)__VSHPROPID7.VSHPROPID_SharedAssetsProject, out sharedAssetsProject)
            && sharedAssetsProject != null)
        {
            foreach (IVsHierarchy importingProject in sharedAssetsProject.EnumImportingProjects())
            {
                yield return importingProject;
            }
        }
    }
    ```

    > [!IMPORTANT]
    > Se o usuário tiver aberto um projeto de aplicativo universal do Windows do C++ na instância experimental, o código acima lançará uma exceção. Este é um problema conhecido. Para evitar a exceção, substitua o `foreach` bloco acima pelo seguinte:

    ```csharp
    var importingProjects = sharedAssetsProject.EnumImportingProjects();
    for (int i = 0; i < importingProjects.Count; ++i)
    {
        yield return importingProjects[i];
    }
    ```

13. No `ShowMessageBox` método, gere a legenda de cada projeto de plataforma. Insira o código a seguir após a linha que gera a legenda do projeto da plataforma ativa. Somente os projetos da plataforma que são carregados aparecem nessa lista.

    ```csharp
    output.OutputStringThreadSafe("Platform projects:\n");

    IEnumerable<IVsHierarchy> projects = this.EnumImportingProjects(sharedHier);

    bool isActiveProjectSet = false;
    foreach (IVsHierarchy platformHier in projects)
    {
        string platformCaption = HierarchyUtilities.GetHierarchyProperty<string>(platformHier, (uint)VSConstants.VSITEMID.Root,
            (int)__VSHPROPID.VSHPROPID_Caption);
        output.OutputStringThreadSafe(string.Format(" * {0}\n", platformCaption));
    }
    ```

14. Altere o projeto da plataforma ativa. O método a seguir define o projeto ativo usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A> .

    ```csharp
    private int SetActiveProjectContext(IVsHierarchy hierarchy, IVsHierarchy activeProjectContext)
    {
        return hierarchy.SetProperty((uint)VSConstants.VSITEMID.Root, (int)__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy, activeProjectContext);
    }
    ```

15. No `ShowMessageBox` método, altere o projeto da plataforma ativa. Insira este código dentro do `foreach` bloco.

    ```csharp
    bool isActiveProjectSet = false;
    string platformCaption = null;
    foreach (IVsHierarchy platformHier in projects)
    {
        platformCaption = HierarchyUtilities.GetHierarchyProperty<string>(platformHier, (uint)VSConstants.VSITEMID.Root,
             (int)__VSHPROPID.VSHPROPID_Caption);
        output.OutputStringThreadSafe(string.Format(" * {0}\n", platformCaption));

        // if this project is neither the shared project nor the current active platform project,
        // set it to be the active project
        if (!isActiveProjectSet && platformHier != activePlatformHier)
        {
            this.SetActiveProjectContext(sharedHier, platformHier);
            activePlatformHier = platformHier;
            isActiveProjectSet = true;
        }
    }
    output.OutputStringThreadSafe("set active project: " + platformCaption +'\n');
    ```

16. Agora experimente. Pressione F5 para iniciar a instância experimental. Crie um projeto de aplicativo de Hub universal do C# na instância experimental (na caixa de diálogo **novo projeto** , aplicativo de   >  Hub universal do **Windows**  >  **Windows 8** do Visual C#  >    >  ). Depois que a solução for carregada, vá para o menu **ferramentas** e clique em **invocar TestUniversalProject** e, em seguida, verifique o texto no painel **saída** . Você verá algo semelhante ao que se segue:

    ```
    Found shared project: HubApp.Shared
    The active platform project: HubApp.Windows
    Platform projects:
     * HubApp.Windows
     * HubApp.WindowsPhone
    set active project: HubApp.WindowsPhone
    ```

### <a name="manage-the-shared-items-in-the-platform-project"></a>Gerenciar os itens compartilhados no projeto da plataforma

1. Localize os itens compartilhados no projeto plataforma. Os itens no projeto compartilhado aparecem no projeto da plataforma como itens compartilhados. Você não pode vê-los na **Gerenciador de soluções**, mas pode percorrer a hierarquia do projeto para encontrá-los. O método a seguir percorre a hierarquia e coleta todos os itens compartilhados. Ele, opcionalmente, produz a legenda de cada item,. Os itens compartilhados são identificados pela nova propriedade <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7.VSHPROPID_IsSharedItem> .

    ```csharp
    private void InspectHierarchyItems(IVsHierarchy hier, uint itemid, int level, List<uint> itemIds, bool getSharedItems, bool printItems)
    {
        string caption = HierarchyUtilities.GetHierarchyProperty<string>(hier, itemid, (int)__VSHPROPID.VSHPROPID_Caption);
        if (printItems)
            output.OutputStringThreadSafe(string.Format("{0}{1}\n", new string('\t', level), caption));

        // if getSharedItems is true, inspect only shared items; if it's false, inspect only unshared items
        bool isSharedItem;
        if (HierarchyUtilities.TryGetHierarchyProperty(hier, itemid, (int)__VSHPROPID7.VSHPROPID_IsSharedItem, out isSharedItem)
            && (isSharedItem == getSharedItems))
        {
            itemIds.Add(itemid);
        }

        uint child;
        if (HierarchyUtilities.TryGetHierarchyProperty(hier, itemid, (int)__VSHPROPID.VSHPROPID_FirstChild, Unbox.AsUInt32, out child)
            && child != (uint)VSConstants.VSITEMID.Nil)
        {
            this.InspectHierarchyItems(hier, child, level + 1, itemIds, isSharedItem, printItems);

            while (HierarchyUtilities.TryGetHierarchyProperty(hier, child, (int)__VSHPROPID.VSHPROPID_NextSibling, Unbox.AsUInt32, out child)
                && child != (uint)VSConstants.VSITEMID.Nil)
            {
                this.InspectHierarchyItems(hier, child, level + 1, itemIds, isSharedItem, printItems);
            }
        }
    }
    ```

2. No `ShowMessageBox` método, adicione o código a seguir para percorrer os itens de hierarquia do projeto de plataforma. Insira-o dentro do `foreach` bloco.

    ```csharp
    output.OutputStringThreadSafe("Walk the active platform project:\n");
    var sharedItemIds = new List<uint>();
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);
    ```

3. Ler os itens compartilhados. Os itens compartilhados aparecem no projeto da plataforma como arquivos vinculados ocultos e você pode ler todas as propriedades como arquivos vinculados comuns. O código a seguir lê o caminho completo do primeiro item compartilhado.

    ```csharp
    var sharedItemId = sharedItemIds[0];
    string fullPath;
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));
    output.OutputStringThreadSafe(string.Format("Shared item full path: {0}\n", fullPath));
    ```

4. Agora experimente. Pressione **F5** para iniciar a instância experimental. Crie um projeto de aplicativo de Hub universal do C# na instância experimental (na caixa de diálogo **novo projeto** , aplicativo de   >  Hub universal do **Windows**  >  **Windows 8** do Visual C#  >    >  ) vá para o menu **ferramentas** e clique em **invocar TestUniversalProject** e, em seguida, verifique o texto no painel de **saída** . Você verá algo semelhante ao que se segue:

    ```
    Found shared project: HubApp.Shared
    The active platform project: HubApp.Windows
    Platform projects:
     * HubApp.Windows
     * HubApp.WindowsPhone
    set active project: HubApp.WindowsPhone
    Walk the active platform project:
        HubApp.WindowsPhone
            <HubApp.Shared>
                App.xaml
                    App.xaml.cs
                Assets
                    DarkGray.png
                    LightGray.png
                    MediumGray.png
                Common
                    NavigationHelper.cs
                    ObservableDictionary.cs
                    RelayCommand.cs
                    SuspensionManager.cs
                DataModel
                    SampleData.json
                    SampleDataSource.cs
                HubApp.Shared.projitems
                Strings
                    en-US
                        Resources.resw
            Assets
                HubBackground.theme-dark.png
                HubBackground.theme-light.png
                Logo.scale-240.png
                SmallLogo.scale-240.png
                SplashScreen.scale-240.png
                Square71x71Logo.scale-240.png
                StoreLogo.scale-240.png
                WideLogo.scale-240.png
            HubPage.xaml
                HubPage.xaml.cs
            ItemPage.xaml
                ItemPage.xaml.cs
            Package.appxmanifest
            Properties
                AssemblyInfo.cs
            References
                .NET for Windows Store apps
                HubApp.Shared
                Windows Phone 8.1
            SectionPage.xaml
                SectionPage.xaml.cs
    ```

### <a name="detect-changes-in-platform-projects-and-shared-projects"></a>Detectar alterações em projetos de plataforma e projetos compartilhados

1. Você pode usar eventos de hierarquia e de projeto para detectar alterações em projetos compartilhados, assim como você pode para projetos de plataforma. No entanto, os itens de projeto no projeto compartilhado não são visíveis, o que significa que determinados eventos não são acionados quando itens de projeto compartilhados são alterados.

    Considere a sequência de eventos quando um arquivo em um projeto for renomeado:

   1. O nome do arquivo é alterado em disco.

   2. O arquivo de projeto é atualizado para incluir o novo nome do arquivo.

      Eventos de hierarquia (por exemplo, <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> ) geralmente controlam as alterações exibidas na interface do usuário, como no **Gerenciador de soluções**. Eventos de hierarquia consideram uma operação de renomeação de arquivo para consistir em uma exclusão de arquivo e, em seguida, uma adição de arquivo. No entanto, quando itens invisíveis são alterados, o sistema de eventos de hierarquia dispara um <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> evento, mas não um <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> evento. Portanto, se você renomear um arquivo em um projeto de plataforma, obterá <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> , mas se renomear um arquivo em um projeto compartilhado, você só obterá <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> .

      Para controlar as alterações em itens de projeto, você pode manipular eventos de item de projeto DTE (aqueles encontrados em <xref:EnvDTE.ProjectItemsEventsClass> ). No entanto, se você estiver lidando com um grande número de eventos, poderá obter melhor desempenho manipulando os eventos no <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> . Neste tutorial, mostramos apenas os eventos de hierarquia e os eventos de DTE. Neste procedimento, você adiciona um ouvinte de eventos a um projeto compartilhado e a um projeto de plataforma. Em seguida, ao renomear um arquivo em um projeto compartilhado e outro arquivo em um projeto de plataforma, você poderá ver os eventos que são acionados para cada operação de renomeação.

      Neste procedimento, você adiciona um ouvinte de eventos a um projeto compartilhado e a um projeto de plataforma. Em seguida, ao renomear um arquivo em um projeto compartilhado e outro arquivo em um projeto de plataforma, você poderá ver os eventos que são acionados para cada operação de renomeação.

2. Adicione um ouvinte de eventos. Adicione um novo arquivo de classe ao projeto e chame-o de *HierarchyEventListener. cs*.

3. Abra o arquivo *HierarchyEventListener. cs* e adicione as seguintes diretivas using:

   ```csharp
   using Microsoft.VisualStudio.Shell.Interop;
   using Microsoft.VisualStudio;
   using System.IO;
   ```

4. Ter a `HierarchyEventListener` classe implementada <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> :

   ```csharp
   class HierarchyEventListener : IVsHierarchyEvents
   { }
   ```

5. Implemente os membros de <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> , como no código abaixo.

   ```csharp
   class HierarchyEventListener : IVsHierarchyEvents
   {
       private IVsHierarchy hierarchy;
       IVsOutputWindowPane output;

       internal HierarchyEventListener(IVsHierarchy hierarchy, IVsOutputWindowPane outputWindow) {
            this.hierarchy = hierarchy;
            this.output = outputWindow;
       }

       int IVsHierarchyEvents.OnInvalidateIcon(IntPtr hIcon) {
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnInvalidateItems(uint itemIDParent) {
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnItemAdded(uint itemIDParent, uint itemIDSiblingPrev, uint itemIDAdded) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemAdded: " + itemIDAdded + "\n");
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnItemDeleted(uint itemID) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemDeleted: " + itemID + "\n");
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnItemsAppended(uint itemIDParent) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemsAppended\n");
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnPropertyChanged(uint itemID, int propID, uint flags) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnPropertyChanged: item ID " + itemID + "\n");
           return VSConstants.S_OK;
       }
   }
   ```

6. Na mesma classe, adicione outro manipulador de eventos para o evento DTE <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> , que ocorre sempre que um item de projeto é renomeado.

   ```csharp
   public void OnItemRenamed(EnvDTE.ProjectItem projItem, string oldName)
   {
       output.OutputStringThreadSafe(string.Format("[Event] Renamed {0} to {1} in project {2}\n",
            oldName, Path.GetFileName(projItem.get_FileNames(1)), projItem.ContainingProject.Name));
   }
   ```

7. Inscreva-se para os eventos de hierarquia. Você precisa se inscrever separadamente para cada projeto que estiver acompanhando. Adicione o seguinte código no `ShowMessageBox` , um para o projeto compartilhado e o outro para um dos projetos da plataforma.

   ```csharp
   // hook up the event listener for hierarchy events on the shared project
   HierarchyEventListener listener1 = new HierarchyEventListener(sharedHier, output);
   uint cookie1;
   sharedHier.AdviseHierarchyEvents(listener1, out cookie1);

   // hook up the event listener for hierarchy events on the
   active project
   HierarchyEventListener listener2 = new HierarchyEventListener(activePlatformHier, output);
   uint cookie2;
   activePlatformHier.AdviseHierarchyEvents(listener2, out cookie2);
   ```

8. Inscreva-se para o evento de item de projeto DTE <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> . Adicione o código a seguir depois de conectar o segundo ouvinte.

   ```csharp
   // hook up DTE events for project items
   Events2 dteEvents = (Events2)dte.Events;
   dteEvents.ProjectItemsEvents.ItemRenamed += listener1.OnItemRenamed;
   ```

9. Modifique o item compartilhado. Não é possível modificar itens compartilhados em um projeto de plataforma; em vez disso, você deve modificá-los no projeto compartilhado que é o proprietário real desses itens. Você pode obter a ID do item correspondente no projeto compartilhado com <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A> , dando a ele o caminho completo do item compartilhado. Em seguida, você pode modificar o item compartilhado. A alteração é propagada para os projetos da plataforma.

    > [!IMPORTANT]
    > Você deve descobrir se um item de projeto é um item compartilhado antes de modificá-lo.

     O método a seguir modifica o nome de um arquivo de item de projeto.

    ```csharp
    private void ModifyFileNameInProject(IVsHierarchy project, string path)
    {
        int found;
        uint projectItemID;
        VSDOCUMENTPRIORITY[] priority = new VSDOCUMENTPRIORITY[1];
        if (ErrorHandler.Succeeded(((IVsProject)project).IsDocumentInProject(path, out found, priority, out projectItemID))
            && found != 0)
        {
            var name = DateTime.Now.Ticks.ToString() + Path.GetExtension(path);
            project.SetProperty(projectItemID, (int)__VSHPROPID.VSHPROPID_EditLabel, name);
            output.OutputStringThreadSafe(string.Format("Renamed {0} to {1}\n", path,name));
        }
    }
    ```

10. Chame esse método depois de todos os outros códigos `ShowMessageBox` para modificar o nome do arquivo no projeto compartilhado. Insira-o após o código que obtém o caminho completo do item no projeto compartilhado.

    ```csharp
    // change the file name of an item in a shared project
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));
    output.OutputStringThreadSafe(string.Format("Shared project item ID = {0}, full path = {1}\n", sharedItemId, fullPath));
    this.ModifyFileNameInProject(sharedHier, fullPath);
    ```

11. Compile e execute o projeto. Crie um aplicativo de Hub universal do C# na instância experimental, vá para o menu **ferramentas** e clique em **invocar TestUniversalProject** e verifique o texto no painel saída geral. O nome do primeiro item no projeto compartilhado (esperamos que seja o arquivo *app. XAML* ) deve ser alterado e você verá que o <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> evento foi acionado. Nesse caso, como renomear o *app. XAML* faz com que o *app. XAML. cs* seja renomeado também, você verá quatro eventos (dois para cada projeto de plataforma). (Os eventos do DTE não rastreiam os itens no projeto compartilhado.) Você deve ver dois <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> eventos (um para cada um dos projetos de plataforma), mas nenhum <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> evento.

12. Agora, tente renomear um arquivo em um projeto de plataforma e você pode ver a diferença nos eventos que são acionados. Adicione o seguinte código `ShowMessageBox` ao após a chamada para `ModifyFileName` .

    ```csharp
    // change the file name of an item in a platform project
    var unsharedItemIds = new List<uint>();
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, unsharedItemIds, false, false);

    var unsharedItemId = unsharedItemIds[0];
    string unsharedPath;
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(unsharedItemId, out unsharedPath));
    output.OutputStringThreadSafe(string.Format("Platform project item ID = {0}, full path = {1}\n", unsharedItemId, unsharedPath));

    this.ModifyFileNameInProject(activePlatformHier, unsharedPath);
    ```

13. Compile e execute o projeto. Crie um projeto universal do C# na instância experimental, vá para o menu **ferramentas** e clique em **invocar TestUniversalProject** e verifique o texto no painel saída geral. Depois que o arquivo no projeto de plataforma for renomeado, você deverá ver um <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> evento e um <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> evento. Uma vez que a alteração do arquivo não fez com que outros arquivos sejam alterados, e como as alterações em itens em um projeto de plataforma não são propagadas em qualquer lugar, há apenas um desses eventos.