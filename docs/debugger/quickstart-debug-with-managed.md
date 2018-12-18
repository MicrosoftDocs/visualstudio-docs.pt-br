---
title: Depurar código gerenciado | Microsoft Docs
description: Depurar C# ou Visual Basic usando o depurador do Visual Studio
ms.custom: mvc
ms.date: 03/18/2018
ms.technology: vs-ide-debug
ms.topic: quickstart
helpviewer_keywords:
- debugger
ms.assetid: f4cea2e1-08dc-47ac-aba2-3b8c338e607f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: e35d102a30ffc7b80d39f359542bbdc4c00feff6
ms.sourcegitcommit: a7de99f36e9ead7ea9e9bac23c88d05ddfc38b00
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52257180"
---
# <a name="quickstart-debug-with-c-or-visual-basic-using-the-visual-studio-debugger"></a>Início Rápido: depurar com C# ou Visual Basic usando o depurador do Visual Studio

O depurador do Visual Studio oferece muitos recursos avançados para ajudar a depurar seus aplicativos. Este tópico fornece uma maneira rápida de conhecer alguns dos recursos básicos.

## <a name="create-a-new-project"></a>Criar um novo projeto 

1. No Visual Studio, escolha **Arquivo > Novo Projeto**.

2. Em **Visual C#** ou **Visual Basic**, escolha **.NET Core** e, em seguida, no painel central, escolha **Aplicativo de Console (.NET Core)**.

     Se você não vir o modelo de projeto do **Aplicativo de Console (.NET Core)**, clique no link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto**. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento de área de trabalho do .NET** e **.NET Core**; em seguida, selecione **Modificar**.

3. Digite um nome como **MyDbgApp** e clique em **OK**.

    O Visual Studio cria o projeto.

4. Em *Program.cs* ou *Module1.vb*, substitua o seguinte código

    ```csharp
    class Program
    {
        static void Main(string[] args)
        {
        }
    }
    ```

    ```vb
    Module Module1
        Sub Main()
        End Sub
    End Module
    ```

    com este código:

    ```csharp
    class Program
    {
        private static void doWork()
        {
            LinkedList<int> c1 = new LinkedList<int>();

            c1.AddLast(10);
            c1.AddLast(20);

            LinkedList<int> c2 = new LinkedList<int>(c1);
            int i = c2.First.Value;
            int j = c2.First.Value;
            Console.Write("The first element is ");
            Console.Write(i);
            Console.Write("\n");
            Console.Write("The second element is ");
            Console.Write(j);
            Console.Write("\n");

        }

        static int Main()
        {
            // using namespace std;
            doWork();
            return 0;

        }
    }
    ```

    ```vb
    Imports System.Collections.Generic

    Namespace MyDbgApp
        Class Program
            Private Shared Sub doWork()
                Dim c1 As New LinkedList(Of Integer)()

                c1.AddLast(10)
                c1.AddLast(20)

                Dim c2 As New LinkedList(Of Integer)(c1)
                Dim i As Integer = c2.First.Value
                Dim j As Integer = c2.First.Value
                Console.Write("The first element is ")
                Console.Write(i)
                Console.Write(vbLf)
                Console.Write("The second element is ")
                Console.Write(j)
                Console.Write(vbLf)

            End Sub

            Public Shared Function Main() As Integer
                ' using namespace std;
                doWork()
                Return 0

            End Function
        End Class
    End Namespace
    ```

    > [!NOTE]
    > No Visual Basic, verifique se o objeto de inicialização é definido como `Sub Main` (**Propriedades > Aplicativo > Objeto de Inicialização**).

## <a name="set-a-breakpoint"></a>Definir um ponto de interrupção

Um *ponto de interrupção* é um marcador que indica quando o Visual Studio deve suspender o código em execução para que você possa examinar os valores das variáveis ou o comportamento de memória ou se um branch de código está sendo executado ou não. É o recurso mais básico na depuração.

