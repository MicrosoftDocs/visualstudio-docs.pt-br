---
title: Estender o filtro do Gerenciador de soluções | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Solution Explorer, extending
- extensibility [Visual Studio], projects and solutions
ms.assetid: df976c76-27ec-4f00-ab6d-a26a745dc6c7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: bf43243abc361df6c5b32b0e71e966c61a501b52
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39498782"
---
# <a name="extend-the-solution-explorer-filter"></a>Estender o filtro do Gerenciador de soluções
Você pode estender **Gerenciador de soluções** filtrar funcionalidade para mostrar ou ocultar arquivos diferentes. Por exemplo, você pode criar um filtro que mostra apenas classe factory arquivos c# na **Gerenciador de soluções**, como demonstra este passo a passo.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
### <a name="create-a-visual-studio-package-project"></a>Criar um projeto de pacote do Visual Studio  
  
1.  Crie um projeto do VSIX chamado `FileFilter`. Adicionar um modelo de item de comando personalizado chamado **FileFilter**. Para obter mais informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
2.  Adicione uma referência ao `System.ComponentModel.Composition` e `Microsoft.VisualStudio.Utilities`.  
  
3.  Fazer com que o comando de menu apareça na **Gerenciador de soluções** barra de ferramentas. Abra o *FileFilterPackage.vsct* arquivo.  
  
4.  Alterar o `<Button>` bloco para o seguinte:  
  
    ```xml  
    <Button guid="guidFileFilterPackageCmdSet" id="FileFilterId" priority="0x0400" type="Button">  
        <Parent guid="guidSHLMainMenu" id="IDG_VS_TOOLBAR_PROJWIN_FILTERS" />  
        <Icon guid="guidImages" id="bmpPic1" />  
        <Strings>  
            <ButtonText>FileNameFilter</ButtonText>  
        </Strings>  
    </Button>  
    ```  
  
### <a name="update-the-manifest-file"></a>Atualizar o arquivo de manifesto  
  
1.  No *vsixmanifest* de arquivo, adicione um ativo que é um componente MEF.  
  
2.  Sobre o **ativos** guia, escolha o **New** botão.  
  
3.  No **tipo** campo, escolha **mefcomponent**.  
  
4.  No **fonte** campo, escolha **um projeto na solução atual**.  
  
5.  No **Project** campo, escolha **FileFilter**e, em seguida, escolha o **Okey** botão.  
  
### <a name="add-the-filter-code"></a>Adicione o código de filtro  
  
1.  Adicione alguns GUIDs para o *FileFilterPackageGuids.cs* arquivo:  
  
    ```csharp  
    public const string guidFileFilterPackageCmdSetString = "00000000-0000-0000-0000-00000000"; // get your GUID from the .vsct file  
    public const int FileFilterId = 0x100;  
    ```  
  
2.  Adicionar um arquivo de classe ao projeto FileFilter nomeado *FileNameFilter.cs*.  
  
