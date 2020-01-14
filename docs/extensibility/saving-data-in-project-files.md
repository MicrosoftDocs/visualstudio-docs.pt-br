---
title: Salvando dados em arquivos de projeto | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- data [Visual Studio], saving in project files
- project files
- project files, saving data
ms.assetid: a3d4b15b-a91e-41ba-b235-e62632d11bc5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 30d6652480318898e1528a6f2bb61b84621636d6
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2020
ms.locfileid: "75848749"
---
# <a name="save-data-in-project-files"></a>Salvar dados em arquivos de projeto
Um subtipo de projeto pode salvar e recuperar dados específicos de subtipo no arquivo de projeto. A MPF (estrutura de pacote gerenciada) fornece duas interfaces para realizar essa tarefa:

- A interface <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> permite acessar valores de propriedade da seção **MSBuild** do arquivo de projeto. Os métodos fornecidos pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> podem ser chamados por qualquer usuário sempre que o usuário precisar carregar ou salvar dados relacionados à compilação.

- O <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> é usado para persistir dados relacionados não compilados em XML de forma livre. Os métodos fornecidos por <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> são chamados por [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] sempre que [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] precisa persistir dados relacionados não compilados no arquivo de projeto.

  Para obter mais informações sobre como persistir dados relacionados à compilação e não à compilação, consulte [persistir dados no arquivo de projeto do MSBuild](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md).

## <a name="save-and-retrieve-build-related-data"></a>Salvar e recuperar dados relacionados à compilação

### <a name="to-save-a-build-related-data-in-the-project-file"></a>Para salvar uma compilação de dados relacionados no arquivo de projeto

- Chame o método <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> para salvar um caminho completo do arquivo de projeto.

    ```
    private SpecializedProject project;
    IVsBuildPropertyStorage projectStorage = (IVsBuildPropertyStorage)project;
    string newFullPath = GetNewFullPath();
    // Set a full path of the project file.
    ErrorHandler.ThrowOnFailure(projectStorage.SetPropertyValue(
        "MSBuildProjectDirectory",
        String.Empty,
        (uint)_PersistStorageType.PST_PROJECT_FILE, newFullPath));
    ```

### <a name="to-retrieve-build-related-data-from-the-project-file"></a>Para recuperar dados relacionados à compilação do arquivo de projeto

- Chame o método <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.GetPropertyValue%2A> para recuperar um caminho completo do arquivo de projeto.

    ```
    private SpecializedProject project;
    IVsBuildPropertyStorage projectStorage = (IVsBuildPropertyStorage)project;
    string fullPath;
    // Get a full path of the project file.
    ErrorHandler.ThrowOnFailure(projectStorage.GetPropertyValue(
        "MSBuildProjectDirectory",
        String.Empty,
        (uint)_PersistStorageType.PST_PROJECT_FILE, out fullPath));
    ```

## <a name="save-and-retrieve-non-build-related-data"></a>Salvar e recuperar dados não relacionados à compilação

### <a name="to-save-non-build-related-data-in-the-project-file"></a>Para salvar dados não relacionados à compilação no arquivo de projeto

1. Implemente o método <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.IsFragmentDirty%2A> para determinar se um fragmento XML foi alterado desde que foi salvo pela última vez em seu arquivo atual.

    ```
    public int IsFragmentDirty(uint storage, out int pfDirty)
    {
        pfDirty = 0;
        switch (storage)
        {
            case (uint)_PersistStorageType.PST_PROJECT_FILE:
            {
                if (isDirty)
                    pfDirty |= 1;
                break;
            }
            case (uint)_PersistStorageType.PST_USER_FILE:
            {
                // We do not store anything in the user file.
                break;
            }
        }

        // Forward the call to inner flavor(s)
        if (pfDirty == 0 && innerCfg != null && this.innerCfg is IPersistXMLFragment)
            return ((IPersistXMLFragment)this.innerCfg).IsFragmentDirty(storage, out pfDirty);

        return VSConstants.S_OK;

    }
    ```

