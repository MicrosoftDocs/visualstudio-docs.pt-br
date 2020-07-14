---
title: Coletar estatísticas para aplicativos Web ASP.NET | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- profiling tools, sampling method
- sampling profling method
ms.assetid: f8383ab1-eb49-4d3f-8608-d8b4d51a81be
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: 8f353f551b3b524cfa49fb2cb638c261dcde660d
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85331923"
---
# <a name="collect-statistics-for-aspnet-web-apps"></a>Coletar estatísticas para aplicativos Web ASP.NET

Esta seção descreve os procedimentos e as opções para coletar estatísticas de desempenho de um aplicativo Web ASP .NET usando a ferramenta de linha de comando **VSPerfASPNETCmd** e **VSPerfCmd** e o método de criação de perfil de amostragem.

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

> [!NOTE]
> Embora a ferramenta **VSPerfCmd** forneça acesso completo à funcionalidade de Ferramentas de Criação de Perfil, inclusive pausar e retomar a criação de perfil e coletar outros dados do processador e de contadores de desempenho do Windows, você deverá usar a ferramenta de linha de comando **VSPerfASPNETCmd** quando não precisar dessa funcionalidade. A ferramenta de linha de comando **VSPerfASPNETCmd** é o método de preferência quando você está criando o perfil de sites da Web ASP.NET usando o criador de perfil autônomo. Em comparação com a ferramenta de linha de comando [VSPerfCmd](../profiling/vsperfcmd.md), nenhuma variável de ambiente precisa ser definida nem é necessário reiniciar o computador. Para saber mais, confira [Criação de perfil de site rápida com VSPerfASPNETCmd](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md).

## <a name="common-tasks"></a>Tarefas comuns

|Tarefa|Conteúdo relacionado|
|----------|---------------------|
|**Attach the profiler to an ASP.NET application (Anexar o criado de perfil a um aplicativo ASP.NET)**|-   [Como: anexar o criador de perfil a um aplicativo Web ASP.NET para coletar estatísticas de aplicativo](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-application-statistics-by-using-the-command-line.md)|

## <a name="related-tasks"></a>Tarefas relacionadas

### <a name="profile-aspnet-web-applications"></a>Criar o perfil de aplicativos Web ASP.NET

|Tarefa|Conteúdo relacionado|
|----------|---------------------|
|**Criar perfil usando o método de instrumentação**|-   [Coletar dados de tempo detalhados usando a instrumentação](../profiling/collecting-detailed-timing-data-aspnet-profiler-instrumentation-method.md)|
|**Profile memory allocation and garbage collection (Alocação de memória de perfil e coleta de lixo)**|-   [Coletar dados de memória](../profiling/collecting-memory-data-from-an-aspnet-web-application.md)|
|**Criar perfil de contenção de recursos e atividade de thread**|-   [Coletar dados de simultaneidade](../profiling/collecting-concurrency-data-for-an-aspnet-web-application.md)|

### <a name="sample-method"></a>Método de exemplo

|Tarefa|Conteúdo relacionado|
|----------|---------------------|
|**Criar o perfil de aplicativos autônomos (clientes)**|-   [Coletar estatísticas do aplicativo usando amostragem](../profiling/collecting-application-statistics-for-stand-alone-applications.md)|
|-   **Profile services (Serviços de perfil)**|-   [Coletar estatísticas do aplicativo usando amostragem](../profiling/collecting-application-statistics-for-services-by-using-the-profiler-sampling-method.md)|

### <a name="analyze-sampling-data-views-and-reports"></a>Analisar exibições e relatórios dos dados de amostragem
- [Exibições de dados do método de amostragem](../profiling/profiler-sampling-method-data-views.md)
