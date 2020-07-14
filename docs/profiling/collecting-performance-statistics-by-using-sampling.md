---
title: Coletando estatísticas de desempenho usando amostragem | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Profiling Tools,sampling
- sampling profiling method
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: adf26a8a1bae495481106506208232ebb383d2ca
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85331655"
---
# <a name="collect-performance-statistics-by-using-sampling"></a>Coletar estatísticas de desempenho usando amostragem

Por padrão, o método de amostragem das Ferramentas de Criação de Perfil do Visual Studio coleta informações de criação de perfil cada 10.000.000 de ciclos do processador (aproximadamente a cada um centésimo de segundo em um computador de 1 GHz). O método de amostragem é útil para localizar problemas de utilização do processador e é o método sugerido para iniciar a maioria das investigações de desempenho.

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

É possível especificar o método de amostragem usando um dos seguintes recursos:

- Na primeira página do Assistente de Criação de Perfil, clique em **Amostragem de CPU (recomendada)**.
- Na barra de ferramentas **Gerenciador de Desempenho**, na lista **Método**, clique em **Amostragem**.
- Na página **Geral** da caixa de diálogo de propriedades da sessão de desempenho, clique em **Amostragem**.

## <a name="common-tasks"></a>Tarefas comuns

Você pode especificar opções adicionais na caixa de diálogo**páginas de propriedades** de _sessão de desempenho_da sessão de desempenho. Para abrir essa caixa de diálogo:

- Em **Gerenciador de desempenho**, clique com o botão direito do mouse no nome da sessão de desempenho e clique em **Propriedades**.

  As tarefas na tabela a seguir descrevem as opções que podem ser especificadas na caixa de diálogo _Sessão de Desempenho_**Páginas de Propriedades** quando você cria o perfil usando o método de amostragem.

|Tarefa|Conteúdo relacionado|
|----------|---------------------|
|Na página **Geral**, adicione a alocação de memória do .NET e coleta de dados de tempo de vida e especifique os detalhes de nomenclatura para o arquivo de dados de criação de perfil gerado (.vsp).|- [Coletando a alocação de memória do .NET e os dados de tempo de vida](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)<br />- [Como definir opções de nome de arquivo de dados de desempenho](../profiling/how-to-set-performance-data-file-name-options.md)|
|Na página **Amostragem**, altere a taxa de amostragem, o evento de amostragem dos ciclos do relógio do processador para outro contador de desempenho do processador ou ambos.|- [Como escolher eventos de amostragem](../profiling/how-to-choose-sampling-events.md)|
|Na página **Iniciar**, especifique o aplicativo a ser iniciado e a ordem de início se você tiver vários projetos .exe na solução do seu código.|- [Coletando dados de interação de camada](../profiling/collecting-tier-interaction-data.md)|
|Na página **Interação de Camada**, adicione informações de chamada ADO.NET aos dados coletados na execução theprofiling.|- [Coletando dados de interação de camada](../profiling/collecting-tier-interaction-data.md)|
|Na página **Eventos do Windows**, especifique um ou mais eventos ETW (Rastreamento de Eventos para Windows) para coletar com os dados de amostragem.|- [Como coletar dados ETW (Rastreamento de Eventos para Windows)](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)|
|Na página **Contadores do Windows**, especifique um ou mais contadores de desempenho de sistema operacional para serem adicionados aos dados de criação de perfil como marcas.|- [Como coletar dados do contador do Windows](../profiling/how-to-collect-windows-counter-data.md)|
|Na página **Avançado**, especifique a versão do runtime do .NET Framework para o perfil se seus módulos de aplicativo usarem várias versões. Por padrão, a primeira versão carregada é analisada.|- [Como especificar o tempo de execução de .NET Framework](../profiling/how-to-specify-the-dotnet-framework-runtime.md)|
