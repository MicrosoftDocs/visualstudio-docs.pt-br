---
title: Usando Métodos da Criação de Perfil para Coletar Dados de Desempenho por meio da Linha de Comando | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 5613fafc-f298-4e7a-9a2d-a853b61cdf9c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5e8dbaf62043897292afbb2805879e0447f3048a
ms.sourcegitcommit: 8d38d5d2f2b75fc1563952c0d6de0fe43af12766
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/26/2018
ms.locfileid: "39276696"
---
# <a name="use-profiling-methods-to-collect-performance-data-from-the-command-line"></a>Usar métodos de criação de perfil para coletar dados de desempenho por meio da linha de comando
A escolha de [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] Ferramentas de Criação de Perfil, ferramentas e opções de linha de comando depende de fatores como o tipo de aplicativo para o qual você está criando um perfil, o método de criação de perfil que você deseja usar e se o aplicativo de destino é gravado no formato nativo ou em código [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)].  
  
 Este tópico organiza os tópicos de procedimentos de linha de comando acordo com o método de criação de perfil que você escolher.  
  
## <a name="use-the-sampling-method-to-collect-performance-statistics"></a>Usar o método de amostragem para coletar estatísticas de desempenho  
 O método de amostragem das Ferramentas de Criação de Perfil coleta dados de desempenho em intervalos especificados em uma execução de criação de perfil. A amostragem de dados pode fornecer informações sobre problemas de desempenho vinculados à CPU e pode ser uma boa maneira de começar a explorar o desempenho de um aplicativo.  
  
 Você pode iniciar o criador de perfil e o aplicativo ao mesmo tempo ou anexar o criador de perfil a uma instância de um aplicativo em execução.  
  
|Tarefa|Tipo de aplicativo de destino|  
|----------|-----------------------------|  
|**Iniciar um aplicativo**|-   [Aplicativos independentes](../profiling/how-to-launch-a-stand-alone-app-and-collect-application-statistics.md)|  
|**Anexar a um processo em execução**|-   [Aplicativos .NET Framework independentes](../profiling/how-to-attach-the-profiler-to-a-dotnet-app-and-collect-application-statistics.md)<br />-   [Aplicativos independentes nativos](../profiling/how-to-attach-the-profiler-to-a-native-app-and-collect-application-statistics.md)<br />-   [Aplicativos Web ASP.NET](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-application-statistics-by-using-the-command-line.md)<br />-   [Serviços do .NET](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-application-statistics-by-using-the-command-line.md)<br />-   [Serviços nativos](../profiling/how-to-attach-the-profiler-to-a-native-service-to-collect-application-statistics-by-using-the-command-line.md)|  
  
## <a name="use-the-instrumentation-method-to-collect-detailed-timing-data"></a>Usar o método de instrumentação para coletar dados de tempo detalhados  
 O método de instrumentação das Ferramentas de Criação de Perfil coleta dados de desempenho de cópias de binários de aplicativos que contêm sondas de software para gravar informações de desempenho. Dados de instrumentação são coletados no início e no final de cada função instrumentada e em cada chamada para outras funções da função instrumentada. O método de instrumentação é útil para descobrir problemas de desempenho com E/S, como o uso do disco.  
  
 O binário instrumentado é criado com a ferramenta [VInstr.exe](../profiling/vsinstr.md). Depois de inicializar o criador de perfil, os dados são coletados automaticamente dos binários instrumentados ao executar o aplicativo de destino.  
  
 **Tipo de Aplicativo de Destino**  
  
-   [Componentes independentes do .NET Framework](../profiling/how-to-instrument-a-dotnet-framework-component-and-collect-timing-data.md)  
  
-   [Componentes independentes nativos](../profiling/how-to-instrument-a-native-component-and-collect-timing-data.md)  
  
-   [Aplicativos Web ASP.NET compilados estaticamente](../profiling/how-to-instrument-statically-compiled-aspnet-and-collect-detailed-timing-data.md)  
  
-   [Aplicativos Web ASP.NET compilados dinamicamente](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-app-and-collect-timing-data.md)  
  
-   [Serviços do .NET](../profiling/how-to-instrument-a-dotnet-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line.md)  
  
