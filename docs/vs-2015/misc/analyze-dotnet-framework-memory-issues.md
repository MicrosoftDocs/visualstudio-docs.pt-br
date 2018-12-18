---
title: Analisar problemas de memória do .NET Framework | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.diagnostics.managedmemoryanalysis
ms.assetid: 43341928-9930-48cf-a57f-ddcc3984b787
caps.latest.revision: 9
ms.author: mikejo
manager: douge
ms.openlocfilehash: 5b5b79e351f828f443e133f40c322ffba3f1a8b6
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51810475"
---
# <a name="analyze-net-framework-memory-issues"></a>Analisar problemas de memória .NET Framework
Encontre perdas de memória e uso ineficiente da memória no código do .NET Framework com o analisador de memória gerenciada do Visual Studio. A versão mínima do .NET Framework do código de destino é o .NET Framework 4.5.  
  
 A ferramenta de análise de memória analisa informações em *arquivos de despejo com dados de heap* que uma cópia dos objetos na memória de um aplicativo. Você pode coletar arquivos de despejo (.dmp) do IDE do Visual Studio ou usar outras ferramentas de sistema.  
  
- É possível analisar um único instantâneo para compreender o impacto relativo dos tipos de objeto sobre o uso da memória e encontrar o código no aplicativo que usa a memória de maneira ineficiente.  
  
