---
title: Modo de exibição de árvore de chamadas – Dados de amostragem | Microsoft Docs
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
- sampling profiling method,Call Tree view
- Call Tree view
ms.assetid: 5c4e8ec3-d0d3-485a-93bd-9060df4eb739
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dc324b621bfc3e472d6eb86227a6081e3384d2af
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51798905"
---
# <a name="call-tree-view---sampling-data"></a>Modo de exibição de árvore de chamadas – Dados de amostragem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O modo de exibição de Árvore de Chamadas exibe os caminhos de execução de função que foram percorridos no aplicativo analisado.  
  
> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos da Windows Store também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).  
  
 A raiz da árvore é o ponto de entrada do aplicativo ou do componente. Cada nó da função lista todas as funções que ela chamou e os dados de desempenho sobre essas chamadas de função.  
  
 Os valores no modo de exibição de Árvore de Chamadas são para as instâncias de função que foram chamadas pela função pai na árvore de chamadas. Valores de percentual são calculados comparando o valor de instância de função para o número total de amostras na execução de criação de perfil.  
  
## <a name="highlighting-the-execution-hot-path"></a>Realce do afunilamento de execução  
 O modo de exibição de Árvore de Chamada pode expandir e realçar o caminho de execução do processo ou da função que foram amostrados com mais frequência. Para exibir o caminho mais ativo, clique com o botão direito do mouse no processo ou na função e, em seguida, clique em **Expandir Afunilamento**.  
  
## <a name="setting-the-call-tree-root-node"></a>Configuração do nó raiz da árvore de chamadas  
 Cada processo na execução de criação de perfil é exibido como um nó raiz. Para definir o nó inicial do modo de exibição de Árvore de Chamadas, clique com o botão direito do mouse no nó que você deseja definir como o nó inicial e selecione **Definir Raiz**.  
  
 Ao definir o nó raiz, você elimina todas as outras entradas da visualização exceto a subárvore do nó selecionado. Para redefinir o nó raiz de volta para o nó original, clique com botão direito do mouse na janela Modo de Exibição de Árvore de Chamadas e selecione **Redefinir Raiz**.  
  
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
|**Nível**|A profundidade dessa função na árvore de chamadas. Somente em relatórios de linha de comando [VSPerfReport](../profiling/vsperfreport.md).|  
|**Amostras Exclusivas**|O número de amostras coletadas nessa função quando ela foi chamada pela função pai na árvore de chamadas. Esse número não inclui amostras coletadas em funções que foram chamadas pela função.|  
|**% de Amostras Exclusivas**|O percentual de todas as amostras na execução de criação de perfil que eram amostras exclusivas dessa função quando ela foi chamada pela função pai na árvore de chamadas.|  
|**Amostras Inclusivas**|O número de amostras coletadas nessa função quando ela foi chamada pela função pai na árvore de chamadas. Esse número inclui amostras coletadas em funções chamadas pela função.|  
|**% de Amostras Inclusivas**|O percentual de todas as amostras na execução de criação de perfil que eram amostras inclusivas dessa função quando ela foi chamada pela função pai na árvore de chamadas.|  
  
## <a name="see-also"></a>Consulte também  
 [Como personalizar as colunas de exibição do relatório](../profiling/how-to-customize-report-view-columns.md)   
 [Modo de exibição de árvore de chamadas – dados de amostragem do criador de perfil](../profiling/call-tree-view-sampling-data.md)   
 [Modo de exibição de árvore de chamadas – amostragem](../profiling/call-tree-view-dotnet-memory-sampling-data.md)   
 [Modo de exibição de árvore de chamadas – instrumentação](../profiling/call-tree-view-dotnet-memory-instrumentation-data.md)   
 [Modo de exibição de árvore de Chamadas](../profiling/call-tree-view-instrumentation-data.md)



