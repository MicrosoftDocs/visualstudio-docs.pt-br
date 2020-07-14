---
title: Criando e gerenciando caixas de diálogo modais | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- dialog boxes, managing in Visual Studio
ms.assetid: 491bc0de-7dba-478c-a76b-923440e090f3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f2f4f296bb155bcde82235d962ae63c8fa4d41d7
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903781"
---
# <a name="create-and-manage-modal-dialog-boxes"></a>Criar e gerenciar caixas de diálogo modais
Ao criar uma caixa de diálogo modal dentro do Visual Studio, você deve verificar se a janela pai da caixa de diálogo está desabilitada enquanto a caixa de diálogo é exibida e reabilitar a janela pai depois que a caixa de diálogo é fechada. Se você não fizer isso, poderá receber o erro: *Microsoft Visual Studio não pode ser desligado porque uma caixa de diálogo modal está ativa. Feche a caixa de diálogo ativa e tente novamente.*

Há duas maneiras de fazer isso. A maneira recomendada, se você tiver uma caixa de diálogo do WPF, é derivá-la de <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> e, em seguida, chamar <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow.ShowModal%2A> para exibir a caixa de diálogo. Se você fizer isso, não será necessário gerenciar o estado modal da janela pai.

Se sua caixa de diálogo não for o WPF, ou por alguma outra razão pela qual você não pode derivar sua classe de caixa de diálogo <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> , você deve obter o pai da caixa de diálogo chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.GetDialogOwnerHwnd%2A> e gerenciando o estado modal por conta própria, chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.EnableModeless%2A> método com um parâmetro de 0 (false) antes de fechar a caixa de diálogo.

## <a name="create-a-dialog-box-derived-from-dialogwindow"></a>Criar uma caixa de diálogo derivada de DialogWindow

1. Crie um projeto VSIX chamado **OpenDialogTest** e adicione um comando de menu chamado **OpenDialog**. Para obter mais informações sobre como fazer isso, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).

2. Para usar a <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> classe, você deve adicionar referências aos seguintes assemblies (na guia estrutura da caixa de diálogo **Adicionar referência** ):

    - *PresentationCore*

    - *PresentationFramework*

    - *WindowsBase*

    - *System.Xaml*

3. No *OpenDialog.cs*, adicione a seguinte `using` instrução:

    ```csharp
    using Microsoft.VisualStudio.PlatformUI;
    ```

4. Declare uma classe chamada `TestDialogWindow` derivada de <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> :

    ```csharp
    class TestDialogWindow : DialogWindow
    {. . .}
    ```

5. Para poder minimizar e maximizar a caixa de diálogo, defina <xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMaximizeButton%2A> e <xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMinimizeButton%2A> como true:

    ```csharp
    internal TestDialogWindow()
    {
        this.HasMaximizeButton = true;
        this.HasMinimizeButton = true;
    }
    ```

6. No `OpenDialog.ShowMessageBox` método, substitua o código existente pelo seguinte:

    ```csharp
    TestDialogWindow testDialog = new TestDialogWindow();
    testDialog.ShowModal();
    ```

7. Criar e executar o aplicativo. A instância experimental do Visual Studio deve aparecer. No menu **ferramentas** da instância experimental, você deve ver um comando chamado **Invoke OpenDialog**. Ao clicar nesse comando, você deverá ver a janela da caixa de diálogo. Você deve ser capaz de minimizar e maximizar a janela.

## <a name="create-and-manage-a-dialog-box-not-derived-from-dialogwindow"></a>Criar e gerenciar uma caixa de diálogo não derivada de DialogWindow

1. Para este procedimento, você pode usar a solução **OpenDialogTest** que você criou no procedimento anterior, com as mesmas referências de assembly.

2. Adicione as seguintes `using` declarações:

    ```csharp
    using System.Windows;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    ```

3. Crie uma classe chamada `TestDialogWindow2` derivada de <xref:System.Windows.Window> :

    ```csharp
    class TestDialogWindow2 : Window
    {. . .}
    ```

4. Adicione uma referência privada a <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> :

    ```
    private IVsUIShell shell;
    ```

5. Adicione um construtor que define a referência a <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> :

    ```csharp
    public TestDialogWindow2(IVsUIShell uiShell)
    {
        shell = uiShell;
    }
    ```

6. No `OpenDialog.ShowMessageBox` método, substitua o código existente pelo seguinte:

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

7. Criar e executar o aplicativo. No menu **ferramentas** , você deverá ver um comando chamado **Invoke OpenDialog**. Ao clicar nesse comando, você deverá ver a janela da caixa de diálogo.
