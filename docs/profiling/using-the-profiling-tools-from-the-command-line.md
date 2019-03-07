---
title: Usando as Ferramentas de Criação de Perfil na Linha de Comando | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- command line, performance tools
- command-line tools, performance tools
- profiling tools,command line
- tools, command-line
- command line, tools
ms.assetid: 6593fa82-181e-4009-a0ed-02aa24c2c063
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 936d2bfe4eecd3e36553cef7c5779f201e190619
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56615813"
---
# <a name="use-the-profiling-tools-from-the-command-line"></a>Usar as Ferramentas de Criação de Perfil por meio da linha de comando
É possível usar as ferramentas da linha de comando das Ferramentas de Criação de Perfil [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para criar perfis de aplicativo no prompt de comando e automatizar a criação de perfil usando arquivos em lote e scripts. Também é possível geral arquivos de relatório em um prompt de comando. Você pode usar o criador de perfil autônomo leve para coletar dados em computadores que não têm o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] instalado.

> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

## <a name="common-tasks"></a>Tarefas comuns

| Tarefa | Conteúdo relacionado |
| - | - |
| **Definir a localização de símbolos:** Para exibir os nomes de funções e parâmetros, o criador de perfil precisa ter acesso aos arquivos de símbolo (.*pdb*) dos binários analisados. Esses arquivos devem incluir os arquivos de símbolo para o sistema operacional da Microsoft e aplicativos que você deseja exibir em sua análise. Use o servidor de símbolos público da Microsoft para garantir que você têm os arquivos .*pdb* corretos dos binários da Microsoft. | -   [Como: Especificar locais de arquivo de símbolo da linha de comando](../profiling/how-to-specify-symbol-file-locations-from-the-command-line.md) |
| **Criar o perfil de seu aplicativo:** As ferramentas de linha de comando e opções que você usa para criar o perfil um aplicativo de destino dependem do tipo de aplicativo, o método de criação de perfil e se o destino é um aplicativo gerenciado ou nativo. | -   [Usar métodos de criação de perfil na linha de comando](../profiling/using-profiling-methods-to-collect-performance-data-from-the-command-line.md)<br />-   [Criar perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)<br />-   [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)<br />-   [Profile services (Serviços de perfil)](../profiling/command-line-profiling-of-services.md) |
| **Crie relatórios .xml e .csv:** A criação de perfil no prompt de comando cria arquivos de dados que podem ser exibidos na interface do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Gere também arquivos .*xml* ou .*csv* (valores separados por vírgula) dos dados usando a ferramenta de linha de comando VSPerfReport. | -   [Criar relatórios do criador de perfil por meio da linha de comando](../profiling/creating-profiler-reports-from-the-command-line.md)<br />-   [VSPerfReport](../profiling/vsperfreport.md) |
| **Criar o perfil de código em computadores sem o Visual Studio:** É possível usar o criador de perfil autônomo das Ferramentas de Criação de Perfil para coletar dados de aplicativos em computadores que não têm o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] instalado. | -   [Como: Instalar o criador de perfil independente](../profiling/how-to-install-the-stand-alone-profiler.md) |

## <a name="reference"></a>Referência
- [Referência de Ferramentas de Criação de Perfil da linha de comando](../profiling/command-line-profiling-tools-reference.md)

## <a name="see-also"></a>Consulte também
- [Gerenciador de Desempenho](../profiling/performance-explorer.md)