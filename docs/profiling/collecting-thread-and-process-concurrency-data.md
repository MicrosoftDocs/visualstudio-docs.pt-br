---
title: Coletar dados de simultaneidade do processo de & de thread
description: Use o método de criação de perfil de simultaneidade Ferramentas de Criação de Perfil para coletar dados sobre cada evento de sincronização que faz com que uma função aguarde o acesso aos recursos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- concurrency profiling method
- Profiling Tools, concurrency method
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 2f5065c3eafc9fb1cd9e36227a09bbf26ed321c6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99950202"
---
# <a name="collect-thread-and-process-concurrency-data"></a>Coletar dados de simultaneidade de thread e do processo

O método de criação de perfil de simultaneidade das Ferramentas de Criação de Perfil do Visual Studio permite coletar dados de contenção de recursos que inclui informações sobre cada evento de sincronização que faz com que uma função no aplicativo analisado aguarde para obter acesso a um recurso.

É possível especificar o método de criação de perfil de simultaneidade usando um dos seguintes recursos:

- Na primeira página do Assistente de Criação de Perfil, clique em **Simultaneidade**
- Na página **Geral** da caixa de diálogo de propriedades da sessão de desempenho, clique em **Simultaneidade**.
- Na barra de ferramentas do **Gerenciador de Desempenho**, na lista **Método**, clique em **Simultaneidade**.

## <a name="common-tasks"></a>Tarefas comuns

Você pode especificar opções adicionais na caixa de diálogo **páginas de propriedades** de _sessão de desempenho_ da sessão de desempenho. Para abrir essa caixa de diálogo:

- Em **Gerenciador de desempenho**, clique com o botão direito do mouse no nome da sessão de desempenho e clique em **Propriedades**.

As tarefas na tabela a seguir descrevem as opções que podem ser especificadas na caixa de diálogo _Sessão de Desempenho_**Páginas de Propriedades** quando você cria o perfil usando o método de simultaneidade.

|Tarefa|Conteúdo relacionado|
|----------|---------------------|
|Na página **Geral**, especifique detalhes de nomenclatura para o arquivo de dados de criação de perfil gerado (.vsp).|- [Como definir opções de nome de arquivo de dados de desempenho](../profiling/how-to-set-performance-data-file-name-options.md)|
|Na página **Iniciar**, especifique o aplicativo a ser iniciado se você tiver vários projetos .exe na solução do seu código.|- [Como especificar o binário a ser iniciado](../profiling/how-to-specify-the-binary-to-start.md)|
|Na página **Interação de Camada**, adicione dados de chamada ADO.NET à execução de criação de perfil.|- [Coletar dados de interação de camada](../profiling/collecting-tier-interaction-data.md)|
|Na página **Contadores do Windows**, especifique um ou mais contadores de desempenho de sistema operacional para serem adicionados aos dados de criação de perfil como marcas.|- [Como: coletar dados do contador do Windows](../profiling/how-to-collect-windows-counter-data.md)|
|Na página **avançado** , especifique a versão do .NET Framework tempo de execução para criar o perfil se os seus módulos de aplicativo usarem várias versões. Por padrão, a primeira versão carregada é analisada.|- [Como especificar o tempo de execução de .NET Framework](../profiling/how-to-specify-the-dotnet-framework-runtime.md)|
