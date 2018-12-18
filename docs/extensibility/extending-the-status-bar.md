---
title: Estendendo a barra de Status | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- status bars, about status bars
- status bars, overview
ms.assetid: f955115c-4c5f-45ec-b41b-365868c5ec0c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 0e072814120f18c7cc1ea09bf0829266958691ba
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39497908"
---
# <a name="extend-the-status-bar"></a>Estender a barra de status
Você pode usar a barra de status do Visual Studio na parte inferior do IDE para exibir informações.  
  
 Quando você estende a barra de status, você pode exibir informações e a interface do usuário em quatro regiões: a região de comentários, a barra de progresso, a região de animação e a região de designer. A região de comentários permite exibir texto e realce o texto exibido. A barra de progresso mostra o progresso incremental para operações de curta execução como salvar um arquivo. A região de animação exibe uma animação em loop continuamente para operações de longa execução ou operação de tamanho indeterminado, tais como a criação de vários projetos em uma solução. E a região de designer mostra o número de linha e coluna do local do cursor.  
  
 Você pode obter a barra de status usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbar> interface (da <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> service). Além disso, qualquer objeto colocado no local em um quadro de janela pode se registrar como um objeto de cliente da barra de status ao implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> interface. Sempre que uma janela é ativada, o Visual Studio consulta o objeto localizado nessa janela para o `IVsStatusbarUser` interface. Se encontrado, ele chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> método sobre a interface retornada e o objeto pode atualizar a barra de status de dentro desse método. Documentar o windows, por exemplo, pode usar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> método para atualizar as informações na região de designer quando eles se tornar ativos.  
  
 Os procedimentos a seguir pressupõem que você compreenda como criar um projeto VSIX e adicione um comando de menu personalizado. Para obter informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
## <a name="modify-the-status-bar"></a>Modificar a barra de status  
 Este procedimento mostra como definir e obter o texto, exibir texto estático e realçar o texto exibido na região de comentários de barra de status.  
  
### <a name="read-and-write-to-the-status-bar"></a>Leitura e gravação para a barra de status  
  
1.  Crie um projeto do VSIX chamado **TestStatusBarExtension** e adicione um comando de menu chamado **TestStatusBarCommand**.  
  
2.  Na *TestStatusBarCommand.cs*, substitua o código de método do manipulador de comando (`MenuItemCallback`) com o seguinte:  
  
    ```csharp  
    private void MenuItemCallback(object sender, EventArgs e)  
    {  
        IVsStatusbar statusBar = (IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));  
  
        // Make sure the status bar is not frozen  
        int frozen;  
  
        statusBar.IsFrozen(out frozen);  
  
        if (frozen != 0)   
        {  
            statusBar.FreezeOutput(0);  
        }  
  
        // Set the status bar text and make its display static.  
        statusBar.SetText("We just wrote to the status bar.");  
  
        // Freeze the status bar.  
        statusBar.FreezeOutput(1);  
  
        // Get the status bar text.   
        string text;  
        statusBar.GetText(out text);  
        System.Windows.Forms.MessageBox.Show(text);  
  
        // Clear the status bar text.  
        statusBar.FreezeOutput(0);  
        statusBar.Clear();  
    }  
    ```  
  
3.  Compile o código e iniciar a depuração.  
  
4.  Abra o **ferramentas** menu na instância experimental do Visual Studio. Clique o **TestStatusBarCommand invocar** botão.  
  
     Você deverá ver que o texto na barra agora leituras de status **acabamos de gravar para a barra de status.** e a caixa de mensagem que aparece tem o mesmo texto.  
  
### <a name="update-the-progress-bar"></a>Atualizar a barra de progresso  
  
1.  Neste procedimento, mostraremos como inicializar e atualizar a barra de progresso.  
  
2.  Abra o *TestStatusBarCommand.cs* do arquivo e substitua o `MenuItemCallback` método com o código a seguir:  
  
    ```csharp  
    private void MenuItemCallback(object sender, EventArgs e)  
    {  
        IVsStatusbar statusBar = (IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));  
        uint cookie = 0;  
        string label = "Writing to the progress bar";  
  
        // Initialize the progress bar.  
        statusBar.Progress(ref cookie, 1, "", 0, 0);  
  
        for (uint i = 0, total = 20; i <= total; i++)  
        {  
            // Display progress every second.  
            statusBar.Progress(ref cookie, 1, label, i, total);  
            System.Threading.Thread.Sleep(1000);  
        }  
  
        // Clear the progress bar.  
        statusBar.Progress(ref cookie, 0, "", 0, 0);  
    }  
    ```  
  
3.  Compile o código e iniciar a depuração.  
  
4.  Abra o **ferramentas** menu na instância experimental do Visual Studio. Clique em **TestStatusBarCommand invocar** botão.  
  
     Você deverá ver que o texto na barra agora leituras de status **escrevendo para a barra de progresso.** Você também deve ver a barra de progresso é atualizada a cada segundo por 20 segundos. Depois que a barra de status e a barra de progresso são desmarcadas.  
  
### <a name="display-an-animation"></a>Exibir uma animação  
  
1.  A barra de status exibe uma animação de loop que indica uma operação de longa execução (por exemplo, compilando vários projetos em uma solução). Se você não vir essa animação, verifique se você tem o correto **ferramentas** > **opções** configurações:  
  
     Vá para o **ferramentas** > **opções** > **geral** guia e desmarque a opção **ajustar automaticamente experiência visual com base no cliente desempenho**. Em seguida, marque a opção de subpropriedades **habilitar experiência visual avançada do cliente**. Agora, você poderá visualizar a animação quando você compila o projeto em sua instância experimental do Visual Studio.  
  
     Neste procedimento, exibimos a animação padrão do Visual Studio que representa a criação de um projeto ou solução.  
  
2.  Abra o *TestStatusBarCommand.cs* do arquivo e substitua o `MenuItemCallback` método com o código a seguir:  
  
    ```csharp  
    private void MenuItemCallback(object sender, EventArgs e)  
    {  
        IVsStatusbar statusBar =(IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));  
  
        // Use the standard Visual Studio icon for building.  
        object icon = (short)Microsoft.VisualStudio.Shell.Interop.Constants.SBAI_Build;  
  
        // Display the icon in the Animation region.  
        statusBar.Animation(1, ref icon);  
  
        // The message box pauses execution for you to look at the animation.  
        System.Windows.Forms.MessageBox.Show("showing?");  
  
        // Stop the animation.   
        statusBar.Animation(0, ref icon);  
    }  
    ```  
  
3.  Compile o código e iniciar a depuração.  
  
4.  Abra o **ferramentas** menu na instância experimental do Visual Studio e clique em **TestStatusBarCommand invocar**.  
  
     Quando você vir a caixa de mensagem, você também verá a animação na barra de status na extrema direita. Quando você descartar a caixa de mensagem, a animação desaparece.