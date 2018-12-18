---
title: Salvando e Exportando Dados de Ferramentas de Desempenho | Microsoft Docs
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
- performance tools, saving and exporting reports
ms.assetid: 2e9b28fe-3ed2-4e1d-b9cb-0a5e384380b0
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a9b96ae54c91e80fe34c817f710cb400e61f9876
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51768502"
---
# <a name="saving-and-exporting-performance-tools-data"></a>Salvando e Exportando Dados de Ferramentas de Desempenho
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como salvar e exportar arquivos de dados de desempenho.  
  
##  <a name="BKMK_Save_Profiler_Data_Files_As_Analyzed_Report_Files"></a> Como Salvar Arquivos de Dados de Desempenho como Arquivos de Relatório Analisados  
 É possível salvar exibições filtradas ou sem filtro de arquivos de dados de criação de perfil (.vsp) como arquivos de relatório analisados (.vsps). Um arquivo de relatório analisado pode ser exibido na janela Exibir Relatório e é significativamente menor do que o arquivo .vsp original. No entanto, não é possível aplicar um filtro aos dados de um arquivo .vsps. É possível criar um arquivo de relatório analisado no Gerenciador de Desempenho sem abrir o arquivo no ambiente de desenvolvimento integrado (IDE) ou você pode abrir e filtrar o arquivo .vsp e salvar os resultados.  
  
#### <a name="to-save-an-analyzed-performance-report-from-the-performance-explorer"></a>Salvar um relatório de desempenho analisado do Gerenciador de Desempenho  
  
1.  Em **Relatórios**, clique com o botão direito do mouse no arquivo de dados de criação de perfil a ser analisado e, em seguida, clique em **Salvar Analisados**.  
  
2.  Na caixa de diálogo **Salvar Dados Analisados**, especifique o diretório e digite o nome de arquivo.  
  
3.  Clique em **Salvar.**  
  
#### <a name="to-save-an-analyzed-performance-report-from-the-report-view-window"></a>Salvar um relatório de desempenho analisado da janela Exibição de Relatório  
  
1.  Abra o arquivo de dados de criação de perfil (.vsp) na janela Exibição de Relatório.  
  
2.  (Opcional) Aplique um filtro aos dados. Para obter mais informações, consulte [Filtro de Exibição de Relatório de Desempenho](../profiling/performance-report-view-filter.md).  
  
3.  Clique em **Salvar Analisados** na barra de ferramentas de janela Exibição de Relatório.  
  
4.  Na caixa de diálogo **Salvar Dados Analisados**, especifique o diretório e digite o nome de arquivo.  
  
5.  Clique em **Salvar.**  
  
## <a name="how-to-export-profiling-tools-reports-to-an-xml-or-csv-file"></a>Como Exportar Relatórios de Ferramentas de Criação de Perfil para um Arquivo .XML ou .CSV  
 É possível exportar uma ou mais exibições de relatório de um arquivo .vsp ou arquivo de dados de criação de perfil .vsps como um arquivo separado por vírgulas ou XML. É possível filtrar os dados na janela Exibição de Relatório antes de exportar ou exportar exibições de relatório de todo o arquivo de dados na janela **Gerenciador de Desempenho**.  
  
> [!NOTE]
>  Também é possível copiar e colar linhas selecionadas da janela Exibição de Relatório como valores separados por tabulação.  
  
#### <a name="to-export-performance-reports-from-the-performance-explorer-window"></a>Exportar relatórios de desempenho da janela Gerenciador de Desempenho  
  
1.  No **Gerenciador de Desempenho**, selecione o relatório e, em seguida, clique com o botão direito do mouse e selecione **Exportar**.  
  
     A caixa de diálogo **Exportar Relatório** aparecerá.  
  
2.  Selecione as exibições de relatório que deseja exportar.  
  
3.  Em **Inserir prefixo no relatório**, especifique o prefixo que deseja adicionar ao nome do relatório.  
  
4.  Em **Local de Relatório Exportado**, especifique o diretório.  
  
5.  Em **Formato de Relatório Exportado**, selecione (*.csv) (delimitado por vírgulas) ou Dados XML (\*.xml).  
  
6.  Clique em **Exportar**.  
  
     Cada exibição de relatório será salva em um arquivo separado denominado \<prefix>_\<report view name>.\<csv&#124;xml>  
  
#### <a name="to-export-performance-reports-from-the-report-view-window"></a>Exportar relatórios de desempenho da janela Exibição de Relatório  
  
1.  Abra o arquivo .vsp na janela Exibição de Relatório.  
  
2.  (Opcional) Aplique um filtro aos dados. Para obter mais informações, consulte [Filtro de Exibição de Relatório de Desempenho](../profiling/performance-report-view-filter.md).  
  
3.  Clique em **Exportar Relatório** na barra de ferramentas de janela Exibição de Relatório.  
  
4.  Selecione as exibições de relatório que deseja exportar.  
  
5.  Em **Inserir prefixo no relatório**, especifique o prefixo que deseja adicionar ao nome do relatório.  
  
6.  Em **Local de Relatório Exportado**, especifique o diretório.  
  
7.  Em **Formato de Relatório Exportado**, selecione (*.csv) (delimitado por vírgulas) ou Dados XML (\*.xml).  
  
8.  Clique em **Exportar**.  
  
     Cada exibição de relatório será salva em um arquivo separado denominado \<prefix>_\<report view name>.\<csv&#124;xml>  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de Desempenho](../profiling/performance-explorer.md)   
 [Analisando dados de ferramentas de desempenho](../profiling/analyzing-performance-tools-data.md)   
 [Comparando Arquivos de Dados de Desempenho](../profiling/comparing-performance-data-files.md)   
 [VSPerfReport](../profiling/vsperfreport.md)



