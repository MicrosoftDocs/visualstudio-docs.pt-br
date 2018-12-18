---
title: Regras de desempenho de memória e paginação | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: f37972b2-efe4-4a1c-a5d1-a246ccd76817
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ec1acb6763d408f9f13ec3044e2cd8137d34e634
ms.sourcegitcommit: 269b55b413d2c82e6aa56c6ab8e53da7926fb2e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35237647"
---
# <a name="memory-and-paging-performance-rules"></a>Regras de desempenho de memória e de paginação
As regras de desempenho na memória e categoria de paginação identificam a atividade de paginação em uma execução de criação de perfil que pode afetar a capacidade de resposta e o desempenho do aplicativo.  
  
|||  
|-|-|  
|[DA0014: taxas extremamente elevadas de paginação de memória ativa para o disco](../profiling/da0014-extremely-high-rates-of-paging-active-memory-to-disk.md)|Uma taxa extremamente alta de paginação de memória ativa de e para o disco ocorreu durante toda a execução de criação de perfil. Geralmente, taxas de paginação nesse nível afetam a capacidade de resposta e o desempenho do aplicativo. Considere a redução das alocações de memória revisando os algoritmos. Talvez você também precise considerar os requisitos de memória do aplicativo. Tente executar a criação de perfil novamente em um computador com mais memória. Essa regra é acionada quando a quantidade de atividade de paginação excede o limite superior de regra D0017.|  
|[DA0017: taxas elevadas de paginação de memória ativa para o disco](../profiling/da0017-high-rates-of-paging-active-memory-to-disk.md)|Uma taxa relativamente alta de paginação de memória ativa de e para o disco ocorreu durante toda a execução de criação de perfil. Geralmente, taxas de paginação nesse nível afetam a capacidade de resposta e o desempenho do aplicativo. Considere a redução das alocações de memória revisando os algoritmos. Talvez você também precise considerar os requisitos de memória do aplicativo. Tente executar a criação de perfil novamente em um computador com mais memória.|