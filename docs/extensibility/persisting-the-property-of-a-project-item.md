---
title: Manter a propriedade de um Item de projeto | Microsoft Docs
ms.date: 03/22/2018
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- properties, adding to a project item
- project items, adding properties
ms.assetid: d7a0f2b0-d427-4d49-9536-54edfb37c0f3
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: da231c924e3167a50c885cf18ef878a02b28b166
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49915575"
---
# <a name="persist-the-property-of-a-project-item"></a>Manter a propriedade de um item de projeto
Você talvez queira manter uma propriedade que você adicionar a um item de projeto, como o autor de um arquivo de origem. Você pode fazer isso, armazenando a propriedade no arquivo de projeto.

 A primeira etapa para manter uma propriedade em um arquivo de projeto é obter a hierarquia do projeto como um <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> interface. Você pode obter essa interface usando a automação ou usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>. Depois de obter a interface, você pode usá-lo para determinar qual item de projeto está selecionado no momento. Depois que a ID do item de projeto, você pode usar <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A> para adicionar a propriedade.

 Nos procedimentos a seguir, você mantém o *VsPkg.cs* propriedade `Author` com o valor `Tom` no arquivo de projeto.

## <a name="to-obtain-the-project-hierarchy-with-the-dte-object"></a>Para obter a hierarquia de projeto com o objeto DTE

1.  Adicione o seguinte código para o VSPackage:

    ```csharp
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));
    EnvDTE.Project project = dte.Solution.Projects.Item(1);

    string uniqueName = project.UniqueName;
    IVsSolution solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));
    IVsHierarchy hierarchy;
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);
    ```

## <a name="to-persist-the-project-item-property-with-the-dte-object"></a>Para manter a propriedade de item de projeto com o objeto DTE

1.  Adicione o seguinte código para o código fornecido no método no procedimento anterior:

    ```csharp
    IVsBuildPropertyStorage buildPropertyStorage =
        hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        uint itemId;
        string fullPath = (string)project.ProjectItems.Item(
            "VsPkg.cs").Properties.Item("FullPath").Value;
        hierarchy.ParseCanonicalName(fullPath, out itemId);
        buildPropertyStorage.SetItemAttribute(itemId, "Author", "Tom");
    }
    ```

## <a name="to-obtain-the-project-hierarchy-using-ivsmonitorselection"></a>Para obter a hierarquia de projeto usando IVsMonitorSelection

1.  Adicione o seguinte código para o VSPackage:

    ```csharp
    IVsHierarchy hierarchy = null;
    IntPtr hierarchyPtr = IntPtr.Zero;
    IntPtr selectionContainer = IntPtr.Zero;
    uint itemid;

    // Retrieve shell interface in order to get current selection
    IVsMonitorSelection monitorSelection =     Package.GetGlobalService(typeof(SVsShellMonitorSelection)) as     IVsMonitorSelection;
    if (monitorSelection == null)
        throw new InvalidOperationException();

    try
    {
        // Get the current project hierarchy, project item, and selection container for the current selection
        // If the selection spans multiple hierachies, hierarchyPtr is Zero
        IVsMultiItemSelect multiItemSelect = null;
        ErrorHandler.ThrowOnFailure(
            monitorSelection.GetCurrentSelection(
                out hierarchyPtr, out itemid,
                out multiItemSelect, out selectionContainer));

        // We only care if there is only one node selected in the tree
        if (!(itemid == VSConstants.VSITEMID_NIL ||
            hierarchyPtr == IntPtr.Zero ||
            multiItemSelect != null ||
            itemid == VSConstants.VSITEMID_SELECTION))
        {
            hierarchy = Marshal.GetObjectForIUnknown(hierarchyPtr)
                as IVsHierarchy;
        }
    }
    finally
    {
        if (hierarchyPtr != IntPtr.Zero)
            Marshal.Release(hierarchyPtr);
        if (selectionContainer != IntPtr.Zero)
            Marshal.Release(selectionContainer);
    }
    ```

## <a name="to-persist-the-selected-project-item-property-given-the-project-hierarchy"></a>Para manter a propriedade de item de projeto selecionado, dada a hierarquia do projeto

1.  Adicione o seguinte código para o código fornecido no método no procedimento anterior:

    ```csharp
    IVsBuildPropertyStorage buildPropertyStorage =
        hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        buildPropertyStorage.SetItemAttribute(itemId, "Author", "Tom");
    }
    ```

## <a name="to-verify-that-the-property-is-persisted"></a>Para verificar que a propriedade é persistida

1. Iniciar [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e, em seguida, abrir ou criar uma solução.

2. Selecione o projeto item VsPkg.cs na **Gerenciador de soluções**.

3. Use um ponto de interrupção ou caso contrário, determinar que o VSPackage é carregado e SetItemAttribute é executado.

   > [!NOTE]
   > Você pode carregar um VSPackage no contexto da interface do usuário automaticamente <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid>. Para obter mais informações, consulte [carregar VSPackages](../extensibility/loading-vspackages.md).

4. Fechar [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e, em seguida, abra o arquivo de projeto no bloco de notas. Você deve ver o \<Autor > marca com o valor de Tom, da seguinte maneira:

   ```xml
   <Compile Include="VsPkg.cs">
       <Author>Tom</Author>
   </Compile>
   ```

## <a name="see-also"></a>Consulte também

- [Ferramentas personalizadas](../extensibility/internals/custom-tools.md)