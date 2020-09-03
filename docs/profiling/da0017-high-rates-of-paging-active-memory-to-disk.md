---
title: DA0017-taxas altas de paginação de memória ativa para o disco | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.17
- vs.performance.rules.DA0017
- vs.performance.DA0017
ms.assetid: 01011eec-5930-43b3-980d-2cb01e2ca7f6
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 06295c1b158fe25b481b2aa036f8448895c546f5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544697"
---
# <a name="da0017-high-rates-of-paging-active-memory-to-disk"></a>DA0017: Altas taxas de paginação de memória ativa para o disco

|Item|Valor|
|-|-|
|ID de regra|DA0017|
|Categoria|Memória e paginação|
|Método de criação de perfil|Tudo|
|Mensagem|Uma alta taxa de paginação de memória ativa em disco está ocorrendo. O aplicativo pode ser associado à memória.|
|Tipo de regra|Informações|

 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.

## <a name="cause"></a>Causa
 Os dados de desempenho do sistema coletados na execução de criação de perfil indicam que ocorreu uma taxa alta de paginação de memória ativa do ou no disco durante a execução de criação de perfil. Normalmente, taxas de paginação nesse nível afetarão a capacidade de resposta e o desempenho do aplicativo. Considere a redução das alocações de memória revisando os algoritmos. Talvez você também precise considerar os requisitos de memória do aplicativo.

## <a name="rule-description"></a>Descrição da regra

> [!NOTE]
> Essa regra informativa é acionada quando os níveis de paginação de memória ativa atingem uma quantidade significativa. Quando ocorre um nível extremamente alto de paginação, a regra de aviso [DA0014: taxas extremamente altas de paginação de memória ativa em disco](../profiling/da0014-extremely-high-rates-of-paging-active-memory-to-disk.md) é acionada.

 A paginação excessiva em disco pode ser causada pela memória física insuficiente. Se as operações de paginação dominarem o uso do disco físico em que o arquivo de paginação reside, elas poderão deixar mais lentas outras operações de disco orientadas por aplicativo no mesmo disco.

 Com frequência, as páginas são lidas do disco ou gravadas no disco em operações de paginação em massa. O número de Saída de páginas/s é geralmente muito maior do que o número de Gravações de página/s, por exemplo. Pois a Saída de páginas/s também inclui as páginas de dados alterados do cache de arquivos do sistema. No entanto, nem sempre é fácil determinar qual processo é diretamente responsável pela paginação e por quê.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Clique duas vezes na mensagem na janela Lista de Erros para navegar até o modo de exibição de [marcas](../profiling/marks-view.md) . Encontre a coluna **Memória\Páginas/s**. Determine se há fases específicas da execução do programa em que a atividade de E/S de paginação é mais pesada do que em outras.

 Se estiver coletando dados de perfil para um aplicativo ASP.NET em um cenário de teste de carga, tente executar novamente o teste de carga em um computador configurado com memória física (ou RAM) adicional.

 Considere a redução das alocações de memória revisando os algoritmos e evitando APIs de uso intensivo de memória, como String.Concat e String.Substring.
