---
title: Criando relatórios básicos de criação de perfil por meio da linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 6d73e21e-c04e-48ea-91cc-e517a5f2cd3f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d6b076023f725ac037ae5863bc8955e6952285ac
ms.sourcegitcommit: 4cd4aef53e7035d23e7d1d0f66f51ac8480622a1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34764901"
---
# <a name="create-basic-profiling-reports-from-the-command-line"></a>Criar relatórios básicos de criação de perfil por meio da linha de comando
Este artigo descreve os comandos básicos do VSPerfReport que geram relatórios de valores separados por vírgula (.*csv*) com base em um arquivo de dados de criação de perfil .*vsp* ou .*vsps*. Para obter uma descrição de todas as opções de relatório, consulte [VSPerfReport](../profiling/vsperfreport.md).  
  
## <a name="report-commands"></a>Comandos de relatório  
 Use um dos comandos a seguir para criar um relatório para um arquivo de dados de criação de perfil especificado.  
  
 **VSPerfReport** `VSPFile` **/Summary:All**  
 Gera todos os relatórios disponíveis para o arquivo .*vsp* ou .*vsps*.  
  
 **VSPerfReport** `VSPFile` **/Summary:**`ReportType`[,`ReportType`...]  
 Gera os tipos de relatório especificados.  
  
 **VSPerfReport** `VSPFile` **/CallTrace**  
 Gera um relatório que lista cada evento de coleta de dados. Apenas instrumentação.  
  
## <a name="summary-report-type-parameters"></a>Parâmetros de tipo de relatório de resumo  
 A tabela a seguir descreve os relatórios são gerados pela opção de tipo de relatório especificado. As colunas de um relatório dependem do método de criação de perfil usado para coletar os dados.  
  
|Parâmetro de Resumo|Descrição do Relatório|Referência de Relatório|  
|-----------------------|------------------------|----------------------|  
|**CallerCallee**|Representa os relacionamentos de pai/filho entre funções.|-   [Dados de amostragem](../profiling/caller-callee-view-sampling-data.md)<br />-   [Dados de instrumentação](../profiling/caller-callee-view-instrumentation-data.md)<br />-   [Dados de amostragem de memória do .NET](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)<br />-   [Dados de instrumentação de memória do .NET](../profiling/caller-callee-view-net-memory-instrumentation-data.md)<br />-   [Dados de contenção](../profiling/caller-callee-view-contention-data.md)|  
|**Função**|Lista dados de criação de perfil por função.|-   [Dados de amostragem](../profiling/functions-view-sampling-data.md)<br />-   [Dados de instrumentação](../profiling/functions-view-instrumentation-data.md)<br />-   [Dados de amostragem de memória do .NET](../profiling/functions-view-dotnet-memory-sampling-data.md)<br />-   [Dados de instrumentação de memória do .NET](../profiling/functions-view-dotnet-memory-instrumentation-data.md)<br />-   [Dados de contenção](../profiling/functions-view-contention-data.md)|  
|**CallTree**|Representa os caminhos de execução e os dados de criação de perfil de funções na execução de criação de perfil.|-   [Dados de instrumentação](../profiling/call-tree-view-instrumentation-data.md)<br />-   [Dados de amostragem](../profiling/call-tree-view-sampling-data.md)<br />-   [Dados de amostragem de memória do .NET](../profiling/call-tree-view-dotnet-memory-sampling-data.md)<br />-   [Dados de instrumentação de memória do .NET](../profiling/call-tree-view-dotnet-memory-instrumentation-data.md)<br />-   [Dados de contenção](../profiling/call-tree-view-contention-data.md)|  
|**Contador**|Lista marcas de criação de perfil e valores de contador de desempenho do Windows que foram coletados durante a execução da criação de perfil.|-   [Exibição de Marcas](../profiling/marks-view.md)|  
|**Ip**|Lista dados de criação de perfil por instrução.|-   [Dados de amostragem](../profiling/instruction-pointers-ips-view-sampling-data.md)<br />-   [Dados de amostragem de memória do .NET](../profiling/instruction-pointers-ips-view-dotnet-memory-sampling-data.md)<br />-   [Dados de contenção](../profiling/instruction-pointers-ips-view-contention-data.md)|  
|**Vida Útil**|Lista o tempo de vida de objetos alocados.|-   [Exibição do Tempo de Vida do Objeto](../profiling/object-lifetime-view.md)|  
|**Linha**|Lista dados de criação de perfil por linha de código-fonte.|-   [Dados de amostragem](../profiling/lines-view-sampling-data.md)<br />-   [Dados de amostragem de memória do .NET](../profiling/lines-view-dotnet-memory-sampling-data.md)<br />-   [Dados de Contenção](../profiling/lines-view-contention-data.md)|  
|**Cabeçalho**|Informações de cabeçalho do arquivo de dados de criação de perfil.|Específico ao arquivo.|  
|**Marca**|Marcas de criação de perfil coletadas na execução de criação de perfil.|-   [Exibição de Marcas](../profiling/marks-view.md)|  
|**Módulo**|Lista dados de criação de perfil para módulos.|-   [Dados de amostragem](../profiling/modules-view-sampling-data.md)<br />-   [Dados de instrumentação](../profiling/modules-view-instrumentation-data.md)<br />-   [Dados de amostragem de memória do .NET](../profiling/modules-view-dotnet-memory-sampling-data.md)<br />-   [Dados de Instrumentação de Memória do .NET](../profiling/modules-view-dotnet-memory-instrumentation-data.md)<br />-   [Dados de contenção](../profiling/modules-view-contention-data.md)|  
|**Processo**|Lista dados de criação de perfil para processos.|-   [Exibição do Processo](../profiling/process-view.md)<br />-   [Dados de contenção](../profiling/process-view-contention-data.md)|  
|**Thread**|Lista dados de criação de perfil para threads.|-   [Exibição do Processo](../profiling/process-view.md)|  
|**Tipo**|Lista dados de criação de perfil de alocação por tipo.|-   [Exibição de Alocações](../profiling/dotnet-memory-allocations-view.md)|  
|**Contenção**|Contenções de recursos.|-   [Contenções de recursos](../profiling/resource-contentions-view-contention-data.md)|  
|**RuleWarnings**|Lista problemas de regra de desempenho.|- Lista CheckId, a descrição e o local do código-fonte do problema da regra.|  
|**ETW**|Lista eventos de Rastreamento de Eventos para Windows (ETW) coletados na execução da criação de perfil.|-   [Relatório do ETW](../profiling/event-tracing-for-windows-etw-report.md)|