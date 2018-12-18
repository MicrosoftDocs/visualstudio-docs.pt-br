---
title: Conclusão de instrução em um serviço de linguagem herdado | Microsoft Docs
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
- statement completion
- language services, statement completion
ms.assetid: 617439dc-3f0e-4e5f-b346-3e4e7fcf3c1b
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: d88ebe84ec3ec5efb1d7c4ac04ebaee50ac65b97
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51796487"
---
# <a name="statement-completion-in-a-legacy-language-service"></a>Preenchimento de declaração em um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Preenchimento de declaração é o processo pelo qual o serviço de linguagem ajuda os usuários a concluir uma palavra-chave do idioma ou um elemento que eles tenham sido iniciados digitando no editor de núcleo. Este tópico discute como funciona o preenchimento de declaração e como implementá-lo em seu serviço de linguagem.  
  
 Serviços de linguagem herdado são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações sobre a nova maneira de implementar o preenchimento de declaração, consulte [instruções passo a passo: exibindo o preenchimento de declaração](../../extensibility/walkthrough-displaying-statement-completion.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitem que você tirar proveito dos novos recursos do editor.  
  
## <a name="implementing-statement-completion"></a>Implementando o preenchimento de declaração  
 No editor de núcleo, a conclusão da instrução ativa uma interface de usuário especial que ajuda você a interativamente com mais facilidade e rapidamente escrever código. Ajuda do preenchimento de declaração exibindo classes ou objetos pertinentes quando eles forem necessários, que evita a ter de lembrar elementos específicos ou precisar examiná-los em um tópico de referência da Ajuda.  
  
 Para implementar o preenchimento de declaração, o idioma deve ter um gatilho de conclusão de instrução, que pode ser analisado. Por exemplo, [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] usa um operador ponto (.), enquanto [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] usa uma seta (->) operador. Um serviço de linguagem pode usar mais de um gatilho para iniciar a conclusão da instrução. Esses gatilhos são programados no filtro de comando.  
  
## <a name="command-filters-and-triggers"></a>Filtros de comando e gatilhos  
 Comandos filtros interceptam as ocorrências de seu gatilho ou gatilhos. Para adicionar o filtro de comando para o modo de exibição, implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> da interface e anexá-lo para o modo de exibição chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> método. Você pode usar o mesmo filtro de comando (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>) para todos os aspectos do seu serviço de linguagem, como preenchimento de declaração, marcadores de erro e dicas de método. Para obter mais informações, consulte [interceptar comandos de serviço de linguagem herdado](../../extensibility/internals/intercepting-legacy-language-service-commands.md).  
  
 Quando o gatilho é inserido no editor — especificamente, o buffer de texto — o serviço de linguagem, em seguida, chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> método. Isso faz com que o editor abrir a interface do usuário para que o usuário pode escolher os candidatos de conclusão de instrução. Esse método requer que você implemente <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> e o <xref:Microsoft.VisualStudio.TextManager.Interop.UpdateCompletionFlags> sinalizadores como parâmetros. A lista de itens de conclusão é exibida em uma caixa de lista de rolagem. Como o usuário continua a digitar, a seleção dentro da caixa de lista é atualizada para refletir que a correspondência mais próxima aos mais recentes caracteres digitados. O editor de núcleo implementa a interface do usuário para a conclusão de instrução, mas o serviço de linguagem deve implementar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> interface para definir um conjunto de itens de conclusão de candidato para a instrução.  
  
## <a name="see-also"></a>Consulte também  
 [Interceptar comandos do serviço de linguagem herdado](../../extensibility/internals/intercepting-legacy-language-service-commands.md)

