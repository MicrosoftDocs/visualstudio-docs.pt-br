---
title: 'DA0014: taxas extremamente altas de paginação de memória ativa em disco | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.performance.rules.DAMemoryBound
- vs.performance.DA0014
- vs.performance.14
- vs.performance.rules.DA0014
ms.assetid: a7fa3749-9191-437a-9331-9d917181e62f
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ba6695b4705a29264f29fa79d23a63062151a62e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51730599"
---
# <a name="da0014-extremely-high-rates-of-paging-active-memory-to-disk"></a>DA0014: taxas extremamente elevadas de paginação de memória ativa em disco
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Id da regra | DA0014 |  
| Categoria | Memória e paginação |  
| Método de criação de perfil | Todos os |  
| Mensagem | Está ocorrendo uma taxa extremamente alta de paginação de memória ativa em disco. Seu aplicativo pode ser associado à memória. |  
| Tipo de regra | Aviso |  
  
 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 25 amostras para disparar essa regra.  
  
## <a name="cause"></a>Causa  
 Os dados de desempenho do sistema coletados na execução de criação de perfil indicam que ocorreu uma taxa extremamente alta de paginação de memória ativa do ou no disco durante a execução de criação de perfil. Geralmente, taxas de paginação nesse nível afetam a capacidade de resposta e o desempenho do aplicativo. Considere a redução das alocações de memória revisando os algoritmos. Talvez você também precise considerar os requisitos de memória do aplicativo. execução da criação de perfil novamente em um computador com mais memória.  
  
## <a name="rule-description"></a>Descrição da Regra  
 A paginação excessiva em disco pode ser causada pela memória física insuficiente. Se as operações de paginação dominarem o uso do disco físico em que o arquivo de paginação reside, elas poderão deixar mais lentas outras operações de disco orientadas por aplicativo no mesmo disco.  
  
 Com frequência, as páginas são lidas do disco ou gravadas no disco em operações de paginação em massa. O número de Saída de páginas/s é frequentemente muito maior do que o número de Gravações de página/s, por exemplo. Pois a Saída de páginas/s também inclui as páginas de dados alterados do cache de arquivos do sistema. No entanto, nem sempre é fácil determinar qual processo é diretamente responsável pela paginação e por quê.  
  
> [!NOTE]
>  Essa regra é acionada quando os níveis de paginação de memória ativa atingem uma taxa muito alta. Quando o nível de paginação é significativo, mas não extremo, a regra informativa [DA0017: altas taxas de paginação de memória ativa em disco](../profiling/da0017-high-rates-of-paging-active-memory-to-disk.md) é acionada.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Clique duas vezes na mensagem da janela Lista de Erros para navegar para a exibição [Marcas](../profiling/marks-view.md). Encontre a coluna **Memória\Páginas/s**. Determine se há fases específicas da execução do programa em que a atividade de E/S de paginação é mais pesada do que em outras.  
  
 Se estiver coletando dados de perfil para um aplicativo ASP.NET em um cenário de teste de carga, tente executar novamente o teste de carga em um computador configurado com memória física (ou RAM) adicional.  
  
 Considere a redução das alocações de memória revisando os algoritmos e evitando APIs de uso intensivo de memória, como String.Concat e String.Substring.



