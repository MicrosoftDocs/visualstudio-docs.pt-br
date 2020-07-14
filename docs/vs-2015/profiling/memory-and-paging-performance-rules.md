---
title: Regras de desempenho de memória e paginação | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: f37972b2-efe4-4a1c-a5d1-a246ccd76817
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: bf868164a8768b01793e6c5ec69b90c89cab34bb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547960"
---
# <a name="memory-and-paging-performance-rules"></a>Regras de desempenho de memória e paginação
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As regras de desempenho na memória e categoria de paginação identificam a atividade de paginação em uma execução de criação de perfil que pode afetar a capacidade de resposta e o desempenho do aplicativo.  
  
|Regra|Descrição|  
|-|-|  
|[DA0014: Taxas de paginação de memória ativa para o disco extremamente altas](../profiling/da0014-extremely-high-rates-of-paging-active-memory-to-disk.md)|Uma taxa extremamente alta de paginação de memória ativa de e para o disco ocorreu durante toda a execução de criação de perfil. Geralmente, taxas de paginação nesse nível afetam a capacidade de resposta e o desempenho do aplicativo. Considere a redução das alocações de memória revisando os algoritmos. Talvez você também precise considerar os requisitos de memória do aplicativo. Tente executar a criação de perfil novamente em um computador com mais memória. Essa regra é acionada quando a quantidade de atividade de paginação excede o limite superior de regra D0017.|  
|[DA0017: Altas taxas de paginação de memória ativa para o disco](../profiling/da0017-high-rates-of-paging-active-memory-to-disk.md)|Uma taxa relativamente alta de paginação de memória ativa de e para o disco ocorreu durante toda a execução de criação de perfil. Geralmente, taxas de paginação nesse nível afetam a capacidade de resposta e o desempenho do aplicativo. Considere a redução das alocações de memória revisando os algoritmos. Talvez você também precise considerar os requisitos de memória do aplicativo. Tente executar a criação de perfil novamente em um computador com mais memória.|
