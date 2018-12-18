---
title: Criação de perfil de linha de comando dos aplicativos Web ASP.NET | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- profiling ASP.NET applications
- profling tools,ASP.NET applications
ms.assetid: 897c00d5-5767-433b-a960-4a29c6023ede
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5436da548acaf16169437fdc98b51d182891d2d9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51759161"
---
# <a name="command-line-profiling-of-aspnet-web-applications"></a>Criação de perfil de linha de comando dos aplicativos Web do ASP.NET
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esta seção descreve os procedimentos e as opções para coletar dados de desempenho para aplicativos Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] usando as Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] na linha de comando.  
  
> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos da Windows Store também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).  
  
## <a name="common-tasks"></a>Tarefas comuns  
  
|Tarefa|Conteúdo relacionado|  
|----------|---------------------|  
|**Coletar dados básicos de criação de perfil ASP.NET facilmente:** use a ferramenta **VSPerfASPNETCmd** para coletar dados de amostragem, de instrumentação, de memória do .NET, de contenção ou de interação de camadas sem os requisitos de configuração e reinicializações do IIS (Serviços de Informações da Internet) necessárias para **VSPerfCmd**. **VSPerfASPNETCmd** não permite coletar dados adicionais ou para controlar a coleta de dados. **Observação:** **VSPerfASPNETCmd** é a ferramenta de preferência para usar o criador de perfil autônomo para criar o perfil de sites Web ASP.NET.|-   [Criação de perfil de site rápida com VSPerfASPNETCmd](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)|  
|**Coletar estatísticas do aplicativo:** use o método de amostragem para coletar estatísticas de desempenho. Os dados de amostragem são úteis para analisar problemas de uso da CPU e para entender as características de desempenho geral de um aplicativo.|-   [Coletando estatísticas do aplicativo usando amostragem](../profiling/collecting-application-statistics-for-aspnet-web-applications-using-the-profiler-sampling-method-from-the-command-line.md)|  
|**Coletar dados de tempo detalhados:** use o método de instrumentação para coletar informações de tempo detalhadas. Os dados de instrumentação são úteis para analisar problemas de E/S e para análise refinada de cenários de aplicativo.|-   [Coletando dados de tempo detalhados usando a instrumentação](../profiling/collecting-detailed-timing-data-for-an-aspnet-web-application-using-the-profiler-instrumentation-method-from-the-command-line.md)|  
|**Coletar dados de memória do .NET:** use a amostragem ou a instrumentação para coletar dados de alocação de memória do .NET que mostra o tamanho e o número de objetos alocados. Também é possível coletar dados de tempo de vida do objeto que mostram o tamanho e o número de objetos recuperados em cada geração de coleta de lixo.|-   [Coletando dados de memória](../profiling/collecting-memory-data-from-an-aspnet-web-application-by-using-the-profiler-command-line.md)|  
|**Coletar dados de simultaneidade:** use o método de simultaneidade para coletar dados de contenção de recursos. **Observação:** não há suporte para coletar a atividade do thread e dados de visualização para aplicativos Web.|-   [Coletando dados de simultaneidade](../profiling/collecting-concurrency-data-for-an-aspnet-web-application-using-the-profiler-command-line.md)|  
|**Adicionar dados de interação de camada:** é possível adicionar dados de desempenho sobre chamadas [!INCLUDE[vstecado](../includes/vstecado-md.md)] síncronas que o aplicativo Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] efetua para um banco de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] da Microsoft.|-   [Coletando dados de interação entre camadas](../profiling/adding-tier-interaction-data-from-the-command-line.md)|  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Tarefa|Conteúdo relacionado|  
|----------|---------------------|  
|**Criar o perfil de aplicativos autônomos (clientes)**|-   [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)|  
|**Profile services (Serviços de perfil)**|-   [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)|



