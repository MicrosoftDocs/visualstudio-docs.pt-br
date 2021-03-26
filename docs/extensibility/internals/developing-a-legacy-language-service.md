---
title: Desenvolvendo um serviço de linguagem herdada | Microsoft Docs
description: Saiba mais sobre como implementar um serviço de linguagem herdado como parte de um VSPackage ou usando as extensões Managed Extensibility Framework (MEF).
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 59c06c96d2a0263c9e76ed4359e0fac93ab2ab25
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056721"
---
# <a name="develop-a-legacy-language-service"></a>Desenvolver um serviço de linguagem herdado
Esta seção contém links para tópicos que ajudam a criar um serviço de idioma herdado.

 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para saber mais sobre a nova maneira de implementar um serviço de linguagem, consulte [extensões de serviço de editor e linguagem](../../extensibility/editor-and-language-service-extensions.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

## <a name="in-this-section"></a>Nesta seção
- [Modelo de um serviço de linguagem herdado](../../extensibility/internals/model-of-a-legacy-language-service.md)

 Fornece um modelo de um serviço de linguagem mínimo para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] editor principal. Você pode usar esse modelo como um guia para criar seu próprio serviço de linguagem.

- [Interfaces de serviço de idioma herdado](../../extensibility/internals/legacy-language-service-interfaces.md)

 Discute os objetos necessários para implementar um serviço de linguagem e fornece uma lista de objetos adicionais que você pode usar para fornecer realce de sintaxe, dados de método e outros recursos.

- [Interceptar comandos do serviço de idioma herdado](../../extensibility/internals/intercepting-legacy-language-service-commands.md)

 Descreve como inserir um filtro de comando em seu serviço de linguagem para interceptar comandos que o modo de exibição de texto trataria de outra forma.

- [Registrar um serviço de idioma herdado](../../extensibility/internals/registering-a-legacy-language-service2.md)

 Fornece informações sobre como registrar seu serviço de idioma usando o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

- [Suporte ao serviço de linguagem para depuração](../../extensibility/internals/language-service-support-for-debugging.md)

 Descreve como um serviço de linguagem pode fornecer recursos para dar suporte a um depurador.

- [Lista de verificação: criar um serviço de idioma herdado](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)

 Fornece instruções passo a passo para criar e integrar um serviço de linguagem para o editor principal.

## <a name="related-sections"></a>Seções relacionadas
- [Cores de sintaxe em um serviço de idioma herdado](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 Discute como implementar o realce de sintaxe em seu serviço de linguagem.

- [Conclusão de instrução em um serviço de linguagem herdada](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)

 Discute a conclusão da instrução, o processo pelo qual um serviço de linguagem ajuda os usuários a concluir uma palavra-chave ou um elemento de idioma que eles começaram a digitar.

- [Informações de parâmetro em um serviço de idioma herdado](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)

 Descreve como fornecer dicas de método para funções e métodos sobrecarregados.

- [Como fornecer suporte a texto oculto em um serviço de idioma herdado](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)

 Explica a finalidade de uma região de texto oculta e fornece instruções sobre como implementar uma região de texto oculta.

- [Como fornecer suporte expandido para estrutura de tópicos em um serviço de linguagem herdado](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)

 Explica as duas opções que estendem o suporte de estrutura de tópicos para sua linguagem além de dar suporte ao comando *recolher para definições* .
