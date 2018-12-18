---
title: Exibição de Funções – Dados de Contenção | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Functions view
ms.assetid: 208773b0-1a54-4b7a-ad37-2b6fd4f731d4
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b7444a4d3e8ad6e3f5fdd91d34058e20e13caf38
ms.sourcegitcommit: 269b55b413d2c82e6aa56c6ab8e53da7926fb2e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35237536"
---
# <a name="functions-view---contention-data"></a>Exibição Funções – dados de contenção
A exibição de relatório de Funções de dados de contenção lista as funções na execução de criação de perfil que foram bloqueadas da execução durante o processo de criação de perfil.  
  
 A tabela a seguir explica os valores que são exibidos na exibição de Funções de um arquivo de dados de criação de perfil que foi coletado usando o método de simultaneidade.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Bloqueado Exclusivo**|A quantidade de tempo durante a qual essa função foi impedida de executar o código no corpo da função. Não inclui o tempo bloqueado nas funções que foram chamadas pela função.|  
|**% de Tempo Bloqueado Exclusivo**|O percentual de todo o tempo bloqueado na execução da criação de perfil que representou o tempo bloqueado exclusivo desta função.|  
|**Contenções Exclusivas**|A quantidade de vezes que essa função foi impedida de executar o código no corpo da função. As contenções em funções que foram chamadas pela função não estão incluídas.|  
|**% de Contenções Exclusivas**|O percentual de todas as contenções na execução de criação de perfil era de contenções exclusivas desta função.|  
|**Endereço da Função**|O endereço da função.|  
|**Nome da Função**|O nome totalmente qualificado da função.|  
|**Tempo Bloqueado Inclusivo**|A hora em que essa função ou uma função que foi chamada por esta função foi impedida de executar.|  
|**% de Tempo Bloqueado Inclusivo**|O percentual de todo o tempo bloqueado na execução da criação de perfil que representou o tempo bloqueado inclusivo desta função ou módulo.|  
|**Contenções Inclusivas**|O número de vezes que essa função ou uma função que foi chamada por esta função foi impedida de executar.|  
|**% de Contenções Inclusivas**|O percentual de todas as contenções na execução de criação de perfil que eram contenções inclusivas dessa função ou módulo.|  
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|  
|**Nome do Módulo**|O nome do módulo que contém a função.|  
|**Caminho do Módulo**|O demarcador do módulo que contém a função.|  
|**ID do Processo**|A PID (ID do processo) do processo no qual a função estava sendo executada.|  
|**Nome do Processo**|O nome do processo.|  
|**Arquivo de Origem**|O arquivo de origem que contém a definição dessa função.|  
  
## <a name="see-also"></a>Consulte também  
 [Como personalizar as colunas de exibição de relatório](../profiling/how-to-customize-report-view-columns.md)   
 [Exibição de Funções](../profiling/functions-view.md)   
 [Exibição Funções – instrumentação](../profiling/functions-view-dotnet-memory-instrumentation-data.md)   
 [Exibição Funções – amostragem](../profiling/functions-view-dotnet-memory-sampling-data.md)   
 [Exibição de Funções](../profiling/functions-view-instrumentation-data.md)   
 [Exibição Funções](../profiling/functions-view-sampling-data.md)