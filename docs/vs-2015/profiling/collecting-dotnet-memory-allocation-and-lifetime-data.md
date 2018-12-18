---
title: Coletando a alocação de memória do .NET e os dados de tempo de vida | Microsoft Docs
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
- .NET memory profiling method
- Profiling Tools,.NET memory method
ms.assetid: 62a6dd5f-db66-4456-9d57-f8913dbfe4d5
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0b31f4cfce52c60e4b8f65758fc56e16e29bef6b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51761581"
---
# <a name="collecting-net-memory-allocation-and-lifetime-data"></a>Coletando a alocação de memória do .NET e os dados de vida útil
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] As Ferramentas de Criação de Perfil dão suporte à coleta de alocação de memória e dados de tempo de vida do objeto do .NET, que ajuda a detectar problemas de desempenho relacionados à memória em seu aplicativo.  
  
- Os Dados sobre alocação de memória do .NET incluem o tamanho e o número de objetos de memória do .NET Framework alocados.  
  
- Os dados de tempo de vida do objeto incluem o tamanho e o número de objetos de memória do .NET Framework reivindicados nas três gerações de coleta de lixo.  
  
  **Requisitos**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos da Windows Store também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).  
  
 É possível coletar dados usando a amostragem ou o método de criação de perfil de instrumentação.  
  
-   Quando você usa o método de amostragem, o criador de perfil rastreia todos os objetos e as alocações de memória do .NET gerados pelo processo que foi iniciado ou ao qual foram anexados.  
  
-   Quando você usa o método de instrumentação, o criador de perfil rastreia somente os objetos e as alocações de memória do .NET gerados pelos módulos instrumentados.  
  
> [!IMPORTANT]
>  Quando você estiver coletando dados de memória do .NET (alocações, tempos de vida do objeto ou ambos) usando o método de amostragem, todos os eventos de amostragem especificados pelo usuário serão ignorados e os eventos de alocação de memória adequados serão usados para coletar dados.  
  
 Se você habilitar a criação de perfil da alocação de memória do .NET, você também habilitará o Modo de Exibição de Alocação. Se você habilitar a criação de perfil de dados de tempo de vida do .NET, você também habilitará o Modo de Exibição de Tempo de Vida de Objetos. Para obter mais informações, consulte [Modo de Exibição de Alocações](../profiling/dotnet-memory-allocations-view.md) e [Modo de Exibição de Tempo de Vida do Objeto](../profiling/object-lifetime-view.md).  
  
 Para obter informações sobre como coletar dados de memória do .NET usando as ferramentas de linha de comando das Ferramentas de Criação de Perfil, consulte Using .NET Memory Methods to Collect Memory Allocation and Object Lifetime Data (Usando métodos de memória .NET para coletar alocação de memória e dados de tempo de vida do objeto) em [Using Profiling Methods From the Command Line (Usando métodos de criação de perfil na linha de comando)](../profiling/using-profiling-methods-to-collect-performance-data-from-the-command-line.md).  
  
### <a name="to-collect-net-memory-data"></a>Para coletar dados de memória do .NET  
  
1.  No **Gerenciador de Desempenho**, clique com o botão direito do mouse na sessão de desempenho e, em seguida, clique em **Propriedades**.  
  
2.  Na caixa de diálogo _Sessão de Desempenho_**Páginas de Propriedades**, clique na guia **Geral** e selecione a caixa de seleção **Coletar informações de alocação de objeto do .NET**.  
  
3.  Para coletar dados de tempo de vida do objeto, selecione a caixa de seleção **Também coletar informações de tempo de vida de objeto .NET**.  
  
## <a name="common-tasks"></a>Tarefas comuns  
 É possível especificar outras opções na caixa de diálogo _Sessão de Desempenho_**Páginas de Propriedades** da sessão de desempenho. Para abrir essa caixa de diálogo:  
  
- No **Gerenciador de Desempenho**, clique com o botão direito do mouse no nome da sessão de desempenho e clique em **Propriedades**.  
  
  As tarefas na tabela a seguir descrevem opções que podem ser especificadas na caixa de diálogo _Sessão de Desempenho_**Páginas de Propriedades** quando você coleta dados de memória do .NET.  
  
