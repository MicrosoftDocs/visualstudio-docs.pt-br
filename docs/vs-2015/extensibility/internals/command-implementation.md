---
title: Implementação de comando | Microsoft Docs
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
- commands, implementation
ms.assetid: c782175c-cce4-4bd0-8374-4a897ceb1b3d
caps.latest.revision: 25
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: be1bcecb740fb0c375d0f461639a8b0d5e40669a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51765197"
---
# <a name="command-implementation"></a>Implementação de comando
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Para implementar um comando em um VSPackage, você deve executar as seguintes tarefas:  
  
1. No arquivo. VSCT, configure um grupo de comandos e, em seguida, adicione o comando a ele. Para obter mais informações, consulte [tabela de comando do Visual Studio (. Arquivos VSCT)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)'  
  
2. Registre o comando com o Visual Studio.  
  
3. Implemente o comando.  
  
   As seções a seguir explicam como registrar e implementar comandos.  
  
## <a name="registering-commands-with-visual-studio"></a>Registrar comandos com o Visual Studio  
 Se o comando deve ser exibido em um menu, você deve adicionar o <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> para o VSPackage e use como um valor que o nome do menu ou sua ID de recurso.  
  
```  
[ProvideMenuResource("Menus.ctmenu", 1)]  
...  
    public sealed class MyPackage : Package  
    {.. ..}  
  
```  
  
 Além disso, você deve registrar o comando com o <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService>. Você pode obter esse serviço usando o <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> método se o VSPackage é derivado de <xref:Microsoft.VisualStudio.Shell.Package>.  
  
```  
OleMenuCommandService mcs = GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
if ( null != mcs )  
{  
    // Create the command for the menu item.  
    CommandID menuCommandID = new CommandID(guidCommandGroup, myCommandID);  
    MenuCommand menuItem = new MenuCommand(MenuItemCallback, menuCommandID );  
    mcs.AddCommand( menuItem );  
}  
  
```  
  
## <a name="implementing-commands"></a>Implementando comandos  
 Há várias maneiras de implementar comandos. Se você quiser que um comando de menu estático, que é um comando que aparece sempre o mesmo propósito e no mesmo menu, criar o comando usando <xref:System.ComponentModel.Design.MenuCommand> conforme mostrado nos exemplos na seção anterior. Para criar um comando estático, você deve fornecer um manipulador de eventos é responsável por executar o comando. Como o comando está sempre visível e habilitado, você não precisa fornecer seu status para o Visual Studio. Se você quiser alterar o status de um comando, dependendo de determinadas condições, você pode criar o comando como uma instância da <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> de classe e, em seu construtor, forneça um manipulador de eventos para executar o comando e um manipulador de status de consulta para notificar o Visual Studio quando muda o status do comando. Você também pode implementar <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> como parte de uma classe de comando ou, você pode implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> se você estiver fornecendo um comando como parte de um projeto. As duas interfaces e o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> classe todos têm métodos que notificam o Visual Studio de uma alteração no status de um comando e outros métodos que fornecem a execução do comando.  
  
 Quando um comando é adicionado ao serviço de comando, ele se torna um de uma cadeia de comandos. Quando você implementa os métodos de notificação e a execução de status para o comando, tome cuidado para fornecer apenas para esse comando específico e passar todos os outros casos para os outros comandos na cadeia. Se você não passar o comando (geralmente retornando <xref:Microsoft.VisualStudio.OLE.Interop.Constants>), Visual Studio podem parar de funcionar corretamente.  
  
## <a name="query-status-methods"></a>Métodos de Status de consulta  
 Se você estiver implementando um os <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método ou o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> método, verificar se o GUID do comando conjunto ao qual pertence o comando e a ID do comando. Siga estas diretrizes:  
  
- Se o GUID não for reconhecido, sua implementação de qualquer um dos métodos deve retornar <xref:Microsoft.VisualStudio.OLE.Interop.Constants>.  
  
- Se sua implementação de qualquer um dos métodos reconhece o GUID, mas não implementou, na verdade, o comando, então o método deverá retornar <xref:Microsoft.VisualStudio.OLE.Interop.Constants>.  
  
