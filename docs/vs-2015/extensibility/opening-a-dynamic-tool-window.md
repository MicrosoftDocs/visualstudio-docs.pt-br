---
title: Abrindo uma janela de ferramenta dinâmica | Microsoft Docs
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
- tool windows, dynamic
ms.assetid: 21547ba7-6e81-44df-9277-265bf34f877a
caps.latest.revision: 22
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 073e8a2e7ff13dad0e413aa47b7875260f612cd2
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51773789"
---
# <a name="opening-a-dynamic-tool-window"></a>Abrindo uma janela de ferramentas dinâmica
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Janelas de ferramentas normalmente são abertas a partir de um comando em um menu ou um atalho de teclado equivalente. Às vezes, no entanto, talvez seja necessário uma janela de ferramenta abre sempre que um contexto de interface do usuário específico se aplica e é fechada quando o contexto de interface do usuário não se aplica. Janelas de ferramentas como esses são chamadas *dinâmica* ou *automaticamente visíveis*.  
  
> [!NOTE]
>  Para obter uma lista de contextos de interface do usuário predefinidas, consulte <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT>. Para o  
  
 Se você deseja abrir uma janela de ferramenta dinâmica na inicialização e é possível que a criação falha, você deve implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx> da interface e testar as condições de falha no <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx.QueryShowTool%2A> método. Para o shell sabe que tem uma janela de ferramenta dinâmica que deve ser aberta na inicialização, você deve adicionar o `SupportsDynamicToolOwner` valor (definido como 1) em seu registro de pacote. Esse valor não é parte do padrão <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>, portanto, você deve criar um atributo personalizado para adicioná-lo. Para obter mais informações sobre atributos personalizados, consulte [usando um atributo personalizado de registro para registrar uma extensão](../misc/using-a-custom-registration-attribute-to-register-an-extension.md).  
  
 Use <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> para abrir uma janela de ferramentas. A janela da ferramenta é criada, conforme necessário.  
  
> [!NOTE]
>  Uma janela de ferramenta dinâmica pode ser fechada pelo usuário. Se você quiser criar um comando de menu para que o usuário pode reabrir a janela da ferramenta, o comando de menu deve ser habilitado no mesmo contexto de interface do usuário que abre a janela de ferramentas e desabilitado caso contrário.  
  
### <a name="to-open-a-dynamic-tool-window"></a>Para abrir uma janela de ferramenta dinâmica  
  
1.  Crie um projeto do VSIX chamado **DynamicToolWindow** e adicione um modelo de item da janela de ferramenta denominado **DynamicWindowPane.cs**. Para obter mais informações, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).  
  
2.  No arquivo DynamicWindowPanePackage.cs, localize a declaração DynamicWindowPanePackage. Adicionar o <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> T:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute atributos e para registrar a janela da ferramenta.  
  
    ```vb  
    [[ProvideToolWindow(typeof(DynamicWindowPane)]  
    [ProvideToolWindowVisibility(typeof(DynamicWindowPane), VSConstants.UICONTEXT.SolutionExists_string)]  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About  
    [ProvideMenuResource("Menus.ctmenu", 1)]  
    [ProvideToolWindow(typeof(DynamicToolWindow.DynamicWindowPane))]  
    [Guid(DynamicWindowPanePackageGuids.PackageGuidString)]  
    public sealed class DynamicWindowPanePackage : Package  
    {. . .}  
    ```  
  
     Isso registra a janela de ferramenta chamada DynamicWindowPane como uma janela transitória que não é persistida quando o Visual Studio é fechado e reaberto. DynamicWindowPane é aberto sempre que <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_string> se aplica e fechado, caso contrário.  
  
3.  Compile o projeto e comece a depuração. A instância experimental deve aparecer. Você não verá a janela da ferramenta.  
  
4.  Abra um projeto na instância experimental. A janela da ferramenta deve aparecer.

