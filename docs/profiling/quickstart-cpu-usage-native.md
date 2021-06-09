---
title: Analisar os dados de uso da CPU (C++)
description: Medir o desempenho do aplicativo em C++ usando a ferramenta de diagnóstico de uso da CPU
ms.date: 02/14/2020
ms.topic: quickstart
f1_keywords:
- ''
helpviewer_keywords:
- Profiling Tools, quick start
- Diagnostics Tools, CPU Usage
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- cplusplus
ms.openlocfilehash: 8c68cc67d768dbe2b1c42671a02360e5cef2b56b
ms.sourcegitcommit: 01a411cd7ae3488b7b979a947bca92fd296a98e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760933"
---
# <a name="quickstart-analyze-cpu-usage-data-in-visual-studio-c"></a>Início Rápido: analisar dados de uso da CPU no Visual Studio (C++)

O Visual Studio fornece muitos recursos poderosos para ajudar a analisar problemas de desempenho em seu aplicativo. Este tópico fornece uma maneira rápida de conhecer alguns dos recursos básicos. Aqui, vamos examinar a ferramenta para identificar os gargalos de desempenho devido ao alto uso da CPU. As Ferramentas de Diagnóstico têm suporte para desenvolvimento de .NET no Visual Studio, incluindo o ASP.NET e para desenvolvimento nativo/C++.

O Hub de diagnósticos oferece várias outras opções para executar e gerenciar sua sessão de diagnóstico. Se a ferramenta **Uso de CPU** descrita aqui não fornecer os dados que você precisa, as [outras ferramentas de criação de perfil](../profiling/profiling-feature-tour.md) fornecerão diferentes tipos de informações que poderão ser úteis. Em muitos casos, o gargalo de desempenho do aplicativo pode ser causado por algo que não seja a CPU, como memória, interface do usuário de renderização ou tempo de solicitação de rede. O Criador de Perfil de Desempenho oferece muitas outras opções para registrar e analisar esse tipo de dados. [PerfTips](../profiling/perftips.md), outra ferramenta de criação de perfil integrada ao depurador, também permite que você ande pelo código e identifique quanto tempo leva para concluir funções ou blocos de código específicos.

O Windows 8 ou posterior é necessário para executar ferramentas de criação de perfil com o depurador (janela **Ferramentas de Diagnóstico**). No Windows 7 e posteriores, você pode usar a ferramenta post-mortem, o [Criador de Perfil de Desempenho](../profiling/profiling-feature-tour.md).

## <a name="create-a-project"></a>Criar um projeto

1. Abra Visual Studio e crie o projeto.

   ::: moniker range="vs-2017"
   Na barra de menus superior, escolha **Arquivo** > **Novo** > **Projeto**.

   Na caixa **de diálogo** Novo Projeto no painel esquerdo, expanda **Visual C++** e escolha Área de Trabalho **do Windows.** No painel central, escolha Aplicativo **de Console do Windows.** Em seguida, nomeia o *Diagnostics_Get_Started_Native*.

   Se você não vir o modelo de projeto Aplicativo de Console do **Windows,** escolha o **link** Abrir Instalador do Visual Studio no painel esquerdo da **caixa** de diálogo Novo Projeto. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho Desenvolvimento de área de trabalho **com C++** e, em seguida, **escolha Modificar**.
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   Se a janela inicial não estiver aberta, escolha **Janela de** Início > **do Arquivo**.

   Na janela inicial, escolha **Criar um novo projeto.**

   Na janela **Criar um novo projeto**, insira ou digite *console* na caixa de pesquisa. Em seguida, **escolha C++** na lista Idioma e, em seguida, **escolha Windows** na lista Plataforma.

   Depois de aplicar os filtros de linguagem e plataforma, escolha o modelo **Aplicativo de Console** e, em seguida, escolha **Próximo.**

   > [!NOTE]
   > Se você não vir o modelo **aplicativo de console,** poderá instalá-lo na **janela Criar um novo** projeto. Na mensagem **Não encontrou o que precisa?**, escolha o link **Instalar mais ferramentas e recursos**. Em seguida, no Instalador do Visual Studio, escolha a carga **de trabalho Desenvolvimento da área de trabalho com C++.**

   Na janela **Configurar seu novo projeto,** digite ou digite *Diagnostics_Get_Started_Native* na caixa **Nome do** projeto. Em seguida, escolha **Criar**.

   ::: moniker-end

   O Visual Studio abre seu novo projeto.

