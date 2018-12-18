---
title: Fornecendo uma janela de propriedades personalizadas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- property browsers, providing
- Properties window, providing your own
ms.assetid: 408dcdef-8ef9-4644-97d2-f311cd35824f
caps.latest.revision: 12
manager: douge
ms.openlocfilehash: 8b3aeae11e087b6a6bd662ed32564d93062426df
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49186271"
---
# <a name="providing-a-custom-properties-window"></a>Fornecendo uma janela de propriedades personalizadas
É possível fornecer seus próprios **propriedades** janela para um sistema de projeto determinado, em vez de ampliar a **propriedades** janela fornecida pelo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE). O cenário mais frequentemente encontrado é quando você mesmo implementa o objeto localizado no quadro de janela.  
  
 No caso de você implementa o objeto localizado no quadro de janela, mas ainda terá acesso a ele por outros meios, há várias maneiras de acessar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> interface conforme listado no último procedimento nesta página.  
  
### <a name="to-provide-your-properties-window"></a>Para fornecer sua janela de propriedades  
  
1.  Definir um GUID que representa sua **propriedades** implementação de janela.  
  
2.  No seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> implementação, use o <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> serviço muito ao seu **propriedades** janela como um serviço para o ambiente do Visual Studio.  
  
### <a name="to-call-your-properties-window"></a>Para chamar sua janela de propriedades  
  
1.  Chame o método <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane.SetSite%2A>.  
  
2.  `QueryService` para <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> do <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> passado para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane.SetSite%2A> método.  
  
3.  Obter <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> de <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> service.  
  
4.  Chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A> com o primeiro parâmetro definido como `SEID_PropertyBrowserSID` (tirados o <xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID> enumeração) e o terceiro parâmetro, `varValue`, que representa um formulário de cadeia de caracteres do GUID que representa seu **propriedades** janela. Fazer essa chamada somente uma vez na primeira criação do seu **propriedades** janela do documento. Após a chamada isso **propriedades** janela está associada com seu quadro de janela.  
  
### <a name="to-obtain-the-window-frame-object-when-you-are-not-the-implementer"></a>Para obter o objeto de quadro de janela quando você não o implementador  
  
-   Você pode `QueryService` para <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> partir <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> com o parâmetro `propid` definido como <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>.  
  
-   Você pode obter a janela do documento ativo chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A> por meio do serviço SVsMonitorSelection. Defina o parâmetro `elementid` à `SEID_WindowFrame`, retirado do <xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID> enumeração.  
  
## <a name="see-also"></a>Consulte também  
 [Estendendo propriedades](../extensibility/internals/extending-properties.md)   
 [Interfaces e campos da janela Propriedades](../extensibility/internals/properties-window-fields-and-interfaces.md)