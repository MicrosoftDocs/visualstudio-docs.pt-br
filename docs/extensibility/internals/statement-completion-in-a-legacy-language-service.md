---
title: Conclusão de instrução em um serviço de linguagem herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- statement completion
- language services, statement completion
ms.assetid: 617439dc-3f0e-4e5f-b346-3e4e7fcf3c1b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: d76face8f43bcb428a9c3b997083f8299d332cc8
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31131321"
---
# <a name="statement-completion-in-a-legacy-language-service"></a>Conclusão de instrução em um serviço de linguagem herdado
Conclusão de instrução é o processo pelo qual o serviço de linguagem ajuda os usuários a concluir uma palavra-chave do idioma ou um elemento que eles tenham sido iniciados digitando no editor de núcleo. Este tópico discute como funciona a conclusão de instrução e como implementá-la em seu serviço de linguagem.  
  
 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações sobre a nova maneira de implementar a conclusão de instrução, consulte [passo a passo: exibindo a conclusão de instrução](../../extensibility/walkthrough-displaying-statement-completion.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API assim que possível. Isso melhorar o desempenho do seu serviço de linguagem e permitem que você aproveite os novos recursos do editor.  
  
## <a name="implementing-statement-completion"></a>Implementação de conclusão de instrução  
 No editor de núcleo, conclusão de instrução ativa uma interface de usuário especial que interativamente torna mais fácil e rapidamente escreve código. Conclusão de instrução ajuda exibindo pertinentes objetos ou classes de quando elas forem necessárias, que evita a você ter de lembrar elementos específicos ou precisar procurá-los em um tópico de referência da Ajuda.  
  
 Para implementar a conclusão de instrução, o idioma deve ter um gatilho de conclusão de instrução, que pode ser analisado. Por exemplo, [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] usa um operador ponto (.), enquanto [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] usa uma seta (->) operador. Um serviço de idioma pode usar mais de um gatilho para iniciar a conclusão de instrução. Esses gatilhos são programados no filtro de comando.  
  
## <a name="command-filters-and-triggers"></a>Filtros de comando e gatilhos  
 Comando filtros interceptam as ocorrências do gatilho ou gatilhos. Para adicionar o filtro de comando para o modo de exibição, implementar a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> de interface e anexá-lo no modo de exibição ao chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> método. Você pode usar o mesmo filtro de comando (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>) para todos os aspectos do seu serviço de linguagem, como a conclusão de instrução, marcadores de erro e dicas de método. Para obter mais informações, consulte [interceptando comandos de serviço de linguagem herdado](../../extensibility/internals/intercepting-legacy-language-service-commands.md).  
  
 Quando o gatilho é inserido no editor — especificamente, o buffer de texto — seu serviço de linguagem, em seguida, chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> método. Isso faz com que o editor exibir a interface do usuário para que o usuário pode escolher entre os candidatos de conclusão de instrução. Esse método requer que você implemente <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> e <xref:Microsoft.VisualStudio.TextManager.Interop.UpdateCompletionFlags> sinalizadores como parâmetros. A lista de itens de conclusão é exibida em uma caixa de lista de rolagem. Como o usuário continua a digitação, a seleção dentro da caixa de lista é atualizada para refletir que a correspondência mais próxima as mais recentes caracteres digitados. O editor de núcleo implementa a interface do usuário para a conclusão de instrução, mas o serviço de linguagem deve implementar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> interface para definir um conjunto de itens de conclusão de candidato para a instrução.  
  
## <a name="see-also"></a>Consulte também  
 [Interceptar comandos do serviço de linguagem herdado](../../extensibility/internals/intercepting-legacy-language-service-commands.md)