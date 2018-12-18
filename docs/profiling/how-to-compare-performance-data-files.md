---
title: Como comparar arquivos de dados de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vsperf.choosediffbinaries
helpviewer_keywords:
- profiling tools, how to compare profiler result files
- profiler result files, how to compare
ms.assetid: 1905b45d-c6b3-43c8-87b1-1aee734f37f9
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: eeb9f26091deaf995ef1221d39aa7264553f5c70
ms.sourcegitcommit: 1b9c1e333c2f096d35cfc77e846116f8e5054557
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34815373"
---
# <a name="how-to-compare-performance-data-files"></a>Como comparar arquivos de dados de desempenho
Você pode comparar os resultados de dois arquivos de dados de criadores de perfil diferentes (.*vsp* ou .*vsps*), criando um relatório ou uma exibição de comparação ("Diff"). A comparação mostra as diferenças, regressões de desempenho e as melhorias que ocorreram de uma sessão de criação de perfil para a outra.  
  
 O relatório de Comparação apresenta uma exibição de tabela dos dados. A tabela apresenta o delta ou a alteração da linha de base. Isso é calculado determinando a diferença entre o valor antigo, o valor de linha de base e o valor do resultado da nova análise.  
  
 As comparações de dados do criador de perfil podem ser baseadas nas funções no código, nos módulos no aplicativo, nas linhas, nos IPs (ponteiros de instrução) e nos tipos.  
  
 Um limite pode ser definido para reduzir o ruído e filtrar na exibição de tabela os dados das linhas que não tenham sido alteradas por uma quantidade especificada.  
  
### <a name="to-create-comparison-file-view-for-a-project-in-performance-explorer"></a>Para criar uma exibição de arquivo de comparação para um projeto no Gerenciador de Desempenho  
  
1.  No **Gerenciador de Desempenho**, em **Relatórios**, selecione o arquivo de relatório .*vsp* ou .*vsps* que você deseja usar como os valores de linha de base para a comparação.  
  
2.  Selecione os arquivos de relatório .*vsp* ou .*vsps* que você deseja comparar.  
  
3.  Clique com o botão direito do mouse em um dos arquivos selecionados e, em seguida, clique em **Comparar Relatórios**.  
  
### <a name="to-compare-values"></a>Para comparar valores  
  
1.  Selecione a guia **Relatório de Comparação** na janela de Exibição de Relatório.  
  
2.  Na lista suspensa **Tabela**, selecione a função ou os módulos para comparar.  
  
3.  Na lista suspensa **Coluna**, selecione o valor que você deseja comparar.  
  
4.  (opcional) Digite um valor para **Limite**.  
  
5.  Clique em **Aplicar**.  
  
### <a name="to-compare-report-files"></a>Para comparar arquivos de relatório  
  
1.  No menu **Analisar**, selecione **Comparar Relatórios de Desempenho**.  
  
2.  Na janela **Selecionar arquivos de análise para comparação**, procure e selecione o arquivo de análise (.*vsp* ou .*vsps*) do **Arquivo de Linha de Base** e o **Arquivo de Comparação** (.*vsp* ou .*vsps*).  
  
3.  Clique em **OK**.