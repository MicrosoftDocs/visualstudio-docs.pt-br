---
title: Estendendo a janela de saída | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Output window, about Output window
ms.assetid: b02fa88c-f92a-4ff6-ba5f-2eb4d48a643a
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 33e34a78fc06bc2b7f40129e33b6d2d78ff561c5
ms.sourcegitcommit: 20d1b9a5bf041bb28453501eb63bc0537a8e4f54
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51645205"
---
# <a name="extend-the-output-window"></a>Estender a janela de saída
O **saída** janela é um conjunto de painéis de texto de leitura/gravação. O Visual Studio tem esses painéis internos: **compilar**, em quais projetos de se comunicar mensagens sobre compilações, e **gerais**, no qual [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] transmite mensagens sobre o IDE. Projetos de obtém uma referência para o **compilar** automaticamente por meio do painel a <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> métodos de interface e o Visual Studio oferece acesso direto ao **geral** painel por meio do <xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane> serviço. Além de painéis internos, você pode criar e gerenciar seus próprios painéis personalizados.  
  
 Você pode controlar a **saída** janela diretamente por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> interfaces. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> interface, que é oferecido pelo <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow> do serviço, que define métodos para criar, recuperar e destruindo **saída** painéis de janela. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> interface define os métodos para mostrar painéis, ocultando painéis e manipular seu texto. Uma maneira alternativa de controlar os **saída** janela é por meio de <xref:EnvDTE.OutputWindow> e <xref:EnvDTE.OutputWindowPane> objetos no modelo de objeto de automação do Visual Studio. Esses objetos encapsulam quase toda a funcionalidade do <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> interfaces. Além disso, o <xref:EnvDTE.OutputWindow> e <xref:EnvDTE.OutputWindowPane> objetos adicionam alguma funcionalidade de nível mais alto para tornar mais fácil enumerar os **saída** painéis de janela e para recuperar o texto de painéis.  
  
## <a name="create-an-extension-that-uses-the-output-pane"></a>Criar uma extensão que usa o painel de saída  
 Você pode tornar uma extensão que exercite diferentes aspectos do painel de saída.  
  
1.  Crie um projeto do VSIX chamado `TestOutput` com um comando de menu denominado **TestOutput**. Para obter mais informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
2.  Adicione as seguintes referências:  
  
    1.  EnvDTE  
  
    2.  EnvDTE80  
  
3.  Na *TestOutput.cs*, adicione a seguinte instrução using:  
  
    ```f#  
    using EnvDTE;  
    using EnvDTE80;  
    ```  
  
4.  Na *TestOutput.cs*, exclua o `ShowMessageBox` método. Adicione o seguinte stub do método:  
  
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
  
6.  As seções a seguir têm diferentes métodos que mostram diferentes maneiras de lidar com o painel de saída. Você pode chamar esses métodos ao corpo do `OutputCommandHandler()` método. Por exemplo, o código a seguir adiciona o `CreatePane()` método fornecido na próxima seção.  
  
    ```csharp  
    private void OutputCommandHandler(object sender, EventArgs e)  
    {  
        CreatePane(new Guid(), "Created Pane", true, false);  
    }  
    ```  
  
## <a name="create-an-output-window-with-ivsoutputwindow"></a>Criar uma janela de saída com IVsOutputWindow  
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
  
## <a name="create-an-output-window-with-outputwindow"></a>Criar uma janela de saída com OutputWindow  
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
  
## <a name="delete-an-output-window"></a>Excluir uma janela de saída  
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
  
## <a name="get-the-general-pane-of-the-output-window"></a>Obter painel geral da janela de saída  
 Este exemplo mostra como obter o interno **gerais** painel da **saída** janela.  
  
```csharp  
void GetGeneralPane()  
{  
    return (IVsOutputWindowPane)GetService(  
        typeof(SVsGeneralOutputWindowPane));  
}  
```  
  
 Se você adicionar esse método para a extensão fornecida na seção anterior, quando você clica o **invocar TestOutput** comando, você deverá ver que o **saída** janela mostra as palavras **geral encontrado painel** no painel.  
  
## <a name="get-the-build-pane-of-the-output-window"></a>Obter o painel de Build da janela de saída  
 Este exemplo mostra como localizar o **Build** painel e gravação a ela. Uma vez que o **Build** painel não está ativado por padrão, ele ativa também.  
  
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
