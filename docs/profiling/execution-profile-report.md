---
title: Relatório do perfil de execução | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.report.execution
helpviewer_keywords:
- Concurrency Visualizer, Execution Profile Report
ms.assetid: c8128472-a8ed-46f4-b1c8-a25358d6f2c1
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: fa0800bcf6a4fedfbcd8c787b3cca89638e9bcb9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49935283"
---
# <a name="execution-profile-report"></a>Relatório do perfil de execução
O relatório do perfil de execução é um perfil de amostragem tradicional. As amostras são colhidas aproximadamente a cada milissegundo durante períodos quando um thread está sendo executado em um núcleo lógico e a Visualização Simultânea cria uma árvore de chamada típica agrupando o conjunto acumulado de pilhas de amostra. Os dados nessa tabela podem ser afetados pelo intervalo de tempo atual e pelos threads ocultos e pelos seguintes filtros que podem ser aplicados:  
  
- Se Apenas Meu Código estiver selecionado, somente os registros de ativação com código do usuário, além de um nível abaixo do código de usuário, serão mostrados.  
  
- Se o valor de redução de ruído for definido, as pilhas agrupadas com menor frequência que a frequência especificada serão filtradas fora do relatório  
  
  A tabela a seguir mostra as colunas no relatório.  
  
|Column|Descrição|  
|------------|-----------------|  
|Nome|O nome da função para cada nível da pilha de chamadas.|  
|Amostras inclusivas|O número total de amostras que são coletadas para todas as pilhas que rolam até esse nível da árvore de pilha de chamadas. O número inclusivo é a soma das amostras exclusivas para essa função e dos contadores inclusivos para todos os seus nós filho.|  
|Amostras Exclusivas|O número total de amostras coletadas para o qual essa função é o nível mais baixo da pilha de chamadas.|  
|% Inclusivo|O percentual do total de amostras que é mostrada na coluna de amostras inclusivas. As porcentagens são arredondadas para duas casas decimais.|  
|% Exclusivo|O percentual do total de amostras que é mostrado na coluna de amostras exclusivas. As porcentagens são arredondadas para duas casas decimais.|  
|Detalhes|O nome totalmente qualificado da função. Isso inclui a contagem de linha, quando disponível.|  
  
 Esta tabela de relatório pode ser vista na exibição [Tempo de execução (exibição de threads)](../profiling/execution-time-threads-view.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de Threads](../profiling/threads-view-parallel-performance.md)