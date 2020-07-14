---
title: Como criar um relatório de comparação do criador de perfil a partir de um prompt de comando | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 00548d16-eb5b-46f7-8a65-862f98a43831
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 8f9679a99ee23886f660914d8914001e395ff797
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85328641"
---
# <a name="how-to-create-a-profiler-comparison-report-from-a-command-prompt"></a>Como criar um relatório de comparação de criador de perfil por meio de um prompt de comando
Você pode gerar um relatório de Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] que compara os dados de desempenho de dois arquivos de dados de criação de perfil (.*vsp* ou .*vsps*). O relatório mostra as diferenças, as regressões de desempenho e as melhorias que ocorreram de uma sessão de criação de perfil para a outra. Os valores no relatório apresentam o delta ou alteração, da linha de base do primeiro arquivo que você especificar. Esse delta é calculado determinando a diferença entre o valor antigo, que é o valor de linha de base e o valor do resultado da nova análise. As comparações de dados do criador de perfil podem ser baseadas nas funções no código, nos módulos no aplicativo, nas linhas, nos IPs (ponteiros de instrução) e nos tipos.

 Para listar os identificadores dos campos e categorias de comparação, digite a seguinte linha de comando:

 **VSPerfReport /querydifftables**  *VspFileName1* *VspFileName2*

 Use a sintaxe a seguir para criar o relatório de comparação:

 **VSPerfReport/diff** `VspFileName1` *VspFileName2* [ **/** `Options` ]  

 Você pode adicionar opções da tabela a seguir para a linha de comando **VSPerfReport /diff**.

|Opção|Descrição|
|------------|-----------------|
|**DiffThreshold:**[*Value*]|Ignore a diferença se ela estiver abaixo desse valor de limite de percentual. Além disso, novos dados com valores abaixo desse limite não aparecerão.|
|**DiffTable:** *TableName*|Use esta tabela para comparar arquivos. Por padrão, a tabela de funções é usada. Especifique o identificador que está listado em **VSPerfReport /querydifftables**.|
|**DiffColumn:** *ColumnName*|Use essa coluna para comparar valores. Por padrão, a coluna de porcentagem de amostras exclusivas é usada. Especifique o identificador que está listado em **VSPerfReport /querydifftables**.|
