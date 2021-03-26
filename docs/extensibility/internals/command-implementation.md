---
title: Implementação de comando | Microsoft Docs
description: Saiba mais sobre a implementação de comando no Visual Studio, como configurar um grupo de comandos em um VSPackage, adicionar um comando a ele, registrar o comando e implementá-lo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, implementation
ms.assetid: c782175c-cce4-4bd0-8374-4a897ceb1b3d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 93c99b131340d2e53b931619d4e5742d9e19f570
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091133"
---
# <a name="command-implementation"></a>Implementação de comando
Para implementar um comando em um VSPackage, você deve executar as seguintes tarefas:

1. No arquivo *. vsct* , configure um grupo de comandos e, em seguida, adicione o comando a ele. Para obter mais informações, consulte [arquivos de tabela de comando do Visual Studio (. vsct)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).

2. Registre o comando com o Visual Studio.

3. Implemente o comando.

As seções a seguir explicam como registrar e implementar comandos.

## <a name="register-commands-with-visual-studio"></a>Registrar comandos com o Visual Studio
 Se o comando for exibido em um menu, você deverá adicionar o <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> ao seu VSPackage e usar como um valor do nome do menu ou sua ID de recurso.

```
[ProvideMenuResource("Menus.ctmenu", 1)]
...
    public sealed class MyPackage : Package
    {.. ..}

```

 Além disso, você deve registrar o comando com o <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> . Você pode obter esse serviço usando o <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> método se seu VSPackage for derivado de <xref:Microsoft.VisualStudio.Shell.Package> .

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
 Há várias maneiras de implementar comandos. Se você quiser um comando de menu estático, que é um comando que sempre aparece da mesma maneira e no mesmo menu, crie o comando usando <xref:System.ComponentModel.Design.MenuCommand> conforme mostrado nos exemplos na seção anterior. Para criar um comando estático, você deve fornecer um manipulador de eventos responsável pela execução do comando. Como o comando está sempre habilitado e visível, você não precisa fornecer seu status para o Visual Studio. Se você quiser alterar o status de um comando dependendo de determinadas condições, poderá criar o comando como uma instância da <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> classe e, em seu construtor, fornecer um manipulador de eventos para executar o comando e um `QueryStatus` manipulador para notificar o Visual Studio quando o status do comando for alterado. Você também pode implementar <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> como parte de uma classe de comando ou pode implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> se estiver fornecendo um comando como parte de um projeto. As duas interfaces e a <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> classe têm métodos que notificam o Visual Studio de uma alteração no status de um comando e outros métodos que fornecem a execução do comando.

 Quando um comando é adicionado ao serviço de comando, ele se torna um de uma cadeia de comandos. Ao implementar a notificação de status e os métodos de execução para o comando, tome cuidado para fornecer somente para esse comando específico e para passar todos os outros casos para os outros comandos na cadeia. Se você não passar o comando (normalmente, retornando <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> ), o Visual Studio poderá parar de funcionar corretamente.

## <a name="querystatus-methods"></a>Métodos QueryStatus
 Se você estiver implementando o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método ou o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> método, verifique o GUID do conjunto de comandos ao qual o comando pertence e a ID do comando. Siga estas diretrizes:

- Se o GUID não for reconhecido, a implementação de um dos métodos deverá retornar <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_UNKNOWNGROUP> .

- Se a implementação de um dos métodos reconhecer o GUID, mas não tiver implementado o comando, o método deverá retornar <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> .

- Se a implementação de um dos métodos reconhecer o GUID e o comando, o método deverá definir o campo de sinalizadores de comando de cada comando (no `prgCmds` parâmetro) usando os seguintes <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> sinalizadores:

  - `OLECMDF_SUPPORTED`: Há suporte para o comando.

  - `OLECMDF_INVISIBLE`: O comando não deve estar visível.

  - `OLECMDF_LATCHED`: O comando é alternado e parece ter sido verificado.

  - `OLECMDF_ENABLED`: O comando está habilitado.

  - `OLECMDF_DEFHIDEONCTXTMENU`: O comando deverá ficar oculto se aparecer em um menu de atalho.

  - `OLECMDF_NINCHED`: O comando é um controlador de menu e não está habilitado, mas sua lista suspensa de menus não está vazia e ainda está disponível. (Esse sinalizador raramente é usado.)

- Se o comando tiver sido definido no arquivo *. vsct* com o `TextChanges` sinalizador, defina os seguintes parâmetros:

  - Defina o `rgwz` elemento do `pCmdText` parâmetro para o novo texto do comando.

  - Defina o `cwActual` elemento do `pCmdText` parâmetro como o tamanho da cadeia de caracteres de comando.

Além disso, certifique-se de que o contexto atual não seja uma função de automação, a menos que o comando seja especificamente destinado a lidar com funções de automação.

Para indicar que você dá suporte a um comando específico, retorne <xref:Microsoft.VisualStudio.VSConstants.S_OK> . Para todos os outros comandos, retorne <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> .

No exemplo a seguir, o `QueryStatus` método primeiro verifica se o contexto não é uma função de automação e localiza o GUID do conjunto de comandos correto e a ID do comando. O próprio comando é definido como habilitado e com suporte. Não há suporte para nenhum outro comando.

```csharp
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
 A implementação do `Exec` método é semelhante à implementação do `QueryStatus` método. Primeiro, verifique se o contexto não é uma função de automação. Em seguida, teste o GUID e a ID do comando. Se o GUID ou a ID do comando não for reconhecido, retorne <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> .

 Para manipular o comando, execute-o e retorne <xref:Microsoft.VisualStudio.VSConstants.S_OK> se a execução for realizada com sucesso. O comando é responsável pela detecção e notificação de erros; Portanto, retorne um código de erro se a execução falhar. O exemplo a seguir demonstra como o método de execução deve ser implementado.

```csharp
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

## <a name="see-also"></a>Confira também

- [Como VSPackages adicionar elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
