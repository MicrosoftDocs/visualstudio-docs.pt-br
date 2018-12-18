---
title: Analisar o uso de memória sem depurar | Microsoft Docs
ms.custom: H1Hack27Feb2017
ms.date: 11/15/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4dcc5c66998501044b04e4a8265d669927e3368a
ms.sourcegitcommit: 54c65f81a138fc1e8ff1826f7bd9dcec710618cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51948927"
---
# <a name="analyze-memory-usage-without-the-debugger"></a>Analisar o uso de memória sem o depurador

A ferramenta **Uso de Memória** monitora o uso de memória do seu aplicativo. É possível usar a ferramenta para estudar os efeitos de memória em tempo real de cenários que você está desenvolvendo ativamente no Visual Studio. É possível tirar instantâneos detalhados dos estados de memória do aplicativo e compará-los para encontrar as causas raiz de problemas de memória.  
  
A ferramenta **Uso de Memória** pode ser executada com ou sem o depurador. As instruções a seguir mostram como usar a ferramenta **Uso de Memória** sem o depurador no **Criador de Perfil de Desempenho** do Visual Studio. 

>[!NOTE]
>- Para medir o uso de memória de um aplicativo .NET Core, é necessário usar a ferramenta **Uso de Memória** com o depurador. Para obter instruções, confira [Profile memory usage in Visual Studio](memory-usage.md) (Uso de memória de perfil no Visual Studio). 
>- Para analisar o uso da memória em aplicativos UWP JavaScript ou HTML, use a ferramenta [Memória do JavaScript](../profiling/javascript-memory.md) no **Criador de Perfil de Desempenho**.
  
## <a name="memory-usage-diagnostic-sessions"></a>Sessões de diagnóstico de Uso de memória  

**Para iniciar uma a sessão de diagnóstico de uso de memória:**

1. Abra um projeto UWP (Universal do Windows) em C# no Visual Studio.  
   
1. Na barra de menus, escolha **Depurar** > **Criador de Perfil de Desempenho**.  
   
1. Selecione **Uso de Memória** e, em seguida, selecione **Iniciar**.  
   
   ![Iniciar uma sessão de diagnóstico de uso de memória](../profiling/media/memuse_start_diagnosticssession.png "Iniciar uma sessão de diagnóstico de uso de memória")  
  
### <a name="monitor-memory-use"></a>Monitorar o uso de memória 

Quando você inicia uma sessão de diagnóstico, seu aplicativo é iniciado e a janela **Ferramentas de Diagnóstico** mostra um grafo de linha do tempo do uso de memória do aplicativo.  

![Página de visão geral do uso de memória](../profiling/media/memuse__reportoverview.png "MEMUSE__ReportOverview")  

O grafo de linha do tempo mostra flutuações de memória à medida que o aplicativo é executado. Picos no gráfico geralmente indicam que um código está coletando ou criando dados e, em seguida, descartando-os quando o processamento é concluído. Grandes picos indicam áreas que você pode otimizar. O que mais preocupa é o aumento no consumo de memória que não é devolvido, pois pode indicar uso de memória ineficiente ou mesmo uma perda de memória.  
  
### <a name="take-snapshots-of-app-memory-states"></a>Tirar instantâneos dos estados de memória do aplicativo 

Um aplicativo usa um grande número de objetos e talvez convenha concentrar sua análise em um cenário. Ou talvez você encontre problemas de memória a serem investigados. É possível tirar instantâneos durante uma sessão de diagnóstico para capturar o uso de memória em momentos específicos. É uma boa ideia obter um instantâneo de linha de base de um aplicativo antes de aparecer um problema de memória, outro instantâneo após a primeira ocorrência do problema e instantâneos adicionais se você puder repetir o cenário.  

Para coletar instantâneos, selecione **Tirar instantâneo** quando desejar capturar os dados de memória.  

###  <a name="BKMK_Close_a_monitoring_session"></a> Fechar a sessão de diagnóstico  

Para parar uma sessão de monitoramento sem criar um relatório, apenas feche a janela de diagnóstico. Para gerar um relatório quando você terminar de coletar ou tiver tirado instantâneos, selecione **Interromper Coleta**.  

![Interromper Coleta](../profiling/media/memuse__stopcollection.png "Interromper Coleta")  

##  <a name="memory-usage-reports"></a>Relatórios de uso de memória 

