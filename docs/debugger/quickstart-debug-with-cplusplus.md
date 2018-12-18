---
title: Depurar C++
description: Depurar código nativo usando o depurador do Visual Studio
ms.custom: mvc
ms.date: 08/06/2018
ms.technology: vs-ide-debug
ms.topic: quickstart
helpviewer_keywords:
- debugger
ms.assetid: 639e430b-6d2d-46bd-b738-8c60dfb384f1
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 036774134f705d95fbc526a9e6a336ac43005820
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39639770"
---
# <a name="quickstart-debug-with-c-using-the-visual-studio-debugger"></a>Início Rápido: depurar com C++ usando o depurador do Visual Studio

O depurador do Visual Studio oferece muitos recursos avançados para ajudar a depurar seus aplicativos. Este tópico fornece uma maneira rápida de conhecer alguns dos recursos básicos.

## <a name="create-a-new-project"></a>Criar um novo projeto 

1. No Visual Studio, escolha **Arquivo > Novo Projeto**.

2. Em **Visual C++**, escolha **Área de Trabalho do Windows** e escolha **Aplicativo de Console do Windows** no painel central.

    Se o modelo de projeto do **Aplicativo de Console do Windows** não for exibido, clique no link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto**. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento para desktop com C++** e, em seguida, selecione **Modificar**.

3. Digite um nome como **MyDbgApp** e clique em **OK**.

    O Visual Studio cria o projeto.

4. Em MyDbgApp.cpp, substitua o código a seguir

    ```c++
    int main()
    {
        return 0;
    }
    ```

    por esse código (não remova `#include "stdafx.h"`):

    ```c++
    #include <list>  
    #include <iostream>

    using namespace std;

    void doWork()
    {
        list <int> c1;

        c1.push_back(10);
        c1.push_back(20);

        const list <int> c2 = c1;
        const int &i = c2.front();
        const int &j = c2.front();
        cout << "The first element is " << i << endl;
        cout << "The second element is " << j << endl;

    }

    int main()
    {
        doWork();
    }
    ```

## <a name="set-a-breakpoint"></a>Definir um ponto de interrupção

Um *ponto de interrupção* é um marcador que indica quando o Visual Studio deve suspender o código em execução para que você possa examinar os valores das variáveis ou o comportamento de memória ou se um branch de código está sendo executado ou não. É o recurso mais básico na depuração.

1. Para definir o ponto de interrupção, clique na medianiz à esquerda da `doWork` chamada de função (ou selecione a linha de código e pressione **F9**).

    ![Definir um ponto de interrupção](../debugger/media/dbg-qs-set-breakpoint.png "Definir um ponto de interrupção")

2. Agora pressione **F5** (ou escolha **Depurar > Iniciar depuração**).

    ![Atingir um ponto de interrupção](../debugger/media/dbg-qs-hit-breakpoint.png "Atingir um ponto de interrupção")

    O depurador pausa no local em que você define o ponto de interrupção. A instrução em que a execução do depurador e do aplicativo está em pausa é indicada pela seta amarela. A linha com a chamada de função `doWork` ainda não foi executada.

    > [!TIP]
    > Se você tiver um ponto de interrupção em um loop ou recursão ou se tiver muitos pontos de interrupção que percorre com frequência, use um [ponto de interrupção condicional](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression) para garantir que seu código seja suspenso APENAS quando condições específicas forem atendidas. Um ponto de interrupção condicional economiza tempo e pode também tornar mais fácil depurar problemas difíceis de reproduzir.

    Ao tentar depurar falhas relacionadas a memória em C++, também é possível usar pontos de interrupção para inspecionar valores de endereço (procure NULL) e contagens de referência. 

## <a name="navigate-code"></a>Navegue pelos códigos

Há diferentes comandos para instruir o depurador a continuar. Mostramos um comando de navegação de código útil que é novo no Visual Studio 2017.

Enquanto estiver em pausa no ponto de interrupção, passe o mouse sobre a instrução `c1.push_back(20)` até que o botão verde **Executar com um clique** ![Executar com um clique](../debugger/media/dbg-tour-run-to-click.png "RunToClick") seja exibido e, em seguida, pressione o botão **Executar com um clique**.

![Executar com um clique](../debugger/media/dbg-qs-run-to-click.png "Executar com um clique")

O aplicativo continua a execução, chamando `doWork`, e é pausado na linha de código em que você clicou no botão.

Comandos de teclado comuns usados para percorrer o código incluem **F10** e **F11**. Para obter mais instruções detalhadas, confira o [Guia do Iniciante](../debugger/getting-started-with-the-debugger.md).

## <a name="inspect-variables-in-a-datatip"></a>Inspecionar variáveis em uma datatip

1. Na linha de código atual (indicada pelo ponteiro de execução amarelo), passe o mouse sobre o objeto `c1` com o mouse para mostrar uma datatip.

    ![Exibir uma datatip](../debugger/media/dbg-qs-data-tip.png "Exibir uma datatip")

    A datatip mostra o valor atual da variável `c1` e permite que você inspecione suas propriedades. Ao depurar, se você vir um valor que não espera, provavelmente haverá um bug nas linhas de código anteriores ou de chamada. 

2. Expanda a datatip para examinar os valores de propriedade atuais do objeto `c1`.

3. Se desejar fixar a datatip para poder continuar vendo o valor de `c1` enquanto executa código, clique no pequeno ícone de marcador. (É possível mover a datatip fixada para uma localização conveniente.)

## <a name="edit-code-and-continue-debugging"></a>Editar o código e continuar a depuração

Se identificar uma alteração que deseja testar em seu código enquanto estiver no meio de uma sessão de depuração, será possível fazer isso também.

1. Clique na segunda instância de `c2.front()` e altere `c2.front()` para `c2.back()`.

2. Pressione **F10** (ou **Depurar > Depuração Parcial**) algumas vezes para avançar o depurador e executar o código editado.

    ![Editar e continuar](../debugger/media/dbg-qs-edit-and-continue.gif "Editar e continuar")

    **F10** avança o depurador uma instrução por vez, mas depura parcialmente as funções, em vez de intervir nelas (o código que você ignora ainda é executado).

Para saber mais sobre como usar editar e continuar e sobre as limitações das funcionalidades, confira [Editar e Continuar](../debugger/edit-and-continue.md).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como iniciar o depurador, percorrer o código e inspecionar variáveis. Talvez você queira obter uma visão geral dos recursos do depurador, com links para mais informações.

> [!div class="nextstepaction"]
> [Tour dos recursos do depurador](../debugger/debugger-feature-tour.md)
