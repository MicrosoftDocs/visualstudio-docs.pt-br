---
title: Estendendo a janela de saída | Microsoft Docs
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
- Output window, about Output window
ms.assetid: b02fa88c-f92a-4ff6-ba5f-2eb4d48a643a
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e4afd91c42eeb60d005b1eb186c30d3896e3101f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51731393"
---
# <a name="extending-the-output-window"></a>Estendendo a Janela de Saída
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O **saída** janela é um conjunto de painéis de texto de leitura/gravação. O Visual Studio tem esses painéis internos: **compilar**, em quais projetos de se comunicar mensagens sobre compilações, e **gerais**, no qual [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] transmite mensagens sobre o IDE. Projetos de obtém uma referência para o **compilar** automaticamente por meio do painel a <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> métodos de interface e o Visual Studio oferece acesso direto ao **geral** painel por meio do <xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane> serviço. Além de painéis internos, você pode criar e gerenciar seus próprios painéis personalizados.  
  
 Você pode controlar a **saída** janela diretamente por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> interfaces. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> interface, que é oferecido pelo <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow> do serviço, que define métodos para criar, recuperar e destruindo **saída** painéis de janela. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> interface define os métodos para mostrar painéis, ocultando painéis e manipular seu texto. Uma maneira alternativa de controlar os **saída** janela é por meio de <xref:EnvDTE.OutputWindow> e <xref:EnvDTE.OutputWindowPane> objetos no modelo de objeto de automação do Visual Studio. Esses objetos encapsulam quase toda a funcionalidade do <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> interfaces. Além disso, o <xref:EnvDTE.OutputWindow> e <xref:EnvDTE.OutputWindowPane> objetos adicionam alguma funcionalidade de nível mais alto para tornar mais fácil enumerar os **saída** painéis de janela e para recuperar o texto de painéis.  
  
## <a name="creating-an-extension-that-uses-the-output-pane"></a>Criando uma extensão que usa o painel de saída  
 Você pode tornar uma extensão que exercite diferentes aspectos do painel de saída.  
  
