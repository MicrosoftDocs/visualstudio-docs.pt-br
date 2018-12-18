---
title: Criação de uma janela de ferramentas de várias instâncias | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- multi
- tool windows
ms.assetid: 4a7872f1-acc9-4f43-8932-5a526b36adea
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 19a41e172fd68687cffeca91bdfb4bc418ecdf60
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39499761"
---
# <a name="create-a-multi-instance-tool-window"></a>Criar uma janela de ferramentas de várias instâncias
Você pode programar uma janela de ferramentas para que várias instâncias dele podem ser abertas simultaneamente. Por padrão, janelas de ferramenta podem ter apenas uma instância abertos.  
  
 Quando você usa uma janela de ferramentas de várias instâncias, você pode mostrar várias origens relacionadas de informações ao mesmo tempo. Por exemplo, você pode colocar uma multilinha <xref:System.Windows.Forms.TextBox> controle em uma janela de ferramenta com várias instâncias para que vários trechos de código estão disponíveis ao mesmo tempo durante uma sessão de programação. Além disso, por exemplo, você pode colocar um <xref:System.Windows.Forms.DataGrid> controle e uma lista suspensa caixa em uma janela de ferramenta com várias instâncias para que várias fontes de dados em tempo real podem ser rastreadas simultaneamente.  
  
## <a name="create-a-basic-single-instance-tool-window"></a>Criar uma janela de ferramentas de básico (instância única)  
  
1.  Crie um projeto chamado **MultiInstanceToolWindow** usando o modelo VSIX e adicionar um modelo de item da janela de ferramenta personalizada denominado **MIToolWindow**.  
  
    > [!NOTE]
    >  Para obter mais informações sobre como criar uma extensão com uma janela de ferramentas, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).  
  
## <a name="make-a-tool-window-multi-instance"></a>Tornar uma instância de vários de janela de ferramenta  
  
1.  Abra o *MIToolWindowPackage.cs* do arquivo e encontre o `ProvideToolWindow` atributo. e o `MultiInstances=true` parâmetro, conforme mostrado no exemplo a seguir:  
  
    ```csharp  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
        [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About  
        [ProvideMenuResource("Menus.ctmenu", 1)]  
        [ProvideToolWindow(typeof(MultiInstanceToolWindow.MIToolWindow), MultiInstances = true)]  
        [Guid(MIToolWindowPackage.PackageGuidString)]  
        public sealed class MIToolWindowPackage : Package  
    {. . .}  
    ```  
  
2.  No *MIToolWindowCommand.cs* do arquivo, localize o `ShowToolWindos()` método. Nesse método, chame o <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> método e defina seu `create` sinalizador como `false` , de modo que ele irá iterar através de instâncias existentes de janela de ferramenta até uma disponível `id` for encontrado.  
  
3.  Para criar uma instância de janela da ferramenta, chame o <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> método e defina seu `id` um valor disponível e seu `create` sinalizador como `true`.  
  
     Por padrão, o valor da `id` parâmetro do <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> método é `0`. Esse valor faz com que uma janela de ferramentas de instância única. Para mais de uma instância a ser hospedado, cada instância deve ter seu próprio exclusivo `id`.  
  
4.  Chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> método na <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> objeto que é retornado pelo <xref:Microsoft.VisualStudio.Shell.ToolWindowPane.Frame%2A> propriedade da instância de janela de ferramenta.  
  
5.  Por padrão, o `ShowToolWindow` método que é criado pelo modelo de item da janela de ferramenta cria uma janela de ferramentas de instância única. O exemplo a seguir mostra como modificar o `ShowToolWindow` método para criar várias instâncias.  
  
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