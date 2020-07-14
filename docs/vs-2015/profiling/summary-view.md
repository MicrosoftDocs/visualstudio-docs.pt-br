---
title: Exibição de resumo | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
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
caps.latest.revision: 42
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f4346b0e7459ee3c78669ab9178555370ffac16d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545503"
---
# <a name="summary-view"></a>Exibição do Resumo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A exibição de resumo exibe informações sobre as funções ou os objetos de desempenho mais caro em uma execução de criação de perfil. Essa exibição fornece um gráfico de linha do tempo e listas de duas ou mais das funções mais caras ou objetos com base nas métricas de desempenho do método de criação de perfil. Os dados nessa exibição dependem do método de criação de perfil que foi usado (amostragem, instrumentação ou simultaneidade) e se a alocação de memória .NET foi coletada.  
  
 Para todas as exibições de resumo exceto a exibição de Resumo dos dados de simultaneidade, o gráfico de linha do tempo na exibição de resumo mostra a utilização do processador (CPU) do aplicativo com perfil ao longo do tempo em que ocorreu a criação de perfil.  
  
- Se você especificar um segmento de tempo no gráfico, você poderá analisar os dados para esse segmento ou ampliar a exibição da linha do tempo para o segmento especificado. Para obter mais informações, consulte [como filtrar modos de exibição de relatório na linha do tempo de resumo](../profiling/how-to-filter-report-views-from-the-summary-timeline.md)  
  
- Você pode clicar em uma função em uma lista de exibição de resumo para abrir a exibição de detalhes da função para a função. Também pode clicar com o botão direito do mouse na função para obter outras opções de exibição.  
  
- Para modificar o número de itens que aparecem na lista de exibição de resumo, abra o menu **Ferramentas**, aponte para **Opções**e, em seguida, clique em **Ferramentas de Desempenho**. Em **Configurações Gerais**, modifique a configuração **Número de Funções na exibição de resumo**.  
  
## <a name="notifications-links"></a>Links de Notificações  
 Você pode clicar em links da lista de notificação para definir opções de exibição para o relatório. A lista está à direita do gráfico de linha do tempo.  
  
|Opção|Descrição|  
|-|-|  
|**Exibir código de não usuário**<br /><br /> **Exibir Apenas Meu Código**|Não disponível para código nativo ou dados que foram coletados usando o método de instrumentação de criação de perfil. Alterna entre exibir somente os dados do código do usuário (**Exibir Apenas Meu Código**) e exibir dados de todo o código, incluindo o código de sistema (**Exibir código de não usuário**). Por padrão, os dados são limitados ao código do usuário. Para alterar a configuração, consulte [Como filtrar exibições de relatório das ferramentas de criação de perfil para Exibir Apenas Meu Código](../profiling/how-to-filter-profiling-tools-report-views-to-display-just-my-code.md).|  
|**Exibir Diretrizes**|Exibe avisos de regra de desempenho na janela **Lista de Erros**. Para mais informações, consulte [Usando regras de desempenho para analisar dados](../profiling/using-performance-rules-to-analyze-data.md)|  
  
## <a name="report"></a>Relatório  
 Você pode clicar em links na lista de relatórios para abrir os diferentes modos de exibição e para comparar, salvar ou filtrar o relatório. A lista está à direita do gráfico de linha do tempo.  
  
|Name|Descrição|  
|-|-|  
|**Exibir Árvore de Chamadas Cortada**|Exibe os caminhos de execução mais caros no modo de exibição de árvore de chamada. Para obter mais informações, consulte o [Modo de exibição de árvore de Chamadas](../profiling/call-tree-view.md).|  
|**Mostrar linhas de acesso**|Não disponível para criação de perfil de dados que foram coletados usando o método de instrumentação. Exibe as linhas de código-fonte mais caras na exibição de linhas. Para obter mais informações, consulte [Exibição de linhas](../profiling/lines-view.md).|  
|**Comparar Relatórios**|Exibe o **selecionar arquivos de análise para comparação** caixa de diálogo na qual você pode especificar outro arquivo de dados de criação de perfil a ser comparado com o arquivo atual. Para mais informações, consulte [Comparando os Arquivos de Dados de desempenho](../profiling/comparing-performance-data-files.md).|  
|**Exportar Dados de Relatório**|Exibe a caixa de diálogo **Exportar relatório**, na qual você pode especificar um ou mais modos de exibição de relatório para salvar como valores separados por vírgulas (. csv) ou arquivos .xml. Para mais informações, consulte [Como exportar relatórios de ferramentas de criação de perfil](https://msdn.microsoft.com/174b5bd3-df9b-4fd4-88d4-76032ab90451).|  
|**Salvar relatório analisado**|Salva o arquivo de dados de criação de perfil atual como um arquivo .vsps, que abre mais rapidamente na interface para [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Para obter mais informações, consulte [Como salvar perfis analisados de arquivos de dados](https://msdn.microsoft.com/0340ddde-caf4-48ac-8af3-d15dcdade556).|  
|**Filtrar Dados de Relatório**|Exibe o painel de filtro de relatório perfil no qual você pode especificar critérios para restringir os dados na exibição do relatório. Para obter mais informações, consulte [Filtro de Exibição do Relatório de Desempenho](../profiling/performance-report-view-filter.md)|  
|**Alternar tela inteira**|Alterna o modo de tela inteira para o modo de exibição de relatório.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibição de resumo](../profiling/summary-view-sampling-data.md)   
 [Exibição de resumo](../profiling/summary-view-instrumentation-data.md)   
 [Exibição do Resumo](../profiling/summary-view-dotnet-memory-data.md)
