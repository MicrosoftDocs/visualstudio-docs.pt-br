---
title: Depurar o ASP.NET
description: Depurar o ASP.NET usando o depurador do Visual Studio
ms.custom: mvc
ms.date: 08/06/2018
ms.technology: vs-ide-debug
ms.topic: quickstart
helpviewer_keywords:
- debugger
ms.assetid: f4cea2e1-08dc-47ac-aba2-3b8c338e607f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
ms.openlocfilehash: 74671401b3e3eaeae5840110dfc37c926266f98a
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39636981"
---
# <a name="quickstart-debug-aspnet-with-the-visual-studio-debugger"></a>Início Rápido: depurar o ASP.NET com o depurador do Visual Studio

O depurador do Visual Studio oferece muitos recursos avançados para ajudar a depurar seus aplicativos. Este tópico fornece uma maneira rápida de conhecer alguns dos recursos básicos.

## <a name="create-a-new-project"></a>Criar um novo projeto 

1. No Visual Studio, escolha **Arquivo > Novo Projeto**.

1. Em **Visual C#**, escolha **Web** e, em seguida, no painel central, escolha **Aplicativo Web ASP.NET Core**.

1. Digite um nome como **MyDbgApp** e clique em **OK**.

1. Na caixa de diálogo exibida, escolha **Aplicativo Web** no painel central e clique em **OK**.

     Se o modelo de projeto **Aplicativo Web** não for exibido, clique no link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto**. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **ASP.NET e desenvolvimento para a Web** e, em seguida, selecione **Modificar**.

    ![Criar um aplicativo Web](../debugger/media/dbg-qs-aspnet-choose-web-app.png)

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

Há diferentes comandos para instruir o depurador a continuar. Mostramos um comando de navegação de código útil que é novo no Visual Studio 2017.

Enquanto estiver em pausa no ponto de interrupção, passe o mouse sobre a instrução `return c2` até que o botão verde **Executar com um clique** ![Executar com um clique](../debugger/media/dbg-tour-run-to-click.png) seja exibido e, em seguida, pressione o botão **Executar com um clique**.

![Executar com um clique](../debugger/media/dbg-qs-run-to-click-aspnet.png)

O aplicativo continua a execução e é pausado na linha de código na qual você clicou no botão.

Comandos de teclado comuns usados para percorrer o código incluem **F10** e **F11**. Para obter mais instruções detalhadas, confira o [Guia do Iniciante](../debugger/getting-started-with-the-debugger.md).

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

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como iniciar o depurador, percorrer o código e inspecionar variáveis. Talvez você queira obter uma visão geral dos recursos do depurador, com links para mais informações.

> [!div class="nextstepaction"]
> [Tour dos recursos do depurador](../debugger/debugger-feature-tour.md)
