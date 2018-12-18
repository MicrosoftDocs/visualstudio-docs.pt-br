---
title: Objetos de contexto de seleção | Microsoft Docs
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
- selection, tracking
- selection, context objects
ms.assetid: 7308ea8f-a42c-47e5-954e-7dee933dce7a
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: beaf1b9c67cdad3237d1ac48b4a8e464b0a203a7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51769406"
---
# <a name="selection-context-objects"></a>Objetos de contexto da seleção
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE) usa um objeto de contexto de seleção global para determinar o que deve ser exibido no IDE. Cada janela no IDE pode ter seu próprio objeto de contexto de seleção enviados por push para o contexto da seleção global. O IDE atualiza o contexto da seleção global com valores de uma janela quando essa janela tem o foco. Para obter mais informações, consulte [comentários ao usuário](../../extensibility/internals/feedback-to-the-user.md).  
  
 Cada site no IDE ou o quadro de janela tem um serviço chamado <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>. O objeto criado pelo VSPackage que é localizado no quadro de janela deve chamar o `QueryService` método para obter um ponteiro para o <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> interface.  
  
 Janelas de quadro podem manter as partes de suas informações de contexto de seleção sejam propagadas para o contexto da seleção global quando eles são iniciados. Essa capacidade é útil para janelas de ferramenta que pode ser necessário iniciar com uma seleção vazia.  
  
 Modificando os seleção global contexto aciona eventos que monitora a VSPackages. Os VSPackages pode executar as seguintes tarefas com a implementação `IVsTrackSelectionEx` e <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> interfaces:  
  
- Atualize o arquivo ativo no momento em uma hierarquia.  
  
- Monitorar as alterações a determinados tipos de elementos. Por exemplo, se o VSPackage usa um especial **propriedades** janela, você pode monitorar as alterações no active **propriedades** janela e reinicie sua quando necessário.  
  
  A sequência a seguir mostra o curso típico de acompanhamento da seleção.  
  
1.  Recupera o contexto da seleção da janela recém-aberta o IDE e o coloca no contexto global de seleção. Se o contexto da seleção usa HIERARCHY_DONTPROPAGATE ou SELCONTAINER_DONTPROPAGATE, essa informação não é propagada para o contexto global. Para obter mais informações, consulte [comentários ao usuário](../../extensibility/internals/feedback-to-the-user.md).  
  
2.  Eventos de notificação forem transmitidos para qualquer VSPackage que solicitou.  
  
3.  O VSPackage atua nos eventos que ele recebe ao executar atividades como a atualização de uma hierarquia, reativando uma ferramenta ou outras tarefas semelhantes.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>   
 [Hierarquias no Visual Studio](../../extensibility/internals/hierarchies-in-visual-studio.md)   
 [Seleção e moeda no IDE](../../extensibility/internals/selection-and-currency-in-the-ide.md)   
 [Tipos de projeto](../../extensibility/internals/project-types.md)

