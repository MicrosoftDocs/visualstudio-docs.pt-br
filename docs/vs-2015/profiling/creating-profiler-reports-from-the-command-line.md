---
title: Criação de relatórios do criador de perfil com a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c886f8af-2014-4fec-9b24-d98b68ecafb7
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c4cf566affff500d372a980a6f07122c2df33a23
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51788583"
---
# <a name="creating-profiler-reports-from-the-command-line"></a>Criando relatórios do criador de perfil a partir da linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A ferramenta da linha de comando **VSPerfReport** permite que você crie relatórios .xml ou valores separados por vírgulas (.csv) de arquivos de dados de criação de perfil (.vsp). Tipos de relatório VSPerfReport correspondem aproximadamente às exibições baseadas em tabela da interface para [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Você pode filtrar o relatório para mostrar somente o seu código e mostrar apenas um segmento do arquivo de dados de criação de perfil. Para obter mais informações, confira [VSPerfReport](../profiling/vsperfreport.md).  
  
 Você também pode facilitar o compartilhamento dos arquivos de dados de criação de perfil vinculando símbolos nos arquivos .vsp e criando arquivos de relatórios previamente analisados (.vsps) que são menores e mais rápidos para abrir.  
  
## <a name="common-tasks"></a>Tarefas comuns  
  
|Tarefa|Conteúdo relacionado|  
|----------|---------------------|  
|**Criar um relatório básico.** Crie todos ou um subconjunto dos tipos de relatório VSPerfReport.|-   [Criação de relatórios básicos](../profiling/creating-basic-profiling-reports-from-the-command-line.md)|  
|**Comparar dois arquivos de dados de criação de perfil.** Crie um relatório "diff" que compara os dados de desempenho em dois arquivos de dados de criação de perfil.|-   [Como: criar um relatório de comparação de criador de perfil por meio de um prompt de comando](../profiling/how-to-create-a-profiler-comparison-report-from-a-command-prompt.md)|  
|**Visualizar o rastreamento de chamada de exibição e rastreamento de eventos para dados do Windows (ETW).** Crie um relatório de rastreamento de chamada que lista informações de tempo para cada ponto de entrada e saída das funções do aplicativo e cada chamada para outras funções por sua função. Ou crie uma lista detalhada de todos os eventos ETW que foram coletados em uma execução de criação de perfil.|-   [Como: criar um relatório de rastreamento de chamada](../profiling/how-to-create-a-profiling-tools-call-trace-report.md)|  
|**Filtrar um relatório.** Limite um relatório apenas às funções em seu código ou em um momento específico no arquivo de dados de criação de perfil.|-   [Como: filtrar relatórios por meio da linha de comando](../profiling/how-to-filter-reports-from-the-command-line.md)|  
|**Criar arquivos de dados de criação de perfil portáteis.** Para tornar mais fácil o compartilhamento de dados de criação de perfil, você pode inserir os símbolos para uma geração de perfil no arquivo .vsp. Você também pode criar um arquivo de dados de criação de perfil previamente analisados (.vsps) que é menor e mais rápido para abrir.|-   [Criação de arquivos de dados de criação de perfil portáteis](../profiling/creating-portable-profiling-data-files-from-the-command-line.md)|