- Você também pode comparar (*diff*) dois instantâneos que fazem com que a memória de um aplicativo para encontrar áreas no seu código usam aumentará ao longo do tempo.  
  
  Para obter uma explicação do analisador de memória gerenciada, consulte [usando o Visual Studio 2013 para diagnosticar problemas de memória do .NET na produção](http://blogs.msdn.com/b/visualstudioalm/archive/2013/06/20/using-visual-studio-2013-to-diagnose-net-memory-issues-in-production.aspx) no Visual Studio ALM + blog Team Foundation Server.  
  
##  <a name="BKMK_Contents"></a> Conteúdo  
 [Uso de memória em aplicativos do .NET Framework](#BKMK_Memory_use_in__NET_Framework_apps)  
  
 [Identificar um problema de memória em um aplicativo](#BKMK_Identify_a_memory_issue_in_an_app)  
  
 [Coletar instantâneos de memória](#BKMK_Collect_memory_snapshots)  
  
 [Analisar o uso de memória](#BKMK_Analyze_memory_use)  
  
##  <a name="BKMK_Memory_use_in__NET_Framework_apps"></a> Uso de memória em aplicativos do .NET Framework  
 Como o .NET Framework é um tempo de execução com coleta de lixo, na maioria dos aplicativos, o uso da memória não é um problema. Mas em aplicativos de longa execução, como serviços e aplicativos Web, e em dispositivos que tenham uma quantidade de memória limitada, o acúmulo de objetos na memória pode afetar o desempenho do aplicativo e o dispositivo no qual é executado. O uso excessivo da memória poderá desabastecer o aplicativo e o computador de recursos se o coletor de lixo estiver sempre em execução ou se o sistema operacional for forçado a transferir memória entre RAM e disco. No pior dos casos, um aplicativo pode falhar com uma exceção "Falta de memória".  
  
 O .NET *heap gerenciado* é uma região de memória virtual em que os objetos de referência criados por um aplicativo são armazenados. O tempo de vida dos objetos é gerenciada pelo GC (coletor de lixo). O coletor de lixo usa referências para acompanhar objetos que ocupam blocos de memória. Uma referência é criada quando um objeto é criado e atribuído a uma variável. Um único objeto pode ter várias referências. Por exemplo, as referências adicionais a um objeto podem ser criadas adicionando-se o objeto a uma classe, coleção ou outra estrutura de dados, ou atribuindo o objeto a uma segunda variável. Uma maneira menos óbvia de criar uma referência é com um objeto adicionando um manipulador ao evento de outro objeto. Nesse caso, o segundo objeto mantém a referência ao primeiro objeto até o manipulador ser removido explicitamente ou o segundo objeto ser destruído.  
  
 Para cada aplicativo, o GC mantém uma árvore de referências que acompanha os objetos mencionados pelo aplicativo. O *árvore de referências* tem um conjunto de raízes, que inclui objetos globais e estáticos, bem como pilhas de threads e dinamicamente objetos instanciados. Um objeto será raiz se tiver pelo menos um objeto pai mantendo uma referência a ele. O GC só poderá recuperar a memória de um objeto quando nenhum outro objeto ou variável no aplicativo tiver uma referência a ele.  
  
 ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
##  <a name="BKMK_Identify_a_memory_issue_in_an_app"></a> Identificar um problema de memória em um aplicativo  
 O sintoma mais visível de problemas de memória é o desempenho do aplicativo, especialmente se o desempenho cair com o passar do tempo. A queda no desempenho de outros aplicativos enquanto o aplicativo está em execução também pode indicar uma perda de memória. Se você suspeitar de um problema de memória, use uma ferramenta como o Gerenciador de tarefas ou [Monitor de desempenho do Windows](http://technet.microsoft.com/library/cc749249.aspx) para investigar mais. Por obter exemplo, procure um aumento no tamanho total da memória que não seja possível explicar como uma origem possível de perdas de memória:  
  
 ![Aumento da memória consistente em Monitor de recursos](../misc/media/mngdmem-resourcemanagerconsistentgrowth.png "MNGDMEM_ResourceManagerConsistentGrowth")  
  
 Você também pode notar picos de memória maiores que o seu conhecimento do código sugeriria, o que pode indicar uso ineficiente da memória em um procedimento:  
  
 ![No Gerenciador de recursos de picos de memória](../misc/media/mngdmem-resourcemanagerspikes.png "MNGDMEM_ResourceManagerSpikes")  
  
##  <a name="BKMK_Collect_memory_snapshots"></a> Coletar instantâneos de memória  
 A ferramenta de análise de memória analisa informações em *arquivos de despejo* que contêm informações de heap. Você pode criar arquivos de despejo no Visual Studio, ou você pode usar uma ferramenta como o [ProcDump](http://technet.microsoft.com/sysinternals/dd996900.aspx) partir [Windows Sysinternals](http://technet.microsoft.com/sysinternals). Ver [o que é um despejo e como criar um?](http://blogs.msdn.com/b/debugger/archive/2009/12/30/what-is-a-dump-and-how-do-i-create-one.aspx) no blog da equipe do depurador do Visual Studio.  
  
> [!NOTE]
>  A maioria das ferramentas pode coletar informações de despejo com ou sem dados completos de memória do heap. O analisador de memória do Visual Studio requer informações completas do heap.  
  
 **Para coletar um despejo do Visual Studio**  
  
1. É possível criar um arquivo de despejo para um processo iniciado em um projeto do Visual Studio ou anexar o depurador a um processo em execução. Ver [anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).  
  
2. Pare a execução. O depurador é interrompido quando você escolhe **interromper tudo** sobre o **depurar** menu, ou uma exceção ou um ponto de interrupção  
  
3. Sobre o **Debug** menu, escolha **Salvar despejo como**. No **Salvar despejo como** diálogo caixa, especifique um local e verifique se **minidespejo com Heap** (o padrão) está selecionado na **Salvar como tipo** lista.  
  
   **Para comparar dois instantâneos de memória**  
  
   Para analisar o aumento do uso da memória de um aplicativo, colete dois arquivos de despejo de uma única instância do aplicativo.  
  
   ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
##  <a name="BKMK_Analyze_memory_use"></a> Analisar o uso de memória  
 [Filtrar a lista de objetos](#BKMK_Filter_the_list_of_objects) **&#124;** [analisar os dados da memória de um único instantâneo](#BKMK_Analyze_memory_data_in_from_a_single_snapshot) **&#124;** [comparar dois de memória instantâneos](#BKMK_Compare_two_memory_snapshots)  
  
 Para analisar um arquivo de despejo em busca de problemas de uso da memória:  
  
1. No Visual Studio, escolha **arquivo**, **abrir** e especifique o arquivo de despejo.  
  
2. Sobre o **resumo do arquivo de minidespejo** , escolha **depurar memória gerenciada**.  
  
    ![Página de resumo do arquivo de despejo](../misc/media/mngdmem-dumpfilesummary.png "MNGDMEM_DumpFileSummary")  
  
   O analisador de memória começa uma sessão de depuração para analisar o arquivo e exibe os resultados na página Exibição do Heap:  
  
   ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
###  <a name="BKMK_Filter_the_list_of_objects"></a> Filtrar a lista de objetos  
 Por padrão, o analisador de memória filtra a lista de objetos em um instantâneo de memória para mostrar apenas os tipos e as instâncias codificados pelo usuário e somente aqueles tipos cujo tamanho total inclusivo excede uma porcentagem limite do tamanho total do heap. Você pode alterar essas opções na **as configurações de exibição** lista:  
  
|||  
|-|-|  
|**Habilitar Apenas Meu Código**|Habilitar Apenas Meu Código oculta os objetos de sistema mais comuns, para que apenas os tipos criados por você sejam exibidos na lista.<br /><br /> Você também pode definir a opção Just My Code no Visual Studio **opções** caixa de diálogo. Sobre o **Debug** menu, escolha **opções e configurações**. No **Debugging**/**geral** guia, marque ou desmarque **Just My Code**.|  
|**Recolher pequenos objetos**|**Recolher pequenos objetos** oculta todos os tipos cujo tamanho inclusivo total é menor que 0,5% do tamanho total do heap.|  
  
 Você também pode filtrar a lista de tipo, inserindo uma cadeia de caracteres a **pesquisa** caixa. A lista exibe apenas os tipos cujos nomes contenham a cadeia de caracteres.  
  
 ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
###  <a name="BKMK_Analyze_memory_data_in_from_a_single_snapshot"></a> Analisar dados da memória de um único instantâneo  
 O Visual Studio inicia uma nova sessão de depuração para analisar o arquivo e exibe os dados da memória na janela Exibição do Heap.  
  
 ![Lista o tipo de objeto](../misc/media/dbg-mma-objecttypelist.png "DBG_MMA_ObjectTypeList")  
  
 ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
#### <a name="object-type-table"></a>Tabela Tipo de Objeto  
 A tabela superior lista os tipos de objetos mantidos na memória.  
  
- **Contagem de** mostra o número de instâncias do tipo no instantâneo.  
  
- **Tamanho (Bytes)** é o tamanho de todas as instâncias do tipo, excluindo o tamanho dos objetos cujas referências ele mantém. O  
  
- **Tamanho inclusivo (Bytes)** inclui os tamanhos de objetos referenciados.  
  
  Você pode escolher o ícone de instâncias (![o ícone de instância na coluna de tipo de objeto](../misc/media/dbg-mma-instancesicon.png "DBG_MMA_InstancesIcon")) na **tipo de objeto** coluna para exibir uma lista das instâncias das tipo.  
  
#### <a name="instance-table"></a>Tabela Instância  
 ![Tabela de instâncias](../misc/media/dbg-mma-instancestable.png "DBG_MMA_InstancesTable")  
  
- **Instância** é o local de memória do objeto que serve como o identificador de objeto do objeto  
  
- **Valor** mostra o valor real de tipos de valor. É possível focalizar o nome de um tipo de referência para exibir os valores de dados em uma dica de dados.  
  
   ![Valores em uma dica de dados da instância](../misc/media/dbg-mma-instancevaluesindatatip.png "DBG_MMA_InstanceValuesInDataTip")  
  
- **Tamanho (Bytes)** é o tamanho do objeto, excluindo o tamanho dos objetos cujas referências ele mantém. O  
  
- **Tamanho inclusivo (Bytes)** inclui os tamanhos de objetos referenciados.  
  
  Por padrão, os tipos e as instâncias são classificadas por **tamanho inclusivo (Bytes)**. Escolha um cabeçalho de coluna na lista para alterar a ordem de classificação.  
  
#### <a name="paths-to-root"></a>demarcadores para a Raiz  
  
-   Para um tipo selecionado na **tipo de objeto** tabela, o **caminhos para raiz** tabela mostra as hierarquias de tipo exclusivo que levam até objetos raiz de todos os objetos do tipo, juntamente com o número de referências para o tipo acima na hierarquia.  
  
-   Para um objeto selecionado na instância de um tipo **caminhos para raiz** mostra um gráfico dos objetos reais que mantém uma referência à instância. É possível focalizar o nome do objeto para exibir os valores de dados em uma dica de dados.  
  
#### <a name="referenced-types--referenced-objects"></a>Tipos Referenciados/Objetos Referenciados  
  
- Um tipo selecionado do **tipo de objeto** tabela, o **tipos referenciados** guia mostra o tamanho e o número de tipos referenciados mantidos por todos os objetos do tipo selecionado.  
  
- Para uma instância selecionada de um tipo **objetos referenciados** mostra os objetos que são mantidos pela instância selecionada. É possível focalizar o nome para exibir os valores de dados em uma dica de dados.  
  
  **Referências circulares**  
  
  Um objeto pode referenciar um segundo objeto que mantém direta ou indiretamente uma referência ao primeiro objeto. Quando o analisador de memória encontra essa situação, ele para de expandir o caminho de referência e adiciona uma **[ciclo detectado]** anotação para a listagem do primeiro objeto e é interrompido.  
  
  **Tipos de raiz**  
  
  O analisador de memória adiciona anotações a objetos raiz que descrevam o tipo de referência mantido:  
  
|Anotação|Descrição|  
|----------------|-----------------|  
|**Variável estática** `VariableName`|Uma variável estática. `VariableName` é o nome da variável.|  
|**Alça de finalização**|Uma referência da fila do finalizador|  
|**Variável local**|Uma variável local.|  
|**Alça forte**|Uma alça para uma referência forte da tabela de identificador de objeto.|  
|**Async. Fixa assíncrona**|Um objeto fixo assíncrono da tabela de identificador de objeto.|  
|**Identificador dependente**|Um objeto dependente da tabela de identificador de objeto.|  
|**Fixa assíncrona**|Uma referência forte fixa da tabela de identificador de objeto.|  
|**Alça RefCount**|Um objeto com contagem de referência da tabela de identificador de objeto.|  
|**Alça SizedRef**|Uma alça forte que mantém um tamanho aproximado do fechamento coletivo de todos os objetos e raízes de objeto no momento da coleta de lixo.|  
|**Variável local fixa**|Uma variável local fixa.|  
  
###  <a name="BKMK_Compare_two_memory_snapshots"></a> Comparar dois instantâneos de memória  
 É possível comparar dois arquivos de despejo de um processo para encontrar objetos que possam ser a causa de perdas de memória. O intervalo entre a coleta do primeiro arquivo (anterior) e do segundo arquivo (posterior) deve ser grande o suficiente para que o aumento no número de objetos perdidos fique claramente aparente. Para comparar os dois arquivos:  
  
1. Abra o segundo arquivo de despejo de memória e, em seguida, escolha **depurar memória gerenciada** sobre o **resumo do arquivo de minidespejo** página.  
  
2. Na página de relatório de análise de memória, abra o **Selecionar linha de base** lista e, em seguida, escolha **procurar** para especificar o primeiro arquivo de despejo.  
  
   O analisador adiciona colunas ao painel superior do relatório que exibem a diferença entre o **contagem**, **tamanho**, e **tamanho inclusivo** dos tipos para esses valores no instantâneo anterior.  
  
   ![Comparação de colunas na lista de tipo](../misc/media/mngdmem-diffcolumns.png "MNGDMEM_DiffColumns")  
  
   Um **Diff contagem de referência** coluna também é adicionada para o **caminhos para raiz** tabela.  
  
   ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
## <a name="see-also"></a>Consulte também  
 [Blog VS ALM TFS: Usando o Visual Studio 2013 para diagnosticar problemas de memória do .NET na produção](http://blogs.msdn.com/b/visualstudioalm/archive/2013/06/20/using-visual-studio-2013-to-diagnose-net-memory-issues-in-production.aspx)   
 [Channel 9 &#124; Visual Studio TV &#124; análise de memória gerenciada](http://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Managed-Memory-Analysis)   
 [Channel 9 &#124; caixa de ferramentas do Visual Studio &#124; gerenciado de análise de memória no Visual Studio 2013](http://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Managed-Memory-Analysis-in-Visual-Studio-2013)