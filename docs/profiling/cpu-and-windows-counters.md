---
title: Contadores de CPU e do Windows | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.property.counters
helpviewer_keywords:
- Windows counters in Profiling Tools
- CPU counters in Profiling Tools
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e63919a13a948f7e6be2d2789aa778bd39514e51
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54950826"
---
# <a name="cpu-and-windows-counters"></a>Contadores de CPU e do Windows

O Criador de Perfil do Visual Studio permite coletar dados de desempenho que foram gerados pelo sistema operacional (contadores do Windows) e dados de desempenho que foram gerados pela unidade do processador (contadores da CPU).

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

## <a name="windows-counters"></a>Contadores do Windows

Os contadores do Windows fazem parte da Infraestrutura de Diagnóstico do Windows que fornece informações sobre o desempenho do sistema operacional, de um aplicativo, serviço ou driver. Os contadores do Windows dependem da configuração do computador atual e podem não estar disponíveis em outros computadores. Os contadores de desempenho do Windows são coletados em arquivos de dados de criação de perfil como marcas de criação de perfil, que podem ser então usadas para filtrar exibições e relatórios.

## <a name="cpu-counters"></a>Contadores de CPU

Contadores da CPU são um recurso da CPU do computador que armazena a contagem de eventos relacionados ao hardware. Ao coletar dados de contadores da CPU usando o método de criação de perfil de instrumentação, os dados são acrescentados aos dados de funções e módulos. Você pode coletar vários contadores da CPU usando o método de instrumentação. Ao usar o método de amostragem, você seleciona um contador a ser usado como o evento do qual a amostragem será coletada.

Os contadores de desempenho são específicos à CPU. Diferentes modelos e versões de uma CPU podem ter configurações consideravelmente diferentes para habilitar o mesmo contador de desempenho. Os eventos portáteis do Criador de Perfil do [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] desacoplam alguns contadores de desempenho comuns de processadores específicos e permitem coletar ou coletar amostras de eventos de desempenho genéricos.

Se você desejar contar um evento específico ao usar o criador de perfil, por exemplo, cache L2 ignorado, poderá criar uma sessão de desempenho em torno desse remetente do evento. É possível fazer isso em qualquer CPU com um cache L2. A sessão de desempenho pode ser movida de uma plataforma para outra sem modificação.

O criador de perfil do Visual Studio continua dando suporte a eventos específicos de uma plataforma específica. Por exemplo, um desenvolvedor em uma plataforma Pentium 4 talvez deseje contar os eventos específicos à arquitetura NetBurst. Esse evento não é portátil, mas ainda está disponível para o desenvolvedor para uma sessão de desempenho específica em uma plataforma específica.

## <a name="portable-and-platform-events"></a>Eventos portáteis e da plataforma

Eventos portáteis são um grupo de contadores da CPU que não são específicos a um processador específico. Todos os outros contadores da CPU são chamados de eventos da plataforma e podem não ter suporte em várias plataformas.

 Contadores para os eventos portáteis e da plataforma são definidos em arquivos .*xml*, em que valores específicos relacionados aos contadores são fornecidos. Há vários arquivos para CPUs diferentes, pois os dados para CPUs Intel e AMD, por exemplo, são diferentes. O Criador de Perfil [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] usa essas informações para apresentar contadores apropriados, portáteis e da plataforma, ao usuário para medição de desempenho.

### <a name="portable-events"></a>Eventos portáteis

Os eventos portáteis contêm os seguintes eventos:

**Eventos gerais**

|Nome do Evento|Descrição do evento|
|----------------|-----------------------|
|Instruções Desativadas|Indica o número de instruções executadas até a conclusão do evento.|
|Ciclos Não Interrompidos|Indica apenas os ciclos nos quais o processador não foi interrompido, por exemplo, aguardando E/S.|

**Eventos de front-end**

|Nome do Evento|Descrição do evento|
|----------------|-----------------------|
|Perdas de ITLB|Indica o número de pesquisas de Buffer à Parte de Translação de Instrução que resultaram em uma perda.|

**Eventos de ramificação**

