---
title: Usando Métodos da Criação de Perfil para Coletar Dados de Desempenho por meio da Linha de Comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5613fafc-f298-4e7a-9a2d-a853b61cdf9c
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d853322762942e874528b35164dc3f04a6c22b0a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51722769"
---
# <a name="using-profiling-methods-to-collect-performance-data-from-the-command-line"></a>Usando métodos da criação de perfil para coletar dados de desempenho a partir da linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A escolha de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Ferramentas de Criação de Perfil, ferramentas e opções de linha de comando depende de fatores como o tipo de aplicativo para o qual você está criando um perfil, o método de criação de perfil que você deseja usar e se o aplicativo de destino é gravado no formato nativo ou em código [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].  
  
 Este tópico organiza os tópicos de procedimentos de linha de comando acordo com o método de criação de perfil que você escolher.  
  
## <a name="in-this-topic"></a>Neste tópico  
 [Usando o método de amostragem para coletar estatísticas de desempenho](#BKMK_Using_the_sampling_method_to_collect_performance_statistics)  
  
 [Usando o método de instrumentação para coletar dados de tempo detalhados](#BKMK_Using_the_instrumentation_method_to_collect_detailed_timing_data)  
  
 [Usando métodos de memória do .NET para coletar alocação de memória e dados de tempo de vida do objeto](#BKMK_Using__NET_memory_methods_to_collect_memory_allocation_and_object_lifetime_data)  
  
 [Usando o método de simultaneidade para coletar dados de contenção de recursos e de atividade de thread](#BKMK_Using_the_concurrency_method_to_collect_resource_contention_and_thread_activity_data)  
  
 [Adicionando dados de interação de camadas a uma execução de criação de perfil](#BKMK_Adding_tier_interaction_data_to_a_profiling_run)  
  
##  <a name="BKMK_Using_the_sampling_method_to_collect_performance_statistics"></a> Usando o método de amostragem para coletar estatísticas de desempenho  
 O método de amostragem das Ferramentas de Criação de Perfil coleta dados de desempenho em intervalos especificados em uma execução de criação de perfil. A amostragem de dados pode fornecer informações sobre problemas de desempenho vinculados à CPU e pode ser uma boa maneira de começar a explorar o desempenho de um aplicativo.  
  
 Você pode iniciar o criador de perfil e o aplicativo ao mesmo tempo ou anexar o criador de perfil a uma instância de um aplicativo em execução.  
  
|Tarefa|Tipo de aplicativo de destino|  
|----------|-----------------------------|  
|**Iniciar um aplicativo**|-   [Aplicativos Autônomos](../profiling/how-to-launch-a-stand-alone-application-with-the-profiler-and-collect-application-statistics-by-using-the-command-line.md)|  
|**Anexar a um processo em execução**|-   [Aplicativos Autônomos do .NET Framework](../profiling/how-to-attach-the-profiler-to-a-dotnet-framework-stand-alone-application-and-collect-application-statistics-by-using-the-command-line.md)<br />-   [Aplicativos Autônomos Nativos](../profiling/how-to-attach-the-profiler-to-a-native-stand-alone-application-and-collect-application-statistics-by-using-the-command-line.md)<br />-   [Aplicativos Web ASP.NET](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-application-statistics-by-using-the-command-line.md)<br />-   [Serviços .NET](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-application-statistics-by-using-the-command-line.md)<br />-   [Serviços Nativos](../profiling/how-to-attach-the-profiler-to-a-native-service-to-collect-application-statistics-by-using-the-command-line.md)|  
  
##  <a name="BKMK_Using_the_instrumentation_method_to_collect_detailed_timing_data"></a> Usando o método de instrumentação para coletar dados de tempo detalhados  
 O método de instrumentação das Ferramentas de Criação de Perfil coleta dados de desempenho de cópias de binários de aplicativos que contêm sondas de software para gravar informações de desempenho. Dados de instrumentação são coletados no início e no final de cada função instrumentada e em cada chamada para outras funções da função instrumentada. O método de instrumentação é útil para descobrir problemas de desempenho com E/S, como o uso do disco.  
  
 O binário instrumentado é criado com a ferramenta [VInstr.exe](../profiling/vsinstr.md). Depois de inicializar o criador de perfil, os dados são coletados automaticamente dos binários instrumentados ao executar o aplicativo de destino.  
  
 **Tipo de Aplicativo de Destino**  
  
-   [Componentes Autônomos do .NET Framework](../profiling/how-to-instrument-a-stand-alone-dotnet-framework-component-and-collect-timing-data-with-the-profiler-from-the-command-line.md)  
  
-   [Componentes Autônomos Nativos](../profiling/how-to-instrument-a-native-stand-alone-component-and-collect-timing-data-with-the-profiler-from-the-command-line.md)  
  
-   [Aplicativos Web do ASP.NET Compilados Estaticamente](../profiling/how-to-instrument-a-statically-compiled-aspnet-web-application-and-collect-detailed-timing-data-with-the-profiler-by-using-the-command-line.md)  
  
-   [Aplicativos Web do ASP.NET Compilados Dinamicamente](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-detailed-timing-data-with-the-profiler-by-using-the-command-line.md)  
  
-   [Serviços .NET](../profiling/how-to-instrument-a-dotnet-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line.md)  
  
-   [Serviços Nativos](../profiling/how-to-instrument-a-native-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line.md)  
  
##  <a name="BKMK_Using__NET_memory_methods_to_collect_memory_allocation_and_object_lifetime_data"></a> Usando métodos de memória do .NET para coletar alocação de memória e dados de tempo de vida do objeto  
 O método de memória do .NET das Ferramentas de Criação de Perfil permite que você colete dados de alocação de memória [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] e informações sobre o tempo de vida de objetos no [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].  
  
 É possível iniciar o aplicativo de destino usando o criador de perfil; anexar o criador de perfil a uma instância em execução de um aplicativo; e criar versões instrumentadas do aplicativo para coletar informações detalhadas de tempo junto com os dados de memória [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].  
  
|Tarefa|Tipo de aplicativo de destino|  
|----------|-----------------------------|  
|**Iniciar um aplicativo**|-   [Aplicativos Autônomos do .NET Framework](../profiling/how-to-launch-a-stand-alone-dotnet-framework-application-with-the-profiler-to-collect-memory-data-by-using-the-command-line.md)|  
|**Anexar a um processo em execução**|-   [Aplicativos Autônomos do .NET Framework](../profiling/how-to-attach-the-profiler-to-a-dotnet-framework-stand-alone-application-to-collect-memory-data-by-using-the-command-line.md)<br />-   [Aplicativos Web ASP.NET](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-memory-data-by-using-the-command-line.md)<br />-   [Serviços .NET](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-memory-data-by-using-the-command-line.md)|  
|**Módulos de instrumento**|-   [Componentes Autônomos do .NET Framework](../profiling/how-to-instrument-a-stand-alone-dotnet-framework-component-and-collect-memory-data-with-the-profiler-by-using-the-command-line.md)<br />-   [Aplicativos Web do ASP.NET Compilados Estaticamente](../profiling/how-to-instrument-a-statically-compiled-aspnet-web-application-and-collect-memory-data-by-using-the-profiler-command-line.md)<br />-   [Aplicativos Web do ASP.NET Compilados Dinamicamente](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-memory-data-by-using-the-profiler-command-line.md)<br />-   [Serviços .NET](../profiling/how-to-instrument-a-dotnet-framework-service-and-collect-memory-data-by-using-the-profiler-command-line.md)|  
  
##  <a name="BKMK_Using_the_concurrency_method_to_collect_resource_contention_and_thread_activity_data"></a> Usando o método de simultaneidade para coletar dados de contenção de recursos e de atividade de thread  
 O método de simultaneidade das Ferramentas de Criação de Perfil permite que você colete dados de contenção de recursos, thread e atividade de processos de aplicativos com multithread.  
  
 Você pode iniciar o aplicativo por meio do criador de perfil ou anexar o criador de perfil a uma instância em execução de um aplicativo.  
  
|Tarefa|Tipo de aplicativo de destino|  
|----------|-----------------------------|  
|**Iniciar um aplicativo**|-   [Aplicativo Autônomo do .NET Framework](../profiling/how-to-launch-a-stand-alone-dotnet-framework-application-with-the-profiler-to-collect-concurrency-data-by-using-the-command-line.md)<br />-   [Aplicativo Autônomo Nativo](../profiling/how-to-launch-a-stand-alone-native-application-with-the-profiler-to-collect-concurrency-data-by-using-the-command-line.md)|  
|**Anexar a um processo em execução**|-   [Aplicativo Autônomo do .NET Framework](../profiling/how-to-attach-the-profiler-to-a-dotnet-framework-stand-alone-application-to-collect-concurrency-data-by-using-the-command-line.md)<br />-   [Aplicativo Autônomo Nativo](../profiling/how-to-attach-the-profiler-to-a-native-stand-alone-application-and-collect-concurrency-data-by-using-the-command-line.md)<br />-   [Aplicativo Web ASP .NET](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-concurrency-data-by-using-the-command-line.md)<br />-   [Serviço do .NET](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-concurrency-data-by-using-the-command-line.md)<br />-   [Serviço Nativo](../profiling/how-to-attach-the-profiler-to-a-native-service-to-collect-concurrency-data-by-using-the-command-line.md)|  
  
##  <a name="BKMK_Adding_tier_interaction_data_to_a_profiling_run"></a> Adicionando dados de interação de camadas a uma execução de criação de perfil  
 Adicionar dados de interação de camada a uma execução de criação de perfil requer procedimentos específicos com ferramentas de criação de perfil de linha de comando. Consulte [Coletando dados de interação entre camadas](../profiling/adding-tier-interaction-data-from-the-command-line.md)  
  
## <a name="see-also"></a>Consulte também  
 [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)