-   [Serviços nativos](../profiling/how-to-instrument-a-native-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line.md)  
  
## <a name="use-net-memory-methods-to-collect-memory-allocation-and-object-lifetime-data"></a>Usar métodos de memória do .NET para coletar dados de alocação de memória e de tempo de vida do objeto  
 O método de memória do .NET das Ferramentas de Criação de Perfil permite que você colete dados de alocação de memória [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] e informações sobre o tempo de vida de objetos no [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)].  
  
 É possível iniciar o aplicativo de destino usando o criador de perfil; anexar o criador de perfil a uma instância em execução de um aplicativo; e criar versões instrumentadas do aplicativo para coletar informações detalhadas de tempo junto com os dados de memória [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)].  
  
|Tarefa|Tipo de aplicativo de destino|  
|----------|-----------------------------|  
|**Iniciar um aplicativo**|-   [Aplicativos .NET Framework independentes](../profiling/how-to-launch-a-stand-alone-dotnet-framework-app-to-collect-memory-data.md)|  
|**Anexar a um processo em execução**|-   [Aplicativos .NET Framework independentes](../profiling/how-to-attach-the-profiler-to-a-dotnet-framework-app-to-collect-memory-data.md)<br />-   [Aplicativos Web ASP.NET](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-memory-data-by-using-the-command-line.md)<br />-   [Serviços do .NET](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-memory-data-by-using-the-command-line.md)|  
|**Módulos de instrumento**|-   [Componentes independentes do .NET Framework](../profiling/how-to-instrument-a-dotnet-framework-component-and-collect-memory-data.md)<br />-   [Aplicativos Web ASP.NET compilados estaticamente](../profiling/how-to-instrument-a-statically-compiled-aspnet-app-and-collect-memory-data.md)<br />-   [Aplicativos Web ASP.NET compilados dinamicamente](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-memory-data.md)<br />-   [Serviços do .NET](../profiling/how-to-instrument-a-dotnet-framework-service-and-collect-memory-data-by-using-the-profiler-command-line.md)|  
  
## <a name="use-the-concurrency-method-to-collect-resource-contention-and-thread-activity-data"></a>Usar o método de simultaneidade para coletar dados de contenção de recurso e da atividade de thread  
 O método de simultaneidade das Ferramentas de Criação de Perfil permite que você colete dados de contenção de recursos, thread e atividade de processos de aplicativos com multithread.  
  
 Você pode iniciar o aplicativo por meio do criador de perfil ou anexar o criador de perfil a uma instância em execução de um aplicativo.  
  
|Tarefa|Tipo de aplicativo de destino|  
|----------|-----------------------------|  
|**Iniciar um aplicativo**|-   [Aplicativo .NET Framework independente](../profiling/how-to-launch-a-stand-alone-dotnet-framework-app-to-collect-concurrency-data.md)<br />-   [Aplicativo nativo independente](../profiling/how-to-launch-a-stand-alone-native-application-to-collect-concurrency-data.md)|  
|**Anexar a um processo em execução**|-   [Aplicativo .NET Framework independente](../profiling/how-to-attach-the-profiler-to-a-dotnet-app-and-collect-concurrency-data.md)<br />-   [Aplicativo independente nativo](../profiling/how-to-attach-the-profiler-to-a-native-app-and-collect-concurrency-data.md)<br />-   [Aplicativo Web ASP.NET](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-concurrency-data-by-using-the-command-line.md)<br />-   [Serviço do .NET](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-concurrency-data-by-using-the-command-line.md)<br />-   [Serviço nativo](../profiling/how-to-attach-the-profiler-to-a-native-service-to-collect-concurrency-data-by-using-the-command-line.md)|  
  
## <a name="add-tier-interaction-data-to-a-profiling-run"></a>Adicionar dados de interação de camada a uma execução de criação de perfil  
 Adicionar dados de interação de camada a uma execução de criação de perfil requer procedimentos específicos com ferramentas de criação de perfil de linha de comando. Confira [Coletar dados de interação de camada](../profiling/adding-tier-interaction-data-from-the-command-line.md)  
  
## <a name="see-also"></a>Consulte também  
 [Criar perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Profile services (Serviços de perfil)](../profiling/command-line-profiling-of-services.md)