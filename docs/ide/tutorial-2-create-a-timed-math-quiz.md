---
title: 'Tutorial 2: Criar um teste de matemática temporizado'
description: Saiba como criar um teste no qual o Secretário de teste deve responder a quatro problemas aritméticos aleatórios em um determinado tempo.
ms.custom: SEO-VS-2020
ms.date: 10/16/2019
ms.assetid: d7165d08-ace3-457d-b57d-fb8f80760a6f
ms.topic: tutorial
ms.technology: vs-ide-general
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6529146f279eddfe010af60df864fe64f5550fb1
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296736"
---
# <a name="tutorial-2-create-a-timed-math-quiz"></a>Tutorial 2: Criar um teste de matemática temporizado

Neste tutorial, você cria um teste no qual o tomador de teste deve responder a quatro problemas aritméticos aleatórios dentro de um tempo especificado.

> [!NOTE]
> Este tutorial aborda tanto o C# quanto o Visual Basic, portanto, concentre-se nas informações específicas para a linguagem de programação que você está usando.

Este tutorial orienta você pelas seguintes tarefas:

- Gere números aleatórios usando a classe de <xref:System.Random>.

- Disparar eventos para que ocorram em um horário específico usando um controle de <xref:System.Windows.Forms.Timer>.

- Fluxo do programa de controle usando instruções de `if else`.

- Execute operações aritméticas básicas no código.

Quando você terminar, seu teste será semelhante à captura de tela a seguir, exceto com números diferentes:

![Teste de matemática com quatro problemas](../ide/media/express_finishedquiz.png)

## <a name="tutorial-links"></a>Links do tutorial

|Título|Descrição|
|-----------|-----------------|
|[Etapa 1: Criar um projeto e adicionar rótulos ao formulário](../ide/step-1-create-a-project-and-add-labels-to-your-form.md)|Comece criando o projeto, alterando propriedades e adicionando controles `Label`.|
|[Etapa 2: Criar um problema de adição aleatório](../ide/step-2-create-a-random-addition-problem.md)|Crie um problema de adição, e use a classe de `Random` para gerar números aleatórios.|
|[Etapa 3: Adicionar um temporizador de contagem regressiva](../ide/step-3-add-a-countdown-timer.md)|Adicione um timer de contagem regressiva de modo que o teste possa ser cronometrado.|
|[Etapa 4: Adicionar o método CheckTheAnswer()](../ide/step-4-add-the-checktheanswer-parens-method.md)|Adicione um método para verificar se o comprador de teste inseriu uma resposta correta para o problema.|
|[Etapa 5: Adicionar manipuladores de eventos de inserção aos controles NumericUpDown](../ide/step-5-add-enter-event-handlers-for-the-numericupdown-controls.md)|Adicione manipuladores de eventos que facilitam a tomada do teste.|
|[Etapa 6: Adicionar um problema de subtração](../ide/step-6-add-a-subtraction-problem.md)|Adicione um problema de subtração que gerencia números aleatórios, usa o timer, e o verifica se as respostas estão corretas.|
|[Etapa 7: Adicionar problemas de multiplicação e divisão](../ide/step-7-add-multiplication-and-division-problems.md)|Adicione problemas de divisão e multiplicação que geram números aleatórios, usam o timer, e verificam se as respostas estão corretas.|
|[Etapa 8: Personalizar o teste](../ide/step-8-customize-the-quiz.md)|Tente outros recursos, como alterar cores e adicionar uma dica.|

Também há excelentes recursos de aprendizado de vídeo gratuitos disponíveis para você. Para saber mais sobre programação em C#, consulte [conceitos básicos do c#: desenvolvimento para iniciantes absolutos](https://channel9.msdn.com/Series/C-Sharp-Fundamentals-Development-for-Absolute-Beginners). Para saber mais sobre programação no Visual Basic, veja [Visual Basic Fundamentals: Development for Absolute Beginners (Conceitos básicos do Visual Basic: desenvolvimento para iniciantes absolutos)](https://channel9.msdn.com/Series/Visual-Basic-Development-for-Absolute-Beginners).

## <a name="next-steps"></a>Próximas etapas

Para iniciar o tutorial, comece com a **[etapa 1: criar um projeto e adicionar rótulos ao formulário](../ide/step-1-create-a-project-and-add-labels-to-your-form.md)**.

## <a name="see-also"></a>Confira também

* [Mais tutoriais sobre C#](../get-started/csharp/index.yml)
* [Tutoriais de Visual Basic](../get-started/visual-basic/index.yml)
* [Tutoriais do C++](/cpp/get-started/tutorial-console-cpp)