1. No *Diagnostics_Get_Started_Native*, substitua o código a seguir

    ```c++
    int main()
    {
        return 0;
    }
    ```

    por esse código (não remova `#include "stdafx.h"`):

    ```c++
    #include <iostream>
    #include <limits>
    #include <mutex>
    #include <random>
    #include <functional>

    //.cpp file code:

    static constexpr int MIN_ITERATIONS = std::numeric_limits<int>::max() / 1000;
    static constexpr int MAX_ITERATIONS = MIN_ITERATIONS + 10000;

    long long m_totalIterations = 0;
    std::mutex m_totalItersLock;

    int getNumber()
    {

        std::uniform_int_distribution<int> num_distribution(MIN_ITERATIONS, MAX_ITERATIONS);
        std::mt19937 random_number_engine; // pseudorandom number generator
        auto get_num = std::bind(num_distribution, random_number_engine);
        int random_num = get_num();

        auto result = 0;
        {
            std::lock_guard<std::mutex> lock(m_totalItersLock);
            m_totalIterations += random_num;
        }
        // we're just spinning here
        // to increase CPU usage
        for (int i = 0; i < random_num; i++)
        {
            result = get_num();
        }
        return result;
    }

    void doWork()
    {
        std::wcout << L"The doWork function is running on another thread." << std::endl;

        auto x = getNumber();
    }

    int main()
    {
        std::vector<std::thread> threads;

        for (int i = 0; i < 10; ++i) {

            threads.push_back(std::thread(doWork));
            std::cout << "The Main() thread calls this after starting the new thread" << std::endl;
        }

        for (auto& thread : threads) {
            thread.join();
        }

        return 0;
    }
    ```

## <a name="step-1-collect-profiling-data"></a>Etapa 1: Coletar dados de criação de perfil

1. Primeiro, defina um ponto de interrupção em seu aplicativo nesta linha de código na função `main`:

    `for (int i = 0; i < 10; ++i) {`

    Defina um ponto de interrupção clicando na medianiz à esquerda da linha de código.

2. Em seguida, defina um segundo ponto de interrupção no colchete de fechamento no final da função `main`:

     ![Definir pontos de interrupção para criação de perfil](../profiling/media/quickstart-cpu-usage-breakpoints-cplusplus.png "Definir pontos de interrupção para criação de perfil")

    Definindo dois pontos de interrupção, você pode limitar a coleta de dados às partes do código que deseja analisar.

3. A janela **Ferramentas de Diagnóstico** já fica visível, a menos que tenha sido desativada. Para abrir a janela novamente, clique em **Depurar**  >  **Windows**  >  **Show Ferramentas de Diagnóstico**.

4. Clique **em Depurar**  >  **Iniciar Depuração** **(ou Iniciar** na barra de ferramentas ou **F5**).

     Quando o aplicativo terminar de ser carregado, a exibição **Resumo** das Ferramentas de Diagnóstico será exibida.

5. Enquanto o depurador estiver em pausa, habilite a coleta dos dados de Uso da CPU escolhendo **Registrar perfil da CPU** e abra a guia **Uso da CPU**.

     ![Habilitar criação de perfil de CPU de Ferramentas de Diagnóstico](../profiling/media/quickstart-cpu-usage-summary.png "Habilitar criação de perfil de CPU de Ferramentas de Diagnóstico")

     Quando a coleta de dados estiver habilitada, o botão de registro exibe um círculo vermelho.

     Quando você escolhe **Registrar perfil de CPU**, o Visual Studio começará a gravar as funções e quanto tempo elas levam para serem executadas, fornecendo também um gráfico de linha do tempo que você pode usar para se concentrar em segmentos específicos da sessão de amostragem. Você só pode exibir os dados coletados quando seu aplicativo é interrompido no ponto de interrupção.

