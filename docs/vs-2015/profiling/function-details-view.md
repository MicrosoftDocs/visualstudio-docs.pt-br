---
title: Exibição Detalhes da Função | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.performance.view.functiondetails
helpviewer_keywords:
- Function Details view
- Profiling Tools, Function Details view
ms.assetid: 8806954f-cf28-48d5-81b2-d722ceaf7d27
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e6f2246cfe9eb2ae9ae6641ca316db440f153f92
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51799577"
---
# <a name="function-details-view"></a>Exibição de detalhes da função
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A janela **Exibição Detalhes da Função** exibe as seguintes informações:  
  
- O gráfico de barras **Distribuição de Custos** representa os relacionamentos entre uma função selecionada e as funções de chamada que executaram a função selecionada e entre a função selecionada e as funções que foram chamadas por ela.  
  
- A tabela **Detalhes de Desempenho da Função** que mostra um resumo dos dados de criação para a função que você especificar.  
  
- A janela **Exibição Código de Função**, que mostra o código de função quando o código está disponível.  
  
  A janela **Exibição Código de Função** é um painel separado. Por padrão, os dois painéis são divididos horizontalmente e a janela **Exibição Código de Função** encontra-se na parte inferior do quadro.  
  
- Para dividir os dois painéis verticalmente, clique em **Dividir a Tela Verticalmente** na barra de ferramentas.  
  
- Para alterar o tamanho relativo dos painéis, clique na borda sombreada entre os quadros e arraste-a para um local diferente.  
  
## <a name="cost-distribution-bar-chart"></a>Gráfico de barras da distribuição de custo  
  
### <a name="performance-metrics"></a>Métricas de desempenho  
 Na lista suspensa **Métrica de desempenho**, você pode especificar quais valores são exibidos na exibição. Os valores disponíveis dependem do método de criação de perfil usado no arquivo de dados de criação de perfil. Os nomes entre parênteses são os nomes das linhas na tabela **Detalhes de Desempenho da Função**.  
  
### <a name="bar-chart"></a>Gráfico de Barras  
 **Funções de Chamada**  
  
 A barra **Funções de Chamada** mostra as funções que chamaram a função selecionada. O tamanho do bloco que contém a função de chamada é proporcional à contribuição da função de chamada para o valor total da métrica de desempenho para a função selecionada.  
  
 Você pode clicar no nome de uma função de chamada para transformá-la na função selecionada da exibição.  
  
- Se houver muitas funções de chamada para listar, as funções com as menor contribuição serão coletadas em um bloco **Outros**. Clique em **Outros** para exibir todas as funções que chamam são chamadas pela função selecionada na janela **Exibição de Chamador/Receptor**. Para obter mais informações, consulte a [Exibição de Chamador/Computador chamado](../profiling/caller-callee-view.md).  
  
- Se não houver nenhuma função de chamada ou se a função for a função de entrada de um thread ou processo, um bloco **Topo da Pilha** será exibido.  
  
  **Função selecionada**  
  
  A barra de função selecionada mostra as contribuições de funções chamadas e do código na função selecionada para a métrica de desempenho total da função selecionada. O tamanho do bloco que contém uma função chamada ou o corpo da função é proporcional à contribuição ao valor total da métrica de desempenho para a função selecionada.  
  
  Você pode clicar no nome de uma função chamada para transformá-la na função selecionada da exibição.  
  
- O valor **Total** é a métrica de desempenho para a função selecionada.  
  
- O bloco **Corpo da Função** representa o valor do total da métrica de desempenho que ocorreu na execução direta do código no corpo da função.  
  
- Funções que são chamadas pela função selecionada são listadas em blocos. O tamanho do bloco de funções selecionadas representa a quantidade da métrica de desempenho total para a função selecionada que ocorreu na função chamada.  
  
- Se houver muitas funções de chamada para listar, as funções com as menor contribuição serão coletadas em um bloco **Outros**. Clique em **Outros** para exibir todas as funções que chamam são chamadas pela função selecionada na janela **Exibição de Chamador/Receptor**. Para obter mais informações, consulte a [Exibição de Chamador/Computador chamado](../profiling/caller-callee-view.md).  
  
- Se não houver nenhuma função chamada, um bloco **Fundo da Pilha** será exibido.  
  
## <a name="function-performance-details"></a>Detalhes de Desempenho da Função  
 A tabela de Detalhes de Desempenho da Função fornece dados de resumo para as métricas de desempenho da função selecionada. O valor e o percentual aparecem. Especifique os dados de criação de perfil que aparecem no gráfico e a tabela de detalhes na lista **Métrica de desempenho**.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Exclusivo**|‑   O valor da métrica de desempenho que ocorreu na execução do corpo da função.|  
|**Em Chamadas**|‑   O valor da métrica de desempenho que ocorreu em funções que a função selecionada chamou.|  
|**Total Inclusivo**|‑   O total dos valores **Exclusivo** e **Em Chamadas**.|  
  
## <a name="function-code-view"></a>Modo de Exibição de Código de Função  
 A janela **Exibição de Código de Função** exibe uma lista do código-fonte quando ela está disponível. Ao lado das linhas de código-fonte que chamam outras funções, uma coluna sombreada contém os valores de métrica de desempenho para a função chamada. Para editar o código-fonte, clique no link para o arquivo de código-fonte.  
  
## <a name="cost-distribution-bar-chart-values"></a>Valores de gráfico de barras da distribuição de custo  
  
