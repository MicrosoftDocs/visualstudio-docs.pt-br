---
title: Exibição de detalhes de recurso – Dados de contenção | Microsoft Docs
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
- vs.performance.view.resourcedetails
helpviewer_keywords:
- Resource Details view
ms.assetid: a4ecfe1c-abbc-4fb3-9ab2-34de50486901
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 98cc1d3f281108ef23f073ceae69d97fa3c0c32a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51782460"
---
# <a name="resource-details-view---contention-data"></a>Exibição de detalhes do recurso – Dados de contenção
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A exibição de Detalhes do Recurso apresenta um gráfico de linha do tempo dos eventos de bloqueio que foram causados por contenções em um recurso selecionado. Um evento de bloqueio ocorre quando um thread é forçado a suspender a execução porque outro thread bloqueou o acesso ao recurso.  
  
 Este modo de exibição representa a linha do tempo de execução de cada thread como uma barra horizontal e cada evento de bloqueio como uma barra vertical na linha do tempo do thread. Quando necessário, você pode ampliar uma seção da linha do tempo para exibir eventos individuais. Para exibir o caminho de execução (pilha de chamadas) das funções que levou ao evento, clique na barra de evento. As funções aparecem na janela **Pilha de Chamadas**. Quando o código-fonte para uma função estiver disponível, você pode clicar no nome de função para editar o arquivo de origem na interface para [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="to-magnify-a-timeline-segment"></a>Para ampliar um segmento de linha do tempo  
  
-   Arraste o ponteiro do mouse sobre uma área da linha do tempo.  
  
     Quando você soltar o botão do mouse, o modo de exibição ampliará o segmento de tempo selecionado. Você pode repetir o processo para ampliar ainda mais o segmento. A caixa de rolagem na barra de rolagem de tempo representa o tamanho relativo do segmento de tempo que aparece na exibição.  
  
#### <a name="to-zoom-out-on-a-timeline"></a>Para reduzir uma linha do tempo  
  
-   Execute uma das seguintes etapas:  
  
    -   Clique em **Reduzir** para retornar ao nível de zoom anterior.  
  
    -   Clique em **Redefinir Zoom** para mostrar toda a linha do tempo na exibição.  
  
#### <a name="to-view-the-call-stack-of-an-event"></a>Para exibir a pilha de chamadas de um evento  
  
-   No gráfico de linha do tempo, clique na barra de eventos.  
  
#### <a name="to-view-or-edit-the-source-code-of-a-function-in-the-call-stack"></a>Para exibir ou editar o código-fonte de uma função na pilha de chamadas  
  
- Na janela **Pilha de Chamadas**, clique no nome da função.  
  
  O código-fonte da função deve fazer parte do projeto atual.  
  
#### <a name="to-view-the-call-tree-of-contention-events-for-the-resource"></a>Para exibir a árvore de chamadas de eventos de contenção do recurso  
  
-   No gráfico de linha do tempo, clique em **Total**.  
  
     A exibição Contenções aparece para o recurso. Para obter mais informações, consulte [Exibição de Contenções de Recursos](../profiling/resource-contentions-view-contention-data.md)  
  
#### <a name="to-view-all-the-contention-events-of-a-thread"></a>Para exibir todos os eventos de contenção de um thread  
  
-   No gráfico de linha do tempo, clique no nome ou ID do thread.  
  
     A Exibição de Detalhes de Thread é exibida para o thread selecionado. Para obter mais informações, consulte [Exibição de Detalhes do Thread](../profiling/thread-details-view-contention-data.md).



