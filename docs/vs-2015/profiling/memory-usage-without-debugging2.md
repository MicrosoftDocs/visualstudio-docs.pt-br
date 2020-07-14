---
title: Uso de memória sem depuração2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 24238fc0-40b8-4079-8579-698211db9a26
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ce7d30b66106b8d0d861fcf782a77ee7f461196b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85532035"
---
# <a name="memory-usage-without-debugging"></a>Uso de memória sem depuração
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar a ferramenta **Uso de Memória** sem depuração para fazer o seguinte  
  
- Monitorar o uso de memória do seu aplicativo diretamente no Visual Studio enquanto estiver desenvolvendo um cenário.  
  
- Criar instantâneos detalhados do estado de memória do seu aplicativo.  
  
- Comparar instantâneos para encontrar a causa raiz de problemas de memória.  
  
  Este tópico descreve como usar a ferramenta Uso de Memória para analisar um aplicativo XAML universal do Windows. Se você quiser analisar o uso de memória em aplicativos universais do Windows que usam JavaScript e HTML, consulte [Analisar o uso de memória (JavaScript)](https://msdn.microsoft.com/library/windows/apps/jj819176.aspx).  
  
## <a name="start-a-memory-usage-diagnostic-session"></a><a name="BKMK_Start_a_Memory_Usage_diagnostic_session"></a>Iniciar uma sessão de diagnóstico de uso de memória  
  
1. Abra um projeto universal do Windows em C# no Visual Studio.  
  
2. Na barra de menus, escolha **Depurar/Criador de Perfil de Desempenho...**.  
  
3. Selecione **Uso de Memória** e, em seguida, escolha o botão **Iniciar** na parte inferior da página.  
  
     ![Iniciar uma a sessão de diagnóstico de uso de memória](../profiling/media/memuse-start-diagnosticssession.png "MEMUSE_Start_DiagnosticsSession")  
  
## <a name="monitor-memory-use"></a><a name="BKMK_Monitor_memory_use"></a>Monitorar o uso da memória  
 Embora você possa usar a ferramenta **Uso de Memória** para gerar relatórios detalhados que podem ser usados para encontrar e corrigir problemas, você também pode usá-la para estudar os efeitos de memória em tempo real de um cenário que esteja desenvolvendo ativamente.  
  
 Quando você inicia uma sessão de diagnóstico, seu aplicativo é iniciado e a janela **Ferramentas de Diagnóstico** mostra um gráfico de linha do tempo do uso de memória do aplicativo.  
  
 ![Página de visão geral de uso de memória](../profiling/media/memuse-reportoverview.png "MEMUSE__ReportOverview")  
  
 O gráfico de linha do tempo mostra flutuações na memória do seu aplicativo, conforme ele é executado. Picos no gráfico geralmente indicam que um código está coletando ou criando dados e, em seguida, descartando-os quando o processamento é concluído. Grandes picos indicam áreas que você pode otimizar. O que mais preocupa é o aumento no consumo de memória que não é devolvido, pois pode indicar uso de memória ineficiente ou mesmo uma perda de memória.  
  
### <a name="close-a-monitoring-session"></a><a name="BKMK_Close_a_monitoring_session"></a> Fechar uma sessão de monitoramento  
 ![Parar coleta](../profiling/media/memuse-stopcollection.png "MEMUSE__StopCollection")  
  
 Para parar uma sessão de monitoramento sem criar um relatório, apenas feche a janela de diagnóstico. Para gerar um relatório quando você tiver tirado instantâneos de memória, escolha **Parar**.  
  
## <a name="take-snapshots-of-the-memory-state-of-your-app"></a><a name="BKMK_Take_snapshots_to_analyze_the_memory_state_of_your_app"></a> Tirar instantâneos do estado de memória do aplicativo  
 Se você descobrir um problema de memória que deseja investigar, será possível tirar instantâneos durante a sessão de diagnóstico para capturar objetos na memória em momentos específicos. Como o aplicativo usa uma grande variedade de tipos de objetos, talvez você queira concentrar sua análise em um cenário. Também é uma boa ideia obter um instantâneo de linha de base do aplicativo antes de aparecer um problema de memória, outro instantâneo após a primeira ocorrência do problema e um ou mais instantâneos adicionais se você puder repetir o cenário.  
  
 Para a coleta de instantâneos, inicie uma nova sessão de diagnóstico. Escolha **Tirar Instantâneo** quando quiser capturar os dados da memória. Para gerar um relatório, escolha **Parar**.  
  
## <a name="memory-usage-overview-page"></a><a name="BKMK_Memory_Usage_overview_page"></a>Página Visão geral de uso de memória  
 Depois de parar a coleta de dados, a ferramenta Uso de Memória para o aplicativo e exibe o relatório geral.  
  
 ![Página de visão geral de uso de memória](../profiling/media/memuse-reportoverview.png "MEMUSE__ReportOverview")  
  
### <a name="memory-usage-snapshot-views"></a><a name="BKMK_Memory_Usage_snapshot_views"></a> Exibições de instantâneo do uso de memória  
 Você usa as exibições de instantâneos para abrir relatórios detalhados em novas janelas do Visual Studio. Há dois tipos de exibições de instantâneos:  
  
- Um [Relatório de detalhes do instantâneo](../profiling/memory-usage-without-debugging2.md#BKMK_Snapshot_details_reports) mostra os tipos e as instâncias em um instantâneo.  
  
- Um [Relatório de diferenças (dif) do instantâneo](../profiling/memory-usage-without-debugging2.md#BKMK_Snapshot_difference__diff__reports) compara os tipos e as instâncias em dois instantâneos.  
  
  ![Links de exibição do instantâneo](../profiling/media/memuse-snapshotview-numbered.png "MEMUSE__SnapshotView_Numbered")  
  
  Os itens numerados na imagem de exibição do instantâneo são links que abrem exibições de relatório de uso de memória.  
  
|Imagem|Descrição|  
|-|-|  
|![Etapa 1](../profiling/media/procguid-1.png "ProcGuid_1")|O texto do link mostra o número total de bytes na memória quando o instantâneo foi tirado.<br /><br /> Selecione esse link para exibir um relatório de detalhes do instantâneo, que é classificado pelo tamanho total de instâncias do tipo.|  
|![Etapa 2](../profiling/media/procguid-2.png "ProcGuid_2")|O texto do link mostra o número total de objetos na memória quando o instantâneo foi tirado.<br /><br /> Selecione esse link para exibir um relatório de detalhes do instantâneo, que é classificado pela contagem de instâncias dos tipos.|  
|![Etapa 3](../profiling/media/procguid-3.png "ProcGuid_3")|O texto do link mostra a diferença entre o tamanho total de objetos na memória no momento desse instantâneo e o tamanho total do instantâneo anterior.<br /><br /> O texto do link é um número positivo quando o tamanho da memória desse instantâneo for maior do que o anterior, e um número negativo quando o tamanho for menor. O texto do link **Linha de Base** indica que esse instantâneo é o primeiro na sessão de diagnóstico, **Nenhuma Diferença** indica que a diferença é igual a zero.<br /><br /> Escolha esse link para exibir um relatório diferente do instantâneo, que é classificado pela diferença no tamanho total das instâncias dos tipos.|  
|![Etapa 4](../profiling/media/procguid-4.png "ProcGuid_4")|O texto do link mostra a diferença entre o tamanho total de objetos de memória nesse instantâneo e o número de objetos no instantâneo anterior.<br /><br /> Escolha esse link para exibir um relatório diferente do instantâneo, que é classificado pela diferença na contagem total das instâncias dos tipos.|  
  
## <a name="snapshot-reports"></a><a name="BKMK_Snapshot_reports"></a> Relatórios de instantâneos  
 ![Relatório de instantâneo de uso de memória](../profiling/media/memuse-snapshotreport-all.png "MEMUSE_SnapshotReport_All")  
  
### <a name="snapshot-report-trees"></a><a name="BKMK_Snapshot_report_trees"></a> Árvores de relatórios de instantâneos  
  
#### <a name="managed-heap"></a><a name="BKMK_Managed_Heap"></a> Heap Gerenciado  
 A árvore de heap gerenciado [Árvore de Heap Gerenciado (detalhes do instantâneo)](../profiling/memory-usage-without-debugging2.md#BKMK_Managed_Heap_tree__Snapshot_details_) e a [Árvore de Heap Gerenciado (diferenças de instantâneo)](../profiling/memory-usage-without-debugging2.md#BKMK_Managed_Heap_tree__Snapshot_diff_) mostram os tipos e instâncias no relatório. Escolher um tipo ou instância exibe as árvores **Caminhos para a Raiz** e **Objetos Referenciados** para o item selecionado.  
  
#### <a name="paths-to-root"></a><a name="BKMK_Paths_to_Root"></a>Caminhos para a raiz  
 A [Árvore de Caminhos para a Raiz (detalhes do instantâneo)](../profiling/memory-usage-without-debugging2.md#BKMK_Paths_to_Root_tree__Snapshot_details_) e os [Árvore de Caminhos para a Raiz (diferenças do instantâneo)](../profiling/memory-usage-without-debugging2.md#BKMK_Paths_to_Root_tree__Snapshot_diff_) mostram uma cadeia de objetos que fazem referência ao tipo ou instância. O coletor de lixo .NET Framework limpa a memória de um objeto apenas quando todas as referências a ele foram liberadas.  
  
#### <a name="referenced-objects"></a><a name="BKMK_Referenced_Objects"></a> Objetos Referenciados  
 A [Árvore de Objetos Referenciados (detalhes do instantâneo)](../profiling/memory-usage-without-debugging2.md#BKMK_Referenced_Objects_tree__Snapshot_details_) e a [Árvore de Objetos Referenciados (diferenças do instantâneo)](../profiling/memory-usage-without-debugging2.md#BKMK_Referenced_Objects_tree__Snapshot_diff_) mostram os objetos aos quais o tipo ou instância selecionada faz referência.  
  
### <a name="object-type-and-instance-fields"></a><a name="BKMK_Object_Type_and_Instance_fields"></a> Campos Tipo de Objeto e Instância  
 Quando uma entrada **Tipo de Objeto** tem entradas filho, você pode escolher o ícone de seta para exibi-las. Se a cor do texto do **Tipo de Objeto** for azul, você poderá escolhê-lo para navegar para o objeto em seu arquivo de código-fonte. O arquivo de origem é aberto em uma janela separada.  
  
 Os nomes de instância são IDs exclusivas geradas pela ferramenta Uso de Memória.  
  
 Se você notar um tipo que não pode ser identificado facilmente ou se não souber como ele está envolvido no código, provavelmente, é um objeto do .NET Framework, do sistema operacional ou do compilador que a ferramenta Uso de Memória exibe porque está envolvido nas cadeias de propriedade de seus objetos.  
  
### <a name="report-tree-filters"></a><a name="BKMK_Report_tree_filters_"></a> Filtros da árvore de relatórios  
 A maioria dos aplicativos contém um número surpreendentemente grande de tipos, a maioria dos quais não são muito interessantes para o desenvolvedor do aplicativo. A ferramenta **Uso de Memória** define dois filtros que podem ser usados ​​para ocultar a maioria desses tipos nas árvores de **Heap Gerenciado** e **Caminhos para a Raiz**. Você também pode filtrar uma árvore pelo nome do tipo.  
  
 ![Opções de classificação e filtro](../profiling/media/memuse-sortandfilter.png "MEMUSE_SortAndFilter")  
  
#### <a name="filter"></a><a name="BKMK_Filter"></a>Sem  
 Digite uma cadeia de caracteres na caixa **Filtrar** para restringir as exibições de árvore a tipos que contêm o texto especificado. O filtro não diferencia maiúsculas de minúsculas e reconhece a cadeia de caracteres especificada em qualquer parte dos nomes do tipo.  
  
#### <a name="collapse-small-objects"></a><a name="BKMK_Collapse_Small_Objects"></a> Recolher pequenos objetos  
 Quando esse filtro é aplicado, os tipos cujo **Tamanho (Bytes)** é inferior a 0,5% do tamanho total da memória do instantâneo são escondidos na lista **Heap Gerenciado**.  
  
#### <a name="just-my-code"></a><a name="BKMK_Just_My_Code"></a>Apenas Meu Código  
 O filtro **Apenas Meu Código** oculta a maioria das instâncias geradas pelo código externo. Tipos externos são de propriedade do sistema operacional, de componentes do Framework ou gerados pelo compilador.  
  
## <a name="snapshot-details-reports"></a><a name="BKMK_Snapshot_details_reports"></a> Relatórios de detalhes do instantâneo  
 Você usa um relatório de detalhes do instantâneo para se concentrar em um instantâneo de uma sessão de diagnóstico. Para abrir um relatório de detalhes, escolha um dos links em uma exibição de instantâneo, como mostrado na figura a seguir. Os dois links abrem o mesmo relatório, a única diferença é a ordem de classificação inicial da árvore **Heap Gerenciado** no relatório. Em ambos os casos, você pode mudar a ordem de classificação depois que o relatório abre.  
  
 ![Links para o relatório de instantâneo em uma exibição de instantâneo](../profiling/media/memuse-snapshotview-snapshotdetailslinks.png "MEMUSE_SnapshotView_SnapshotDetailsLinks")  
  
- O link **MB** classifica o relatório pela coluna **Tamanho Inclusivo (Bytes)**.  
  
- O link **objetos** classifica o relatório pela coluna **Contagem**.  
  
### <a name="managed-heap-tree-snapshot-details"></a><a name="BKMK_Managed_Heap_tree__Snapshot_details_"></a> Árvore de Heap Gerenciado (detalhes do instantâneo)  
 A árvore **Heap Gerenciado** lista os tipos de objetos que são mantidos na memória. Você pode expandir um nome do tipo para ver as dez maiores instâncias do tipo, classificadas por tamanho. Escolher um tipo ou instância exibe as árvores **Caminhos para a Raiz** e **Objetos Referenciados** para o item selecionado.  
  
 ![Árvore de heap gerenciada](../profiling/media/memuse-snapshotdetails-managedheaptree.png "MEMUSE__SnapshotDetails_ManagedHeapTree")  
  
|Nome|Descrição|  
|-|-|  
|**Tipo de Objeto**|O nome do tipo ou instância de objeto.|  
|**Count**|O número de instâncias do objeto do tipo. O número é sempre 1 para uma instância.|  
|**Tamanho (Bytes)**|No caso de um tipo, o tamanho de todas as instâncias do tipo no instantâneo de memória, excluindo o tamanho dos objetos contidos nas instâncias.<br /><br /> No caso de uma instância, o tipo, o tamanho do objeto excluindo o tamanho dos objetos contidos na instância. instâncias.|  
|**Tamanho Inclusivo (Bytes)**|O tamanho das instâncias do tipo ou o tamanho de uma única instância, incluindo o tamanho dos objetos contidos.|  
  
### <a name="paths-to-root-tree-snapshot-details"></a><a name="BKMK_Paths_to_Root_tree__Snapshot_details_"></a> Árvore de Caminhos para a Raiz (detalhes do instantâneo)  
 A **árvore de Caminhos para a Raiz** mostra a cadeia de objetos que faz referência ao tipo ou instância. O coletor de lixo .NET Framework limpa a memória de um objeto apenas quando todas as referências a ele foram liberadas.  
  
 ![Caminhos para a árvore raiz para tipos](../profiling/media/memuse-snapshotdetails-type-pathstoroottree.png "MEMUSE_SnapshotDetails_Type_PathsToRootTree")  
  
 Ao exibir um tipo na árvore de **Caminhos para a Raiz**, o número de objetos dos tipos que têm referências a esse tipo é exibido na coluna **Contagem de Referência**. A coluna não aparece quando você analisa uma instância.  
  
### <a name="referenced-objects-tree-snapshot-details"></a><a name="BKMK_Referenced_Objects_tree__Snapshot_details_"></a> Árvore de Objetos Referenciados (detalhes do instantâneo)  
 A árvore de **Objetos Referenciados** mostra os objetos que mencionam o tipo ou a instância escolhida.  
  
 ![Árvore Objjects referenciada para instâncias](../profiling/media/memuse-snapshotdetails-referencedobjects-instance.png "MEMUSE_SnapshotDetails_ReferencedObjects_Instance")  
  
|Nome|Descrição|  
|-|-|  
|**Tipo/Instância de Objeto**|O nome do tipo ou instância de objeto.|  
|**Tamanho (Bytes)**|No caso de um tipo, o tamanho de todas as instâncias do tipo, excluindo o tamanho dos objetos contidos no tipo.<br /><br /> No caso de uma instância, o tamanho do objeto, excluindo o tamanho dos objetos contidos no objeto.|  
|**Tamanho Inclusivo (Bytes)**|O tamanho total das instâncias do tipo ou o tamanho da instância, incluindo o tamanho dos objetos contidos.|  
  
## <a name="snapshot-difference-diff-reports"></a><a name="BKMK_Snapshot_difference__diff__reports"></a> Relatórios de diferenças (dif) do instantâneo  
 O relatório de diferença (dif) do instantâneo mostra as mudanças entre um instantâneo primário e o instantâneo que foi tirado imediatamente antes dele. Para abrir um relatório de diferença, escolha um dos links em uma exibição de instantâneo, como mostrado na figura a seguir. Os dois links abrem o mesmo relatório, a única diferença é a ordem de classificação inicial da árvore **Heap Gerenciado** no relatório. Você pode mudar a ordem de classificação depois que o relatório abre.  
  
 ![Links para o relatório de diferenças em uma exibição de instantâneo](../profiling/media/memuse-snapshotview-snapshotdifflinks.png "MEMUSE_SnapshotView_SnapshotDiffLinks")  
  
- O link **MB** classifica o relatório pela coluna **Tamanho Inclusivo (Bytes)**.  
  
- O link **objetos** classifica o relatório pela coluna **Contagem**.  
  
### <a name="managed-heap-tree-snapshot-diff"></a><a name="BKMK_Managed_Heap_tree__Snapshot_diff_"></a> Árvore de Heap Gerenciado (diferenças de instantâneo)  
 A árvore **Heap Gerenciado** lista os tipos de objetos que são mantidos na memória. Você pode expandir um nome do tipo para ver as dez maiores instâncias do tipo, classificadas por tamanho. Escolher um tipo ou instância exibe as árvores **Caminhos para a Raiz** e **Objetos Referenciados** para o item selecionado.  
  
 ![Árvore de heap gerenciada para um tipo no relatório de diferenças](../profiling/media/memuse-snapshotdiff-type-heap.png "MEMUSE_SnapshotDiff_Type_Heap")  
  
 Observe que as colunas **Contagem**, **Tamanho (Bytes)** e **Tamanho Inclusivo (Bytes)** foram recolhidas na imagem.  
  
|Nome|Descrição|  
|-|-|  
|**Tipo de Objeto**|O nome do tipo ou instância de objeto.|  
|**Count**|O número de instâncias de um tipo no instantâneo primário. **Count** é sempre 1 para uma instância.|  
|**Dif. de Contagem**|No caso de um tipo, a diferença no número de instâncias do tipo entre o instantâneo primário e o instantâneo anterior. O campo fica em branco no caso de uma instância.|  
|**Tamanho (Bytes)**|O tamanho dos objetos no instantâneo primário, excluindo o tamanho dos objetos contidos nos objetos. No caso de um tipo, **Tamanho (Bytes)** e **Tamanho Inclusivo (Bytes)** são os totais dos tamanhos das instâncias de tipo.|  
|**Dif. de Tamanho Total (Bytes)**|No caso de um tipo, a diferença no tamanho total de instâncias do tipo entre o instantâneo primário e o instantâneo anterior, excluindo o tamanho dos objetos contidos nas instâncias. O campo fica em branco no caso de uma instância.|  
|**Tamanho Inclusivo (Bytes)**|O tamanho dos objetos no instantâneo primário, incluindo o tamanho dos objetos contidos nos objetos.|  
|**Diferença de Tamanho Inclusivo (Bytes)**|No caso de um tipo, a diferença no tamanho de todas as instâncias do tipo entre o instantâneo primário e o instantâneo anterior, incluindo o tamanho dos objetos contidos nos objetos. O campo fica em branco no caso de uma instância.|  
  
### <a name="paths-to-root-tree-snapshot-diff"></a><a name="BKMK_Paths_to_Root_tree__Snapshot_diff_"></a> Árvore de Caminhos para a Raiz (diferenças do instantâneo)  
 A **árvore de Caminhos para a Raiz** mostra a cadeia de objetos que faz referência ao tipo ou instância. O coletor de lixo .NET Framework limpa a memória de um objeto apenas quando todas as referências a ele foram liberadas.  
  
 ![Caminhos para a árvore raiz para instâncias em uma exibição de comparação](../profiling/media/memuse-snapshotdiff-pathstoroot-instance-all.png "MEMUSE_SnapshotDiff_PathsToRoot_Instance_All")  
  
### <a name="referenced-objects-tree-snapshot-diff"></a><a name="BKMK_Referenced_Objects_tree__Snapshot_diff_"></a> Árvore de Objetos Referenciados (diferenças do instantâneo)  
 A árvore de **Objetos Referenciados** mostra a cadeia de objetos que mencionam o tipo primário ou a instância.  
  
 ![Árvore Objjects referenciada para instâncias](../profiling/media/memuse-snapshotdetails-referencedobjects-instance.png "MEMUSE_SnapshotDetails_ReferencedObjects_Instance")  
  
|Nome|Descrição|  
|-|-|  
|**Tipo/Instância de Objeto**|O nome do tipo ou instância de objeto.|  
|**Tamanho (Bytes)**|No caso de uma instância, o tamanho do objeto no instantâneo primário, excluindo o tamanho dos objetos contidos na instância.<br /><br /> No caso de um tipo, o tamanho total das instâncias do tipo no instantâneo primário, excluindo o tamanho dos objetos contidos na instância.|  
|**Tamanho Inclusivo (Bytes)**|O tamanho dos objetos no instantâneo primário, incluindo o tamanho dos objetos contidos nos objetos.|  
  
## <a name="see-also"></a>Consulte Também  
 [Memória JavaScript](../profiling/javascript-memory.md)   
 [Analisar o desempenho do aplicativo](https://msdn.microsoft.com/library/58acb30b-8428-41a6-b195-b0fdedb89575)   
 [Executar ferramentas de desempenho e diagnóstico](https://msdn.microsoft.com/library/788279d8-f56b-40a0-9bef-facc3dfba471)   
 [Práticas recomendadas de desempenho para aplicativos da Windows Store usando C++, C# e Visual Basic](https://msdn.microsoft.com/library/windows/apps/hh750313.aspx)   
 [Diagnosing memory issues with the new Memory Usage Tool in Visual Studio](https://devblogs.microsoft.com/devops/diagnosing-memory-issues-with-the-new-memory-usage-tool-in-visual-studio/) (Diagnosticando problemas de memória com a nova Ferramenta de Uso de Memória no Visual Studio)
