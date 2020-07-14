---
title: Criação de relatórios do criador de perfil com a linha de comando | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: c886f8af-2014-4fec-9b24-d98b68ecafb7
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 475c8da2d10dea4953486fc9c564c5bde7fb0887
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329071"
---
# <a name="create-profiler-reports-from-the-command-line"></a>Criar relatórios do criador de perfil por meio da linha de comando
A ferramenta de linha de comando **VSPerfReport** permite que você crie relatórios .*xml* ou de valores separados por vírgulas (.*csv*) de arquivos de dados de criação de perfil (.*vsp*). Tipos de relatório VSPerfReport correspondem aproximadamente às exibições baseadas em tabela da interface para [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Você pode filtrar o relatório para mostrar somente o seu código e mostrar apenas um segmento do arquivo de dados de criação de perfil. Para obter mais informações, confira [VSPerfReport](../profiling/vsperfreport.md).

 Também é possível facilitar o compartilhamento dos arquivos de dados de criação de perfil inserindo símbolos nos arquivos .*vsp* e criando arquivos de relatórios previamente analisados (.*vsps*) que são menores e mais rápidos para abrir.

## <a name="common-tasks"></a>Tarefas comuns

|Tarefa|Conteúdo relacionado|
|----------|---------------------|
|**Crie um relatório básico.** Crie todos ou um subconjunto dos tipos de relatório VSPerfReport.|-   [Criar relatórios básicos](../profiling/creating-basic-profiling-reports-from-the-command-line.md)|
|**Comparar dois arquivos de dados de criação de perfil.** Crie um relatório "diff" que compara os dados de desempenho em dois arquivos de dados de criação de perfil.|-   [Como: criar um relatório de comparação do criador de perfil de um prompt de comando](../profiling/how-to-create-a-profiler-comparison-report-from-a-command-prompt.md)|
|**Visualizar o rastreamento de chamada de exibição e rastreamento de eventos para dados do Windows (ETW).** Crie um relatório de rastreamento de chamada que lista informações de tempo para cada ponto de entrada e saída das funções do aplicativo e cada chamada para outras funções por sua função. Ou crie uma lista detalhada de todos os eventos ETW que foram coletados em uma execução de criação de perfil.|-   [Como: criar um relatório de rastreamento de chamada](../profiling/how-to-create-a-profiling-tools-call-trace-report.md)|
|**Filtrar um relatório.** Limite um relatório apenas às funções em seu código ou em um momento específico no arquivo de dados de criação de perfil.|-   [Como filtrar relatórios da linha de comando](../profiling/how-to-filter-reports-from-the-command-line.md)|
|**Criar arquivos de dados de criação de perfil portáteis.** Para facilitar o compartilhamento de dados de criação de perfil, você pode inserir os símbolos para uma criação de perfil no. arquivo *VSP* . Você também pode criar um dado de criação de perfil previamente analisado (.* vsps*) arquivo que é menor e mais rápido de abrir.|-   [Criar arquivos de dados de criação de perfil portáteis](../profiling/creating-portable-profiling-data-files-from-the-command-line.md)|
