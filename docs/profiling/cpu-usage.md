---
title: Analisar o uso da CPU | Microsoft Docs
ms.custom: seodec18
ms.date: 04/02/2020
ms.topic: how-to
ms.assetid: 7501a20d-04a1-480f-a69c-201524aa709d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e5ab97f3db8e5d44aa649455c313a5681ed93c8c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543384"
---
# <a name="analyze-cpu-usage"></a>Analisar o uso de CPU

Uma boa maneira para começar a investigar problemas de desempenho em seu aplicativo é compreender o uso da CPU. A ferramenta de desempenho **Uso da CPU** mostra o tempo de CPU e percentual gasto executando código em C++, C#/Visual Basic e aplicativos JavaScript.

A ferramenta **Uso da CPU** pode ser executada em um projeto aberto do Visual Studio, em um aplicativo instalado da Microsoft Store ou anexada a um aplicativo ou a um processo em execução. Para obter mais informações, consulte [executar ferramentas de criação de perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md).

É possível executar a ferramenta **Uso da CPU** com ou sem depuração. No depurador, é possível ativar e desativar a criação de perfil da CPU e ver um detalhamento por função do uso da CPU. Será possível exibir os resultados de uso da CPU quando a execução estiver em pausa, por exemplo, em um ponto de interrupção.

As instruções a seguir mostram como usar a ferramenta **Uso da CPU** sem o depurador, usando o **Criador de Perfil de Desempenho** do Visual Studio. Os exemplos usam um build de versão em um computador local. Builds de versão fornecem a melhor exibição do desempenho real do aplicativo. Para analisar o uso da CPU com Depurar builds, confira [Guia do iniciante para a criação de perfil do desempenho](../profiling/beginners-guide-to-performance-profiling.md).

Geralmente, o computador local replica melhor a execução do aplicativo instalado. Para aplicativos Windows Phone, a coleta de dados diretamente do dispositivo fornece os dados mais precisos. Para coletar dados de um dispositivo remoto, execute o aplicativo diretamente no dispositivo, não por meio de uma Conexão de Área de Trabalho Remota.

>[!NOTE]
>O Windows 7 ou posterior é necessário para usar o [Criador de Perfil de Desempenho](../profiling/profiling-feature-tour.md).

## <a name="collect-cpu-usage-data"></a>Coletar dados de uso da CPU

1. No projeto do Visual Studio, defina a configuração da solução como **liberar** e selecione **depurador local do Windows** (ou **computador local**) como o destino de implantação.

    ![Selecionar versão e computador local](../profiling/media/cpuuse_selectreleaselocalmachine.png "Selecionar versão e computador local")

1. Selecione **depurar**  >  **criador de perfil de desempenho**.

1. Em **Ferramentas disponíveis**, selecione **Uso da CPU** e, em seguida, selecione **Iniciar**.

    ![Selecionar uso da CPU](../profiling/media/cpuuse_lib_choosecpuusage.png "Selecionar uso da CPU")

4. Depois que o aplicativo é iniciado, a sessão de diagnóstico começa e exibe os dados de uso da CPU. Quando tiver terminado de coletar os dados, selecione **Interromper Coleta**.

   ![Parar a coleta de dados de uso da CPU](../profiling/media/cpu_use_wt_stopcollection.png "Parar a coleta de dados de uso da CPU")

   A ferramenta Uso da CPU analisa os dados e exibe o relatório.

   ![Relatório de uso da CPU](../profiling/media/cpu_use_wt_report.png "Relatório de uso da CPU")

## <a name="analyze-the-cpu-usage-report"></a>Analise o relatório de uso da CPU

O relatório de diagnóstico é classificado por **CPU total**, do mais alto para o mais baixo. Altere a ordem de classificação ou a coluna de classificação selecionando os cabeçalhos de coluna. Use o menu suspenso **Filtrar** para marcar ou desmarcar os threads a serem exibidos e use a caixa **Pesquisar** para procurar um thread ou um nó específico.

::: moniker range=">=vs-2019"
A partir do Visual Studio 2019, você pode clicar nos botões **Expandir Afunilamento** e **Mostrar Afunilamento** para ver as chamadas de função que usam a porcentagem mais alta da CPU no modo de exibição de árvore de chamada.
::: moniker-end

### <a name="cpu-usage-data-columns"></a><a name="BKMK_Call_tree_data_columns"></a> Colunas de dados de Uso da CPU

|Nome|Descrição|
|-|-|
|**CPU total [unidade, %]**|![Equação total de dados de %](../profiling/media/cpu_use_wt_totalpercentequation.png "CPU_USE_WT_TotalPercentEquation")<br /><br /> Os milissegundos e o percentual da CPU usados por chamadas à função e as funções chamadas por ela, no intervalo de tempo selecionado. Isso é diferente do grafo de linha de tempo **Uso da CPU**, que compara a atividade total da CPU em um intervalo de tempo com a CPU total disponível.|
|**CPU própria [unidade, %]**|![Equação % própria](../profiling/media/cpu_use_wt_selflpercentequation.png "CPU_USE_WT_SelflPercentEquation")<br /><br /> Os milissegundos e o percentual da CPU usados por chamadas à função no intervalo de tempo selecionado, excluindo funções chamadas pela função.|
|**Módulo**|O nome do módulo que contém a função.

### <a name="the-cpu-usage-call-tree"></a><a name="BKMK_The_CPU_Usage_call_tree"></a> A árvore de chamadas de Uso da CPU

Para exibir a árvore de chamadas, selecione o nó pai no relatório. A página **Uso da CPU** é aberta na exibição **Chamador/receptor**. Na lista suspensa **Exibição Atual**, selecione **Árvore de Chamadas**.

