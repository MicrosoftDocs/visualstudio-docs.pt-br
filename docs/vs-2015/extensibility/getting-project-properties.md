---
title: Obter propriedades do projeto | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project properties, displaying in tool window
- tool windows, displaying project properties
ms.assetid: 96ba07ca-0811-4013-8602-12550ac4ba79
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: af78a1c8e89710af73bf5f6d25cf3446cd0d50af
ms.sourcegitcommit: c496a77add807ba4a29ee6a424b44a5de89025ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "58926826"
---
# <a name="getting-project-properties"></a>Obtendo as propriedades do projeto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo mostra como exibe as propriedades do projeto em uma janela de ferramenta.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
### <a name="to-create-a-vsix-project-and-add-a-tool-window"></a>Para criar um projeto VSIX e adicionar uma janela de ferramentas  
  
1.  Cada extensão do Visual Studio inicia com um projeto de implantação do VSIX que conterá os ativos de extensão. Criar uma [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto do VSIX chamado `ProjectPropertiesExtension`. Você pode encontrar o modelo de projeto VSIX na **novo projeto** diálogo sob **Visual C# / extensibilidade**.  
  
2.  Adicionar uma janela de ferramentas, adicionando um modelo de item da janela de ferramenta personalizada denominado `ProjectPropertiesToolWindow`. No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **Add / Novo Item**. No **caixa de diálogo Adicionar Novo Item**, acesse **itens do Visual C# / extensibilidade** e selecione **janela de ferramenta personalizada**. No **nome** campo na parte inferior da caixa de diálogo, altere o nome de arquivo para `ProjectPropertiesToolWindow.cs`. Para obter mais informações sobre como criar uma janela de ferramentas personalizada, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).  
  
3.  Compile a solução e verificar se ele é compilado sem erros.  
  
### <a name="to-display-project-properties-in-a-tool-window"></a>Para exibir as propriedades do projeto em uma janela de ferramentas  
  
1.  No arquivo ProjectPropertiesToolWindowCommand.cs, adicione as seguintes instruções using.  
  
    ```csharp  
    using EnvDTE;  
    using System.Windows.Controls;  
  
    ```  
  
2.  No ProjectPropertiesToolWindowControl.xaml, remova o botão existente e adicione um modo de exibição de árvore da caixa de ferramentas. Você também pode remover o manipulador de eventos click do arquivo ProjectPropertiesToolWindowControl.xaml.cs.  
  
3.  Na ProjectPropertiesToolWindowCommand.cs, use o método ShowToolWindow() para abrir o projeto e leia suas propriedades e adicionar as propriedades para o modo de exibição de árvore. O código para ShowToolWindow deve ser semelhante ao seguinte:  
  
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
  
4.  Compile o projeto e comece a depuração. A instância experimental deve aparecer.  
  
5.  Na instância experimental, abra um projeto.  
  
6.  No **exibição / Windows outras** clique em **ProjectPropertiesToolWindow**.  
  
     Você deve ver o controle de árvore na janela da ferramenta junto com o nome do primeiro projeto e de todas as suas propriedades de projeto.
