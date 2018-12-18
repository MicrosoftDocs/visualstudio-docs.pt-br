---
title: Janela do Gerenciador de Desempenho | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.performanceexplorer
- vs.performance.explorer
helpviewer_keywords:
- performance tools, Performance Explorer
ms.assetid: cb6a6efc-93a5-49a2-8d03-6969b5f3b6d7
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 20a68ecb9f45265dd304a9bebf601020c6a300b8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51798190"
---
# <a name="performance-explorer-window"></a>Janela do Performance Explorer
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A janela do **Gerenciador de Desempenho** no IDE (ambiente de desenvolvimento integrado) do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] permite configurar e iniciar sessões de desempenho usando o as Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 **Requisitos**  
  
-   [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
## <a name="performance-explorer-toolbar"></a>Barra de Ferramentas do Gerenciador de Desempenho  
 As seguintes opções estão disponíveis na barra de ferramenta do **Gerenciador de Desempenho**:  
  
-   **Iniciar o Assistente de Desempenho** – Exibe o Assistente de Desempenho para adicionar uma nova sessão de desempenho à janela do Gerenciador de Desempenho.  
  
-   **Nova Sessão de Desempenho** – Adiciona uma sessão de desempenho vazia à janela do Gerenciador de Desempenho.  
  
-   **Launch** – a lista do botão de comando **Launch** permite iniciar o aplicativo de destino com criação de perfil habilitada imediatamente (**Inicializar com criação de perfil**) ou com a criação de perfil suspensa (**Inicializar com criação de perfil em pausa**).  
  
-   **Método** – Especifica se o método de criação de perfil da sessão é amostragem ou instrumentação.  
  
-   **Parar** – Sai imediatamente do aplicativo de destino e do criador de perfil.  
  
-   **Anexar/Desanexar** – exibe a caixa de diálogo **Anexar Criador de Perfil ao Processo** para selecionar um processo em execução ao qual anexar o criador de perfil.  
  
## <a name="performance-explorer-window"></a>Janela do Performance Explorer  
 A janela do **Gerenciador de Desempenho** contém um controle de árvore que exibe os binários e arquivos de dados do relatório de uma ou mais sessões de desempenho.  
  
-   **Nome da Sessão** – A raiz do controle de árvore contém o nome da sessão. Clique com o botão direito do mouse no nome de sessão para definir as propriedades de sessão ou para iniciar o aplicativo de destino e o criador de perfil.  
  
-   **Destinos** – Exibe os nomes dos binários que devem ser criados na sessão. Clique com botão direito do mouse em **Destinos** para adicionar ou remover um binário, projeto do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ou site. Clique com o botão direito do mouse no nome de um destino para definir propriedades para o binário individual.  
  
-   **Relatórios** – Exibe os nomes dos arquivos de dados do criador de perfil que são gerados para a sessão. Clique com botão direito do mouse em **Relatórios** para adicionar um relatório existente ou comparar dois arquivos de dados do criador de perfil. Clique com o botão direito do mouse em um nome de relatório para abrir, remover ou exportar um arquivo de dados do criador de perfil.  
  
## <a name="see-also"></a>Consulte também  
 [Visões gerais](../profiling/overviews-performance-tools.md)   
 [Configurando sessões de desempenho](../profiling/configuring-performance-sessions.md)   
 [Controlando a coleta de dados](../profiling/controlling-data-collection.md)



