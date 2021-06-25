---
title: Objetos de contexto de seleção | Microsoft Docs
description: Saiba mais sobre os internos de como o Visual Studio IDE usa um objeto de contexto de seleção global para determinar o que deve ser exibido no IDE.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- selection, tracking
- selection, context objects
ms.assetid: 7308ea8f-a42c-47e5-954e-7dee933dce7a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b0c97108eaba426a4def4c1052d3adc7348eb88b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898481"
---
# <a name="selection-context-objects"></a>Objetos de contexto da seleção
O IDE (ambiente de desenvolvimento integrado) usa um objeto de contexto de seleção global para determinar o que deve ser [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] exibido no IDE. Cada janela no IDE pode ter seu próprio objeto de contexto de seleção para o contexto de seleção global. O IDE atualiza o contexto de seleção global com valores de uma janela quando essa janela tem o foco. Para obter mais informações, [consulte Comentários para o usuário.](../../extensibility/internals/feedback-to-the-user.md)

 Cada quadro de janela ou site no IDE tem um serviço chamado <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> . O objeto criado pelo VSPackage que está no quadro da janela deve chamar o método para obter `QueryService` um ponteiro para a <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> interface.

 As janelas de quadro podem impedir que partes de suas informações de contexto de seleção sejam propagadas para o contexto de seleção global quando elas são iniciadas. Essa capacidade é útil para janelas de ferramentas que podem ter que começar com uma seleção vazia.

 Modificar o contexto de seleção global dispara eventos que o VSPackages pode monitorar. O VSPackages pode executar as seguintes tarefas implementando `IVsTrackSelectionEx` <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> interfaces e :

- Atualize o arquivo ativo no momento em uma hierarquia.

- Monitore as alterações em determinados tipos de elementos. Por exemplo, se o VSPackage usar uma janela Propriedades  especial, você poderá monitorar as alterações na janela Propriedades ativas e reiniciar a sua quando necessário. 

  A sequência a seguir mostra o curso típico do acompanhamento de seleção.

1. O IDE recupera o contexto de seleção da janela recém-aberta e o coloca no contexto de seleção global. Se o contexto de seleção usar HIERARCHY_DONTPROPAGATE ou SELCONTAINER_DONTPROPAGATE, essas informações não serão propagadas para o contexto global. Para obter mais informações, [consulte Comentários para o usuário.](../../extensibility/internals/feedback-to-the-user.md)

2. Os eventos de notificação são transmitidos para qualquer VSPackage que os solicitou.

3. O VSPackage atua nos eventos recebidos executando atividades como atualizar uma hierarquia, reativar uma ferramenta ou outras tarefas semelhantes.

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>
- [Hierarquias no Visual Studio](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [Seleção e moeda no IDE](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [Tipos de Projeto](../../extensibility/internals/project-types.md)
