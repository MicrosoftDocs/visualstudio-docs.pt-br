---
title: Introdução com extensibilidade do depurador | Microsoft Docs
description: Introdução à criação e à personalização de componentes do depurador usados para depurar programas de dentro do ambiente do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- getting started, Debugging SDK
- debugging [Debugging SDK], getting started
- Debugging SDK, getting started
ms.assetid: d6ce6f43-1409-4bf7-93cd-f3464ca23504
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 20591adffbfdfd21d1ff1a77eaade39c165b9c51
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059971"
---
# <a name="get-started-with-debugger-extensibility"></a>Introdução à extensibilidade do depurador
O [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] fornece as informações necessárias para criar e personalizar os componentes do depurador usados para depurar programas de dentro do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente.

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] a depuração adicionou melhorias derivadas do extensivo teste de usabilidade realizado em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depuradores anteriores. Você pode usar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] a depuração para percorrer um aplicativo em vários idiomas ou pode implementar a edição imediata de variáveis durante a depuração de aplicativos e soluções de vários idiomas.

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] a depuração é executada fora do processo com o programa que está sendo depurado e, portanto, é menos invasiva no espaço de processo do aplicativo. Consequentemente, é mais fácil escrever componentes que interajam com o depurador sem afetar o programa de depuração.

 Para usar melhor o [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] , você deve estar familiarizado com os seguintes itens:

- O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente de desenvolvimento integrado (IDE)

- A linguagem de programação C++

- COM ATL

## <a name="in-this-section"></a>Nesta seção
 [Roteiro para estender o depurador](../../extensibility/debugger/roadmap-for-extending-the-debugger.md) Descreve o processo de implementação da depuração em seu produto, dependendo do seu compilador e de sua saída.

 [Componentes do depurador](../../extensibility/debugger/debugger-components.md) Fornece uma visão geral dos [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] componentes de depuração, que incluem o mecanismo de depuração, o avaliador de expressão (EE) e o manipulador de símbolo (SH).

 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md) Descreve os principais conceitos de arquitetura da depuração.

 [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md) Explica como o mecanismo de depuração (DE) opera simultaneamente nos contextos de avaliação de código, documentação e expressão. Descreve, para cada um dos três contextos, o local, a posição ou a avaliação relevante para ele.

 [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md) Contém links para várias tarefas de depuração, como iniciar um programa e avaliar expressões.