|Tarefa|Conteúdo relacionado|  
|----------|---------------------|  
|Na página **Geral**, especifique detalhes de nomenclatura para o arquivo de dados de criação de perfil gerado (.vsp).|-   [Coletando a alocação de memória do .NET e os dados de tempo de vida](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)<br />-   [Como definir opções de nome de arquivo de dados de desempenho](../profiling/how-to-set-performance-data-file-name-options.md)|  
|Na página **Iniciar**, especifique o aplicativo a ser iniciado se você tiver vários projetos .exe na solução do seu código.|-   [Coletando dados de interação entre camadas](../profiling/collecting-tier-interaction-data.md)|  
|Na página **Interação de Camada**, adicione dados de chamada ADO.NET à execução de criação de perfil.|-   [Coletando dados de interação entre camadas](../profiling/collecting-tier-interaction-data.md)|  
|Na página **Eventos do Windows**, especifique um ou mais eventos ETW (Rastreamento de Eventos para Windows) para coletar com os dados de amostragem.|-   [Como coletar dados ETW (Rastreamento de Eventos para Windows)](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)|  
|Na página **Contadores do Windows**, especifique um ou mais contadores de desempenho de sistema operacional para serem adicionados aos dados de criação de perfil como marcas.|-   [Como coletar dados do contador do Windows](../profiling/how-to-collect-windows-counter-data.md)|  
|Na página **Avançado**, especifique a versão do tempo de execução do .NET Framework para o perfil se seus módulos de aplicativo usarem várias versões. Por padrão, a primeira versão carregada é analisada.|-   [Como especificar o tempo de execução do .NET Framework](../profiling/how-to-specify-the-dotnet-framework-runtime.md)|  
  
## <a name="instrumentation-tasks"></a>Tarefas de instrumentação  
 As tarefas na tabela a seguir são opções na caixa de diálogo **Páginas de Propriedades** específicas para a criação de perfil com o método de instrumentação.  
  
|Tarefa|Conteúdo relacionado|  
|----------|---------------------|  
|Na página **Binários**, especifique um local para as cópias instrumentadas dos módulos. Por padrão, os binários originais são movidos para uma pasta de backup.|-   [Como realocar binários instrumentados](../profiling/how-to-relocate-instrumented-binaries.md)|  
|Na página **Instrumentação**, exclua pequenas funções de criação de perfil para reduzir a sobrecarga da criação de perfil, criar perfil de código JavaScript em páginas Web ASP.NET e especificar comandos para serem executados em um prompt de comando antes e depois do processo de instrumentação.|-   [Como excluir ou incluir funções curtas por meio da instrumentação](../profiling/how-to-exclude-or-include-short-functions-from-instrumentation.md)<br />-   [Como analisar código JavaScript em páginas da Web](../profiling/how-to-profile-javascript-code-in-web-pages.md)<br />-   [Como especificar comandos pré e pós-instrumento](../profiling/how-to-specify-pre-and-post-instrument-commands.md)|  
|Na página **Contadores de CPU**, especifique um ou mais contadores de desempenho de processador para serem adicionados aos dados de criação de perfil.|-   [Como coletar dados do contador de CPU](../profiling/how-to-collect-cpu-counter-data.md)|  
|Na página **Avançado**, especifique outras opções VSInstr.exe que você desejar, como opções para incluir ou excluir funções específicas. Para obter mais informações sobre opções VSInstr, consulte [VSInstr](../profiling/vsinstr.md)|-   [Como especificar opções de instrumentação adicionais](../profiling/how-to-specify-additional-instrumentation-options.md)<br />-   [Como limitar a instrumentação a funções específicas](../profiling/how-to-limit-instrumentation-to-specific-functions.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Configurando sessões de desempenho](../profiling/configuring-performance-sessions.md)   
 [Como escolher métodos de coleta](../profiling/how-to-choose-collection-methods.md)   
 [Propriedades da sessão de desempenho](../profiling/performance-session-properties.md)