#### <a name="call-tree-structure"></a><a name="BKMK_Call_tree_structure"></a> Estrutura da árvore de chamadas

::: moniker range=">=vs-2019"
![Estrutura de árvore de chamada](../profiling/media/vs-2019/cpu-use-wt-getmaxnumbercalltree-annotated.png "Estrutura da árvore de chamadas")
::: moniker-end
::: moniker range="vs-2017"
![Estrutura de árvore de chamada](../profiling/media/cpu_use_wt_getmaxnumbercalltree_annotated.png "Estrutura da árvore de chamadas")
::: moniker-end

|Imagem|Descrição|
|-|-|
|![Etapa 1](../profiling/media/procguid_1.png "ProcGuid_1")|O nó de nível superior nas árvores de chamadas de Uso da CPU é um pseudonó.|
|![Etapa 2](../profiling/media/procguid_2.png "ProcGuid_2")|Na maioria dos aplicativos, quando a opção **Mostrar Código Externo** está desabilitada, o nó de segundo nível é um **[Código Externo]**. O nó contém o código do sistema e do framework que inicia e interrompe o aplicativo, elabora a interface do usuário, controla o agendamento de threads e fornece ao aplicativo outros serviços de nível baixo.|
|![Etapa 3](../profiling/media/procguid_3.png "ProcGuid_3")|Os filhos do nó de segundo nível são métodos e rotinas assíncronas do código de usuário que são chamados ou criados pelo sistema de segundo nível e código do framework.|
|![Etapa 4](../profiling/media/procguid_4.png "ProcGuid_4")|Os nós filhos de um método só têm dados das chamadas do método pai. Quando **Mostrar Código Externo** é desabilitado, os métodos de aplicativo também podem conter um nó **[Código Externo]**.|

#### <a name="external-code"></a><a name="BKMK_External_Code"></a>Código externo

As funções do sistema e do framework executadas pelo seu código são chamadas *código externo*. As funções do código externo iniciam e interrompem o aplicativo, elaboram a interface do usuário, controlam o threading e fornecem ao aplicativo outros serviços de nível inferior. Na maioria dos casos, você não se interessa pelo código externo, então, a árvore de chamadas de Uso da CPU coleta as funções externas de um método de usuário em um nó **[Código Externo]**.

Para exibir os caminhos de chamada do código externo, na página principal do relatório de diagnóstico (painel direito), selecione **Mostrar Código Externo** na lista suspensa **Filtrar** e, em seguida, selecione **Aplicar**. O modo de exibição de **Árvore de Chamadas** da página **Uso da CPU** expande as chamadas de código externo. (A lista suspensa **Filtrar** está disponível na página principal do diagnóstico, não nas exibições detalhadas.)

![Mostrar Código Externo](../profiling/media/cpu_use_wt_filterview.png "Mostrar Código Externo")

Muitas cadeias de chamadas de código externo são muito aninhadas; portanto, a largura da cadeia pode exceder a largura de exibição da coluna **Nome da Função**. Os nomes de função são exibidos como **...**.

![Código externo aninhado na árvore de chamada](../profiling/media/cpu_use_wt_showexternalcodetoowide.png "Código externo aninhado na árvore de chamada")

Para localizar um nome de função que você está procurando, use a caixa de pesquisa. Passe o mouse sobre a linha selecionada ou use a barra de rolagem horizontal para exibir os dados.

::: moniker range=">=vs-2019"
![Pesquisar código externo aninhado](../profiling/media/vs-2019/cpu-use-wt-showexternalcodetoowide-found.png "Pesquisar código externo aninhado")
::: moniker-end
::: moniker range="vs-2017"
![Pesquisar código externo aninhado](../profiling/media/cpu_use_wt_showexternalcodetoowide_found.png "Pesquisar código externo aninhado")
::: moniker-end

### <a name="asynchronous-functions-in-the-cpu-usage-call-tree"></a><a name="BKMK_Asynchronous_functions_in_the_CPU_Usage_call_tree"></a>Funções assíncronas na árvore de chamadas de uso da CPU

 Quando o compilador encontra um método assíncrono, ele cria uma classe oculta para controlar a execução do método. Conceitualmente, a classe é uma máquina de estado. A classe tem funções geradas por compilador que chamam os métodos originais de maneira assíncrona e os retornos de chamada, agendadores e iteradores necessários para executá-los. Quando um método pai chama o método original, o compilador remove o método do contexto de execução do pai e executa os métodos de classe ocultos no contexto do código do sistema e da estrutura que controla a execução do aplicativo. Os métodos assíncronos são geralmente, mas nem sempre, executados em uma ou mais segmentos diferentes. Esse código é exibido na árvore de chamadas **Uso da CPU** como filhos do nó **[Código Externo]** imediatamente embaixo do nó superior da árvore.

No exemplo a seguir, os primeiros dois nós em **[Código Externo]** são os métodos gerados por compilador da classe da máquina de estado. O terceiro nó é a chamada ao método original.

![Nó assíncrono](media/cpu_use_wt_getmaxnumberasync_selected.png "Nó assíncrono")

Expanda os métodos gerados para mostrar o que está acontecendo:

![Nó assíncrono expandido](media/cpu_use_wt_getmaxnumberasync_expandedcalltree.png "Nó assíncrono expandido")

- `MainPage::GetMaxNumberAsyncButton_Click` apenas gerencia uma lista de valores da tarefa, calcula o máximo de resultados e exibe a saída.

- `MainPage+<GetMaxNumberAsyncButton_Click>d__3::MoveNext` mostra a atividade necessária para agendar e iniciar as 48 tarefas que encapsulam a chamada para `GetNumberAsync`.

- `MainPage::<GetNumberAsync>b__b` mostra a atividade das tarefas que chamam `GetNumber`.
