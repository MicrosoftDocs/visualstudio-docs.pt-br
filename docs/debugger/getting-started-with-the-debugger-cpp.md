---
title: 'Tutorial: depurar código C++'
description: Conheça os recursos do depurador do Visual Studio e como iniciar o depurador, percorrer o código e inspecionar dados em um aplicativo C++.
ms.custom: debug-experiment, seodec18, get-started
ms.date: 02/04/2020
ms.technology: vs-ide-debug
ms.topic: tutorial
dev_langs:
- C++
helpviewer_keywords:
- debugger
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cd02bbd2264720a5443807fb431b4dafa2a0a578
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306430"
---
# <a name="tutorial-learn-to-debug-c-code-using-visual-studio"></a>Tutorial: aprenda a depurar código C++ usando o Visual Studio

Este artigo apresenta os recursos do depurador do Visual Studio passo a passo. Caso deseje obter uma exibição de nível superior das funcionalidades do depurador, confira [Introdução ao depurador](../debugger/debugger-feature-tour.md). Quando você *depura seu aplicativo*, isso normalmente significa executar o aplicativo com o depurador anexado. Quando você faz isso, o depurador fornece várias maneiras de mostrar o que o código está fazendo enquanto é executado. Você pode percorrer o código e examinar os valores armazenados em variáveis, definir inspeções em variáveis para ver quando os valores mudam, examinar o caminho de execução do código, ver se um branch de código está em execução e assim por diante. Se esta for sua primeira tentativa de depurar um código, leia [Como depurar para iniciantes absolutos](../debugger/debugging-absolute-beginners.md) antes continuar neste artigo.

Embora o aplicativo de demonstração seja C++, a maioria dos recursos é aplicável a C#, Visual Basic, F #, Python, JavaScript e outras linguagens compatíveis com o Visual Studio (o F # não dá suporte a editar e continuar. F# e JavaScript não dão suporte à janela **Autos**). As capturas de tela estão em C++.

Neste tutorial, você irá:

> [!div class="checklist"]
> * Iniciar o depurador e atingir os pontos de interrupção.
> * Aprender os comandos para percorrer o código no depurador
> * Inspecionar variáveis em dicas de dados e janelas do depurador
> * Examinar a pilha de chamadas

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range=">=vs-2019"

É necessário ter o Visual Studio 2019 instalado e a carga de trabalho **Desenvolvimento para desktop com C++**.

::: moniker-end
::: moniker range="vs-2017"

Você precisa ter o Visual Studio 2017 instalado e a carga de trabalho de **Desenvolvimento para desktop com C++**.

::: moniker-end

::: moniker range="vs-2017"

Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range=">=vs-2019"

Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range="vs-2022"

