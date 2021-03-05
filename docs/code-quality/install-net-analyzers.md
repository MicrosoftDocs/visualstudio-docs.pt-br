---
title: Habilitar ou instalar analisadores de .NET de primeira empresa
ms.date: 08/03/2018
description: Saiba como habilitar os analisadores de .NET de primeira empresa no SDK do .NET ou instalar esses analisadores como um pacote NuGet.
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- .NET analyzers
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 368fd5bc9c8b7e2659c86b6e3dc69a609da37617
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102144657"
---
# <a name="enable-or-install-first-party-net-analyzers"></a>Habilitar ou instalar analisadores de .NET de primeira empresa

## <a name="overview"></a>Visão geral

Os analisadores do .NET Compiler Platform (Roslyn) inspecionam código em C# ou no Visual Basic em busca de problemas de estilo e de qualidade. Os analisadores de .NET primários são **independentes de plataforma de destino**. Ou seja, seu projeto não precisa ter como destino uma plataforma .NET específica. Os analisadores funcionam para projetos direcionados `net5.0` , bem como para versões anteriores do .net, como `netcoreapp` , `netstandard` e `net472` .

Você pode habilitar ou instalar os analisadores de .NET primários de uma das seguintes maneiras:

- **Habilitar do SDK do .net**: a partir do Visual Studio 2019 16,8 e do .NET 5,0, esses analisadores estão [incluídos no SDK do .net](/dotnet/fundamentals/code-analysis/overview). A análise é habilitada, por padrão, para projetos direcionados ao .NET 5,0 ou posterior. Você pode habilitar a análise de código em projetos direcionados a versões anteriores do .NET definindo a propriedade MSBUILD [EnableNETAnalyzers](/dotnet/core/project-sdk/msbuild-props#enablenetanalyzers) como `true` . Você também pode desabilitar a análise de código para seu projeto definindo `EnableNETAnalyzers` como `false` .

- **Instalar como um pacote NuGet**: se você não quiser migrar para o SDK do .NET 5 + ou se preferir um modelo baseado em pacote NuGet, os analisadores também estarão disponíveis no `Microsoft.CodeAnalysis.NetAnalyzers` [pacote NuGet](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers) no Visual Studio 2019.  Você pode preferir um modelo baseado em pacote para atualizações de versão sob demanda. Se você estiver no Visual Studio 2017, instale a versão mais recente `2.9.x` do `Microsoft.CodeAnalysis.FxCopAnalyzers` [pacote NuGet](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/) .

> [!NOTE]
> É recomendável que você habilite os analisadores do SDK do .NET em vez de instalar o `Microsoft.CodeAnalysis.NetAnalyzers` [pacote NuGet](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers), quando possível. Habilitar os analisadores do SDK do .NET garante que você obtenha automaticamente as correções de bugs do analisador e novos analisadores assim que atualizar o SDK. No modelo NuGet, você precisa atualizar o pacote NuGet cada vez que desejar as correções de bug mais recentes. O pacote NuGet é atualizado com mais frequência.

## <a name="see-also"></a>Confira também

- [Visão geral dos analisadores de código no Visual Studio](roslyn-analyzers-overview.md)
- [Usar analisadores de código no Visual Studio](use-roslyn-analyzers.md)
- [Migrar da análise herdada para analisadores de .NET](migrate-from-legacy-analysis-to-net-analyzers.md)
- [Migrar de analisadores do FxCop para analisadores de .NET](migrate-from-fxcop-analyzers-to-net-analyzers.md)
