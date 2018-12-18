---
title: Exibição de árvore de chamadas | Microsoft Docs
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
- vs.performance.view.calltree
helpviewer_keywords:
- Call Tree view
- profiling tools reports, Call Tree view
- performance reports, Call Tree view
- profiling tools, Call Tree view
ms.assetid: b2dbc033-bf95-4d10-8e51-f9462979133e
caps.latest.revision: 39
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8f09b85c20d84cb25d6a1fdbbd8493c47056318a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51738744"
---
# <a name="call-tree-view"></a>Exibição de árvore de chamadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O modo de exibição de Árvore de Chamadas exibe os caminhos de execução de função que foram percorridos no aplicativo analisado. A raiz da árvore é o ponto de entrada do aplicativo ou do componente. Cada nó da função lista todas as funções que ela chamou e os dados de desempenho sobre essas chamadas de função.  
  
 O Modo de exibição de árvore de Chamadas também expande e realça o caminho de execução de uma função que consumiu mais tempo ou que gerou amostras com mais frequência. Para exibir o caminho com mais custo de desempenho, clique com o botão direito do mouse na função e, em seguida, clique em **Expandir Afunilamento**.  
  
 Cada processo na execução de criação de perfil é exibido como um nó raiz. Você pode definir o nó inicial do modo de exibição de árvore de chamadas clicando duas vezes no nó que você deseja definir como o nó inicial e, em seguida, selecionar **Definir Raiz**.  
  
 Ao definir o nó raiz, você elimina todas as outras entradas da visualização exceto a subárvore do nó selecionado. Você pode redefinir o nó raiz para o nó que você estava exibindo. Na janela de exibição de árvore de chamadas, clique com o botão direito do mouse e selecione **Redefinir Raiz**.  
  
 A exibição de árvore de chamadas pode ser personalizada para adicionar ou remover colunas. Clique com o botão direito do mouse na **Barra de Título do Nome da Coluna** e, em seguida, selecione **Adicionar/remover Colunas**.  
  
 A exibição de árvore de chamadas pode ser configurada para redução de ruído, limitando a quantidade de dados que são apresentados. Ao usar a redução de ruído, os problemas de desempenho serão mais proeminentes na visualização. Quando os problemas de desempenho são fáceis de distinguir, a análise é mais fácil. Para obter mais informações, confira [Como: configurar a redução de ruído em exibições de relatório](../profiling/how-to-configure-noise-reduction-in-report-views.md).  
  
> [!NOTE]
>  Se a redução de ruído está configurada para exibir um aviso quando está ativada, uma barra de informações é exibida no relatório.  
  
 Para obter mais informações sobre as definições de colunas na exibição de árvore de chamadas, confira o seguinte:  
  
 [Modo de exibição de árvore de Chamadas](../profiling/call-tree-view-sampling-data.md)  
  
 [Modo de exibição de árvore de Chamadas](../profiling/call-tree-view-instrumentation-data.md)  
  
 [Modo de exibição de árvore de chamadas – amostragem](../profiling/call-tree-view-dotnet-memory-sampling-data.md)  
  
 [Modo de exibição de árvore de Chamadas](../profiling/call-tree-view-contention-data.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de relatório de desempenho](../profiling/performance-report-views.md)   
 [Noções básicas sobre valores de dados de instrumentação](../profiling/understanding-instrumentation-data-values.md)   
 [Noções básicas sobre valores de dados de amostragem](../profiling/understanding-sampling-data-values.md)