1.  Crie um projeto do VSIX chamado `TestOutput` com um comando de menu denominado **TestOutput**. Para obter mais informações, consulte [criar uma extensão com um comando de Menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
2.  Adicione as seguintes referências:  
  
    1.  EnvDTE  
  
    2.  EnvDTE80  
  
3.  No TestOutput.cs, adicione a seguinte instrução using:  
  
    ```f#  
    using EnvDTE;  
    using EnvDTE80;  
    ```  
  
4.  No TestOutput.cs, exclua o método ShowMessageBox. Adicione o seguinte stub do método:  
  
    ```csharp  
    private void OutputCommandHandler(object sender, EventArgs e)  
    {  
    }  
    ```  
  
5.  No construtor TestOutput, altere o manipulador de comandos para OutputCommandHandler. Aqui está a parte que adiciona os comandos:  
  
    ```csharp  
    OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
    if (commandService != null)  
    {  
        CommandID menuCommandID = new CommandID(MenuGroup, CommandId);  
        EventHandler eventHandler = OutputCommandHandler;  
        MenuCommand menuItem = new MenuCommand(eventHandler, menuCommandID);  
        commandService.AddCommand(menuItem);  
    }  
    ```  
  
6.  As seções a seguir têm diferentes métodos que mostram diferentes maneiras de lidar com o painel de saída. Você pode chamar esses métodos ao corpo do método OutputCommandHandler(). Por exemplo, o código a seguir adiciona o método CreatePane() fornecido na próxima seção.  
  
    ```csharp  
    private void OutputCommandHandler(object sender, EventArgs e)  
    {  
        CreatePane(new Guid(), "Created Pane", true, false);  
    }  
    ```  
  
## <a name="creating-an-output-window-with-ivsoutputwindow"></a>Criação de uma janela de saída com IVsOutputWindow  
 Este exemplo mostra como criar um novo **saída** painel de janela usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> interface.  
  
```csharp  
void CreatePane(Guid paneGuid, string title,   
    bool visible, bool clearWithSolution)  
{  
    IVsOutputWindow output =   
        (IVsOutputWindow)GetService(typeof(SVsOutputWindow));  
    IVsOutputWindowPane pane;  
  
    // Create a new pane.  
    output.CreatePane(  
        ref paneGuid,   
        title,   
        Convert.ToInt32(visible),   
        Convert.ToInt32(clearWithSolution));  
  
    // Retrieve the new pane.  
    output.GetPane(ref paneGuid, out pane);  
  
     pane.OutputString("This is the Created Pane \n");  
}  
```  
  
 Se você adicionar esse método para a extensão fornecida na seção anterior, quando você clica o **invocar TestOutput** comando você deve ver o **saída** janela com um cabeçalho que diz **Mostrar saída de: CreatedPane** e as palavras **isso é o painel criado** no painel em si.  
  
## <a name="creating-an-output-window-with-outputwindow"></a>Criação de uma janela de saída com OutputWindow  
 Este exemplo mostra como criar uma **saída** painel de janela usando o <xref:EnvDTE.OutputWindow> objeto.  
  
```csharp  
void CreatePane(string title)  
{  
    DTE2 dte = (DTE2)GetService(typeof(DTE));  
    OutputWindowPanes panes =  
        dte.ToolWindows.OutputWindow.OutputWindowPanes;  
  
    try  
    {  
        // If the pane exists already, write to it.  
        panes.Item(title);  
    }  
    catch (ArgumentException)  
    {  
        // Create a new pane and write to it.  
        return panes.Add(title);  
    }  
}  
```  
  
 Embora o <xref:EnvDTE.OutputWindowPanes> coleção permite que você recupere um **saída** painel da janela pelo seu título, títulos do painel não têm garantia de ser exclusivo. Quando você tiver dúvidas a exclusividade de um título, use o <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow.GetPane%2A> método para recuperar o painel correto pelo seu GUID.  
  
 Se você adicionar esse método para a extensão fornecida na seção anterior, quando você clica o **invocar TestOutput** comando você deve ver a janela de saída com um cabeçalho que diz **Mostrar saída de: DTEPane** e as palavras **adicionado painel de DTE** no painel em si.  
  
## <a name="deleting-an-output-window"></a>Exclusão de uma janela de saída  
 Este exemplo mostra como excluir uma **saída** painel da janela.  
  
```csharp  
void DeletePane(Guid paneGuid)  
{  
    IVsOutputWindow output =  
    (IVsOutputWindow)ServiceProvider.GetService(typeof(SVsOutputWindow));  
  
    IVsOutputWindowPane pane;  
    output.GetPane(ref paneGuid, out pane);  
  
    if (pane == null)  
    {  
        CreatePane(paneGuid, "New Pane\n", true, true);  
    }  
     else  
    {  
        output.DeletePane(ref paneGuid);  
    }  
}  
```  
  
 Se você adicionar esse método para a extensão fornecida na seção anterior, quando você clica o **invocar TestOutput** comando você deve ver a janela de saída com um cabeçalho que diz **Mostrar saída de: painel novo** e as palavras **adicionado painel criado** no painel em si. Se você clicar na **TestOutput invocar** comando novamente, o painel é excluído.  
  
## <a name="getting-the-general-pane-of-the-output-window"></a>Obtendo o painel geral da janela de saída  
 Este exemplo mostra como obter o interno **gerais** painel da **saída** janela.  
  
```csharp  
void GetGeneralPane()  
{  
    return (IVsOutputWindowPane)GetService(  
        typeof(SVsGeneralOutputWindowPane));  
}  
```  
  
 Se você adicionar esse método para a extensão fornecida na seção anterior, quando você clica o **invocar TestOutput** comando, você deverá ver que o **saída** janela mostra as palavras **geral encontrado painel** no painel.  
  
## <a name="getting-the-build-pane-of-the-output-window"></a>Obtendo o painel de Build da janela de saída  
 Este exemplo mostra como localizar o painel de Build e gravar nele. Uma vez que o painel de compilação não está ativado por padrão, ele ativa-lo também.  
  
```csharp  
void OutputTaskItemStringExExample(string buildMessage)  
{  
    EnvDTE80.DTE2 dte = (EnvDTE80.DTE2)ServiceProvider.GetService(typeof(EnvDTE.DTE));  
  
    EnvDTE.OutputWindowPanes panes =  
        dte.ToolWindows.OutputWindow.OutputWindowPanes;  
    foreach (EnvDTE.OutputWindowPane pane in panes)  
        {  
            if (pane.Name.Contains("Build"))  
            {  
                pane.OutputString(buildMessage + "\n");  
                pane.Activate();  
                return;  
             }  
        }  
}  
```

