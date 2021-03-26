---
title: Features1 do serviço de linguagem herdada | Microsoft Docs
description: Saiba mais sobre os recursos do Visual Studio que têm suporte em um serviço de linguagem MPF (Managed Package Framework).
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework]
ms.assetid: a646e4f0-767d-4cd1-8e1a-9a2aa210a1b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2bb5169eeb53aa16d0827cdf50cb50d0db34d996
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074505"
---
# <a name="legacy-language-service-features-1"></a>Recursos do serviço de linguagem herdada 1
Um serviço de linguagem MPF (Managed Package Framework) pode dar suporte A um ou mais [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] recursos, como realce de sintaxe, IntelliSense e validação de ponto de interrupção. Cada recurso pode ser implementado independentemente dos outros, mas todos exigem um analisador e um scanner, exceto o realce de sintaxe, que requer apenas um scanner.

## <a name="in-this-section"></a>Nesta seção
- [Correspondência de chaves em um serviço de linguagem herdado](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)

 Descreve o que é necessário para dar suporte à correspondência de pares de idiomas, também conhecido como correspondência de chaves.

- [Comentando o código em um serviço de linguagem herdado](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)

 Descreve o que é necessário para dar suporte a comentários e remover comentários do código selecionado.

- [Propriedades de documento personalizadas em um serviço de linguagem herdado](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)

 Descreve o que é necessário para dar suporte a propriedades de documento que são inseridas em um arquivo de origem.

- [Estrutura de tópicos em um serviço de linguagem herdado](../../extensibility/internals/outlining-in-a-legacy-language-service.md)

 Descreve o que é necessário para dar suporte à estrutura de tópicos por meio da implementação de regiões ocultas.

- [Reformatando o código em um serviço de linguagem herdado](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)

 Descreve o que é necessário para dar suporte ao código de reformatação.

- [Suporte para snippets de código em um serviço de linguagem herdado](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)

 Descreve o que é necessário para dar suporte a trechos de código, que são segmentos de código que são inseridos e podem ser editados.

- [Informações de parâmetro em um serviço de linguagem herdado](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)

 Descreve o que é necessário para dar suporte à operação de informações de parâmetro do IntelliSense para exibir uma assinatura de método, pois o método é digitado.

- [Informações rápidas em um serviço de linguagem herdado](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)

 Descreve o que é necessário para dar suporte à operação de informações rápidas do IntelliSense para exibir informações sobre um identificador.

- [Preenchimento de membro em um serviço de linguagem herdado](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)

 Descreve o que é necessário para dar suporte à operação de conclusão de membro do IntelliSense para selecionar um membro de um namespace de uma lista.

- [Preenchimento de palavra em um serviço de linguagem herdado](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)

 Descreve o que é necessário para dar suporte à operação do IntelliSense Complete Word para concluir palavras com tipo parcial.

- [Suporte para a janela de automáticos em um serviço de linguagem herdado](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)

 Descreve o que um serviço de linguagem pode fazer para dar suporte à janela de **automóveis** enquanto você está depurando.

- [Suporte para a barra de navegação em um serviço de linguagem herdado](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)

 Descreve como usar a **barra de navegação** na parte superior da exibição do editor para fornecer navegação rápida para qualquer tipo ou membro no arquivo mostrado nessa exibição.

- [Coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

 Descreve o que é necessário para dar suporte ao realce de sintaxe do código-fonte.

- [Validando pontos de interrupção em um serviço de linguagem herdado](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)

 Descreve o que um serviço de linguagem pode fazer para dar suporte à validação de pontos de interrupção fora de um depurador.

## <a name="related-sections"></a>Seções relacionadas
- [Analisador e scanner do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 Descreve o analisador e o scanner que são necessários para implementar todos os recursos de um serviço de linguagem que usa a estrutura de pacote gerenciada.

- [Implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 Descreve o que é necessário para implementar um serviço de linguagem usando o MPF.

- [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)

 Descreve as etapas necessárias para registrar um serviço de linguagem baseado em MPF com o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

- [Usando o IntelliSense](../../ide/using-intellisense.md)

 Explica como o IntelliSense torna as referências de linguagem fáceis de acessar.

- [Implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service1.md)

 Fornece informações sobre como usar a MPF (estrutura de pacote gerenciada) para implementar um serviço de linguagem repleto de recursos em código gerenciado.
