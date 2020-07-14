---
title: Guia do iniciante para amostragem de CPU
ms.custom: seodec18
ms.date: 02/27/2017
ms.topic: how-to
f1_keywords:
- vs.performance.wizard.intropage
helpviewer_keywords:
- Profiling Tools, quick start
- performance tools, wizard
- Performance Wizard
ms.assetid: 85161cc4-18ee-49b3-9487-33680e687597
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: a58803747e0da411012226325c390352edf4e919
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330599"
---
# <a name="beginners-guide-to-cpu-sampling"></a>Guia do iniciante para amostragem de CPU
Você pode usar as ferramentas de criação de perfil do Visual Studio para analisar problemas de desempenho em seu aplicativo. Este procedimento mostra como usar dados de **Amostragem**.

> [!NOTE]
> Recomendamos que você use a ferramenta [Uso de CPU](../profiling/beginners-guide-to-performance-profiling.md) na janela Ferramentas de Diagnóstico em vez da ferramenta de amostragem de CPU herdada, a menos que você precise de recursos especializados, como suporte para instrumentação.

 **Amostragem** é um método de criação de perfil estatístico que mostra as funções que fazem a maior parte do trabalho do modo de usuário no aplicativo. A amostragem é uma boa opção para começar a procurar áreas para acelerar seu aplicativo.

 Em intervalos especificados, o método de **Amostragem** coleta informações sobre as funções que estão em execução em seu aplicativo. Depois de concluir uma execução de criação de perfil, a exibição **Resumo** dos dados de criação de perfil mostra a árvore de chamadas de função mais ativa, chamada de **Afunilamento**, em que foi executada a maior parte do trabalho no aplicativo. A exibição também lista as funções que executaram o trabalho mais individual e fornece um gráfico de linha do tempo que você pode usar para se concentrar em segmentos específicos da sessão de amostragem.

 Se a **Amostragem** não fornecer os dados que você precisa, outros métodos de coleção das ferramentas de criação de perfil fornecem diferentes tipos de informações que poderão ser úteis. Para obter mais informações sobre esses outros métodos, consulte [como: escolher métodos de coleção](../profiling/how-to-choose-collection-methods.md).

> [!TIP]
> Se você criar um perfil de código que chama o Windows functions, deverá ter certeza de que tem o mais atual. arquivos *PDB* . Sem esses arquivos, as exibições de relatório listarão nomes de funções do Windows criptografadas e difíceis de entender. Para obter mais informações sobre como verificar se você tem os arquivos necessários, consulte [como fazer referência a informações de símbolo do Windows](../profiling/how-to-reference-windows-symbol-information.md).

## <a name="create-and-run-a-performance-session"></a>Criar e executar uma sessão de desempenho
 Para obter os dados que precisa analisar, você deve primeiro criar uma sessão de desempenho e, em seguida, executar a sessão. O **Assistente de Desempenho** permite executar esses dois procedimentos.

 Se não estiver criando perfil de um aplicativo da área de trabalho do Windows ou de um aplicativo ASP.NET, você deverá usar uma das outras ferramentas de criação de perfil. Confira [Introdução às ferramentas de criação de perfil](../profiling/profiling-feature-tour.md).

#### <a name="to-create-and-run-a-performance-session"></a>Para criar e executar uma sessão de desempenho

