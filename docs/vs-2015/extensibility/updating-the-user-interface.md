---
title: Atualizando a Interface do usuário | Microsoft Docs
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
- user interfaces, updating
- commands, updating UI
ms.assetid: 376e2f56-e7bf-4e62-89f5-3dada84a404b
caps.latest.revision: 42
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e4e6b282ac58e523e8a2047e7f882d90b9f202bf
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51765549"
---
# <a name="updating-the-user-interface"></a>Atualizando a interface do usuário
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Depois de implementar um comando, você pode adicionar código para atualizar a interface do usuário com o estado de seus novos comandos.  
  
 Em um aplicativo típico do Win32, o conjunto de comandos pode ser sondado continuamente e o estado de comandos individuais pode ser ajustado conforme o usuário vê-los. No entanto, porque o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] shell pode hospedar um número ilimitado de VSPackages, sondagem extenso pode diminuir a capacidade de resposta, especialmente de sondagem em assemblies de interoperabilidade entre código gerenciado e COM.  
  
### <a name="to-update-the-ui"></a>Para atualizar a interface do usuário  
  
1.  Execute uma das seguintes etapas:  
  
    -   Chame o método <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A>.  
  
         Uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> interface pode ser obtido o <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> de serviço, da seguinte maneira.  
  
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
  
         Se o parâmetro do <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> for diferente de zero (`TRUE`), em seguida, a atualização é executada de forma síncrona e imediatamente. É recomendável que você passe zero (`FALSE`) para esse parâmetro ajudar a manter um bom desempenho. Se você quiser evitar o armazenamento em cache, aplique o `DontCache` sinalizador quando você cria o comando no arquivo. VSCT. No entanto, use o sinalizador com cuidado, ou pode diminuir o desempenho. Para obter mais informações sobre os sinalizadores de comando, consulte o [elemento Command Flag](../extensibility/command-flag-element.md) documentação.  
  
    -   Em VSPackages que hospedam um controle ActiveX por meio do modelo de ativação no local em uma janela, pode ser mais conveniente usar o <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A> método. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> método na <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> interface e o <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A> método no <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> interface são funcionalmente equivalentes. Ambos fazem com que o ambiente consultar novamente o estado de todos os comandos. Normalmente, uma atualização não é executada imediatamente. Em vez disso, uma atualização é atrasada até o tempo ocioso. O shell armazena em cache o estado do comando para ajudar a manter um bom desempenho. Se você quiser evitar o armazenamento em cache, aplique o `DontCache` sinalizador quando você cria o comando no arquivo. VSCT. No entanto, use o sinalizador com cuidado porque pode diminuir o desempenho.  
  
         Observe que você pode obter o <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> interface chamando o `QueryInterface` método em um <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager> do objeto ou por Obtendo a interface do <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> service.  
  
## <a name="see-also"></a>Consulte também  
 [Como os VSPackages adicionam elementos da Interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [Implementação](../extensibility/internals/command-implementation.md)

