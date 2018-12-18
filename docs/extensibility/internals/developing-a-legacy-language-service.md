---
title: Desenvolver um serviço de linguagem herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- vs.vsip.LangServWiz.langtoks
- vs.vsip.LangServWiz.welcome
- vs.vsip.LangServWiz.langSpec
- vs.vsip.LangServWiz.langInfo
- vs.vsip.LangServWiz.langServOpts
helpviewer_keywords:
- language services, developing
ms.assetid: 6151ba88-c1c3-41de-a1cc-668f494d48d1
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 6d92c07742dcc4433aa96071d655f58d938a1f80
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39497824"
---
# <a name="develop-a-legacy-language-service"></a>Desenvolver um serviço de linguagem herdado
Links essas seção para tópicos que ajudam você a criar um serviço de linguagem herdada.  
  
 Serviços de linguagem herdado são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações sobre a nova maneira de implementar um serviço de linguagem, consulte [extensões de serviços do Editor e linguagem](../../extensibility/editor-and-language-service-extensions.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitem que você tirar proveito dos novos recursos do editor.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Modelo de um serviço de linguagem herdado](../../extensibility/internals/model-of-a-legacy-language-service.md)  
 Fornece um modelo de um serviço de linguagem mínima para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] editor de núcleo. Você pode usar esse modelo como um guia para criar seu próprio serviço de linguagem.  
  
 [Interfaces de serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-interfaces.md)  
 Discute os objetos necessários para implementar um serviço de linguagem e fornece uma lista de objetos adicionais que você pode usar para fornecer realce de sintaxe, os dados de método e outros recursos.  
  
 [Interceptar comandos do serviço de linguagem herdado](../../extensibility/internals/intercepting-legacy-language-service-commands.md)  
 Descreve como inserir um filtro de comando em seu serviço de linguagem para comandos de interceptação que trataria a exibição de texto.  
  
 [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service2.md)  
 Fornece informações sobre como registrar seu serviço de linguagem usando [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].  
  
 [Suporte do serviço de linguagem para depuração](../../extensibility/internals/language-service-support-for-debugging.md)  
 Descreve como um serviço de linguagem pode fornecer recursos para dar suporte a um depurador.  
  
 [Lista de verificação: Criar um serviço de linguagem herdado](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)  
 Fornece instruções passo a passo para criar e integrar um serviço de linguagem para o editor de núcleo.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)  
 Discute como implementar o realce de sintaxe em seu serviço de linguagem.  
  
 [Conclusão de instrução em um serviço de linguagem herdado](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)  
 Discute o preenchimento de declaração, o processo pelo qual um serviço de linguagem ajuda os usuários a concluir um elemento que eles começaram a digitação ou a palavra-chave language.  
  
 [Informações de parâmetro em um serviço de linguagem herdado](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)  
 Descreve como fornecer dicas de método para métodos e funções sobrecarregadas.  
  
 [Como: texto oculto de fornecer suporte a um serviço de linguagem herdado](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)  
 Explica a finalidade de uma região de texto oculto e fornece instruções sobre como implementar uma região de texto oculto.  
  
 [Como: fornecer suporte expandido de estrutura de tópicos em um serviço de linguagem herdado](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)  
 Explica as duas opções que estendem o suporte de estrutura de tópicos para seu idioma além do suporte a *recolher para definições de* comando.