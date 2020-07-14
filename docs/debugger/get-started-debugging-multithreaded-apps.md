---
title: Aprenda a depurar aplicativos multithread
description: Depurar usando as pilhas paralelas e as janelas de inspeção paralelas no Visual Studio
ms.custom: ''
ms.date: 02/14/2020
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- multithreaded debugging, tutorial
- tutorials, multithreaded debugging
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 30fd29357ab8b42ea6a8baa6412f9ccf7eafed28
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350505"
---
# <a name="get-started-debugging-multithreaded-applications-c-visual-basic-c"></a>Introdução à depuração de aplicativos multithread (C#, Visual Basic, C++)

O Visual Studio fornece várias ferramentas e elementos de interface do usuário para ajudá-lo a depurar aplicativos multithread. Este tutorial mostra como usar marcadores de thread, a janela **pilhas paralelas** , a janela de **inspeção paralela** , pontos de interrupção condicionais e pontos de interrupção de filtro. A conclusão deste tutorial irá familiarizar você com os recursos do Visual Studio para depurar aplicativos multissegmentados.

Esses dois tópicos fornecem informações adicionais sobre como usar outras ferramentas de depuração multi-threaded:

- Para usar a barra de ferramentas do **local de depuração** e a janela **threads** , consulte [Walkthrough: Depurar um aplicativo multi-threaded](../debugger/how-to-use-the-threads-window.md).

- Para obter um exemplo que usa <xref:System.Threading.Tasks.Task> (código gerenciado) e o runtime de simultaneidade (C++), consulte [passo a passo: Depurando um aplicativo paralelo](../debugger/walkthrough-debugging-a-parallel-application.md). Para obter dicas gerais de depuração que se aplicam à maioria dos tipos de aplicativos multithread, leia esse tópico e este.

Primeiro, você precisará de um projeto de aplicativo multi-threaded. Há um exemplo a seguir.

## <a name="create-a-multithreaded-app-project"></a>Criar um projeto de aplicativo multithread

1. Abra o Visual Studio e crie um projeto.

   ::: moniker range=">=vs-2019"

   Se a janela iniciar não estiver aberta, escolha **arquivo** > **Iniciar janela**.

   Na janela iniciar, escolha **criar um novo projeto**.

   Na janela **Criar um novo projeto**, insira ou digite *console* na caixa de pesquisa. Em seguida, escolha **C#**, **C++** ou **Visual Basic** na lista idioma e, em seguida, escolha **Windows** na lista plataforma. 

   Depois de aplicar os filtros de idioma e plataforma, escolha o **aplicativo de console (.NET Core)** ou, para C++, modelo de **aplicativo de console** e escolha **Avançar**.

   > [!NOTE]
   > Se você não vir o modelo correto, vá para **ferramentas**  >  **obter ferramentas e recursos...**, que abre a instalador do Visual Studio. Escolha o desenvolvimento de **área de trabalho .net** ou **desenvolvimento de desktop com** carga de trabalho C++ e, em seguida, escolha **Modificar**.

   Na janela **configurar seu novo projeto** , digite ou insira *MyThreadWalkthroughApp* na caixa **nome do projeto** . Em seguida, escolha **criar**.

   ::: moniker-end
   ::: moniker range="vs-2017"
   Na barra de menus superior, escolha **arquivo**  >  **novo**  >  **projeto**. No painel esquerdo da caixa de diálogo **novo projeto** , escolha o seguinte:

   - Para um aplicativo C#, em **Visual C#**, escolha **Windows Desktop**e, no painel central, escolha **aplicativo de console (.NET Framework)**.
   - Para um aplicativo Visual Basic, em **Visual Basic**, escolha **área de trabalho do Windows**e, no painel central, escolha **aplicativo de console (.NET Framework)**.
   - Para um aplicativo C++, em **Visual C++**, escolha **Windows Desktop**, e, em seguida, escolha **aplicativo de console do Windows**.

   Se você não vir o **aplicativo de console (.NET Core)** ou, para C++, o modelo de projeto de **aplicativo de console** , vá para **ferramentas**  >  **obter ferramentas e recursos...**, que abre a instalador do Visual Studio. Escolha o desenvolvimento de **área de trabalho .net** ou **desenvolvimento de desktop com** carga de trabalho C++ e, em seguida, escolha **Modificar**.

   Em seguida, digite um nome como *MyThreadWalkthroughApp* e clique em **OK**.

   Selecione **OK**.
   ::: moniker-end

   Um novo projeto de console é exibido. Depois que o projeto tiver sido criado, um arquivo de origem será exibido. Dependendo do idioma escolhido, o arquivo de origem pode ser chamado *Program.cs*, *MyThreadWalkthroughApp. cpp*ou *Module1. vb*.

