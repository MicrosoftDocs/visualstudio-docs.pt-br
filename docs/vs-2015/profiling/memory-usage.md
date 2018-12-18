---
title: Uso da memória | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bbb58d6c-3362-4ca3-8e87-64b2d4415bf6
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f62137fcbc71df87fb0569ed0516a7ae36d8a30a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51746200"
---
# <a name="memory-usage"></a>Uso de Memória
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Encontre vazamentos de memória e memória ineficiente enquanto estiver depurando com a ferramenta de diagnóstico **Uso de Memória** integrada ao depurador. A ferramenta Uso de Memória permite que você tire um ou mais *instantâneos* do heap de memória gerenciada e do heap de memória nativa. Você pode coletar instantâneos de aplicativos .NET, nativos ou mistos (.NET e nativos).  
  
- É possível analisar um único instantâneo para compreender o impacto relativo dos tipos de objeto sobre o uso da memória e encontrar o código no aplicativo que usa a memória de maneira ineficiente.  
  
- Também é possível comparar (diff) dois instantâneos de um aplicativo para encontrar áreas no código que causam o aumento do uso da memória com o passar do tempo.  
  
  O gráfico a seguir mostra a janela **Ferramentas de Diagnóstico** no Visual Studio 2015 Atualização 1:  
  
  ![DiagnosticTools&#45;Update1](../profiling/media/diagnostictools-update1.png "DiagnosticTools-Update1")  
  
  Embora você possa coletar instantâneos de memória a qualquer momento na ferramenta **Uso de Memória**, pode usar o depurador do Visual Studio para controlar como o seu aplicativo é executado ao investigar problemas de desempenho. A definição de pontos de interrupção, passo a passo, Interromper Tudo e outras ações de depurador podem ajudá-lo a concentrar as investigações de desempenho nos caminhos de código mais relevantes. A execução dessas ações enquanto o aplicativo é executado pode eliminar o ruído do código que não lhe interessa e reduzir significativamente a quantidade de tempo que leva para diagnosticar um problema.  
  
  Você também pode usar a ferramenta de memória fora do depurador. Confira [Uso de memória sem depuração](http://msdn.microsoft.com/library/8883bc5f-df86-4f84-aa2b-a21150f499b0).  
  
> [!NOTE]
>  **Suporte de alocador personalizado** O criador de perfil de memória nativa funciona com a coleta de dados de evento [ETW](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) de alocação emitidos durante o tempo de execução.  Os alocadores no CRT e no SDK do Windows foram anotados no nível de origem para que seus dados de alocação possam ser capturados.  Se você estiver escrevendo seus próprios alocadores, todas as funções que retornam um ponteiro para um heap de memória recém-alocada poderão ser decoradas com [declspec](http://msdn.microsoft.com/library/832db681-e8e1-41ca-b78c-cd9d265cdb87)(allocator), como visto neste exemplo de myMalloc:  
>   
>  `__declspec(allocator) void* myMalloc(size_t size)`  
  
## <a name="analyze-memory-use-with-the-debugger"></a>Analisar o uso da memória com o depurador  
  
> [!NOTE]
>  Como a coleta de dados de memória pode afetar o desempenho de depuração de seus aplicativos mistos ou nativos, os instantâneos de memória são desabilitados por padrão. Para habilitar instantâneos de aplicativos mistos ou nativos, inicie uma sessão de depuração (Tecla de atalho: **F5**). Quando a janela **Ferramentas de Diagnóstico** é exibida, escolha a guia Uso de Memória e escolha **Habilitar instantâneos**.  
>   
>  ![Habilitar instantâneos](../profiling/media/dbgdiag-mem-mixedtoolbar-enablesnapshot.png "DBGDIAG_MEM_MixedToolbar_EnableSnapshot")  
>   
>  Pare (Tecla de atalho: **Shift+F5**) e reinicie a depuração.  
  
 Sempre que você deseja capturar o estado da memória, escolha **Tirar instantâneo** na barra de ferramentas de resumo **Uso de Memória**.  
  
 ![Tirar instantâneo](../profiling/media/dbgdiag-mem-mixedtoolbar-takesnapshot.png "DBGDIAG_MEM_MixedToolbar_TakeSnapshot")  
  
> [!TIP]
> - Para criar uma linha de base para comparações de memória, tire um instantâneo no início da sessão de depuração.  
>   -   Como pode ser um desafio capturar o perfil de memória de uma operação de seu interesse quando o aplicativo aloca e desaloca memória com frequência, defina pontos de interrupção no início e no final da operação ou percorra a operação para localizar o ponto exato em que a memória foi alterada.  
  
## <a name="viewing-memory-snapshot-details"></a>Exibindo detalhes do instantâneo de memória  
 As linhas da tabela de resumo Uso de Memória lista os instantâneos que você fez durante a sessão de depuração.  
  
 As colunas da linha dependem do modo de depuração escolhido nas propriedades do projeto: .NET, nativo ou misto (.NET e nativo).  
  
- As colunas **Objetos Gerenciados** e **Alocações Nativas** exibem o número de objetos nas memórias .NET e nativa quando o instantâneo foi tirado.  
  
- As colunas **Tamanho de Heap Gerenciado** e **Tamanho de Heap Nativo** exibem o número de bytes nos heaps .NET e nativos  
  
- Quando você tira vários instantâneos, as células da tabela de resumo incluem a alteração no valor entre o instantâneo de linha e o instantâneo anterior.  
  
   ![Célula da tabela de resumo de memória](../profiling/media/dbgdiag-mem-summarytablecell.png "DBGDIAG_MEM_SummaryTableCell")  
  
  **Para exibir um relatório de detalhes:**  
  
- Para exibir detalhes apenas do instantâneo selecionado, escolha o link atual.  
  
- Para exibir detalhes da diferença entre o instantâneo atual e o instantâneo anterior, escolha o link de alteração.  
  
  O relatório é exibido em uma janela separada.  
  
## <a name="memory-usage-details-reports"></a>Relatórios de detalhes Uso de Memória  
  
### <a name="managed-types-reports"></a>Relatórios de tipos gerenciados  
 Escolha o link atual de uma célula **Objetos Gerenciados** ou **Tamanho de Heap Gerenciado** da tabela de resumo Uso de Memória.  
  
 ![Relatório de tipo gerenciado pelo depurador - caminhos para a raiz](../profiling/media/dbgdiag-mem-managedtypesreport-pathstoroot.png "DBGDIAG_MEM_ManagedTypesReport_PathsToRoot")  
  
 O painel superior mostra a contagem e o tamanho dos tipos no instantâneo, incluindo o tamanho de todos os objetos referenciados pelo tipo (**inclusive tamanho**).  
  
 A árvore **Caminhos para a Raiz** no painel inferior exibe os objetos que referenciam o tipo selecionado no painel superior. O coletor de lixo .NET Framework limpa a memória de um objeto apenas quando o último tipo que faz referência a ele é liberado.  
  
 A árvore **Tipos Referenciados** exibe as referências mantidas pelo tipo selecionado no painel superior.  
  
 ![Modo de exibição de relatório Tipos referenciados gerenciados](../profiling/media/dbgdiag-mem-managedtypesreport-referencedtypes.png "DBGDIAG_MEM_ManagedTypesReport_ReferencedTypes")  
  
 Para exibir as instâncias de um tipo selecionado no painel superior, escolha o ícone ![Instância](../profiling/media/dbgdiag-mem-instanceicon.png "DBGDIAG_MEM_InstanceIcon").  
  
 ![Modo de exibição Instâncias](../profiling/media/dbgdiag-mem-managedtypesreport-instances.png "DBGDIAG_MEM_ManagedTypesReport_Instances")  
  
 O modo de exibição **Instâncias** exibe as instâncias do objeto selecionado no instantâneo no painel superior. O painel Caminhos para Raiz e Objetos Referenciados exibem os objetos que fazem referência à instância selecionada e os tipos referenciados pela instância selecionada. Quando o depurador é interrompido no ponto em que o instantâneo foi tirado, você pode passar o mouse sobre a célula Valor para exibir os valores do objeto em uma dica de ferramenta.  
  
### <a name="native-type-reports"></a>Relatórios de tipo nativo  
 Escolha o link atual da célula **Alocações Nativas** ou **Tamanho de Heap Nativo** na tabela de resumo Uso de Memória da janela **Ferramentas de Diagnóstico**.  
  
 ![Modo de exibição do tipo nativo](../profiling/media/dbgdiag-mem-native-typesview.png "DBGDIAG_MEM_Native_TypesView")  
  
 O **Modo de exibição de tipos** exibe o número e tamanho dos tipos no instantâneo.  
  
-   Escolha o ícone de instâncias (![O ícone de instância na coluna Tipo de Objeto](../misc/media/dbg-mma-instancesicon.png "DBG_MMA_InstancesIcon")) de um tipo selecionado para exibir informações sobre os objetos do tipo selecionado no instantâneo.  
  
     O modo de exibição **Instâncias** mostra cada instância do tipo selecionado. A seleção de uma instância exibe a pilha de chamadas resultou na criação da instância no painel **Pilha de Chamadas de Alocação**.  
  
     ![Modo de exibição de instâncias](../profiling/media/dbgdiag-mem-native-instances.png "DBGDIAG_MEM_Native_Instances")  
  
-   Escolha **Exibição de Pilhas** na lista **Exibir Modo** para ver a pilha de alocação do tipo selecionado.  
  
     ![Exibição de Pilhas](../profiling/media/dbgdiag-mem-native-stacksview.png "DBGDIAG_MEM_Native_StacksView")  
  
### <a name="change-diff-reports"></a>Relatórios de comparação (Diff)  
  
- Escolha o link de alteração em uma célula da tabela de resumo da guia **Uso de Memória** na janela **Ferramentas de Diagnóstico**.  
  
   ![Escolher um relatório de comparação](../profiling/media/dbgdiag-mem-choosediffreport.png "DBGDIAG_MEM_ChooseDiffReport")  
  
- Escolha um instantâneo na lista **Comparar com** de um relatório gerenciado ou nativo.  
  
   ![Escolher um instantâneo na lista Comparar com](../profiling/media/dbgdiag-mem-choosecompareto.png "DBGDIAG_MEM_ChooseCompareTo")  
  
  O relatório de comparação adiciona colunas (marcadas com **(Diff)**) ao relatório base que mostra a diferença entre o valor do instantâneo base e o do instantâneo de comparação. Veja como o relatório de comparação Exibição de Tipo Nativo pode se parecer:  
  
  ![Exibição de comparação de tipos nativos](../profiling/media/dbgdiag-mem-native-typesviewdiff.png "DBGDIAG_MEM_Native_TypesViewDiff")  
  
## <a name="blogs-and-videos"></a>Blogs e vídeos  
 [Janela do depurador Ferramentas de Diagnóstico no Visual Studio 2015](http://blogs.msdn.com/b/visualstudioalm/archive/2015/01/16/diagnostic-tools-debugger-window-in-visual-studio-2015.aspx)  
  
 [Blog: Ferramenta Uso de Memória durante a depuração no Visual Studio 2015](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/13/memory-usage-tool-while-debugging-in-visual-studio-2015.aspx)  
  
 [Blog do Visual C++: Diagnóstico de Memória Nativa na visualização do VS2015](http://blogs.msdn.com/b/vcblog/archive/2014/11/21/native-memory-diagnostics-in-vs2015-preview.aspx)  
  
 [Blog do Visual C++: Ferramentas de Diagnóstico de Memória Nativa para Visual Studio 2015 CTP](http://blogs.msdn.com/b/vcblog/archive/2014/06/04/native-memory-diagnostic-tools-for-visual-studio-14-ctp1.aspx)