Após interromper a coleta de dados, a ferramenta **Uso de Memória** interromperá o aplicativo e exibirá a página de visão geral **Uso de Memória**.  

![Página de visão geral do uso de memória](../profiling/media/memuse__reportoverview1.png "Página de visão geral do uso de memória")  

### <a name="BKMK_Memory_Usage_snapshot_views"></a> Instantâneos do uso de memória 

Os números nos painéis **Instantâneo** mostram os bytes e objetos na memória quando cada instantâneo foi tirado e a diferença entre o instantâneo e o anterior. 

Os números são links que abrem exibições do relatório **Uso de Memória** detalhadas em novas janelas do Visual Studio. Um [relatório de detalhes do instantâneo](#snapshot-details-report) mostra os tipos e instâncias em um instantâneo. Um [relatório de comparações de diferenças de instantâneos](#snapshot-difference-diff-reports) compara os tipos e as instâncias em dois instantâneos.  
  
  ![Links de exibição do instantâneo](../profiling/media/memuse__snapshotview_numbered.png "Links de exibição do instantâneo")  
  
|||  
|-|-|  
|![Etapa 1](../profiling/media/procguid_1.png "ProcGuid_1")|O número total de bytes na memória quando o instantâneo foi tirado.<br /><br /> Selecione esse link para exibir um relatório de detalhes do instantâneo classificado pelo tamanho total de instâncias do tipo.|  
|![Etapa 2](../profiling/media/procguid_2.png "ProcGuid_2")|O número total de objetos na memória quando o instantâneo foi tirado.<br /><br /> Selecione esse link para exibir um relatório de detalhes do instantâneo classificado pela contagem de instâncias dos tipos.|  
|![Etapa 3](../profiling/media/procguid_3.png "ProcGuid_3")|A diferença entre o tamanho total de objetos de memória neste instantâneo e o instantâneo anterior. <br /><br /> Um número positivo significa que o tamanho da memória deste instantâneo é maior do que o anterior e um número negativo significa que o tamanho é menor. **Linha de base** significa que um instantâneo é o primeiro em uma sessão de diagnóstico. **Nenhuma diferença** significa que a diferença é zero.<br /><br /> Selecione esse link para exibir um relatório de diferenças de instantâneos classificado pela diferença no tamanho total das instâncias dos tipos.|  
|![Etapa 4](../profiling/media/procguid_4.png "ProcGuid_4")|A diferença entre o número total de objetos de memória neste instantâneo e no instantâneo anterior.<br /><br /> Selecione esse link para exibir um relatório de diferenças de instantâneos classificado pela diferença na contagem total de instâncias dos tipos.|  
  
## <a name="memory-usage-snapshot-reports"></a>Relatórios de instantâneo de Uso de Memória 

<a name="BKMK_Snapshot_report_trees"></a> Quando você seleciona um dos links do instantâneo na página de visão geral **Uso de Memória**, um relatório de instantâneos é aberto em uma nova página. 

![Relatório de instantâneos de Uso de Memória](../profiling/media/memuse_snapshotreport_all.png "Relatório de instantâneos de Uso de Memória")  
  
Em um relatório de instantâneos, é possível expandir entradas **Tipo de Objeto** para exibir entradas filho. Os nomes de instância são IDs exclusivas geradas pela ferramenta Uso de Memória. 

Se um **Tipo de Objeto** for azul, será possível selecioná-lo para navegar até o objeto no código-fonte, em uma janela separada.  

Os tipos que você não puder identificar ou cujo envolvimento no seu código você não entende serão provavelmente .NET Framework, sistema operacional ou objetos de compilador. A ferramenta **Uso de Memória** exibirá esses objetos se eles estiverem envolvidos nas cadeias de propriedade de seus objetos.  

No relatório de instantâneos: 

- A árvore de **Heap Gerenciado** mostra os tipos e as instâncias no relatório. Escolher um tipo ou instância exibe as árvores **Caminhos para a Raiz** e **Objetos Referenciados** para o item selecionado.  
  
- A árvore **Caminhos para a Raiz** mostra a cadeia de objetos que referenciam um tipo ou uma instância. O coletor de lixo .NET Framework limpa a memória de um objeto apenas quando todas as referências a ele foram liberadas.  
  
- A árvore **Tipos Referenciados** ou **Objetos Referenciados** mostra os objetos que a instância ou tipo selecionado referencia.  
  
###  <a name="BKMK_Report_tree_filters_"></a> Filtros da árvore de relatórios  

Muitos tipos em aplicativos não são muito interessantes para os desenvolvedores de aplicativos. Os filtros de relatório de instantâneos podem ocultar a maioria desses tipos nas árvores de **Heap Gerenciado** e **Caminhos para a Raiz**.   

![Opções de filtro e classificação](../profiling/media/memuse_sortandfilter.png "MEMUSE_SortAndFilter")  

- <a name="BKMK_Filter"></a> Para filtrar uma árvore por nome de tipo, digite o nome na caixa **Filtrar**. O filtro não diferencia maiúsculas de minúsculas e reconhece a cadeia de caracteres especificada em qualquer parte dos nomes do tipo.  
  
- <a name="BKMK_Collapse_Small_Objects"></a> Selecione **Recolher Pequenos Objetos** na lista suspenso **Filtrar** para ocultar os tipos cujo **Tamanho (bytes)** é inferior a 0,5% do total de memória.  
  
- <a name="BKMK_Just_My_Code"></a> Selecione **Apenas Meu Código** na lista suspensa **Filtrar** para ocultar a maioria das instâncias geradas pelo código externo. Tipos externos pertencem ao sistema operacional ou aos componentes de estrutura ou são gerados pelo compilador.  
  
## <a name="snapshot-details-reports"></a>Relatórios de detalhes do instantâneo  

 Um relatório de detalhes do instantâneo descreve um instantâneo de uma sessão de diagnóstico. Para abrir o relatório, selecione o link de tamanho ou de objetos em um painel de instantâneo. 

 ![Links para o relatório de instantâneos em um painel de instantâneo](../profiling/media/memuse_snapshotview_snapshotdetailslinks.png "Links para o relatório de instantâneos em um painel de instantâneo")  
  
Os dois links abrem o mesmo relatório. A única diferença é a ordem de classificação inicial da árvore de **Heap Gerenciado**. O link do tamanho classifica o relatório pela coluna **Tamanho Inclusivo (Bytes)**. O link de classifica o relatório pela coluna **Contagem**. É possível alterar a ordem ou coluna de classificação depois que o relatório é aberto.  
  
###  <a name="BKMK_Managed_Heap_tree__Snapshot_details_"></a> Árvore de Heap Gerenciado (relatórios de detalhes do instantâneo)  
 A árvore **Heap Gerenciado** lista os tipos de objetos que são mantidos na memória. Expanda um nome do tipo para exibir as dez maiores instâncias do tipo, classificadas por tamanho. Selecione um tipo ou instância para exibir as árvores **Caminhos para a Raiz** e **Objetos Referenciados** para o item selecionado.  
  
 ![Árvore de Heap Gerenciado](../profiling/media/memuse__snapshotdetails_managedheaptree.png "Árvore de Heap Gerenciado")  
  
A árvore de **Heap Gerenciado** em um relatório de detalhes do instantâneo tem as seguintes colunas:

|||  
|-|-|  
|**Tipo de objeto**|O nome do tipo ou instância de objeto.|  
|**Contagem**|O número de instâncias do objeto do tipo. **Contagem** é sempre 1 para uma instância.|  
|**Tamanho (bytes)**|No caso de um tipo, o tamanho de todas as instâncias do tipo no instantâneo, menos o tamanho dos objetos contidos nas instâncias.<br /><br /> No caso de uma instância, o tamanho do objeto, menos o tamanho dos objetos contidos na instância. |  
|**Tamanho Inclusivo (Bytes)**|O tamanho das instâncias do tipo ou o tamanho de uma única instância, incluindo o tamanho dos objetos contidos.|  
|**Módulo**|O módulo que contém o objeto.|  
  
###  <a name="BKMK_Paths_to_Root_tree__Snapshot_details_"></a> Árvore de Caminhos para a Raiz (relatórios detalhes do instantâneo)  
A **árvore Caminhos para a Raiz** mostra a cadeia de objetos que referenciam um tipo ou uma instância. O coletor de lixo .NET Framework limpa a memória de um objeto apenas quando todas as referências a ele foram liberadas.  
  
Para um tipo na árvore **Caminhos para a Raiz**, o número de objetos que têm referências para esse tipo é exibido na coluna **Contagem de Referência**. 

![Árvore de Caminhos para a Raiz para tipos](../profiling/media/memuse_snapshotdetails_type_pathstoroottree.png "Árvore de Caminhos para a Raiz para tipos")  
  
###  <a name="BKMK_Referenced_Objects_tree__Snapshot_details_"></a> Árvore de Tipos referenciados ou de Objetos referenciados (relatórios de detalhes do instantâneo)  
A árvore **Tipos Referenciados** ou **Objetos Referenciados** mostra os objetos que a instância ou tipo selecionado referencia.  
  
![Árvore de Objetos referenciados para instâncias](../profiling/media/memuse_snapshotdetails_referencedobjects_instance.png "Árvore de Objetos referenciados para instâncias")  
  
A árvore de **Tipos Referenciados** em um relatório de detalhes do instantâneo tem as seguintes colunas. Uma árvore de **Objetos Referenciados** não tem a coluna **Contagem de Referência**.

|||  
|-|-|  
|**Tipo de Objeto** ou **Instância**|O nome do tipo ou da instância.|  
|**Contagem de Referência**|No caso de tipos, o número de instâncias de objeto do tipo.|  
|**Tamanho (bytes)**|No caso de um tipo, o tamanho de todas as instâncias do tipo, menos o tamanho dos objetos contidos no tipo.<br /><br /> No caso de uma instância, o tamanho do objeto, menos o tamanho dos objetos contidos no objeto.|  
|**Tamanho Inclusivo (Bytes)**|O tamanho total das instâncias do tipo ou o tamanho da instância, incluindo o tamanho dos objetos contidos.|  
|**Módulo**|O módulo que contém o objeto.|  
  
## <a name="snapshot-difference-diff-reports"></a>Relatório de diferenças (dif) do instantâneo  

Um relatório de diferenças de instantâneos mostra as alterações entre um instantâneo primário e o instantâneo anterior. Para abrir um relatório de diferenças, selecione um dos links de diferenças em um painel de instantâneo. 

Os dois links abrem o mesmo relatório. A única diferença é a ordem de classificação inicial da árvore de **Heap Gerenciado** no relatório. O link do tamanho classifica o relatório pela coluna **Diferenças de Tamanho Inclusivo (Bytes)**. O link de objetos classifica o relatório pela coluna **Diferença de Contagem**. É possível alterar a ordem ou coluna de classificação depois que o relatório é aberto.  
  
 ![Links para o relatório de diferenças em um painel de instantâneo](../profiling/media/memuse_snapshotview_snapshotdifflinks.png "Links para o relatório de diferenças em um painel de instantâneo")  
  
###  <a name="BKMK_Managed_Heap_tree__Snapshot_diff_"></a> Árvore de Heap Gerenciado (relatórios de diferenças de instantâneos) 

 A árvore **Heap Gerenciado** lista os tipos de objetos que são mantidos na memória. Você pode expandir um nome do tipo para ver as dez maiores instâncias do tipo, classificadas por tamanho. Selecione um tipo ou instância para exibir as árvores **Caminhos para a Raiz** e **Objetos Referenciados** para o item selecionado.  
  
 ![Árvore de Heap gerenciado para um tipo no relatório de diferenças](../profiling/media/memuse_snapshotdiff_type_heap.png "Árvore de Heap gerenciado para um tipo no relatório de diferenças")  
  
A árvore de **Heap Gerenciado** em um relatório de diferenças de instantâneos tem as seguintes colunas:

|||  
|-|-|  
|**Tipo de objeto**|O nome do tipo ou instância de objeto.|  
|**Contagem**|O número de instâncias de um tipo no instantâneo primário. **Contagem** é sempre 1 para uma instância.|  
|**Dif. de Contagem**|No caso de um tipo, a diferença no número de instâncias do tipo entre o instantâneo primário e o instantâneo anterior. O campo fica em branco no caso de uma instância.|  
|**Tamanho (bytes)**|O tamanho dos objetos no instantâneo primário, menos o tamanho dos objetos nos objetos. No caso de um tipo, **Tamanho (Bytes)** e **Tamanho Inclusivo (Bytes)** são os totais dos tamanhos das instâncias de tipo.|  
|**Dif. de Tamanho Total (Bytes)**|No caso de um tipo, a diferença no tamanho total de instâncias do tipo entre o instantâneo primário e o instantâneo anterior, menos o tamanho dos objetos nas instâncias. O campo fica em branco no caso de uma instância.|  
|**Tamanho Inclusivo (Bytes)**|O tamanho dos objetos no instantâneo primário, incluindo o tamanho dos objetos nos objetos.|  
|**Diferença de Tamanho Inclusivo (Bytes)**|No caso de um tipo, a diferença no tamanho de todas as instâncias do tipo entre o instantâneo primário e o instantâneo anterior, incluindo o tamanho dos objetos nos objetos. O campo fica em branco no caso de uma instância.|  
|**Módulo**|O módulo que contém o objeto.|  
  
###  <a name="BKMK_Paths_to_Root_tree__Snapshot_diff_"></a> Árvore de Caminhos para a Raiz (relatórios de diferenças de instantâneos)  

A **árvore Caminhos para a Raiz** mostra a cadeia de objetos que referenciam um tipo ou uma instância. O coletor de lixo .NET Framework limpa a memória de um objeto apenas quando todas as referências a ele foram liberadas. 

Para um tipo na árvore **Caminhos para a Raiz**, o número de objetos que têm referências para esse tipo é exibido na coluna **Contagem de Referência**. A diferença na contagem do instantâneo anterior é a coluna **Diferença de Referência**. 

 ![Árvore de Caminhos para a raiz em um relatório de diferenças](../profiling/media/memuse_snapshotdiff_pathstoroot_instance_all.png "Árvore de Caminhos para a raiz em um relatório de diferenças")  
  
###  <a name="BKMK_Referenced_Objects_tree__Snapshot_diff_"></a> Árvore de Tipos referenciados ou de Objetos referenciados (relatórios de diferenças de instantâneos)  

A árvore **Tipos Referenciados** ou **Objetos Referenciados** mostra os objetos que a instância ou tipo selecionado referencia.  

![Tipos referenciados em um relatório de diferenças](../profiling/media/memuse_snapshotdiff_referencedtypes.png "Tipos referenciados em um relatório de diferenças")  

Uma árvore **Tipos Referenciados** em um relatório de diferenças de instantâneos tem as seguintes colunas. Uma árvore de **Objetos Referenciados** tem as colunas **Instância**, **Tamanho (Bytes)**, **Tamanho Inclusivo (Bytes)** e **Módulo**.

|||  
|-|-|  
|**Tipo de Objeto** ou **Instância**|O nome do tipo ou instância de objeto.|  
|**Contagem de Referência**|O número de instâncias de um tipo no instantâneo primário.|  
|**Diferença de Contagem de referência**|No caso de um tipo, a diferença no número de instâncias do tipo entre o instantâneo primário e o instantâneo anterior.|  
|**Tamanho (bytes)**|O tamanho dos objetos no instantâneo primário, menos o tamanho dos objetos nos objetos. No caso de um tipo, **Tamanho (Bytes)** e **Tamanho Inclusivo (Bytes)** são os totais dos tamanhos das instâncias de tipo.|  
|**Dif. de Tamanho Total (Bytes)**|No caso de um tipo, a diferença no tamanho total de instâncias do tipo entre o instantâneo primário e o instantâneo anterior, menos o tamanho dos objetos nas instâncias. |  
|**Tamanho Inclusivo (Bytes)**|O tamanho dos objetos no instantâneo primário, incluindo o tamanho dos objetos nos objetos.|  
|**Diferença de Tamanho Inclusivo (Bytes)**|No caso de um tipo, a diferença no tamanho de todas as instâncias do tipo entre o instantâneo primário e o instantâneo anterior, incluindo o tamanho dos objetos nos objetos.|  
|**Módulo**|O módulo que contém o objeto.|  

## <a name="see-also"></a>Consulte também  
 [Memória JavaScript](../profiling/javascript-memory.md)  
 [Criação de perfis no Visual Studio](../profiling/index.md)  
 [Introdução às ferramentas de criação de perfil](../profiling/profiling-feature-tour.md)  
 [Práticas recomendadas de desempenho para aplicativos UWP em C++, C# e Visual Basic](/previous-versions/windows/apps/hh750313\(v\=win.10\))   
 [Diagnosing memory issues with the new Memory Usage Tool in Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=394706) (Diagnosticando problemas de memória com a nova Ferramenta de Uso de Memória no Visual Studio)