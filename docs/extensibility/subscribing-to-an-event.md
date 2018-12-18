---
title: Assinar um evento | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- running document table (RDT), responding to events
- running document table (RDT), subscribing to events
ms.assetid: e94a4fea-94df-488e-8560-9538413422bc
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 41ed19cb31924e90ef9326aad5c8cad117996793
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31141897"
---
# <a name="subscribing-to-an-event"></a>Assinar um evento
Este passo a passo explica como criar uma janela de ferramenta que responde a eventos em uma tabela de documento (RDT) em execução. Uma janela de ferramentas hospeda um controle de usuário implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> método conecta-se a interface para os eventos.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instalar o SDK do Visual Studio no Centro de download. Ele está incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS posteriormente. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="subscribing-to-rdt-events"></a>Assinando eventos RDT  
  
#### <a name="to-create-an-extension-with-a-tool-window"></a>Para criar uma extensão com uma janela de ferramenta  
  
1.  Crie um projeto chamado **RDTExplorer** usando o modelo VSIX e adicionar um modelo de item da janela de ferramenta personalizada denominado **RDTExplorerWindow**.  
  
     Para obter mais informações sobre como criar uma extensão com uma janela da ferramenta, consulte [criando uma extensão com uma janela de ferramenta](../extensibility/creating-an-extension-with-a-tool-window.md).  
  
#### <a name="to-subscribe-to-rdt-events"></a>Para assinar eventos RDT  
  
1.  Abra o arquivo RDTExplorerWindowControl.xaml e excluir o botão chamado `button1`. Adicionar um <xref:System.Windows.Forms.ListBox> controlar e aceite o nome padrão. O elemento de grade deve ter esta aparência:  
  
    ```xml  
    <Grid>  
        <StackPanel Orientation="Vertical" Margin="-10,10,10,0">  
            <TextBlock Margin="10" HorizontalAlignment="Center">RDTExplorerWindow</TextBlock>  
            <ListBox x:Name="listBox" Height="100" />  
        </StackPanel>  
    </Grid>  
    ```  
  
2.  Abra o arquivo RDTExplorerWindow.cs no modo de exibição de código. Adicione o seguinte usando instruções para o início do arquivo.  
  
    ```csharp  
    using Microsoft.VisualStudio;  
    using Microsoft.VisualStudio.Shell;  
    using Microsoft.VisualStudio.Shell.Interop;  
    ```  
  
3.  Modificar o `RDTExplorerWindow` classe isso que, além de derivação do <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> classe, ele implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> interface.  
  
    ```csharp  
    public class RDTExplorerWindow : ToolWindowPane, IVsRunningDocTableEvents  
    {. . .}  
    ```  
  
4.  Implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>.  
  
    -   Implemente a interface. Posicione o cursor no nome do IVsRunningDocTableEvents. Você deve ver uma lâmpada na margem esquerda. Clique na seta para baixo à direita da lâmpada e selecione **implementar interface**.  
  
5.  Cada método na interface, substitua a linha `throw new NotImplementedException();` com isso:  
  
    ```csharp  
    return VSConstants.S_OK;  
    ```  
  
6.  Adicione um campo de cookie para a classe RDTExplorerWindow.  
  
    ```csharp  
    private uint rdtCookie;   
    ```  
  
     Isso mantém o cookie é retornado pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> método.  
  
7.  Substitua método de Initialize () do RDTExplorerWindow para registrar eventos de RDT. Você sempre deve obter serviços no método Initialize () do ToolWindowPane, não no construtor.  
  
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
  
     O <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnadviseRunningDocTableEvents%2A> método exclui a conexão entre `RDTExplorer` e RDT notificação de evento.  
  
9. Adicione a seguinte linha ao corpo do <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnBeforeLastDocumentUnlock%2A> manipulador, antes de `return` instrução.  
  
    ```csharp  
    public int OnBeforeLastDocumentUnlock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)  
    {  
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnBeforeLastDocumentUnlock");  
        return VSConstants.S_OK;  
    }  
    ```  
  
10. Adicione uma linha semelhante ao corpo do <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterFirstDocumentLock%2A> manipulador e outros eventos que você deseja ver na caixa de listagem.  
  
    ```csharp  
    public int OnAfterFirstDocumentLock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)  
    {  
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnAfterFirstDocumentLock");  
        return VSConstants.S_OK;  
    }  
    ```  
  
11. Compile o projeto e comece a depuração. É exibida a instância experimental do Visual Studio.  
  
12. Abra o **RDTExplorerWindow** (**exibição / outras janelas / RDTExplorerWindow**).  
  
     O **RDTExplorerWindow** janela é aberta com uma lista de eventos em branco.  
  
13. Abra ou crie uma solução.  
  
     Como `OnBeforeLastDocument` e `OnAfterFirstDocument` os eventos são disparados, notificação de cada evento será exibido no evento lista.