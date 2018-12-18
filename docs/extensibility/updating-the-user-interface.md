---
title: Atualizando a Interface do usuário | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, updating
- commands, updating UI
ms.assetid: 376e2f56-e7bf-4e62-89f5-3dada84a404b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 6b3bc8c4b87aefe62cbd27e64fc426ddb7abf96e
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31139150"
---
# <a name="updating-the-user-interface"></a>Atualizando a Interface do usuário
Depois de implementar um comando, você pode adicionar código para atualizar a interface do usuário com o estado dos seus comandos de novo.  
  
 Em um aplicativo típico do Win32, o conjunto de comandos pode ser controlado continuamente e o estado de comandos individuais pode ser ajustado como o usuário vê-los. No entanto, como o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] shell pode hospedar um número ilimitado de VSPackages, ampla sondagem pode diminuir a capacidade de resposta, especialmente de sondagem em assemblies de interoperabilidade entre código gerenciado e COM.  
  
### <a name="to-update-the-ui"></a>Para atualizar a interface do usuário  
  
1.  Execute uma das seguintes etapas:  
  
    -   Chame o método <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A>.  
  
         Um <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> interface pode ser obtida o <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> de serviço, da seguinte maneira.  
  
        ```csharp  
        void UpdateUI(Microsoft.VisualStudio.Shell.ServiceProvider sp)  
        {  
            IVsUIShell vsShell = (IVsUIShell)sp.GetService(typeof(IVsUIShell));  
            if (vsShell != null)  
            {  
                int hr = vsShell.UpdateCommandUI(0);  
                Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(hr);  
            }  
        }  
  
        ```  
  
         Se o parâmetro do <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> é diferente de zero (`TRUE`), a atualização será executada de forma síncrona e imediatamente. É recomendável que você passe zero (`FALSE`) para esse parâmetro ajudar a manter o bom desempenho. Se você quiser evitar o cache, aplicar o `DontCache` sinalizador ao criar o comando no arquivo. VSCT. No entanto, use o sinalizador com cuidado, ou pode diminuir o desempenho. Para obter mais informações sobre sinalizadores de comando, consulte o [comando sinalizador elemento](../extensibility/command-flag-element.md) documentação.  
  
    -   Em VSPackages que hospedam um controle ActiveX usando o modelo de ativação no local em uma janela, pode ser mais conveniente usar o <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A> método. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> método no <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> interface e o <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A> método o <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> interface são funcionalmente equivalentes. Ambos fazem com que o ambiente para o estado de todos os comandos de consulta novamente. Normalmente, uma atualização não é executada imediatamente. Em vez disso, uma atualização é atrasada até o tempo ocioso. O shell armazena em cache o estado do comando para ajudar a manter o bom desempenho. Se você quiser evitar o cache, aplicar o `DontCache` sinalizador ao criar o comando no arquivo. VSCT. No entanto, use o sinalizador com cuidado porque pode diminuir o desempenho.  
  
         Observe que você pode obter o <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> interface chamando o `QueryInterface` método em um <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager> do objeto ou por obter a interface do <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> service.  
  
## <a name="see-also"></a>Consulte também  
 [Como VSPackages adicionar elementos da Interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [Implementação](../extensibility/internals/command-implementation.md)