---
title: Analisar o uso do banco de dados para projetos do .NET Core | Microsoft Docs
ms.date: 5/5/2020
ms.topic: conceptual
helpviewer_keywords:
- database, profiling
author: esteban-herrera
ms.author: esherrer
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: b369fe6998cd7ef134af765d6d849f41bc93527c
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290065"
---
# <a name="analyze-database-performance-using-the-database-tool"></a>Analisar o desempenho do banco de dados usando a ferramenta de banco de dados

Use a ferramenta de banco de dados para registrar as consultas de banco de dados que seu aplicativo faz durante uma sessão de diagnóstico. Em seguida, você pode analisar informações sobre consultas individuais para encontrar locais para melhorar o desempenho do aplicativo.

> [!NOTE]
> A ferramenta de banco de dados requer o Visual Studio 2019 versão 16,3 ou posterior e um projeto do .NET Core no Windows usando o [ADO.net]( https://docs.microsoft.com/dotnet/framework/data/adonet/ado-net-overview) ou o [Entity Framework Core](https://docs.microsoft.com/ef/core/).

## <a name="setup"></a>Instalação

1. Selecione **ALT + F2** para abrir o criador de perfil de desempenho no Visual Studio.

1. Marque a caixa de seleção **banco de dados** .

   ![Ferramenta de banco de dados selecionada](./media/db-launch.png "Ferramenta de banco de dados selecionada")

   > [!NOTE]
   > Se a ferramenta não estiver disponível para seleção, desmarque a caixa de seleção de todas as outras ferramentas, pois algumas ferramentas precisam ser executadas sozinhas. Para saber mais sobre como executar ferramentas juntas, consulte [usando ferramentas de criação de perfil na linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md).
   >
   > Se a ferramenta ainda não estiver disponível, verifique se o seu projeto atende aos requisitos anteriores. Verifique se o projeto está no modo de liberação para capturar os dados mais precisos.

1. Selecione o botão **Iniciar** para executar a ferramenta.

1. Depois que a ferramenta começar a ser executada, percorra o cenário no qual você deseja criar o perfil em seu aplicativo. Em seguida, selecione **parar coleta** ou feche seu aplicativo para ver seus dados.

1. Após a coleta parar, você verá uma tabela das consultas que foram executadas durante a sessão de criação de perfil.

   ![Ferramenta de banco de dados interrompida](./media/db-after.png "Ferramenta de banco de dados interrompida")

As consultas são organizadas em ordem cronológica, mas você pode classificá-las por qualquer uma das colunas. Você pode mostrar mais colunas clicando com o botão direito do mouse nos títulos das colunas. A seleção da coluna **Duration** ordena as consultas da mais longa duração até a mais curta.

Depois de encontrar uma consulta que você deseja investigar, clique com o botão direito do mouse na consulta. Em seguida, selecione **ir para o arquivo de origem** para ver qual código é responsável por essa consulta.

![Ir para o arquivo de origem selecionado](./media/db-gotosource.png "Ir para o arquivo de origem selecionado")

Se você selecionar um intervalo de tempo em um grafo, a tabela de consulta mostrará somente as consultas que ocorreram durante esse intervalo de tempo. Esse comportamento é especialmente útil quando você também executa a [ferramenta de uso da CPU](https://docs.microsoft.com/visualstudio/profiling/cpu-usage?view=vs-2019).

## <a name="see-also"></a>Veja também

- [Otimizando as configurações do criador de perfil](../profiling/optimize-profiler-settings.md)
