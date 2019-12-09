---
title: Conclusão de instrução em um serviço de linguagem herdada | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- statement completion
- language services, statement completion
ms.assetid: 617439dc-3f0e-4e5f-b346-3e4e7fcf3c1b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d4c813052892c21a6a3e04560452b503205df117
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72723229"
---
# <a name="statement-completion-in-a-legacy-language-service"></a>Preenchimento de declaração em um serviço de linguagem herdado
A conclusão da instrução é o processo pelo qual o serviço de idioma ajuda os usuários a concluir uma palavra-chave ou um elemento de linguagem que eles começaram a digitar no editor principal. Este tópico discute como a conclusão da instrução funciona e como implementá-la em seu serviço de idioma.

 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para saber mais sobre a nova maneira de implementar a conclusão da instrução, consulte [passo a passos: exibindo a conclusão da instrução](../../extensibility/walkthrough-displaying-statement-completion.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

## <a name="implementing-statement-completion"></a>Implementando a conclusão da instrução
 No editor principal, a conclusão da instrução ativa uma interface do usuário especial que o ajuda a escrever código de maneira interativa e mais fácil e rápida. A conclusão da instrução ajuda exibindo objetos ou classes pertinentes quando eles são necessários, o que evita que você precise se lembrar de elementos específicos ou ter que procurar em um tópico de referência de ajuda.

 Para implementar a conclusão da instrução, seu idioma deve ter um gatilho de conclusão de instrução, que pode ser analisado. Por exemplo, [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] usa um operador de ponto (.), enquanto [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] usa um operador de seta (->). Um serviço de linguagem pode usar mais de um gatilho para iniciar a conclusão da instrução. Esses gatilhos são programados no filtro de comando.

## <a name="command-filters-and-triggers"></a>Filtros de comando e gatilhos
 Filtros de comando interceptam ocorrências de gatilhos ou gatilhos. Para adicionar o filtro de comando à exibição, implemente a interface <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> e anexe-a à exibição chamando o método <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>. Você pode usar o mesmo filtro de comando (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>) para todos os aspectos do seu serviço de idioma, como conclusão de instrução, marcadores de erro e dicas de método. Para obter mais informações, consulte [interceptando comandos do serviço de idioma herdado](../../extensibility/internals/intercepting-legacy-language-service-commands.md).

 Quando o gatilho é inserido no editor — especificamente, o buffer de texto — o serviço de linguagem chama o método <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>. Isso faz com que o editor traga a interface do usuário para que o usuário possa escolher entre os candidatos de conclusão da instrução. Esse método exige que você implemente <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> e os sinalizadores de <xref:Microsoft.VisualStudio.TextManager.Interop.UpdateCompletionFlags> como parâmetros. A lista de itens de conclusão aparece em uma caixa de listagem de rolagem. À medida que o usuário continua digitando, a seleção dentro da caixa de listagem é atualizada para refletir a correspondência mais próxima com os caracteres mais recentes digitados. O editor central implementa a interface do usuário para conclusão de instrução, mas o serviço de linguagem deve implementar a interface <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> para definir um conjunto de itens de conclusão candidatos para a instrução.

## <a name="see-also"></a>Consulte também
- [Interceptar comandos do serviço de linguagem herdado](../../extensibility/internals/intercepting-legacy-language-service-commands.md)