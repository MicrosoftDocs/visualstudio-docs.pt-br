---
title: Filtrando Exibições de Relatório | Microsoft Docs
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
- profiling tools, configuring
ms.assetid: 820cf192-7fd6-4bee-9a51-aa69154aca85
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b5ce703fdc3b0d20feda83b59706e7c4792d2ade
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51753440"
---
# <a name="filtering-report-views"></a>Filtrando exibições de relatório
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode aplicar filtros para arquivos de dados de criação de perfil para limitar os dados de criação de perfil que são exibidos nas exibições de Relatório de Desempenho e exportados para arquivos de relatório. Você pode limitar um relatório aos dados entre os valores de carimbo de data/hora e limitar os dados a processos e threads específicos. Você pode salvar filtros em um arquivo e, em seguida, criar um filtro em um arquivo de dados de criação de perfil diferente importando o filtro salvo.  
  
 Você também pode limitar um relatório a um segmento de tempo usando a linha de tempo gráfica na Exibição de Resumo. Consulte [Como filtrar exibições de relatório por meio da linha do tempo de resumo](../profiling/how-to-filter-report-views-from-the-summary-timeline.md).  
  
 Para excluir o código do sistema e de terceiros de um relatório, consulte [Como filtrar exibições de relatório de ferramentas de criação de perfil do filtro para exibir Apenas Meu Código](../profiling/how-to-filter-profiling-tools-report-views-to-display-just-my-code.md)  
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="to-create-a-profiler-report-filter"></a>Para criar um filtro de relatório do criador de perfil  
  
1.  Se a janela de Filtro de exibição de relatório de desempenho não for exibida, clique em **Mostrar Filtro** na barra de ferramentas Exibição de Relatório de Desempenho.  
  
     O Filtro de Exibição do Relatório de Desempenho é uma tabela. Cada linha da tabela representa uma cláusula do filtro. Você pode adicionar quantas cláusulas quiser a um filtro.  
  
2.  Para cada cláusula que desejar adicionar a um filtro, selecione ou insira valores nos seguintes campos de uma linha.  
  
    |Campo|Descrição|  
    |-----------|-----------------|  
    |**And/Or**|Escolha **And** se essa cláusula e a próxima devem ambas ser verdadeiras para corresponder a um resultado. Escolha **Or** se essa cláusula ou a próxima podem ser verdadeiras para corresponder a um resultado.|  
    |**Campo**|Selecione o campo de relatório para usar na cláusula de filtro da lista de campos de dados exibida.|  
    |**Operador**|Selecione o operador que especifica o relacionamento que deseja na cláusula entre o campo e o valor.<br /><br /> =    É igual a<br /><br /> <>  Não é igual a<br /><br /> <    Menor que<br /><br /> >    Maior que<br /><br /> <=  Menor ou igual a<br /><br /> >= Maior ou igual a|  
    |**Valor**|Selecione ou insira o valor a ser procurado. Alguns campos listam os valores disponíveis para o campo.|  
  
3.  
  
#### <a name="to-create-a-profiler-report-filter-from-the-marks-report-view"></a>Para criar um filtro de relatório do criador de perfil na exibição de Relatório de Marcas  
  
1. Selecione **Marcas** na lista **Exibição Atual** na barra de ferramentas de Exibição de Relatório de Desempenho.  
  
    O relatório do criador de perfil de Marcas é exibido.  
  
2. Selecione o ETW ou amostragem mesmo que deseje usar como o ponto inicial do relatório.  
  
3. Pressione e segure a tecla CTRL e clique no evento que deseja usar como o ponto final do relatório.  
  
4. Clique com o botão direito do mouse e depois clique em uma das seguintes opções:  
  
   - **Adicionar filtro em Marcas** cria cláusulas de filtro que usam a coluna de Marca como campo de filtro.  
  
   - **Adicionar Filtro em Carimbos de Data/Hora** cria cláusulas de filtro que usam o carimbo de data/hora em milésimos de segundo como campo de filtro.  
  
     As duas opções filtram o arquivo de dados atual nos mesmo pontos inicial e final. Qualquer opção pode ser a melhor se exportar o filtro a ser usado em outros relatórios.  
  
#### <a name="to-load-an-existing-filter-from-a-file"></a>Para carregar um filtro existente de um arquivo  
  
1.  Na barra de ferramentas de Exibição de relatório de desempenho, clique em **Filtro de Importação**.  
  
     A caixa de diálogo **Carregar Filtro** é exibida.  
  
2.  Especifique o local e o nome do arquivo do filtro (.vspf) para carregar.  
  
#### <a name="to-execute-a-filter"></a>Para executar um filtro  
  
-   Na barra de ferramentas de Exibição de Relatório de Desempenho, clique em **Executar Filtro**.  
  
#### <a name="to-stop-a-filter-that-is-taking-too-long-to-execute"></a>Para interromper um filtro que esteja levando muito tempo para executar  
  
-   Na barra de ferramentas de Exibição de Relatório de Desempenho, clique em **Parar Filtro**.  
  
#### <a name="to-remove-a-filter-on-a-report-view"></a>Para remover um filtro em uma exibição de relatório  
  
1.  Exclua as linhas das cláusulas no filtro de Exibição de Relatório de Desempenho.  
  
2.  Na barra de ferramentas de Exibição de Relatório de Desempenho, clique em **Executar Filtro**.  
  
#### <a name="to-save-a-filter-to-a-file"></a>Para salvar um filtro em um arquivo  
  
1.  Na barra de ferramentas de Exibição de Relatório de Desempenho, clique em **Exportar Filtro**.  
  
     A caixa de diálogo **Salvar Filtro** é exibida.  
  
2.  Especifique o local e o nome do arquivo do filtro (.vspf) para salvar.  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando exibições de relatório das ferramentas de desempenho](../profiling/customizing-performance-tools-report-views.md)



