---
title: VSPerfCmd-obter dados de tempo para o aplicativo Web ASP.NET usando a instrumentação
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- profiling tools,instrumentation method
- instrumentation profiling method
ms.assetid: 29f2fc55-aaf7-4e18-a672-8815455fba73
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: 55f682152731391bdb0d4c0de0a307c00c16e2c7
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85331840"
---
# <a name="collect-detailed-timing-data-for-an-aspnet-web-application-using-the-profiler-instrumentation-method-from-the-command-line"></a>Coletar dados de tempo detalhados para um aplicativo Web ASP.NET usando o método de instrumentação do criador de perfil por meio da linha de comando
Esta seção descreve os procedimentos e opções para coletar dados de desempenho detalhados para um aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] usando a ferramenta **VSPerfCmd** da linha de comando e o método de instrumentação.

> [!NOTE]
> A ferramenta **VSPerfCmd** dá acesso completo à funcionalidade de Ferramentas de Criação de Perfil, inclusive pausar e retomar a criação de perfil e coletar dados adicionais do processador e de contadores de desempenho do Windows. Também é possível usar a ferramenta de linha de comando **VSPerfASPNETCmd** quando essa funcionalidade não for necessária. Em comparação com a ferramenta de linha de comando [VSPerfCmd](../profiling/vsperfcmd.md), nenhuma variável de ambiente precisa ser definida e não é necessário reinicializar o computador. Para saber mais, confira [Criação de perfil de site rápida com VSPerfASPNETCmd](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md).

## <a name="common-tasks"></a>Tarefas comuns

|Tarefa|Conteúdo relacionado|
|----------|---------------------|
|**Criar perfil para binários compilados estatisticamente**|-   [Como instrumentar um aplicativo ASP.NET compilado estaticamente e coletar dados de tempo detalhados](../profiling/how-to-instrument-statically-compiled-aspnet-and-collect-detailed-timing-data.md)|
|**Criar perfil para binários compilados dinamicamente**|-   [Como instrumentar um aplicativo ASP.NET compilado dinamicamente e coletar dados de tempo detalhados](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-app-and-collect-timing-data.md)|

## <a name="related-tasks"></a>Tarefas relacionadas

### <a name="profile-aspnet-web-applications"></a>Criar o perfil de aplicativos Web ASP.NET

|Tarefa|Conteúdo relacionado|
|----------|---------------------|
|**Criar perfil usando o método de amostragem**|-   [Coletar estatísticas do aplicativo usando amostragem](../profiling/collecting-application-statistics-for-aspnet-using-the-profiler-sampling-method.md)|
|**Profile memory allocation and garbage collection (Alocação de memória de perfil e coleta de lixo)**|-   [Coletar dados de memória](../profiling/collecting-memory-data-from-an-aspnet-web-application.md)|
|**Criar perfil de contenção de recursos e atividade de thread**|-   [Coletar dados de simultaneidade](../profiling/collecting-concurrency-data-for-an-aspnet-web-application.md)|

### <a name="profile-by-using-the-instrumentation-method"></a>Criar perfil usando o método de instrumentação

|Tarefa|Conteúdo relacionado|
|----------|---------------------|
|**Criar o perfil de aplicativos autônomos (clientes)**|-   [Coletar dados de tempo detalhados usando a instrumentação](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application.md)|
|**Profile services (Serviços de perfil)**|-   [Coletar dados de tempo detalhados usando a instrumentação](../profiling/collecting-detailed-timing-data-for-services-by-using-the-instrumentation-method.md)|

### <a name="analyze-instrumentation-data-views-and-reports"></a>Analisar modos de exibição e relatórios de dados de instrumentação
- [Exibições de dados do método de instrumentação](../profiling/instrumentation-method-data-views.md)
