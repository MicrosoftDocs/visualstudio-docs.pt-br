---
title: Exibição de chamador/computador chamado – Dados de amostragem de memória do .NET | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Caller/Callee view
ms.assetid: 36f5b4de-5686-4f40-9e72-f4aee27d833c
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: edeccd8318de36a09a9191a30274ff342cb7a41d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51816782"
---
# <a name="callercallee-view---net-memory-sampling-data"></a>Exibição Chamador/Receptor da Chamada – dados de amostragem da memória do .NET
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A exibição de Chamador/Computador Chamado exibe dados de criação de perfil de memória do .NET para uma função selecionada e suas funções pai e filho. A exibição de Chamador/Computador Chamado contém três grades.  
  
 A **Função atual** é exibida na grade do meio exibe informações de criação de perfil de memória sobre a função selecionada. Os valores incluem todas as chamadas amostradas para a função.  
  
 **Funções que chamaram a função atual** são exibidas na grade superior e mostram a quantidade do valor da função selecionada (atual) gerado por chamadas da função do chamador (pai).  
  
 **Funções que foram chamadas pela função atual** são exibidas na grade inferior e mostram dados de criação de perfil de memória para as funções do computador chamado (filho) da função selecionada quando a função filho foi chamada pela função atual.  
  
 Clique duas vezes em uma linha de função de chamador ou computador chamado para tornar essa linha a função atual.  
  
|Column|Descrição|  
|------------|-----------------|  
|**ID do Processo**|A ID de processo (PID) da criação de perfil.|  
|**Nome do Processo**|O nome do processo.|  
|**Nome do Módulo**|O nome do módulo que contém a função.|  
|**Caminho do Módulo**|O demarcador do módulo que contém a função.|  
|**Arquivo de Origem**|O arquivo de origem que contém a definição dessa função.|  
|**Nome da Função**|O nome totalmente qualificado da função.|  
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|  
|**Endereço da Função**|O endereço da função.|  
|**Tipo**|O contexto da função:<br /><br /> **0** – a função atual<br /><br /> **1** – uma função que chama a função atual<br /><br /> **2** – uma função que é chamada pela função atual<br /><br /> Somente em relatórios de linha de comando [VSPerfReport](../profiling/vsperfreport.md).|  
|**Nível**|A profundidade da função na árvore de chamadas. Somente em relatórios de linha de comando [VSPerfReport](../profiling/vsperfreport.md).|  
|**Alocações Inclusivas**|–   Para a função atual, o número de objetos que foram alocados pela função na execução de criação de perfil. Esse número inclui objetos criados em funções do computador chamado.<br />–   Para uma função do chamador, o número das alocações inclusivas da função atual que foram geradas por chamadas dessa função.<br />–   Para uma função do computador chamado, o número de objetos alocados pela instância dessa função que foram chamados pela função atual. O número inclui alocações que foram feitas por funções chamadas pela função do computador chamado.|  
|**% de Alocações Inclusivas**|O percentual de todos os objetos que foram criados na execução de criação de perfil que eram alocações inclusivas dessa função.|  
|**Alocações Exclusivas**|– Para a função atual, o número de objetos que foram criados quando a função estava executando código do corpo da função (isto é, quando a função estava na parte superior da pilha de chamadas). O número não inclui objetos que foram criados em funções que foram chamadas pela função.<br />–   Para uma função do chamador, o número das alocações exclusivas da função atual que foram geradas por chamadas dessa função.<br />–   Para uma função do computador chamado, o número de objetos criados pelas instâncias dessa função que foram chamados pela função atual. O número não inclui os objetos alocados por funções criadas pela função do computador chamado.|  
|**% de Alocações Exclusivas**|O percentual de todos os objetos que foram criados na execução de criação de perfil que eram alocações inclusivas dessa função.|  
|**Bytes Inclusivos**|–   Para a função atual, o número de bytes de memória que foram alocados pela função na execução de criação de perfil. O número inclui memória foi alocada em funções que foram chamadas por essa função.<br />–   Para uma função do chamador, o número de bytes inclusivos da função atual que foram gerados por chamadas pela função do chamador.<br />–   Para uma função do computador chamado, o número de bytes alocados pelas instâncias dessa função que foram gerados por chamadas da função atual. O número inclui os bytes alocados por funções chamadas pela função do computador chamado.|  
|**% de Bytes Inclusivos**|O percentual de todos os bytes de memória que foram alocados na execução de criação de perfil que eram alocações inclusivas dessa função.|  
|**Bytes Exclusivos**|–   Para a função atual, o número de bytes de memória que foram alocados pela função na execução de criação de perfil. Esse número não inclui memória alocada por funções chamadas pela função atual.<br />–   Para uma função do chamador, o número de bytes exclusivos da função atual que foram gerados por chamadas da função do chamador.<br />–   Para uma função do computador chamado, o número de bytes alocados por instâncias da função que foram gerados por chamadas da função atual. O número não inclui os bytes alocados por funções chamadas pela função do computador chamado.|  
|**% de Bytes Exclusivos**|O percentual de todos os bytes de memória que foram alocados na execução de criação de perfil que eram alocações exclusivas dessa função.|  
  
## <a name="see-also"></a>Consulte também  
 [Como personalizar as colunas de exibição do relatório](../profiling/how-to-customize-report-view-columns.md)   
 [Exibição Chamador/Receptor da Chamada – dados de instrumentação da memória do .NET](../profiling/caller-callee-view-net-memory-instrumentation-data.md)   
 [Exibição de chamador/computador chamado – dados de amostragem](../profiling/caller-callee-view-sampling-data.md)   
 [Exibição de chamador/computador chamado – dados de instrumentação](../profiling/caller-callee-view-instrumentation-data.md)



