---
title: Implementação de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, implementation
ms.assetid: c782175c-cce4-4bd0-8374-4a897ceb1b3d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8f002e660b2c3b745e4a7ea67f715b613b96bd0a
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39510433"
---
# <a name="command-implementation"></a>Implementação do comando
Para implementar um comando em um VSPackage, você deve executar as seguintes tarefas:  
  
1.  No *VSCT* de arquivos, configure um grupo de comando e, em seguida, adicione o comando a ele. Para obter mais informações, consulte [arquivos de tabela (. VSCT) de comando do Visual Studio](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).
  
2.  Registre o comando com o Visual Studio.  
  
3.  Implemente o comando.  
    
As seções a seguir explicam como registrar e implementar comandos.  
  
## <a name="register-commands-with-visual-studio"></a>Registre-se comandos com o Visual Studio  
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
  
## <a name="implement-commands"></a>Implementar comandos  
 Há várias maneiras de implementar comandos. Se você quiser que um comando de menu estático, que é um comando que aparece sempre o mesmo propósito e no mesmo menu, criar o comando usando <xref:System.ComponentModel.Design.MenuCommand> conforme mostrado nos exemplos na seção anterior. Para criar um comando estático, você deve fornecer um manipulador de eventos é responsável por executar o comando. Como o comando está sempre visível e habilitado, você não precisa fornecer seu status para o Visual Studio. Se você quiser alterar o status de um comando, dependendo de determinadas condições, você pode criar o comando como uma instância das <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> de classe e, em seu construtor, forneça um manipulador de eventos para executar o comando e um `QueryStatus` manipulador para notificar o Visual Studio quando muda o status do comando. Você também pode implementar <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> como parte de uma classe de comando ou, você pode implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> se você estiver fornecendo um comando como parte de um projeto. As duas interfaces e o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> classe todos têm métodos que notificam o Visual Studio de uma alteração no status de um comando e outros métodos que fornecem a execução do comando.  
  
 Quando um comando é adicionado ao serviço de comando, ele se torna um de uma cadeia de comandos. Quando você implementa os métodos de notificação e a execução de status para o comando, tome cuidado para fornecer apenas para esse comando específico e passar todos os outros casos para os outros comandos na cadeia. Se você não passar o comando (geralmente retornando <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>), Visual Studio podem parar de funcionar corretamente.  
  
## <a name="querystatus-methods"></a>Métodos de QueryStatus  
 Se você estiver implementando um os <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método ou o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> método, verificar se o GUID do comando conjunto ao qual pertence o comando e a ID do comando. Siga estas diretrizes:  
  
-   Se o GUID não for reconhecido, sua implementação de qualquer um dos métodos deve retornar <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_UNKNOWNGROUP>.  
  
-   Se sua implementação de qualquer um dos métodos reconhece o GUID, mas não implementou o comando, então o método deverá retornar <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>.  
  
-   Se sua implementação de qualquer um dos métodos reconhece o GUID e o comando e, em seguida, o método deve definir o campo de sinalizadores de comando de cada comando (na `prgCmds` parâmetro) usando os seguintes <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> sinalizadores:  
  
    -   `OLECMDF_SUPPORTED`: O comando é suportado.  
  
    -   `OLECMDF_INVISIBLE`: O comando não deve estar visível.  
  
    -   `OLECMDF_LATCHED`: O comando é ativado e parece ter sido marcada.  
  
    -   `OLECMDF_ENABLED`: O comando é habilitado.  
  
    -   `OLECMDF_DEFHIDEONCTXTMENU`: O comando deve ser ocultado, se ele for exibido em um menu de atalho.  
  
    -   `OLECMDF_NINCHED`: O comando é um controlador de menu e não está habilitado, mas sua lista do menu suspenso não está vazia e ainda está disponível. (Esse sinalizador é raramente usado.)  
  
-   Se o comando tiver sido definido na *. VSCT* do arquivo com o `TextChanges` sinalizador, defina os seguintes parâmetros:  
  
    -   Defina as `rgwz` elemento do `pCmdText` parâmetro para o novo texto do comando.  
  
    -   Defina as `cwActual` elemento do `pCmdText` parâmetro para o tamanho da cadeia de caracteres de comando.  
  

Além disso, certifique-se de que o contexto atual não é uma função de automação, a menos que o comando é projetado especificamente para lidar com funções de automação.  
  
Para indicar que há suporte para um comando específico, retornar <xref:Microsoft.VisualStudio.VSConstants.S_OK>. Para todos os outros comandos, retornar <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>.  
  
No exemplo a seguir, o `QueryStatus` primeiro método torna-se de que o contexto não é uma função de automação e, em seguida, localiza o GUID do conjunto de comandos correto e a ID de comando. O comando em si é definido como habilitado e tem suporte. Não há suporte para nenhum outro comando.  
  
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
 Implementação do `Exec` método é semelhante a implementação do `QueryStatus` método. Primeiro, certifique-se de que o contexto não é uma função de automação. Em seguida, teste para o GUID e a ID de comando. Se o GUID ou o ID de comando não é reconhecida, retorne <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>.  
  
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