6. Pressione F5 para executar o aplicativo até o segundo ponto de interrupção.

     Agora, você tem dados de desempenho do aplicativo especificamente para a região do código que é executada entre os dois pontos de interrupção.

     O criador de perfil começa a preparar os dados de thread. Aguarde sua conclusão.

     A ferramenta de Uso de CPU exibe o relatório na guia **Uso da CPU**.

     Neste ponto, você pode começar a analisar os dados.

## <a name="step-2-analyze-cpu-usage-data"></a>Etapa 2: Analisar os dados de uso de CPU

Recomendamos que você comece a analisar os dados examinando a lista de funções em Uso da CPU, identificando as funções que fazem a maior parte do trabalho e, em seguida, fazendo uma análise mais detalhada de cada uma.

1. Na lista de funções, examine as funções que fazem a maior parte do trabalho.

     ![Guia Uso da CPU das Ferramentas de Diagnóstico](../profiling/media/quickstart-cpu-usage-cpu-cplusplus.png "DiagToolsCPUUsageTab")

    > [!TIP]
    > As funções são listadas em ordem, começando com as que fazem a maior parte do trabalho (elas não ficam na ordem de chamada). Isso ajuda a identificar rapidamente as funções com execução mais longa.

2. Na lista de função, clique duas vezes na função `getNumber`.

    Quando você clica duas vezes na função, a exibição **Chamador/Computador Chamado** é aberta no painel esquerdo.

    ![Exibição Chamador/Computador Chamado das Ferramentas de Diagnóstico](../profiling/media/quickstart-cpu-usage-caller-callee-cplusplus.png "DiagToolsCallerCallee")

    Nesta exibição, a função selecionada aparece no título e na caixa **Função Atual** (`getNumber`, neste exemplo). A função que chamou a função atual é mostrada à esquerda em **Função Chamadora** e todas as funções chamadas pela função atual são mostradas na caixa **Funções Chamadas** à direita. (Você pode selecionar cada uma das caixas para alterar a função atual.)

    Essa exibição mostra o tempo total (ms) e o percentual do tempo de execução geral do aplicativo que a função levou para ser concluída.

    **Corpo da Função** também mostra a quantidade total de tempo (e o percentual de tempo) gasta no corpo da função, excluindo o tempo gasto nas funções chamadoras e chamadas. (Nesta ilustração, 119 de 43602 ms foram gastos no corpo da função e o tempo restante foi gasto em outro código chamado por essa função). Os valores reais serão muito diferentes dependendo do seu ambiente.

    > [!TIP]
    > Valores altos em **Corpo da Função** podem indicar um gargalo de desempenho dentro da própria função.

## <a name="next-steps"></a>Próximas etapas

- [Analisar o uso de memória](../profiling/memory-usage.md)para identificar gargalos de desempenho.
- [Analisar o uso da CPU](../profiling/cpu-usage.md) para obter informações mais detalhadas sobre a ferramenta de uso de CPU.
- Analise o uso da CPU sem um depurador conectado ou direcionando um aplicativo em execução. Para saber mais, confira [Coletar dados de criação de perfil sem depuração](../profiling/running-profiling-tools-with-or-without-the-debugger.md#collect-profiling-data-without-debugging) em [Executar ferramentas de criação de perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md).

## <a name="see-also"></a>Confira também

- [Criação de perfis no Visual Studio](../profiling/index.yml)
- [Introdução às ferramentas de criação de perfil](../profiling/profiling-feature-tour.md)