1. Exclua o código que aparece no arquivo de origem e substitua-o pela listagem de código de exemplo apropriada abaixo.

    ```csharp
    using System;
    using System.Threading;

    public class ServerClass
    {

        static int count = 0;
        // The method that will be called when the thread is started.
        public void InstanceMethod()
        {
            Console.WriteLine(
                "ServerClass.InstanceMethod is running on another thread.");

            int data = count++;
            // Pause for a moment to provide a delay to make
            // threads more apparent.
            Thread.Sleep(3000);
            Console.WriteLine(
                "The instance method called by the worker thread has ended. " + data);
        }
    }

    public class Simple
    {
        public static void Main()
        {
            for (int i = 0; i < 10; i++)
            {
                CreateThreads();
            }
        }
        public static void CreateThreads()
        {
            ServerClass serverObject = new ServerClass();

            Thread InstanceCaller = new Thread(new ThreadStart(serverObject.InstanceMethod));
            // Start the thread.
            InstanceCaller.Start();

            Console.WriteLine("The Main() thread calls this after "
                + "starting the new InstanceCaller thread.");

        }
    }
    ```

    ```C++
    // #include "pch.h" // Use with pre-compiled header
    #include <thread>
    #include <iostream>
    #include <vector>
    #include <string>

    int count = 0;

    void doSomeWork() {

        std::cout << "The doSomeWork function is running on another thread." << std::endl;
        int data = count++;
        // Pause for a moment to provide a delay to make
        // threads more apparent.
        std::this_thread::sleep_for(std::chrono::seconds(3));
        std::string str = std::to_string(data);
        std::cout << "The function called by the worker thread has ended. " + str<< std::endl;
    }

    int main() {
        std::vector<std::thread> threads;

        for (int i = 0; i < 10; ++i) {

            threads.push_back(std::thread(doSomeWork));
            std::cout << "The Main() thread calls this after starting the new thread" << std::endl;
    }

    for (auto& thread : threads) {
        thread.join();
    }

    return 0;
    }
    ```

    ```VB
    Imports System.Threading

    Public Class ServerClass
        ' The method that will be called when the thread is started.
        Public count = 0
        Public Sub InstanceMethod()
            Console.WriteLine(
                    "ServerClass.InstanceMethod is running on another thread.")

            Dim data = count + 1
            ' Pause for a moment to provide a delay to make
            ' threads more apparent.
            Thread.Sleep(3000)
            Console.WriteLine(
                    "The instance method called by the worker thread has ended. " + data)
        End Sub

    End Class

    Public Class Simple

        Public Shared Sub Main()

            Dim ts As New ThreadStarter
            For index = 1 To 10
                ts.CreateThreads()
            Next

        End Sub

    End Class
    Public Class ThreadStarter
        Public Sub CreateThreads()
            Dim serverObject As New ServerClass()

            ' Create the thread object, passing in the
            ' serverObject.InstanceMethod method using a
            ' ThreadStart delegate.
            Dim InstanceCaller As New Thread(AddressOf serverObject.InstanceMethod)

            ' Start the thread.
            InstanceCaller.Start()

            Console.WriteLine("The Main() thread calls this after " _
                        + "starting the new InstanceCaller thread.")

        End Sub
    End Class
    ```

1. No menu **arquivo** , selecione **salvar tudo**.

1. (Somente Visual Basic) Em Gerenciador de Soluções (painel direito), clique com o botão direito do mouse no nó do projeto, escolha **Propriedades**. Na guia **aplicativo** , altere o **objeto de inicialização** para **simples**.

## <a name="debug-the-multithreaded-app"></a>Depurar o aplicativo multi-threaded

1. No editor de código-fonte, procure um dos seguintes trechos de código:

    ```csharp
    Thread.Sleep(3000);
    Console.WriteLine();
    ```

    ```C++
    std::this_thread::sleep_for(std::chrono::seconds(3));
    std::cout << "The function called by the worker thread has ended." << std::endl;
    ```

    ```VB
    Thread.Sleep(3000)
    Console.WriteLine()
    ```

1. Clique com o botão esquerdo do mouse na medianiz esquerdo da `Thread.Sleep` `std::this_thread::sleep_for` instrução ou para inserir um novo ponto de interrupção.

    Na medianiz, um círculo vermelho indica que um ponto de interrupção está definido neste local.

2. No menu **depurar** , selecione **Iniciar Depuração** (**F5**).

    O Visual Studio cria a solução, o aplicativo começa a ser executado com o depurador anexado e, em seguida, o aplicativo é interrompido no ponto de interrupção.

3. No editor de código-fonte, localize a linha que contém o ponto de interrupção.

### <a name="discover-the-thread-marker"></a><a name="ShowThreadsInSource"></a>Descobrir o marcador de thread  

