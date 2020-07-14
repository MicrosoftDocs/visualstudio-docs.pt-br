---
title: API do MSBuild | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f9d3cdaf2bcc7d7c62f7224c3a8c439d03282ef0
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371918"
---
# <a name="use-the-msbuild-api"></a>Usar a API do MSBuild

O MSBuild fornece uma superfície de API pública para que seu programa possa executar builds e inspecionar projetos. Versões recentes das APIs do MSBuild podem ser encontradas nos seguintes pacotes NuGet:

| Nome do pacote | Description |
| ------------ | ----------- |
| [Microsoft. Build](https://www.nuget.org/packages/Microsoft.Build) | Contém o assembly Microsoft. Build, que é usado para criar, editar e avaliar projetos do MSBuild.|
| [Microsoft.Build.Framework](https://www.nuget.org/packages/Microsoft.Build.Framework)| Contém o assembly de estrutura MSBuild comum usado por outros assemblies do MSBuild. |
| [Microsoft. Build. Runtime](https://www.nuget.org/packages/Microsoft.Build.Runtime) | Fornece uma cópia executável completa do MSBuild. Referencie esse pacote somente se seu aplicativo precisar carregar projetos ou executar compilações em processo sem exigir a instalação do MSBuild. A avaliação bem-sucedida de projetos usando este pacote requer a agregação de componentes adicionais (como os compiladores) em um diretório de aplicativos. |
| [Microsoft. Build. Tasks. Core](https://www.nuget.org/packages/Microsoft.Build.Tasks.Core) | Contém o assembly Microsoft. Build. Tasks que implementa as tarefas comumente usadas do MSBuild. |
| [Microsoft. Build. Utilities. Core](https://www.nuget.org/packages/Microsoft.Build.Utilities.Core) | Contém o assembly Microsoft. Build. Utilities, que é usado para implementar tarefas personalizadas do MSBuild. |

Além disso, o NuGet também hospeda um assembly herdado, [Microsoft. Build. Engine](https://www.nuget.org/packages/Microsoft.Build.Engine), que é preterido.

Há várias versões diferentes da API do MSBuild e, para as versões 15 e 16, há duas formas distintas dos assemblies nos pacotes NuGet, uma compilada com a .NET Framework e outra compilada com o .NET Core, que é um subconjunto da superfície da API .NET Framework.  A versão do .NET Core do MSBuild é usada quando você invoca o `dotnet` comando e ao usar o MSBuild em sistemas Mac e Linux.

A documentação da API do MSBuild pode ser encontrada usando o [navegador de API do .net](/dotnet/api)ou procurando os namespaces na lista a seguir.

::: moniker range="vs-2017"
| Namespace | Aplica-se A | Description |
|-----------| -----------| ----------- |
| [Microsoft. Build. Construction](/dotnet/api/Microsoft.Build.Construction?view=msbuild-15) | Tudo |  Contém tipos que o modelo de objeto do MSBuild usa para construir raízes de projeto com valores não avaliados. Cada raiz de projeto corresponde a um arquivo de projeto ou de destino. |
| [Microsoft. Build. Definition](/dotnet/api/Microsoft.Build.Definition?view=msbuild-15) | Tudo | Contém a `ProjectOptions` classe, que dá suporte à construção do projeto. |
| [Microsoft.Build.Evaluation](/dotnet/api/Microsoft.Build.Evaluation?view=msbuild-15) | Tudo | Contém tipos que o modelo de objeto do MSBuild usa para avaliar projetos. Cada projeto é associado a uma ou mais raízes de projeto. |
| [Microsoft. Build. Evaluation. Context](/dotnet/api/Microsoft.Build.Evaluation.Context?view=msbuild-15) | Tudo | Contém a `EvaluationContext` classe, usada para armazenar o estado de avaliação entre chamadas. |
| [Microsoft. Build. Exceptions](/dotnet/api/Microsoft.Build.Exceptions?view=msbuild-15) | Tudo | Contém tipos de exceção que podem ser gerados durante o processo de build. |
| [Microsoft.Build.Execution](/dotnet/api/Microsoft.Build.Execution?view=msbuild-15) | Tudo | Contém tipos que o modelo de objeto do MSBuild usa para criar projetos. |
| [Microsoft.Build.Framework](/dotnet/api/Microsoft.Build.Framework?view=msbuild-15) | Tudo | Contém os tipos que definem como as tarefas e os agentes interagem com o mecanismo do MSBuild.|
| [Microsoft. Build. Framework. Profiler](/dotnet/api/Microsoft.Build.Framework.Profiler?view=msbuild-15) | Tudo | Contém os tipos que dão suporte à criação de perfil de desempenho. |
| [Microsoft. Build. Framework. XamlTypes](/dotnet/api/Microsoft.Build.Framework.XamlTypes?view=msbuild-15) | Somente .NET Framework | Contém classes usadas para representar tipos XAML analisados de arquivos, regras e outras fontes. |
| [Microsoft. Build. mascaramento](/dotnet/api/Microsoft.Build.Globbing?view=msbuild-15) | Tudo | Contém classes que dão suporte ao processamento de curinga. |
| [Microsoft. Build. Mascaration. Extensions](/dotnet/api/Microsoft.Build.Globbing.Extensions?view=msbuild-15) | Tudo | Contém tipos que dão suporte a extensões para processamento de curinga. |
| [Microsoft. Build. Graph](/dotnet/api/Microsoft.Build.Graph?view=msbuild-15) | Tudo | Contém tipos que dão suporte à `-graph` opção MSBuild. |
| [Microsoft.Build.Logging](/dotnet/api/Microsoft.Build.Logging?view=msbuild-15) | Tudo | Contém tipos usados para registrar em log o progresso de um build. |
| [Microsoft. Build. ObjectModelRemoting](/dotnet/api/Microsoft.Build.ObjectModelRemoting?view=msbuild-15) | Tudo | Contém tipos que oferecem suporte a comunicação remota no MSBuild. |
| [Microsoft.Build.Tasks](/dotnet/api/Microsoft.Build.Tasks?view=msbuild-15) | Tudo | Contém a implementação de todas as tarefas fornecidas com o MSBuild. |
| [Microsoft. Build. Tasks. Deployment. Bootstrapper](/dotnet/api/Microsoft.Build.Tasks.Deployment.Bootstrapper?view=msbuild-15) | Somente .NET Framework | Contém classes usadas internamente pelo MSBuild. |
| [Microsoft.Build.Tasks.Deployment.ManifestUtilities](/dotnet/api/Microsoft.Build.Tasks.Deployment.ManifestUtilities?view=msbuild-15) | Somente .NET Framework | Contém classes que o MSBuild usa.|
| [Microsoft. Build. Tasks. Hosting](/dotnet/api/Microsoft.Build.Tasks.Hosting?view=msbuild-15) | Tudo | Contém classes usadas internamente pelo MSBuild. |
| [Microsoft. Build. Tasks. XAML](/dotnet/api/Microsoft.Build.Tasks.Xaml?view=msbuild-15) | Somente .NET Framework | Contém classes relacionadas a tarefas de compilação XAML. |
| [Microsoft.Build.Utilities](/dotnet/api/Microsoft.Build.Utilities?view=msbuild-15) | Tudo | Contém classes auxiliares que você pode usar para criar seus próprios agentes e tarefas do MSBuild.|
:::moniker-end
:::moniker range=">=vs-2019"
| Namespace | Aplica-se A | Description |
|-----------| -----------| ----------- |
| [Microsoft. Build. Construction](/dotnet/api/Microsoft.Build.Construction?view=msbuild-16) | Tudo |  Contém tipos que o modelo de objeto do MSBuild usa para construir raízes de projeto com valores não avaliados. Cada raiz de projeto corresponde a um arquivo de projeto ou de destino. |
| [Microsoft. Build. Definition](/dotnet/api/Microsoft.Build.Definition?view=msbuild-16) | Tudo | Contém a `ProjectOptions` classe, que dá suporte à construção do projeto. |
| [Microsoft.Build.Evaluation](/dotnet/api/Microsoft.Build.Evaluation?view=msbuild-16) | Tudo | Contém tipos que o modelo de objeto do MSBuild usa para avaliar projetos. Cada projeto é associado a uma ou mais raízes de projeto. |
| [Microsoft. Build. Evaluation. Context](/dotnet/api/Microsoft.Build.Evaluation.Context?view=msbuild-16) | Tudo | Contém a `EvaluationContext` classe, usada para armazenar o estado de avaliação entre chamadas. |
| [Microsoft. Build. Exceptions](/dotnet/api/Microsoft.Build.Exceptions?view=msbuild-16) | Tudo | Contém tipos de exceção que podem ser gerados durante o processo de build. |
| [Microsoft.Build.Execution](/dotnet/api/Microsoft.Build.Execution?view=msbuild-16) | Tudo | Contém tipos que o modelo de objeto do MSBuild usa para criar projetos. |
| [Microsoft.Build.Framework](/dotnet/api/Microsoft.Build.Framework?view=msbuild-16) | Tudo | Contém os tipos que definem como as tarefas e os agentes interagem com o mecanismo do MSBuild.|
| [Microsoft. Build. Framework. Profiler](/dotnet/api/Microsoft.Build.Framework.Profiler?view=msbuild-16) | Tudo | Contém os tipos que dão suporte à criação de perfil de desempenho. |
| [Microsoft. Build. Framework. XamlTypes](/dotnet/api/Microsoft.Build.Framework.XamlTypes?view=msbuild-16) | Somente .NET Framework | Contém classes usadas para representar tipos XAML analisados de arquivos, regras e outras fontes. |
| [Microsoft. Build. mascaramento](/dotnet/api/Microsoft.Build.Globbing?view=msbuild-16) | Tudo | Contém classes que dão suporte ao processamento de curinga. |
| [Microsoft. Build. Mascaration. Extensions](/dotnet/api/Microsoft.Build.Globbing.Extensions?view=msbuild-16) | Tudo | Contém tipos que dão suporte a extensões para processamento de curinga. |
| [Microsoft. Build. Graph](/dotnet/api/Microsoft.Build.Graph?view=msbuild-16) | Tudo | Contém tipos que dão suporte à `-graph` opção MSBuild. |
| [Microsoft.Build.Logging](/dotnet/api/Microsoft.Build.Logging?view=msbuild-16) | Tudo | Contém tipos usados para registrar em log o progresso de um build. |
| [Microsoft. Build. ObjectModelRemoting](/dotnet/api/Microsoft.Build.ObjectModelRemoting?view=msbuild-16) | Tudo | Contém tipos que oferecem suporte a comunicação remota no MSBuild. |
| [Microsoft.Build.Tasks](/dotnet/api/Microsoft.Build.Tasks?view=msbuild-16) | Tudo | Contém a implementação de todas as tarefas fornecidas com o MSBuild. |
| [Microsoft. Build. Tasks. Deployment. Bootstrapper](/dotnet/api/Microsoft.Build.Tasks.Deployment.Bootstrapper?view=msbuild-16) | Somente .NET Framework | Contém classes usadas internamente pelo MSBuild. |
| [Microsoft.Build.Tasks.Deployment.ManifestUtilities](/dotnet/api/Microsoft.Build.Tasks.Deployment.ManifestUtilities?view=msbuild-16) | Somente .NET Framework | Contém classes que o MSBuild usa.|
| [Microsoft. Build. Tasks. Hosting](/dotnet/api/Microsoft.Build.Tasks.Hosting?view=msbuild-16) | Tudo | Contém classes usadas internamente pelo MSBuild. |
| [Microsoft. Build. Tasks. XAML](/dotnet/api/Microsoft.Build.Tasks.Xaml?view=msbuild-16) | Somente .NET Framework | Contém classes relacionadas a tarefas de compilação XAML. |
| [Microsoft.Build.Utilities](/dotnet/api/Microsoft.Build.Utilities?view=msbuild-16) | Tudo | Contém classes auxiliares que você pode usar para criar seus próprios agentes e tarefas do MSBuild.|
:::moniker-end

Na tabela anterior, All na coluna aplica-se a significa que os tipos no namespace estão disponíveis nas versões do .NET Framework e do .NET Core da API do MSBuild.
