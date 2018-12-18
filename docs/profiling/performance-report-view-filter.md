---
title: Filtro de Exibições do Relatório de Desempenho | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, Profiler Report view filter
- Profiler Report View filter, profiling tools
ms.assetid: 35f89d86-4683-4db1-aa0c-ae0ce65fa524
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 17fc42eab94d98ceb636e53e3ed6efd39a08f920
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35254264"
---
# <a name="performance-report-view-filter"></a>Filtro de exibição de relatório de desempenho
A janela **Filtro de Exibição de Relatório do Criador de Perfil** está localizada na parte superior da janela **Relatório de Desempenho**. Se não estiver visível, clique no botão **Mostrar Filtro**.  
  
 Você pode modificar cada cláusula de filtro para refinar os resultados. As seguintes colunas estão disponíveis no construtor de filtro.  
  
|Filtrar item|Descrição|  
|-----------------|-----------------|  
|And/Or|Escolha **And** se essa cláusula e a próxima devem ambas ser verdadeiras para corresponder a um resultado. Escolha **Or** se essa cláusula ou a próxima podem ser verdadeiras para corresponder a um resultado.|  
|Campo|Selecione o campo a ser usado na cláusula de filtro da lista de campos de dados que estão disponíveis no arquivo de relatório atual.|  
|Operador|Escolha o operador que especifica a relação entre o campo e o valor desejado.<br /><br /> =    É igual a<br /><br /> <>  Não é igual a<br /><br /> <    Menor que<br /><br /> >    Maior que<br /><br /> <=  Menor ou igual a<br /><br /> >= Maior ou igual a|  
|Valor|Selecione ou insira o valor a ser procurado. Alguns campos listam os valores disponíveis para o campo.|  
  
 Você pode adicionar cláusulas ao filtro até achar que ele fornecem os melhores resultados. Clique em **Executar Filtro** para aplicar o filtro ao arquivo de dados.  
  
 Na exibição de relatório **Marcas**, você pode gerar cláusulas de filtro para limitar os dados nas exibições de relatório para os dados coletados entre duas marcas. Selecione as marcas nas quais você deseja começar e terminar o relatório de dados e clique com botão direito e selecione **Adicionar Filtro nas Marcas** ou **Adicionar Filtro em Carimbos de Data/Hora**. Ambos os filtros limitam os dados no arquivo de dados para o mesmo período; **Adicionar Filtro nas Marcas** pode ser aplicado a outros arquivos .vsp.  
  
 Para salvar o filtro, clique em **Exportar filtro** na barra de ferramentas **Relatório de Desempenho** e, em seguida, especifique um local e um nome para o arquivo .*vspf*. Para carregar um filtro salvo anteriormente, clique em **Importar Filtro** e localize o arquivo de filtro salvo. Arquivos de filtro também podem ser usados para filtrar arquivos de dados em computadores que têm as ferramentas de criação de perfil autônomas instaladas. Para obter mais informações, confira [VSPerfReport](../profiling/vsperfreport.md).  
  
## <a name="see-also"></a>Consulte também  
 [Analisar dados de ferramentas de desempenho](../profiling/analyzing-performance-tools-data.md)   
 [VSPerfReport](../profiling/vsperfreport.md)