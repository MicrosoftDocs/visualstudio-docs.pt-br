---
title: Criando relatórios básicos de criação de perfil por meio da linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6d73e21e-c04e-48ea-91cc-e517a5f2cd3f
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 30361f0f4ae147458252400a5232a657574553d4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51786751"
---
# <a name="creating-basic-profiling-reports-from-the-command-line"></a>Criando relatórios de criação de perfil básicos a partir da linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve os comandos básicos do VSPerfReport que geram relatórios de valores separados por vírgulas (.csv) de um arquivo de dados de criação de perfil .vsp ou .vsps. Para obter uma descrição de todas as opções de relatório, consulte [VSPerfReport](../profiling/vsperfreport.md).  
  
## <a name="report-commands"></a>Relatar Comandos  
 Use um dos comandos a seguir para criar um relatório para um arquivo de dados de criação de perfil especificado.  
  
 **VSPerfReport** `VSPFile` **/Summary:All**  
 Gera todos os relatórios disponíveis para o arquivo .vsp ou .vsps.  
  
 **VSPerfReport** `VSPFile` **/Summary:**`ReportType`[,`ReportType`...]  
 Gera os tipos de relatório especificados.  
  
 **VSPerfReport** `VSPFile` **/CallTrace**  
 Gera um relatório que lista cada evento de coleta de dados. Apenas instrumentação.  
  
## <a name="summary-report-type-parameters"></a>Parâmetros de Tipo de Relatório de Resumo  
 A tabela a seguir descreve os relatórios são gerados pela opção de tipo de relatório especificado. As colunas de um relatório dependem do método de criação de perfil usado para coletar os dados.  
  
|Parâmetro de Resumo|Descrição do Relatório|Referência de Relatório|  
|-----------------------|------------------------|----------------------|  
|**CallerCallee**|Representa os relacionamentos de pai/filho entre funções.|-   [Dados de Amostragem](../profiling/caller-callee-view-sampling-data.md)<br />-   [Dados de Instrumentação](../profiling/caller-callee-view-instrumentation-data.md)<br />-   [Dados de Amostragem de Memória do .NET](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)<br />-   [Dados de Instrumentação de Memória do .NET](../profiling/caller-callee-view-net-memory-instrumentation-data.md)<br />-   [Dados de Contenção](../profiling/caller-callee-view-contention-data.md)|  
|**Função**|Lista dados de criação de perfil por função.|-   [Dados de Amostragem](../profiling/functions-view-sampling-data.md)<br />-   [Dados de Instrumentação](../profiling/functions-view-instrumentation-data.md)<br />-   [Dados de Amostragem de Memória do .NET](../profiling/functions-view-dotnet-memory-sampling-data.md)<br />-   [Dados de Instrumentação de Memória do .NET](../profiling/functions-view-dotnet-memory-instrumentation-data.md)<br />-   [Dados de Contenção](../profiling/functions-view-contention-data.md)|  
|**CallTree**|Representa os caminhos de execução e os dados de criação de perfil de funções na execução de criação de perfil.|-   [Dados de Instrumentação](../profiling/call-tree-view-instrumentation-data.md)<br />-   [Dados de Amostragem](../profiling/call-tree-view-sampling-data.md)<br />-   [Dados de Amostragem de Memória do .NET](../profiling/call-tree-view-dotnet-memory-sampling-data.md)<br />-   [Dados de Instrumentação de Memória do .NET](../profiling/call-tree-view-dotnet-memory-instrumentation-data.md)<br />-   [Dados de Contenção](../profiling/call-tree-view-contention-data.md)|  
|**Contador**|Lista marcas de criação de perfil e valores de contador de desempenho do Windows que foram coletados durante a execução da criação de perfil.|-   [Exibição de Marcas](../profiling/marks-view.md)|  
|**Ip**|Lista dados de criação de perfil por instrução.|-   [Dados de Amostragem](../profiling/instruction-pointers-ips-view-sampling-data.md)<br />-   [Dados de Amostragem de Memória do .NET](../profiling/instruction-pointers-ips-view-dotnet-memory-sampling-data.md)<br />-   [Dados de Contenção](../profiling/instruction-pointers-ips-view-contention-data.md)|  
|**Vida Útil**|Lista o tempo de vida de objetos alocados.|-   [Exibição do Tempo de Vida do Objeto](../profiling/object-lifetime-view.md)|  
|**Linha**|Lista dados de criação de perfil por linha de código-fonte.|-   [Dados de Amostragem](../profiling/lines-view-sampling-data.md)<br />-   [Dados de Amostragem de Memória do .NET](../profiling/lines-view-dotnet-memory-sampling-data.md)<br />-   [Dados de Contenção](../profiling/lines-view-contention-data.md)|  
|**Cabeçalho**|Informações de cabeçalho do arquivo de dados de criação de perfil.|Específico ao arquivo.|  
|**Marca**|Marcas de criação de perfil coletadas na execução de criação de perfil.|-   [Exibição de Marcas](../profiling/marks-view.md)|  
|**Módulo**|Lista dados de criação de perfil para módulos.|-   [Dados de Amostragem](../profiling/modules-view-sampling-data.md)<br />-   [Dados de Instrumentação](../profiling/modules-view-instrumentation-data.md)<br />-   [Dados de Amostragem de Memória do .NET](../profiling/modules-view-dotnet-memory-sampling-data.md)<br />-   [Dados de Instrumentação de Memória do .NET](../profiling/modules-view-dotnet-memory-instrumentation-data.md)<br />-   [Dados de Contenção](../profiling/modules-view-contention-data.md)|  
|**Processo**|Lista dados de criação de perfil para processos.|-   [Exibição do Processo](../profiling/process-view.md)<br />-   [Dados de Contenção](../profiling/process-view-contention-data.md)|  
|**Thread**|Lista dados de criação de perfil para threads.|-   [Exibição do Processo](../profiling/process-view.md)|  
|**Tipo**|Lista dados de criação de perfil de alocação por tipo.|-   [Exibição de Alocações](../profiling/dotnet-memory-allocations-view.md)|  
|**Contenção**|Contenções de recursos.|-   [Contenções de Recursos](../profiling/resource-contentions-view-contention-data.md)|  
|**RuleWarnings**|Lista problemas de regra de desempenho.|- Lista CheckId, a descrição e o local do código-fonte do problema da regra.|  
|**ETW**|Lista eventos de Rastreamento de Eventos para Windows (ETW) coletados na execução da criação de perfil.|-   [Relatório de ETW](../profiling/event-tracing-for-windows-etw-report.md)|



