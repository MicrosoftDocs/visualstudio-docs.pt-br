---
title: ASP.NET Core de depuração
description: Depurar ASP.NET Core usando o depurador do Visual Studio
ms.custom: mvc
ms.date: 08/06/2018
ms.topic: quickstart
helpviewer_keywords:
- debugger
ms.assetid: f4cea2e1-08dc-47ac-aba2-3b8c338e607f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: bbe3d23301f0853626a930855acf4b595c6a2923
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2020
ms.locfileid: "75847883"
---
# <a name="quickstart-debug-aspnet-core-with-the-visual-studio-debugger"></a>Início rápido: Depurar ASP.NET Core com o depurador do Visual Studio

O depurador do Visual Studio oferece muitos recursos avançados para ajudar a depurar seus aplicativos. Este tópico fornece uma maneira rápida de conhecer alguns dos recursos básicos.

## <a name="create-a-new-project"></a>Crie um novo projeto

1. {1&gt;Abra o Visual Studio.&lt;1}

    ::: moniker range=">=vs-2019"
    Pressione **Esc** para fechar a janela de início. Digite **Ctrl + Q** para abrir a caixa de pesquisa, digite **asp.net**, escolha **Modelos** e, em seguida, escolha **Criar novo projeto de Aplicativo Web ASP.NET Core**. Na caixa de diálogo que aparece, escolha **Criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Na barra de menus superior, escolha **Arquivo** > **Novo** > **Projeto**. No painel esquerdo da caixa de diálogo **Novo projeto**, em **Visual C#** , escolha **Web** e, em seguida, no painel central, escolha **Aplicativo Web ASP.NET Core**. Digite um nome como **MyDbgApp** e clique em **OK**.

    Na caixa de diálogo exibida, escolha **Aplicativo Web** no painel central e clique em **OK**.

    ![Criar um aplicativo Web](../debugger/media/dbg-qs-aspnet-choose-web-app.png)
    ::: moniker-end

    Caso não veja o modelo de projeto **Aplicativo Web do ASP.NET Core**, acesse **Ferramentas** > **Obter Ferramentas e Recursos...** , que abre o Instalador do Visual Studio. Escolha a carga de trabalho **ASP.NET e desenvolvimento para a Web** e, em seguida, selecione **Modificar**.

    O Visual Studio cria o projeto.

1. No Gerenciador de Soluções, abra About.cshtml.cs (em Páginas/About.cshtml) e substitua o seguinte código

    ```csharp
    public void OnGet()
    {
        Message = "Your application description page.";
    }
    ```

    com este código:

    ```csharp
    public void OnGet()
    {
        LinkedList<int> result = doWork();
        Message = "Result of work: " + result.First.Value + ", " + result.First.Value;
    }

    private static LinkedList<int> doWork()
    {
        LinkedList<int> c1 = new LinkedList<int>();

        c1.AddLast(10);
        c1.AddLast(20);

        LinkedList<int> c2 = new LinkedList<int>(c1);

        return c2;

    }
    ```

## <a name="set-a-breakpoint"></a>Definir um ponto de interrupção

Um *ponto de interrupção* é um marcador que indica quando o Visual Studio deve suspender o código em execução para que você possa examinar os valores das variáveis ou o comportamento de memória ou se um branch de código está sendo executado ou não. É o recurso mais básico na depuração.

1. Para definir o ponto de interrupção, clique na medianiz à esquerda da função `doWork` (ou selecione a linha de código e pressione **F9**).

    ![Definir um ponto de interrupção](../debugger/media/dbg-qs-set-breakpoint-aspnet.png)

    O ponto de interrupção é definido à esquerda da chave de abertura (`{`).

1. Agora pressione **F5** (ou escolha **Depurar > Iniciar depuração**).

1. Quando a página da Web for carregada, clique no link **Sobre** na parte superior da página da Web.

    O depurador pausa no local em que você define o ponto de interrupção. A instrução em que a execução do depurador e do aplicativo está em pausa é indicada pela seta amarela. A linha com a chave de abertura (`{`) após a declaração da função `doWork` ainda não foi executada.

    ![Atingir um ponto de interrupção](../debugger/media/dbg-qs-hit-breakpoint-aspnet.png)

    > [!TIP]
    > Se você tiver um ponto de interrupção em um loop ou recursão ou se tiver muitos pontos de interrupção que percorre com frequência, use um [ponto de interrupção condicional](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression) para garantir que seu código seja suspenso APENAS quando condições específicas forem atendidas. Isso economiza tempo e pode também tornar mais fácil depurar problemas difíceis de reproduzir.

## <a name="navigate-code"></a>Navegue pelos códigos

Há diferentes comandos para instruir o depurador a continuar. Mostramos um comando de navegação de código útil que está disponível começando pelo Visual Studio 2017.

Enquanto estiver em pausa no ponto de interrupção, passe o mouse sobre a instrução `return c2` até que o botão verde **Executar com um clique**![Executar com um clique](../debugger/media/dbg-tour-run-to-click.png) seja exibido e, em seguida, pressione o botão **Executar com um clique**.

![Executar com um clique](../debugger/media/dbg-qs-run-to-click-aspnet.png)

O aplicativo continua a execução e é pausado na linha de código na qual você clicou no botão.

Comandos de teclado comuns usados para percorrer o código incluem **F10** e **F11**. Para obter instruções mais detalhadas, confira [Introdução ao depurador](../debugger/debugger-feature-tour.md).

## <a name="inspect-variables-in-a-datatip"></a>Inspecionar variáveis em uma datatip

1. Na linha de código atual (indicada pelo ponteiro de execução amarelo), passe o mouse sobre o objeto `c2` com o mouse para mostrar uma datatip.

    ![Exibir uma datatip](../debugger/media/dbg-qs-data-tip-aspnet.png)

    A datatip mostra o valor atual da variável `c2` e permite que você inspecione suas propriedades. Ao depurar, se você vir um valor que não espera, provavelmente haverá um bug nas linhas de código anteriores ou de chamada.

2. Expanda a datatip para examinar os valores de propriedade atuais do objeto `c2`.

3. Se desejar fixar a datatip para poder continuar vendo o valor de `c2` enquanto executa código, clique no pequeno ícone de marcador. (É possível mover a datatip fixada para uma localização conveniente.)

## <a name="edit-code-and-continue-debugging"></a>Editar o código e continuar a depuração

Se identificar uma alteração que deseja testar em seu código enquanto estiver no meio de uma sessão de depuração, será possível fazer isso também.

1. No método `OnGet`, clique na segunda instância de `result.First.Value` e altere `result.First.Value` para `result.Last.Value`.

1. Pressione **F10** (ou **Depurar > Depuração Parcial**) algumas vezes para avançar o depurador e executar o código editado.

    ![Editar e continuar](../debugger/media/dbg-qs-edit-and-continue-aspnet.png "Editar e continuar")

    **F10** avança o depurador uma instrução por vez, mas depura parcialmente as funções, em vez de intervir nelas (o código que você ignora ainda é executado).

Para saber mais sobre como usar editar e continuar e sobre as limitações das funcionalidades, confira [Editar e Continuar](../debugger/edit-and-continue.md).

## <a name="next-steps"></a>{1&gt;{2&gt;Próximas etapas&lt;2}&lt;1}

Neste tutorial, você aprendeu como iniciar o depurador, percorrer o código e inspecionar variáveis. Talvez você queira obter uma visão geral dos recursos do depurador, com links para mais informações.

> [!div class="nextstepaction"]
> [Introdução ao depurador](../debugger/debugger-feature-tour.md)
