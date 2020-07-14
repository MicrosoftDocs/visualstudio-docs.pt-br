---
title: Como escolher métodos de coleção | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- performance tools, choosing collection method
- profiling tools, choosing collection method
- performance collection methods
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 4dbc54fc394f75778f74d9b6b02e93882129cdb9
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329267"
---
# <a name="how-to-choose-collection-methods"></a>Como escolher métodos de coleta

As Ferramentas de Criação de Perfil do Visual Studio dão suporte a três métodos de coleta de dados de desempenho: amostragem, instrumentação e simultaneidade. Você também pode usar o método de amostragem ou instrumentação para coletar dados de tempo de vida e de alocação de memória do .NET.

Você pode usar a propriedade **Método** da sessão de desempenho para especificar o método de coleta mais apropriado para o seu aplicativo. É possível definir o método de coleta no Assistente de Desempenho, do Gerenciador de Desempenho ou de páginas de propriedades de uma sessão de desempenho. Se você estiver usando ferramentas de linha de comando, consulte [Criação de perfil na linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md) para obter mais informações.

## <a name="performance-wizard"></a>Assistente de Desempenho

### <a name="to-select-a-collection-method-using-the-performance-wizard"></a>Para selecionar um método de coleta usando o Assistente de Desempenho

- Na primeira página do assistente, selecione uma das seguintes opções:

| Opção | Descrição |
|----------------------------| - |
| **Amostragem de CPU** | Coleta estatísticas de aplicativo que são úteis para a análise inicial e para analisar problemas de utilização de CPU. |
| **Instrumentação** | Coleta dados de tempo detalhados que são úteis para análise concentrada e para analisar problemas de desempenho de entrada/saída. |
| **Alocação de memória do .NET** | Coleta dados de alocação de memória do .NET Framework usando o método de criação de perfil de amostragem. |
| **Simultaneidade** | Coleta dados de contenção de recursos numéricos. |

## <a name="performance-explorer"></a>Performance Explorer

### <a name="to-select-a-collection-method-using-performance-explorer"></a>Para selecionar um método de coleta usando o Gerenciador de Desempenho

1. Na barra de ferramentas do **Gerenciador de Desempenho**, clique na seta ao lado da lista suspensa **Método**.

2. Clique no método de coleta que você preferir.

## <a name="performance-session-property-pages"></a>Páginas de propriedades da Sessão de Desempenho

### <a name="to-select-the-sampling-or-instrumentation-method-using-performance-session-properties"></a>Para selecionar o método de amostragem ou de instrumentação usando propriedades da sessão de desempenho

1. No **Gerenciador de Desempenho**, selecione a sessão de desempenho.

     Um nome de arquivo de sessão de desempenho tem uma extensão .*psess*.

2. Clique com o botão direito do mouse na sessão de desempenho e, em seguida, clique em **Propriedades**.

3. Nas **Páginas de Propriedades**, clique em **Geral**.

4. Clique no método de coleta que você preferir.

    - Para obter informações sobre as outras opções que estão disponíveis ao coletar dados de amostragem, consulte [Coletando estatísticas de desempenho usando amostragem](../profiling/collecting-performance-statistics-by-using-sampling.md)

    - Para obter informações sobre as outras opções que estão disponíveis ao coletar dados de amostragem, consulte [Coletando dados de tempo detalhados usando instrumentação](../profiling/collecting-detailed-timing-data-by-using-instrumentation.md).

### <a name="to-select-net-memory-data-collection-by-using-performance-session-properties"></a>Para selecionar a coleção de dados de memória do .NET usando as propriedades da sessão de desempenho

1. No **Gerenciador de Desempenho**, selecione a sessão de desempenho.

     Um nome de arquivo de sessão de desempenho tem uma extensão .psess.

2. Clique com o botão direito do mouse na sessão de desempenho e, em seguida, clique em **Propriedades**.

3. Nas **Páginas de Propriedades**, clique em **Geral**.

4. Clique em **Amostragem** ou **Instrumentação**.

5. Clique em **Coletar informações de alocação de objeto .NET** para coletar o tamanho e o número de alocações de objeto do .NET Framework.

6. (Opcional) Clique em **Também coletar informações de tempo de vida do objeto .NET** para coletar dados sobre as gerações de coleta de lixo nas quais a memória do objeto foi recuperada.

     Para obter informações sobre as outras opções disponíveis durante a coleta de dados da memória do .NET, confira [Coletar dados de tempo de vida e de alocação de memória do .NET](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md).

### <a name="to-select-concurrency-data-collection-by-using-performance-session-properties"></a>Para selecionar a coleta de dados de simultaneidade usando as propriedades da sessão de desempenho

1. Em **Gerenciador de desempenho**, clique com o botão direito do mouse na sessão de desempenho e clique em **Propriedades**.

2. Nas **Páginas de Propriedades**, clique em **Geral**.

3. Clique em **Simultaneidade**.

## <a name="see-also"></a>Veja também

[Configurar sessões](../profiling/configuring-performance-sessions.md) 
 de desempenho [Entender os valores](../profiling/understanding-sampling-data-values.md) 
 de dados de amostragem [Propriedades da sessão de desempenho](../profiling/performance-session-properties.md)
