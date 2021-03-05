---
title: Descubra quem está passando um valor de parâmetro errado | Microsoft Docs
description: Você pode descobrir qual código está chamando sua função e passando um valor de parâmetro incorreto. Saiba como usar um ponto de interrupção condicional para fazer isso.
ms.custom: SEO-VS-2020, seodec18
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.parameters
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], parameters
- parameters [debugger]
- passing parameters, troubleshooting wrong values
- functions [debugger], detecting wrong parameter values
- parameter values, troubleshooting
ms.assetid: 1f1ae455-0e25-4e9d-b33f-53908f5bd6ce
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cb4b3c41b46817d15a13626983ccf55ffa9acc5f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102155174"
---
# <a name="how-can-i-find-out-who-is-passing-a-wrong-parameter-value"></a>Como posso descobrir quem está passando um valor de parâmetro incorreto?
## <a name="problem-description"></a>Descrição do problema
 O valor de parâmetro errado está sendo passado a uma de minhas funções. Essa função é chamada de todos os pontos Como posso descobrir o que está passando o valor errado?

## <a name="solution"></a>Solução

#### <a name="to-resolve-this-problem"></a>Para resolver esse problema

1. Defina um local de ponto de interrupção no início da função.

2. Clique com o botão direito do mouse no ponto de interrupção e selecione **Condição**.

3. Na caixa de diálogo **Condição de Ponto de Interrupção**, clique na caixa de seleção **Condição**. Consulte [pontos de interrupção avançados](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression).

4. Digite uma expressão, como `Var==3`, na caixa de texto, onde `Var` é o nome do parâmetro que contém o valor incorreto, e `3` é o valor incorreto passado para ele.

5. Selecione o botão de opção **é True** e clique no botão **OK**.

6. Agora, execute o programa novamente. O ponto de interrupção faz com que o programa pare no início da função quando o parâmetro `Var` tiver o valor `3`.

7. Use a janela Pilha de Chamadas para localizar a função de chamada e navegar até seu código-fonte. Para obter mais informações, consulte [como: usar a janela pilha de chamadas](../debugger/how-to-use-the-call-stack-window.md).

## <a name="see-also"></a>Confira também
- [Perguntas frequentes sobre depuração de código nativo](../debugger/debugging-native-code-faqs.md)
- [Pontos de Interrupção](/previous-versions/ktf38f66(v=vs.100))
- [Depurando código nativo](../debugger/debugging-native-code.md)
