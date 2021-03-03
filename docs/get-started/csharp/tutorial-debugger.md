---
title: 'Tutorial: depurar código C#'
description: Conheça os recursos do depurador do Visual Studio e como iniciar o depurador, percorrer o código e inspecionar dados em um aplicativo C#.
ms.custom: debug-experiment, seodec18, get-started
ms.date: 04/23/2020
ms.technology: vs-ide-debug
ms.topic: tutorial
dev_langs:
- CSharp
helpviewer_keywords:
- debugger
ms.assetid: 62734c0d-a75a-4576-8f73-0e97c19280e1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6eac51637b3f3b732f1293337080ef851f34c459
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101682750"
---
# <a name="tutorial-learn-to-debug-c-code-using-visual-studio"></a>Tutorial: aprenda a depurar código C# usando o Visual Studio

Este artigo apresenta os recursos do depurador do Visual Studio passo a passo. Caso deseje obter uma exibição de nível superior das funcionalidades do depurador, confira [Introdução ao depurador](../../debugger/debugger-feature-tour.md). Quando você *depura seu aplicativo*, isso normalmente significa executar o aplicativo com o depurador anexado. Quando você faz isso, o depurador fornece várias maneiras de mostrar o que o código está fazendo enquanto é executado. Você pode percorrer o código e examinar os valores armazenados em variáveis, definir inspeções em variáveis para ver quando os valores mudam, examinar o caminho de execução do código, ver se um branch de código está em execução e assim por diante. Se esta for sua primeira tentativa de depurar um código, leia [Como depurar para iniciantes absolutos](../../debugger/debugging-absolute-beginners.md) antes continuar neste artigo.

Embora o aplicativo de demonstração esteja em C#, a maioria dos recursos são aplicáveis a C++, Visual Basic, F#, Python, JavaScript e outras linguagens compatíveis com o Visual Studio (o F# não é compatível com editar e continuar). F# e JavaScript não dão suporte à janela **Autos**). As capturas de tela estão em C#.

Neste tutorial, você irá:

> [!div class="checklist"]
> * Iniciar o depurador e atingir os pontos de interrupção.
> * Aprender os comandos para percorrer o código no depurador
> * Inspecionar variáveis em dicas de dados e janelas do depurador
> * Examinar a pilha de chamadas

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range=">=vs-2019"

Você deve ter o Visual Studio 2019 instalado e a carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** .

::: moniker-end
::: moniker range="vs-2017"

Você deve ter o Visual Studio 2017 instalado e a carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** .

::: moniker-end

::: moniker range="vs-2017"

Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range="vs-2019"

Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

::: moniker-end

Se você precisar instalar a carga de trabalho, mas já tiver o Visual Studio, vá para **ferramentas**  >  **obter ferramentas e recursos...**, que abre o instalador do Visual Studio. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** e, em seguida, escolha **Modificar**.

## <a name="create-a-project"></a>Criar um projeto

Primeiro, você criará um projeto de aplicativo de console do .NET Core. O tipo de projeto inclui todos os arquivos de modelo que você precisará, mesmo sem adicionar nada!

::: moniker range="vs-2017"

1. Abra o Visual Studio 2017.

2. Na barra de menus superior, escolha **arquivo** > **novo** > **projeto**.

3. Na caixa de diálogo **Novo Projeto** no painel esquerdo, expanda **C#** e escolha **.NET Core**. No painel central, escolha **Aplicativo de Console (.NET Core)**. Em seguida, nomeie o projeto de introdução à *depuração*.

     Se você não vir o modelo de projeto do **Aplicativo de Console (.NET Core)**, escolha o link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto**.

     O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento multiplaforma do .NET Core** e, em seguida, selecione **Modificar**.

::: moniker-end

::: moniker range="vs-2019"

1. Abra o Visual Studio 2019.

   Se a janela iniciar não estiver aberta, escolha **arquivo** > **Iniciar janela**.

1. Na janela iniciar, escolha **criar um novo projeto**.

