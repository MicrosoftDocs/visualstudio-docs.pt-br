---
title: Exibição de chamador-computador chamado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 973c65927e3732cff44ab8eecb684f3c75af8614
ms.sourcegitcommit: 209c2c068ff0975994ed892b62aa9b834a7f6077
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34264288"
---
# <a name="callercallee-view"></a>exibição do Chamador/Receptor
A exibição de Chamador/Computador Chamado exibe informações de perfil para uma função selecionada e suas funções pai e filho. A exibição de Chamador/Computador Chamado contém três grades:  
  
 **Função atual** é exibida na grade intermediária e mostra informações de criação de perfil para a função selecionada. Os valores incluem todas as chamadas para a função que foram coletadas na execução de criação de perfil.  
  
 **Funções que chamaram a função atual** são exibidas na grade superior e mostram o número dos valores da função selecionada (atual) gerados por chamadas da função de chamador (pai).  
  
 **Funções que foram chamadas pela função atual** são exibidas na grade inferior e mostram informações de criação de perfil para as funções do computador chamado (filho) da função selecionada quando a função filho foi chamada pela função atual.  
  
 As colunas que estão disponíveis na exibição de Chamador/Computador Chamado dependem do método de criação de perfil (amostragem ou instrumentação) usado para coletar os dados e de se os dados de memória do .NET foram coletados na execução da criação de perfil.  
  
 Você pode selecionar uma função diferente para ser a Função Atual na parte do meio da exibição de Relatório clicando duas vezes em qualquer uma das funções listadas nas outras duas partes da exibição. A exibição de Relatório é atualizada automaticamente para refletir as alterações.  
  
 Você pode classificar os dados clicando em nomes de coluna. Colunas adicionais podem ser incluídas na exibição de Chamador/Computador Chamado. Para saber mais, confira [Como personalizar colunas de exibição de relatório](../profiling/how-to-customize-report-view-columns.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibição do chamador/chamado – dados de amostragem](../profiling/caller-callee-view-sampling-data.md)   
 [Exibição do Chamador/Receptor – dados de instrumentação](../profiling/caller-callee-view-instrumentation-data.md)   
 [Exibição do Chamador/Receptor – dados de instrumentação da memória do .NET](../profiling/caller-callee-view-net-memory-instrumentation-data.md)   
 [Exibição do Chamador/Receptor – dados de amostragem da memória do .NET](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)   
 [Exibição do Chamador/Receptor– dados de contenção](../profiling/caller-callee-view-contention-data.md)