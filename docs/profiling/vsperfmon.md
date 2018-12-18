---
title: VSPerfMon | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- VSPerfMon tool
- command line, tools
- command-line tools, VSPerfMon tool
- data [Visual Studio ALM], VSPerfMon tool
- performance data, VSPerfMon tool
- performance tools, VSPerfMon tool
- profilng tools,VSPerfCmd
ms.assetid: 37052afb-7a58-441f-bb17-f1587cc57068
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e9754d4f324c178c117e14ff5949bd6c8ef352e9
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35254804"
---
# <a name="vsperfmon"></a>VSPerfMon
Use a ferramenta VSPerfMon para coletar dados de desempenho de um aplicativo. Normalmente, essa ferramenta é iniciada pelo *VSPerfCmd.exe*. VSPerfMon exibe informações adicionais sobre como anexar ou desanexar processo que não está disponível usando a ferramenta VSPerfCmd. Para exibir essas informações, inicie o VSPerfMon em uma janela separada. Para invocar VSPerfMon use a seguinte sintaxe:  
  
```cmd  
VSPerfMon [/U] </TRACE [/COUNTER:cfg] | /SAMPLE | /COVERAGE> /CROSSSESSION /OUTPUT <file name> [/WINCOUNTER:cfg] [/USER [DOMAIN\]username]  
```  
  
 A tabela a seguir descreve as opções da ferramenta VSPerfMon:  
  
|Opções|Descrição|  
|-------------|-----------------|  
|**U**|Saída de console redirecionada gravada como Unicode.  Deve ser a primeira opção especificada.|  
|**OUTPUT:** `<` *nome do arquivo* `>`|Redireciona a saída para o nome de arquivo especificado.|  
|**TRACE**|Inicia o monitor de desempenho para criação de perfil instrumentada.|  
|**SAMPLE**|Inicia o monitor de desempenho para criação de perfil de amostragem.|  
|**COVERAGE**|Inicia o monitor de desempenho para coleta de dados de cobertura de código.|  
|**CONCURRENCY**|Inicia o monitor de desempenho para criação de perfil de contenção de recursos.|  
|**USER:** `[` *domínio* `\]` *nome do usuário*|Permite o acesso do cliente ao monitor de desempenho da conta especificada.|  
|**CROSSSESSION**|Habilitar criação de perfil de sessão cruzada.|  
|**COUNTER** `:cfg`|Quando o método de criação de perfil (TRACE) de instrumentação é usado, especifica um contador de CPU a ser coletado em cada ponto de instrumentação. Você pode coletar dados do contador de vários especificando diversas opções de contador.<br /><br /> Use a sintaxe a seguir para especificar os dados do contador (*cfg*):<br /><br /> **CounterName** [**,Reload**[,**FriendlyName**]]<br /><br /> -   **CounterName** é o nome de um contador retornado pelo comando VSPerfCmd /QueryCounters.<br />-   **Reload** é o intervalo de amostragem de eventos do contador. Não use *Reload* com o método de instrumentação.<br />– Quando especificado, **FriendlyName** substitui **CounterName** em nomes de coluna de relatório em ferramentas de criação de perfil.|  
|**WINCOUNTER** `:path`|Especifica um contador de desempenho do Windows para incluir com os dados de marca. `path` é uma cadeia de caracteres do contador de desempenho do Windows no formato de caminho de contador PDH. Por exemplo:<br /><br /> \Processor(0)\\% Processor Time<br /><br /> \System\Context Switches/sec|  
|**AUTOMARK** `:n`|Especifica o intervalo de tempo (em milissegundos) entre as marcas automática quando você usa /WINCOUNTER. Arredondado para cima até a 500 ms mais próximos.<br /><br /> Use 0 para desabilitar marcas automáticas. (padrão=500 ms se não especificado)|  
  
## <a name="see-also"></a>Consulte também  
 [VSInstr](../profiling/vsinstr.md)   
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [VSPerfReport](../profiling/vsperfreport.md)   
 [Exibições de relatório de desempenho](../profiling/performance-report-views.md)