1. Na barra de ferramentas depurar, selecione o botão **Mostrar threads no código-fonte** ![Mostrar threads na origem](../debugger/media/dbg-multithreaded-show-threads.png "ThreadMarker").

2. Pressione **F11** uma vez para avançar o depurador de uma linha de código.

3. Examine a medianiz no lado esquerdo da janela. Nessa linha, você verá um ![marcador](../debugger/media/dbg-thread-marker.png "ThreadMarker") de thread com ícone de *marcador de thread* que se assemelha a dois threads trançados. O marcador de thread indica que um thread está parado nesse local.

    Um marcador de thread pode ser parcialmente escondido por um ponto de interrupção.

4. Passe o ponteiro sobre o marcador de thread. Um DataTip é exibido informando o nome e o número da ID do thread para cada thread interrompido. Nesse caso, o nome é provavelmente `<noname>` .

5. Selecione o marcador de thread para ver as opções disponíveis no menu de atalho.

### <a name="view-the-thread-locations"></a><a name="ParallelStacks"></a>Exibir os locais de thread

Na janela **pilhas paralelas** , você pode alternar entre uma exibição de threads e a exibição de tarefas (para a programação baseada em tarefas) e pode exibir informações da pilha de chamadas para cada thread. Nesse aplicativo, podemos usar a exibição threads.

1. Abra a janela **pilhas paralelas** escolhendo **depurar**  >  **Windows**  >  **pilhas paralelas**do Windows. Você verá algo semelhante ao seguinte. As informações exatas serão diferentes dependendo do local atual de cada thread, do hardware e da linguagem de programação.

    ![Janela pilhas paralelas](../debugger/media/dbg-multithreaded-parallel-stacks.png "ParallelStacksWindow")

    Neste exemplo, da esquerda para a direita, vemos essas informações para o código gerenciado:

    - O thread principal (lado esquerdo) parou em `Thread.Start` , em que o ponto de interrupção é indicado pelo ![marcador de thread](../debugger/media/dbg-thread-marker.png "ThreadMarker")ícone de marcador de thread.
    - Dois threads inseriram o `ServerClass.InstanceMethod` , um dos quais é o thread atual (seta amarela), enquanto o outro thread foi interrompido no `Thread.Sleep` .
    - Um novo thread (à direita) também está sendo iniciado, mas é interrompido `ThreadHelper.ThreadStart` .

2. Clique com o botão direito do mouse em entradas na janela **pilhas paralelas** para ver as opções disponíveis no menu de atalho.

    Você pode executar várias ações a partir desses menus de clique com o botão direito do mouse, mas, para este tutorial, mostraremos mais desses detalhes na janela de **inspeção paralela** (próximas seções).

    > [!NOTE]
    > Para ver um modo de exibição de lista com informações sobre cada thread, use a janela **threads** em vez disso. Consulte [Walkthrough: Depurar um aplicativo multi-threaded](../debugger/how-to-use-the-threads-window.md).

### <a name="set-a-watch-on-a-variable"></a>Definir uma inspeção em uma variável

1. Abra a janela de **inspeção paralela** selecionando **depurar**  >  **Windows**  >  **Parallel Watch**  >  **paralela Watch 1**.

2. Selecione a célula onde você vê o `<Add Watch>` texto (ou a célula de cabeçalho vazia na 4ª coluna) e Enter `data` .

    Os valores da variável de dados para cada thread aparecem na janela.

3. Selecione a célula onde você vê o `<Add Watch>` texto (ou a célula de cabeçalho vazia na quinta coluna) e digite `count` .

    Os valores da `count` variável para cada thread aparecem na janela. Se você ainda não vir essa quantidade de informações, tente pressionar **F11** algumas vezes para avançar a execução dos threads no depurador.

    ![Janela de inspeção paralela](../debugger/media/dbg-multithreaded-parallel-watch.png "ParallelWatchWindow")

4. Clique com o botão direito do mouse em uma das linhas na janela para ver as opções disponíveis.

### <a name="flag-and-unflag-threads"></a>Sinalizar e remover sinalizador de threads
Você pode sinalizar threads para manter o controle de threads importantes e ignorar os outros threads.

1. Na janela de **inspeção paralela** , mantenha pressionada a tecla **Shift** e selecione várias linhas.

2. Clique com o botão direito do mouse e selecione **sinalizador**.

    Todos os threads selecionados são sinalizados. Agora, você pode filtrar para mostrar apenas threads sinalizados.

