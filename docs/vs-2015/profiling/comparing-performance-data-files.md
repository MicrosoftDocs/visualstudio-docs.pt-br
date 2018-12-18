---
title: Comparando arquivos de dados de desempenho | Microsoft Docs
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
- profiling tools, comparing profiling tools report files
- profiling tools reports, comparing
ms.assetid: e6fda144-f21d-4912-9d16-1b8d3555a210
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3aa37462915b3155a21248a968325a24b8da05bd
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741579"
---
# <a name="comparing-performance-data-files"></a>Comparando arquivos de dados de desempenho
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A funcionalidade de comparação dos arquivos de dados das Ferramentas de Criação de Perfil permite selecionar dois arquivos de relatório (.VSP /ou .VSPS) e gerar um relatório que mostra as diferenças, regressões de desempenho e melhorias que ocorreram de uma sessão de criação de perfil para outra.  
  
 Um relatório de comparação de arquivos de dados de Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] compara os resultados de uma análise em um arquivo de dados de criação de perfil com os resultados de uma análise de linha de base em outro arquivo de dados. Os dois arquivos de dados devem ter sido gerados usando o mesmo método de criação de perfil. O relatório das comparações analisadas é salvo como um arquivo .vsps.  
  
 O modo de exibição do relatório de comparação apresenta uma exibição de tabela dos dados alterados. A tabela apresenta o delta ou a alteração da linha de base. O delta é calculado determinando a diferença entre o valor antigo, o valor de linha de base e o valor do resultado da nova análise.  
  
 As comparações de dados do criador de perfil podem ser baseadas nas funções no código, nos módulos no aplicativo, nas linhas, nos IPs (ponteiros de instrução) e nos tipos.  
  
 Os dados de criação de perfil disponíveis para comparação incluem as informações exibidas nas colunas. Para obter definições desses nomes de coluna, consulte [Exibições de relatório de desempenho](../profiling/performance-report-views.md).  
  
 Um limite pode ser definido para reduzir o ruído e filtrar dados na exibição de tabela de comparação das linhas que não tenham sido alterados por uma quantidade especificada.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Como comparar arquivos de dados de desempenho](../profiling/how-to-compare-performance-data-files.md)



