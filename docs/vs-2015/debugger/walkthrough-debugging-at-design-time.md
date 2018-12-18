---
title: 'Passo a passo: Depuração em tempo de Design | Microsoft Docs'
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
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], design-time
- breakpoints, design-time debugging
- Immediate window, design-time debugging
- design-time debugging
ms.assetid: 35bfdd2c-6f60-4be1-ba9d-55fce70ee4d8
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4b6660bc4d9cf0073f1e18b0960c3fa9c0ae9c13
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51737778"
---
# <a name="walkthrough-debugging-at-design-time"></a>Instruções passo a passo: depurando na hora de design
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar o Visual Studio **imediato** janela para executar uma função ou sub-rotina enquanto seu aplicativo não está em execução. Se a função ou a sub-rotina contiverem um ponto de interrupção, o Visual Studio interromperá a execução no ponto apropriado. Então, você poderá usar o depurador do Windows para examinar o estado do programa. Esse recurso é chamado de depuração em tempo de design.  
  
 O procedimento a seguir exibe como usar esse recurso.  
  
### <a name="to-hit-breakpoints-from-the-immediate-window"></a>Para usar pontos de interrupção da janela Imediato  
  
1.  Cole o seguinte código no aplicativo de console do Visual Basic:  
  
    ```  
    Module Module1  
  
        Sub Main()  
            MySub()  
        End Sub  
  
        Function MyFunction() As Decimal  
            Static i As Integer  
            i = i + 1  
            Dim s As String  
  
            s = "Add Breakpoint here"  
            Return 4  
        End Function  
  
        Sub MySub()  
            MyFunction()  
        End Sub  
    End Module  
    ```  
  
2.  Defina um ponto de interrupção na linha em que se lê `s="Add BreakPoint Here"`.  
  
3.  Digite o seguinte na **imediato** janela: `?MyFunction<enter>`  
  
4.  Certifique-se de que o ponto de interrupção foi alcançado, e que a pilha de chamadas está correta.  
  
5.  Sobre o **Debug** menu, clique em **continuar**e verificar se você estiver no modo de design.  
  
6.  Digite o seguinte na **imediato** janela: `?MyFunction<enter>`  
  
7.  Digite o seguinte na **imediato** janela: `?MySub<enter>`  
  
8.  Verifique se o ponto de interrupção e examinar o valor da variável estática `i` no **Locals** janela. Deve ter o valor 3.  
  
9. Verifique se a pilha de chamadas está correta.  
  
10. Sobre o **Debug** menu, clique em **continuar**e verificar se você estiver no modo de design.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Noções básicas do depurador](../debugger/debugger-basics.md)



