---
title: Salvando dados em arquivos de projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data [Visual Studio], saving in project files
- project files
- project files, saving data
ms.assetid: a3d4b15b-a91e-41ba-b235-e62632d11bc5
caps.latest.revision: 29
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 87d858d675fb1b2fb60280321a319b24684d9d83
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51755828"
---
# <a name="saving-data-in-project-files"></a>Salvando dados em arquivos de projeto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um subtipo de projeto pode salvar e recuperar dados específicos subtipo-no arquivo de projeto. Estrutura de pacote gerenciado (MPF) oferece duas interfaces para realizar essa tarefa:  
  
- O <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> interface permite que os valores de propriedade de acesso da **MSBuild** seção do arquivo de projeto. Os métodos fornecidos pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> pode ser chamado por qualquer usuário sempre que o usuário precisará carregar ou salvar dados relacionados de compilar.  
  
- O <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> é usada para persistir dados relacionados de não compilação no XML de forma livre. Os métodos fornecidos pelo <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> são chamados pelo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] sempre que [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] precisa para persistir dados relacionados de não compilação no arquivo de projeto.  
  
  Para obter mais informações sobre como manter o build e os dados relacionados de não-compilação, consulte [persistência de dados no arquivo de projeto MSBuild](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md).  
  
## <a name="saving-and-retrieving-build-related-data"></a>Salvando e recuperando build relacionados a dados  
  
#### <a name="to-save-a-build-related-data-in-the-project-file"></a>Para salvar um build relacionados a dados no arquivo de projeto  
  
-   Chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> método para salvar um caminho completo do arquivo de projeto.  
  
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
  
#### <a name="to-retrieve-build-related-data-from-the-project-file"></a>Para recuperar a compilação dados relacionados do arquivo de projeto  
  
-   Chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.GetPropertyValue%2A> método para recuperar um caminho completo do arquivo de projeto.  
  
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
  
## <a name="saving-and-retrieving-non-build-related-data"></a>Salvando e recuperando não-compilação dados relacionados  
  
#### <a name="to-save-non-build-related-data-in-the-project-file"></a>Para salvar não-build relacionados a dados no arquivo de projeto  
  
1.  Implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.IsFragmentDirty%2A> método para determinar se um fragmento XML foi alterado desde a última é salvo no arquivo atual.  
  
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
  
2.  Implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A> método para salvar os dados XML no arquivo de projeto.  
  
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
  
#### <a name="to-retrieve-non-build-related-data-in-the-project-file"></a>Para recuperar dados relacionados de não compilação no arquivo de projeto  
  
1.  Implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.InitNew%2A> método para inicializar as propriedades de extensão de projeto e outros dados de compilação independente. Este método é chamado se não houver nenhum dado de configuração XML presente no arquivo de projeto.  
  
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
  
2.  Implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A> método para carregar os dados XML do arquivo de projeto.  
  
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
>  Todos os exemplos de código fornecidos neste tópico são partes de um exemplo maior, [exemplos de VSSDK](../misc/vssdk-samples.md).  
  
## <a name="see-also"></a>Consulte também  
 [Persistir os dados no arquivo de projeto do MSBuild](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)

