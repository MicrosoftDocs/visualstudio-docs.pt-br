---
title: Regras de desempenho de uso do .NET Framework | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ab573755-6370-48aa-853d-a7321c424c79
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0706a5279a2ab338cc6e50cce25051b4fba7b366
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51756138"
---
# <a name="net-framework-usage-performance-rules"></a>Regras de desempenho de uso do .NET Framework
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As regras de desempenho na categoria de uso do .NET Framework identificam métodos específicos que podem ser otimizados e também identificam padrões de uso mais gerais, como coleta de lixo e contenção de bloqueio, o que pode ser investigado para problemas de desempenho.  
  
|||  
|-|-|  
|[DA0001: usar StringBuilder para concatenações](../profiling/da0001-use-stringbuilder-for-concatenations.md)|As chamadas a <xref:System.String.Concat%28System.String%2CSystem.String%29?displayProperty=fullName> são uma proporção significativa dos dados de criação de perfil. Considere o uso da classe <xref:System.Text.StringBuilder> para construir cadeias de caracteres com base em vários segmentos.|  
|[DA0005: coletas GC2 frequentes](../profiling/da0005-frequent-gc2-collections.md)|Um número relativamente alto de objetos de memória do .NET está sendo recuperado na coleta de lixo de geração 2. Se muitos objetos de curta duração sobrevivem à coleta de geração 1, o custo de gerenciamento de memória pode facilmente se tornar excessivo.|  
|[DA0006: substituir Equals() para tipos de valor](../profiling/da0006-override-equals-parens-for-value-types.md)|Chama o método `Equals` ou os operadores de igualdade de um tipo de valor público são uma parte significativa dos dados de criação de perfil. Considere a implementação de um método mais eficiente.|  
|[DA0007: evitar usar exceções no fluxo de controle](../profiling/da0007-avoid-using-exceptions-for-control-flow.md)|Uma alta taxa de manipuladores de exceção do .NET Framework foram chamados nos dados de criação de perfil. Considere o uso de outra lógica de fluxo de controle para reduzir o número de exceções geradas.|  
|[DA0010: função GetHashCode cara](../profiling/da0010-expensive-gethashcode.md)|As chamadas para o método `GetHashCode` do tipo são uma parte significativa dos dados de criação de perfil ou o método `GetHashCode` aloca memória. Reduza a complexidade do método.|  
|[DA0011: CompareTo dispendiosa](../profiling/da0011-expensive-compareto.md)|O método `CompareTo` do tipo é dispendioso ou o método aloca memória. Reduza a complexidade do método `CompareTo`.|  
|[DA0012: volume significativo de reflexão](../profiling/da0012-significant-amount-of-reflection.md)|As chamadas aos métodos <xref:System.Reflection?displayProperty=fullName>, como <xref:System.Reflection.IReflect.InvokeMember%2A> e <xref:System.Reflection.IReflect.GetMember%2A>, ou métodos de Tipo, como <xref:System.Type.InvokeMember%2A>, são uma parte significativa dos dados de criação de perfil. Quando possível, considere a substituição desses métodos pela associação antecipada aos métodos de assemblies dependentes.|  
|[DA0013: alto uso de String.Split ou String.Substring](../profiling/da0013-high-usage-of-string-split-or-string-substring.md)|As chamadas aos métodos <xref:System.String.Split%2A?displayProperty=fullName> ou <xref:System.String.Substring%2A> são uma parte significativa dos dados de criação de perfil. Considere o uso de <xref:System.String.IndexOf%2A> ou <xref:System.String.IndexOfAny%2A> se você estiver testando para verificar a existência de uma subcadeia em uma cadeia de caracteres.|  
|[DA0018: aplicativo de 32 bits em execução em limites de memória gerenciada do processo](../profiling/da0018-32-bit-application-running-at-process-managed-memory-limits.md)|Os dados do sistema coletados durante a execução de criação de perfil indicam que os heaps de memória do .NET Framework se aproximaram do tamanho máximo que os heaps gerenciados podem atingir em um processo de 32 bits. Considere uma nova criação de perfil usando o método de criação de perfil da memória do .NET e otimização do uso de recursos gerenciados pelo aplicativo.|  
|[DA0021: taxa alta de coletas de lixo da geração 1](../profiling/da0021-high-rate-of-gen-1-garbage-collections.md)|Um número relativamente alto de objetos de memória do .NET está sendo recuperado na coleta de lixo de geração 1. Se muitos objetos de curta duração sobrevivem à coleta de geração 0, o custo de gerenciamento de memória pode facilmente se tornar excessivo.|  
|[DA0022: taxa alta de coletas de lixo da geração 2](../profiling/da0022-high-rate-of-gen-2-garbage-collections.md)|Um número alto de objetos de memória do .NET está sendo recuperado na coleta de lixo de geração 2. Se muitos objetos de curta duração sobrevivem à coleta de geração 1, o custo de gerenciamento de memória pode facilmente se tornar excessivo. Essa regra é acionada quando a taxa de contenções de bloqueio excede o valor do limite superior da regra DA0005.|  
|[DA0023: tempo de CPU em GC alto](../profiling/da0023-high-gc-cpu-time.md)|Os dados de desempenho do sistema coletados durante a criação de perfil indicam que a quantidade de tempo gasto na coleta de lixo é significativa em comparação com o tempo total de processamento do aplicativo.|  
|[DA0024: tempo de CPU para GC excessivo](../profiling/da0024-excessive-gc-cpu-time.md)|Os dados de desempenho do sistema coletados durante a criação de perfil indicam que a quantidade de tempo gasto na coleta de lixo é excessivamente alta em comparação com o tempo total de processamento do aplicativo. Essa regra é acionada quando a quantidade de tempo gasto na coleta de lixo excede o valor do limite superior da regra DA0023.|  
|[DA0038: taxa alta de contenções de bloqueio](../profiling/da0038-high-rate-of-lock-contentions.md)|Os dados de desempenho do sistema coletados com os dados de criação de perfil indicam que ocorreu uma taxa consideravelmente alta de contenções de bloqueio durante a execução do aplicativo. Considere uma nova criação de perfil usando o método de criação de perfil de simultaneidade para descobrir a causa das contenções.|  
|[DA0039: taxa muito alta de contenções de bloqueio](../profiling/da0039-very-high-rate-of-lock-contentions.md)|Os dados de desempenho do sistema coletados com os dados de criação de perfil indicam que ocorreu uma taxa excessivamente alta de contenções de bloqueio durante a execução do aplicativo. Considere uma nova criação de perfil usando o método de criação de perfil de simultaneidade para descobrir a causa das contenções. Essa regra é acionada quando a taxa de contenções de bloqueio excede o valor do limite superior da regra DA0038.|



