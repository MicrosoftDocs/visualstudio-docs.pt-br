---
title: Visão geral do serviço de linguagem herdada | Microsoft Docs
description: Saiba mais sobre os serviços de linguagem herdados no Visual Studio e os recursos com suporte pelas classes de serviço de linguagem MPF (Managed Package Framework).
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], about language services
ms.assetid: bb44e27b-d228-463c-b2cf-cd5c24c7c1b5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 236fc2a2923ffd0829f74ab56a119ff81b29cd7f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061167"
---
# <a name="legacy-language-service-overview"></a>Visão geral do serviço de linguagem herdado
Um serviço de linguagem fornece suporte ao editor que permite que você implemente determinados [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] recursos. As classes de serviço de linguagem MPF (Managed Package Framework) fornecem suporte completo para recursos usados com frequência e suporte parcial para outros recursos.

## <a name="fully-supported-features-in-the-mpf"></a>Recursos totalmente suportados no MPF
 As classes de serviço de linguagem MPF oferecem suporte aos seguintes recursos:

- Realce de sintaxe

- Estrutura de tópicos

- Comentando blocos de código

- Correspondência de chaves

- Snippets de código

- Propriedades do documento personalizado

- Informações de parâmetro do IntelliSense

- Informações rápidas do IntelliSense

- Conclusão de membro do IntelliSense

- Preenchimento de palavra do IntelliSense

## <a name="partially-supported-features-in-the-mpf"></a>Recursos com suporte parcial no MPF
 O MPF fornece apenas suporte parcial para os recursos a seguir. Isso significa que você deve implementar os métodos que são chamados pelo MPF.

- Reformatando código. Você fornece o código que implementa a reformatação.

- Validando pontos de interrupção identificando trechos de código válidos. Você fornece o código que identifica os trechos de código.

- Suporte à janela de **auto** -depurador para exibição de variáveis. Você fornece o código que determina o que mostrar na janela.

- Suporte à **barra de navegação** para navegação rápida entre tipos e membros. Você implementa e retorna uma classe auxiliar que popula as listas nas caixas de combinação da **barra de navegação** .

## <a name="implementation"></a>Implementação
 Você deve concluir várias etapas para implementar o próprio serviço de linguagem e os recursos de serviço de idioma para os quais você deseja dar suporte para seu idioma. Essas etapas são discutidas nos seguintes tópicos:

- [Implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service2.md)

- [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)

- [Coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

- [Correspondência de chaves em um serviço de linguagem herdado](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)

- [Estrutura de tópicos em um serviço de linguagem herdado](../../extensibility/internals/outlining-in-a-legacy-language-service.md)

- [Comentando o código em um serviço de linguagem herdado](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)

- [Reformatando o código em um serviço de linguagem herdado](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)

- [Propriedades de documento personalizadas em um serviço de linguagem herdado](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)

- [Suporte para snippets de código em um serviço de linguagem herdado](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)

- [Suporte para a barra de navegação em um serviço de linguagem herdado](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)

- [Preenchimento de palavra em um serviço de linguagem herdado](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)

- [Preenchimento de membro em um serviço de linguagem herdado](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)

- [Informações de parâmetro em um serviço de linguagem herdado](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)

- [Informações rápidas em um serviço de linguagem herdado](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)

- [Suporte para a janela de automáticos em um serviço de linguagem herdado](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)

- [Validando pontos de interrupção em um serviço de linguagem herdado](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)

## <a name="see-also"></a>Confira também
- [Implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [Extensibilidade do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-extensibility.md)
