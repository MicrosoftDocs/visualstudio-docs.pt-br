---
title: Medir o uso de memória em seus aplicativos
description: Encontre vazamentos de memória e memória ineficiente enquanto estiver depurando com a ferramenta de diagnóstico integrada ao depurador.
ms.custom: seodec18
ms.date: 04/25/2018
ms.topic: tutorial
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ef2ddd4011f807099c6bc82447f888b56f151e72
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99969406"
---
# <a name="measure-memory-usage-in-visual-studio"></a>Medir o uso de memória no Visual Studio

Encontre vazamentos de memória e memória ineficiente enquanto estiver depurando com a ferramenta de diagnóstico **Uso de Memória** integrada ao depurador. A ferramenta Uso de Memória permite que você obtenha um ou mais *instantâneos* do heap de memória gerenciada e do heap de memória nativa para entender o impacto do uso de memória dos tipos de objeto. Você também pode analisar o uso de memória sem um depurador anexado ou direcionando a um aplicativo em execução. Para obter mais informações, consulte [executar ferramentas de criação de perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md).

Embora você possa coletar instantâneos de memória a qualquer momento na ferramenta **Uso de Memória**, pode usar o depurador do Visual Studio para controlar como o seu aplicativo é executado ao investigar problemas de desempenho. A definição de pontos de interrupção, passo a passo, Interromper Tudo e outras ações de depurador podem ajudá-lo a concentrar as investigações de desempenho nos caminhos de código mais relevantes. A execução dessas ações enquanto o aplicativo é executado pode eliminar o ruído do código que não lhe interessa e reduzir significativamente a quantidade de tempo necessário para diagnosticar um problema.

> [!Important]
> As ferramentas de diagnóstico integradas ao depurador têm suporte para o desenvolvimento do .NET no Visual Studio, incluindo ASP.NET, ASP.NET Core, desenvolvimento nativo/C++ e aplicativos de modo misto (.NET e nativo). O Windows 8 ou posterior é necessário para executar ferramentas de criação de perfil com o depurador (janela **Ferramentas de Diagnóstico**).

Neste tutorial, você irá:

> [!div class="checklist"]
> * Tirar instantâneos da memória
> * Analisar dados de uso de memória

