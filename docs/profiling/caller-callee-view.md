---
title: Exibição de chamador-computador chamado | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.callercallee
helpviewer_keywords:
- profiling tools, reports, Caller/Callee view
- profiling tools, Caller/Callee view
- performance reports, Caller/Callee view
- Caller/Callee view
ms.assetid: d3511bcf-cce0-4cbe-aecb-b94c7c80ad1b
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: bab816a0b71adef190a7d919b5ada7138a6a0e7c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "74779708"
---
# <a name="callercallee-view"></a>exibição Chamador/Receptor
A exibição de Chamador/Computador Chamado exibe informações de perfil para uma função selecionada e suas funções pai e filho. A exibição de Chamador/Computador Chamado contém três grades:

 **Função atual** é exibida na grade intermediária e mostra informações de criação de perfil para a função selecionada. Os valores incluem todas as chamadas para a função que foram coletadas na execução de criação de perfil.

 **Funções que chamaram a função atual** são exibidas na grade superior e mostram o número dos valores da função selecionada (atual) gerados por chamadas da função de chamador (pai).

 **Funções que foram chamadas pela função atual** são exibidas na grade inferior e mostram informações de criação de perfil para as funções do computador chamado (filho) da função selecionada quando a função filho foi chamada pela função atual.

 As colunas que estão disponíveis na exibição de Chamador/Computador Chamado dependem do método de criação de perfil (amostragem ou instrumentação) usado para coletar os dados e de se os dados de memória do .NET foram coletados na execução da criação de perfil.

 Você pode selecionar uma função diferente para ser a Função Atual na parte do meio da exibição de Relatório clicando duas vezes em qualquer uma das funções listadas nas outras duas partes da exibição. A exibição de Relatório é atualizada automaticamente para refletir as alterações.

 Você pode classificar os dados clicando em nomes de coluna. Colunas adicionais podem ser incluídas na exibição de Chamador/Computador Chamado. Para obter mais informações, consulte [como: Personalizar colunas de exibição de relatório](../profiling/how-to-customize-report-view-columns.md).

## <a name="see-also"></a>Confira também
- [Exibição do chamador/chamado – dados de amostragem](../profiling/caller-callee-view-sampling-data.md)
- [Exibição do chamador/receptor-dados de instrumentação](../profiling/caller-callee-view-instrumentation-data.md)
- [Exibição do chamador/receptor-dados de instrumentação de memória .NET](../profiling/caller-callee-view-net-memory-instrumentation-data.md)
- [Exibição Caller/Callee-dados de amostragem de memória .NET](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)
- [Exibição do Chamador/Receptor– dados de contenção](../profiling/caller-callee-view-contention-data.md)