3.  Substitua o namespace vazio e a classe vazia com o código a seguir.  
  
     O `Task<IReadOnlyObservableSet> GetIncludedItemsAsync(IEnumerable<IVsHierarchyItem rootItems)` método usa a coleção que contém a raiz da solução (`rootItems`) e retorna a coleção de itens a serem incluídos no filtro.  
  
     O `ShouldIncludeInFilter` método filtra os itens na **Gerenciador de soluções** hierarquia com base na condição se você especificar.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.ComponentModel.Composition;  
    using System.Text.RegularExpressions;  
    using System.Threading.Tasks;  
    using Microsoft.Internal.VisualStudio.PlatformUI;  
    using Microsoft.VisualStudio.Shell;  
  
    namespace FileFilter  
    {  
        // Implements ISolutionTreeFilterProvider. The SolutionTreeFilterProvider attribute declares it as a MEF component  
        [SolutionTreeFilterProvider(FileFilterPackageGuids.guidFileFilterPackageCmdSetString, (uint)(FileFilterPackageGuids.FileFilterId))]  
        public sealed class FileNameFilterProvider : HierarchyTreeFilterProvider  
        {  
            SVsServiceProvider svcProvider;  
            IVsHierarchyItemCollectionProvider hierarchyCollectionProvider;  
  
            // Constructor required for MEF composition  
            [ImportingConstructor]  
            public FileNameFilterProvider(SVsServiceProvider serviceProvider, IVsHierarchyItemCollectionProvider hierarchyCollectionProvider)  
            {  
                this.svcProvider = serviceProvider;  
                this.hierarchyCollectionProvider = hierarchyCollectionProvider;  
            }  
  
            // Returns an instance of Create filter class.  
            protected override HierarchyTreeFilter CreateFilter()  
            {  
                return new FileNameFilter(this.svcProvider, this.hierarchyCollectionProvider, FileNamePattern);  
            }  
  
            // Regex pattern for CSharp factory classes  
            private const string FileNamePattern = @"\w*factory\w*(.cs$)";  
  
            // Implementation of file filtering  
            private sealed class FileNameFilter : HierarchyTreeFilter  
            {  
                private readonly Regex regexp;  
                private readonly IServiceProvider svcProvider;  
                private readonly IVsHierarchyItemCollectionProvider hierarchyCollectionProvider;  
  
                public FileNameFilter(  
                    IServiceProvider serviceProvider,  
                    IVsHierarchyItemCollectionProvider hierarchyCollectionProvider,  
                    string fileNamePattern)  
                {  
                    this.svcProvider = serviceProvider;  
                    this.hierarchyCollectionProvider = hierarchyCollectionProvider;  
                    this.regexp = new Regex(fileNamePattern, RegexOptions.IgnoreCase);  
                }  
  
                // Gets the items to be included from this filter provider.   
                // rootItems is a collection that contains the root of your solution  
                // Returns a collection of items to be included as part of the filter  
                protected override async Task<IReadOnlyObservableSet> GetIncludedItemsAsync(IEnumerable<IVsHierarchyItem> rootItems)  
                {  
                    IVsHierarchyItem root = HierarchyUtilities.FindCommonAncestor(rootItems);  
                    IReadOnlyObservableSet<IVsHierarchyItem> sourceItems;  
                    sourceItems = await hierarchyCollectionProvider.GetDescendantsAsync(  
                                        root.HierarchyIdentity.NestedHierarchy,  
                                        CancellationToken);  
  
                    IFilteredHierarchyItemSet includedItems = await hierarchyCollectionProvider.GetFilteredHierarchyItemsAsync(  
                        sourceItems,  
                        ShouldIncludeInFilter,  
                        CancellationToken);  
                    return includedItems;  
                }  
  
                // Returns true if filters hierarchy item name for given filter; otherwise, false</returns>  
                private bool ShouldIncludeInFilter(IVsHierarchyItem hierarchyItem)  
                {  
                    if (hierarchyItem == null)  
                    {  
                        return false;  
                    }  
                    return this.regexp.IsMatch(hierarchyItem.Text);  
                }  
            }  
        }  
    }  
  
    ```  
  
4.  Na *FileFilter.cs*, remova o posicionamento de comando e código do construtor FileFilter de manipulação. O resultado deve ter esta aparência:  
  
    ```csharp  
    private FileFilter(Package package)  
    {  
        if (package == null)  
        {  
            throw new ArgumentNullException("package");  
        }  
  
        this.package = package;  
    }  
    ```  
  
     Remover o `ShowMessageBox()` método também.  
  
5.  Na *FileFilterPackage.cs*, substitua o código no `Initialize()` método com o seguinte:  
  
    ```csharp  
    protected override void Initialize()  
    {  
        Debug.WriteLine (string.Format(CultureInfo.CurrentCulture, "Entering Initialize() of: {0}", this.ToString()));  
        base.Initialize();  
    }  
    ```  
  
### <a name="test-your-code"></a>Testar seu código  
  
1.  Compile e execute o projeto. Uma segunda instância do Visual Studio é exibida. Isso é chamado na instância experimental.  
  
2.  Na instância experimental do Visual Studio, abra um projeto c#.  
  
3.  Procure pelo botão, você adicionou na **Gerenciador de soluções** barra de ferramentas. Ele deve ser o quarto botão da esquerda.  
  
4.  Quando você clicar no botão, todos os arquivos devem ser filtrados e você deverá ver **todos os itens foram filtrados da exibição.** no **Gerenciador de soluções**.