Se o **uso de memória** não fornecer os dados de que você precisa, outras ferramentas de criação de perfil no criador de perfil de [desempenho](../profiling/profiling-feature-tour.md#post_mortem) fornecerão diferentes tipos de informações que podem ser úteis para você. Em muitos casos, o afunilamento de desempenho do seu aplicativo pode ser causado por algo diferente da memória, como CPU, renderização da interface do usuário ou tempo de solicitação de rede.

> [!NOTE]
> **Suporte a alocador personalizado** O criador de perfil de memória nativa funciona coletando dados de eventos [ETW](/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-) de alocação emitidos durante o tempo de execução.  Os alocadores no CRT e no SDK do Windows foram anotados no nível de origem para que seus dados de alocação possam ser capturados. Se você estiver escrevendo seus próprios alocadores, todas as funções que retornarem um ponteiro para uma memória heap recém-alocada poderão ser decoradas com [__declspec](/cpp/cpp/declspec)(allocator), como visto neste exemplo de myMalloc:
>
> `__declspec(allocator) void* myMalloc(size_t size)`

## <a name="collect-memory-usage-data"></a>Coletar dados de uso de memória

1. Abra o projeto que deseja depurar no Visual Studio e defina um ponto de interrupção no aplicativo no ponto em que deseja começar a examinar o uso da memória.

    Se houver uma área em que você suspeite de um problema de memória, defina o primeiro ponto de interrupção antes que ocorra o problema de memória.

    > [!TIP]
    > Como pode ser um desafio capturar o perfil de memória de uma operação de seu interesse quando o aplicativo aloca e desaloca memória com frequência, defina pontos de interrupção no início e no final da operação (ou percorra a operação) para localizar o ponto exato em que a memória foi alterada.

2. Defina um segundo ponto de interrupção ao fim da função ou região de código que você deseja analisar (ou após a ocorrência de um problema de memória suspeito).

3. A janela de **ferramentas de diagnóstico** aparece automaticamente, a menos que você a tenha desativado. Para exibir a janela novamente, clique em **depurar**  >  **janelas**  >  **Mostrar ferramentas de diagnóstico**.

4. Escolha **Uso de Memória** com a configuração **Selecionar Ferramentas** na barra de ferramentas.

     ![Mostrar ferramentas de diagnóstico](../profiling/media/diag-tools-select-tool-2.png "DiagToolsSelectTool")

5. Clique em **Depurar/Iniciar Depuração** (ou em **Iniciar** na barra de ferramentas ou em **F5**).

     Quando o aplicativo terminar de ser carregado, a exibição Resumo das Ferramentas de Diagnóstico será exibida.

     ![Guia Resumo das ferramentas de diagnóstico](../profiling/media/diag-tools-summary-tab-2.png "DiagToolsSummaryTab")

     > [!NOTE]
     > Como a coleta de dados de memória pode afetar o desempenho de depuração de seus aplicativos mistos ou nativos, os instantâneos de memória são desabilitados por padrão. Para habilitar instantâneos de aplicativos mistos ou nativos, inicie uma sessão de depuração (Tecla de atalho: **F5**). Quando a janela **Ferramentas de Diagnóstico** for exibida, escolha a guia **Uso de Memória** e, em seguida, **Criação de Perfil de Heap**.
     >
     >  ![Habilitar instantâneos](../profiling/media/dbgdiag_mem_mixedtoolbar_enablesnapshot.png "DBGDIAG_MEM_MixedToolbar_EnableSnapshot")
     >
     >  Pare (tecla de atalho: **Shift** + **F5**) e reinicie a depuração.

6. Para obter um instantâneo no início da sessão de depuração, escolha **Tirar instantâneo** na barra de ferramentas de resumo **Uso de Memória**. (Talvez seja útil definir um ponto de interrupção aqui também.)

    ![Tirar instantâneo](../profiling/media/dbgdiag_mem_mixedtoolbar_takesnapshot.png "DBGDIAG_MEM_MixedToolbar_TakeSnapshot")

     > [!TIP]
     > Para criar uma linha de base para comparações de memória, tire um instantâneo no início da sessão de depuração.

6. Execute o cenário que fará com que o primeiro ponto de interrupção seja atingido.

7. Enquanto o depurador estiver pausado no primeiro ponto de interrupção, escolha **Tirar instantâneo** na barra de ferramentas de resumo **Uso de Memória**.

8. Pressione **F5** para executar o aplicativo até o segundo ponto de interrupção.

9. Agora, crie outro instantâneo.

     Neste ponto, você pode começar a analisar os dados.

## <a name="analyze-memory-usage-data"></a>Analisar dados de uso de memória
As linhas da tabela de resumo de Uso de Memória listam os instantâneos que você criou durante a sessão de depuração e fornecem links para modos de exibição mais detalhados.

![Tabela de Resumo de memória](../profiling/media/dbgdiag_mem_summarytable.png "DBGDIAG_MEM_SummaryTable")

 O nome das colunas depende do modo de depuração escolhido nas propriedades do projeto: .NET, nativo ou misto (.NET e nativo).

- As colunas **Objetos (Diff)** e **Alocações (Diff)** exibem o número de objetos no .NET e na memória nativa quando o instantâneo foi criado.

- A coluna **Tamanho do Heap (Diff)** exibe o número de bytes no .NET e heaps nativos

Quando você tira vários instantâneos, as células da tabela de resumo incluem a alteração no valor entre o instantâneo de linha e o instantâneo anterior.

Para analisar o uso da memória, clique em um dos links que abre um relatório detalhado do uso de memória:

- Para exibir detalhes da diferença entre o instantâneo atual e o instantâneo anterior, escolha o link alterar à esquerda da seta (![aumento de uso de memória](../profiling/media/prof-tour-mem-usage-up-arrow.png "Aumento de uso de memória")). Uma seta vermelha indica um aumento no uso de memória e uma seta verde indica uma diminuição.

> [!TIP]
> Para ajudar a identificar problemas de memória mais rapidamente, os relatórios de comparação são classificados pelos tipos de objeto que mais aumentaram no número geral (clique no link de alteração na coluna **Objetos (Comparação)**) ou que mais aumentaram quanto ao tamanho geral do heap (clique no link de alteração na coluna **Tamanho do Heap (Comparação)**).

- Para exibir detalhes apenas do instantâneo selecionado, clique no link que não é de alteração.

   O relatório é exibido em uma janela separada.

### <a name="managed-types-reports"></a>Relatórios de tipos gerenciados
 Escolha o link atual de uma célula **Objetos (Diff)** ou **Alocações (Diff)** da tabela de resumo de Uso de Memória.

 ![Relatório de tipo gerenciado do depurador &#45; caminhos para raiz](../profiling/media/dbgdiag_mem_managedtypesreport_pathstoroot.png "DBGDIAG_MEM_ManagedTypesReport_PathsToRoot")

 O painel superior mostra a contagem e o tamanho dos tipos no instantâneo, incluindo o tamanho de todos os objetos referenciados pelo tipo (**inclusive tamanho**).

 A árvore **Caminhos para a Raiz** no painel inferior exibe os objetos que referenciam o tipo selecionado no painel superior. O coletor de lixo do .NET limpa a memória de um objeto somente quando o último tipo que faz referência a ele foi liberado.

 A árvore **objetos referenciados** exibe as referências que são mantidas pelo tipo selecionado no painel superior.

 ![Exibição de relatório de objetos referenciados gerenciados](../profiling/media/dbgdiag_mem_managedtypesreport_referencedtypes.png "DBGDIAG_MEM_ManagedTypesReport_ReferencedTypes")

 Para exibir as instâncias de um tipo selecionado no painel superior, escolha o ícone do ![ícone de instância](../profiling/media/dbgdiag_mem_instanceicon.png "DBGDIAG_MEM_InstanceIcon") .

 ![Captura de tela da exibição de instâncias na ferramenta de uso de memória do Visual Studio, mostrando o painel instâncias e os caminhos para o painel objetos de referência e raiz.](../profiling/media/dbgdiag_mem_managedtypesreport_instances.png "DBGDIAG_MEM_ManagedTypesReport_Instances")

 O modo de exibição **Instâncias** exibe as instâncias do objeto selecionado no instantâneo no painel superior. O painel **Caminhos para Raiz** e **Objetos Referenciados** exibe os objetos que referenciam a instância selecionada e os tipos de que a instância selecionada referencia. Quando o depurador é interrompido no ponto em que o instantâneo foi tirado, você pode passar o mouse sobre a célula **Valor** para exibir os valores do objeto em uma dica de ferramenta.

### <a name="native-type-reports"></a>Relatórios de tipo nativo
 Escolha o link atual de uma célula **Alocações (Diff)** ou **Tamanho do Heap (Diff)** na tabela de resumo de Uso de Memória da janela **Ferramentas de Diagnóstico**.

 ![Exibição de tipo nativo](../profiling/media/dbgdiag_mem_native_typesview.png "DBGDIAG_MEM_Native_TypesView")

 O **Modo de exibição de tipos** exibe o número e tamanho dos tipos no instantâneo.

- Escolha o ícone instâncias (![o ícone de instância na coluna tipo de objeto](../profiling/media/dbg_mma_instancesicon.png "DBG_MMA_InstancesIcon")) de um tipo selecionado para exibir informações sobre os objetos do tipo selecionado no instantâneo.

     O modo de exibição **Instâncias** mostra cada instância do tipo selecionado. A seleção de uma instância exibe a pilha de chamadas resultou na criação da instância no painel **Pilha de Chamadas de Alocação**.

     ![Captura de tela da exibição de instâncias na ferramenta de uso de memória do Visual Studio, mostrando o painel instâncias e o painel de pilha de chamadas de alocação.](../profiling/media/dbgdiag_mem_native_instances.png "DBGDIAG_MEM_Native_Instances")

- Escolha **Exibição de Pilhas** na lista **Exibir Modo** para ver a pilha de alocação do tipo selecionado.

     ![Exibição de pilhas](../profiling/media/dbgdiag_mem_native_stacksview.png "DBGDIAG_MEM_Native_StacksView")

### <a name="change-diff-reports"></a>Relatórios de comparação (Diff)

- Escolha o link de alteração em uma célula da tabela de resumo da guia **Uso de Memória** na janela **Ferramentas de Diagnóstico**.

   ![Escolha uma alteração &#40;relatório de&#41; diff](../profiling/media/dbgdiag_mem_choosediffreport.png "DBGDIAG_MEM_ChooseDiffReport")

- Escolha um instantâneo na lista **Comparar com** de um relatório gerenciado ou nativo.

   ![Escolha um instantâneo da lista comparar com](../profiling/media/dbgdiag_mem_choosecompareto.png "DBGDIAG_MEM_ChooseCompareTo")

O relatório de comparação adiciona colunas (marcadas com **(Diff)**) ao relatório base que mostra a diferença entre o valor do instantâneo base e o do instantâneo de comparação. Veja como pode ser a aparência de um relatório de comparação Exibição de Tipo Nativo:

![Exibição de comparação de tipos nativos](../profiling/media/dbgdiag_mem_native_typesviewdiff.png "DBGDIAG_MEM_Native_TypesViewDiff")

## <a name="blogs-and-videos"></a>Blogs e vídeos

[Analisar a CPU e a memória durante a depuração](https://devblogs.microsoft.com/visualstudio/analyze-cpu-memory-while-debugging/)

[Visual C++ Blog: Memory Profiling in Visual C++ 2015](https://devblogs.microsoft.com/cppblog/memory-profiling-in-visual-c-2015/) (Blog do Visual C++: Criação de perfil de memória no Visual C++ 2015)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como coletar e analisar dados de uso da memória. Se você já concluiu o [tour do criador de perfil](../profiling/profiling-feature-tour.md), obtenha uma visão geral de como analisar o uso de CPU em seus aplicativos.

> [!div class="nextstepaction"]
> [Analisar o uso da CPU](../profiling/beginners-guide-to-performance-profiling.md)
