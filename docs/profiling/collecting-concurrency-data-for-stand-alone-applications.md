---
title: Linha de comando do criador de perfil para os obter os dados de simultaneidade do aplicativo Web autônomo
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- concurrency profiling method
- profiling tools,concurrency method
ms.assetid: 0a2c6d8a-50b3-48aa-b617-9137b049d21e
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 15e8be092a8e1e065f2aa1a80be7447a370974b0
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85331868"
---
# <a name="collect-concurrency-data-for-stand-alone-applications-by-using-the-profiler-command-line"></a>Coletar dados de simultaneidade para aplicativos autônomos usando a linha de comando do criador de perfil
O método de simultaneidade das Ferramentas de Criação de Perfil [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] permite coletar dados de contenção de recursos e dados de atividade do thread que mostram a utilização da CPU, contenção e migração do thread, atrasos na sincronização, áreas de ES sobrepostas e outros eventos do sistema.

## <a name="common-tasks"></a>Tarefas comuns

|Tarefa|Conteúdo relacionado|
|----------|---------------------|
|**Start a .NET Framework application and profile concurrency data (Iniciar um aplicativo do .NET Framework e criar o perfil de dados de simultaneidade)**|-   [Como iniciar um aplicativo de .NET Framework para coletar dados de simultaneidade](../profiling/how-to-launch-a-stand-alone-dotnet-framework-app-to-collect-concurrency-data.md)|
|**Start a C/C++ application and profile concurrency data (Iniciar um aplicativo C/C++ e criar o perfil de dados de simultaneidade)**|-   [Como iniciar um aplicativo nativo para coletar dados de simultaneidade](../profiling/how-to-launch-a-stand-alone-native-application-to-collect-concurrency-data.md)|
|**Attach the profiler to a running .NET Framework application (Anexar o criador de perfil a um aplicativo do .NET Framework em execução)**|-   [Como: anexar o criador de perfil a um aplicativo .NET Framework para coletar dados de simultaneidade](../profiling/how-to-attach-the-profiler-to-a-dotnet-app-and-collect-concurrency-data.md)|
|**Attach the profiler to a running C/C++ application (Anexar o criador de perfil a um aplicativo C/C++ em execução)**|-   [Como: anexar o criador de perfil a um aplicativo nativo e coletar dados de simultaneidade](../profiling/how-to-attach-the-profiler-to-a-native-app-and-collect-concurrency-data.md)|

## <a name="related-tasks"></a>Tarefas relacionadas

### <a name="profile-stand-alone-applications"></a>Criar perfil de aplicativos autônomos

|Tarefa|Conteúdo relacionado|
|----------|---------------------|
|**Criar perfil usando o método de amostragem**|-   [Coletar estatísticas do aplicativo usando amostragem](../profiling/collecting-application-statistics-for-stand-alone-applications.md)|
|**Criar perfil usando o método de instrumentação**|-   [Coletar dados de tempo detalhados usando a instrumentação](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application.md)|
|**Profile .NET memory allocation and garbage collection (Criar o perfil de alocação de memória e coleta de lixo do .NET)**|-   [Coletar dados de memória do .NET Framework](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications.md)|
|**Adicionar dados de interação de camada**|-   [Coletar dados de interação de camada](../profiling/adding-tier-interaction-data-from-the-command-line.md)|

### <a name="profile-concurrency-issues"></a>Criar perfil de problemas de simultaneidade

|Tarefa|Conteúdo relacionado|
|----------|---------------------|
|**Aplicativos ASP.NET do perfil**|-   [Coletar dados de simultaneidade](../profiling/collecting-concurrency-data-for-an-aspnet-web-application.md)|
|**Profile services (Serviços de perfil)**|-   [Coletar dados de simultaneidade](../profiling/collecting-concurrency-data-for-a-service-by-using-the-profiler-command-line.md)|

### <a name="analyze-concurrency-data-views-and-reports"></a>Analisar modos de exibição e relatórios de Dados de Simultaneidade
- [Exibições de dados de contenção de recursos](../profiling/resource-contention-data-views.md)

- [Visualizador de Simultaneidade](../profiling/concurrency-visualizer.md)

## <a name="reference"></a>Referência
- [Referência de ferramentas de criação de perfil de linha de comando](../profiling/command-line-profiling-tools-reference.md)
