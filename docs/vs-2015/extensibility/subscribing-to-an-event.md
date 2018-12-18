---
title: Assinar um evento | Microsoft Docs
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
- running document table (RDT), responding to events
- running document table (RDT), subscribing to events
ms.assetid: e94a4fea-94df-488e-8560-9538413422bc
caps.latest.revision: 36
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 2e01d10f68436cacdb3a662540723335743b9f10
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51776571"
---
# <a name="subscribing-to-an-event"></a>Assinando um evento
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo explica como criar uma janela de ferramentas que responde a eventos em uma tabela de documento (RDT) em execução. Uma janela de ferramentas hospeda um controle de usuário que implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> método conecta-se a interface para os eventos.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="subscribing-to-rdt-events"></a>Assinando eventos RDT  
  
#### <a name="to-create-an-extension-with-a-tool-window"></a>Para criar uma extensão com uma janela de ferramentas  
  
1.  Crie um projeto chamado **RDTExplorer** usando o modelo VSIX e adicionar um modelo de item da janela de ferramenta personalizada denominado **RDTExplorerWindow**.  
  
     Para obter mais informações sobre como criar uma extensão com uma janela de ferramentas, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).  
  
#### <a name="to-subscribe-to-rdt-events"></a>Para assinar eventos RDT  
  
1.  Abra o arquivo RDTExplorerWindowControl.xaml e exclua o botão chamado `button1`. Adicionar um <xref:System.Windows.Forms.ListBox> controlar e aceite o nome padrão. O elemento de grade deve ter esta aparência:  
  
    ```xml  
    <Grid>  
        <StackPanel Orientation="Vertical" Margin="-10,10,10,0">  
            <TextBlock Margin="10" HorizontalAlignment="Center">RDTExplorerWindow</TextBlock>  
            <ListBox x:Name="listBox" Height="100" />  
        </StackPanel>  
    </Grid>  
    ```  
  
2.  Abra o arquivo de RDTExplorerWindow.cs na exibição de código. Adicione o seguinte usando instruções ao início do arquivo.  
  
    ```csharp  
    using Microsoft.VisualStudio;  
    using Microsoft.VisualStudio.Shell;  
    using Microsoft.VisualStudio.Shell.Interop;  
    ```  
  
3.  Modificar a `RDTExplorerWindow` classe isso que, além de derivar do <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> classe, ele implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> interface.  
  
    ```csharp  
    public class RDTExplorerWindow : ToolWindowPane, IVsRunningDocTableEvents  
    {. . .}  
    ```  
  
4.  Implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>.  
  
    -   Implemente a interface. Coloque o cursor no nome do IVsRunningDocTableEvents. Você deve ver uma lâmpada na margem esquerda. Clique na seta para baixo à direita da lâmpada e selecione **implementar interface**.  
  
5.  Em cada método na interface, substitua a linha `throw new NotImplementedException();` com este:  
  
    ```csharp  
    return VSConstants.S_OK;  
    ```  
  
6.  Adicione um campo de cookie para a classe RDTExplorerWindow.  
  
    ```csharp  
    private uint rdtCookie;   
    ```  
  
     Isso mantém o cookie que é retornado pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> método.  
  
7.  Substitua método de Initialize () do RDTExplorerWindow para registrar eventos RDT. Você sempre deve obter serviços no método Initialize () do ToolWindowPane, não no construtor.  
  
    ```csharp  
    protected override void Initialize()  
    {  
        IVsRunningDocumentTable rdt = (IVsRunningDocumentTable)  
        this.GetService(typeof(SVsRunningDocumentTable));  
        rdt.AdviseRunningDocTableEvents(this, out rdtCookie);  
    }  
    ```  
  
     O <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> serviço é chamado para obter um <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> interface. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> método conecta eventos RDT para um objeto que implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>, nesse caso, um objeto RDTExplorer.  
  
8.  Atualização do RDTExplorerWindow Dispose ().  
  
    ```csharp  
    protected override void Dispose(bool disposing)  
    {  
        // Release the RDT cookie.  
        IVsRunningDocumentTable rdt = (IVsRunningDocumentTable)  
            Package.GetGlobalService(typeof(SVsRunningDocumentTable));  
        rdt.UnadviseRunningDocTableEvents(rdtCookie);  
  
        base.Dispose(disposing);  
    }  
    ```  
  
     O <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnadviseRunningDocTableEvents%2A> método exclui a conexão entre `RDTExplorer` e notificação de evento RDT.  
  
9. Adicione a seguinte linha ao corpo do <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnBeforeLastDocumentUnlock%2A> manipulador, imediatamente antes o `return` instrução.  
  
    ```csharp  
    public int OnBeforeLastDocumentUnlock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)  
    {  
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnBeforeLastDocumentUnlock");  
        return VSConstants.S_OK;  
    }  
    ```  
  
10. Adicione uma linha semelhante ao corpo do <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterFirstDocumentLock%2A> manipulador e a outros eventos que você deseja ver na caixa de listagem.  
  
    ```csharp  
    public int OnAfterFirstDocumentLock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)  
    {  
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnAfterFirstDocumentLock");  
        return VSConstants.S_OK;  
    }  
    ```  
  
11. Compile o projeto e comece a depuração. A instância experimental do Visual Studio é exibida.  
  
12. Abra o **RDTExplorerWindow** (**modo de exibição / outros Windows / RDTExplorerWindow**).  
  
     O **RDTExplorerWindow** janela é aberta com uma lista de eventos vazio.  
  
13. Abra ou crie uma solução.  
  
     Como `OnBeforeLastDocument` e `OnAfterFirstDocument` os eventos são disparados, notificação de cada evento é exibido no evento lista.

