---
title: Criação de perfil de linha de comando de aplicativos autônomos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- profillng tools,stand-alone applications
- profling stand-alone applications
ms.assetid: a47f2bf2-186d-4120-bb79-34e2f3a1ee42
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1def2cea8727502af32814d18c34ab36e27e3596
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49938065"
---
# <a name="command-line-profiling-of-stand-alone-applications"></a>Criação de perfil de linha de comando para aplicativos autônomos
Esta seção descreve os procedimentos e as opções para coletar dados de desempenho para aplicativos autônomos (clientes) usando as Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] na linha de comando.  

## <a name="common-tasks"></a>Tarefas comuns  

| Tarefa | Conteúdo relacionado |
| - | - |
| **Coletar estatísticas do aplicativo:** use o método de amostragem para coletar estatísticas de desempenho. Os dados de amostragem são úteis para analisar problemas de utilização de CPU e para entender as características de desempenho geral de um aplicativo. | -   [Coletar estatísticas do aplicativo usando amostragem](../profiling/collecting-application-statistics-for-stand-alone-applications.md) |
| **Coletar dados de tempo detalhados:** use o método de instrumentação para coletar informações de tempo detalhadas. Os dados de instrumentação são úteis para analisar problemas de E/S e para análise refinada de cenários de aplicativo. | -   [Coletar dados de tempo detalhados usando a instrumentação](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application.md) |
| **Coletar dados de memória do .NET:** use a amostragem ou a instrumentação para coletar dados de alocação de memória do .NET que mostra o tamanho e o número de objetos alocados. Também é possível coletar dados de tempo de vida do objeto que mostram o tamanho e o número de objetos recuperados em cada geração de coleta de lixo. | -   [Coletar dados de memória do .NET Framework](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications.md) |
| **Coletar dados de simultaneidade:** use o método de simultaneidade para coletar dados de contenção de recursos e dados de atividade do thread que mostram a utilização da CPU, contenção e migração de threads, atrasos na sincronização, áreas de E/S sobrepostas e outros eventos do sistema. | -   [Coletar dados de simultaneidade](../profiling/collecting-concurrency-data-for-stand-alone-applications.md) |
| **Adicionar dados de interação de camada:** é possível adicionar dados de desempenho sobre chamadas ADO.NET síncronas que o aplicativo efetuou para um banco de dados [!INCLUDE[ssNoVersion](../data-tools/includes/ssnoversion_md.md)] da Microsoft. Adicionar dados de interação de camada a uma execução de criação de perfil requer procedimentos específicos com ferramentas de criação de perfil de linha de comando. | -   [Coletar dados de interação entre camadas](../profiling/adding-tier-interaction-data-from-the-command-line.md) |
| **Experimente:** use procedimentos passo a passo para criar o perfil de um aplicativo cliente de exemplo usando o método de amostragem ou de instrumentação. | -   [Passo a passo: criação de perfil de linha de comando usando amostragem](../profiling/walkthrough-command-line-profiling-using-sampling.md)<br />-   [Passo a passo: criação de perfil de linha de comando usando instrumentação](../profiling/walkthrough-command-line-profiling-using-instrumentation.md) |

## <a name="related-tasks"></a>Tarefas relacionadas  

|Tarefa|Conteúdo relacionado|  
|----------|---------------------|  
|**Aplicativos ASP.NET do perfil**|-   [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)|  
|**Profile services (Serviços de perfil)**|-   [Profile services (Serviços de perfil)](../profiling/command-line-profiling-of-services.md)|