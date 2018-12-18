---
title: Tem 2 serviço de linguagem herdada | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], code development aides
ms.assetid: 97c38622-ae0b-4ae0-90ed-604072c298d3
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b807f5f776690e86cb44334c1822a8facd6ec824
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31130736"
---
# <a name="legacy-language-service-features"></a>Recursos de serviço de linguagem herdada
Os tópicos a seguir listam alguns dos recursos de serviço de linguagem herdada que pode fornecer.  
  
 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações sobre a nova maneira de implementar um serviço de idioma, consulte [Editor e extensões de serviço de linguagem](../../extensibility/editor-and-language-service-extensions.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API assim que possível. Isso melhorar o desempenho do seu serviço de linguagem e permitem que você aproveite os novos recursos do editor.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)  
 Explica como implementar a coloração de sintaxe.  
  
 [Formatação automática em um serviço de linguagem herdado](../../extensibility/internals/automatic-formatting-in-a-legacy-language-service.md)  
 Explica como implementar a formatação automática.  
  
 [Informações de parâmetro em um serviço de linguagem herdado](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)  
 Explica como implementar a dica de ferramenta de informações de parâmetro do IntelliSense.  
  
 [Preenchimento de declaração em um serviço de linguagem herdado](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)  
 Explica como implementar a lista de instruções IntelliSense e a lista de conclusão de membro.  
  
 [Estruturar em tópicos e texto oculto em um serviço de linguagem herdado](../../extensibility/internals/outlining-and-hidden-text-in-a-legacy-language-service.md)  
 Explica como implementar o texto oculto ou estrutura de tópicos.  
  
 [Como fornecer suporte estendido à estrutura de tópicos em um serviço de linguagem herdado](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)  
 Explica algumas das etapas da implementação do suporte do depurador.  
  
## <a name="related-sections"></a>Seções relacionadas