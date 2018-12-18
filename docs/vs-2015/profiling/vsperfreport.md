---
title: VSPerfReport | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- command-line tools, VSPerfReporttool
- performance tools, VSPerfReport tool
- profiling tools,VSPerfReport
- VSPerfReport tool
- command line, tools
- instrumentation, VSPerfReporttool
ms.assetid: dbfd8d91-4430-4b82-81b9-97ac61412a6c
caps.latest.revision: 37
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 12b76923a0687125643f95228397d3051cb08c5b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51806822"
---
# <a name="vsperfreport"></a>VSPerfReport
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ferramenta de linha de comando VSPerfReport é usada para criar relatórios usando [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ferramentas de criação de perfil de arquivos de dados de criação de perfil. O formato de relatório padrão é um arquivo .csv.  
  
 VSPerfReport usa a seguinte sintaxe:  
  
```  
VSPerfReport [/U] vspfilename [/options]  
```  
  
 Observe que `filename` deve ser um arquivo .vsp ou .vsps válido.  
  
 A ferramenta de linha de comando VSPerfReport também é usada para comparar arquivos .vsp ou .vsps. Para gerar um relatório de diferença ("diff"), use a seguinte sintaxe:  
  
```  
VSPerfReport [/U] /diff vspfilename1 vspfilename2 [/options]  
```  
  
 `vspfilename1 and vspfilename2` devem ser arquivos .vsp ou .vsps válidos.  
  
## <a name="symbol-files"></a>Arquivos de Símbolo  
 Para exibir informações de símbolo como nomes de função e números de linha, o VSPerfReport necessita de acesso aos arquivos de símbolo (.PDB) dos componentes analisados e aos arquivos de símbolo do Windows. Para saber mais, confira [Como especificar locais de arquivos de símbolo na linha de comando](../profiling/how-to-specify-symbol-file-locations-from-the-command-line.md).  
  
## <a name="general-report-options"></a>Opções de Relatório Geral  
 A tabela a seguir descreve o opções e as opções que selecionar os dados a serem relatados de formatação do relatório geral.  
  
|Opções|Descrição|  
|-------------|-----------------|  
|**U**|A saída de relatório e a saída redirecionada do console são gravadas como Unicode. Deve ser a primeira opção especificada.|  
|**Resumo:**[*types*]|Cria um ou mais tipos de relatórios.<br /><br /> -   `All` - todos os tipos de relatório gerados.<br />-   `CallerCallee` - relações pai/filho entre funções.<br />-   `Function` - funções chamadas.<br />-   `CallTree` - hierarquia de funções chamadas.<br />-   `Counter` - todas as marcações juntas com os valores de contador de desempenho do Windows.<br />-   `Ip` - instruções perfiladas.<br />-   `Life` - tempo de vida dos objetos alocados (disponíveis quando os dados de alocação foram coletados).<br />-   `Line` dados de perfil de linha de código-fonte.<br />-   `Header` - o relatório contém informações de cabeçalho do arquivo.<br />-   `Mark` todas as marcas.<br />-   `Module` - módulos perfilados.<br />-   `Process` - processos perfilados.<br />-   `Thread` - segmentos perfilados.<br />-   `Type` - tipos alocados.<br />-   `Contention` - contenções de recurso.<br />-   `RuleWarnings` - problemas de regra de desempenho<br />-   `ETW` - todos os eventos de Rastreamento de Eventos para Windows (ETW) coletados na execução da criação de perfil. O arquivo de dados .etl deve estar em seu local original ou no diretório que contém o arquivo .vsp ou .vsps.|  
|**Xml**|Relatório de saída no formato XML.|  
|**CallTrace**|Cria uma lista de entradas e saídas da função, eventos ETW e marcas.|  
|**ClearPackedSymbols**|Remove símbolos inseridos anteriormente de um arquivo de dados do criador de perfil. Execute esse comando antes de executar PackSymbols uma segunda vez.|  
|**SymbolPath:** `path`|Especifica um ou mais caminhos de pesquisa ou servidores de símbolo que contêm símbolos para o arquivo de dados do criador de perfil.|  
|**DebugSymPath**|Lista os locais pesquisados para símbolos e se eles são encontrados. Essa opção é útil para resolver problemas de resolução de símbolo.|  
|**PackSymbols**|Salva os símbolos no arquivo de criação de perfil de dados (.vsp) para que não seja necessário analisar os arquivos de símbolo (.pdb).|  
|**Saída:** *caminho*&#124;*nomedoarquivo*|Especifica um local alternativo para os arquivos de relatório gerados. Por padrão, os relatórios são criados no diretório atual.|  
|**SummaryFile**|Analise e salve as informações analisadas em um arquivo de resumo .vsps.|  
|**PrintMarks**|Mostre os nomes e os carimbos de data e hora para todas as marcas no arquivo de relatório especificado.|  
|**?**|Exibe informações de uso.|  
|**NoLogo**|Oculta as informações de versão quando o relatório está em execução.|  
|**UserRulesDirectory**|Especifica o diretório que contém regras de desempenho definidas pelo usuário [ainda não implementado].|  
  
## <a name="filter-options"></a>Opções de filtro  
 A tabela a seguir descreve as opções para filtrar os dados disponíveis.  
  
|Opções|Descrição|  
|-------------|-----------------|  
|**JustMyCode**[**:**[`caller`][,`callee`]]|Mostrar somente chamadas de função de aplicativo do usuário; ocultar chamadas do sistema.<br /><br /> - Sem parâmetros - ocultar todas as funções do sistema.<br />-   `caller` - mostrar um nível de funções do sistema que chamam funções de aplicativo.<br />-   `callee` - mostrar um nível de funções do sistema que são chamadas por funções de aplicativo do usuário.|  
|**StartTime:**[*value*]|Mostrar apenas os dados coletados depois do valor (em milissegundos).|  
|**EndTime:**[*value*]|Mostrar apenas os dados coletados antes do valor (em milissegundos).|  
|**FilterFile:** `VSPFFile`|Especifica o local de um arquivo de filtro que foi gerado a partir da janela do relatório de desempenho do Visual Studio.|  
|**MsFilter:**[*starttime,duration*]|Mostrar apenas os dados de `starttime` até a duração de `duration` (em milissegundos).|  
|**Process:**[*pid*]|Mostrar somente os dados do processo especificado.|  
|**Thread:**[*threadid*]|Mostra apenas os dados do thread especificado.|  
|**Thread:**[*threadid,processid*]|Mostra apenas os dados do thread especificado associado ao processo especificado.|  
  
## <a name="difference-report-options"></a>Opções de Relatório de Diferença  
 A tabela a seguir descreve as opções para comparar arquivos de relatório.  
  
|Opções|Descrição|  
|-------------|-----------------|  
|**Diff**  `vspfile1 vspfile2`|Compare dois arquivos de relatório ( .vsp ou .vsps). As opções de resumo serão ignoradas usando a opção diff.|  
|**Diff:**[*value*]|A diferença entre dois valores será desconsiderada abaixo desse valor de limite. Além disso, os novos dados com valores sob esse limite não serão exibidos.|  
|**DiffTable:**[*tablename*]|Use essa tabela específica para comparar arquivos. O padrão é a tabela de funções.|  
|**DiffColumn:**[*columnname*]|Use estes valores de comparação de colunas específicos. O padrão é a coluna de porcentagem de amostras exclusivas.|  
|**QueryDiffTables**|Liste as tabelas e as colunas válidas para os dois arquivos de relatório fornecidos.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de relatório de desempenho](../profiling/performance-report-views.md)



