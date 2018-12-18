---
title: Medir o uso de memória em seus aplicativos
description: Encontre vazamentos de memória e memória ineficiente enquanto estiver depurando com a ferramenta de diagnóstico integrada ao depurador.
ms.custom: mvc
ms.date: 04/25/2017
ms.technology: vs-ide-debug
ms.topic: tutorial
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: eeacfb15b02c19ea4a166fbc8511aab644d41ea5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49861404"
---
# <a name="profile-memory-usage-in-visual-studio"></a>Uso de memória de perfil no Visual Studio
Encontre vazamentos de memória e memória ineficiente enquanto estiver depurando com a ferramenta de diagnóstico **Uso de Memória** integrada ao depurador. A ferramenta Uso de Memória permite que você obtenha um ou mais *instantâneos* do heap de memória gerenciada e do heap de memória nativa para entender o impacto do uso de memória dos tipos de objeto. Você pode coletar instantâneos de aplicativos .NET, nativos ou mistos (.NET e nativos).  
  
 O gráfico a seguir mostra a janela **Ferramentas de Diagnóstico** (disponível no Visual Studio 2015 Atualização 1 e versões posteriores):  
  
 ![DiagnosticTools&#45;Update1](../profiling/media/diagnostictools-update1.png "DiagnosticTools-Update1")  
  
 Embora você possa coletar instantâneos de memória a qualquer momento na ferramenta **Uso de Memória**, pode usar o depurador do Visual Studio para controlar como o seu aplicativo é executado ao investigar problemas de desempenho. A definição de pontos de interrupção, passo a passo, Interromper Tudo e outras ações de depurador podem ajudá-lo a concentrar as investigações de desempenho nos caminhos de código mais relevantes. A execução dessas ações enquanto o aplicativo é executado pode eliminar o ruído do código que não lhe interessa e reduzir significativamente a quantidade de tempo necessário para diagnosticar um problema.  
  
 Você também pode usar a ferramenta de memória fora do depurador. Confira [Uso de memória sem depuração](../profiling/memory-usage-without-debugging2.md). Você pode usar as ferramentas de criação de perfil sem nenhum depurador anexado, com o Windows 7 e posteriores. O Windows 8 ou posterior é necessário para executar ferramentas de criação de perfil com o depurador (janela **Ferramentas de Diagnóstico**).
  
> [!NOTE]
>  **Suporte de alocador personalizado** O criador de perfil de memória nativa funciona com a coleta de dados de evento [ETW](/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-) de alocação emitidos durante o tempo de execução.  Os alocadores no CRT e no SDK do Windows foram anotados no nível de origem para que seus dados de alocação possam ser capturados.  Se você estiver escrevendo seus próprios alocadores, todas as funções que retornarem um ponteiro para uma memória heap recém-alocada poderão ser decoradas com [__declspec](/cpp/cpp/declspec)(allocator), como visto neste exemplo de myMalloc:  
>   
>  `__declspec(allocator) void* myMalloc(size_t size)` 

Neste tutorial, você irá:

> [!div class="checklist"]
> * Tirar instantâneos da memória
> * Analisar dados de uso de memória

## <a name="collect-memory-usage-data"></a>Coletar dados de uso de memória

1.  Abra o projeto que deseja depurar no Visual Studio e defina um ponto de interrupção no aplicativo no ponto em que deseja começar a examinar o uso da memória.

    Se houver uma área em que você suspeite de um problema de memória, defina o primeiro ponto de interrupção antes que ocorra o problema de memória.

    > [!TIP]
    >  Como pode ser um desafio capturar o perfil de memória de uma operação de seu interesse quando o aplicativo aloca e desaloca memória com frequência, defina pontos de interrupção no início e no final da operação (ou percorra a operação) para localizar o ponto exato em que a memória foi alterada. 

2.  Defina um segundo ponto de interrupção ao fim da função ou região de código que você deseja analisar (ou após a ocorrência de um problema de memória suspeito).
  
3.  A janela **Ferramentas de Diagnóstico** é exibida automaticamente, a menos que tenha sido desativada. Para abrir a janela novamente, clique em **Depurar** > **Windows** > **Mostrar Ferramentas de Diagnóstico**.

4.  Escolha **Uso de Memória** com a configuração **Selecionar Ferramentas** na barra de ferramentas.

     ![Mostrar Ferramentas de Diagnósticos](../profiling/media/DiagToolsSelectTool.png "DiagToolsSelectTool")

5.  Clique em **Depurar/Iniciar Depuração** (ou em **Iniciar** na barra de ferramentas ou em **F5**).

     Quando o aplicativo terminar de ser carregado, a exibição Resumo das Ferramentas de Diagnóstico será exibida.

     ![Guia Resumo das Ferramentas de Diagnóstico](../profiling/media/DiagToolsSummaryTab.png "DiagToolsSummaryTab")

     > [!NOTE]
     >  Como a coleta de dados de memória pode afetar o desempenho de depuração de seus aplicativos mistos ou nativos, os instantâneos de memória são desabilitados por padrão. Para habilitar instantâneos de aplicativos mistos ou nativos, inicie uma sessão de depuração (Tecla de atalho: **F5**). Quando a janela **Ferramentas de Diagnóstico** for exibida, escolha a guia **Uso de Memória** e, em seguida, **Criação de Perfil de Heap**.  
     >   
     >  ![Habilitar instantâneos](../profiling/media/dbgdiag_mem_mixedtoolbar_enablesnapshot.png "DBGDIAG_MEM_MixedToolbar_EnableSnapshot")  
     >   
     >  Pare (tecla de atalho: **Shift**+**F5**) e reinicie a depuração.  

6.  Para obter um instantâneo no início da sessão de depuração, escolha **Tirar instantâneo** na barra de ferramentas de resumo **Uso de Memória**. (Talvez seja útil definir um ponto de interrupção aqui também.)

    ![Tirar instantâneo](../profiling/media/dbgdiag_mem_mixedtoolbar_takesnapshot.png "DBGDIAG_MEM_MixedToolbar_TakeSnapshot") 
     
     > [!TIP]
     >  Para criar uma linha de base para comparações de memória, tire um instantâneo no início da sessão de depuração.  

6.  Execute o cenário que fará com que o primeiro ponto de interrupção seja atingido.

7.  Enquanto o depurador estiver pausado no primeiro ponto de interrupção, escolha **Tirar instantâneo** na barra de ferramentas de resumo **Uso de Memória**.  

8.  Pressione **F5** para executar o aplicativo até o segundo ponto de interrupção.

9.  Agora, crie outro instantâneo.

     Neste ponto, você pode começar a analisar os dados.    
  
## <a name="analyze-memory-usage-data"></a>Analisar dados de uso de memória
As linhas da tabela de resumo de Uso de Memória listam os instantâneos que você criou durante a sessão de depuração e fornecem links para modos de exibição mais detalhados.

![Tabela de resumo de memória](../profiling/media/dbgdiag_mem_summarytable.png "DBGDIAG_MEM_SummaryTable")

 O nome das colunas depende do modo de depuração escolhido nas propriedades do projeto: .NET, nativo ou misto (.NET e nativo).  
  
-   As colunas **Objetos (Diff)** e **Alocações (Diff)** exibem o número de objetos no .NET e na memória nativa quando o instantâneo foi criado.  
  
-   A coluna **Tamanho do Heap (Diff)** exibe o número de bytes no .NET e heaps nativos 

Quando você tira vários instantâneos, as células da tabela de resumo incluem a alteração no valor entre o instantâneo de linha e o instantâneo anterior.  

Para analisar o uso da memória, clique em um dos links que abre um relatório detalhado do uso de memória:  

- Para exibir detalhes da diferença entre o instantâneo atual e o instantâneo anterior, escolha o link de alteração à esquerda da seta (![Aumento do Uso de Memória](../profiling/media/prof-tour-mem-usage-up-arrow.png "Aumento do Uso de Memória")). Uma seta vermelha indica um aumento no uso de memória e uma seta verde indica uma diminuição.

  > [!TIP]
  >  Para ajudar a identificar problemas de memória mais rapidamente, os relatórios de comparação são classificados pelos tipos de objeto que mais aumentaram no número geral (clique no link de alteração na coluna **Objetos (Comparação)**) ou que mais aumentaram quanto ao tamanho geral do heap (clique no link de alteração na coluna **Tamanho do Heap (Comparação)**).

- Para exibir detalhes apenas do instantâneo selecionado, clique no link que não é de alteração. 
  
  O relatório é exibido em uma janela separada.   
  
### <a name="managed-types-reports"></a>Relatórios de tipos gerenciados  
 Escolha o link atual de uma célula **Objetos (Diff)** ou **Alocações (Diff)** da tabela de resumo de Uso de Memória.  
  
 ![Relatório de tipo gerenciado pelo depurador - caminhos para a raiz](../profiling/media/dbgdiag_mem_managedtypesreport_pathstoroot.png "DBGDIAG_MEM_ManagedTypesReport_PathsToRoot")  
  
 O painel superior mostra a contagem e o tamanho dos tipos no instantâneo, incluindo o tamanho de todos os objetos referenciados pelo tipo (**inclusive tamanho**).  
  
 A árvore **Caminhos para a Raiz** no painel inferior exibe os objetos que referenciam o tipo selecionado no painel superior. O coletor de lixo .NET Framework limpa a memória de um objeto apenas quando o último tipo que faz referência a ele é liberado.  
  
 A árvore **Tipos Referenciados** exibe as referências mantidas pelo tipo selecionado no painel superior.  
  
 ![Modo de exibição de relatório Tipos referenciados gerenciados](../profiling/media/dbgdiag_mem_managedtypesreport_referencedtypes.png "DBGDIAG_MEM_ManagedTypesReport_ReferencedTypes")  
  
 Para exibir as instâncias de um tipo selecionado no painel superior, escolha o ícone ![Instância](../profiling/media/dbgdiag_mem_instanceicon.png "DBGDIAG_MEM_InstanceIcon").  
  
 ![Modo de exibição Instâncias](../profiling/media/dbgdiag_mem_managedtypesreport_instances.png "DBGDIAG_MEM_ManagedTypesReport_Instances")  
  
 O modo de exibição **Instâncias** exibe as instâncias do objeto selecionado no instantâneo no painel superior. O painel **Caminhos para Raiz** e **Objetos Referenciados** exibe os objetos que referenciam a instância selecionada e os tipos de que a instância selecionada referencia. Quando o depurador é interrompido no ponto em que o instantâneo foi tirado, você pode passar o mouse sobre a célula **Valor** para exibir os valores do objeto em uma dica de ferramenta.  
  
### <a name="native-type-reports"></a>Relatórios de tipo nativo  
 Escolha o link atual de uma célula **Alocações (Diff)** ou **Tamanho do Heap (Diff)** na tabela de resumo de Uso de Memória da janela **Ferramentas de Diagnóstico**.  
  
 ![Modo de exibição do tipo nativo](../profiling/media/dbgdiag_mem_native_typesview.png "DBGDIAG_MEM_Native_TypesView")  
  
 O **Modo de exibição de tipos** exibe o número e tamanho dos tipos no instantâneo.  
  
-   Escolha o ícone de instâncias (![O ícone de instância na coluna Tipo de Objeto](../profiling/media/dbg_mma_instancesicon.png "DBG_MMA_InstancesIcon")) de um tipo selecionado para exibir informações sobre os objetos do tipo selecionado no instantâneo.  
  
     O modo de exibição **Instâncias** mostra cada instância do tipo selecionado. A seleção de uma instância exibe a pilha de chamadas resultou na criação da instância no painel **Pilha de Chamadas de Alocação**.  
  
     ![Modo de exibição de instâncias](../profiling/media/dbgdiag_mem_native_instances.png "DBGDIAG_MEM_Native_Instances")  
  
-   Escolha **Exibição de Pilhas** na lista **Exibir Modo** para ver a pilha de alocação do tipo selecionado.  
  
     ![Exibição de Pilhas](../profiling/media/dbgdiag_mem_native_stacksview.png "DBGDIAG_MEM_Native_StacksView")  
  
### <a name="change-diff-reports"></a>Relatórios de comparação (Diff)  
  
- Escolha o link de alteração em uma célula da tabela de resumo da guia **Uso de Memória** na janela **Ferramentas de Diagnóstico**.  
  
   ![Escolher um relatório de comparação](../profiling/media/dbgdiag_mem_choosediffreport.png "DBGDIAG_MEM_ChooseDiffReport")  
  
- Escolha um instantâneo na lista **Comparar com** de um relatório gerenciado ou nativo.  
  
   ![Escolher um instantâneo na lista Comparar com](../profiling/media/dbgdiag_mem_choosecompareto.png "DBGDIAG_MEM_ChooseCompareTo")  
  
  O relatório de comparação adiciona colunas (marcadas com **(Diff)**) ao relatório base que mostra a diferença entre o valor do instantâneo base e o do instantâneo de comparação. Veja como pode ser a aparência de um relatório de comparação Exibição de Tipo Nativo:  
  
  ![Exibição de comparação de tipos nativos](../profiling/media/dbgdiag_mem_native_typesviewdiff.png "DBGDIAG_MEM_Native_TypesViewDiff")  
  
## <a name="blogs-and-videos"></a>Blogs e vídeos  

| | |
|---------|---------|
| ![ícone de câmera para vídeo](../install/media/video-icon.png "Assistir a um vídeo") | [Assista a um vídeo](https://mva.microsoft.com/en-US/training-courses-embed/getting-started-with-visual-studio-2017-17798/Profiling-with-Diagnostics-Tools-in-Visual-Studio-2017-daHnzMD6D_9211787171) sobre como usar as ferramentas de diagnóstico que mostra como analisar o uso de memória e o uso de CPU no Visual Studio 2017. |

 [Analyze CPU and Memory While Debugging](https://blogs.msdn.microsoft.com/visualstudio/2016/02/15/analyze-cpu-memory-while-debugging/) (Analisar a CPU e a memória durante a depuração)  
  
 [Visual C++ Blog: Memory Profiling in Visual C++ 2015](https://blogs.msdn.microsoft.com/vcblog/2015/10/21/memory-profiling-in-visual-c-2015/) (Blog do Visual C++: Criação de perfil de memória no Visual C++ 2015)  

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como coletar e analisar dados de uso da memória. Se você já concluiu o [tour do criador de perfil](../profiling/profiling-feature-tour.md), obtenha uma visão geral de como analisar o uso de CPU em seus aplicativos.

> [!div class="nextstepaction"]
> [Analisar o uso de CPU](../profiling/beginners-guide-to-performance-profiling.md) 