---
title: Obtendo propriedades do projeto | Microsoft Docs
description: Saiba como exibir as propriedades do projeto em uma janela de ferramentas. Este exemplo mostra o controle de árvore na janela de ferramentas.
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- project properties, displaying in tool window
- tool windows, displaying project properties
ms.assetid: 96ba07ca-0811-4013-8602-12550ac4ba79
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8de3f32951cb70b8115781ce067950c7e518b102
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057657"
---
# <a name="get-project-properties"></a>Obter propriedades do projeto

Este tutorial mostra como exibir as propriedades do projeto em uma janela de ferramentas.

## <a name="prerequisites"></a>Pré-requisitos

A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

### <a name="to-create-a-vsix-project-and-add-a-tool-window"></a>Para criar um projeto VSIX e adicionar uma janela de ferramentas

1. Cada extensão do Visual Studio começa com um projeto de implantação VSIX, que conterá os ativos de extensão. Crie um [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] projeto VSIX denominado `ProjectPropertiesExtension` . Você pode encontrar o modelo de projeto VSIX na caixa de diálogo **novo projeto** pesquisando por "VSIX".

2. Adicione uma janela de ferramentas adicionando um modelo de item de janela de ferramenta personalizada chamado `ProjectPropertiesToolWindow` . Na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >  **novo item**. Na **caixa de diálogo Adicionar novo item**, vá para extensibilidade de **itens do Visual C#**  >   e selecione **janela de ferramenta personalizada**. No campo **nome** na parte inferior da caixa de diálogo, altere o nome do arquivo para `ProjectPropertiesToolWindow.cs` . Para obter mais informações sobre como criar uma janela de ferramentas personalizada, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).

3. Compile a solução e verifique se ela é compilada sem erros.

### <a name="to-display-project-properties-in-a-tool-window"></a>Para exibir as propriedades do projeto em uma janela de ferramentas

1. No arquivo ProjectPropertiesToolWindowCommand. cs, adicione as seguintes diretivas using.

    ```csharp
    using EnvDTE;
    using System.Windows.Controls;

    ```

2. Em *ProjectPropertiesToolWindowControl. XAML*, remova o botão existente e adicione um TreeView da caixa de ferramentas. Você também pode remover o manipulador de eventos de clique do arquivo *ProjectPropertiesToolWindowControl. XAML. cs* .

3. Em *ProjectPropertiesToolWindowCommand. cs*, use o `ShowToolWindow()` método para abrir o projeto e ler suas propriedades e, em seguida, adicione as propriedades ao TreeView. O código para ShowToolWindow deve ser semelhante ao seguinte:

    ```csharp
    private void ShowToolWindow(object sender, EventArgs e)
    {
        ToolWindowPane window = this.package.FindToolWindow(typeof(ProjectPropertiesToolWindow), 0, true);
        if ((null == window) || (null == window.Frame))
        {
            throw new NotSupportedException("Cannot create window.");
        }
        IVsWindowFrame windowFrame = (IVsWindowFrame)window.Frame;
        Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(windowFrame.Show());

        // Get the tree view and populate it if there is a project open.
        ProjectPropertiesToolWindowControl control = (ProjectPropertiesToolWindowControl)window.Content;
        TreeView treeView = control.treeView;

        // Reset the TreeView to 0 items.
        treeView.Items.Clear();

        DTE dte = (DTE)this.ServiceProvider.GetService(typeof(DTE));
        Projects projects = dte.Solution.Projects;
        if (projects.Count == 0)   // no project is open
        {
            TreeViewItem item = new TreeViewItem();
            item.Name = "Projects";
            item.ItemsSource = new string[]{ "no projects are open." };
            item.IsExpanded = true;
            treeView.Items.Add(item);
            return;
        }

        Project project = projects.Item(1);
        TreeViewItem item1 = new TreeViewItem();
        item1.Header = project.Name + "Properties";
        treeView.Items.Add(item1);

        foreach (Property property in project.Properties)
        {
            TreeViewItem item = new TreeViewItem();
            item.ItemsSource = new string[] { property.Name };
            item.IsExpanded = true;
            treeView.Items.Add(item);
        }
    }
    ```

4. Compile o projeto e comece a depuração. A instância experimental deve aparecer.

5. Na instância experimental, abra um projeto.

6. Em **Exibir**  >  **outras janelas** , clique em **ProjectPropertiesToolWindow**.

  Você deve ver o controle de árvore na janela de ferramentas junto com o nome do primeiro projeto e de todas as suas propriedades de projeto.