1. Para definir o ponto de interrupção, clique na medianiz à esquerda da `doWork` chamada de função (ou selecione a linha de código e pressione **F9**).

    ![Definir um ponto de interrupção](../debugger/media/dbg-qs-set-breakpoint-csharp.png "Definir um ponto de interrupção")

2. Agora pressione **F5** (ou escolha **Depurar > Iniciar depuração**).

    ![Atingir um ponto de interrupção](../debugger/media/dbg-qs-hit-breakpoint-csharp.png "Atingir um ponto de interrupção")

    O depurador pausa no local em que você define o ponto de interrupção. A instrução em que a execução do depurador e do aplicativo está em pausa é indicada pela seta amarela. A linha com a chamada de função `doWork` ainda não foi executada.

    > [!TIP]
    > Se você tiver um ponto de interrupção em um loop ou recursão ou se tiver muitos pontos de interrupção que percorre com frequência, use um [ponto de interrupção condicional](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression) para garantir que seu código seja suspenso APENAS quando condições específicas forem atendidas. Um ponto de interrupção condicional pode economizar tempo e também tornar mais fácil depurar problemas difíceis de reproduzir.

## <a name="navigate-code"></a>Navegue pelos códigos

Há diferentes comandos para instruir o depurador a continuar. Mostramos um comando de navegação de código útil que é novo no Visual Studio 2017.

Enquanto estiver em pausa no ponto de interrupção, passe o mouse sobre a instrução `c1.AddLast(20)` até que o botão verde **Executar com um clique** ![Executar com um clique](../debugger/media/dbg-tour-run-to-click.png "RunToClick") seja exibido e, em seguida, pressione o botão **Executar com um clique**.

![Executar com um clique](../debugger/media/dbg-qs-run-to-click-csharp.png "Executar com um clique")

O aplicativo continua a execução, chamando `doWork`, e é pausado na linha de código em que você clicou no botão.

Comandos de teclado comuns usados para percorrer o código incluem **F10** e **F11**. Para obter mais instruções detalhadas, confira o [Guia do Iniciante](../debugger/getting-started-with-the-debugger.md).

## <a name="inspect-variables-in-a-datatip"></a>Inspecionar variáveis em uma datatip

1. Na linha de código atual (indicada pelo ponteiro de execução amarelo), passe o mouse sobre o objeto `c1` com o mouse para mostrar uma datatip.

    ![Exibir uma datatip](../debugger/media/dbg-qs-data-tip-csharp.png "Exibir uma datatip")

    A datatip mostra o valor atual da variável `c1` e permite que você inspecione suas propriedades. Ao depurar, se você vir um valor que não espera, provavelmente haverá um bug nas linhas de código anteriores ou de chamada. 

2. Expanda a datatip para examinar os valores de propriedade atuais do objeto `c1`.

3. Se desejar fixar a datatip para poder continuar vendo o valor de `c1` enquanto executa código, clique no pequeno ícone de marcador. (É possível mover a datatip fixada para uma localização conveniente.)

## <a name="edit-code-and-continue-debugging"></a>Editar o código e continuar a depuração

Se identificar uma alteração que deseja testar em seu código enquanto estiver no meio de uma sessão de depuração, será possível fazer isso também.

1. Clique na segunda instância de `c2.First.Value` e altere `c2.First.Value` para `c2.Last.Value`.

2. Pressione **F10** (ou **Depurar > Depuração Parcial**) algumas vezes para avançar o depurador e executar o código editado.

    ![Editar e continuar](../debugger/media/dbg-qs-edit-and-continue-csharp.gif "Editar e continuar")

    **F10** avança o depurador uma instrução por vez, mas depura parcialmente as funções, em vez de intervir nelas (o código que você ignora ainda é executado).

Para saber mais sobre como usar editar e continuar e sobre as limitações das funcionalidades, confira [Editar e Continuar](../debugger/edit-and-continue.md).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como iniciar o depurador, percorrer o código e inspecionar variáveis. Talvez você queira obter uma visão geral dos recursos do depurador, com links para mais informações.

> [!div class="nextstepaction"]
> [Tour dos recursos do depurador](../debugger/debugger-feature-tour.md)
