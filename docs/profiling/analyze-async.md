---
title: Analisar o desempenho do código assíncrono do .NET | Microsoft Docs
ms.date: 5/5/2020
ms.topic: conceptual
helpviewer_keywords:
- asynchronous, async, profiling
author: esteban-herrera
ms.author: esherrer
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 49091ba472637d480c04c39f0170c2aee00595d2
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290066"
---
# <a name="analyze-performance-of-net-asynchronous-code"></a>Analisar o desempenho do código assíncrono do .NET

Use a ferramenta Async do .NET para analisar o desempenho do código assíncrono em seu aplicativo.

> [!NOTE]
> A ferramenta Async do .NET requer o Visual Studio 2019 versão 16,7 ou posterior e um projeto .NET que usa **Async** e **Await**.

## <a name="setup"></a>Instalação

1. Selecione **ALT + F2** para abrir o criador de perfil de desempenho no Visual Studio.

1. Marque a caixa de seleção **.net Async** .

   ![Ferramenta assíncrona do .NET selecionada](../profiling/media/async-tool-selected.png "Ferramenta assíncrona do .NET selecionada")

1. Clique no botão **Iniciar** para executar a ferramenta.

1. Depois que a ferramenta começar a ser executada, percorra o cenário no qual você deseja criar o perfil em seu aplicativo. Em seguida, selecione **parar coleta** ou feche seu aplicativo para ver seus dados.

1. Após a coleta parar, você verá uma tabela das atividades que ocorreram durante a sessão de criação de perfil.

   ![Ferramenta Async do .NET interrompida](../profiling/media/async-tool-opened.png "Ferramenta Async do .NET interrompida")

Os eventos assíncronos são organizados em atividades cronologicamente. Cada exibe a hora de início, a hora de término e a duração.

Cada linha que corresponde a uma [tarefa](https://docs.microsoft.com/dotnet/api/system.threading.tasks) é rotulada na coluna **nome** . Para qualquer nome de tarefa que não pode ser resolvido, uma **tarefa no** rótulo é exibida. Ele é seguido pelo nome do método no qual a tarefa ocorre. Se uma atividade assíncrona não for concluída na sessão de coleta, um rótulo **incompleto** aparecerá na coluna **hora de término** .

Para investigar melhor uma tarefa ou atividade específica, clique com o botão direito do mouse na linha. Em seguida, selecione **ir para o arquivo de origem** para ver onde o código ocorreu na atividade.

![Ferramenta Async do .NET com ir para arquivo de origem selecionado](../profiling/media/async-tool-gotosource.png "Ferramenta Async do .NET com ir para arquivo de origem selecionado")

## <a name="see-also"></a>Veja também

- [Otimizando as configurações do criador de perfil](../profiling/optimize-profiler-settings.md)
