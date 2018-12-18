---
title: Visão Geral do Relatório de Desempenho | Microsoft Docs
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
- profiling tools, about performance rerports
- performance, reports
- performance reports, about performance reports
ms.assetid: 7324c24c-fd09-479b-b2ad-e0c3b613e040
caps.latest.revision: 50
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6b9a729698841d1bbbcd9b49ffe0d3dd9bddccc8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51790507"
---
# <a name="performance-report-overview"></a>Visão geral de Relatório de Desempenho
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode exibir os dados de criação de perfil de uma sessão de desempenho na janela **Relatório de Desempenho** do IDE (Ambiente de Desenvolvimento Integrado) do Visual Studio Team System Development Edition. Os dados de criação de perfil são salvos em arquivos .vsp e .vsps. As janelas de exibição de relatório permitem exibir e analisar problemas de desempenho do aplicativo.  
  
> [!CAUTION]
>  Um arquivo de dados de criação de perfil contém informações confidenciais como o nome do computador, a versão do sistema operacional, caminhos de arquivo, informações de memória e outras informações de configuração do computador. Você deve manter um controle rígido sobre a distribuição de dados, tanto em seu formato .vsp nativo quanto exportado para um arquivo .csv ou .xml.  
>   
>  Se os dados de rastreamento de eventos forem coletados como parte da sessão de desempenho, informações adicionais podem aparecer no arquivo de log de rastreamento de evento (.etl). Essas informações incluem seu nome de usuário e domínio, por isso, você deve manter um rígido controle sobre a distribuição do arquivo de log.  
  
## <a name="performance-report-window"></a>Janela no Relatório de Desempenho  
 A janela Relatório de Desempenho é uma janela de ferramentas que é usada para exibir, gerenciar e filtrar dados de desempenho e inclui um controle de consulta personalizável.  
  
 Na barra de ferramentas principal da janela Relatório de Desempenho, você pode acessar cada modo de exibição. Clique na seta ao lado da lista **Exibição Atual** para exibir e selecionar as exibições individuais que estão disponíveis.  
  
 A janela Relatório de Desempenho fornece as seguintes exibições de dados:  
  
### <a name="summary-view"></a>Exibição do Resumo  
 Por padrão, os dados de criação de perfis são exibidos na exibição Resumo. Essa exibição é um ponto de partida na sua investigação de problemas de desempenho. De cada linha da exibição Resumo, você pode acessar exibições mais detalhadas clicando com o botão direito do mouse no nome de uma função ou módulo. Para mais informações, consulte [Exibição de Resumo](../profiling/summary-view.md).  
  
### <a name="callercallee-view"></a>Exibição Chamador/Receptor da Chamada  
 A exibição de Chamador/Computador chamado exibe uma árvore de chamadas para uma função individual. A exibição está dividida em três partes:  
  
- A função de destino é exibida no meio da exibição.  
  
- As funções que chamaram tal função (chamadores) são exibidas acima da função de destino.  
  
- As funções que são chamadas pela função de destino (computadores chamados) são exibidas abaixo do destino.  
  
  Você pode selecionar uma função diferente clicando duas vezes em qualquer função na lista de chamador ou de computador chamado. Para obter mais informações, consulte a [Exibição de Chamador/Computador chamado](../profiling/caller-callee-view.md).  
  
### <a name="call-tree-view"></a>Exibição de árvore de chamadas  
 O modo de exibição de Árvore de Chamadas exibe os caminhos de execução de função que foram percorridos no aplicativo analisado. A raiz da árvore é o ponto de entrada do aplicativo ou componente. Cada nó da função lista todas as funções que ela chamou e os dados de desempenho sobre essas chamadas de função.  
  
 O Modo de exibição de árvore de Chamadas também expande e realça o caminho de execução de uma função que consumiu mais tempo ou que gerou amostras com mais frequência. Para exibir o caminho mais ativo, clique com o botão direito do mouse na função de atalho e, em seguida, clique em **Expandir Afunilamento**. Para obter mais informações, consulte o [Modo de exibição de árvore de Chamadas](../profiling/call-tree-view.md).  
  
### <a name="process-view"></a>Exibição de processo  
 A exibição Processo exibe dados de desempenho para cada processo e thread que foi analisado. Para mais informações, consulte [Exibição de Processo](../profiling/process-view.md).  
  
