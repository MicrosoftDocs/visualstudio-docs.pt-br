---
title: Medir o desempenho da linha de comando
description: Meça o desempenho da CPU e o uso da memória gerenciada em seu aplicativo na linha de comando.
ms.custom: ''
ms.date: 02/21/2020
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools, command-line
- Diagnostics Tools, command-line
- CPU Usage, command-line
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: ba5915e687bd4e1f6afb200f4ca3e7a866c6151c
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285838"
---
# <a name="measure-application-performance-from-the-command-line"></a>Medir o desempenho do aplicativo na linha de comando

Colete informações de desempenho sobre um aplicativo usando ferramentas de linha de comando.

No exemplo descrito neste artigo, você coletará informações de desempenho para o Bloco de notas da Microsoft, mas o mesmo método poderá ser usado para analisar qualquer processo.

## <a name="prerequisites"></a>Pré-requisitos

* Visual Studio 2019 ou versões posteriores

* Familiaridade com ferramentas de linha de comando

* Para coletar informações de desempenho em um computador remoto sem o Visual Studio instalado, instale as [ferramentas de desempenho do Visual Studio](https://visualstudio.microsoft.com/downloads#remote-tools-for-visual-studio-2019) no computador remoto. A versão das ferramentas deve corresponder à sua versão do Visual Studio.

## <a name="collect-performance-data"></a>Coletar dados de desempenho

A criação de perfil usando as ferramentas da CLI de Diagnóstico do Visual Studio funciona com a anexação da ferramenta de criação de perfil, junto com um dos agentes coletores, a um processo. Ao anexar a ferramenta de criação de perfil, você inicia uma sessão de diagnóstico que captura e armazena dados de criação de perfil até a ferramenta ser interrompida, cujo momento esses dados são exportados para um arquivo *.diagsession*. Em seguida, você pode abrir esse arquivo no Visual Studio para analisar os resultados.

1. Inicie o Bloco de notas e, em seguida, abra o Gerenciador de Tarefas para obter o PID (ID de processo). No Gerenciador de Tarefas, encontre o PID na guia **Detalhes**.

1. Abra um prompt de comando e altere para o diretório com o executável do agente de coleta, normalmente aqui.

   ```<Visual Studio installation folder>\2019\Preview\Team Tools\DiagnosticsHub\Collector\```

1. Inicie *VSDiagnostics.exe* digitando o comando a seguir.

   ```cmd
   VSDiagnostics.exe start <id> /attach:<pid> /loadConfig:<configFile>
   ```

   Os argumentos que precisam ser incluídos são:

   * \<*id*>Identifica a sessão de coleta. A ID precisa ser um número entre 1 e 255.
   * \<*pid*>, O PID do processo no qual você deseja criar o perfil, nesse caso, o PID encontrado na etapa 1
   * \<*configFile*>, o arquivo de configuração para o agente de coleta que você deseja iniciar. Para obter mais informações, confira [Arquivos de configuração para os agentes](#config_file).

1. Redimensione o Bloco de notas ou digite algo para garantir que algumas informações interessantes de criação de perfil sejam coletadas.

1. Interrompa a sessão de coleta e envie a saída para um arquivo digitando o comando a seguir.

   ```cmd
   VSDiagnostics.exe stop <id> /output:<path to file>
   ```

1. Acesse a saída de arquivo do comando anterior e abra-a no Visual Studio para examinar as informações coletadas.

## <a name="agent-configuration-files"></a><a name="config_file"></a> Arquivos de configuração do Agente

Os Agentes de Coleta são componentes intercambiáveis que coletam diferentes tipos de dados, dependendo do que você está tentando medir.

Para sua conveniência, você pode armazenar essas informações em um arquivo de configuração do agente. O arquivo de configuração é um arquivo *.json* que contém, no mínimo, o nome da *.dll* e o CLSID COM. Estes são os arquivos de configuração de exemplo que podem ser encontrados na seguinte pasta:

```<Visual Studio installation folder>Team Tools\DiagnosticsHub\Collector\AgentConfigs\```

Consulte os links a seguir para baixar e exibir os arquivos de configuração do agente:

- https://aka.ms/vs/diaghub/agentconfig/cpubase
- https://aka.ms/vs/diaghub/agentconfig/cpuhigh
- https://aka.ms/vs/diaghub/agentconfig/cpulow
- https://aka.ms/vs/diaghub/agentconfig/database
- https://aka.ms/vs/diaghub/agentconfig/dotnetasyncbase
- https://aka.ms/vs/diaghub/agentconfig/dotnetallocbase
- https://aka.ms/vs/diaghub/agentconfig/dotnetalloclow

As configurações de os (base/alta/baixa) correspondem aos dados coletados para a ferramenta de criação de perfil de [uso da CPU](../profiling/cpu-usage.md) .
As configurações de DotNetObjectAlloc (base/baixa) correspondem aos dados coletados para a [ferramenta de alocação de objeto .net](../profiling/dotnet-alloc-tool.md).

As configurações Base/Baixa/Alta referem-se à taxa de amostragem. Por exemplo, Baixa representa 100 amostras/segundo e Alta, 4.000 amostras/segundo.

Para que a ferramenta *VSDiagnostics.exe* funcione com um agente de coleta, ela exige uma DLL e um CLSID COM para o agente apropriado e o agente pode ter outras opções de configuração também. Se você usar um agente sem um arquivo de configuração, use o formato no comando a seguir.

```cmd
VSDiagnostics.exe start <id> /attach:<pid> /loadAgent:<agentCLSID>;<agentName>[;<config>]
```

## <a name="permissions"></a>Permissões

Para analisar um aplicativo que exige permissões elevadas, faça isso em um prompt de comandos com privilégios elevados.
