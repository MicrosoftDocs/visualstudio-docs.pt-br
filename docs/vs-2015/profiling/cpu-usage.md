---
title: Uso da CPU | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7501a20d-04a1-480f-a69c-201524aa709d
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7732a5757281e83c501a8258dd1d44b4f329a87a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548051"
---
# <a name="cpu-usage"></a>Uso da CPU
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você precisa investigar problemas de desempenho no aplicativo, um bom começo é entender como ele usa a CPU. A ferramenta **Uso da CPU** mostra a você os momentos em que a CPU está gastando tempo executando o código do Visual C++, Visual C#/Visual Basic e JavaScript.  
  
 A partir do Visual Studio 2015 Atualização 1, é possível ver um detalhamento por função do uso da CPU sem sair do depurador. É possível ativar e desativar a criação de perfil da CPU durante a depuração e exibir os resultados quando a execução é interrompida, por exemplo, em um ponto de interrupção. Para obter mais informações, consulte [Crie o perfil de sua CPU no Depurador do Visual Studio 2015](https://devblogs.microsoft.com/devops/profile-your-cpu-in-the-debugger-in-visual-studio-2015/).  
  
 Para obter um passo a passo que analisa o desempenho de um aplicativo da Windows Store, consulte [Analisar o uso da CPU nos aplicativos da Loja](https://msdn.microsoft.com/library/windows/apps/dn641982.aspx).  
  
 o hub de Desempenho e Diagnóstico oferece várias outras opções para executar e gerenciar a sessão de diagnóstico. Por exemplo, é possível executar a ferramenta **Uso da CPU** em computadores locais ou remotos ou em um simulador ou emulador. Você pode analisar o desempenho de um projeto aberto no Visual Studio, anexado a um aplicativo em execução ou iniciar um aplicativo instalado por meio da Windows Store. Para obter mais informações, consulte [executar ferramentas de criação de perfil sem depuração](https://msdn.microsoft.com/library/e97ce1a4-62d6-4b8e-a2f7-61576437ff01)  
  
## <a name="collect-cpu-usage-data"></a><a name="BKMK_Collect_CPU_usage_data"></a> Coletar dados de uso da CPU  
  
1. No Visual Studio, defina a configuração da solução como **Versão** e escolha o destino da implantação.  
  
    ![Selecionar versão e computador local](../profiling/media/cpuuse-selectreleaselocalmachine.png "CPUUSE_SelectReleaseLocalMachine")  
  
   - Executar o aplicativo no modo **Versão** fornece uma melhor exibição do desempenho real do aplicativo.  
  
   - Executar o aplicativo no computador local replica melhor a execução do aplicativo instalado.  
  
   - Se você estiver coletando dados de um dispositivo remoto, execute o aplicativo diretamente no dispositivo e não usando uma Conexão de Área de Trabalho Remota.  
  
   - Para aplicativos Windows Phone, coletar dados diretamente do **dispositivo** fornece os dados mais precisos.  
  
2. No menu **depurar** , escolha **criador de perfil de desempenho...**.  
  
3. Escolha **Uso da CPU** e, em seguida, **Iniciar**.  
  
    ![Escolher uso da CPU](../profiling/media/cpuuse-lib-choosecpuusage.png "CPUUSE_LIB_ChooseCpuUsage")  
  
4. Quando o aplicativo for iniciado, clique em **Obter Número Máximo**. Aguarde cerca de um segundo após a exibição da saída e escolha **Obter Número Máximo Assíncrono**. Esperar entre cliques de botão torna mais fácil isolar as rotinas de clique do botão no relatório de diagnóstico.  
  
5. Depois que a segunda linha de saída for exibida, escolha **Parar Coleção** no hub Desempenho e Diagnóstico.  
  
   ![Parar coleta de dados os](../profiling/media/cpu-use-wt-stopcollection.png "CPU_USE_WT_StopCollection")  
  
   A ferramenta Uso da CPU analisa os dados e exibe o relatório.  
  
   ![Relatório de os](../profiling/media/cpu-use-wt-report.png "CPU_USE_WT_Report")  
  
## <a name="analyze-the-cpu-usage-report"></a>Analise o relatório de uso da CPU  
  
### <a name="the-cpu-usage-call-tree"></a><a name="BKMK_The_CPU_Usage_call_tree"></a> A árvore de chamadas de Uso da CPU  
 Para começar a compreender as informações da árvore de chamadas, escolha novamente o segmento `GetMaxNumberButton_Click`, e veja os detalhes da árvore de chamadas.  
  
#### <a name="call-tree-structure"></a><a name="BKMK_Call_tree_structure"></a> Estrutura da árvore de chamadas  
 ![GetMaxNumberButton&#95;clique em árvore de chamadas](../profiling/media/cpu-use-wt-getmaxnumbercalltree-annotated.png "CPU_USE_WT_GetMaxNumberCallTree_annotated")  
  
|Imagem|Descrição|  
|-|-|  
|![Etapa 1](../profiling/media/procguid-1.png "ProcGuid_1")|O nó de nível superior nas árvores de chamada de uso da CPU é um pseudo-nó|  
|![Etapa 2](../profiling/media/procguid-2.png "ProcGuid_2")|Na maioria dos aplicativos, quando a opção **Mostrar Código Externo** está desabilitada, o nó de segundo nível é um nó **[Código Externo]** que contém o código do sistema e da estrutura que inicia e para o aplicativo, desenha a interface do usuário, controla o agendamento de thread e fornece ao aplicativo outros serviços de nível inferior.|  
|![Etapa 3](../profiling/media/procguid-3.png "ProcGuid_3")|Os filhos do nó de segundo nível são métodos e rotinas assíncronas do código de usuário que são chamados ou criados pelo sistema de segundo nível e código do framework.|  
|![Etapa 4](../profiling/media/procguid-4.png "ProcGuid_4")|Os nós filhos de um método só contêm dados das chamadas do método pai. Quando **Mostrar Código Externo** é desabilitado, os métodos de aplicativo também podem conter um nó **[Código Externo]**.|  
  
#### <a name="external-code"></a><a name="BKMK_External_Code"></a>Código externo  
 O código externo é uma função nos componentes do sistema e do framework executados pelo código que você grava. O código externo inclui funções que iniciam e param o aplicativo, elaboram a interface do usuário, controlam a segmentação e fornecem ao aplicativo outros serviços de nível inferior. Na maioria dos casos, você não se interessará pelo código externo, então, a árvore de chamadas de Uso da CPU coletará as funções externas de um método de usuário em um nó de **[Código Externo]**.  
  
 Quando desejar exibir os caminhos de chamada do código externo, escolha **Mostrar Código Externo** na lista **Exibição de filtro** e escolha **Aplicar**.  
  
 ![Escolha o modo de exibição de filtro e, em seguida, mostrar código externo](../profiling/media/cpu-use-wt-filterview.png "CPU_USE_WT_FilterView")  
  
 Saiba que muitas correntes de chamada de código externo são muito aninhadas, de forma que a largura da coluna Nome da Função pode exceder a largura da tela de todos os monitores de computador, exceto dos maiores. Quando isso acontece, os nomes de função são mostrados como **[...]**:  
  
 ![Código externo aninhado na árvore de chamada](../profiling/media/cpu-use-wt-showexternalcodetoowide.png "CPU_USE_WT_ShowExternalCodeTooWide")  
  
 Use a caixa de pesquisa para encontrar um nó que você está procurando, em seguida, use a barra de rolagem horizontal para trazer os dados para exibição:  
  
 ![Pesquisar código externo aninhado](../profiling/media/cpu-use-wt-showexternalcodetoowide-found.png "CPU_USE_WT_ShowExternalCodeTooWide_Found")  
  
### <a name="call-tree-data-columns"></a><a name="BKMK_Call_tree_data_columns"></a> Colunas de dados da árvore de chamadas  
  
|Propriedade|Descrição|
|-|-|  
|**CPU total (%)**|![Equação total de dados de %](../profiling/media/cpu-use-wt-totalpercentequation.png "CPU_USE_WT_TotalPercentEquation")<br /><br /> A porcentagem de atividade da CPU do aplicativo no intervalo de tempo selecionado que foi usado por chamadas para as funções e as funções chamadas pela função. Observe que isso é diferente do gráfico de linha de tempo **Utilização da CPU**, que compara a atividade total do aplicativo em um intervalo de tempo com a capacidade total disponível da CPU.|  
|**CPU própria (%)**|![Equação % própria](../profiling/media/cpu-use-wt-selflpercentequation.png "CPU_USE_WT_SelflPercentEquation")<br /><br /> A porcentagem de atividade da CPU do aplicativo no intervalo de tempo selecionado que foi usada pelas chamadas para as funções, exceto a atividade das funções chamadas pela função.|  
|**CPU total (ms)**|O número de milissegundos gastos em chamadas para a função no intervalo de tempo escolhido e as funções chamadas pela função.|  
|**CPU própria (ms)**|O número de milissegundos gastos em chamadas para a função no intervalo de tempo escolhido e as funções chamadas pela função.|  
|**Módulo**|O nome do módulo que contém a função ou o número de módulos que contêm as funções em um nó de [Código Externo].|  
  
### <a name="asynchronous-functions-in-the-cpu-usage-call-tree"></a><a name="BKMK_Asynchronous_functions_in_the_CPU_Usage_call_tree"></a> Funções assíncronas na árvore de chamadas de Uso da CPU  
 Quando o compilador encontra um método assíncrono, ele cria uma classe oculta para controlar o método de execução. Conceitualmente, a classe é uma máquina de estado que inclui uma lista de funções geradas pelo compilador que chamam corretamente as operações do método original de modo assíncrono, os retornos de chamadas, o agendador e os iteradores necessários a eles. Quando o método original é chamado por um método pai, o runtime remove o método do contexto de execução do pai e executa os métodos da classe oculta no contexto do código do sistema e do framework que controla a execução do aplicativo. Os métodos assíncronos são geralmente, mas nem sempre, executados em uma ou mais segmentos diferentes. Esse código é mostrado na árvore de chamadas de Uso da CPU como filhos do nó **[Código Externo]** logo abaixo do nó superior da árvore.  
  
 Para ver isso em nosso exemplo, escolha novamente o segmento `GetMaxNumberAsyncButton_Click` na linha de tempo.  
  
 ![GetMaxNumberAsyncButton&#95;clique em seleção de relatório](../profiling/media/cpu-use-wt-getmaxnumberasync-selected.png "CPU_USE_WT_GetMaxNumberAsync_Selected")  
  
 Os dois primeiros nós em **[Código Externo]** são os métodos gerados pelo compilador da classe de computador de estado. O terceiro é a chamada ao método original. Expandir os métodos gerados mostra o que está acontecendo.  
  
 ![GetMaxNumberAsyncButton expandida&#95;clique em árvore de chamadas](../profiling/media/cpu-use-wt-getmaxnumberasync-expandedcalltree.png "CPU_USE_WT_GetMaxNumberAsync_ExpandedCallTree")  
  
- `MainPage::GetMaxNumberAsyncButton_Click` faz muito pouco; gerencia uma lista de valores da tarefa, computa o máximo de resultados e exibe a saída.  
  
- `MainPage+<GetMaxNumberAsyncButton_Click>d__3::MoveNext` mostra a atividade necessária para agendar e iniciar as 48 tarefas que encapsulam a chamada para `GetNumberAsync`.  
  
- `MainPage::<GetNumberAsync>b__b` mostra a atividade das tarefas que chamam `GetNumber`.
