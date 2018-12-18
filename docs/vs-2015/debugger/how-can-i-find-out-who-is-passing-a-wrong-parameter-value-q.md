---
title: Como posso descobrir quem está passando um valor de parâmetro incorreto? | Microsoft Docs
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
- vs.debug.parameters
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- debugging [C++], parameters
- parameters [debugger]
- passing parameters, troubleshooting wrong values
- functions [debugger], detecting wrong parameter values
- parameter values, troubleshooting
ms.assetid: 1f1ae455-0e25-4e9d-b33f-53908f5bd6ce
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2505d8f733554e90c14a46deafd0936682d38d66
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51729571"
---
# <a name="how-can-i-find-out-who-is-passing-a-wrong-parameter-value"></a>Como posso descobrir quem está passando um valor de parâmetro incorreto?
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Descrição do problema  
 O valor de parâmetro errado está sendo passado a uma de minhas funções. Essa função é chamada de todos os pontos Como posso descobrir o que está passando o valor errado?  
  
## <a name="solution"></a>Solução  
  
#### <a name="to-resolve-this-problem"></a>Para resolver esse problema  
  
1.  Defina um local de ponto de interrupção no início da função.  
  
2.  O ponto de interrupção com o botão direito e selecione **condição**.  
  
3.  No **condição de ponto de interrupção** caixa de diálogo, clique no **condição** caixa de seleção. Ver [avançadas de pontos de interrupção](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression).  
  
4.  Digite uma expressão, como `Var==3`, na caixa de texto, onde `Var` é o nome do parâmetro que contém o valor incorreto, e `3` é o valor incorreto passado para ele.  
  
5.  Selecione o **é True** botão de opção e, em seguida, clique no **Okey** botão.  
  
6.  Agora, execute o programa novamente. O ponto de interrupção faz com que o programa pare no início da função quando o parâmetro `Var` tiver o valor `3`.  
  
7.  Use a janela Pilha de Chamadas para localizar a função de chamada e navegar até seu código-fonte. Para obter mais informações, consulte [como: usar a janela pilha de chamadas](../debugger/how-to-use-the-call-stack-window.md).  
  
## <a name="see-also"></a>Consulte também  
 [Perguntas frequentes do código nativo de depuração](../debugger/debugging-native-code-faqs.md)   
 [Pontos de interrupção](http://msdn.microsoft.com/en-us/fe4eedc1-71aa-4928-962f-0912c334d583)   
 [Depurando código nativo](../debugger/debugging-native-code.md)



