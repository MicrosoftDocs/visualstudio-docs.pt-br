---
title: Exibição Detalhes do Thread – Dados de contenção | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.view.threaddetails
helpviewer_keywords:
- Thread Details view
ms.assetid: 874c3b1c-88d8-479a-bb35-1291d9aa8e67
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e832088c49366cee3cb2a4f45df7a1250171e7df
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49849522"
---
# <a name="thread-details-view---contention-data"></a>Exibição Detalhes do Thread – dados de contenção
A exibição Detalhes do Thread apresenta um gráfico de linha do tempo dos eventos de bloqueio no thread selecionado de uma execução de criação de perfil que foram causados por contenções em recursos. Um evento de bloqueio ocorre quando o thread é forçado a suspender a execução porque outro thread bloqueou o acesso a um recurso.  
  
 Esta exibição representa a linha do tempo de execução do thread como uma barra horizontal e os eventos de bloqueio como uma barra vertical em uma linha do tempo horizontal do thread. Quando necessário, é possível ampliar uma seção da linha do tempo para exibir os eventos individuais. Para exibir o caminho de execução das funções que levaram ao evento, clique na barra de eventos. As funções aparecem na janela **Pilha de Chamadas**. Quando o código-fonte de uma função está disponível, é possível clicar no nome da função para editar o arquivo de origem na IDE do Visual Studio.  
  
## <a name="navigate-the-timeline"></a>Navegar pela linha do tempo  
  
#### <a name="to-zoom-in-on-a-timeline-segment"></a>Para ampliar um segmento de linha do tempo  
  
-   Clique e arraste o ponteiro do mouse para selecionar uma área da linha do tempo.  
  
     Ao liberar o mouse, a exibição amplia o segmento de tempo selecionado. É possível repetir o processo para aplicar zoom mais detalhadamente. A caixa de rolagem na barra de rolagem de tempo representa o tamanho relativo do segmento de tempo que aparece na exibição.  
  
#### <a name="to-zoom-out-on-a-timeline"></a>Para reduzir uma linha do tempo  
  
-   Clique em **Reduzir** para retornar ao nível de zoom anterior.  
  
-   Clique em **Redefinir Zoom** para mostrar a linha do tempo inteira na exibição.  
  
#### <a name="to-view-the-call-stack-of-an-event"></a>Para exibir a pilha de chamadas de um evento  
  
-   No grafo de linha do tempo, clique na barra vertical que representa o evento.  
  
#### <a name="to-view-or-edit-the-source-code-of-a-function-in-the-call-stack"></a>Para exibir ou editar o código-fonte de uma função na pilha de chamadas  
  
- Na janela **Pilha de Chamadas**, clique no nome da função.  
  
  O código-fonte da função deve fazer parte do projeto atual.  
  
#### <a name="to-view-the-contention-events-of-a-resource-in-all-threads-in-the-profiling-run"></a>Para exibir os eventos de contenção de um recurso em todos os threads na execução de criação de perfil  
  
-   No grafo de linha do tempo, clique no nome ou na ID do recurso.  
  
     A [Exibição Detalhes do Recurso](../profiling/resource-details-view-contention-data.md) é mostrada para o recurso selecionado.  
  
#### <a name="to-view-the-thread-contention-data-in-the-processes-window"></a>Para exibir os dados de contenção de thread na janela Processos  
  
-   No gráfico de linha do tempo, clique em **Total**.  
  
     A [Exibição Processo](../profiling/process-view-contention-data.md) é mostrada com o thread selecionado.