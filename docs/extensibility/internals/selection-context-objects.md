---
title: Objetos de contexto de seleção | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- selection, tracking
- selection, context objects
ms.assetid: 7308ea8f-a42c-47e5-954e-7dee933dce7a
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: f09bcb260f4edd09045f860ed08d951622e54a5d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49913157"
---
# <a name="selection-context-objects"></a>Objetos de contexto da seleção
O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o ambiente de desenvolvimento integrado (IDE) usa um objeto de contexto de seleção global para determinar o que deve ser exibido no IDE. Cada janela no IDE pode ter seu próprio objeto de contexto de seleção enviados por push para o contexto da seleção global. O IDE atualiza o contexto da seleção global com valores de uma janela quando essa janela tem o foco. Para obter mais informações, consulte [comentários ao usuário](../../extensibility/internals/feedback-to-the-user.md).  
  
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