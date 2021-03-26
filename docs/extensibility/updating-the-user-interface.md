---
title: Atualizando a interface do usuário | Microsoft Docs
description: Saiba como adicionar código para atualizar a interface do usuário depois de implementar um novo comando em seu VSPackage.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, updating
- commands, updating UI
ms.assetid: 376e2f56-e7bf-4e62-89f5-3dada84a404b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e5aecf97683ff22b8c384acf1c8ffb83e671fa57
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073723"
---
# <a name="updating-the-user-interface"></a>Atualizando a interface do usuário
Depois de implementar um comando, você pode adicionar código para atualizar a interface do usuário com o estado dos novos comandos.

 Em um aplicativo Win32 típico, o conjunto de comandos pode ser sondado continuamente e o estado de comandos individuais pode ser ajustado conforme o usuário os exibe. No entanto, como o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] shell pode hospedar um número ilimitado de VSPackages, a sondagem extensiva pode diminuir a capacidade de resposta, especialmente sondando entre assemblies de interoperabilidade entre código gerenciado e com.

### <a name="to-update-the-ui"></a>Para atualizar a interface do usuário

1. Execute uma das seguintes etapas:

    - Chame o método <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> .

         Uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> interface pode ser obtida do <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> serviço, da seguinte maneira.

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

         Se o parâmetro de <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> for diferente de zero ( `TRUE` ), a atualização será executada de forma síncrona e imediata. Recomendamos que você passe zero ( `FALSE` ) para esse parâmetro para ajudar a manter um bom desempenho. Se você quiser evitar o cache, aplique o `DontCache` sinalizador ao criar o comando no arquivo. vsct. No entanto, use o sinalizador com cuidado ou o desempenho pode diminuir. Para obter mais informações sobre sinalizadores de comando, consulte a documentação do [elemento de sinalizador de comando](../extensibility/command-flag-element.md) .

    - No VSPackages que hospeda um controle ActiveX usando o modelo de ativação in-loco em uma janela, pode ser mais conveniente usar o <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A> método. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> método na <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> interface e o <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A> método na <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> interface são funcionalmente equivalentes. Ambos fazem com que o ambiente consulte novamente o estado de todos os comandos. Normalmente, uma atualização não é executada imediatamente. Em vez disso, uma atualização é atrasada até o tempo ocioso. O Shell armazena em cache o estado do comando para ajudar a manter um bom desempenho. Se você quiser evitar o cache, aplique o `DontCache` sinalizador ao criar o comando no arquivo. vsct. No entanto, use o sinalizador com cuidado porque o desempenho pode diminuir.

         Observe que você pode obter a <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> interface chamando o `QueryInterface` método em um <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager> objeto ou obtendo a interface do <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> serviço.

## <a name="see-also"></a>Confira também
- [Como os VSPackages adicionam elementos da interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Implementação](../extensibility/internals/command-implementation.md)
