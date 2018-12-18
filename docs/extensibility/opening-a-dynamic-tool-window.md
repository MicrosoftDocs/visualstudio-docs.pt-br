---
title: Abrindo uma janela de ferramenta dinâmica | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- tool windows, dynamic
ms.assetid: 21547ba7-6e81-44df-9277-265bf34f877a
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 9d37a72629dfb7c10eeb51bcd2317151447e9edd
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39636640"
---
# <a name="open-a-dynamic-tool-window"></a>Abra uma janela de ferramenta dinâmica
Janelas de ferramentas normalmente são abertas a partir de um comando em um menu ou um atalho de teclado equivalente. Às vezes, no entanto, talvez seja necessário uma janela de ferramenta abre sempre que um contexto de interface do usuário específico se aplica e é fechada quando o contexto de interface do usuário não se aplica. Esses tipos de janelas de ferramenta são chamados *dinâmica* ou *automaticamente visíveis*.  
  
> [!NOTE]
>  Para obter uma lista de contextos de interface do usuário predefinidas, consulte <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT>.  
  
 Se você deseja abrir uma janela de ferramenta dinâmica na inicialização e é possível que a criação falha, você deve implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx> da interface e testar as condições de falha no <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx.QueryShowTool%2A> método. Para o shell sabe que tem uma janela de ferramenta dinâmica que deve ser aberta na inicialização, você deve adicionar o `SupportsDynamicToolOwner` valor (definido como 1) em seu registro de pacote. Esse valor não é parte do padrão <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>, portanto, você deve criar um atributo personalizado para adicioná-lo. Para obter mais informações sobre atributos personalizados, consulte [usa um atributo de registro personalizado para registrar uma extensão](../extensibility/registering-and-unregistering-vspackages.md#using-a-custom-registration-attribute-to-register-an-extension).  
  
 Use <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> para abrir uma janela de ferramentas. A janela da ferramenta é criada, conforme necessário.  
  
> [!NOTE]
>  Uma janela de ferramenta dinâmica pode ser fechada pelo usuário. Se você quiser criar um comando de menu para que o usuário pode reabrir a janela da ferramenta, o comando de menu deve ser habilitado no mesmo contexto de interface do usuário que abre a janela de ferramentas e desabilitado caso contrário.  
  
## <a name="to-open-a-dynamic-tool-window"></a>Para abrir uma janela de ferramenta dinâmica  
  
1.  Crie um projeto do VSIX chamado **DynamicToolWindow** e adicione um modelo de item da janela de ferramenta denominado *DynamicWindowPane.cs*. Para obter mais informações, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).  
  
2.  No *DynamicWindowPanePackage.cs* arquivo, localize a declaração DynamicWindowPanePackage. Adicione a <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> e <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute> atributos para registrar a janela da ferramenta.  
  
    ```vb  
    [ProvideToolWindow(typeof(DynamicWindowPane)]  
    [ProvideToolWindowVisibility(typeof(DynamicWindowPane), VSConstants.UICONTEXT.SolutionExists_string)]  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About  
    [ProvideMenuResource("Menus.ctmenu", 1)]  
    [ProvideToolWindow(typeof(DynamicToolWindow.DynamicWindowPane))]  
    [Guid(DynamicWindowPanePackage.PackageGuidString)]  
    public sealed class DynamicWindowPanePackage : Package  
    {. . .}  
    ```  
  
     Os atributos acima Registre-se a janela de ferramenta chamada DynamicWindowPane como uma janela transitória que não é persistida quando o Visual Studio é fechado e reaberto. DynamicWindowPane é aberto sempre que <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_string> se aplica e fechado, caso contrário.  
  
3.  Compile o projeto e comece a depuração. A instância experimental deve aparecer. Você não verá a janela da ferramenta.  
  
4.  Abra um projeto na instância experimental. A janela da ferramenta deve aparecer.