1. Na janela **Criar um novo projeto**, insira ou digite *console* na caixa de pesquisa. Em seguida, escolha **C#** na lista Linguagem de programação e, em seguida, escolha **Windows** na lista Plataforma. 

   Depois de aplicar os filtros de idioma e plataforma, escolha o modelo de **aplicativo de console** para .NET Core e, em seguida, escolha **Avançar**.

   ![Escolha o modelo C# para o aplicativo de console](../csharp/media/vs-2019/get-started-create-console-project.png)

   > [!NOTE]
   > Se você não vir o modelo de **aplicativo de console** , poderá instalá-lo na janela **criar um novo projeto** . Na mensagem **Não encontrou o que precisa?**, escolha o link **Instalar mais ferramentas e recursos**. Em seguida, no Instalador do Visual Studio, escolha a carga de trabalho de **desenvolvimento multiplataforma do .NET Core**.

1. Na janela **configurar seu novo projeto** , digite ou insira *GetStartedDebugging* na caixa **nome do projeto** . Em seguida, escolha **Avançar**.

1. Escolha a estrutura de destino recomendada (.NET Core 3,1) ou .NET 5 e, em seguida, escolha **criar**.

   O Visual Studio abre seu novo projeto.

::: moniker-end

## <a name="create-the-application"></a>Criar o aplicativo

1. No *Program.cs*, substitua todo o código padrão pelo código a seguir, em vez disso:

    ```csharp
    using System;
    class ArrayExample
    {
        static void Main()
        {
            char[] letters = { 'f', 'r', 'e', 'd', ' ', 's', 'm', 'i', 't', 'h'};
            string name = "";
            int[] a = new int[10];
            for (int i = 0; i < letters.Length; i++)
            {
                name += letters[i];
                a[i] = i + 1;
                SendMessage(name, a[i]);
            }
            Console.ReadKey();
        }
        static void SendMessage(string name, int msg)
        {
            Console.WriteLine("Hello, " + name + "! Count to " + msg);
        }
    }
    ```

## <a name="start-the-debugger"></a>Inicie o depurador.

1. Pressione **F5** (**debug > iniciar depuração**) ou o botão **Iniciar Depuração** ![Iniciar Depuração](../../debugger/media/dbg-tour-start-debugging.png "Iniciar Depuração") na barra de ferramentas Depurar.

     **F5** inicia o aplicativo com o depurador anexado ao processo do aplicativo, mas nós ainda não fizemos nada de especial para examinar o código. Portanto, o aplicativo apenas é carregado e a saída do console é exibida.

    ```cmd
    Hello, f! Count to 1
    Hello, fr! Count to 2
    Hello, fre! Count to 3
    Hello, fred! Count to 4
    Hello, fred ! Count to 5
    Hello, fred s! Count to 6
    Hello, fred sm! Count to 7
    Hello, fred smi! Count to 8
    Hello, fred smit! Count to 9
    Hello, fred smith! Count to 10
    ```

     Neste tutorial, vamos analisar melhor esse aplicativo usando o depurador e analisar os recursos do depurador.

2. Pare o depurador pressionando o botão vermelho parar ![parar depuração](../../debugger/media/dbg-tour-stop-debugging.png "Parar Depuração") (**Shift**  +  **F5**).

3. Na janela do console, pressione uma tecla para fechar a janela do console.

## <a name="set-a-breakpoint-and-start-the-debugger"></a>Definir um ponto de interrupção e iniciar o depurador

1. No loop `for` da função `Main`, defina um ponto de interrupção clicando na margem esquerda da seguinte linha de código:

    `name += letters[i];`

    Um ponto de ![interrupção](../../debugger/media/dbg-breakpoint.png "Ponto de interrupção") de círculo vermelho aparece onde você define o ponto de interrupção.

    Os pontos de interrupção são um dos recursos mais básicos e essenciais da depuração confiável. Um ponto de interrupção indica quando o Visual Studio deve suspender o código em execução para que você possa examinar os valores das variáveis ou o comportamento de memória ou se uma ramificação de código está sendo executada ou não.

2. Pressione **F5** ou o botão **Iniciar Depuração** ![inicie a depuração](../../debugger/media/dbg-tour-start-debugging.png "Iniciar Depuração"), o aplicativo é iniciado e o depurador é executado na linha de código em que você define o ponto de interrupção.

    ![Definir e atingir um ponto de interrupção](../csharp/media/get-started-set-breakpoint.gif)

    A seta amarela representa a instrução na qual o depurador ficou em pausa, que também suspende a execução do aplicativo no mesmo ponto (essa instrução ainda não foi executada).

     Se o aplicativo ainda não estiver em execução, **F5** iniciará o depurador e o interromperá no primeiro ponto de interrupção. Caso contrário, **F5** continuará executando o aplicativo até o próximo ponto de interrupção.

    Os pontos de interrupção são um recurso útil quando você sabe qual linha ou seção de código deseja examinar em detalhes. Para obter informações sobre os diferentes tipos de pontos de interrupção que você pode definir, como pontos de interrupção condicionais, consulte [usando pontos de interrupção](../../debugger/using-breakpoints.md).

## <a name="navigate-code-and-inspect-data-using-data-tips"></a>Navegar pelo código e inspecionar dados usando dicas de dados

Geralmente, usamos atalhos de teclado aqui porque essa é uma boa maneira de executar o aplicativo rapidamente no depurador (os comandos equivalentes, como os comandos de menu, são mostrados entre parênteses).

1. Enquanto estiver em pausa na `name += letters[i]` instrução, focalize a `letters` variável e você verá o valor padrão, o valor do primeiro elemento na matriz, `char[10]` .

     Os recursos que permitem que você inspecione variáveis são uns dos mais úteis do depurador e há diferentes maneiras de fazer isso. Muitas vezes, ao tentar depurar um problema, você tenta descobrir se as variáveis estão armazenando os valores que elas deveriam conter em um momento específico.

1. Expanda a `letters` variável para ver suas propriedades, que incluem todos os elementos que a variável contém.

     ![Captura de tela do depurador do Visual Studio com a instrução ' name + = Letters [I] ' realçada e uma lista suspensa que mostra os elementos na matriz de letras.](../csharp/media/get-started-view-data-tip.png)

1. Em seguida, passe o mouse sobre a `name` variável e você verá seu valor atual, uma cadeia de caracteres vazia.

1. Pressione **F10** (ou escolha **depurar > etapas**) duas vezes para avançar para a `SendMessage` chamada de método e, em seguida, pressione **F10** mais uma vez.

     F10 avança o depurador para a próxima instrução sem passar para funções ou métodos no seu código de aplicativo (o código ainda é executado). Ao pressionar F10 na `SendMessage` chamada do método, ignoramos o código de implementação para `SendMessage` (que talvez não estejamos interessados no momento).

1. Pressione **F10** (ou **depure**  >  as **etapas**) algumas vezes para iterar várias vezes pelo `for` loop, pausando novamente no ponto de interrupção e passando o mouse sobre a `name` variável a cada vez para verificar seu valor.

     ![Uma captura de tela animada do depurador do Visual Studio mostrando o efeito de pressionar F10 para "percorrer" e iterar por meio de um loop durante a depuração.](../csharp/media/get-started-data-tip.gif)

     O valor da variável é alterado com cada iteração do `for` loop, mostrando valores de `f` , então, `fr` `fre` e assim por diante. Para avançar o depurador por meio do loop mais rapidamente neste cenário, você pode pressionar **F5** (ou escolher **depurar**  >  **continuar**) em vez disso, o que o avança para o ponto de interrupção em vez da próxima instrução.

     Muitas vezes, durante a depuração, você deseja uma maneira rápida de verificar valores de propriedade em variáveis, para ver se eles estão armazenando os valores que você espera que armazenem. As dicas de dados são uma boa maneira de fazer isso.

1. Enquanto ainda estiver em pausa no `for` loop no `Main` método, pressione **F11** (ou escolha **depurar > etapa**) até que você pause na chamada do `SendMessage` método.

     Você deve estar nesta linha de código:

     `SendMessage(name, a[i]);`

1. Pressione **F11** mais uma vez para entrar no `SendMessage` método.

     O ponteiro amarelo avança para o `SendMessage` método.

     ![Use F11 para entrar no código](../csharp/media/get-started-f11.png "Passo F10")

     F11 é o comando **Intervir**, que avança a execução do aplicativo uma instrução por vez. F11 é uma boa maneira de examinar o fluxo de execução com o máximo de detalhes. Por padrão, o depurador ignora as partes do código que não são do usuário (se quiser saber mais detalhes, confira [Apenas Meu Código](../../debugger/just-my-code.md)).

     Digamos que você concluiu a análise do `SendMessage` método e deseja sair do método, mas permanecerá no depurador. Você pode fazer isso usando o comando **Depuração Circular**.

1. Pressione **Shift**  +  **F11** (ou **debug > Step Out**).

     Esse comando retoma a execução do aplicativo (e avança o depurador) até que o método ou a função atual retorne.

     Você deve estar de volta no `for` loop no `Main` método, em pausa na chamada do `SendMessage` método. Para obter mais informações sobre diferentes maneiras de se mover pelo seu código, consulte [navegar no código no depurador](../../debugger/navigating-through-code-with-the-debugger.md).

## <a name="navigate-code-using-run-to-click"></a>Navegar usando Executar até o Clique

1. Pressione **F5** para avançar para o ponto de interrupção novamente.

1. No editor de código, role para baixo e focalize o `Console.WriteLine` método no `SendMessage` método até que a **execução verde clique** no botão ![Executar para clicar](../../debugger/media/dbg-tour-run-to-click.png "RunToClick") em aparecer à esquerda. A dica de ferramenta para o botão mostra "Realizar a execução até aqui".

     ![Usar o recurso executar para clicar](../csharp/media/get-started-run-to-click.png "Executar com um Clique")

   > [!NOTE]
   > O botão **Executar até o Clique** é novo no [!include[vs_dev15](../../misc/includes/vs_dev15_md.md)]. (Se você não vir o botão de seta verde, use **F11** neste exemplo em vez de avançar o depurador para o lugar certo.)

2. Clique no botão **Executar para clicar** em ![Executar para clicar em](../../debugger/media/dbg-tour-run-to-click.png "RunToClick").

    O depurador avança para o `Console.WriteLine` método.

    O uso desse botão é semelhante à configuração de um ponto de interrupção temporário. **Executar até o Clique** é útil para abranger rapidamente uma região visível do código do aplicativo (você pode clicar em qualquer arquivo aberto).

## <a name="restart-your-app-quickly"></a>Reinicie o aplicativo rapidamente

Clique no botão **reiniciar** ![aplicativo de reinicialização](../../debugger/media/dbg-tour-restart.png "RestartApp") na barra de ferramentas depurar (**Ctrl**  +  **Shift**  +  **F5**).

Ao pressionar **Reiniciar**, você economiza tempo em comparação com a opção de parar o aplicativo e reiniciar o depurador. O depurador é pausado no primeiro ponto de interrupção que é atingido pela execução do código.

O depurador para novamente no ponto de interrupção que você definiu anteriormente dentro do `for` loop.

## <a name="inspect-variables-with-the-autos-and-locals-windows"></a>Inspecionar variáveis com as janelas Autos e Locais

1. Examine a janela **Autos** na parte inferior do editor de códigos.

    Se ele estiver fechado, abra-o enquanto estiver em pausa no depurador escolhendo **depurar**  >  **janelas**  >  **automáticas**.

    Na janela **Autos**, veja as variáveis e seus valores atuais. A janela **Autos** mostra todas as variáveis usadas na linha atual ou a linha anterior (verifique a documentação para saber o comportamento específico a uma linguagem).

1. Em seguida, examine a janela **Locais**, em uma guia ao lado da janela **Autos**.

1. Expanda a `letters` variável para mostrar os elementos que ela contém.

     ![Inspecionar variáveis na janela locais](../csharp/media/get-started-locals-window.png "Janela Locais")

    A janela **Locais** mostra as variáveis que estão no [escopo](https://www.wikipedia.org/wiki/Scope_(computer_science)) atual, ou seja, o contexto de execução atual.

## <a name="set-a-watch"></a>Definir uma inspeção

1. Na janela principal do editor de código, clique com o botão direito do mouse na `name` variável e escolha **Adicionar inspeção**.

    A janela **Inspeção** é aberta na parte inferior do editor de códigos. Você pode usar uma janela **Inspeção** para especificar uma variável (ou uma expressão) que deseja acompanhar.

    Agora, você tem um observador definido na `name` variável e pode ver seu valor alterado à medida que percorre o depurador. Ao contrário das outras janelas de variáveis, a janela **Inspeção** sempre mostra as variáveis que você está inspecionando (eles ficam esmaecidas quando estão fora do escopo).

## <a name="examine-the-call-stack"></a>Examinar a pilha de chamadas

1. Durante a pausa no loop `for`, clique na janela **Pilha de Chamadas** que fica aberta por padrão no painel inferior direito.

    Se ele estiver fechado, abra-o enquanto estiver em pausa no depurador escolhendo **depurar**  >    >  **pilha de chamadas** do Windows.

2. Clique em **F11** algumas vezes até ver a pausa do depurador no `SendMessage` método. Examine a janela **Pilha de Chamadas**.

    ![Examinar a pilha de chamadas](../csharp/media/get-started-call-stack.png "ExamineCallStack")

    A janela **Pilha de Chamadas** mostra a ordem em que os métodos e as funções são chamados. A linha superior mostra a função atual (o método `SendMessage` neste aplicativo). A segunda linha mostra que `SendMessage` foi chamado por meio do método `Main` e assim por diante.

   > [!NOTE]
   > A janela **Pilha de Chamadas** é semelhante à perspectiva de Depuração em alguns IDEs, como o Eclipse.

    A pilha de chamadas é uma boa maneira de examinar e entender o fluxo de execução de um aplicativo.

    Você pode clicar duas vezes em uma linha de código para examinar esse código-fonte. Isso também altera o escopo atual que está sendo inspecionado pelo depurador. Essa ação não avança o depurador.

    Você também pode usar os menus acessados ao clicar com o botão direito do mouse na janela **Pilha de Chamadas** para fazer outras coisas. Por exemplo, você pode inserir pontos de interrupção em funções especificadas, avançar o depurador usando **Executar até o Cursor** e examinar o código-fonte. Para obter mais informações, confira [Como examinar a pilha de chamadas](../../debugger/how-to-use-the-call-stack-window.md).

## <a name="change-the-execution-flow"></a>Alterar o fluxo de execução

1. Pressione **F11** duas vezes para executar o `Console.WriteLine` método.

1. Com o depurador pausado na `SendMessage` chamada do método, use o mouse para pegar a seta amarela (o ponteiro de execução) à esquerda e mova a seta amarela uma linha para cima, voltando para `Console.WriteLine` .

1. Pressione **F11**.

    O depurador executa novamente o método `Console.WriteLine` (você vê isso na saída da janela do console).

    Alterando o fluxo de execução, você pode fazer coisas como testar caminhos de execução de código diferentes ou executar novamente o código sem reiniciar o depurador.

    > [!WARNING]
    > Geralmente, você precisa ter cuidado com esse recurso. Um aviso é exibido na dica de ferramenta. Outros avisos também podem ser exibidos. Ao mover o ponteiro não é possível reverter o aplicativo para um estado anterior.

1. Pressione **F5** para continuar a execução do aplicativo.

    Parabéns por concluir este tutorial.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como iniciar o depurador, percorrer o código e inspecionar variáveis. Talvez você queira obter uma visão geral dos recursos do depurador, com links para mais informações.

> [!div class="nextstepaction"]
> [Introdução ao depurador](../../debugger/debugger-feature-tour.md)
