---
title: Como comparar arquivos de dados de desempenho | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vsperf.choosediffbinaries
helpviewer_keywords:
- profiling tools, how to compare profiler result files
- profiler result files, how to compare
ms.assetid: 1905b45d-c6b3-43c8-87b1-1aee734f37f9
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 5fdb8057823732503a215fb4f2c12ebee33b34c4
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330821"
---
# <a name="how-to-compare-performance-data-files"></a>Como comparar arquivos de dados de desempenho
Você pode comparar os resultados de dois arquivos de dados do criador de perfil diferentes (.* VSP* ou. *vsps*) Criando um relatório ou exibição de comparação ("diff"). A comparação mostra as diferenças, regressões de desempenho e as melhorias que ocorreram de uma sessão de criação de perfil para a outra.

 O relatório de Comparação apresenta uma exibição de tabela dos dados. A tabela apresenta o delta ou a alteração da linha de base. Isso é calculado determinando a diferença entre o valor antigo, o valor de linha de base e o valor do resultado da nova análise.

 As comparações de dados do criador de perfil podem ser baseadas nas funções no código, nos módulos no aplicativo, nas linhas, nos IPs (ponteiros de instrução) e nos tipos.

 Um limite pode ser definido para reduzir o ruído e filtrar na exibição de tabela os dados das linhas que não tenham sido alteradas por uma quantidade especificada.

### <a name="to-create-comparison-file-view-for-a-project-in-performance-explorer"></a>Para criar uma exibição de arquivo de comparação para um projeto no Gerenciador de Desempenho

1. Em **Gerenciador de desempenho**, em **relatórios**, selecione o. *VSP* ou. *vsps* arquivo de relatório que você deseja usar como os valores de linha de base para comparação.

2. Selecione o. *VSP* ou. *vsps* os arquivos de relatório que você deseja comparar.

3. Clique com o botão direito do mouse em um dos arquivos selecionados e, em seguida, clique em **Comparar Relatórios**.

### <a name="to-compare-values"></a>Para comparar valores

1. Selecione a guia **Relatório de Comparação** na janela de Exibição de Relatório.

2. Na lista suspensa **Tabela**, selecione a função ou os módulos para comparar.

3. Na lista suspensa **Coluna**, selecione o valor que você deseja comparar.

4. (opcional) Digite um valor para **Limite**.

5. Clique em **Aplicar**.

### <a name="to-compare-report-files"></a>Para comparar arquivos de relatório

1. No menu **Analisar**, selecione **Comparar Relatórios de Desempenho**.

2. Na janela **selecionar arquivos de análise para comparação** , procure e selecione o arquivo de análise de **arquivo de linha de base** (.* VSP* ou. *vsps*) e o **arquivo de comparação** (.* VSP* ou. *vsps*).

3. Clique em **OK**.
