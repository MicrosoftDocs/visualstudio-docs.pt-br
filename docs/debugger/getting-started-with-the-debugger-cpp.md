---
title: Aprenda a depurar C++ usando o depurador do Visual Studio
ms.description: Learn how to start the Visual Studio debugger, step through code, and inspect data.
ms.custom: debug-experiment
ms.date: 08/01/2018
ms.technology: vs-ide-debug
ms.topic: tutorial
dev_langs:
- C++
helpviewer_keywords:
- debugger
ms.assetid: 62734c0d-a75a-4576-8f73-0e97c19280e1
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 56ef97401a87f39e9c3bfd3138ee3a26646064c6
ms.sourcegitcommit: d7f232a7596420e40ff8051d42cdf90203af4a74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52825860"
---
# <a name="tutorial-learn-to-debug-c-code-using-visual-studio"></a>Tutorial: aprenda a depurar código C++ usando o Visual Studio

Este artigo apresenta os recursos do depurador do Visual Studio passo a passo. Se você quiser obter uma visão mais detalhada dos recursos do depurador, confira [Tour pelos recursos do depurador](../debugger/debugger-feature-tour.md). Quando você *depura seu aplicativo*, isso normalmente significa executar o aplicativo com o depurador anexado. Quando você faz isso, o depurador fornece várias maneiras de mostrar o que o código está fazendo enquanto é executado. Você pode percorrer o código e examinar os valores armazenados em variáveis, definir inspeções em variáveis para ver quando os valores mudam, examinar o caminho de execução do código, ver se um branch de código está em execução e assim por diante. Se esta for sua primeira tentativa de depurar um código, leia [Como depurar para iniciantes absolutos](../debugger/debugging-absolute-beginners.md) antes continuar neste artigo.

