---
title: Saiba como depurar aplicativos multithread
description: Depurar usando as janelas de pilhas paralelas e inspeção paralela no Visual Studio
ms.custom: H1HackMay2017
ms.date: 11/16/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- multithreaded debugging, tutorial
- tutorials, multithreaded debugging
ms.assetid: 62df746b-b0f6-4df4-83cf-b1d9d2e72833
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2a6ded522a917dd7207da7731850303535e19fdb
ms.sourcegitcommit: 54c65f81a138fc1e8ff1826f7bd9dcec710618cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51948979"
---
# <a name="get-started-debugging-multithreaded-applications"></a>Introdução ao depurar aplicativos multithread
Visual Studio fornece várias ferramentas e os elementos de interface do usuário para ajudá-lo a depurar aplicativos multi-threaded. Este tutorial mostra como usar marcadores de thread, o **pilhas paralelas** janela, o **inspeção paralela** janela pontos de interrupção condicionais e pontos de interrupção de filtro. Concluir este tutorial você se familiarizará com recursos do Visual Studio para depurar aplicativos multithread.

| | |
|---------|---------|
| ![ícone de câmera para vídeo](../install/media/video-icon.png "Assistir a um vídeo") | [Assista a um vídeo](https://mva.microsoft.com/en-US/training-courses-embed/getting-started-with-visual-studio-2017-17798/Debugging-Multi-threaded-Apps-in-Visual-Studio-2017-MoZPKMD6D_111787171) sobre depuração com multithread que mostra etapas semelhantes. |

Esses dois tópicos fornecem informações adicionais sobre como usar outras ferramentas de depuração multithread:

- Para usar o **local de depuração** barra de ferramentas e o **Threads** janela, consulte [passo a passo: depurar um aplicativo multi-threaded](../debugger/how-to-use-the-threads-window.md).

- Para obter um exemplo que usa <xref:System.Threading.Tasks.Task> (código gerenciado) e o tempo de execução de simultaneidade (C++), consulte [passo a passo: depurar um aplicativo paralelo](../debugger/walkthrough-debugging-a-parallel-application.md). Para dicas de depuração gerais que se aplicam a tipos de aplicativos multithread mais, leia esse tópico e esta.
  
Você precisará primeiro um projeto de aplicativo multithread. Segue um exemplo.  
  
## <a name="create-a-multithreaded-app-project"></a>Criar um projeto de aplicativo multithread  
  
1.  No menu **Arquivo**, selecione **Novo** > **Projeto**.  
  
     A caixa de diálogo **Novo Projeto** é exibida.  
  
2.  Selecione um idioma: **Visual C#** , **Visual C++**, ou **Visual Basic**.  
  
3.  Sob **área de trabalho do Windows**, escolha **aplicativo de Console**.  
  
4.  No **nome** , insira MyThreadWalkthroughApp.  
  
5.  Selecione **OK**.  
  
     Um novo projeto de console é exibido. Depois que o projeto tiver sido criado, um arquivo de origem é exibido. Dependendo da linguagem escolhida, o arquivo de origem pode ser chamado *Program.cs*, *mythreadwalkthroughapp. cpp*, ou *Module1.vb*.  
  
6.  Exclua o código que aparece no arquivo de origem e substitua-o com o código de exemplo apropriado listando abaixo.

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
                "The instance method called by the worker thread has ended.");
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
    #include "stdafx.h"
    #include <thread>
    #include <iostream>
    #include <vector>

    using namespace;

    int count = 0;

    void doSomeWork() {

        cout << "The doSomeWork function is running on another thread." << endl;
        int data = count++;
        // Pause for a moment to provide a delay to make
        // threads more apparent.
        this_thread::sleep_for(chrono::seconds(3));
        cout << "The function called by the worker thread has ended." << endl;
    }

    int main() {
        vector<thread> threads;

        for (int i = 0; i < 10; ++i) {

            threads.push_back(thread(doSomeWork));
            cout << "The Main() thread calls this after starting the new thread" << endl;
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
                    "The instance method called by the worker thread has ended.")
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
  
7.  Sobre o **arquivo** menu, selecione **Salvar tudo**.  
  
## <a name="debug-the-multithreaded-app"></a>Depurar o aplicativo com multithread  
  
1. No editor de código fonte, procure por um dos seguintes trechos de código: 
  
    ```csharp  
    Thread.Sleep(3000);  
    Console.WriteLine();  
    ```  
  
    ```C++  
    this_thread::sleep_for(chrono::seconds(3));
    cout << "The function called by the worker thread has ended." << endl; 
    ```  

    ```VB
    Thread.Sleep(3000)
    Console.WriteLine()
    ```

1. Botão esquerdo do mouse na medianiz esquerda do `Thread.Sleep` ou `this_thread::sleep_for` instrução para inserir um novo ponto de interrupção.  
  
    Na medianiz, um círculo vermelho indica que um ponto de interrupção está definido neste local. 
  
2. Sobre o **Debug** menu, selecione **iniciar depuração** (**F5**).  
  
    Visual Studio compila a solução, o aplicativo começa a ser executado com o depurador anexado e, em seguida, o aplicativo for interrompida no ponto de interrupção.  
  
3. No editor de código fonte, localize a linha que contém o ponto de interrupção.
  
### <a name="ShowThreadsInSource"></a>Descobrir o marcador de thread  

1.  Na barra de ferramentas de depuração, selecione o **Mostrar Threads em origem** botão ![Mostrar Threads em origem](../debugger/media/dbg-multithreaded-show-threads.png "ThreadMarker").

2. Pressione **F11** uma vez para Avançar a linha de um do depurador de código.
  
3.  Examine a medianiz no lado esquerdo da janela. Nessa linha, você verá uma *marcador de thread* ícone ![marcador de Thread](../debugger/media/dbg-thread-marker.png "ThreadMarker") que se parece com dois threads trançados. O marcador de thread indica que um thread está parado nesse local.

    Um marcador de thread pode ser parcialmente ocultos, um ponto de interrupção. 
  
4.  Passe o ponteiro sobre o marcador de thread. Um DataTip é exibido informando que o número de ID de nome e o thread para cada thread parado. Nesse caso, o nome é provavelmente `<noname>`. 
  
5.  Selecione o marcador de thread para ver as opções disponíveis no menu de atalho.
    
### <a name="ParallelStacks"></a>Exibir os locais de thread

No **pilhas paralelas** janela, você pode alternar entre um modo de exibição de Threads e (para a programação baseada em tarefa) o modo de exibição de tarefas e você pode exibir informações de pilha de chamada para cada thread. Neste aplicativo, podemos usar o modo de exibição de Threads.

1. Abra o **pilhas paralelas** janela escolhendo **Debug** > **Windows** > **pilhas paralelas**. Você deverá ver algo semelhante ao seguinte. As informações exatas variarão dependendo do local atual de cada thread, o hardware e a linguagem de programação.

    ![Janela de pilhas paralelas](../debugger/media/dbg-multithreaded-parallel-stacks.png "ParallelStacksWindow")

    Neste exemplo, da esquerda para direita, podemos ver essas informações para código gerenciado:
    
    - O thread principal (lado esquerdo) foi interrompido no `Thread.Start`, onde o ponto de interrupção é indicado pelo ícone de marcador de thread ![marcador de Thread](../debugger/media/dbg-thread-marker.png "ThreadMarker").
    - Dois threads inseriu a `ServerClass.InstanceMethod`, um dos quais é o thread atual (seta amarela), enquanto o outro thread foi interrompido no `Thread.Sleep`.
    - Um novo thread (à direita) também está sendo iniciado, mas é interrompido no `ThreadHelper.ThreadStart`.

2.  Clique com botão direito entradas na **pilhas paralelas** janela para ver as opções disponíveis no menu de atalho.

    Você pode executar várias ações desses menus de atalho, mas para este tutorial, mostraremos mais desses detalhes na **inspeção paralela** janela (próximas seções).

    > [!NOTE]
    > Para ver uma lista para exibir informações sobre cada thread, use o **Threads** janela em vez disso. Ver [instruções passo a passo: depurar um aplicativo multi-threaded](../debugger/how-to-use-the-threads-window.md).

### <a name="set-a-watch-on-a-variable"></a>Definir uma inspeção em uma variável

1. Abra o **inspeção paralela** janela selecionando **Debug** > **Windows** > **inspeção paralela**  >  **Inspeção 1 paralela**.

2. Selecione a célula em que você consulte os `<Add Watch>` texto (ou a célula de cabeçalho vazio na coluna 4º) e insira `data`.

    Os valores para a variável de dados para cada thread aparecem na janela.

3. Selecione a célula em que você consulte os `<Add Watch>` texto (ou a célula de cabeçalho vazio na coluna 5ª) e insira `count`.

    Os valores para o `count` variável para cada thread aparecem na janela. Se você não vir ainda muitas informações, tente pressionar **F11** algumas vezes para Avançar a execução dos threads no depurador.

    ![Janela de inspeção em paralelo](../debugger/media/dbg-multithreaded-parallel-watch.png "ParallelWatchWindow")

4. Clique duas vezes em uma das linhas na janela para ver as opções disponíveis.

### <a name="flag-and-unflag-threads"></a>Sinalizar e remover sinalizador de threads  
Você pode sinalizar os threads para manter o controle de threads importantes e ignorar os outros threads.  
  
1. No **inspeção paralela** janela, mantenha pressionada a **Shift** de chave e selecionar várias linhas.

2. Clique com botão direito e selecione **sinalizador**.

    Todos os threads sinalizados. Agora, você pode filtrar para mostrar somente threads sinalizados.
  
3.  No **inspeção paralela** janela, selecione a **Mostrar somente Threads sinalizados** botão ![Mostrar Threads sinalizados](../debugger/media/dbg-threads-show-flagged.png "ThreadMarker").  
  
    Apenas os threads sinalizados aparecem na lista.

    > [!TIP]
    > Depois que você sinalizou alguns threads, pode ser uma linha de código no editor de códigos com o botão direito e escolha **executar Threads sinalizados Cursor**. Certifique-se de escolher entrará em código que todos os threads sinalizados. Visual Studio fará uma pausa segmentos na linha selecionada de código, tornando mais fácil controlar a ordem de execução pelo [congelando e Descongelando threads](#bkmk_freeze).

4.  Selecione o **Mostrar somente Threads sinalizados** botão novamente para voltar ao **Mostrar todos os Threads** modo.
    
5. Para remover a sinalização de threads, clique com botão direito um ou mais threads sinalizados na **inspeção paralela** janela e selecione **Remover sinalização**.

### <a name="bkmk_freeze"></a> Congelar e descongelar a execução de thread 

> [!TIP]
> Você pode congelar e descongelar (suspender e retomar) threads para controlar a ordem na qual threads executam o trabalho. Isso pode ajudá-lo a resolver problemas de simultaneidade, como deadlocks e condições de corrida.
   
1.  No **inspeção paralela** janela, com todas as linhas selecionadas, clique com botão direito e selecione **congelar**.

    Na segunda coluna, um ícone de pausa é exibido para cada linha. O ícone de pausa indica que o thread está congelado.

2.  Desmarque todas as outras linhas, selecionando apenas uma linha.

3.  Uma linha com o botão direito e selecione **descongelar**.

    O ícone de pausa desaparece nesta linha, que indica que o thread não está congelado.

4.  Alterne para o editor de código e pressione **F11**. Somente as execuções de thread não congeladas.

    O aplicativo também pode criar uma instância de alguns novos threads. Quaisquer novos threads são sem sinalização e não estão congelados.

### <a name="bkmk_follow_a_thread"></a> Execute um único thread com pontos de interrupção condicionais

Ele pode ser útil acompanhar a execução de um único thread no depurador. É uma maneira de fazer isso ao congelar threads que não está interessado. Em alguns cenários você precisa seguir um único thread sem congelamento de outros threads, por exemplo, para reproduzir um bug específico. Para seguir um thread sem congelamento de outros threads, você deve evitar a interrupção no código, exceto no thread em que você está interessado. Você pode fazer isso definindo uma [ponto de interrupção condicional](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression).

Você pode definir pontos de interrupção em diferentes condições, como o nome do thread ou a ID do thread. Pode ser útil é definir a condição nos dados que você sabe que é exclusivo para cada thread. Isso é um cenário comum de depuração, no qual você está mais interessado em alguns valores de dados específico que em qualquer thread específico.

1. O ponto de interrupção que você criou anteriormente com o botão direito e selecione **condições**.

2. No **configurações de ponto de interrupção** janela, digite `data == 5` para a expressão condicional.

    ![Ponto de interrupção condicional](../debugger/media/dbg-multithreaded-conditional-breakpoint.png "ConditionalBreakpoint")

    > [!TIP]
    > Se você estiver mais interessado em um thread específico, use um nome de thread ou a ID do thread para a condição. Para fazer isso na **configurações de ponto de interrupção** janela, selecione **filtro** em vez de **expressão condicional**e siga as dicas de filtro. Você talvez queira nomear seus threads no código do aplicativo, conforme as IDs de threads mudam quando você reiniciar o depurador.

3. Fechar o **configurações de ponto de interrupção** janela.

4. Selecione a reinicialização ![aplicativo reinicie](../debugger/media/dbg-tour-restart.png "RestartApp") botão reiniciar a sessão de depuração.

    Você vai entrar no código no thread em que o valor da variável de dados é 5. No **inspeção paralela** janela, procure a seta amarela indicando o contexto atual do depurador.

5. Agora, você poderá passar por código (**F10**) e intervir no código (**F11**) e siga a execução de thread único.

    Desde que a condição de ponto de interrupção é exclusiva para o thread e o depurador não usar quaisquer outros pontos de interrupção em outros threads (talvez seja necessário desabilitá-las), você pode step over no código e intervir no código sem alternar para outros threads.

    > [!NOTE]
    > Quando você avança o depurador, todos os threads serão executados. No entanto, o depurador não quebre em código em outros threads, a menos que um dos outros threads atinge um ponto de interrupção. 
  
## <a name="see-also"></a>Consulte também  
[Depurar aplicativos multi-threaded](../debugger/debug-multithreaded-applications-in-visual-studio.md)  
[Como mudar para outro thread durante a depuração](../debugger/how-to-switch-to-another-thread-while-debugging.md)  
[Como: usar a janela de pilha paralela](../debugger/using-the-parallel-stacks-window.md)  
[Como usar a janela Inspeção Paralela](../debugger/how-to-use-the-parallel-watch-window.md)  