2. Implemente o método <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A> para salvar os dados XML no arquivo de projeto.

    ```
    public int Save(ref Guid guidFlavor, uint storage, out string pbstrXMLFragment, int fClearDirty)
    {
        pbstrXMLFragment = null;

        if (IsMyFlavorGuid(ref guidFlavor))
        {
            switch (storage)
            {
                case (uint)_PersistStorageType.PST_PROJECT_FILE:
                {
                    // Create XML for our data.
                    XmlDocument doc = new XmlDocument();
                    XmlNode root = doc.CreateElement(this.GetType().Name);

                    XmlNode node = doc.CreateElement(targetsTag);
                    node.AppendChild(doc.CreateTextNode(this.TargetsToExecute));
                    root.AppendChild(node);

                    node = doc.CreateElement(updateTargetsTag);
                    node.AppendChild(doc.CreateTextNode(this.UpdateTargetList.ToString()));
                    root.AppendChild(node);

                    doc.AppendChild(root);
                    // Get XML fragment representing our data
                    pbstrXMLFragment = doc.InnerXml;

                    if (fClearDirty != 0)
                        isDirty = false;
                    break;
                }
                case (uint)_PersistStorageType.PST_USER_FILE:
                {
                    // We do not store anything in the user file.
                    break;
                }
            }
        }

        // Forward the call to inner flavor(s)
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)
            return ((IPersistXMLFragment)this.innerCfg).Save(ref guidFlavor, storage, out pbstrXMLFragment, fClearDirty);

        return VSConstants.S_OK;
    }
    ```

### <a name="to-retrieve-non-build-related-data-in-the-project-file"></a>Para recuperar dados não relacionados à compilação no arquivo de projeto

1. Implemente o método <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.InitNew%2A> para inicializar as propriedades de extensão do projeto e outros dados independentes de compilação. Esse método será chamado se não houver nenhum dado de configuração XML presente no arquivo de projeto.

    ```
    public int InitNew(ref Guid guidFlavor, uint storage)
    {
        //Return,if it is our guid.
        if (IsMyFlavorGuid(ref guidFlavor))
            return VSConstants.S_OK;

        //Forward the call to inner flavor(s).
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)
            return ((IPersistXMLFragment)this.innerCfg).InitNew(ref guidFlavor, storage);

        return VSConstants.S_OK;
    ```

2. Implemente o método <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A> para carregar os dados XML do arquivo de projeto.

    ```
    public int Load(ref Guid guidFlavor, uint storage, string pszXMLFragment)
    {
        if (IsMyFlavorGuid(ref guidFlavor))
        {
            switch (storage)
            {
                case (uint)_PersistStorageType.PST_PROJECT_FILE:
                {
                    // Load our data from the XML fragment.
                    XmlDocument doc = new XmlDocument();
                    XmlNode node = doc.CreateElement(this.GetType().Name);
                    node.InnerXml = pszXMLFragment;
                    if (node == null
                        || node.FirstChild == null
                        || node.FirstChild.ChildNodes.Count == 0
                        || node.FirstChild.ChildNodes[0].Name != targetsTag)
                        break;
                    this.TargetsToExecute = node.FirstChild.ChildNodes[0].InnerText;

                    if (node.FirstChild.ChildNodes.Count <= 1
                        || node.FirstChild.ChildNodes[1].Name != updateTargetsTag)
                        break;
                    this.UpdateTargetList = bool.Parse(node.FirstChild.ChildNodes[1].InnerText);
                    break;
                }
                case (uint)_PersistStorageType.PST_USER_FILE:
                {
                    // We do not store anything in the user file.
                    break;
                }
            }
        }

        // Forward the call to inner flavor(s)
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)
            return ((IPersistXMLFragment)this.innerCfg).Load(ref guidFlavor, storage, pszXMLFragment);

        return VSConstants.S_OK;
    }
    ```

> [!NOTE]
> Todos os exemplos de código fornecidos neste tópico são partes de um exemplo maior em [exemplos de VSSDK](https://github.com/Microsoft/VSSDK-Extensibility-Samples).

## <a name="see-also"></a>Veja também
- [Manter dados no arquivo de projeto do MSBuild](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)
