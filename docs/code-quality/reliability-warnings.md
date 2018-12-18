---
title: Avisos de confiabilidade
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- vs.codeanalysis.reliabilityrules
helpviewer_keywords:
- warnings, reliability
- reliability warnings
- managed code analysis warnings, reliability warnings
ms.assetid: 77886846-10a2-4585-968a-7eb60ebe07e8
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c690be59758ca17a573d742fc0f75c81b955d5ad
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31916742"
---
# <a name="reliability-warnings"></a>Avisos de confiabilidade
Avisos de confiabilidade oferecem suporte a confiabilidade de biblioteca e o aplicativo, como uso de memória e thread correto.

## <a name="in-this-section"></a>Nesta seção

|Regra|Descrição|
|----------|-----------------|
|[CA2000: descartar objetos antes de perder o escopo](../code-quality/ca2000-dispose-objects-before-losing-scope.md)|Como pode ocorrer um evento excepcional que impedirá a execução do finalizador de um objeto, o objeto deve ser explicitamente descartado antes que todas as referências a ele estejam fora do escopo.|
|[CA2001: evitar chamar métodos problemáticos](../code-quality/ca2001-avoid-calling-problematic-methods.md)|Um membro chama um método potencialmente perigoso ou problemático.|
|[CA2002: não bloquear objetos com identidade fraca](../code-quality/ca2002-do-not-lock-on-objects-with-weak-identity.md)|Diz-se que um objeto tem uma identidade fraca quando puder ser acessado diretamente em todos os limites de domínio do aplicativo. Um thread que tente adquirir um bloqueio em um objeto com uma identidade fraca pode ser bloqueado por um segundo thread em um domínio de aplicativo diferente com um bloqueio no mesmo objeto.|
|[CA2003: não tratar fibras como threads](../code-quality/ca2003-do-not-treat-fibers-as-threads.md)|Um thread gerenciado está sendo tratado como um thread do Win32.|
|[CA2004: remover chamadas para GC.KeepAlive](../code-quality/ca2004-remove-calls-to-gc-keepalive.md)|Se você estiver convertendo para o uso de SafeHandle, remova todas as chamadas para GC. KeepAlive (object). Nesse caso, as classes não devem ter que chamar GC. Tratar KeepAlive, supondo que eles não têm um finalizador, mas dependem de SafeHandle para finalizar o sistema operacional para eles.|
|[CA2006: use SafeHandle para encapsular recursos nativos](../code-quality/ca2006-use-safehandle-to-encapsulate-native-resources.md)|O uso de IntPtr em código gerenciado pode indicar um problema de segurança e confiabilidade em potencial. Todos os usos de IntPtr devem ser examinados para determinar se o uso de um SafeHandle, ou tecnologia semelhante, é necessário em seu lugar.|