---
title: Assinando um evento | Microsoft Docs
description: Saiba como criar uma janela de ferramentas que responde a eventos em uma tabela de documentos em execução no SDK do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- running document table (RDT), responding to events
- running document table (RDT), subscribing to events
ms.assetid: e94a4fea-94df-488e-8560-9538413422bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 01271016eed9a4a157b333a2f0435589b0a028d5
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899377"
---
# <a name="subscribing-to-an-event"></a>Assinando um evento
Este passo a passo explica como criar uma janela de ferramentas que responde a eventos em uma RDT (tabela de documentos em execução). Uma janela de ferramentas hospeda um controle de usuário que implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> . O <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> método conecta a interface aos eventos.

## <a name="prerequisites"></a>Pré-requisitos
 A partir Visual Studio 2015, você não instala o SDK do Visual Studio do centro de download. Ele é incluído como um recurso opcional na Visual Studio configuração. Você também pode instalar o SDK do VS posteriormente. Para obter mais informações, [consulte Instalando o SDK Visual Studio .](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="subscribing-to-rdt-events"></a>Assinando eventos RDT

#### <a name="to-create-an-extension-with-a-tool-window"></a>Para criar uma extensão com uma janela de ferramentas

1. Crie um projeto chamado **RDTExplorer** usando o modelo VSIX e adicione um modelo de item de janela de ferramentas personalizado chamado **RDTExplorerWindow**.

     Para obter mais informações sobre como criar uma extensão com uma janela de ferramentas, consulte [Criando uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).

#### <a name="to-subscribe-to-rdt-events"></a>Para assinar eventos RDT

1. Abra o arquivo RDTExplorerWindowControl.xaml e exclua o botão chamado `button1` . Adicione um <xref:System.Windows.Forms.ListBox> controle e aceite o nome padrão. O elemento Grid deve ter esta aparência:

    ```xml
    <Grid>
        <StackPanel Orientation="Vertical" Margin="-10,10,10,0">
            <TextBlock Margin="10" HorizontalAlignment="Center">RDTExplorerWindow</TextBlock>
            <ListBox x:Name="listBox" Height="100" />
        </StackPanel>
    </Grid>
    ```

2. Abra o arquivo RDTExplorerWindow.cs na exibição de código. Adicione as seguintes diretivas using ao início do arquivo.

    ```csharp
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

3. Modifique `RDTExplorerWindow` a classe para que, além de derivar da classe , ela <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> implemente a interface <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> .

    ```csharp
    public class RDTExplorerWindow : ToolWindowPane, IVsRunningDocTableEvents
    {. . .}
    ```

4. Implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>.

    - Implemente a interface . Coloque o cursor no nome IVsRunningDocTableEvents. Você deverá ver uma lâmpada na margem esquerda. Clique na seta Para baixo à direita da lâmpada e selecione **Implementar interface**.

5. Em cada método na interface, substitua a linha `throw new NotImplementedException();` por esta:

    ```csharp
    return VSConstants.S_OK;
    ```

6. Adicione um campo de cookie à classe RDTExplorerWindow.

    ```csharp
    private uint rdtCookie;
    ```

     Isso contém o cookie retornado pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> método .

7. Substitua o método Initialize() da RDTExplorerWindow para se registrar em eventos RDT. Você sempre deve obter serviços no método Initialize() do ToolWindowPane, não no construtor.

    ```csharp
    protected override void Initialize()
    {
        IVsRunningDocumentTable rdt = (IVsRunningDocumentTable)
        this.GetService(typeof(SVsRunningDocumentTable));
        rdt.AdviseRunningDocTableEvents(this, out rdtCookie);
    }
    ```

     O <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> serviço é chamado para obter uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> interface. O método conecta eventos RDT a um objeto que implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> , nesse caso, um objeto RDTExplorer.

8. Atualize o método Dispose() do RDTExplorerWindow.

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

     O <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnadviseRunningDocTableEvents%2A> método exclui a conexão entre e a `RDTExplorer` notificação de evento RDT.

9. Adicione a linha a seguir ao corpo do <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnBeforeLastDocumentUnlock%2A> manipulador, logo antes da `return` instrução .

    ```csharp
    public int OnBeforeLastDocumentUnlock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)
    {
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnBeforeLastDocumentUnlock");
        return VSConstants.S_OK;
    }
    ```

10. Adicione uma linha semelhante ao corpo do manipulador e a <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterFirstDocumentLock%2A> outros eventos que você deseja ver na caixa de listagem.

    ```csharp
    public int OnAfterFirstDocumentLock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)
    {
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnAfterFirstDocumentLock");
        return VSConstants.S_OK;
    }
    ```

11. Compile o projeto e comece a depuração. A Visual Studio experimental é exibida.

12. Abra **o RDTExplorerWindow** (**View/Other Windows/RDTExplorerWindow**).

     A **janela RDTExplorerWindow** é aberta com uma lista de eventos vazia.

13. Abra ou crie uma solução.

     À `OnBeforeLastDocument` medida que os eventos e são `OnAfterFirstDocument` acionados, a notificação de cada evento aparece na lista de eventos.
