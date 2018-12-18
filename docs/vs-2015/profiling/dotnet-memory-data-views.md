---
title: Exibições de dados de memória do .NET | Microsoft Docs
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
- .NET memory profiling method views
- profiling tools,.NET memory profiling views
ms.assetid: 79184d8e-769b-4ace-be2b-521147772081
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bc893857e56d97442efd9ceee8ffb8a5aed72ea2
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51762483"
---
# <a name="net-memory-data-views"></a>Exibições de dados da memória do .NET
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esta seção contém informações de referência para as exibições e os relatórios dos arquivos de dados do criador de perfil que contêm os dados de criação de perfil de memória do .NET.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Exibição de Resumo](../profiling/summary-view-dotnet-memory-data.md)  
 Lista as funções e os tipos que alocaram mais memória.  
  
 [Exibição de alocações](../profiling/dotnet-memory-allocations-view.md)  
 Lista os tipos que foram alocados na execução de criação de perfil e as árvores de chamada (caminhos de execução) que resultaram na alocação do tipo.  
  
 [Exibição do tempo de vida do objeto](../profiling/object-lifetime-view.md)  
 Lista os tipos que foram alocados na execução de criação de perfil e o número de instâncias, tamanho em bytes e a geração de coleta de lixo do tipo.  
  
 [Modo de exibição de árvore de chamadas – amostragem](../profiling/call-tree-view-dotnet-memory-sampling-data.md)  
 Exibe uma árvore hierárquica que representa os caminhos de execução e os dados de alocação de memória das funções de execução de criação de perfil.  
  
 [Exibição Módulos – amostragem](../profiling/modules-view-dotnet-memory-sampling-data.md)  
 Organiza os dados de alocação de memória .NET por módulo e lista as funções, as linhas de código-fonte e as instruções que estavam em execução quando a memória foi alocada.  
  
 [Exibição Chamador/Receptor da Chamada – dados de amostragem da memória do .NET](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)  
 Lista os dados de alocação de memória para uma função selecionada, as funções que chamaram a função selecionada e as funções que foram chamadas pela função selecionada.  
  
 [Exibição de Funções – Amostragem](../profiling/functions-view-dotnet-memory-sampling-data.md)  
 Lista os dados de alocação de memória para as funções na execução de criação de perfil.  
  
 [Exibição de Linhas – Amostragem](../profiling/lines-view-dotnet-memory-sampling-data.md)  
 Lista os dados de alocação de memória para as linhas de código-fonte das funções na execução de criação de perfil.  
  
 [Exibição de IPs (ponteiros de instrução) – Amostragem](../profiling/instruction-pointers-ips-view-dotnet-memory-sampling-data.md)  
 Lista os dados de alocação de memória para as instruções de funções na execução de criação de perfil.  
  
 [Modo de exibição de árvore de chamadas – instrumentação](../profiling/call-tree-view-dotnet-memory-instrumentation-data.md)  
 Exibe uma árvore hierárquica que representa os caminhos de execução, os dados de alocação de memória e os dados de tempo detalhados das funções instrumentadas da execução de criação de perfil.  
  
 [Exibição Módulos – Instrumentação](../profiling/modules-view-dotnet-memory-instrumentation-data.md)  
 Organiza os dados de criação de perfil por módulo e lista as funções, os dados de alocação de memória e as informações detalhadas de tempo para o módulo.  
  
 [Exibição Chamador/Receptor da Chamada – dados de instrumentação da memória do .NET](../profiling/caller-callee-view-net-memory-instrumentation-data.md)  
 Lista os dados de alocação de memória e informações de tempo detalhadas para uma função instrumentada selecionada, as funções que chamaram a função selecionada e as funções que foram chamadas pela função selecionada.  
  
 [Exibição de Funções – Instrumentação](../profiling/functions-view-dotnet-memory-instrumentation-data.md)  
 Lista os dados de alocação de memória para as funções instrumentadas na execução de criação de perfil.  
  
## <a name="reference"></a>Referência  
 [Exibição de Detalhes da Função](../profiling/function-details-view.md)  
 Exibe um gráfico da relação entre uma função selecionada e as funções que chamaram e foram chamadas pela função selecionada.  
  
 [Exibição de Processo](../profiling/process-view.md)  
 Lista o processo e as horas final e inicial do thread.  
  
 [Exibição de Marcas](../profiling/marks-view.md)  
 Lista ETW e eventos de amostragem inseridos em um arquivo de dados de criação de perfil.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Exibições de dados do método de amostragem](../profiling/profiler-sampling-method-data-views.md)  
 Informações de referência sobre as exibições e os relatórios dos arquivos de dados do criador de perfil que foram gerados usando o método de amostragem.  
  
 [Exibições de dados do método de instrumentação](../profiling/instrumentation-method-data-views.md)  
 As informações de referência sobre as exibições e os relatórios dos arquivos de dados do criador de perfil que foram gerados usando o método de instrumentação.



