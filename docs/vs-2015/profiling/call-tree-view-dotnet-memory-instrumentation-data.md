---
title: Modo de exibição de árvore de chamadas – Dados de instrumentação da memória do .NET | Microsoft Docs
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
- Call Tree view
ms.assetid: dd359707-245a-4a36-8305-2e980b9edd53
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ed87363751c18794d9cf4c00e156d75760e0bf8d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51782499"
---
# <a name="call-tree-view---net-memory-instrumentation-data"></a>Modo de exibição de árvore de chamadas – Dados de instrumentação de memória do .NET
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O modo de exibição de árvore de chamada dos dados de criação de perfil de alocação de memória .NET que foram coletados usando o método de instrumentação exibe os caminhos de execução de função que foram percorridos no aplicativo com perfil. A raiz da árvore é o ponto de entrada do aplicativo ou componente. Cada nó de função lista todas as funções que ele chamou e os dados de memória e timing do .NET da função.  
  
 Os valores no modo de exibição de Árvore de Chamadas são para as instâncias de função que foram chamadas pela função pai na árvore de chamadas. Os valores de porcentagem são calculados comparando o valor de instância de função para o número total ou tamanho de alocações na execução da criação de perfil.  
  
## <a name="highlighting-the-execution-hot-path"></a>Realce do afunilamento de execução  
 O modo de exibição de árvore de chamada pode expandir e realçar o caminho de execução do processo ou a função que criou o maior ou a maioria dos objetos de memória. Para exibir o caminho mais ativo, clique com o botão direito do mouse no processo ou na função e, em seguida, clique em **Expandir Afunilamento**.  
  
## <a name="setting-the-call-tree-root-node"></a>Configuração do nó raiz da árvore de chamadas  
 Cada processo na execução de criação de perfil é exibido como um nó raiz. Defina o nó inicial do modo de exibição de árvore de chamadas clicando com o botão direito do mouse no nó que você deseja definir como o nó inicial e, em seguida, selecione **Definir Raiz**.  
  
 Ao definir o nó raiz, você elimina todas as outras entradas da visualização exceto a subárvore do nó selecionado. Você pode redefinir o nó raiz para o nó que você estava exibindo. Clique com o botão direito na janela do modo de exibição de árvore de chamada e selecione **Redefinir Raiz**.  
  
## <a name="general"></a>Geral  
  
|Column|Descrição|  
|------------|-----------------|  
|**Nome da Função**|O nome da função.|  
|**Endereço da Função**|O endereço da função.|  
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|  
|**Número de Chamadas**|O número total de chamadas feitas para essa função.|  
|**Arquivo de Origem**|O arquivo de origem que contém a definição dessa função.|  
|**Nome do Módulo**|O nome do módulo que contém a função.|  
|**Caminho do Módulo**|O demarcador do módulo que contém a função.|  
|**ID do Processo**|A ID de processo (PID) da criação de perfil.|  
|**Nome do Processo**|O nome atribuído ao processo.|  
|**Sobrecarga de Investigação Exclusiva de Tempo**|A sobrecarga de tempo para essa função que é causada pela instrumentação. A sobrecarga de investigação foi subtraída de todos os tempos exclusivos.|  
|**Sobrecarga de Investigação Inclusiva de Tempo**|A sobrecarga de tempo para essa função e as respectivas funções filho que é causada pela instrumentação. A sobrecarga de investigação foi subtraída de todos os tempos inclusivos.|  
|**Tipo**|O contexto da função:<br /><br /> -   **0** – a função atual<br />-   **1** – uma função que chama a função atual<br />-   **2** – uma função que é chamada pela função atual<br /><br /> Somente em relatórios de linha de comando [VSPerfReport](../profiling/vsperfreport.md).|  
|**Nome da Função Raiz**|O nome da função atual. Somente em relatórios de linha de comando [VSPerfReport](../profiling/vsperfreport.md).|  
  
## <a name="net-memory-values"></a>Valores de memória do .NET  
 Os valores de memória do .NET inclusivos de uma função indicam o número (alocações) e o tamanho (bytes) de objetos que foram criados pela função e as funções que foram chamadas pela outa função.  
  
 Os valores de memória exclusivos indicam o número e o tamanho dos objetos que foram criados pelo código no corpo da função, e não por funções chamadas pela outra função.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Alocações Inclusivas**|O número de objetos que foram alocados pelas instâncias desta função que foram chamadas pela função pai na árvore de chamada. Esse número inclui alocações feitas por funções filho.|  
