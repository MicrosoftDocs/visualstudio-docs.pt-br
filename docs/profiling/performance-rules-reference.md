---
title: Referência das Regras de Desempenho | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 59fc9424-76ca-4365-ae47-bb14a736c9c2
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 5280226aaba40de42052d72e58928a53af53f631
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543631"
---
# <a name="performance-rules-reference"></a>Referência de regras de desempenho
As regras de desempenho das Ferramentas de Criação de Perfil fornecem avisos adicionais e informações sobre o desempenho do seu aplicativo. Regras de desempenho analisam os dados em uma execução de criação de perfil que é coletada das fontes, tal como Windows e contadores de desempenho do processador. Mensagens de regra aparecem na janela Saída de Erro do ambiente de desenvolvimento integrado do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]. As mensagens são listadas com um dos seguintes níveis de regra:

|Categoria|Descrição|
|-|-|
|**Erro**|Algumas regras geram mensagens de erro porque a maioria dos problemas de desempenho não são erros diretos. Uma mensagem de erro pode indicar uma falha ao coletar dados de criação de perfil.|
|**Aviso**|Os avisos indicam uma área do aplicativo que pode ser uma fonte de problemas de desempenho em potencial ou que poderia se beneficiar com otimizações.|
|**Informações**|Mensagens informativas indicam que a análise de uma condição de regra não atingiu o limite para gerar uma mensagem de erro ou que as informações na mensagem é útil, mas não representa um problema de desempenho.|

## <a name="in-this-section"></a>Nesta seção

[Regras de desempenho por ID](../profiling/performance-rules-by-id.md)

As regras de desempenho de Ferramentas de Criação de Perfil são organizadas em quatro categorias:

|Categoria|Descrição|
|-|-|
|[Regras de desempenho de uso do .NET Framework](../profiling/dotnet-framework-usage-performance-rules.md)|Regras que ajudam a usar o .NET Framework com eficiência.|
|[Regras de desempenho de memória e paginação](../profiling/memory-and-paging-performance-rules.md)|Regras que analisam a memória gerenciada e o comportamento de paginação de seu aplicativo.|
|[Regras de uso de Ferramentas de Criação de Perfil](../profiling/profiling-tools-usage-rules.md)|Regras que ajudam a usar as Ferramentas de Criação de Perfil com eficiência.|
|[Regras de desempenho de monitoramento de recursos](../profiling/resource-monitoring-performance-rules.md)|Mensagens informativas sobre a utilização de processador e de memória em uma execução de criação de perfil.|
