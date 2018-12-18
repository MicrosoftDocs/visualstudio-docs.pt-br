---
title: Janela do Gerenciador de Desempenho | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performanceexplorer
- vs.performance.explorer
helpviewer_keywords:
- performance tools, Performance Explorer
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f27d1436aaeb0ec75876edf9119dff93f7539483
ms.sourcegitcommit: 42ea834b446ac65c679fa1043f853bea5f1c9c95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31582105"
---
# <a name="performance-explorer-window"></a>Janela do Performance Explorer

A janela **Gerenciador de Desempenho** no IDE do Visual Studio permite que você configure e inicie sessões de desempenho usando as Ferramentas de Criação de Perfil do Visual Studio.

## <a name="performance-explorer-toolbar"></a>Barra de Ferramentas do Gerenciador de Desempenho

As seguintes opções estão disponíveis na barra de ferramenta do **Gerenciador de Desempenho**:

- **Iniciar o Assistente de Desempenho** – Exibe o Assistente de Desempenho para adicionar uma nova sessão de desempenho à janela do Gerenciador de Desempenho.

- **Nova Sessão de Desempenho** – Adiciona uma sessão de desempenho vazia à janela do Gerenciador de Desempenho.

- **Launch** – a lista do botão de comando **Launch** permite iniciar o aplicativo de destino com criação de perfil habilitada imediatamente (**Inicializar com criação de perfil**) ou com a criação de perfil suspensa (**Inicializar com criação de perfil em pausa**).

- **Método** – Especifica se o método de criação de perfil da sessão é amostragem ou instrumentação.

- **Parar** – Sai imediatamente do aplicativo de destino e do criador de perfil.

- **Anexar/Desanexar** – exibe a caixa de diálogo **Anexar Criador de Perfil ao Processo** para selecionar um processo em execução ao qual anexar o criador de perfil.

## <a name="performance-explorer-window"></a>Janela do Performance Explorer

A janela do **Gerenciador de Desempenho** contém um controle de árvore que exibe os binários e arquivos de dados do relatório de uma ou mais sessões de desempenho.

- **Nome da Sessão** – A raiz do controle de árvore contém o nome da sessão. Clique com o botão direito do mouse no nome de sessão para definir as propriedades de sessão ou para iniciar o aplicativo de destino e o criador de perfil.

- **Destinos** – Exibe os nomes dos binários que devem ser criados na sessão. Clique com botão direito do mouse em **Destinos** para adicionar ou remover um binário, projeto do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ou site. Clique com o botão direito do mouse no nome de um destino para definir propriedades para o binário individual.

- **Relatórios** – Exibe os nomes dos arquivos de dados do criador de perfil que são gerados para a sessão. Clique com botão direito do mouse em **Relatórios** para adicionar um relatório existente ou comparar dois arquivos de dados do criador de perfil. Clique com o botão direito do mouse em um nome de relatório para abrir, remover ou exportar um arquivo de dados do criador de perfil.

## <a name="see-also"></a>Consulte também

[Visões gerais](../profiling/overviews-performance-tools.md)  
[Configurando sessões de desempenho](../profiling/configuring-performance-sessions.md)  
[Controlando a coleta de dados](../profiling/controlling-data-collection.md)