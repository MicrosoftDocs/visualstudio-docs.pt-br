---
title: Configurando sessões de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- common tasks, performance
- common tasks, profiling tools
- profiling tools, common tasks
- performance, gathering data
ms.assetid: e1c3ba41-ffca-4edf-9a7f-8a5a9244ef9b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1e00c31643a5f894612daa24d4a271856d8e21f1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49853424"
---
# <a name="configure-performance-sessions"></a>Configurar sessões de desempenho
Usando as Ferramentas de criação de perfil [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], é possível coletar uma grande variedade de dados de desempenho para um grande número de tipos de aplicativos. Esta seção mostra como usar o Assistente de Desempenho, as propriedades da sessão de desempenho e o binário de destino para configurar as Ferramentas de Criação de Perfil para coletar os dados que lhe interessam. As propriedades de configuração das Ferramentas de Criação de Perfil também podem ser usadas para controlar a quantidade de dados coletada em uma execução de criação de perfil. Para saber mais, confira [Controlar a coleta de dados](../profiling/controlling-data-collection.md).  
  
> [!NOTE]
>  Em muitos casos, usar as propriedades padrão do Assistente de Desempenho é uma maneira eficiente de coletar dados de criação de perfil. Para saber mais, veja o [Guia para iniciantes da criação de perfil de desempenho](../profiling/beginners-guide-to-performance-profiling.md) e a [Introdução](../profiling/getting-started-with-performance-tools.md).  
  
## <a name="common-tasks"></a>Tarefas comuns
  
| Tarefa | Conteúdo relacionado |
| - | - |
| **Definir as opções básicas de criação de perfil:** é necessário configurar [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] para usar o servidor de símbolos da Microsoft. Isso garantirá que você tenha acesso aos símbolos, como nomes de função e de parâmetro, da versão atual do Windows e de outros aplicativos da Microsoft. Também é possível especificar outras opções gerais antes que uma sessão de criação de perfil seja iniciada, como permissões de sistema para as ferramentas de criação de perfil e os nomes dos arquivos de dados de criação de perfil. | -   [Como fazer referência a informações de símbolo do Windows](../profiling/how-to-reference-windows-symbol-information.md)<br />-   [Como serializar informações de símbolo](../profiling/how-to-serialize-symbol-information.md)<br />-   [Como definir a sessão atual](../profiling/how-to-set-the-current-session.md)<br />-   [Como definir permissões](../profiling/how-to-set-permissions.md)<br />-   [Como definir opções do nome do arquivo de dados de desempenho](../profiling/how-to-set-performance-data-file-name-options.md) |
| **Especificar os dados que você deseja coletar:** os procedimentos usados para configurar uma sessão de criação de perfil dependem do tipo de aplicativo de destino para o qual você deseja criar um perfil e o tipo de dados de desempenho que você deseja coletar. | -   [Como escolher métodos de coleta](../profiling/how-to-choose-collection-methods.md)<br />-   [Coletar estatísticas de desempenho usando amostragem](../profiling/collecting-performance-statistics-by-using-sampling.md)<br />-   [Coletar a alocação de memória do .NET e os dados de tempo de vida](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)<br />-   [Coletar dados de tempo detalhados usando a instrumentação](../profiling/collecting-detailed-timing-data-by-using-instrumentation.md)<br />-   [Como criar perfil de código JavaScript em páginas da Web](../profiling/how-to-profile-javascript-code-in-web-pages.md)<br />-   [Coletar dados de simultaneidade do thread e do processo](../profiling/collecting-thread-and-process-concurrency-data.md)<br />-   [Coletar dados de desempenho adicionais](../profiling/collecting-additional-performance-data.md) |
| **Definir opções avançadas de configuração:** ao criar o perfil de aplicativos .NET Framework que carregam várias versões do CLR (Common Language Runtime), é possível especificar qual versão terá o perfil criado. Quando você tiver vários arquivos .exe em uma sessão de desempenho, será possível definir a ordem de inicialização dos binários. | -   [Como especificar o tempo de execução do .NET Framework](../profiling/how-to-specify-the-dotnet-framework-runtime.md)<br />-   [Como especificar o binário a iniciar](../profiling/how-to-specify-the-binary-to-start.md) |
  
## <a name="related-sections"></a>Seções relacionadas  
 [Controlar a coleta de dados](../profiling/controlling-data-collection.md)  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de Desempenho](../profiling/performance-explorer.md)