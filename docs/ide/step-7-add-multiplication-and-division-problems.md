---
title: 'Etapa 7: Adicionar problemas de multiplicação e divisão'
description: Saiba como adicionar problemas de multiplicação e divisão.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: e638959e-f6a4-4eb4-b2e9-f63b7855cf8f
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8027b248fd675a112d64c9889686b9ef9a9c8514
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106214181"
---
# <a name="step-7-add-multiplication-and-division-problems"></a>Etapa 7: Adicionar problemas de multiplicação e divisão

Na sétima parte deste tutorial, você adicionará problemas de multiplicação e de divisão, mas primeiro pense em como fazer essa alteração. Considere a etapa inicial, que envolve armazenar valores.

> [!NOTE]
> Esse tópico faz parte de uma série de tutoriais sobre conceitos de codificação básica. Para obter uma visão geral do tutorial, consulte [tutorial 2: criar um teste de matemática cronometrado](../ide/tutorial-2-create-a-timed-math-quiz.md).

## <a name="to-add-multiplication-and-division-problems"></a>Para adicionar problemas de multiplicação e de divisão

1. Adicione mais quatro variáveis inteiras ao formulário.

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb" id="Snippet15":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs" id="Snippet15":::

     [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

2. Como você fez antes, modifique o método de `StartTheQuiz()` para preencher números aleatórios para os problemas de multiplicação e de divisão.

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb" id="Snippet16":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs" id="Snippet16":::

3. Modifique o método de `CheckTheAnswer()` de modo que ele também verifique os problemas de multiplicação e de divisão.

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb" id="Snippet17":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs" id="Snippet17":::

     Você não pode inserir facilmente o sinal de multiplicação (×) e o sinal de divisão (÷) usando o teclado, portanto, o C# e Visual Basic aceitam um asterisco (*) para multiplicação e uma barra (/) para divisão.

4. Altere a parte a mais recente do manipulador de eventos de escala <xref:System.Windows.Forms.Timer.Tick> do timer de modo que preencha a resposta correta quando o tempo de execução se esgotar.

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb" id="Snippet23":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs" id="Snippet23":::

5. Salve e execute seu programa.

     Os participantes de teste devem responder quatro problemas para concluir o teste, conforme mostrado na ilustração.

     ![Teste de matemática com quatro problemas](../ide/media/express_finishedquiz.png)<br/>
***Teste de matemática** _ _with quatro problemas *

## <a name="to-continue-or-review"></a>Para continuar ou revisar

- Para ir para a próxima etapa do tutorial, consulte **[Step 8: Customize The Quiz](../ide/step-8-customize-the-quiz.md)**.

- Para retornar à etapa anterior do tutorial, veja [Etapa 6: Adicionar um problema de subtração](../ide/step-6-add-a-subtraction-problem.md).
