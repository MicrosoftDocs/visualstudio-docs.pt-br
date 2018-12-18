---
title: 'Como: depurar em um Cluster de alto desempenho | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- cluster debugging
- high-perfomance debugging
ms.assetid: a2f0eb07-840e-4f95-a1b1-9509217e5b8f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9964621c216d058581d9298956ba90ac6cdbef86
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44280784"
---
# <a name="how-to-debug-on-a-high-performance-cluster"></a>Como depurar em um cluster de alto desempenho
A depuração de um programa com vários processamentos em um cluster de alto desempenho é semelhante à depuração de um programa comum em um computador remoto. No entanto, há algumas considerações adicionais. Para requisitos gerais de configuração remota, consulte [depuração remota](../debugger/remote-debugging.md).  
  
 Ao depurar em um cluster de alto desempenho, você pode usar todas as janelas e técnicas de depuração do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] que estiverem disponíveis para a depuração remota. Como você está depurando remotamente, no entanto, a janela do console externo não está disponível.  
  
 O **Threads** janela e **processos** janela são especialmente úteis para depurar aplicativos paralelos. Para obter dicas sobre como usar essas janelas, consulte [como: usar a janela de processos](/previous-versions/visualstudio/visual-studio-2010/7h8h5sdw(v=vs.100)) e [passo a passo: depurar usando a janela Threads](../debugger/how-to-use-the-threads-window.md).  
  
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
  
`(MachineName = marvin) & (ThreadName = fourier1)`  

  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos multithread](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [Depuração remota](../debugger/remote-debugging.md)   
 [Como: usar a janela processos](/previous-versions/visualstudio/visual-studio-2010/7h8h5sdw(v=vs.100))   
 [Introdução à depuração de aplicativos multithread](../debugger/get-started-debugging-multithreaded-apps.md)   
 [Threads e processos](/previous-versions/visualstudio/visual-studio-2010/ms164740(v=vs.100))   
 [Usando pontos de interrupção](../debugger/using-breakpoints.md)