---
title: Criar e gerenciar caixas de diálogo modais | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- dialog boxes, managing in Visual Studio
ms.assetid: 491bc0de-7dba-478c-a76b-923440e090f3
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b6c5a4bdcb6496bae9bf718c38bcf512fbf69756
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39498743"
---
# <a name="create-and-manage-modal-dialog-boxes"></a>Criar e gerenciar caixas de diálogo modais
Quando você cria uma caixa de diálogo modal dentro do Visual Studio, você deve garantir que a janela pai da caixa de diálogo é desabilitada enquanto a caixa de diálogo é exibida e habilite novamente a janela pai depois que a caixa de diálogo é fechada. Se você não fizer isso, você poderá receber o erro: *Microsoft Visual Studio não é possível desligar porque uma caixa de diálogo modal está ativa. Feche a caixa de diálogo e tente novamente.*  
  
 Há duas maneiras de fazer isso. A maneira recomendada, se você tiver uma caixa de diálogo do WPF é derivá-lo partir <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>e, em seguida, chame <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow.ShowModal%2A> para exibir a caixa de diálogo. Se você fizer isso, você precisa gerenciar o estado modal da janela pai.  
  
 Se a caixa de diálogo não for WPF, ou para algum outro motivo, você não pode derivar sua caixa de diálogo classe de <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>, em seguida, você deve obter o pai da caixa de diálogo chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.GetDialogOwnerHwnd%2A> e gerenciar o estado modal por conta própria, chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.EnableModeless%2A> método com um parâmetro de 0 (false) antes de exibir a caixa de diálogo e chamando o método novamente com um parâmetro de 1 (verdadeiro) depois de fechar a caixa de diálogo.  
  
## <a name="create-a-dialog-box-derived-from-dialogwindow"></a>Criar uma caixa de diálogo derivada de DialogWindow  
  
1.  Crie um projeto do VSIX chamado **OpenDialogTest** e adicione um comando de menu chamado **OpenDialog**. Para obter mais informações sobre como fazer isso, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
2.  Para usar o <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> classe, você deve adicionar referências aos assemblies a seguir (na guia estrutura do **adicionar referência** caixa de diálogo):  
  
    -   *PresentationCore*  
  
    -   *PresentationFramework*  
  
    -   *WindowsBase*  
  
    -   *System. XAML*  
  
3.  Na *OpenDialog.cs*, adicione o seguinte `using` instrução:  
  
    ```csharp  
    using Microsoft.VisualStudio.PlatformUI;  
    ```  
  
4.  Declare uma classe chamada `TestDialogWindow` que deriva de <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>:  
  
    ```csharp  
    class TestDialogWindow : DialogWindow  
    {. . .}  
    ```  
  
5.  Para poder minimizar e maximizar a caixa de diálogo, defina <xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMaximizeButton%2A> e <xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMinimizeButton%2A> como true:  
  
    ```csharp  
    internal TestDialogWindow()  
    {  
        this.HasMaximizeButton = true;  
        this.HasMinimizeButton = true;  
    }  
    ```  
  
6.  No `OpenDialog.ShowMessageBox` método, substitua o código existente pelo seguinte:  
  
    ```csharp  
    TestDialogWindow testDialog = new TestDialogWindow();  
    testDialog.ShowModal();  
    ```  
  
7.  Crie e execute o aplicativo. A instância experimental do Visual Studio deve aparecer. Sobre o **ferramentas** menu da instância experimental, você verá um comando chamado **OpenDialog invocar**. Quando você clica nesse comando, você deverá ver a janela de diálogo. Você deve ser capaz de minimizar e maximizar a janela.  
  
## <a name="create-and-manage-a-dialog-box-not-derived-from-dialogwindow"></a>Criar e gerenciar uma caixa de diálogo não derivada de DialogWindow  
  
1.  Para este procedimento, você pode usar o **OpenDialogTest** solução criada no procedimento anterior, com as mesmas referências de assembly.  
  
2.  Adicione o seguinte `using` declarações:  
  
    ```csharp  
    using System.Windows;  
    using Microsoft.Internal.VisualStudio.PlatformUI;  
    ```  
  
3.  Crie uma classe denominada `TestDialogWindow2` que deriva de <xref:System.Windows.Window>:  
  
    ```csharp  
    class TestDialogWindow2 : Window  
    {. . .}  
    ```  
  
4.  Adicione uma referência privada ao <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>:  
  
    ```  
    private IVsUIShell shell;  
    ```  
  
5.  Adicione um construtor que define a referência à <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>:  
  
    ```csharp  
    public TestDialogWindow2(IVsUIShell uiShell)  
    {  
        shell = uiShell;  
    }  
    ```  
  
6.  No `OpenDialog.ShowMessageBox` método, substitua o código existente pelo seguinte:  
  
    ```csharp  
    IVsUIShell uiShell = (IVsUIShell)ServiceProvider.GetService(typeof(SVsUIShell));  
  
    TestDialogWindow2 testDialog2 = new TestDialogWindow2(uiShell);  
    //get the owner of this dialog  
    IntPtr hwnd;  
    uiShell.GetDialogOwnerHwnd(out hwnd);  
    testDialog2.WindowStartupLocation = System.Windows.WindowStartupLocation.CenterOwner;  
    uiShell.EnableModeless(0);  
    try  
    {  
        WindowHelper.ShowModal(testDialog2, hwnd);  
    }  
    finally  
    {  
        // This will take place after the window is closed.  
        uiShell.EnableModeless(1);  
    }  
    ```  
  
7.  Crie e execute o aplicativo. Sobre o **ferramentas** menu, você verá um comando chamado **OpenDialog invocar**. Quando você clica nesse comando, você deverá ver a janela de diálogo.