### <a name="modules-view"></a>Exibição de módulos  
 A exibição Módulos lista os módulos no projeto e apresenta os dados de criação de perfil para cada módulo. Expanda ou recolha o nome do módulo para exibir dados de criação de perfil de função. Quando os dados foram coletados por meio de amostragem, a linha de código-fonte e os dados de criação de perfil de ponteiro de instrução também estão disponíveis. Para mais informações, consulte [Exibição de Módulos](../profiling/modules-view.md).  
  
### <a name="functions-view"></a>Exibição de funções  
 A exibição Funções lista as funções que foram chamadas durante a criação de perfil. Para obter mais informações, consulte a [Exibição de Funções](../profiling/functions-view.md).  
  
### <a name="line-view"></a>Exibição de Linha  
 A exibição Linhas permite exibir as linhas de código-fonte específicas que foram executadas durante a criação de perfil de amostragem. Para obter mais informações, consulte [Exibição de linhas](../profiling/lines-view.md).  
  
### <a name="instruction-pointer-ip-view"></a>Exibição IP (Ponteiros de Instrução)  
 A exibição Ponteiro de Instrução permite exibir as instruções específicas que foram executadas durante a criação de perfil de amostragem. Para obter mais informações, consulte [Exibição de IPs (Ponteiros de Instrução)](../profiling/instruction-pointers-ips-view.md).  
  
### <a name="allocation-view"></a>Exibição de alocação  
 A exibição Alocação estará disponível se **Coletar alocação de objeto .NET** tiver sido selecionado na página **Geral** da caixa de diálogo de propriedades da **Sessão de Desempenho**. Consulte [Visão geral da sessão de desempenho](../profiling/performance-session-overview.md). A exibição Alocação lista os objetos do .NET que foram alocados pelo aplicativo ou componente. Quando uma linha de objeto é expandida, uma árvore de chamadas é exibida. A árvore de chamadas exibe os caminhos de execução que resultaram na criação do objeto. Informações também são exibidas sobre o número de alocações inclusivas e exclusivas para cada função na árvore de chamadas. A exibição Alocação também pode expandir e realçar o caminho de execução de uma função que alocou o número máximo de objetos. Para exibir o caminho mais ativo, clique com o botão direito do mouse na função de atalho e, em seguida, clique em **Expandir Afunilamento**. Para obter mais informações, consulte [Coletando alocação de memória e dados de tempo de vida do .NET](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md) e [Exibição Alocações](../profiling/dotnet-memory-allocations-view.md).  
  
### <a name="objects-lifetime-view"></a>Exibição Tempo de Vida de Objetos  
 A exibição Tempo de Vida do Objeto estará disponível se **Coletar informações de alocação de objeto do .NET** e **Coletar também as informações de tempo de vida do objeto .NET** forem marcados na página **Geral** a caixa de diálogo de propriedades **Sessão de Desempenho**.  
  
 A exibição Tempo de Vida do Objeto exibe o número total de instâncias de cada tipo e o número de objetos que foram coletados em cada geração de coleta de lixo. Para obter mais informações, consulte [Exibição de tempo de vida do objeto](../profiling/object-lifetime-view.md).  
  
## <a name="customizable-filter-control"></a>Controle de filtro personalizável  
 O controle de filtro personalizável tem as seguintes opções:  
  
-   **Importar Filtro** – recupera uma consulta personalizada salva anteriormente.  
  
-   **Exportar Filtro** – salva a consulta personalizada para o local especificado.  
  
-   **Executar Consulta** – executa a consulta, conforme exibido no controle de consulta personalizada.  
  
-   **Parar Consulta** – interrompe a execução de uma consulta que está em execução. Este botão não estará disponível se nenhuma consulta estiver em execução.  
  
-   **Mostrar Consulta** – Mostra/oculta o controle de consulta personalizada.  
  
-   **Salvar Analisados** – salva o relatório junto com sua análise atual como um arquivo .vsps.  
  
-   **Exportar** – salva o relatório atual como um arquivo formatado em .CVS ou .XML, com opções para salvar as diferentes exibições.  
  
## <a name="see-also"></a>Consulte também  
 [Analisando dados de ferramentas de desempenho](../profiling/analyzing-performance-tools-data.md)   
 [Exibições de relatório de desempenho](../profiling/performance-report-views.md)



