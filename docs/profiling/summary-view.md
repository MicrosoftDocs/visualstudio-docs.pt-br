---
title: Exibição de resumo | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.view.summary
helpviewer_keywords:
- performance reports, summary view
- profiling tools reports, Summary view
- profiling tools, Summary view
- Summary view
ms.assetid: 98a1eb71-bbf5-4ce7-8559-cdc29f082c4b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 65da91ea1182a5c14d6c4b27057b6561221077e8
ms.sourcegitcommit: bccb05b5b4e435f3c1f7c36ba342e7d4031eb398
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51220822"
---
# <a name="summary-view"></a>Exibição resumida
A exibição de resumo exibe informações sobre as funções ou os objetos de desempenho mais caro em uma execução de criação de perfil. Essa exibição fornece um gráfico de linha do tempo e listas de duas ou mais das funções mais caras ou objetos com base nas métricas de desempenho do método de criação de perfil. Os dados nessa exibição dependem do método de criação de perfil que foi usado (amostragem, instrumentação ou simultaneidade) e se a alocação de memória .NET foi coletada.  

 Para todas as exibições de resumo exceto a exibição de Resumo dos dados de simultaneidade, o gráfico de linha do tempo na exibição de resumo mostra a utilização do processador (CPU) do aplicativo com perfil ao longo do tempo em que ocorreu a criação de perfil.  

-   Se você especificar um segmento de tempo no gráfico, você poderá analisar os dados para esse segmento ou ampliar a exibição da linha do tempo para o segmento especificado. Para obter mais informações, confira [Como filtrar exibições de relatório por meio da Linha do Tempo de Resumo](../profiling/how-to-filter-report-views-from-the-summary-timeline.md)  

-   Você pode clicar em uma função em uma lista de exibição de resumo para abrir a exibição de detalhes da função para a função. Também pode clicar com o botão direito do mouse na função para obter outras opções de exibição.  

-   Para modificar o número de itens que aparecem na lista de exibição de resumo, abra o menu **Ferramentas**, aponte para **Opções**e, em seguida, clique em **Ferramentas de Desempenho**. Em **Configurações Gerais**, modifique a configuração **Número de Funções na exibição de resumo**.  

## <a name="notifications-links"></a>Links de notificações  
 Você pode clicar em links da lista de notificação para definir opções de exibição para o relatório. A lista está à direita do gráfico de linha do tempo.  

|||  
|-|-|  
|**Exibir código de não usuário**<br /><br /> **Exibir Apenas Meu Código**|Não disponível para código nativo ou dados que foram coletados usando o método de instrumentação de criação de perfil. Alterna entre exibir somente os dados do código do usuário (**Exibir Apenas Meu Código**) e exibir dados de todo o código, incluindo o código de sistema (**Exibir código de não usuário**). Por padrão, os dados são limitados ao código do usuário. Para alterar a configuração, confira [Como filtrar exibições de relatório das ferramentas de criação de perfil para exibir Apenas Meu Código](../profiling/how-to-filter-profiling-tools-report-views-to-display-just-my-code.md).|  
|**Exibir Diretrizes**|Exibe avisos de regra de desempenho na janela **Lista de Erros**. Para obter mais informações, confira [Usar regras de desempenho para analisar dados](../profiling/using-performance-rules-to-analyze-data.md)|  

## <a name="report"></a>Relatório  
 Você pode clicar em links na lista de relatórios para abrir os diferentes modos de exibição e para comparar, salvar ou filtrar o relatório. A lista está à direita do gráfico de linha do tempo.  


| | |
|----------------------------| - |
| **Exibir Árvore de Chamadas Cortada** | Exibe os caminhos de execução mais caros no modo de exibição de árvore de chamada. Para obter mais informações, confira [Exibição Árvore de Chamadas](../profiling/call-tree-view.md). |
| **Mostrar linhas de acesso** | Não disponível para criação de perfil de dados que foram coletados usando o método de instrumentação. Exibe as linhas de código-fonte mais caras na exibição de linhas. Para obter mais informações, confira [Exibição Linhas](../profiling/lines-view.md). |
| **Comparar Relatórios** | Exibe o **selecionar arquivos de análise para comparação** caixa de diálogo na qual você pode especificar outro arquivo de dados de criação de perfil a ser comparado com o arquivo atual. Para obter mais informações, confira [Comparar arquivos de dados de desempenho](../profiling/comparing-performance-data-files.md). |
| **Exportar Dados de Relatório** | Exibe a caixa de diálogo **Exportar relatório**, na qual você pode especificar um ou mais modos de exibição de relatório para salvar como valores separados por vírgulas (. csv) ou arquivos .xml. Para obter mais informações, confira [Como exportar relatórios de ferramentas de criação de perfil](/previous-versions/visualstudio/visual-studio-2010/ms182394\(v\=vs.100\)). |
| **Salvar relatório analisado** | Salva o arquivo de dados de criação de perfil atual como um arquivo .vsps, que abre mais rapidamente na interface para [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Para obter mais informações, confira [Como salvar arquivos de dados de perfis analisados](/previous-versions/visualstudio/visual-studio-2010/bb763106\(v\=vs.100\)). |
| **Filtrar Dados de Relatório** | Exibe o painel de filtro de relatório perfil no qual você pode especificar critérios para restringir os dados na exibição do relatório. Para obter mais informações, confira [Filtro de exibição de relatório de desempenho](../profiling/performance-report-view-filter.md) |
| **Alternar Tela Inteira** | Alterna o modo de tela inteira para o modo de exibição de relatório. |

## <a name="see-also"></a>Consulte também  
 [Exibição Resumo – dados de amostragem](../profiling/summary-view-sampling-data.md)   
 [Exibição Resumo – dados de instrumentação](../profiling/summary-view-instrumentation-data.md)   
 [Exibição Resumo – dados de memória do .NET](../profiling/summary-view-dotnet-memory-data.md)