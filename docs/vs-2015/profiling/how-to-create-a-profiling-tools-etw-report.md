---
title: Como criar um relatório ETW das ferramentas de criação de perfil | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bf5547b3-f6c7-4989-9d47-2fe4f1261444
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1901cf0800483ee4ce8ba0bce26fe3cf7ac073e6
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51761598"
---
# <a name="how-to-create-a-profiling-tools-etw-report"></a>Como criar um relatório ETW das ferramentas de criação de perfil
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Relatório de Rastreamento de Eventos para Windows (ETW) lista os eventos ETW que são registrados em uma sessão de desempenho de Ferramentas de Criação de Perfil [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Dados de ETW são coletados em um arquivo binário (.etl). Para obter mais informações sobre este relatório, consulte [Relatório de Rastreamento de Eventos para Windows (ETW)](../profiling/event-tracing-for-windows-etw-report.md).  
  
> [!NOTE]
>  Não é possível exibir relatórios ETW na interface para [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
- Para obter informações sobre como coletar dados ETW por meio da interface de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], consulte [Como coletar dados de Rastreamento de Eventos para Windows (ETW)](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md).  
  
- Para obter informações sobre como coletar dados de ETW de um prompt de comando, consulte [VSPerfCmd](../profiling/vsperfcmd.md) e [Eventos](../profiling/events-vsperfcmd.md).  
  
  O relatório de ETW é gerado usando o comando **VSReport/summary:etw**. O .etl que contém os dados de ETW deve estar no mesmo diretório que o arquivo com os dados de criação de perfil (.vsp ou .vsps). Por padrão, o relatório é gerado como um arquivo de valores separados por vírgula (.csv). Para obter mais informações, confira [VSPerfReport](../profiling/vsperfreport.md).  
  
### <a name="to-generate-an-etw-report"></a>Para criar um relatório ETW  
  
-   Em uma janela de **Prompt de Comando**, digite a seguinte linha de comando:  
  
     *ToolsPath* **VSPerfReport** *VSPFile*  **/Summary:ETW [/Xml]**  
  
    |||  
    |-|-|  
    |*ToolsPath*|O caminho do utilitário de Ferramentas de Criação de Perfil. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).|  
    |*VSPFile*|Os dados de criação de perfil (arquivo .vsp ou .vsps). Caminhos completos e parciais são aceitos.|  
    |Xml|Gera um relatório que é formatado em XML.|



