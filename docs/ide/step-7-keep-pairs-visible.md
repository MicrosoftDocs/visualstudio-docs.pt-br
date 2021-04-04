---
title: 'Etapa 7: Manter os pares visíveis'
description: Saiba como adicionar uma instrução If para que, quando o Player selecionar um par correspondente de ícones, os ícones fiquem visíveis.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 42e1d08c-7b2e-4efd-9f47-85d6206afe35
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 341d0e54af991390a3ff5146a29d9e66ad7c737e
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106214142"
---
# <a name="step-7-keep-pairs-visible"></a>Etapa 7: Manter os pares visíveis
O jogo funciona bem, desde que o jogador escolha apenas pares de ícones que não correspondam. Porém, considere o que deve acontecer quando o jogador escolher um par correspondente. Em vez de fazer os ícones desaparecerem ativando o temporizador (usando o método <xref:System.Windows.Forms.Timer.Start>), o jogo deve redefinir a si próprio para que ele não acompanhe mais nenhum rótulo usando as variáveis de referência `firstClicked` e `secondClicked`, sem redefinir as cores dos dois rótulos que foram escolhidos.

## <a name="to-keep-pairs-visible"></a>Para manter os pares visíveis

1. Adicione a instrução `if` a seguir ao método do manipulador de eventos `label_Click()`, próximo do fim do código, logo acima da instrução onde você inicia o temporizador. Observe mais detalhadamente o código enquanto o adiciona ao programa. Leve em consideração como o código funciona.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step7/cs/form1.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step7/vb/form1.vb" id="Snippet9":::

     > [!IMPORTANT]
     > Use o controle linguagem de programação no canto superior direito desta página para exibir o trecho de código C# ou o trecho de código de Visual Basic.<br><br>![Controle de linguagem de programação para Docs.Microsoft.com](../ide/media/docs-programming-language-control.png)

     A primeira linha da instrução `if` que você acabou de adicionar verifica se o ícone no primeiro rótulo que o jogador escolhe é igual ao ícone no segundo rótulo. Se os ícones forem idênticos, o programa executará as três instruções entre as chaves no C# ou as três instruções na instrução `if` do Visual Basic. As primeiras duas instruções redefinem as variáveis de referência `firstClicked` e `secondClicked` para que elas não acompanhem mais nenhum dos rótulos. (Você pode reconhecer essas duas instruções do manipulador de eventos do temporizador <xref:System.Windows.Forms.Timer.Tick> .) A terceira instrução é uma `return` instrução, que diz ao programa para ignorar o restante das instruções no método sem executá-las.

     Se estiver programando em C#, talvez você tenha notado que parte do código usa um único sinal de igual ( `=` ), enquanto outras instruções usam dois sinais de igual ( `==` ). Leve em consideração por que `=` é usado em alguns locais, mas `==` é usado em outros.

     Esse é um bom exemplo que mostra a diferença. Observe atentamente o código entre os parênteses na instrução `if`.

    ```vb
    firstClicked.Text = secondClicked.Text
    ```

    ```csharp
    firstClicked.Text == secondClicked.Text
    ```

     Em seguida, observe atentamente a primeira instrução no bloco de código após a instrução `if`.

    ```vb
    firstClicked = Nothing
    ```

    ```csharp
    firstClicked = null;
    ```

     A primeira dessas duas instruções verifica se dois ícones são iguais. Como dois valores estão sendo comparados, o programa C# usa o `==` operador de igualdade. A segunda instrução realmente altera o valor (chamado *atribuição*), definindo a variável de referência `firstClicked` igual a `null` para redefini-la. Por esse motivo, ela usa o operador de atribuição `=` no lugar. O C# usa `=` para definir valores e `==` compará-los. O Visual Basic usa `=` para atribuição de variável e comparação.

2. Salve e execute o programa e, em seguida, comece a escolher os ícones no formulário. Se você escolher um par que não corresponda, o evento Tick do temporizador é disparado e ambos os ícones desaparecem. Se você escolher um par correspondente, a nova `if` instrução será executada e a instrução de retorno fará com que o método ignore o código que inicia o temporizador, para que os ícones fiquem visíveis, conforme mostrado na imagem a seguir.

     ![Jogo criado neste tutorial](../ide/media/express_finishedgame.png)<br/>
***Jogo de correspondência** _ _with pares de ícones visíveis *

## <a name="to-continue-or-review"></a>Para continuar ou revisar

- Para ir para a próxima etapa do tutorial, consulte **[etapa 8: adicionar um método para verificar se o jogador venceu](../ide/step-8-add-a-method-to-verify-whether-the-player-won.md)**.

- Para retornar à etapa anterior do tutorial, consulte [etapa 6: adicionar um temporizador](../ide/step-6-add-a-timer.md).
