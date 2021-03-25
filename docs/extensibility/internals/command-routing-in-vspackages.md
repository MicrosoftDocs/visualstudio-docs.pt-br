---
title: Roteamento de comandos em VSPackages | Microsoft Docs
description: Saiba mais sobre o roteamento de comandos no VSPackages e como os comandos são roteados com base no contexto no qual eles são executados no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, routing
- command routing, Visual Studio SDK
ms.assetid: a9c7f9ae-3594-4557-a314-8cf76f5f8772
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 35ab5e7989fdeb46592f38cb7e55854885e076d1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057293"
---
# <a name="command-routing-in-vspackages"></a>Roteamento de comandos em VSPackages
Um comando é roteado [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] com base no contexto no qual ele é executado. Ele é roteado do contexto inicial para fora para o contexto global.

## <a name="in-this-section"></a>Nesta seção
- [Algoritmo de roteamento de comando](../../extensibility/internals/command-routing-algorithm.md)

 Descreve a ordem de resolução de roteamento de comandos.

- [Disponibilidade do comando](../../extensibility/internals/command-availability.md)

 Discute o roteamento de comandos.

- [Comandos e menus que usam assemblies de interoperabilidade](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)

 Discute considerações em comandos de roteamento entre código gerenciado e COM.

## <a name="related-sections"></a>Seções relacionadas
- [Objetos de contexto de seleção](../../extensibility/internals/selection-context-objects.md)

 Discute o modelo de como você pode determinar o foco de contexto de seleção do usuário em uma janela.

- [Comandos, menus e barras de ferramentas](../../extensibility/internals/commands-menus-and-toolbars.md)

 Explica como criar uma interface do usuário que inclui menus, barras de ferramentas e caixas de combinação de comandos.
