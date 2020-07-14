---
title: Regras de desempenho de uso do .NET Framework | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ab573755-6370-48aa-853d-a7321c424c79
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: ac78ffb3455940cf2379af44ff5c2bc5870dc684
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85531996"
---
# <a name="net-framework-usage-performance-rules"></a>Regras de desempenho de uso do .NET Framework
As regras de desempenho na categoria de uso do .NET Framework identificam métodos específicos que podem ser otimizados e também identificam padrões de uso mais gerais, como coleta de lixo e contenção de bloqueio, o que pode ser investigado para problemas de desempenho.

|Regra|Descrição|
|-|-|
|[DA0001: Usar StringBuilder para concatenações](../profiling/da0001-use-stringbuilder-for-concatenations.md)|As chamadas a <xref:System.String.Concat(System.String,System.String)?displayProperty=fullName> são uma proporção significativa dos dados de criação de perfil. Considere o uso da classe <xref:System.Text.StringBuilder> para construir cadeias de caracteres com base em vários segmentos.|
|[DA0005: Coletas de GC2 frequentes](../profiling/da0005-frequent-gc2-collections.md)|Um número relativamente alto de objetos de memória do .NET está sendo recuperado na coleta de lixo de geração 2. Se muitos objetos de curta duração sobrevivem à coleta de geração 1, o custo de gerenciamento de memória pode facilmente se tornar excessivo.|
|[DA0006: Substituir Equals() por tipos de valor](../profiling/da0006-override-equals-parens-for-value-types.md)|Chama o método `Equals` ou os operadores de igualdade de um tipo de valor público são uma parte significativa dos dados de criação de perfil. Considere a implementação de um método mais eficiente.|
|[DA0007: Evitar usar exceções no fluxo de controle](../profiling/da0007-avoid-using-exceptions-for-control-flow.md)|Uma alta taxa de manipuladores de exceção do .NET Framework foram chamados nos dados de criação de perfil. Considere o uso de outra lógica de fluxo de controle para reduzir o número de exceções geradas.|
|[DA0010: Função GetHashCode dispendiosa](../profiling/da0010-expensive-gethashcode.md)|As chamadas para o método `GetHashCode` do tipo são uma parte significativa dos dados de criação de perfil ou o método `GetHashCode` aloca memória. Reduza a complexidade do método.|
|[DA0011: Função CompareTo dispendiosa](../profiling/da0011-expensive-compareto.md)|O método `CompareTo` do tipo é dispendioso ou o método aloca memória. Reduza a complexidade do método `CompareTo`.|
|[DA0012: Volume significativo de reflexão](../profiling/da0012-significant-amount-of-reflection.md)|As chamadas aos métodos <xref:System.Reflection?displayProperty=fullName>, como <xref:System.Reflection.IReflect.InvokeMember%2A> e <xref:System.Reflection.IReflect.GetMember%2A>, ou métodos de Tipo, como <xref:System.Type.InvokeMember%2A>, são uma parte significativa dos dados de criação de perfil. Quando possível, considere a substituição desses métodos pela associação antecipada aos métodos de assemblies dependentes.|
|[DA0013: Alto uso de String.Split ou String.Substring](../profiling/da0013-high-usage-of-string-split-or-string-substring.md)|As chamadas aos métodos <xref:System.String.Split%2A?displayProperty=fullName> ou <xref:System.String.Substring%2A> são uma parte significativa dos dados de criação de perfil. Considere o uso de <xref:System.String.IndexOf%2A> ou <xref:System.String.IndexOfAny%2A> se você estiver testando para verificar a existência de uma subcadeia em uma cadeia de caracteres.|
|[DA0018: Aplicativo de 32 bits em execução nos limites de memória gerenciada por processo](../profiling/da0018-32-bit-application-running-at-process-managed-memory-limits.md)|Os dados do sistema coletados durante a execução de criação de perfil indicam que os heaps de memória do .NET Framework se aproximaram do tamanho máximo que os heaps gerenciados podem atingir em um processo de 32 bits. Considere uma nova criação de perfil usando o método de criação de perfil da memória do .NET e otimização do uso de recursos gerenciados pelo aplicativo.|
|[DA0021: Alta taxa de coletas de lixo de Geração 1](../profiling/da0021-high-rate-of-gen-1-garbage-collections.md)|Um número relativamente alto de objetos de memória do .NET está sendo recuperado na coleta de lixo de geração 1. Se muitos objetos de curta duração sobrevivem à coleta de geração 0, o custo de gerenciamento de memória pode facilmente se tornar excessivo.|
|[DA0022: Alta taxa de coletas de lixo de Geração 2](../profiling/da0022-high-rate-of-gen-2-garbage-collections.md)|Um número alto de objetos de memória do .NET está sendo recuperado na coleta de lixo de geração 2. Se muitos objetos de curta duração sobrevivem à coleta de geração 1, o custo de gerenciamento de memória pode facilmente se tornar excessivo. Essa regra é acionada quando a taxa de contenções de bloqueio excede o valor do limite superior da regra DA0005.|
|[DA0023: Tempo de CPU de GC elevado](../profiling/da0023-high-gc-cpu-time.md)|Os dados de desempenho do sistema coletados durante a criação de perfil indicam que a quantidade de tempo gasto na coleta de lixo é significativa em comparação com o tempo total de processamento do aplicativo.|
|[DA0024: tempo excessivo de CPU do GC](../profiling/da0024-excessive-gc-cpu-time.md)|Os dados de desempenho do sistema coletados durante a criação de perfil indicam que a quantidade de tempo gasto na coleta de lixo é excessivamente alta em comparação com o tempo total de processamento do aplicativo. Essa regra é acionada quando a quantidade de tempo gasto na coleta de lixo excede o valor do limite superior da regra DA0023.|
|[DA0038: alta taxa de contenções de bloqueio](../profiling/da0038-high-rate-of-lock-contentions.md)|Os dados de desempenho do sistema coletados com os dados de criação de perfil indicam que ocorreu uma taxa consideravelmente alta de contenções de bloqueio durante a execução do aplicativo. Considere uma nova criação de perfil usando o método de criação de perfil de simultaneidade para descobrir a causa das contenções.|
|[DA0039: taxa muito alta de contenções de bloqueio](../profiling/da0039-very-high-rate-of-lock-contentions.md)|Os dados de desempenho do sistema coletados com os dados de criação de perfil indicam que ocorreu uma taxa excessivamente alta de contenções de bloqueio durante a execução do aplicativo. Considere uma nova criação de perfil usando o método de criação de perfil de simultaneidade para descobrir a causa das contenções. Essa regra é acionada quando a taxa de contenções de bloqueio excede o valor do limite superior da regra DA0038.|