### <a name="sampling"></a>Amostragem  
 A tabela a seguir explica os valores na lista Métrica de Desempenho para os dados de criação de perfil coletados usando o método de amostragem.  
  
|||  
|-|-|  
|**Amostras Inclusivas (Amostras Coletadas)**|‑   Para uma função de chamada, o número de amostras que foram coletados quando a função selecionada foi chamada por essa função de chamada.<br />‑   Para o Corpo da Função, o número de exemplos que foram coletados quando a função selecionada estava executando seu próprio código.<br />‑   Para uma função chamada, o número de amostras que foram coletados quando a função chamada estava em execução devido a uma chamada da função selecionada.|  
  
### <a name="instrumentation"></a>Instrumentação  
 A tabela a seguir explica os valores na lista Métrica de Desempenho para os dados de criação de perfil coletados usando o método de instrumentação.  
  
|||  
|-|-|  
|**Tempo Inclusivo Decorrido (Tempo Decorrido)**|O tempo decorrido inclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudanças de contexto.<br /><br /> ‑   Para uma **Função de Chamada**, a quantidade de tempo decorrido gasto para executar as instâncias da função selecionada que foram chamadas pela função. O tempo gasto nas funções que foram chamadas pela função selecionada é incluído.<br />‑   Para o **Corpo da Função**, a quantidade total de tempo decorrido gasto para executar o código da função selecionada. O tempo gasto nas funções chamadas não é incluído.<br />‑   Para uma função chamada, a quantidade de tempo decorrido gasto para executar as instâncias da função que foram chamadas pela função selecionada. O total inclui o tempo gasto em funções que foram chamadas pela função. O tempo gasto nas funções que foram chamadas pela função selecionada é incluído.|  
|**Tempo Inclusivo do Aplicativo (Tempo de Aplicação)**|O tempo de aplicação não inclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto.<br /><br /> ‑   Para uma **Função de Chamada**, a quantidade de tempo de aplicação que foi gasto para executar as instâncias da função selecionada que foram chamadas pela função. O tempo gasto nas funções que foram chamadas pela função selecionada é incluído.<br />‑   Para o **Corpo da Função**, a quantidade total de tempo de aplicação gasto para executar o código da função selecionada. O tempo gasto nas funções chamadas não é incluído.<br />‑   Para uma função chamada, a quantidade de tempo de aplicação gasto para executar as instâncias da função que foram chamadas pela função selecionada. O total inclui o tempo gasto em funções que foram chamadas pela função.|  
  
### <a name="net-memory"></a>Memória do .NET  
 A tabela a seguir explica os valores na lista Métrica de Desempenho para os dados de criação de perfil coletados usando o método de criação de perfil de memória .NET.  
  
|||  
|-|-|  
|**Alocações Inclusivas (Alocações)**|–   Para uma **Função de Chamada**, o número de objetos alocados pelas instâncias da função selecionada que a função chamou. O número inclui objetos que foram alocados por funções que a função selecionada chamou.<br />–   Para o **Corpo da Função**, o número de objetos que foram coletados pela função selecionada quando estava executando seu próprio código. Objetos alocados em funções chamadas por essa função selecionada não são incluídos.<br />–   Para uma função chamada, o número de objetos que foram alocados pela instância da função que foram chamados pela função selecionada. O número inclui objetos que foram alocados por funções que a função chamou.|  
|**Bytes Inclusivos (Bytes)**|–   Para uma **Função de Chamada**, o número de bytes alocados pelas instâncias da função selecionada que a função chamou. O número inclui bytes que foram alocados por funções que a função selecionada chamou.<br />–   Para o **Corpo da Função**, o número total de bytes que foram alocados pela função selecionada quando ela estava executando seu próprio código. Bytes alocados em funções chamadas pela função selecionada não são incluídos.<br />–   Para uma função chamada, o número de bytes que foram alocados pela instância da função que foram chamados pela função selecionada. O número inclui bytes que foram alocados por funções que a função chamou.|  
  
### <a name="concurrency"></a>Concorrência  
 A tabela a seguir explica os valores na lista Métrica de Desempenho para os dados de criação de perfil coletados usando o método de simultaneidade.  
  
|||  
|-|-|  
|**Contenções Inclusivas (Contenções)**|–   Para uma **Função de Chamada**, o número de eventos de contenção de recursos que ocorreram nas instâncias da função selecionada que a função chamou. O número inclui eventos de contenção em funções que a função selecionada chamou.<br />–   Para o **Corpo da Função**, o número total de eventos de contenção que ocorreram quando a função estava executando seu próprio código. As contenções que ocorreram nas funções que foram chamadas pelas função selecionada não são incluídas.<br />–   Para uma função chamada, o número de eventos de contenção que ocorreram nas instâncias da função que foram chamadas pela função selecionada. O número inclui eventos de contenção que ocorreram nas funções que a função chamou.|  
|**Tempo Bloqueado Inclusivo (Tempo Bloqueado)**|–   Para uma função de chamada, o tempo gasto em eventos de contenção de recursos para as instâncias da função selecionada que a função chamou. O tempo inclui o tempo bloqueado em funções que a função selecionada chamou.<br />–   Para o **Corpo da Função**, o tempo total que foi gasto em eventos de contenção que ocorreram quando a função estava executando seu próprio código. As contenções que ocorreram nas funções que a função selecionada chamou não são incluídas.<br />–   Para uma função chamada, o tempo gasto em eventos de contenção de recursos para as instâncias da função que a função selecionada chamou. O tempo inclui o tempo bloqueado que ocorreu em funções que a função selecionada chamou.|



