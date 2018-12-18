---
title: Como criar um relatório de comparação de criador de perfil por meio de um prompt de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 00548d16-eb5b-46f7-8a65-862f98a43831
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 88fac8339491acbe73a4a446cde8afb54fa63143
ms.sourcegitcommit: 1b9c1e333c2f096d35cfc77e846116f8e5054557
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34814645"
---
# <a name="how-to-create-a-profiler-comparison-report-from-a-command-prompt"></a>Como criar um relatório de comparação de criador de perfil por meio de um prompt de comando
Você pode gerar um relatório de Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] que compara os dados de desempenho de dois arquivos de dados de criação de perfil (.*vsp* ou .*vsps*). O relatório mostra as diferenças, as regressões de desempenho e as melhorias que ocorreram de uma sessão de criação de perfil para a outra. Os valores no relatório apresentam o delta ou alteração, da linha de base do primeiro arquivo que você especificar. Esse delta é calculado determinando a diferença entre o valor antigo, que é o valor de linha de base e o valor do resultado da nova análise. As comparações de dados do criador de perfil podem ser baseadas nas funções no código, nos módulos no aplicativo, nas linhas, nos IPs (ponteiros de instrução) e nos tipos.  
  
 Para listar os identificadores dos campos e categorias de comparação, digite a seguinte linha de comando:  
  
 **VSPerfReport /querydifftables**  *VspFileName1* *VspFileName2*  
  
 Use a sintaxe a seguir para criar o relatório de comparação:  
  
 **VSPerfReport /diff**  `VspFileName1` *VspFileName2* [**/**`Options`]  
  
 Você pode adicionar opções da tabela a seguir para a linha de comando **VSPerfReport /diff**.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**DiffThreshold:**[*Value*]|Ignore a diferença se ela estiver abaixo desse valor de limite de percentual. Além disso, novos dados com valores abaixo desse limite não aparecerão.|  
|**DiffTable:** *TableName*|Use esta tabela para comparar arquivos. Por padrão, a tabela de funções é usada. Especifique o identificador que está listado em **VSPerfReport /querydifftables**.|  
|**DiffColumn:** *ColumnName*|Use essa coluna para comparar valores. Por padrão, a coluna de porcentagem de amostras exclusivas é usada. Especifique o identificador que está listado em **VSPerfReport /querydifftables**.|