---
title: Salvando e Exportando Dados de Ferramentas de Desempenho | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- performance tools, saving and exporting reports
ms.assetid: 2e9b28fe-3ed2-4e1d-b9cb-0a5e384380b0
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8136369a09145c46c7989bebe12796642851a7b0
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35668094"
---
# <a name="save-and-export-performance-tools-data"></a>Salvar e exportar dados de ferramentas de desempenho
Este artigo descreve como salvar e exportar arquivos de dados de desempenho.  
  
## <a name="how-to-save-performance-data-files-as-analyzed-report-files"></a>Como salvar arquivos de dados de desempenho como arquivos de relatório analisados  
 É possível salvar exibições filtradas ou sem filtro de arquivos de dados de criação de perfil (.*vsp*) como arquivos de relatório analisados (.*vsps*). Um arquivo de relatório analisado pode ser exibido na janela de exibição de Relatório e é significativamente menor do que o arquivo .*vsp* original. No entanto, não é possível aplicar um filtro aos dados de um arquivo .*vsps*. É possível criar um arquivo de relatório analisado no Gerenciador de Desempenho sem abrir o arquivo no IDE (ambiente de desenvolvimento integrado) ou abrir e filtrar o arquivo .*vsp* e, em seguida, salvar os resultados.  
  
#### <a name="to-save-an-analyzed-performance-report-from-the-performance-explorer"></a>Salvar um relatório de desempenho analisado do Gerenciador de Desempenho  
  
1.  Em **Relatórios**, clique com o botão direito do mouse no arquivo de dados de criação de perfil a ser analisado e, em seguida, clique em **Salvar Analisados**.  
  
2.  Na caixa de diálogo **Salvar Dados Analisados**, especifique o diretório e digite o nome de arquivo.  
  
3.  Clique em **Salvar.**  
  
#### <a name="to-save-an-analyzed-performance-report-from-the-report-view-window"></a>Salvar um relatório de desempenho analisado da janela Exibição de Relatório  
  
1.  Abra o arquivo de dados de criação de perfil (.*vsp*) na janela de exibição de Relatório.  
  
2.  (Opcional) Aplique um filtro aos dados. Para obter mais informações, confira [Filtro de exibição de relatório de desempenho](../profiling/performance-report-view-filter.md).  
  
3.  Clique em **Salvar Analisados** na barra de ferramentas de janela Exibição de Relatório.  
  
4.  Na caixa de diálogo **Salvar Dados Analisados**, especifique o diretório e digite o nome de arquivo.  
  
5.  Clique em **Salvar.**  
  
## <a name="how-to-export-profiling-tools-reports-to-an-xml-or-csv-file"></a>Como exportar relatórios de ferramentas de criação de perfil para um arquivo .xml ou .csv  
 É possível exportar uma ou mais exibições de relatório de um arquivo .*vsp* ou de um arquivo de dados de criação de perfil .*vsps* como um arquivo separado por vírgulas ou XML. É possível filtrar os dados na janela Exibição de Relatório antes de exportar ou exportar exibições de relatório de todo o arquivo de dados na janela **Gerenciador de Desempenho**.  
  
> [!NOTE]
>  Também é possível copiar e colar linhas selecionadas da janela Exibição de Relatório como valores separados por tabulação.  
  
#### <a name="to-export-performance-reports-from-the-performance-explorer-window"></a>Exportar relatórios de desempenho da janela Gerenciador de Desempenho  
  
1.  No **Gerenciador de Desempenho**, selecione o relatório e, em seguida, clique com o botão direito do mouse e selecione **Exportar**.  
  
     A caixa de diálogo **Exportar Relatório** aparecerá.  
  
2.  Selecione as exibições de relatório que deseja exportar.  
  
3.  Em **Inserir prefixo no relatório**, especifique o prefixo que deseja adicionar ao nome do relatório.  
  
4.  Em **Local de Relatório Exportado**, especifique o diretório.  
  
5.  Em **Formato de relatório exportado**, selecione (delimitado por vírgula) (\*.csv\) ou Dados XML (\*.xml\).  
  
6.  Clique em **Exportar**.  
  
     Cada exibição de relatório será salva em um arquivo separado denominado \<prefix>_\<report view name>.\<csv&#124;xml>  
  
#### <a name="to-export-performance-reports-from-the-report-view-window"></a>Exportar relatórios de desempenho da janela Exibição de Relatório  
  
1.  Abra o arquivo .*vsp* na janela de exibição de Relatório.  
  
2.  (Opcional) Aplique um filtro aos dados. Para obter mais informações, confira [Filtro de exibição de relatório de desempenho](../profiling/performance-report-view-filter.md).  
  
3.  Clique em **Exportar Relatório** na barra de ferramentas de janela Exibição de Relatório.  
  
4.  Selecione as exibições de relatório que deseja exportar.  
  
5.  Em **Inserir prefixo no relatório**, especifique o prefixo que deseja adicionar ao nome do relatório.  
  
6.  Em **Local de Relatório Exportado**, especifique o diretório.  
  
7.  Em **Formato de relatório exportado**, selecione (delimitado por vírgula) (\*.csv) ou Dados XML (\*.xml).  
  
8.  Clique em **Exportar**.  
  
     Cada exibição de relatório será salva em um arquivo separado denominado \<prefix>_\<report view name>.\<csv&#124;xml>  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de Desempenho](../profiling/performance-explorer.md)   
 [Analisar dados de ferramentas de desempenho](../profiling/analyzing-performance-tools-data.md)   
 [Comparar arquivos de dados de desempenho](../profiling/comparing-performance-data-files.md)   
 [VSPerfReport](../profiling/vsperfreport.md)
