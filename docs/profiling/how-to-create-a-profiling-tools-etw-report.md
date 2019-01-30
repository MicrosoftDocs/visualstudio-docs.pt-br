---
title: 'Como: Criar um relatório ETW das Ferramentas de Criação de Perfil | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: bf5547b3-f6c7-4989-9d47-2fe4f1261444
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 20b7c92c8cbbf500b44816fbb0f34e0df6f04720
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54940928"
---
# <a name="how-to-create-a-profiling-tools-etw-report"></a>Como: Criar um relatório de ETW das ferramentas de criação de perfil
O Relatório de Rastreamento de Eventos para Windows (ETW) lista os eventos ETW que são registrados em uma sessão de desempenho de Ferramentas de Criação de Perfil [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Os dados do ETW são coletados em um arquivo binário (.*etl*). Para obter mais informações sobre esse relatório, confira [Relatório ETW (Rastreamento de Eventos para Windows)](../profiling/event-tracing-for-windows-etw-report.md).  
  
> [!NOTE]
>  Não é possível exibir relatórios ETW na interface para [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].  
  
- Para obter informações de como coletar dados de ETW usando a interface do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], confira [Como: Coletar dados do ETW (Rastreamento de Eventos para Windows)](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md).  
  
- Para obter informações sobre como coletar dados de ETW de um prompt de comando, consulte [VSPerfCmd](../profiling/vsperfcmd.md) e [Eventos](../profiling/events-vsperfcmd.md).  
  
  O relatório de ETW é gerado usando o comando **VSReport/summary:etw**. O .*etl* que contém os dados de ETW precisam estar no mesmo diretório que o arquivo de dados de criação de perfil (.*vsp* ou .*vsps*). Por padrão, o relatório é gerado como um arquivo de valor separado por vírgula (.*csv*). Para obter mais informações, confira [VSPerfReport](../profiling/vsperfreport.md).  
  
### <a name="to-generate-an-etw-report"></a>Para criar um relatório ETW  
  
-   Em uma janela de **Prompt de Comando**, digite a seguinte linha de comando:  
  
     *ToolsPath* **VSPerfReport** *VSPFile*  **/Summary:ETW [/Xml]**  
  
    |||  
    |-|-|  
    |*ToolsPath*|O caminho do utilitário de Ferramentas de Criação de Perfil. Para saber mais, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).|  
    |*VSPFile*|O arquivo de dados de criação de perfil (.*vsp* ou .*vsps*). Caminhos completos e parciais são aceitos.|  
    |Xml|Gera um relatório que é formatado em XML.|