3. Na janela de **inspeção paralela** , selecione o botão **Mostrar somente threads sinalizados** ![Mostrar threads sinalizados](../debugger/media/dbg-threads-show-flagged.png "ThreadMarker").

    Somente os threads sinalizados aparecem na lista.

    > [!TIP]
    > Depois de sinalizar alguns threads, você pode clicar com o botão direito do mouse em uma linha de código no editor de códigos e escolher **executar threads sinalizados para o cursor**. Verifique se você escolheu o código que todos os threads sinalizados atingirão. O Visual Studio pausará threads na linha de código selecionada, facilitando o controle da ordem de execução [congelando e descongelando threads](#bkmk_freeze).

4. Selecione o botão **Mostrar somente threads sinalizados** novamente para alternar novamente para **Mostrar todos os modos de threads** .

5. Para remover o sinalizador de threads, clique com o botão direito do mouse em um ou mais threads sinalizados na janela de **inspeção paralela** e selecione **remover sinalizador**.

### <a name="freeze-and-thaw-thread-execution"></a><a name="bkmk_freeze"></a>Congelar e descongelar a execução do thread

> [!TIP]
> Você pode congelar e descongelar (suspender e retomar) threads para controlar a ordem em que os threads executam o trabalho. Isso pode ajudá-lo a resolver problemas de simultaneidade, como deadlocks e condições de corrida.

1. Na janela de **inspeção paralela** , com todas as linhas selecionadas, clique com o botão direito do mouse e selecione **congelar**.

    Na segunda coluna, um ícone de pausa é exibido para cada linha. O ícone de pausa indica que o thread está congelado.

2. Desmarque todas as outras linhas selecionando apenas uma linha.

3. Clique com o botão direito do mouse em uma linha e selecione **descongelar**.

    O ícone de pausa desaparece nessa linha, indicando que o thread não está mais congelado.

4. Alterne para o editor de código e pressione **F11**. Somente o thread descongelado é executado.

    O aplicativo também pode instanciar alguns novos threads. Os novos threads não são sinalizados e não são congelados.

### <a name="follow-a-single-thread-with-conditional-breakpoints"></a><a name="bkmk_follow_a_thread"></a>Seguir um único thread com pontos de interrupção condicionais

Pode ser útil seguir a execução de um único thread no depurador. Uma maneira de fazer isso é congelar threads nos quais você não está interessado. Em alguns cenários, talvez seja necessário seguir um único thread sem congelar outros threads, por exemplo, para reproduzir um bug específico. Para seguir um thread sem congelar outros threads, você deve evitar dividir o código, exceto no thread no qual você está interessado. Você pode fazer isso definindo um [ponto de interrupção condicional](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression).

Você pode definir pontos de interrupção em condições diferentes, como o nome do thread ou a ID do thread. Pode ser útil definir a condição nos dados que você sabe que é exclusiva para cada thread. Esse é um cenário comum de depuração, no qual você está mais interessado em algum valor de dados específico do que em qualquer thread específico.

1. Clique com o botão direito do mouse no ponto de interrupção criado anteriormente e selecione **condições**.

2. Na janela **configurações de ponto de interrupção** , insira `data == 5` para a expressão condicional.

    ![Ponto de interrupção condicional](../debugger/media/dbg-multithreaded-conditional-breakpoint.png "ConditionalBreakpoint")

    > [!TIP]
    > Se você estiver mais interessado em um thread específico, use um nome de thread ou ID de thread para a condição. Para fazer isso na janela **configurações de ponto de interrupção** , selecione **Filtrar** em vez de **expressão condicional**e siga as dicas de filtro. Talvez você queira nomear seus threads no código do aplicativo, pois as IDs de threads são alteradas quando você reinicia o depurador.

3. Feche a janela **configurações de ponto de interrupção** .

4. Selecione o botão reiniciar ![aplicativo](../debugger/media/dbg-tour-restart.png "RestartApp") de reinicialização para reiniciar a sessão de depuração.

    Você irá dividir o código no thread em que o valor da variável de dados é 5. Na janela de **inspeção paralela** , procure a seta amarela indicando o contexto do depurador atual.

5. Agora, você pode passar pelo código (**F10**) e entrar em código (**F11**) e seguir a execução do único thread.

    Desde que a condição de ponto de interrupção seja exclusiva para o thread e o depurador não atinja nenhum outro ponto de interrupção em outros threads (talvez seja necessário desabilitá-los), você pode passar pelo código e entrar em código sem alternar para outros threads.

    > [!NOTE]
    > Quando você avança o depurador, todos os threads serão executados. No entanto, o depurador não interromperá o código em outros threads, a menos que um dos outros threads atinja um ponto de interrupção.

## <a name="see-also"></a>Veja também

- [Depurar aplicativos multissegmentados](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [Como mudar para outro thread durante a depuração](../debugger/how-to-switch-to-another-thread-while-debugging.md)
- [Como: usar a janela de pilha paralela](../debugger/using-the-parallel-stacks-window.md)
- [Como usar a janela Inspeção Paralela](../debugger/how-to-use-the-parallel-watch-window.md)