| | |
|---------|---------|
| ![ícone de câmera para vídeo](../install/media/video-icon.png "Assistir a um vídeo") | [Assista a um vídeo](https://mva.microsoft.com/en-US/training-courses-embed/getting-started-with-visual-studio-2017-17798/Debugger-Feature-tour-of-Visual-studio-2017-sqwiwLD6D_1111787171) sobre depuração que mostra etapas semelhantes. |

Neste tutorial, você irá:

> [!div class="checklist"]
> * Iniciar o depurador e atingir os pontos de interrupção.
> * Aprender os comandos para percorrer o código no depurador
> * Inspecionar variáveis em dicas de dados e janelas do depurador
> * Examinar a pilha de chamadas

## <a name="prerequisites"></a>Pré-requisitos

* Você precisa ter o Visual Studio 2017 instalado e a carga de trabalho de **Desenvolvimento para desktop com C++**.

    Se você ainda não instalou o Visual Studio, acesse a página  [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)  para instalá-lo gratuitamente.

    Se você precisar instalar a carga de trabalho, mas já tiver o Visual Studio, clique no link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto** (selecione **Arquivo** > **Novo** > **Projeto**). O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento para desktop com C++** e, em seguida, selecione **Modificar**.

## <a name="create-a-project"></a>Criar um projeto

1. No Visual Studio, escolha **Arquivo > Novo Projeto**.

2. Em **Visual C++**, escolha **Área de Trabalho do Windows** e escolha **Aplicativo de Console do Windows** no painel central.

    Se o modelo de projeto do **Aplicativo de Console do Windows** não for exibido, clique no link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto**. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento para desktop com C++** e, em seguida, selecione **Modificar**.

3. Digite um nome como **get-started-debugging** e clique em **OK**.

    O Visual Studio cria o projeto.

4. Em *get-started-debugging.cpp*, substitua o código a seguir

    ```c++
    int main()
    {
        return 0;
    }
    ```

    com este código:

    ```c++
    #include "pch.h"

    #include <string>
    #include <vector>
    #include <iostream>

    class Shape
    {
        int privateX = 0;
        int privateY = 0;
        int privateHeight = 0;
        int privateWidth = 0;

        int getX() const { return privateX; }
        void setX(int value) { privateX = value; }

        int getY() const { return privateY; }
        void setY(int value) { privateY = value; }

        int getHeight() const { return privateHeight; }
        void setHeight(int value) { privateHeight = value; }

        int getWidth() const { return privateWidth; }
        void setWidth(int value) { privateWidth = value; }

        public:
        // Virtual method
        virtual void Draw()
        {
            std::wcout << L"Performing base class drawing tasks" << std::endl;
        }
    };

    class Circle : public Shape
    {
        public:
        void Draw() override
        {
        // Code to draw a circle...
        std::wcout << L"Drawing a circle" << std::endl;
        Shape::Draw();
        }
    };

    class Rectangle : public Shape
    {
        public:
        void Draw() override
        {
        // Code to draw a rectangle...
        std::wcout << L"Drawing a rectangle" << std::endl;
        Shape::Draw();
        }
    };

    class Triangle : public Shape
    {
        public:
        void Draw() override
        {
        // Code to draw a triangle...
        std::wcout << L"Drawing a trangle" << std::endl;
        Shape::Draw();
        }
    };

    int main(std::vector<std::wstring> &args)
    {
        auto shapes = std::vector<Shape*>
        {
            new Rectangle(),
            new Triangle(),
            new Circle()
        };

        for (auto shape : shapes)
        {
            shape->Draw();
        }
    }

    /* Output:
    Drawing a rectangle
    Performing base class drawing tasks
    Drawing a triangle
    Performing base class drawing tasks
    Drawing a circle
    Performing base class drawing tasks
    */
    ```

## <a name="start-the-debugger"></a>Inicie o depurador.

1. Pressione **F5** (**Depurar > Iniciar Depuração**) ou o botão **Iniciar Depuração** ![Iniciar Depuração](../debugger/media/dbg-tour-start-debugging.png "Iniciar Depuração") na barra de ferramentas Depurar.

     **F5** inicia o aplicativo com o depurador anexado ao processo do aplicativo, mas nós ainda não fizemos nada de especial para examinar o código. Portanto, o aplicativo apenas é carregado e a saída do console é exibida.

    ```
    Drawing a rectangle
    Performing base class drawing tasks
    Drawing a triangle
    Performing base class drawing tasks
    Drawing a circle
    Performing base class drawing tasks
    ```

     Neste tutorial, vamos analisar melhor esse aplicativo usando o depurador e analisar os recursos do depurador.

2. Pare o depurador pressionando o botão de parada vermelho ![Parar Depuração](../debugger/media/dbg-tour-stop-debugging.png "Parar Depuração").

## <a name="set-a-breakpoint-and-start-the-debugger"></a>Definir um ponto de interrupção e iniciar o depurador

1. No loop `for` da função `main`, defina um ponto de interrupção clicando na margem esquerda da seguinte linha de código:

    `shape->Draw()`

    Aparece um círculo vermelho no qual você definiu o ponto de interrupção.

    Pontos de interrupção são o recurso mais básico e essencial da depuração confiável. Um ponto de interrupção indica quando o Visual Studio deve suspender o código em execução para que você possa examinar os valores das variáveis ou o comportamento de memória ou se uma ramificação de código está sendo executada ou não. 

2. Pressione **F5** ou o botão **Iniciar Depuração** ![Start Debugging](../debugger/media/dbg-tour-start-debugging.png "Iniciar Depuração", o aplicativo é iniciado e o depurador executa a linha de código em que você definiu o ponto de interrupção.

    ![Definir e atingir um ponto de interrupção](../debugger/media/get-started-set-breakpoint-cpp.gif)

    A seta amarela representa a instrução na qual o depurador está em pausa, que também suspende a execução do aplicativo no mesmo ponto (essa instrução ainda não foi executada).

     Se o aplicativo ainda não estiver em execução, **F5** iniciará o depurador e o interromperá no primeiro ponto de interrupção. Caso contrário, **F5** continuará executando o aplicativo até o próximo ponto de interrupção.

    Os pontos de interrupção são um recurso útil quando você sabe qual linha ou seção de código deseja examinar em detalhes.

## <a name="navigate-code-in-the-debugger-using-step-commands"></a>Navegar pelo código no depurador usando comandos de etapa

Geralmente, usamos atalhos de teclado aqui porque essa é uma boa maneira de executar o aplicativo rapidamente no depurador (os comandos equivalentes, como os comandos de menu, são mostrados entre parênteses).

1. Enquanto estiver em pausa na chamada de método `shape->Draw` na função `main`, pressione **F11** (ou escolha **Depurar > Intervir**) para avançar no código até a classe `Rectangle`.

     ![Usar F11 para intervir no código](../debugger/media/get-started-f11-cpp.png "F11 Intervir")

     F11 é o comando **Intervir**, que avança a execução do aplicativo uma instrução por vez. F11 é uma boa maneira de examinar o fluxo de execução com o máximo de detalhes. (Também vamos mostrar algumas outras opções para percorrer o código com mais rapidez.) Por padrão, o depurador ignora as partes do código que não são do usuário (se quiser saber mais detalhes, confira [Apenas Meu Código](../debugger/just-my-code.md)).

2. Pressione **F10** (ou escolha **Depurar > Depuração Parcial**) algumas vezes até que o depurador pare na chamada de método `Shape::Draw`. Em seguida, pressione **F10** mais uma vez.

     ![Usar F10 para Depuração Parcial do código](../debugger/media/get-started-step-over-cpp.png "F10 Depuração Parcial")

     Observe neste momento que o depurador não intervém no método `Draw` da classe base (`Shape`). **F10** avança o depurador sem intervir em funções ou métodos no código do aplicativo (o código ainda é executado). Pressionando F10 na chamada de método `Shape::Draw` (em vez de **F11**), ignoramos o código de implementação de `Draw` na classe base (no qual talvez não estejamos interessados no momento).

## <a name="navigate-code-using-run-to-click"></a>Navegar usando Executar até o Clique

1. No editor de códigos, role para baixo e passe o mouse sobre o `std::cout` na classe `Triangle` até que o botão verde **Executar até o Clique** ![Executar até o Clique](../debugger/media/dbg-tour-run-to-click.png "RunToClick") apareça à esquerda.

     ![Usar o recurso Executar até o Clique](../debugger/media/get-started-run-to-click-cpp.png "Executar até o Clique")

   > [!NOTE]
   > O botão **Executar até o Clique** é novo no [!include[vs_dev15](../misc/includes/vs_dev15_md.md)]. Se o botão de seta verde não for exibido, use **F11**, neste exemplo, para avançar o depurador até o lugar certo.

2. Clique no botão **Executar até o Clique** ![Executar até o Clique](../debugger/media/dbg-tour-run-to-click.png "RunToClick").

    O uso desse botão é semelhante à configuração de um ponto de interrupção temporário. **Executar até o Clique** é útil para abranger rapidamente uma região visível do código do aplicativo (você pode clicar em qualquer arquivo aberto).

    O depurador avança para a implementação do método `std::cout` da classe `Triangle`.

    Durante a pausa, você poderá observar um erro de digitação! A saída "Drawing a trangle" contém um erro de digitação. Podemos corrigir isso aqui mesmo enquanto o aplicativo é executado no depurador.

## <a name="edit-code-and-continue-debugging"></a>Editar o código e continuar a depuração

1. Clique em "Drawing a trangle" e digite uma correção, alterando "trangle" para "triangle".

1. Pressione **F11** uma vez, você verá uma mensagem que o código está recompilando e, em seguida, o depurador avançará novamente.

    > [!NOTE]
    > Dependendo de qual tipo de código você editar no depurador, será exibida uma mensagem de aviso. Em alguns cenários, o código precisará ser recompilado para que você possa continuar.

## <a name="step-out"></a>Depuração circular

Digamos que você termine de examinar o método `Draw` na classe `Triangle` e queira sair da função, mas continuar no depurador. Você pode fazer isso usando o comando **Depuração Circular**.

1. Pressione **Shift** + **F11** (ou **Depurar > Depuração Circular**).

     Este comando retoma a execução do aplicativo (e avança o depurador) até que a função atual retorne.

     Você deve ter voltado ao loop `for` no método `main`.

## <a name="restart-your-app-quickly"></a>Reinicie o aplicativo rapidamente

Clique no botão **Reiniciar** ![Reiniciar Aplicativo](../debugger/media/dbg-tour-restart.png "RestartApp") na barra de ferramentas Depurar (**Ctrl** + **Shift** + **F5**).

Ao pressionar **Reiniciar**, você economiza tempo em comparação com a opção de parar o aplicativo e reiniciar o depurador. O depurador é pausado no primeiro ponto de interrupção que é encontrado pela execução do código.

O depurador para novamente no ponto de interrupção definido por você no método `shape->Draw()`.

## <a name="inspect-variables-with-data-tips"></a>Inspecionar variáveis com dicas de dados

Os recursos que permitem que você inspecione variáveis são uns dos mais úteis do depurador e há diferentes maneiras de fazer isso. Muitas vezes, ao tentar depurar um problema, você tenta descobrir se as variáveis estão armazenando os valores que elas deveriam conter em um momento específico.

1. Durante a pausa no método `shape->Draw()`, passe o mouse sobre o contêiner `shapes` (objeto de vetor) e veja o valor da propriedade padrão dele, a propriedade `size`, mostrando `size=3`.

1. Expanda o objeto `shapes` para ver todas as suas propriedades, como o primeiro índice da matriz `[0]`, que tem um endereço de memória.

    Você pode expandir mais os objetos para exibir suas propriedades.

1. Expanda o primeiro índice `[0]` para ver a propriedade `privateHeight` do retângulo.

     ![Exibir uma dica de dados](../debugger/media/get-started-data-tip-cpp.png "Exibir uma dica de dados")

     Muitas vezes, durante a depuração, queremos uma maneira rápida de verificar valores de propriedade em objetos e as dicas de dados são uma ótima maneira de fazer isso.

## <a name="inspect-variables-with-the-autos-and-locals-windows"></a>Inspecionar variáveis com as janelas Autos e Locais

1. Examine a janela **Autos** na parte inferior do editor de códigos.

     ![Inspecionar variáveis na janela Autos](../debugger/media/get-started-autos-window-cpp.png "Janela Autos")

    Na janela **Autos**, veja as variáveis e seus valores atuais. Para C++, a janela **Autos** mostra as variáveis nas três linhas de código anteriores.

2. Em seguida, examine a janela **Locais**, em uma guia ao lado da janela **Autos**.

    A janela **Locais** mostra as variáveis que estão no [escopo](https://www.wikipedia.org/wiki/Scope_(computer_science)) atual, ou seja, o contexto de execução de código atual.

## <a name="set-a-watch"></a>Definir uma inspeção

1. Na janela principal do editor de códigos, clique com o botão direito do mouse no objeto `shapes` e escolha **Adicionar Inspeção**.

    A janela **Inspeção** é aberta na parte inferior do editor de códigos. Você pode usar uma janela **Inspeção** para especificar uma variável (ou uma expressão) que deseja acompanhar.

    Agora, há uma inspeção definida no objeto `shapes` e você pode ver seu valor sendo alterado, conforme percorre o depurador. Ao contrário das outras janelas de variáveis, a janela **Inspeção** sempre mostra as variáveis que você está inspecionando (eles ficam esmaecidas quando estão fora do escopo).

## <a name="examine-the-call-stack"></a>Examinar a pilha de chamadas

1. Durante a pausa no loop `for`, clique na janela **Pilha de Chamadas** que fica aberta por padrão no painel inferior direito.

2. Pressione **F11** algumas vezes até que o depurador seja colocado em pausa no método `Shape::Draw` da classe `Rectangle` no editor de códigos. Examine a janela **Pilha de Chamadas**.

    ![Examinar a pilha de chamadas](../debugger/media/get-started-call-stack-cpp.png "ExamineCallStack")

    A janela **Pilha de Chamadas** mostra a ordem em que os métodos e as funções são chamados. A linha superior mostra a função atual (o método `Rectangle::Draw` neste exemplo). A segunda linha mostra que `Rectangle::Draw` foi chamado por meio da função `main` e assim por diante.

   > [!NOTE]
   > A janela **Pilha de Chamadas** é semelhante à perspectiva de Depuração em alguns IDEs, como o Eclipse.

    A pilha de chamadas é uma boa maneira de examinar e entender o fluxo de execução de um aplicativo.

    Você pode clicar duas vezes em uma linha de código para examinar esse código-fonte. Isso também altera o escopo atual que está sendo inspecionado pelo depurador. Essa ação não avança o depurador.

    Você também pode usar os menus acessados ao clicar com o botão direito do mouse na janela **Pilha de Chamadas** para fazer outras coisas. Por exemplo, você pode inserir pontos de interrupção em funções especificadas, avançar o depurador usando **Executar até o Cursor** e examinar o código-fonte. Para obter mais informações, confira [Como examinar a pilha de chamadas](../debugger/how-to-use-the-call-stack-window.md).

## <a name="change-the-execution-flow"></a>Alterar o fluxo de execução

1. Com o depurador em pausa na chamada de método `Shape::Draw`, use o mouse para segurar a seta amarela (o ponteiro de execução) à esquerda e movê-la uma linha para cima, até a chamada de método `std::cout`.

1. Pressione **F11**.

    O depurador executa novamente o método `std::cout` (você vê isso na saída da janela do console).

    Alterando o fluxo de execução, você pode fazer coisas como testar caminhos de execução de código diferentes ou executar novamente o código sem reiniciar o depurador.

    > [!WARNING]
    > Geralmente, você precisa ter cuidado com esse recurso. Um aviso é exibido na dica de ferramenta. Outros avisos também podem ser exibidos. Ao mover o ponteiro não é possível reverter o aplicativo para um estado anterior.

1. Pressione **F5** para continuar a execução do aplicativo.

    Parabéns por concluir este tutorial.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como iniciar o depurador, percorrer o código e inspecionar variáveis. Talvez você queira obter uma visão geral dos recursos do depurador, com links para mais informações.

> [!div class="nextstepaction"]
> [Introdução ao depurador](../debugger/debugger-feature-tour.md)
