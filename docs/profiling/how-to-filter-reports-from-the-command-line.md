---
title: Como filtrar relatórios da linha de comando | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 6e9b140f-b44f-4a5c-bd65-d868ddc94023
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 3461965f0944200c44570cff5362aeeb143ed43c
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332242"
---
# <a name="how-to-filter-reports-from-the-command-line"></a>Como filtrar relatórios por meio da linha de comando
Ao usar as opções para o comando **VSPerfReport**, você pode filtrar relatórios para um segmento de tempo específico do arquivo de dados de criação de perfil ou restringir os dados a um ou mais processos ou threads. Para obter mais informações sobre esse comando, consulte [VSPerfReport](../profiling/vsperfreport.md).

|Opções|Descrição|
|-------------|-----------------|
|**StartTime:**[*valor*]|Mostrar apenas os dados coletados depois do valor (em milissegundos).|
|**EndTime:**[*valor*]|Mostrar apenas os dados coletados antes do valor (em milissegundos).|
|**FilterFile:** `VSPFFile`|Especifica o local de um arquivo de filtro que foi gerado na janela **relatório de desempenho do Visual Studio** .|
|**MsFilter:**[*tempo de início, duração*]|Mostrar apenas os dados de `StartTime` até a duração de `Duration` (em milissegundos).|
|**Processo:**[*pid*]|Mostrar somente os dados do processo especificado.|
|**Thread:**[*ThreadID*]|Mostra apenas os dados do thread especificado.|
|**Thread:**[*ThreadID, ProcessId*]|Mostrar somente os dados do thread especificado associados ao processo especificado.|
