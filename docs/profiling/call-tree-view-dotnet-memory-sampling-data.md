---
title: Modo de exibição de árvore – Dados de amostragem de memória do .NET | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Call Tree view
ms.assetid: fbb6cb60-420b-4ca9-8306-2494f7d321fe
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: c3c7c70057380289272e86cf7187680746dafdd2
ms.sourcegitcommit: 37144589d9f850ff81ec7bfb884429989925a43d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34336039"
---
# <a name="call-tree-view---net-memory-sampling-data"></a>Modo de exibição de árvore de chamadas – dados de amostragem de memória do .NET
O modo de exibição de Árvore de Chamadas exibe os caminhos de execução de função que foram percorridos no aplicativo analisado. A raiz da árvore é o ponto de entrada do aplicativo ou do componente. Cada nó de função lista todas as funções que ele chamou e os dados de alocação de memória do .NET sobre essas chamadas de função.  
  
 Os valores no modo de exibição de Árvore de Chamadas são para as instâncias de função que foram chamadas pela função pai na árvore de chamadas. Os valores de porcentagem são calculados comparando o valor de instância de função para o número total ou tamanho de alocações na execução da criação de perfil.  
  
## <a name="highlight-the-execution-hot-path"></a>Realçar o afunilamento de execução  
 O modo de exibição de árvore de chamada pode expandir e realçar o caminho de execução do processo ou a função que criou o maior ou a maioria dos objetos de memória. Para exibir o caminho mais ativo, clique com o botão direito do mouse no processo ou na função e, em seguida, clique em **Expandir Afunilamento**.  
  
## <a name="set-the-call-tree-root-node"></a>Configurar do nó raiz da árvore de chamadas  
 Cada processo na execução de criação de perfil é exibido como um nó raiz. Para definir o nó inicial do modo de exibição de árvore de chamadas, clique com o botão direito do mouse no nó que você deseja definir como o nó inicial e selecione **Definir Raiz**.  
  
 Ao definir o nó raiz, você elimina todas as outras entradas da visualização exceto a subárvore do nó selecionado. Você pode redefinir o nó raiz para o nó que você estava exibindo. Clique com o botão direito do mouse na janela do modo de exibição de árvore de chamada e selecione **Redefinir Raiz**.  
  
|Column|Descrição|  
|------------|-----------------|  
|**ID do Processo**|A ID de processo (PID) da criação de perfil.|  
|**Nome do Processo**|O nome do processo.|  
|**Nome do Módulo**|O nome do módulo que contém a função.|  
|**Caminho do Módulo**|O demarcador do módulo que contém a função.|  
|**Arquivo de Origem**|O arquivo de origem que contém a definição dessa função.|  
|**Nome da Função**|O nome totalmente qualificado da função.|  
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|  
|**Endereço da Função**|O endereço da função.|  
|**Nível**|A profundidade da função na árvore de chamadas.|  
|**Alocações Inclusivas**|O número de objetos que foram alocados pelas instâncias desta função que foram chamadas pela função pai na árvore de chamada. Esse número inclui alocações feitas por funções filho.|  
|**% de Alocações Inclusivas**|O percentual de todos os objetos que foram criados na execução de criação de perfil que eram alocações inclusivas dessa função.|  
|**Alocações Exclusivas**|O número de objetos que foram alocados pelas instâncias desta função que foram chamadas pela função pai na árvore de chamada. Esse número não inclui alocações feitas por funções filho.|  
|**% de Alocações Exclusivas**|O percentual de todos os objetos que foram criados na execução da criação de perfil que eram alocações exclusivas das instâncias de função que foram chamadas pela função pai na árvore de chamada.|  
|**Bytes Inclusivos**|O número de bytes na memória que foram alocados pelas instâncias desta função que foram chamadas pela função pai na árvore de chamada. Esse número inclui alocações feitas por funções filho.|  
|**% de Bytes Inclusivos**|O percentual de todos os bytes de memória que foram alocados na execução de criação de perfil que eram alocações inclusivas dessa função.|  
|**Bytes Exclusivos**|O número de bytes na memória que foram alocados pelas instâncias desta função que foram chamadas pela função pai na árvore de chamada. Esse número não inclui alocações feitas por funções filho.|  
|**% de Bytes Exclusivos**|O percentual de todos os bytes de memória que foram alocados na execução de criação de perfil que eram alocações exclusivas dessa função.|  
  
## <a name="see-also"></a>Consulte também  
 [Modo de exibição de árvore de chamadas – instrumentação](../profiling/call-tree-view-dotnet-memory-instrumentation-data.md)   
 [Modo de exibição de árvore de chamadas](../profiling/call-tree-view-sampling-data.md)   
 [Modo de exibição de árvore de chamadas](../profiling/call-tree-view-instrumentation-data.md)