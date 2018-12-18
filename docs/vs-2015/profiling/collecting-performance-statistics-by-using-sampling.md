---
title: Coletando estatísticas de desempenho usando amostragem | Microsoft Docs
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
- Profiling Tools,sampling
- sampling profiling method
ms.assetid: 8e36361b-bb3d-40c6-b286-0e68c0ecb915
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a67c6542c2b838de7e80ee23588847cc15c15292
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51755269"
---
# <a name="collecting-performance-statistics-by-using-sampling"></a>Coletando estatísticas de desempenho usando amostragem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Por padrão, o método de amostragem das Ferramentas de Criação de Perfil [!INCLUDE[vsPreShort](../includes/vspreshort-md.md)] coleta informações de criação de perfil cada 10.000.000 de ciclos do processador (aproximadamente a cada um centésimo de segundo em um computador de 1 GHz). O método de amostragem é útil para localizar problemas de utilização do processador e é o método sugerido para iniciar a maioria das investigações de desempenho.  
  
 **Requisitos**  
  
-   [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos da Windows Store também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).  
  
 É possível especificar o método de amostragem usando um dos seguintes recursos:  
  
-   Na primeira página do Assistente de Criação de Perfil, clique em **Amostragem de CPU (recomendada)**.  
  
-   Na barra de ferramentas **Gerenciador de Desempenho**, na lista **Método**, clique em **Amostragem**.  
  
-   Na página **Geral** da caixa de diálogo de propriedades da sessão de desempenho, clique em **Amostragem**.  
  
## <a name="common-tasks"></a>Tarefas comuns  
 É possível especificar outras opções na caixa de diálogo _Sessão de Desempenho_**Páginas de Propriedades** da sessão de desempenho. Para abrir essa caixa de diálogo:  
  
- No **Gerenciador de Desempenho**, clique com o botão direito do mouse no nome da sessão de desempenho e clique em **Propriedades**.  
  
  As tarefas na tabela a seguir descrevem as opções que podem ser especificadas na caixa de diálogo _Sessão de Desempenho_**Páginas de Propriedades** quando você cria o perfil usando o método de amostragem.  
  
|Tarefa|Conteúdo relacionado|  
|----------|---------------------|  
|Na página **Geral**, adicione a alocação de memória do .NET e coleta de dados de tempo de vida e especifique os detalhes de nomenclatura para o arquivo de dados de criação de perfil gerado (.vsp).|-   [Coletando a alocação de memória do .NET e os dados de tempo de vida](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)<br />-   [Como definir opções de nome de arquivo de dados de desempenho](../profiling/how-to-set-performance-data-file-name-options.md)|  
|Na página **Amostragem**, altere a taxa de amostragem, o evento de amostragem dos ciclos do relógio do processador para outro contador de desempenho do processador ou ambos.|-   [Como escolher eventos de amostragem](../profiling/how-to-choose-sampling-events.md)|  
|Na página **Iniciar**, especifique o aplicativo a ser iniciado e a ordem de início se você tiver vários projetos .exe na solução do seu código.|-   [Coletando dados de interação entre camadas](../profiling/collecting-tier-interaction-data.md)|  
|Na página **Interação de Camada**, adicione informações de chamada ADO.NET aos dados coletados na execução theprofiling.|-   [Coletando dados de interação entre camadas](../profiling/collecting-tier-interaction-data.md)|  
|Na página **Eventos do Windows**, especifique um ou mais eventos ETW (Rastreamento de Eventos para Windows) para coletar com os dados de amostragem.|-   [Como coletar dados ETW (Rastreamento de Eventos para Windows)](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)|  
|Na página **Contadores do Windows**, especifique um ou mais contadores de desempenho de sistema operacional para serem adicionados aos dados de criação de perfil como marcas.|-   [Como coletar dados do contador do Windows](../profiling/how-to-collect-windows-counter-data.md)|  
|Na página **Avançado**, especifique a versão do tempo de execução do .NET Framework para o perfil se seus módulos de aplicativo usarem várias versões. Por padrão, a primeira versão carregada é analisada.|-   [Como especificar o tempo de execução do .NET Framework](../profiling/how-to-specify-the-dotnet-framework-runtime.md)|



