---
title: Criando uma janela de ferramentas de várias instâncias | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- multi
- tool windows
ms.assetid: 4a7872f1-acc9-4f43-8932-5a526b36adea
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1bb84ed9961cac5159e15bc0c45fada5426d2f2c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904061"
---
# <a name="create-a-multi-instance-tool-window"></a>Criar uma janela de ferramentas de várias instâncias
Você pode programar uma janela de ferramentas para que várias instâncias dela possam ser abertas simultaneamente. Por padrão, as janelas de ferramentas podem ter apenas uma instância aberta.

Ao usar uma janela de ferramenta de várias instâncias, você pode mostrar várias fontes de informações relacionadas ao mesmo tempo. Por exemplo, você pode colocar um <xref:System.Windows.Forms.TextBox> controle de várias linhas em uma janela de ferramenta de várias instâncias para que vários trechos de código estejam simultaneamente disponíveis durante uma sessão de programação. Além disso, por exemplo, você pode colocar um <xref:System.Windows.Forms.DataGrid> controle e uma caixa de listagem suspensa em uma janela de ferramentas de várias instâncias para que várias fontes de dados em tempo real possam ser controladas simultaneamente.

## <a name="create-a-basic-single-instance-tool-window"></a>Criar uma janela de ferramentas básica (instância única)

1. Crie um projeto chamado **MultiInstanceToolWindow** usando o modelo VSIX e adicione um modelo de item de janela de ferramenta personalizada chamado **MIToolWindow**.

    > [!NOTE]
    > Para obter mais informações sobre como criar uma extensão com uma janela de ferramentas, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).

## <a name="make-a-tool-window-multi-instance"></a>Criar uma janela de ferramentas com várias instâncias

1. Abra o arquivo *MIToolWindowPackage.cs* e localize o `ProvideToolWindow` atributo. e o `MultiInstances=true` parâmetro, conforme mostrado no exemplo a seguir:

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
        [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
        [ProvideMenuResource("Menus.ctmenu", 1)]
        [ProvideToolWindow(typeof(MultiInstanceToolWindow.MIToolWindow), MultiInstances = true)]
        [Guid(MIToolWindowPackage.PackageGuidString)]
        public sealed class MIToolWindowPackage : Package
    {. . .}
    ```

2. No arquivo *MIToolWindowCommand.cs* , localize o `ShowToolWindos()` método. Nesse método, chame o <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> método e defina seu `create` sinalizador como para `false` que ele seja iterado por meio das instâncias da janela de ferramentas existentes até que uma disponível `id` seja encontrada.

3. Para criar uma instância de janela de ferramenta, chame o <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> método e defina seu `id` como um valor disponível e seu `create` sinalizador como `true` .

    Por padrão, o valor do `id` parâmetro do <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> método é `0` . Esse valor faz uma janela de ferramenta de instância única. Para que mais de uma instância seja hospedada, cada instância deve ter seu próprio exclusivo `id` .

4. Chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> método no <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> objeto que é retornado pela <xref:Microsoft.VisualStudio.Shell.ToolWindowPane.Frame%2A> propriedade da instância da janela de ferramentas.

5. Por padrão, o `ShowToolWindow` método criado pelo modelo de item da janela de ferramentas cria uma janela de ferramenta de instância única. O exemplo a seguir mostra como modificar o `ShowToolWindow` método para criar várias instâncias.

    ```csharp
    private void ShowToolWindow(object sender, EventArgs e)
    {
        for (int i = 0; i < 10; i++)
        {
            ToolWindowPane window = this.package.FindToolWindow(typeof(MIToolWindow), i, false);
            if (window == null)
            {
                // Create the window with the first free ID.
                window = (ToolWindowPane)this.package.FindToolWindow(typeof(MIToolWindow), i, true);
                if ((null == window) || (null == window.Frame))
                {
                    throw new NotSupportedException("Cannot create tool window");
                }

            IVsWindowFrame windowFrame = (IVsWindowFrame)window.Frame;
            Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(windowFrame.Show());
            break;
            }
        }
    }
    ```
