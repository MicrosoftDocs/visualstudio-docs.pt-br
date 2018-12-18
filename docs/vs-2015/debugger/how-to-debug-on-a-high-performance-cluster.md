---
title: 'Como: depurar em um Cluster de alto desempenho | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- cluster debugging
- high-perfomance debugging
ms.assetid: a2f0eb07-840e-4f95-a1b1-9509217e5b8f
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 75f2a96df18137f04b8b7637940c70378842e23d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51747728"
---
# <a name="how-to-debug-on-a-high-performance-cluster"></a>Como depurar em um cluster de alto desempenho
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A depuração de um programa com vários processamentos em um cluster de alto desempenho é semelhante à depuração de um programa comum em um computador remoto. No entanto, há algumas considerações adicionais. Para requisitos gerais de configuração remota, consulte [depuração remota](../debugger/remote-debugging.md).  
  
 Ao depurar em um cluster de alto desempenho, você pode usar todas as janelas e técnicas de depuração do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] que estiverem disponíveis para a depuração remota. Como você está depurando remotamente, no entanto, a janela do console externo não está disponível.  
  
 O **Threads** janela e **processos** janela são especialmente úteis para depurar aplicativos paralelos. Para obter dicas sobre como usar essas janelas, consulte [como: usar a janela de processos](http://msdn.microsoft.com/en-us/0207ce2f-8ceb-4fe7-b2b5-4dd35b035ed7) e [como: usar a janela Threads](../debugger/how-to-use-the-threads-window.md).  
  
 Os procedimentos a seguir mostram algumas técnicas que são muito úteis para depurar em um conjunto de alto desempenho.  
  
 Ao depurar um aplicativo paralelo, convém definir um ponto de interrupção em um segmento, processo, ou em um computador específico. Você pode fazer isso criando um ponto de interrupção normal, e depois adicionando um filtro de ponto de interrupção.  
  
### <a name="to-open-the-breakpoint-filter-dialog-box"></a>Para abrir a caixa de diálogo Filtro de Ponto de Interrupção  
  
1.  Um glifo de ponto de interrupção em uma janela de origem, com o botão direito do **desmontagem** janela, o **pilha de chamadas** janela, ou o **pontos de interrupção** janela.  
  
2.  No menu de atalho, clique em **filtro**. Essa opção pode aparecer na parte superior, nível ou no submenu em **pontos de interrupção**.  
  
### <a name="to-set-a-breakpoint-on-a-specific-computer"></a>Para definir um ponto de interrupção em um computador específico  
  
1.  Obter o nome do computador a **processos** janela.  
  
2.  Selecione um ponto de interrupção e abra o **filtro de ponto de interrupção** caixa de diálogo, conforme descrito no procedimento anterior.  
  
3.  No **filtro de ponto de interrupção** caixa de diálogo, digite:  
  
     MachineName =*nomeseucomputador*  
  
     Para criar um filtro mais complexo, você pode combinar cláusulas usando `&`, o operador AND, `||`, o operador OR, `!`, o operador NOT, e parênteses.  
  
4.  Clique em **OK**.  
  
### <a name="to-set-a-breakpoint-on-a-specific-process"></a>Para definir um ponto de interrupção em um processo específico  
  
1.  Obter o nome do processo ou o número de ID de processo do **processos** janela.  
  
2.  Selecione um ponto de interrupção e abra o **filtro de ponto de interrupção** caixa de diálogo, como no primeiro procedimento.  
  
3.  No **filtro de ponto de interrupção** caixa de diálogo, digite:  
  
     `ProcessName =`  *yourprocessname*  
  
     —ou—  
  
     `ProcessID =` *yourprocessIDnumber*  
  
     Para criar um filtro mais complexo, você pode combinar cláusulas usando `&`, o operador AND, `||`, o operador OR, `!`, o operador NOT, e parênteses.  
  
4.  Clique em **OK**.  
  
### <a name="to-set-a-breakpoint-on-a-specific-thread"></a>Para definir um ponto de interrupção em um segmento específico  
  
1.  Obter o nome do thread ou do número da ID do thread a **Threads** janela.  
  
2.  Selecione um ponto de interrupção e abra o **filtro de ponto de interrupção** caixa de diálogo, conforme descrito no primeiro procedimento.  
  
3.  No **filtro de ponto de interrupção** caixa de diálogo, digite:  
  
     `ThreadName =` *yourthreadname*  
  
     —ou—  
  
     `ThreadID =` *yourthreadIDnumber*  
  
     Para criar um filtro mais complexo, você pode combinar cláusulas usando `&`, o operador AND, `||`, o operador OR, `!`, o operador NOT, e parênteses.  
  
4.  Clique em **OK**.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como criar um filtro para um ponto de interrupção em um computador chamado `marvin` e um thread chamado `fourier1`.  
  
```  
(MachineName = marvin) & (ThreadName = fourier1)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos multithread](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [Depuração remota](../debugger/remote-debugging.md)   
 [Como: usar a janela processos](http://msdn.microsoft.com/en-us/0207ce2f-8ceb-4fe7-b2b5-4dd35b035ed7)   
 [Como: usar a janela Threads](../debugger/how-to-use-the-threads-window.md)   
 [Threads e processos](http://msdn.microsoft.com/en-us/73d87480-9af3-4d1b-baf5-397d5d876ae6)   
 [Usando pontos de interrupção](../debugger/using-breakpoints.md)



