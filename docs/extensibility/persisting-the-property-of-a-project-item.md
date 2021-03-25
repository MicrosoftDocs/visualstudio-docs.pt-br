---
title: Persistindo a propriedade de um item de projeto | Microsoft Docs
description: Saiba como manter uma propriedade que você adiciona a um item de projeto armazenando a propriedade no arquivo de projeto em seu tipo de projeto estendido.
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: how-to
helpviewer_keywords:
- properties, adding to a project item
- project items, adding properties
ms.assetid: d7a0f2b0-d427-4d49-9536-54edfb37c0f3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 58c46da9023cc64246f1ea9ee4bde1ec866c545d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090350"
---
# <a name="persist-the-property-of-a-project-item"></a>Persistir a propriedade de um item de projeto
Talvez você queira manter uma propriedade adicionada a um item de projeto, como o autor de um arquivo de origem. Você pode fazer isso armazenando a propriedade no arquivo de projeto.

 A primeira etapa para manter uma propriedade em um arquivo de projeto é obter a hierarquia do projeto como uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> interface. Você pode obter essa interface usando a automação ou usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> . Depois de obter a interface, você pode usá-la para determinar qual item de projeto está selecionado no momento. Quando tiver a ID de item do projeto, você poderá usar <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A> para adicionar a propriedade.

 Nos procedimentos a seguir, você mantém a propriedade *VsPkg. cs* `Author` com o valor `Tom` no arquivo de projeto.

## <a name="to-obtain-the-project-hierarchy-with-the-dte-object"></a>Para obter a hierarquia do projeto com o objeto DTE

1. Adicione o seguinte código ao seu VSPackage:

    ```csharp
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));
    EnvDTE.Project project = dte.Solution.Projects.Item(1);

    string uniqueName = project.UniqueName;
    IVsSolution solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));
    IVsHierarchy hierarchy;
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);
    ```

## <a name="to-persist-the-project-item-property-with-the-dte-object"></a>Para manter a propriedade item do projeto com o objeto DTE

1. Adicione o código a seguir ao código fornecido no método no procedimento anterior:

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

## <a name="to-obtain-the-project-hierarchy-using-ivsmonitorselection"></a>Para obter a hierarquia do projeto usando IVsMonitorSelection

1. Adicione o seguinte código ao seu VSPackage:

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

## <a name="to-persist-the-selected-project-item-property-given-the-project-hierarchy"></a>Para persistir a propriedade de item de projeto selecionada, dada a hierarquia do projeto

1. Adicione o código a seguir ao código fornecido no método no procedimento anterior:

    ```csharp
    IVsBuildPropertyStorage buildPropertyStorage =
        hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        buildPropertyStorage.SetItemAttribute(itemId, "Author", "Tom");
    }
    ```

## <a name="to-verify-that-the-property-is-persisted"></a>Para verificar se a propriedade é persistente

1. Inicie [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] o e, em seguida, abra ou crie uma solução.

2. Selecione o item de projeto VsPkg. cs em **Gerenciador de soluções**.

3. Use um ponto de interrupção ou determine se o VSPackage está carregado e se SetItemAttribute é executado.

   > [!NOTE]
   > Você pode Autocarregar um VSPackage no contexto da interface do usuário <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid> . Para obter mais informações, consulte [Load VSPackages](../extensibility/loading-vspackages.md).

4. Feche [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e abra o arquivo de projeto no bloco de notas. Você deve ver a \<Author> marca com o valor Tom, da seguinte maneira:

   ```xml
   <Compile Include="VsPkg.cs">
       <Author>Tom</Author>
   </Compile>
   ```

## <a name="see-also"></a>Confira também

- [Ferramentas personalizadas](../extensibility/internals/custom-tools.md)