1. Abra a solução no Visual Studio. Defina a configuração como Versão. (Localize a caixa **Configurações da Solução** na barra de ferramentas, que é definida como **Depurar**, por padrão. Altere-a para **Versão**.)

    > [!IMPORTANT]
    > Se você não for um administrador do computador que está usando, execute o Visual Studio como um administrador enquanto estiver usando o criador de perfil. (Clique com o botão direito do mouse no ícone do aplicativo do Visual Studio e, em seguida, clique em **Executar como administrador**.

2. No menu **Depurar**, selecione **Criador de Perfil** e, em seguida, **Criador de Perfil de Desempenho**.

3. Marque a opção **Assistente de Desempenho** e, em seguida, clique em **Iniciar**.

4. Marque a opção **Amostragem de CPU (recomendado)** e clique em **Concluir**.

5. O aplicativo é iniciado e o criador de perfil começa a coletar dados.

6. Execute as funcionalidades que podem conter problemas de desempenho.

7. Feche o aplicativo como de costume.

     Depois de concluir a execução do aplicativo, a exibição **Resumo** dos dados de criação de perfil aparecerá na janela principal do Visual Studio e um ícone para a nova sessão aparecerá na janela **Gerenciador de Desempenho**.

## <a name="step-2-analyze-sampling-data"></a>Etapa 2: Analisar os dados de amostragem
 Quando você concluir a execução de uma sessão de desempenho, a exibição **Resumo** do relatório de criação de perfil aparecerá na janela principal do Visual Studio.

 Recomendamos que você comece a analisar os dados examinando o **Afunilamento** e, em seguida, a lista de funções que estão fazendo a maior parte do trabalho e, finalmente, se concentrando em outras funções usando o **Linha do Tempo de Resumo**. Você também pode exibir sugestões e avisos de criação de perfil na janela **Lista de Erros**.

 Lembre-se de que o método de amostragem pode não oferecer as informações que você precisa. Por exemplo, as amostras somente são coletadas quando o aplicativo está executando o código de modo de usuário. Portanto, algumas funcionalidades, como operações de entrada e saída, não são capturadas pela amostragem. As Ferramentas de Criação de Perfil fornecem vários métodos de coleta que podem permitir que você se concentre nos dados mais importantes. Para obter mais informações sobre os outros métodos, consulte [como: escolher métodos de coleção](../profiling/how-to-choose-collection-methods.md).

 Cada área enumerada na figura está relacionada a uma etapa do procedimento.

 ![Exibição de relatório de resumo para amostragem](../profiling/media/summary_sampling.png "Summary_Sampling")

#### <a name="to-analyze-sampling-data"></a>Para analisar os dados de amostragem

1. Na exibição **Resumo**, o **Afunilamento** mostra a ramificação da árvore de chamadas do aplicativo com as amostras mais inclusivas. Este é o caminho de execução que estava mais ativo quando os dados foram coletados. Valores inclusivos altos podem indicar que o algoritmo que gera a árvore de chamadas pode ser otimizado. Localize a função no código que está mais inferior no caminho. Observe que o caminho também pode incluir funções do sistema ou funções em módulos externos.

     ![Hot Path do profiler](../profiling/media/profiler_hotpath.png "Profiler_HotPath")

    1. **Amostras Inclusivas** indicam quanto trabalho foi feito pela função e todas as funções chamadas por ela. Contagens inclusivas altas apontam para as funções que são mais dispendiosas em geral.

    2. **Amostras Exclusivas** indicam quanto trabalho foi feito pelo código no corpo da função, exceto o trabalho realizado pelas funções que foram chamadas por ele. Contagens exclusivas altas podem indicar um gargalo de desempenho dentro da própria função.

2. Clique no nome da função para exibir a exibição **Detalhes da Função** dos dados de criação de perfil. A exibição **Detalhes da Função** apresenta uma exibição gráfica dos dados de criação de perfil para a função selecionada, mostrando todas as funções que chamaram essa função e todas as funções que foram chamadas pela função selecionada.

    - Os tamanhos dos blocos das funções que chamaram e que foram chamadas representam a frequência relativa em que as funções chamaram ou foram chamadas.

    - Você pode clicar no nome de uma função que chamou ou que foi chamada para torná-la a função selecionada da exibição Detalhes da Função.

    - O painel inferior da janela **Detalhes da Função** exibe o próprio código da função. Se você examinar o código e encontrar uma oportunidade para otimizar seu desempenho, clique no nome do arquivo de origem para abrir o arquivo no editor do Visual Studio.

3. Para continuar sua análise, retorne ao modo de exibição de **Resumo** selecionando **Resumo** na lista suspensa **exibição** . Examine as funções em **Funções que Fazem o Trabalho Mais Individual**. Esta lista exibe as funções com as amostras mais exclusivas. O código no corpo da função dessas funções executou um trabalho significativo e talvez seja possível otimizá-lo. Para analisar melhor uma função específica, clique no nome da função para mostrá-la na exibição **Detalhes da Função**.

     ![Lista de funções que fazem mais trabalho](../profiling/media/functions_mostwork.png "Functions_MostWork")

     Para continuar a investigação sobre a execução de criação de perfil, você pode analisar novamente um segmento dos dados de criação de perfil usando a linha do tempo na exibição **Resumo** para mostrar o **Afunilamento** e as **Funções que fazem a maior parte do trabalho individual** de um segmento selecionado. Por exemplo, focar um pico menor na linha do tempo pode revelar árvores de chamadas e funções dispendiosas que não foram mostradas na análise da execução inteira da criação de perfil.

     Para reanalisar um segmento, selecione um segmento dentro da caixa **linha do tempo de resumo** e clique em **Filtrar por seleção**.

     ![Linha do tempo de exibição de Resumo de desempenho](../profiling/media/performancesummary.png "PerformanceSummary")

4. O criador de perfil também usa um conjunto de regras para sugerir maneiras de melhorar a execução de criação de perfil e identificar possíveis problemas de desempenho. Quando um problema é encontrado, um aviso é exibido na **Lista de Erros**. Para abrir a janela **Lista de Erros**, no menu **Exibição**, clique em **Lista de Erros**.

    - Para ver a função que gerou um aviso, na exibição **Detalhes da função**, clique duas vezes no aviso.

    - Para exibir informações detalhadas sobre o aviso, clique com o botão direito do mouse no erro e, em seguida, clique em **Mostrar Ajuda para Erros**

## <a name="step-3-revise-code-and-rerun-a-session"></a>Etapa 3: Revisar o código e executar uma sessão novamente
 Depois de localizar e otimizar uma ou mais funções, você poderá repetir a execução de criação de perfil e comparar os dados para ver a diferença que as alterações acarretaram no desempenho do aplicativo.

#### <a name="to-revise-code-and-rerun-the-profiler"></a>Para revisar o código e executar novamente o criador de perfil

1. Altere seu código.

2. Para abrir o **Gerenciador de Desempenho**, no menu **Depurar**, clique em **Criador de Perfil**, em seguida, em **Gerenciador de Desempenho** e, finalmente, em **Mostrar Gerenciador de Desempenho**.

3. No **Gerenciador de Desempenho**, clique com o botão direito do mouse na sessão que deseja executar novamente e, em seguida, clique em **Inicializar com a Criação de Perfil.**

4. Depois que você executar novamente a sessão, outro arquivo de dados será adicionado à pasta *Relatórios* da sessão no **Gerenciador de Desempenho**. Selecione tanto os dados de criação perfil originais quanto os novos, clique com o botão direito do mouse na seleção e, em seguida, clique em **Comparar Relatórios de Desempenho**.

     Uma nova janela de relatório é aberta, exibindo os resultados da comparação. Para saber mais sobre como usar a exibição de comparação, veja [Como comparar arquivos de dados de desempenho](../profiling/how-to-compare-performance-data-files.md).

## <a name="see-also"></a>Veja também
- [Performance Explorer](../profiling/performance-explorer.md)
- [Guia de Introdução](../profiling/getting-started-with-performance-tools.md)
- [Visões gerais](../profiling/overviews-performance-tools.md)
- [Criação de perfis no Visual Studio](../profiling/index.yml)
- [Introdução às ferramentas de criação de perfil](../profiling/profiling-feature-tour.md)