Se você ainda não instalou o Visual Studio 2022 Preview, vá para a página de [downloads do visual studio 2022 Preview](https://visualstudio.microsoft.com/vs/preview/vs2022) para instalá-lo gratuitamente.

::: moniker-end

Se você precisar instalar a carga de trabalho, mas já tiver o Visual Studio, vá para **ferramentas**  >  **obter ferramentas e recursos...**, que abre o instalador do Visual Studio. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento para desktop com C++** e, em seguida, selecione **Modificar**.

## <a name="create-a-project"></a>Criar um projeto

Primeiro, você criará um projeto de aplicativo de console do C++. O tipo de projeto inclui todos os arquivos de modelo que você precisará, mesmo sem adicionar nada!

::: moniker range="vs-2017"

1. Abra o Visual Studio 2017.

2. Na barra de menus superior, escolha **arquivo** > **novo** > **projeto**.

3. Na caixa de diálogo **novo projeto** no painel esquerdo, expanda **Visual C++** e, em seguida, escolha **área de trabalho do Windows**. No painel central, escolha **aplicativo de console do Windows**. Em seguida, nomeie o projeto de introdução à *depuração*.

     Se você não vir o modelo de projeto de **aplicativo de console** , escolha o link **abrir instalador do Visual Studio** no painel esquerdo da caixa de diálogo **novo projeto** . O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento multiplaforma do .NET Core** e, em seguida, selecione **Modificar**.

4. Clique em **OK**.

   O Visual Studio abre seu novo projeto.

::: moniker-end

::: moniker range=">=vs-2019"

1. Abra o Visual Studio 2019.

   Se a janela iniciar não estiver aberta, escolha **arquivo** > **Iniciar janela**.

1. Na janela iniciar, escolha **criar um novo projeto**.

1. Na janela **Criar um novo projeto**, insira ou digite *console* na caixa de pesquisa. Em seguida, escolha **C++** na lista idioma e, em seguida, escolha **Windows** na lista plataforma. 

   Depois de aplicar os filtros de idioma e plataforma, escolha o modelo de **aplicativo de console** e escolha **Avançar**.

   ![Escolha o modelo C++ para o aplicativo de console](../debugger/media/vs-2019/get-started-create-console-project-cpp.png)

   > [!NOTE]
   > Se você não vir o modelo de **aplicativo de console** , poderá instalá-lo na janela **criar um novo projeto** . Na mensagem **Não encontrou o que precisa?**, escolha o link **Instalar mais ferramentas e recursos**. Em seguida, na Instalador do Visual Studio, escolha o **desenvolvimento de desktop com** carga de trabalho do C++.

1. Na janela **configurar seu novo projeto** , digite ou digite *Get-Started-Debugging* na caixa **nome do projeto** . Em seguida, escolha **criar**.

   O Visual Studio abre seu novo projeto.

::: moniker-end

## <a name="create-the-application"></a>Criar o aplicativo

1. Em *Get-Started-Debugging. cpp*, substitua todo o código padrão pelo código a seguir, em vez disso:

    ```cpp
    #include <string>
    #include <vector>
    #include <iostream>

    void SendMessage(const std::wstring& name, int msg)
    {
        std::wcout << L"Hello, " << name << L"! Count to " << msg << std::endl;
    }

    int main()
    {
        std::vector<wchar_t> letters = { L'f', L'r', L'e', L'd', L' ', L's', L'm', L'i', L't', L'h' };
        std::wstring name = L"";
        std::vector<int> a(10);
        std::wstring key = L"";

        for (int i = 0; i < letters.size(); i++)
        {
            name += letters[i];
            a[i] = i + 1;
            SendMessage(name, a[i]);
        }
        std::wcin >> key;
        return 0;
    }
    ```

## <a name="start-the-debugger"></a>Inicie o depurador.

1. Pressione **F5** (**debug > iniciar depuração**) ou o botão **Iniciar Depuração** ![Iniciar Depuração](../debugger/media/dbg-tour-start-debugging.png "Iniciar Depuração") na barra de ferramentas Depurar.

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

2. Pare o depurador pressionando o botão vermelho parar ![parar depuração](../debugger/media/dbg-tour-stop-debugging.png "Parar Depuração") (**Shift**  +  **F5**).

3. Na janela do console, pressione uma tecla e **insira** para fechar a janela do console.

## <a name="set-a-breakpoint-and-start-the-debugger"></a>Definir um ponto de interrupção e iniciar o depurador

1. No loop `for` da função `main`, defina um ponto de interrupção clicando na margem esquerda da seguinte linha de código:

    `name += letters[i];`

    Um ponto de ![interrupção](../debugger/media/dbg-breakpoint.png "Ponto de interrupção") de círculo vermelho aparece onde você define o ponto de interrupção.

    Os pontos de interrupção são um dos recursos mais básicos e essenciais da depuração confiável. Um ponto de interrupção indica quando o Visual Studio deve suspender o código em execução para que você possa examinar os valores das variáveis ou o comportamento de memória ou se uma ramificação de código está sendo executada ou não.

2. Pressione **F5** ou o botão **Iniciar Depuração** ![inicie a depuração](../debugger/media/dbg-tour-start-debugging.png "Iniciar Depuração"), o aplicativo é iniciado e o depurador é executado na linha de código em que você define o ponto de interrupção.

    ![Definir e atingir um ponto de interrupção](../debugger/media/get-started-set-breakpoint-cpp.png)

    A seta amarela representa a instrução na qual o depurador ficou em pausa, que também suspende a execução do aplicativo no mesmo ponto (essa instrução ainda não foi executada).

     Se o aplicativo ainda não estiver em execução, **F5** iniciará o depurador e o interromperá no primeiro ponto de interrupção. Caso contrário, **F5** continuará executando o aplicativo até o próximo ponto de interrupção.

    Os pontos de interrupção são um recurso útil quando você sabe qual linha ou seção de código deseja examinar em detalhes. Para obter informações sobre os diferentes tipos de pontos de interrupção que você pode definir, como pontos de interrupção condicionais, consulte [usando pontos de interrupção](../debugger/using-breakpoints.md).

## <a name="navigate-code-in-the-debugger-using-step-commands"></a>Navegar pelo código no depurador usando comandos de etapa

Geralmente, usamos atalhos de teclado aqui porque essa é uma boa maneira de executar o aplicativo rapidamente no depurador (os comandos equivalentes, como os comandos de menu, são mostrados entre parênteses).

1. Enquanto estiver em pausa no `for` loop no `main` método, pressione **F11** (ou escolha **debug > Step Into**) duas vezes para avançar para a `SendMessage` chamada de método.

     Depois de pressionar **F11** duas vezes, você deve estar nesta linha de código:

     `SendMessage(name, a[i]);`

1. Pressione **F11** mais uma vez para entrar no `SendMessage` método.

     O ponteiro amarelo avança para o `SendMessage` método.

     ![Use F11 para entrar no código](../debugger/media/get-started-f11-cpp.png "Passo F10")

     F11 é o comando **Intervir**, que avança a execução do aplicativo uma instrução por vez. F11 é uma boa maneira de examinar o fluxo de execução com o máximo de detalhes. (Para mover-se mais rapidamente pelo código, mostraremos algumas outras opções também.) Por padrão, o depurador ignora o código que não é do usuário (se você quiser obter mais detalhes, consulte [apenas meu código](../debugger/just-my-code.md)).

     Digamos que você concluiu a análise do `SendMessage` método e deseja sair do método, mas permanecerá no depurador. Você pode fazer isso usando o comando **Depuração Circular**.

1. Pressione **Shift**  +  **F11** (ou **debug > Step Out**).

     Esse comando retoma a execução do aplicativo (e avança o depurador) até que o método ou a função atual retorne.

     Você deve estar de volta no `for` loop no `main` método, em pausa na chamada do `SendMessage` método.

1. Pressione **F11** várias vezes até voltar para a chamada do `SendMessage` método novamente.

1. Enquanto estiver em pausa na chamada do método, pressione **F10** (ou escolha **depurar > etapas**) uma vez.

     ![Use F10 para percorrer o código](../debugger/media/get-started-step-over-cpp.png "Passo F10")

     Observe que, desta vez, o depurador não Percorra o `SendMessage` método. **F10** avança o depurador sem intervir em funções ou métodos no código do aplicativo (o código ainda é executado). Pressionando **F10** na chamada do método `SendMessage` (em vez de **F11**), ignoramos o código de implementação de `SendMessage` (que, no momento, talvez não seja de nosso interesse). Para obter mais informações sobre diferentes maneiras de se mover pelo seu código, consulte [navegar no código no depurador](../debugger/navigating-through-code-with-the-debugger.md).

## <a name="navigate-code-using-run-to-click"></a>Navegar usando Executar até o Clique

1. Pressione **F5** para avançar para o ponto de interrupção.

1. No editor de código, role para baixo e focalize a `std::wcout` função no `SendMessage` método até que a **execução verde clique** no botão ![Executar para clicar](../debugger/media/dbg-tour-run-to-click.png "RunToClick") em aparecer à esquerda. A dica de ferramenta para o botão mostra "Realizar a execução até aqui".

     ![Usar o recurso executar para clicar](../debugger/media/get-started-run-to-click-cpp.png "Executar com um Clique")

   > [!NOTE]
   > O botão **Executar até o Clique** é novo no [!include[vs_dev15](../misc/includes/vs_dev15_md.md)]. (Se você não vir o botão de seta verde, use **F11** neste exemplo em vez de avançar o depurador para o lugar certo.)

2. Clique no botão **Executar para clicar** em ![Executar para clicar em](../debugger/media/dbg-tour-run-to-click.png "RunToClick").

    O depurador avança para a `std::wcout` função.

    O uso desse botão é semelhante à configuração de um ponto de interrupção temporário. **Executar até o Clique** é útil para abranger rapidamente uma região visível do código do aplicativo (você pode clicar em qualquer arquivo aberto).

## <a name="restart-your-app-quickly"></a>Reinicie o aplicativo rapidamente

Clique no botão **reiniciar** ![aplicativo de reinicialização](../debugger/media/dbg-tour-restart.png "RestartApp") na barra de ferramentas depurar (**Ctrl**  +  **Shift**  +  **F5**).

Ao pressionar **Reiniciar**, você economiza tempo em comparação com a opção de parar o aplicativo e reiniciar o depurador. O depurador é pausado no primeiro ponto de interrupção que é atingido pela execução do código.

O depurador para novamente no ponto de interrupção que você definiu anteriormente dentro do `for` loop.

## <a name="inspect-variables-with-data-tips"></a>Inspecionar variáveis com dicas de dados

Os recursos que permitem que você inspecione variáveis são uns dos mais úteis do depurador e há diferentes maneiras de fazer isso. Muitas vezes, ao tentar depurar um problema, você tenta descobrir se as variáveis estão armazenando os valores que elas deveriam conter em um momento específico.

1. Enquanto estiver em pausa na `name += letters[i]` instrução, focalize a `letters` variável e você verá o valor padrão, `size={10}` .

1. Expanda a `letters` variável para ver suas propriedades, que incluem todos os elementos que a variável contém.

1. Em seguida, passe o mouse sobre a `name` variável e você verá seu valor atual, uma cadeia de caracteres vazia.

1. Pressione **F5** (ou **debug**  >  **continue**) algumas vezes para iterar várias vezes pelo `for` loop, pausando novamente no ponto de interrupção e passando o mouse sobre a `name` variável a cada vez para verificar seu valor.

     ![Exibir uma dica de dados](../debugger/media/get-started-data-tip-cpp.png "Exibir uma dica de dados")

     O valor da variável é alterado com cada iteração do `for` loop, mostrando valores de `f` , então, `fr` `fre` e assim por diante.

     Muitas vezes, durante a depuração, você deseja uma maneira rápida de verificar valores de propriedade em variáveis, para ver se eles estão armazenando os valores que você espera que armazenem. As dicas de dados são uma boa maneira de fazer isso.

## <a name="inspect-variables-with-the-autos-and-locals-windows"></a>Inspecionar variáveis com as janelas Autos e Locais

1. Examine a janela **Autos** na parte inferior do editor de códigos.

    Se ele estiver fechado, abra-o enquanto estiver em pausa no depurador escolhendo **depurar**  >  **janelas**  >  **automáticas**.

    Na janela **Autos**, veja as variáveis e seus valores atuais. A janela **Autos** mostra todas as variáveis usadas na linha atual ou a linha anterior (verifique a documentação para saber o comportamento específico a uma linguagem).

1. Em seguida, examine a janela **Locais**, em uma guia ao lado da janela **Autos**.

1. Expanda a `letters` variável para mostrar os elementos que ela contém.

     ![Inspecionar variáveis na janela locais](../debugger/media/get-started-locals-window-cpp.png "Janela Locais")

    A janela **Locais** mostra as variáveis que estão no [escopo](https://www.wikipedia.org/wiki/Scope_(computer_science)) atual, ou seja, o contexto de execução atual.

## <a name="set-a-watch"></a>Definir uma inspeção

1. Na janela principal do editor de código, clique com o botão direito do mouse na `name` variável e escolha **Adicionar inspeção**.

    A janela **Inspeção** é aberta na parte inferior do editor de códigos. Você pode usar uma janela **Inspeção** para especificar uma variável (ou uma expressão) que deseja acompanhar.

    Agora, você tem um observador definido na `name` variável e pode ver seu valor alterado à medida que percorre o depurador. Ao contrário das outras janelas de variáveis, a janela **Inspeção** sempre mostra as variáveis que você está inspecionando (eles ficam esmaecidas quando estão fora do escopo).

## <a name="examine-the-call-stack"></a>Examinar a pilha de chamadas

1. Durante a pausa no loop `for`, clique na janela **Pilha de Chamadas** que fica aberta por padrão no painel inferior direito.

    Se ele estiver fechado, abra-o enquanto estiver em pausa no depurador escolhendo **depurar**  >    >  **pilha de chamadas** do Windows.

2. Clique em **F11** algumas vezes até ver a pausa do depurador no `SendMessage` método. Examine a janela **Pilha de Chamadas**.

    ![Examinar a pilha de chamadas](../debugger/media/get-started-call-stack-cpp.png "ExamineCallStack")

    A janela **Pilha de Chamadas** mostra a ordem em que os métodos e as funções são chamados. A linha superior mostra a função atual (o método `SendMessage` neste aplicativo). A segunda linha mostra que `SendMessage` foi chamado por meio do método `main` e assim por diante.

   > [!NOTE]
   > A janela **Pilha de Chamadas** é semelhante à perspectiva de Depuração em alguns IDEs, como o Eclipse.

    A pilha de chamadas é uma boa maneira de examinar e entender o fluxo de execução de um aplicativo.

    Você pode clicar duas vezes em uma linha de código para examinar esse código-fonte. Isso também altera o escopo atual que está sendo inspecionado pelo depurador. Essa ação não avança o depurador.

    Você também pode usar os menus acessados ao clicar com o botão direito do mouse na janela **Pilha de Chamadas** para fazer outras coisas. Por exemplo, você pode inserir pontos de interrupção em funções especificadas, avançar o depurador usando **Executar até o Cursor** e examinar o código-fonte. Para obter mais informações, confira [Como examinar a pilha de chamadas](../debugger/how-to-use-the-call-stack-window.md).

## <a name="change-the-execution-flow"></a>Alterar o fluxo de execução

1. Pressione **F11** duas vezes para executar a `std::wcout` função.

1. Com o depurador pausado na `SendMessage` chamada do método, use o mouse para pegar a seta amarela (o ponteiro de execução) à esquerda e mova a seta amarela uma linha para cima, voltando para `std::wcout` .

1. Pressione **F11**.

    O depurador executa novamente a `std::wcout` função (você vê isso na saída da janela do console).

    Alterando o fluxo de execução, você pode fazer coisas como testar caminhos de execução de código diferentes ou executar novamente o código sem reiniciar o depurador.

    > [!WARNING]
    > Geralmente, você precisa ter cuidado com esse recurso. Um aviso é exibido na dica de ferramenta. Outros avisos também podem ser exibidos. Ao mover o ponteiro não é possível reverter o aplicativo para um estado anterior.

1. Pressione **F5** para continuar a execução do aplicativo.

    Parabéns por concluir este tutorial.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como iniciar o depurador, percorrer o código e inspecionar variáveis. Talvez você queira obter uma visão geral dos recursos do depurador, com links para mais informações.

> [!div class="nextstepaction"]
> [Introdução ao depurador](../debugger/debugger-feature-tour.md)