|**% de Alocações Inclusivas**|A porcentagem de todos os objetos que foram criados na execução da criação de perfil que eram alocações inclusivas das instâncias de função que foram chamadas pela função pai na árvore de chamada.|  
|**Alocações Exclusivas**|O número de objetos que foram alocados pelas instâncias desta função que foram chamadas pela função pai na árvore de chamada. Esse número não inclui alocações feitas por funções filho.|  
|**% de Alocações Exclusivas**|A porcentagem de todos os objetos que foram criados na execução da criação de perfil que eram alocações exclusivas das instâncias de função que foram chamadas pela função pai na árvore de chamada.|  
  
## <a name="elapsed-inclusive-values"></a>Valores Inclusivos Decorridos  
 Os valores inclusivos decorridos indicam o tempo que uma função ficou na pilha de chamadas. O tempo inclui o tempo gasto em funções chamadas pela função e em chamadas para o sistema operacional, como mudanças de contexto e operações de entrada/saída.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo Decorrido**|O tempo total inclusivo decorrido de todas as chamadas a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
|**% de Tempo Inclusivo Decorrido**|O percentual do tempo inclusivo decorrido total da execução da criação de perfil que foi gasto no tempo inclusivo decorrido total dessa função quando foi chamada pela função na árvore de chamadas.|  
|**Tempo Inclusivo Decorrido Médio**|O tempo médio inclusivo decorrido de uma chamada a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
|**Tempo Inclusivo Decorrido Máximo**|O tempo máximo inclusivo decorrido de uma chamada a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
|**Tempo Inclusivo Decorrido Mínimo**|O tempo mínimo inclusivo decorrido de uma chamada a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
  
## <a name="elapsed-exclusive-values"></a>Valores Exclusivos Decorridos  
 Valores exclusivos decorridos indicam o tempo durante o qual uma função estava diretamente em execução no topo da pilha de chamadas. O tempo inclui o tempo em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto. No entanto, o tempo não inclui o tempo gasto em funções que foram chamadas pela função.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo Decorrido**|O tempo total exclusivo decorrido de todas as chamadas a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
|**% de Tempo Exclusivo Decorrido**|O percentual do tempo total exclusivo decorrido da execução da criação de perfil que foi gasto no tempo total exclusivo decorrido dessa função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
|**Tempo Exclusivo Decorrido Médio**|O tempo médio exclusivo decorrido de uma chamada a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
|**Tempo Exclusivo Decorrido Máximo**|O tempo máximo exclusivo decorrido de uma chamada a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
|**Tempo Exclusivo Decorrido Mínimo**|O tempo mínimo exclusivo decorrido de uma chamada a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
  
## <a name="application-inclusive-values"></a>Valores Inclusivos do Aplicativo  
 Os valores inclusivos do aplicativo indicam o tempo que uma função ficou na pilha de chamadas. O tempo não inclui o tempo gasto em chamadas para o sistema operacional, como operações de entrada/saída e de mudança de contexto. O tempo inclui o tempo gasto em funções filho que foram chamadas pela função.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Inclusivo do Aplicativo**|O tempo total inclusivo do aplicativo de todas as chamadas a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
|**% de Tempo Inclusivo do Aplicativo**|O percentual do tempo total inclusivo decorrido da execução da criação de perfil que foi gasto no tempo total inclusivo do aplicativo dessa função, quando ela tiver sido chamada pela função na árvore de chamadas.|  
|**Tempo Inclusivo Médio do Aplicativo**|O tempo médio inclusivo do aplicativo de uma chamada a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
|**Tempo Inclusivo Máximo do Aplicativo**|O tempo máximo inclusivo do aplicativo de uma chamada a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
|**Tempo Inclusivo Mínimo do Aplicativo**|O tempo mínimo inclusivo do aplicativo de uma chamada a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
  
## <a name="application-exclusive-values"></a>Valores Exclusivos do Aplicativo  
 Valores exclusivos do aplicativo indicam o tempo gasto na função, excluindo o tempo gasto em funções filho chamadas pela função. O tempo também exclui as chamadas para o sistema operacional, como alterações de contexto e operações de entrada/saída.  
  
|Column|Descrição|  
|------------|-----------------|  
|**Tempo Exclusivo do Aplicativo**|O tempo total exclusivo do aplicativo de todas as chamadas a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
|**% de Tempo Exclusivo do Aplicativo**|O percentual do tempo total exclusivo decorrido da execução da criação de perfil que foi gasto no tempo total exclusivo do aplicativo dessa função, quando ela tiver sido chamada pela função na árvore de chamadas.|  
|**Tempo Exclusivo Médio do Aplicativo**|O tempo médio exclusivo do aplicativo de todas as chamadas a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
|**Tempo Exclusivo Máximo do Aplicativo**|O tempo máximo exclusivo do aplicativo de todas as chamadas a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|  
|**Tempo Exclusivo Mínimo do Aplicativo**|O tempo mínimo exclusivo do aplicativo de todas as chamadas a esta função, quando ela tiver sido chamada pela função pai na árvore de chamadas.|



