---
title: Exibição tempo de vida do objeto | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.objectlifetime
helpviewer_keywords:
- lifetime, objects
- Objects Lifetime view
- profiling tools reports, Lifetime view
- performance reports, objects lifetime view
- profiling tools, Lifetime view
ms.assetid: d0501fdd-4b3a-4e74-b6ac-51d950a2e15b
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: d4ea486930d0ea9f266b4ee57b69a50f7c570651
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2020
ms.locfileid: "74772618"
---
# <a name="object-lifetime-view"></a>Exibição do tempo de vida do objeto
A exibição Tempo de Vida do Objeto está disponível quando **Também coletar dados de tempo de vida do objeto .NET** está marcada nas páginas de propriedades da **Sessão de Desempenho**.

 O coletor de lixo do .NET Framework gerencia a alocação e a liberação de memória para seu aplicativo. Para otimizar o desempenho do coletor de lixo, o heap gerenciado é dividido em três gerações: 0, 1 e 2. O coletor de lixo do runtime armazena novos objetos na geração 0. Os objetos que sobrevivem as coletas são promovidos e armazenados para as gerações 1 e 2.

 O coletor de lixo recupera memória, desalocando uma geração inteira de objetos. Para objetos que foram criados pelo aplicativo com perfil criado, a exibição do Tempo de vida do objeto exibe o número e o tamanho dos objetos e a geração na qual eles são recuperados.

## <a name="general"></a>Geral

|Coluna|Descrição|
|------------|-----------------|
|**Nome da Classe**|O nome de classe do tipo alocado.|
|**ID do Processo**|A ID de processo da execução de criação de perfil.|
|**Nome do processo**|O nome do processo.|
|**Nome do módulo**|O nome do módulo que contém a função.|
|**Caminho do Módulo**|O demarcador do módulo que contém a função.|

## <a name="instance-data"></a>Dados de instância
 Dados de instância indicam o número de objetos do tipo que foram criados na execução de criação de perfil e a geração na qual os objetos foram desalocados pelo coletor de lixo.

|Coluna|Descrição|
|------------|-----------------|
|**Instâncias**|O número de alocações de objetos desse tipo.|
|**% Total de Instâncias**|O percentual do número total de alocações feitas na execução da criação de perfil.|
|**Instâncias de Ger 0 Coletadas**|O número de instâncias do tipo que foram desalocadas na geração 0 do algoritmo de coleta de lixo.|
|**Instâncias de Ger 1 Coletadas**|O número de instâncias do tipo que foram desalocadas na geração 1 do algoritmo de coleta de lixo.|
|**Instâncias de Ger 2 Coletadas**|O número de instâncias do tipo que foram desalocadas na geração 2 do algoritmo de coleta de lixo.|
|**Instâncias Ativas ao Final**|O número de instâncias do tipo que não foram desalocadas até o final da execução de criação de perfil.|

## <a name="size-byte-data"></a>Dados de tamanho (bytes)
 Dados de tamanho (byte) indicam o tamanho de objetos do tipo que foram criados na execução de criação de perfil e a quantidade de memória que foi recuperada em cada geração na qual os objetos foram desalocados.

|Coluna|Descrição|
|------------|-----------------|
|**Total de Bytes Alocados**|O número total de bytes para todas as instâncias do tipo.|
|**% Total de Bytes**|O percentual do número total de bytes alocados na execução de criação que foram alocados para as instâncias desse tipo.|
|**Bytes de Ger 0 Coletados**|O tamanho das instâncias do tipo que foram desalocadas na geração 0 do algoritmo de coleta de lixo.|
|**Bytes de Ger 1 Coletados**|O tamanho das instâncias do tipo que foram desalocadas na geração 1 do algoritmo de coleta de lixo.|
|**Bytes de Ger 2 Coletados**|O tamanho das instâncias do tipo que foram desalocadas na geração 2 do algoritmo de coleta de lixo.|

## <a name="large-object-heap-data"></a>Dados de heap de objeto grande
 O alocador de memória .NET gerencia objetos muito grandes em um local separado de heap gerenciado padrão. Dados de heap de objeto grande indicam o número e tamanho dos objetos do tipo que foram gerenciados neste local.

|Coluna|Descrição|
|------------|-----------------|
|**Instâncias de Heap de Objetos Grandes Coletados**|O número de instâncias desse tipo que estavam no heap de objeto grande e que foram coletadas na execução da criação de perfil.|
|**Bytes de Heap de Objetos Grandes Coletados**|O tamanho, em bytes, das instâncias desse tipo que estavam no heap de objeto grande e que foram coletadas na execução da criação de perfil.|

## <a name="see-also"></a>Confira também
- [Exibições de dados de memória .NET](../profiling/dotnet-memory-data-views.md)
