---
title: Estendendo o filtro de Gerenciador de Soluções | Microsoft Docs
description: Saiba como estender Gerenciador de Soluções funcionalidade de filtro para mostrar ou ocultar arquivos diferentes no SDK do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Solution Explorer, extending
- extensibility [Visual Studio], projects and solutions
ms.assetid: df976c76-27ec-4f00-ab6d-a26a745dc6c7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d1256b807d67f95aa8ca1e952a4dca7bd550e0fc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075010"
---
# <a name="extend-the-solution-explorer-filter"></a>Estender o filtro de Gerenciador de Soluções
Você pode estender **Gerenciador de soluções** funcionalidade de filtro para mostrar ou ocultar arquivos diferentes. Por exemplo, você pode criar um filtro que mostra somente arquivos de fábrica de classes C# no **Gerenciador de soluções**, como demonstra este passo a passos.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

### <a name="create-a-visual-studio-package-project"></a>Criar um projeto de pacote do Visual Studio

1. Crie um projeto VSIX denominado `FileFilter` . Adicione um modelo de item de comando personalizado chamado **FileFilter**. Para obter mais informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).

2. Adicione uma referência a `System.ComponentModel.Composition` e `Microsoft.VisualStudio.Utilities` .

3. Faça com que o comando de menu apareça na barra de ferramentas **Gerenciador de soluções** . Abra o arquivo *FileFilterPackage. vsct* .

4. Altere o `<Button>` bloco para o seguinte:

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

1. No arquivo *Source. Extension. vsixmanifest* , adicione um ativo que seja um componente MEF.

2. Na guia **ativos** , escolha o botão **novo** .

3. No campo **tipo** , escolha **Microsoft. VisualStudio. MefComponent**.

4. No campo **origem** , escolha **um projeto na solução atual**.

5. No campo **projeto** , escolha **FileFilter** e, em seguida, escolha o botão **OK** .

### <a name="add-the-filter-code"></a>Adicionar o código do filtro

1. Adicione alguns GUIDs ao arquivo *FileFilterPackageGuids. cs* :

    ```csharp
    public const string guidFileFilterPackageCmdSetString = "00000000-0000-0000-0000-00000000"; // get your GUID from the .vsct file
    public const int FileFilterId = 0x100;
    ```

2. Adicione um arquivo de classe ao projeto FileFilter chamado *FileNameFilter. cs*.

3. Substitua o namespace vazio e a classe vazia pelo código abaixo.

     O `Task<IReadOnlyObservableSet> GetIncludedItemsAsync(IEnumerable<IVsHierarchyItem rootItems)` método usa a coleção que contém a raiz da solução ( `rootItems` ) e retorna a coleção de itens a serem incluídos no filtro.

     O `ShouldIncludeInFilter` método filtra os itens na hierarquia de **Gerenciador de soluções** com base na condição que você especificar.

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

4. Em *FileFilter. cs*, remova o posicionamento do comando e manuseie o código do Construtor FileFilter. O resultado deve ser assim:

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

     Remova o `ShowMessageBox()` método também.

5. No *FileFilterPackage. cs*, substitua o código no `Initialize()` método pelo seguinte:

    ```csharp
    protected override void Initialize()
    {
        Debug.WriteLine (string.Format(CultureInfo.CurrentCulture, "Entering Initialize() of: {0}", this.ToString()));
        base.Initialize();
    }
    ```

### <a name="test-your-code"></a>Testar seu código

1. Compile e execute o projeto. Uma segunda instância do Visual Studio é exibida. Isso é chamado de instância experimental.

2. Na instância experimental do Visual Studio, abra um projeto C#.

3. Procure o botão que você adicionou na barra de ferramentas **Gerenciador de soluções** . Deve ser o quarto botão à esquerda.

4. Quando você clica no botão, todos os arquivos devem ser filtrados e você deve ver que **todos os itens foram filtrados da exibição.** na **Gerenciador de soluções**.
