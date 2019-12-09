---
title: Janela Imediato | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ImmediateWindow
helpviewer_keywords:
- design-time expression evaluation
- Immediate window
- first-chance exception notifications
ms.assetid: d33e7937-73f3-4c69-9df0-777a8713c6f2
caps.latest.revision: 28
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3177c92713f6fdeb9b9b8a47a0da38608714174d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651281"
---
# <a name="immediate-window"></a>Janela imediata
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A janela **Imediato** é usada para depurar e avaliar expressões, executar instruções, imprimir valores de variáveis e assim por diante. Ela permite inserir expressões a serem avaliadas ou executadas pela linguagem de desenvolvimento durante a depuração. Para exibir a janela **Imediato**, abra um projeto para edição, escolha **Windows** no menu **Depurar** e selecione **Imediato**, ou pressione CTRL + ALT + I.

 É possível usar essa janela para emitir comandos [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] individuais. Os comandos disponíveis incluem `EvaluateStatement`, que pode ser usado para atribuir valores a variáveis. A janela **Imediato** também dá suporte ao IntelliSense.

## <a name="displaying-the-values-of-variables"></a>Exibindo os valores de variáveis
 Essa janela pode ser particularmente útil ao depurar um aplicativo. Por exemplo, para verificar o valor de uma variável `varA`, você pode usar o [Comando Imprimir](../../ide/reference/print-command.md):

```
>Debug.Print varA
```

 O ponto de interrogação (?) é um alias para `Debug.Print`, portanto, esse comando também pode ser escrito:

```
>? varA
```

 As duas versões desse comando retornarão o valor da variável `varA`.

> [!NOTE]
> Para emitir um comando [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] na janela **Imediato**, você deve preceder o comando com um sinal de maior que (>). Para inserir vários comandos, mude para a janela **Comando**.

## <a name="design-time-expression-evaluation"></a>Avaliação de expressões em tempo de design
 Você pode usar a janela **Imediato** para executar uma função ou sub-rotina em tempo de design.

#### <a name="to-execute-a-function-at-design-time"></a>Para executar uma função em tempo de design

1. Copie o código a seguir em um aplicativo de console do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]:

   ```
   Module Module1

       Sub Main()
           MyFunction(5)
       End Sub

       Function MyFunction(ByVal input as Integer) As Integer
           Return input * 2
       End Function

   End Module
   ```

2. No menu **Depurar**, clique em **Janelas** e clique em **Imediato**.

3. Digite `?MyFunction(2)` na janela **Imediato** e pressione Enter.

    A janela **Imediato** executará `MyFunction` e exibirá `4`.

   Se a função ou a sub-rotina contiver um ponto de interrupção, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] interromperá a execução no ponto apropriado. Então, você poderá usar o depurador do Windows para examinar o estado do programa. Para obter mais informações, consulte [Passo a passo: depuração em tempo de design](../../debugger/walkthrough-debugging-at-design-time.md).

   Não é possível usar a avaliação de expressão em tempo de design em tipos de projetos que exigem a inicialização de um ambiente de execução, incluindo projetos [!INCLUDE[trprVSTOshort](../../includes/trprvstoshort-md.md)], projetos Web, projetos de dispositivo inteligente e projetos SQL.

### <a name="design-time-expression-evaluation-in-multi-project-solutions"></a>Avaliação de expressão em tempo de design em soluções multiprojeto
 Ao estabelecer o contexto para a avaliação de expressão em tempo de design, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] faz referência ao projeto selecionado atualmente no Gerenciador de Soluções. Se nenhum projeto estiver selecionado no Gerenciador de Soluções, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] tenta avaliar a função com relação ao projeto de inicialização. Se a função não puder ser avaliada no contexto atual, você receberá uma mensagem de erro. Se você estiver tentando avaliar uma função em um projeto que não é o projeto de inicialização da solução e receber um erro, tente selecionar o projeto no Gerenciador de Soluções e tente avaliar novamente.

## <a name="entering-commands"></a>Inserindo comandos
 Você precisa inserir o sinal de maior que (>) ao emitir comandos [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] na janela **Imediato**. Use as teclas de SETA PARA CIMA e SETA PARA BAIXO para rolar os comandos emitidos anteriormente.

|Tarefa|Solução|Exemplo|
|----------|--------------|-------------|
|Avaliar uma expressão.|Preceda a expressão com um ponto de interrogação (?).|`? a+b`|
|Entrar temporariamente no modo Comando enquanto está no modo Imediato (para executar um único comando).|Digite o comando precedendo-o com um sinal de maior que (>).|`>alias`|
|Mude para a janela Comando.|Digite `cmd` na janela, precedendo-o com um sinal de maior que (>).|`>cmd`|
|Mude para a janela Imediato.|Digite `immed` na janela, sem o sinal de maior que (>).|`immed`|

## <a name="mark-mode"></a>Modo de Marca
 Quando clica em qualquer linha anterior na janela **Imediato**, você muda automaticamente para o modo de Marca. Isso permite selecionar, editar e copiar o texto de comandos anteriores como você faria em qualquer editor de texto e colá-lo na linha atual.

## <a name="the-equals--sign"></a>O sinal de igual (=)
 A janela usada para inserir o comando `EvaluateStatement` determina se um sinal de igual (=) é interpretado como um operador de comparação ou um operador de atribuição.

 Na janela **Imediato**, um sinal de igual (=) é interpretado como um operador de atribuição. Assim, por exemplo, o comando

```
>Debug.EvaluateStatement(varA=varB)
```

 atribuirá à variável `varA` o valor da variável `varB`.

 Na janela **Comando**, por outro lado, o sinal de igual (=) é interpretado como um operador de comparação. Você não pode usar operações de atribuição na janela **Comando**. Dessa forma, por exemplo, se os valores das variáveis `varA` e `varB` forem diferentes, o comando

```
>Debug.EvaluateStatement(varA=varB)
```

 retornará um valor de `False`.

## <a name="first-chance-exception-notifications"></a>Notificações de exceção de primeira tentativa
 Em algumas configurações, notificações de exceção de primeira tentativa são exibidas na janela **Imediato**.

#### <a name="to-toggle-first-chance-exception-notifications-in-the-immediate-window"></a>Para ativar ou desativar notificações de exceção de primeira tentativa na janela Imediato

1. No menu **Exibir**, clique em **Outras Janelas** e clique em **Saída**.

2. Clique com o botão direito do mouse na área de texto da Janela de **Saída** e marque ou desmarque **Mensagens de Exceção**.

## <a name="see-also"></a>Consulte também
 [Navegando pelo código com a](../../debugger/navigating-through-code-with-the-debugger.md) depuração da [janela de comando](../../ide/reference/command-window.md) do depurador [no Visual Studio](../../debugger/debugging-in-visual-studio.md) [conceitos básicos do depurador](../../debugger/debugger-basics.md) [: Depurando em tempo de design,](../../debugger/walkthrough-debugging-at-design-time.md) [aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md) [usando regular Expressões no Visual Studio](../../ide/using-regular-expressions-in-visual-studio.md)