|Nome do Evento|Descrição do evento|
|----------------|-----------------------|
|Ramificações Desativadas|Indica o número de instruções de ramificação executadas até a conclusão do evento.|
|Ramificações Previstas Incorretamente|Indica ramificações previstas incorretamente que ocorrem devido ao fato de o processador ter previsto um caminho incorreto. Ramificações previstas incorretamente afetam o desempenho, pois o processador deve descartar todo o trabalho feito e começar novamente em um caminho correto.|

**Eventos de memória:**

|Nome do Evento|Descrição do evento|
|----------------|-----------------------|
|Erros de Leitura de Cache L2|Indica o número de perdas de leitura do cache de segundo nível.|
|Referências de Leitura de Cache L2|Indica o número de referências de leitura do cache de segundo nível. Inclui perdas de carga e perdas e ocorrências de RFO (leitura de propriedade).|

## <a name="view-available-counters"></a>Exibir contadores disponíveis

É possível listar os contadores da CPU disponíveis na IDE do Visual Studio em uma janela do Prompt de Comando.

### <a name="visual-studio-ui"></a>Interface do usuário do Visual Studio

Para listar os contadores disponíveis em um computador na IDE do Visual Studio, é necessário ter uma sessão de desempenho do criador de perfil aberta no Gerenciador de Desempenho.

#### <a name="to-view-a-list-of-a-list-of-all-cpu-counters-that-are-supported-on-the-current-platform"></a>Para exibir uma lista de todos os contadores da CPU com suporte na plataforma atual

1. No Gerenciador de Desempenho, clique com o botão direito do mouse na sessão de desempenho e clique em **Propriedades**.

2. Realize um dos seguintes procedimentos:

   - Clique em **Amostragem** e, em seguida, selecione **Contador de desempenho** na lista de eventos **Amostra**. Os contadores da CPU são listados em **Contadores de desempenho disponíveis**.

      **Observação** Clique em **Cancelar** para retornar à configuração de amostragem anterior.

     - ou -

   - Selecione **Contadores da CPU** e, em seguida, **Coletar Contadores da CPU**. Os contadores da CPU são listados em **Contadores disponíveis**.

      **Observação** Clique em **Cancelar** para retornar à configuração de coleta de contadores anterior.

#### <a name="to-view-a-list-of-a-list-of-window-counters-that-are-supported-on-the-current-platform"></a>Para exibir uma lista de contadores do Windows com suporte na plataforma atual

1. No Gerenciador de Desempenho, clique com o botão direito do mouse na sessão de desempenho e clique em **Propriedades**.

2. Clique em **Contadores do Windows**.

3. Selecione **Coletar Contadores do Windows**.

4. Na lista **Categoria de Contador**, selecione um grupo de contadores. O contador do Windows para o grupo é exibido na caixa de listagem.

     **Observação:** Clique em **Cancelar** para retornar à configuração anterior de coleta de contadores.

### <a name="command-line"></a>Linha de comando

Com a ferramenta de linha de comando [VSPerfCmd](../profiling/vsperfcmd.md), é possível listar os contadores da CPU disponíveis em um computador por meio da linha de comando.

#### <a name="to-list-of-cpu-counters-that-are-supported-on-the-current-platform"></a>Para listar os contadores da CPU com suporte na plataforma atual

1. Abra uma janela do prompt de comando.

2. Tipo

     **\<Visual Studio Performance Tools Directory>\VSPerfCmd /querycounters**

     em que *\<Diretório das Ferramentas de Desempenho do Visual Studio>* é o caminho para o diretório das Ferramentas de Desempenho da instalação do Visual Studio. Para obter o caminho para as ferramentas de desempenho, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).

## <a name="see-also"></a>Consulte também

[Visões gerais](../profiling/overviews-performance-tools.md)  
[Como: Escolher eventos de amostragem](../profiling/how-to-choose-sampling-events.md)  
[Como: Coletar dados do contador de CPU](../profiling/how-to-collect-cpu-counter-data.md)  
[Como: Coletar dados de contadores do Windows](../profiling/how-to-collect-windows-counter-data.md)