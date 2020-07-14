---
title: Coletando dados de tempo detalhados usando a instrumentação | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Profiling Tools,instrumentation method
- instrumentation profiling method
ms.assetid: e9deb370-c459-45ac-84d3-14d646590d05
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 682ae4bf31f44f3dff5f6dfadf7b8c316d9d9721
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85331851"
---
# <a name="collect-detailed-timing-data-by-using-instrumentation"></a>Coletar dados de tempo detalhados usando a instrumentação
O método de instrumentação das Ferramentas de Criação [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] injeta código de criação de perfil em uma cópia de um módulo. O código registra cada entrada, saída e a chamada de função das funções no módulo durante uma execução de criação de perfil. O método de instrumentação é útil para coletar informações detalhadas de tempo sobre uma seção do seu código e para compreender o impacto das operações de entrada e saída sobre o desempenho do aplicativo.

 É possível especificar o método de amostragem usando um dos seguintes procedimentos:

- Na primeira página do Assistente de Criação de Perfil, selecione **Instrumentação**.

- Na barra de ferramentas do **Gerenciador de Desempenho**, na lista **Método**, clique em **Instrumentação**.

- Na página **Geral** da caixa de diálogo de propriedades da sessão de desempenho, clique em **Instrumentação**.

## <a name="common-tasks"></a>Tarefas comuns
 Você pode especificar opções adicionais na caixa de diálogo**páginas de propriedades** de _sessão de desempenho_da sessão de desempenho. Para abrir essa caixa de diálogo:

- Em **Gerenciador de desempenho**, clique com o botão direito do mouse no nome da sessão de desempenho e clique em **Propriedades**.

  As tarefas na tabela a seguir descrevem as opções que você pode especificar na caixa de diálogo**páginas de propriedades** de _sessão de desempenho_ao criar o perfil usando o método de instrumentação.

|Tarefa|Conteúdo relacionado|
|----------|---------------------|
|Na página **Geral**, adicione a alocação de memória do .NET e dados de tempo de vida e especifique os detalhes de nomenclatura para o arquivo de dados de criação de perfil gerado (.vsp).|-   [Coletar dados de tempo de vida e alocação de memória do .NET](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)<br />-   [Como definir opções de nome de arquivo de dados de desempenho](../profiling/how-to-set-performance-data-file-name-options.md)|
|Na página **Iniciar**, se você tiver vários projetos .exe em sua solução, especifique o aplicativo a ser iniciado e sua ordem de início.|-   [Como especificar o binário a ser iniciado](../profiling/how-to-specify-the-binary-to-start.md)|
|Na página **Binários**, especifique um local para as cópias instrumentadas dos módulos. Por padrão, os binários originais são movidos para uma pasta de backup.|-   [Como: realocar binários instrumentados](../profiling/how-to-relocate-instrumented-binaries.md)|
|Na página **Interação de Camada**, adicione dados de chamada ADO.NET à execução de criação de perfil.|-   [Coletar dados de interação de camada](../profiling/collecting-tier-interaction-data.md)|
|Na página **Instrumentação**, exclua pequenas funções de criação de perfil para reduzir a sobrecarga da criação de perfil, criar perfil de código JavaScript em páginas Web ASP.NET e especificar comandos para serem executados em um prompt de comando antes e depois do processo de instrumentação.|-   [Como: excluir ou incluir funções curtas da instrumentação](../profiling/how-to-exclude-or-include-short-functions-from-instrumentation.md)<br />-   [Como: criar um perfil de código JavaScript em páginas da Web](../profiling/how-to-profile-javascript-code-in-web-pages.md)<br />-   [Como especificar comandos pré e pós-instrumento](../profiling/how-to-specify-pre-and-post-instrument-commands.md)|
|Na página **Contadores de CPU**, especifique um ou mais contadores de desempenho de processador para serem adicionados aos dados de criação de perfil.|-   [Como: coletar dados do contador de CPU](../profiling/how-to-collect-cpu-counter-data.md)|
|Na página **Eventos do Windows**, selecione um ou mais eventos ETW (Rastreamento de Eventos para Windows) para coletar com os dados de amostragem.|-   [Como coletar dados do ETW (rastreamento de eventos para Windows)](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)|
|Na página **Contadores do Windows**, especifique um ou mais contadores de desempenho de sistema operacional para serem adicionados aos dados de criação de perfil como marcas.|-   [Como: coletar dados do contador do Windows](../profiling/how-to-collect-windows-counter-data.md)|
|Na página **Avançado**, especifique outras opções que você deseja passar para o programa de instrumentação VSInstr.exe, como opções para incluir ou excluir funções específicas.|-   [Como especificar opções de instrumentação adicionais](../profiling/how-to-specify-additional-instrumentation-options.md)<br />-   [Como limitar a instrumentação a funções específicas](../profiling/how-to-limit-instrumentation-to-specific-functions.md)<br />-   [VSInstr](../profiling/vsinstr.md)|
