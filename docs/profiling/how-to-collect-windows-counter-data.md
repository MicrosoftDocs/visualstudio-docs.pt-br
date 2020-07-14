---
title: Como coletar dados do contador do Windows | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.performance.property.syscounter
- vs.performance.property.wincounter
helpviewer_keywords:
- windows counters
- performance tools, using windows counters
- profiling tools, using windows counters
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 16e29d82d1cee2237886d88a24929b4c794464a5
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330866"
---
# <a name="how-to-collect-windows-counter-data"></a>Como coletar dados do contador do Windows

Os contadores do Windows são contadores de desempenho do sistema que podem ser coletados em intervalos definidos durante a criação de perfil. Na exibição de Marcas do relatório das Ferramentas de Criação de Perfil, uma linha é rotulada **AutoMark** para cada intervalo de coleta. A linha contém colunas que descrevem os valores do contador de desempenho nesse intervalo. Para restringir a análise a um período de tempo entre duas marcas específicas, selecione as marcas, clique com o botão direito do mouse e selecione **Filtrar por**  >  **marcas** no menu de atalho.

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

## <a name="to-collect-windows-counter-data"></a>Para coletar dados do contador do Windows

1. No Gerenciador de Desempenho, clique com botão direito do mouse na sessão para a qual você deseja configurar os contadores do Windows e selecione **Propriedades**.

2. Nas **Páginas de Propriedades**, clique em **Contadores do Windows**.

3. Selecione a caixa de seleção **Coletar Contadores do Windows**.

4. Na caixa de texto **Intervalo de coleta (ms)**, digite um intervalo de tempo.

5. Selecione uma categoria da lista suspensa **Categoria de Contador**.

6. Selecione uma instância da lista suspensa de **Instância**.

7. Selecione os contadores que você deseja usar ao analisar seu aplicativo.

8. Clique em **aplicar.**

## <a name="see-also"></a>Veja também

[Configurar sessões](../profiling/configuring-performance-sessions.md) 
 de desempenho Propriedades da sessão de [desempenho](../profiling/performance-session-properties.md) 
 [Contadores de CPU e do Windows](../profiling/cpu-and-windows-counters.md)