- Se sua implementação de qualquer um dos métodos reconhece o GUID e o comando e, em seguida, o método deve definir o campo de sinalizadores de comando de cada comando (no `prgCmds` parâmetro) usando os sinalizadores a seguir:  
  
  -   <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> Se o comando é suportado.  
  
  -   <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> Se o comando não deve ser visível.  
  
  -   <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> Se o comando é ativado e parece ter sido verificado.  
  
  -   <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> Se o comando é habilitado.  
  
  -   <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> Se o comando deve ser ocultado se ele for exibido em um menu de atalho.  
  
  -   <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> Se o comando é um controlador de menu e não está habilitado, mas sua lista do menu suspenso não está vazia e ainda está disponível. (Esse sinalizador é raramente usado.)  
  
- Se o comando foi definido no arquivo. VSCT com o `TextChanges` sinalizador, defina os seguintes parâmetros:  
  
  -   Defina as `rgwz` elemento do `pCmdText` parâmetro para o novo texto do comando.  
  
  -   Defina as `cwActual` elemento do `pCmdText` parâmetro para o tamanho da cadeia de caracteres de comando.  
  
  Certifique-se de que o contexto atual não é uma função de automação, também, a menos que o comando é projetado especificamente para lidar com funções de automação.  
  
  Para indicar que há suporte para um comando específico, retornar <xref:Microsoft.VisualStudio.VSConstants.S_OK>. Para todos os outros comandos, retornar <xref:Microsoft.VisualStudio.OLE.Interop.Constants>.  
  
  No exemplo a seguir, o método de status da consulta primeiro garante que o contexto não é uma função de automação e, em seguida, localiza o GUID do conjunto de comandos correto e a ID de comando. O comando em si é definido como habilitado e tem suporte. Não há suporte para nenhum outro comando.  
  
```  
public int QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)  
{  
    if (!VsShellUtilities.IsInAutomationFunction(m_provider.ServiceProvider))  
    {  
        if (pguidCmdGroup == VSConstants.VSStd2K && cCmds > 0)  
        {  
            // make the Right command visible   
            if ((uint)prgCmds[0].cmdID == (uint)VSConstants.VSStd2KCmdID.RIGHT)  
            {  
                prgCmds[0].cmdf = (int)Microsoft.VisualStudio.OLE.Interop.Constants.MSOCMDF_ENABLED | (int)Microsoft.VisualStudio.OLE.Interop.Constants.MSOCMDF_SUPPORTED;  
                return VSConstants.S_OK;  
            }  
        }  
        return Constants.OLECMDERR_E_NOTSUPPORTED;  
    }  
}  
  
```  
  
## <a name="execution-methods"></a>Métodos de execução  
 Implementação do método execute é semelhante a implementação do método de status da consulta. Primeiro, certifique-se de que o contexto não é uma função de automação. Em seguida, teste para o GUID e a ID de comando. Se o GUID ou o ID de comando não é reconhecida, retorne <xref:Microsoft.VisualStudio.OLE.Interop.Constants>.  
  
 Para lidar com o comando, executá-lo e retornar <xref:Microsoft.VisualStudio.VSConstants.S_OK> se a execução for bem-sucedida. O comando é responsável pela detecção de erro e notificação; Portanto, retorne um código de erro se a execução falhará. O exemplo a seguir demonstra como o método de execução deve ser implementado.  
  
```  
public int Exec(ref Guid pguidCmdGroup, uint nCmdID, uint nCmdexecopt, IntPtr pvaIn, IntPtr pvaOut)  
{  
    if (!VsShellUtilities.IsInAutomationFunction(m_provider.ServiceProvider))  
    {  
        if (pguidCmdGroup == VSConstants.GUID_VSStandardCommandSet97)  
        {  
             if (nCmdID ==(uint) uint)VSConstants.VSStd2KCmdID.RIGHT)  
            {  
                //execute the command  
                return VSConstants.S_OK;  
            }  
        }  
    }  
    return Constants.OLECMDERR_E_NOTSUPPORTED;  
}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

