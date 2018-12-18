---
title: Noções básicas sobre valores de dados de instrumentação| Microsoft Docs
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
- Profiling Tools,instrumentation
- instrumentation profiling method
ms.assetid: 2cf94cf9-c317-4a52-bf00-670f1262165e
caps.latest.revision: 34
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: aaa94700c22858be5b6a739034715d1bc926eaf9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51787933"
---
# <a name="understanding-instrumentation-data-values"></a>Noções básicas sobre valores de dados de instrumentação
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O método de criação de perfil de *instrumentação* dos [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] registra informações detalhadas de tempo para as chamadas de função, linhas e instruções no aplicativo de perfil  
  
 **Requisitos**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
  O método de instrumentação injeta código no início e no final das funções de destino no binário com perfil e antes e depois de cada chamada por essas funções para outras funções. O código injetado registra o seguinte:  
  
- O intervalo entre esse evento de coleta e a anterior.  
  
- Se o sistema operacional executou uma operação durante o intervalo. Por exemplo, o sistema operacional pode ler ou gravar em disco ou mudar entre o thread-alvo e outro thread em outro processo.  
  
  **Requisitos**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
  Para cada intervalo, a análise do criador de perfil reconstrói a pilha de chamadas que estava presente no final do intervalo. Uma pilha de chamadas é a lista de funções que estão ativas em um processador em um ponto no tempo. Apenas uma função (a função atual) está executando o código; as outras funções são a cadeia de chamadas de função que resultou na chamada para a função atual (a pilha de chamadas).  
  
  Para cada função na pilha de chamadas quando o intervalo foi gravado, a análise do criador de perfil adiciona o intervalo para um ou mais dos valores de dados de quatro para a função. A análise adiciona o intervalo como um valor de dados para uma função com base em dois critérios:  
  
- Se o intervalo ocorreu no código da função ou em um *função filho* (uma função que foi chamada pela função).  
  
- Se ocorreu um evento de sistema operacional no intervalo.  
  
  Os valores de dados para um intervalo de um intervalo de dados ou de uma função são nomeados *decorrido Inclusive*, *decorrido exclusivo*, *aplicativo Inclusive* e *aplicativo exclusivo*:  
  
- Todos os intervalos de uma função são adicionados ao valor dos dados inclusivos decorridos.  
  
- Se o intervalo ocorreu no código da função e não em uma função filho, o intervalo é adicionado ao valor dos dados exclusivos decorridos da função.  
  
- Se um evento de sistema operacional não ocorreu no intervalo, o intervalo é adicionado ao valor dos dados inclusivos do aplicativo.  
  
- Se um evento de sistema operacional não ocorreu no intervalo e o intervalo ocorreu na execução direta do código de função (ou seja, ele não tenha ocorrido em uma função filho), o intervalo é adicionado ao valor de dados exclusivos do aplicativo.  
  
  Os relatórios das Ferramentas de criação de perfil agregam os valores totais das funções na sessão de criação de perfil em si e os processos, threads e binários da sessão.  
  
## <a name="elapsed-inclusive-values"></a>Valores Inclusivos Decorridos  
 O tempo total gasto para executar uma função e suas funções filho.  
  
 Valores Inclusivos decorridos incluem os intervalos que foram gastos na execução diretamente o código de função e os intervalos que foram gastos na execução de funções filho da função de destino. Intervalos de função ou suas funções filho, que incluem aguardar o sistema operacional, também estão inclusas nos valores inclusivos decorridos.  
  
## <a name="elapsed-exclusive-values"></a>Valores Exclusivos Decorridos  
 O tempo gasto para executar uma função, excluindo o tempo gasto em funções filho.  
  
 Valores exclusivos decorridos incluem os intervalos que foram gastos na execução direta do código de função, independentemente se um evento de sistema operacional ocorreu no intervalo. Todos os intervalos gastos em funções filho, que foram chamadas pela função de destino, não estão incluídos nos valores exclusivos decorridos.  
  
## <a name="application-inclusive-values"></a>Valores Inclusivos do Aplicativo  
 O tempo gasto para executar uma função e suas funções filho, exceto o tempo gasto em eventos do sistema operacional.  
  
 Valores Inclusivos de Aplicativo não incluem os intervalos que contêm eventos de sistema operacional. Valores inclusivos do aplicativo incluem todos os outros intervalos que foram gastos na execução de uma função, independentemente se o intervalo foi gasto para executar diretamente o código de função ou foi gasto em funções filho da função de destino.  
  
## <a name="application-exclusive-values"></a>Valores Exclusivos do Aplicativo  
 O tempo gasto para executar uma função, excluindo o tempo gasto em funções filho e o tempo gasto em eventos do sistema operacional.  
  
 Valores exclusivos do aplicativo não incluem os intervalos que contêm eventos de sistema operacional ou intervalos que foram gastos na execução de funções que foram chamadas pela função. Valores exclusivos do aplicativo incluem somente os intervalos que foram gastos diretamente na execução do código de função e que não continham um evento do sistema operacional.  
  
## <a name="elapsed-inclusive-percent"></a>Porcentagem Inclusiva Decorrido  
 O percentual dos valores Inclusivos totais decorridos da sessão de criação de perfil que eram valores inclusivos decorridos de função, módulo, thread ou processo.  
  
 100 * função Inclusiva decorrida / sessão Inclusiva decorrida  
  
## <a name="elapsed-exclusive-percent"></a>Porcentagem exclusiva decorrida  
 O percentual dos valores Inclusivos totais decorridos da sessão de criação de perfil que eram valores exclusivos decorridos de função, módulo, thread ou processo.  
  
 100 * função exclusiva decorrida / sessão inclusiva decorrida  
  
## <a name="application-inclusive-percent"></a>Porcentagem inclusiva do aplicativo  
 O percentual dos valores Inclusivos totais do aplicativo da sessão de criação de perfil que eram valores inclusivos do aplicativo de função, módulo, thread ou processo.  
  
 100 * Função inclusiva do aplicativo / Sessão inclusiva do aplicativo  
  
## <a name="application-exclusive-percent"></a>Porcentagem exclusiva do aplicativo  
 O percentual dos valores Inclusivos totais do aplicativo da sessão de criação de perfil que eram intervalos exclusivos do aplicativo de função, módulo, thread ou processo.  
  
 100 * Função exclusiva do aplicativo / Sessão inclusiva do aplicativo  
  
## <a name="see-also"></a>Consulte também  
 [Analisando dados de ferramentas de desempenho](../profiling/analyzing-performance-tools-data.md)   
 [Como escolher métodos de coleta](../profiling/how-to-choose-collection-methods.md)



