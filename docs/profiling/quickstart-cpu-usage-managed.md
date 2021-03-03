---
title: Analisar dados de uso da CPU (C#, Visual Basic)
description: Medir o desempenho do aplicativo em C# e Visual Basic usando a ferramenta de diagnóstico de Uso da CPU
ms.custom: mvc
ms.date: 02/14/2020
ms.topic: quickstart
helpviewer_keywords:
- Profiling Tools, quick start
- Diagnostics Tools, CPU Usage
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 7fc8eeccdb020d07ff48965d9eb3d5df1dafa7da
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683540"
---
# <a name="quickstart-analyze-cpu-usage-data-in-visual-studio-c-visual-basic"></a>Início rápido: analisar dados de uso da CPU no Visual Studio (C#, Visual Basic)

O Visual Studio fornece muitos recursos poderosos para ajudar a analisar problemas de desempenho em seu aplicativo. Este tópico fornece uma maneira rápida de conhecer alguns dos recursos básicos. Aqui, vamos examinar a ferramenta para identificar os gargalos de desempenho devido ao alto uso da CPU. As Ferramentas de Diagnóstico têm suporte para desenvolvimento de .NET no Visual Studio, incluindo o ASP.NET e para desenvolvimento nativo/C++.

O Hub de diagnósticos oferece várias outras opções para executar e gerenciar sua sessão de diagnóstico. Se a ferramenta **Uso de CPU** descrita aqui não fornecer os dados que você precisa, as [outras ferramentas de criação de perfil](../profiling/profiling-feature-tour.md) fornecerão diferentes tipos de informações que poderão ser úteis. Em muitos casos, o gargalo de desempenho do aplicativo pode ser causado por algo que não seja a CPU, como memória, interface do usuário de renderização ou tempo de solicitação de rede. O criador de perfil de desempenho oferece muitas outras opções para registrar e analisar esse tipo de dados. [PerfTips](../profiling/perftips.md), outra ferramenta de criação de perfil integrada ao depurador, também permite percorrer o código e identificar quanto tempo as funções específicas ou os blocos de código são concluídos.

O Windows 8 ou posterior é necessário para executar ferramentas de criação de perfil com o depurador (janela **Ferramentas de Diagnóstico**). No Windows 7 e posteriores, você pode usar a ferramenta post-mortem, o [Criador de Perfil de Desempenho](../profiling/profiling-feature-tour.md).

## <a name="create-a-project"></a>Criar um projeto

1. Abra o Visual Studio e crie o projeto.

   ::: moniker range="vs-2017"
   Na barra de menus superior, escolha **arquivo** > **novo** > **projeto**.

   Na caixa de diálogo **novo projeto** no painel esquerdo, expanda **C#** ou **Visual Basic** e, em seguida, escolha **.NET Core**. No painel central, escolha **Aplicativo de Console (.NET Core)**. Em seguida, nomeie o projeto *MyProfilerApp*.

   Se você não vir o modelo de projeto do **Aplicativo de Console (.NET Core)**, escolha o link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto**. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento multiplaforma do .NET Core** e, em seguida, selecione **Modificar**.
   ::: moniker-end
   ::: moniker range="vs-2019"
   Se a janela iniciar não estiver aberta, escolha **arquivo** > **Iniciar janela**.

   Na janela iniciar, escolha **criar um novo projeto**.

   Na janela **Criar um novo projeto**, insira ou digite *console* na caixa de pesquisa. Em seguida, escolha **C#** ou **Visual Basic** na lista idioma e, em seguida, escolha **Windows** na lista plataforma.

   Depois de aplicar os filtros de idioma e plataforma, escolha o modelo de **aplicativo de console** para .NET Core e, em seguida, escolha **Avançar**.

   > [!NOTE]
   > Se você não vir o modelo de **aplicativo de console** , poderá instalá-lo na janela **criar um novo projeto** . Na mensagem **Não encontrou o que precisa?**, escolha o link **Instalar mais ferramentas e recursos**. Em seguida, no Instalador do Visual Studio, escolha a carga de trabalho de **desenvolvimento multiplataforma do .NET Core**.

   Na janela **configurar seu novo projeto** , digite ou insira *MyProfilerApp* na caixa **nome do projeto** . Em seguida, escolha **Avançar**.

   Escolha a estrutura de destino recomendada (.NET Core 3,1) ou .NET 5 e, em seguida, escolha **criar**.

   ::: moniker-end

   O Visual Studio abre seu novo projeto.

2. Abra *Program.cs* e substitua todo o código pelo código a seguir:

    ```csharp
    using System;
    using System.Threading;
    public class ServerClass
    {
        const int MIN_ITERATIONS = int.MaxValue / 1000;
        const int MAX_ITERATIONS = MIN_ITERATIONS + 10000;

        long m_totalIterations = 0;
        readonly object m_totalItersLock = new object();
        // The method that will be called when the thread is started.
        public void DoWork()
        {
            Console.WriteLine(
                "ServerClass.InstanceMethod is running on another thread.");

            var x = GetNumber();
        }

        private int GetNumber()
        {
            var rand = new Random();
            var iters = rand.Next(MIN_ITERATIONS, MAX_ITERATIONS);
            var result = 0;
            lock (m_totalItersLock)
            {
                m_totalIterations += iters;
            }
            // we're just spinning here
            // and using Random to frustrate compiler optimizations
            for (var i = 0; i < iters; i++)
            {
                result = rand.Next();
            }
            return result;
        }
    }

    public class Simple
    {
        public static void Main()
        {
            for (int i = 0; i < 200; i++)
            {
                CreateThreads();
            }
        }
        public static void CreateThreads()
        {
            ServerClass serverObject = new ServerClass();

            Thread InstanceCaller = new Thread(new ThreadStart(serverObject.DoWork));
            // Start the thread.
            InstanceCaller.Start();

            Console.WriteLine("The Main() thread calls this after "
                + "starting the new InstanceCaller thread.");

        }
    }
    ```

    ```vb
    Imports System
    Imports System.Threading

    Namespace MyProfilerApp
        Public Class ServerClass
            Const MIN_ITERATIONS As Integer = Integer.MaxValue / 1000
            Const MAX_ITERATIONS As Integer = MIN_ITERATIONS + 10000

            Private m_totalIterations As Long = 0
            ReadOnly m_totalItersLock As New Object()
            ' The method that will be called when the thread is started.
            Public Sub DoWork()
                Console.WriteLine("ServerClass.InstanceMethod is running on another thread.")

                Dim x = GetNumber()
            End Sub

            Private Function GetNumber() As Integer
                Dim rand = New Random()
                Dim iters = rand.[Next](MIN_ITERATIONS, MAX_ITERATIONS)
                Dim result = 0
                SyncLock m_totalItersLock
                    m_totalIterations += iters
                End SyncLock
                ' we're just spinning here
                ' and using Random to frustrate compiler optimizations
                For i As Integer = 0 To iters - 1
                    result = rand.[Next]()
                Next
                Return result
            End Function
        End Class

        Public Class Simple
            Public Shared Sub Main()
                For i As Integer = 0 To 199
                    CreateThreads()
                Next
            End Sub
            Public Shared Sub CreateThreads()
                Dim serverObject As New ServerClass()

                Dim InstanceCaller As New Thread(New ThreadStart(AddressOf serverObject.DoWork))
                ' Start the thread.
                InstanceCaller.Start()

                Console.WriteLine("The Main() thread calls this after " + "starting the new InstanceCaller thread.")

            End Sub
        End Class
    End Namespace
    ```

    > [!NOTE]
    > Em Visual Basic, certifique-se de que o objeto de inicialização está definido como `Sub Main` (**Propriedades** do  >  **aplicativo**  >  **Startup object**).

## <a name="step-1-collect-profiling-data"></a>Etapa 1: Coletar dados de criação de perfil

1. Primeiro, defina um ponto de interrupção em seu aplicativo nesta linha de código na função `Main`:

    `for (int i = 0; i < 200; i++)`

    ou, para o Visual Basic:

    `For i As Integer = 0 To 199`

    Defina um ponto de interrupção clicando na medianiz à esquerda da linha de código.

2. Em seguida, defina um segundo ponto de interrupção no colchete de fechamento no final da função `Main`:

     ![Definir pontos de interrupção para criação de perfil](../profiling/media/quickstart-cpu-usage-breakpoints.png "Definir pontos de interrupção para criação de perfil")

    Definindo dois pontos de interrupção, você pode limitar a coleta de dados às partes do código que deseja analisar.

3. A janela **Ferramentas de Diagnóstico** já fica visível, a menos que tenha sido desativada. Para exibir a janela novamente, clique em **depurar**  >  **janelas**  >  **Mostrar ferramentas de diagnóstico**.

4. Clique em **depurar**  >  **Iniciar Depuração** (ou **Iniciar** na barra de ferramentas ou **F5**).

     Quando o aplicativo terminar de ser carregado, a exibição **Resumo** das Ferramentas de Diagnóstico será exibida.

5. Enquanto o depurador estiver em pausa, habilite a coleta dos dados de Uso da CPU escolhendo **Registrar perfil da CPU** e abra a guia **Uso da CPU**.

     ![Habilitar criação de perfil de CPU de Ferramentas de Diagnóstico](../profiling/media/quickstart-cpu-usage-summary.png "Habilitar criação de perfil de CPU de Ferramentas de Diagnóstico")

     Quando a coleta de dados estiver habilitada, o botão de registro exibe um círculo vermelho.

     Quando você escolhe **Registrar perfil de CPU**, o Visual Studio começará a gravar as funções e quanto tempo elas levam para serem executadas, fornecendo também um gráfico de linha do tempo que você pode usar para se concentrar em segmentos específicos da sessão de amostragem. Você só pode exibir os dados coletados quando seu aplicativo é interrompido no ponto de interrupção.

6. Pressione **F5** para executar o aplicativo até o segundo ponto de interrupção.

     Agora, você tem dados de desempenho do aplicativo especificamente para a região do código que é executada entre os dois pontos de interrupção.

     O criador de perfil começa a preparar os dados de thread. Aguarde sua conclusão.

     A ferramenta de Uso de CPU exibe o relatório na guia **Uso da CPU**.

     Neste ponto, você pode começar a analisar os dados.

## <a name="step-2-analyze-cpu-usage-data"></a>Etapa 2: Analisar os dados de uso de CPU

Recomendamos que você comece a analisar os dados examinando a lista de funções em Uso da CPU, identificando as funções que fazem a maior parte do trabalho e, em seguida, fazendo uma análise mais detalhada de cada uma.

1. Na lista de funções, examine as funções que fazem a maior parte do trabalho.

     ![Guia uso de CPU das ferramentas de diagnóstico](../profiling/media/quickstart-cpu-usage-cpu.png "DiagToolsCPUUsageTab")

    > [!TIP]
    > As funções são listadas em ordem, começando com as que fazem a maior parte do trabalho (elas não ficam na ordem de chamada). Isso ajuda a identificar rapidamente as funções com execução mais longa.

2. Na lista de função, clique duas vezes na função `ServerClass::GetNumber`.

    Quando você clica duas vezes na função, a exibição **Chamador/Computador Chamado** é aberta no painel esquerdo.

    ![Exibição Chamador/Computador Chamado das Ferramentas de Diagnóstico](../profiling/media/quickstart-cpu-usage-caller-callee.png "DiagToolsCallerCallee")

    Nesta exibição, a função selecionada aparece no título e na caixa **Função Atual** (`GetNumber`, neste exemplo). A função que chamou a função atual é mostrada à esquerda em **Função Chamadora** e todas as funções chamadas pela função atual são mostradas na caixa **Funções Chamadas** à direita. (Você pode selecionar cada uma das caixas para alterar a função atual.)

    Essa exibição mostra o tempo total (ms) e o percentual do tempo de execução geral do aplicativo que a função levou para ser concluída.

    **Corpo da Função** também mostra a quantidade total de tempo (e o percentual de tempo) gasta no corpo da função, excluindo o tempo gasto nas funções chamadoras e chamadas. (Nesta ilustração, 2856 de 2863 ms foram gastos no corpo da função e o tempo restante [<20 ms] foi gasto em outro código externo chamado por essa função). Os valores reais serão diferentes dependendo do seu ambiente.

    > [!TIP]
    > Valores altos em **Corpo da Função** podem indicar um gargalo de desempenho dentro da própria função.

## <a name="next-steps"></a>Próximas etapas

- [Analisar o uso de memória](../profiling/memory-usage.md)para identificar gargalos de desempenho.
- [Analisar o uso da CPU](../profiling/cpu-usage.md) para obter informações mais detalhadas sobre a ferramenta de uso de CPU.
- Analise o uso da CPU sem um depurador conectado ou direcionando um aplicativo em execução. Para saber mais, confira [Coletar dados de criação de perfil sem depuração](../profiling/running-profiling-tools-with-or-without-the-debugger.md#collect-profiling-data-without-debugging) em [Executar ferramentas de criação de perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md).

## <a name="see-also"></a>Confira também

- [Criação de perfis no Visual Studio](../profiling/index.yml)
- [Introdução às ferramentas de criação de perfil](../profiling/profiling-feature-tour.md)
