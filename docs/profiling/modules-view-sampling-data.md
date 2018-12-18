---
title: Exibição Módulo – dados de amostragem | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Modules view
- sampling profiling method,Modules view
ms.assetid: 816f5633-65d7-41e5-aee1-033628d4e2df
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 97b3289119ec77c191d540285b235bab443ab6f3
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35256862"
---
# <a name="modules-view---sampling-data"></a>Exibição Módulos – dados de amostragem
A exibição Módulos dos dados de amostragem mostra dados de desempenho agrupados pelos módulos que tiveram a amostragem realizada nos dados de criação de perfil. Cada módulo é a raiz de uma árvore hierárquica. As funções que tiveram a amostragem realizada do módulo são listadas abaixo do nó do módulo.  
  
> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).  
  
 Se a função estava em execução quando amostras foram coletadas (ou seja, a função estava na parte superior da pilha de chamadas), as linhas de origem e os endereços de instrução que estavam em execução são listados sob o nó de função. Como os dados são coletados para uma linha de origem ou um ponteiro de instrução quando a linha ou a instrução está em execução, os valores exclusivos e inclusivos são sempre os mesmos dados de linha e dados de instrução.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Nome**|O nome do módulo, função, número de linha ou endereço de ponteiro de instrução.|  
|**ID do Processo**|A ID de processo (PID) da criação de perfil.|  
|**Nome do Processo**|O nome do processo.|  
|**Nome do Módulo**|O nome do módulo que contém a função, linha ou ponteiro de instrução.|  
|**Caminho do Módulo**|O caminho do módulo que contém o módulo, função, linha ou ponteiro de instrução.|  
|**Arquivo de Origem**|O arquivo de origem que contém a definição dessa função.|  
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|  
|**Amostras Inclusivas**|– Para uma função, o número de amostras em que estava executando essa função ou uma função que foi chamada por essa função; ou seja, o número de amostras da pilha de chamadas que continham essa função.<br />– Para um módulo, o número de amostras em que pelo menos uma função do módulo estava sendo executada.<br />– Para uma linha ou instrução, o número de amostras no qual essa linha ou instrução estava sendo executada.|  
|**% de Amostras Inclusivas**|– Para uma função ou módulo, o percentual de todas as amostras na execução de criação de perfil que eram amostras inclusivas dessa função ou módulo.<br />– Para uma linha ou instrução, o percentual de todas as amostras na execução de criação de perfil em que essa linha ou instrução estava em execução.|  
|**Amostras Exclusivas**|– Para uma função, o número de amostras da pilha de chamadas em que essa função estava diretamente em execução, isto é, o número de amostras em que essa função estava na parte superior da pilha de chamadas.<br />– Para um módulo, a soma das amostras exclusivas das funções no módulo.<br />– Para uma linha ou instrução, o número de amostras no qual essa linha ou instrução estava sendo executada.|  
|**% de Amostras Exclusivas**|– Para uma função ou módulo, o percentual de todas as amostras na execução de criação de perfil que eram amostras exclusivas dessa função ou módulo.<br />– Para uma linha ou instrução, o percentual de todas as amostras na execução de criação de perfil em que essa linha ou instrução estava em execução.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibição Módulos – amostragem](../profiling/modules-view-dotnet-memory-sampling-data.md)   
 [Exibição Módulos – instrumentação](../profiling/modules-view-dotnet-memory-instrumentation-data.md)   
 [Exibição Módulos](../profiling/modules-view-instrumentation-data.md)