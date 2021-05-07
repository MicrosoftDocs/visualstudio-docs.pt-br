---
title: Migrar do FxCop para a análise de origem (analisadores .NET)
ms.custom: SEO-VS-2020
description: Saiba como analisar o código pela primeira vez ou como migrar do FxCop (análise binária) para a nova maneira de analisar o código gerenciado usando a análise de origem (analisadores .NET).
ms.date: 03/06/2020
ms.topic: conceptual
f1_keywords:
- vs.projectpropertypages.codeanalysis
helpviewer_keywords:
- FxCop, migration
- legacy analysis, migration
- source code analysis, migration
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.openlocfilehash: 9a673e7467816e71b8240de9e5f68840c9188dcd
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798226"
---
# <a name="migrate-from-legacy-analysis-fxcop-to-source-analysis-net-analyzers"></a>Migrar da análise herdada (FxCop) para a análise de origem (analisadores .NET)

Análise de origem por .NET Compiler Platform ("Roslyn") analisadores substitui a [análise herdada](../code-quality/code-analysis-for-managed-code-overview.md) para código gerenciado. Para modelos de projeto mais recentes, como projetos .NET Core e .NET Standard, a análise herdada não está disponível.

Muitas das regras de análise herdada (FxCop) já foram reescritas para analisadores .NET, um conjunto de analisadores de código Roslyn. Os analisadores Roslyn executam a análise baseada em código-fonte durante a execução do compilador. Os resultados do analisador são relatados junto com os resultados do compilador.

Para obter mais informações sobre as diferenças entre análise herdada e análise de origem, consulte o seguinte:

- [Análise de código-fonte versus análise herdada](../code-quality/net-analyzers-faq.yml#what-s-the-difference-between-legacy-fxcop-and--net-analyzers-)

- [Perguntas frequentes sobre os analisadores do .NET](../code-quality/net-analyzers-faq.yml)

## <a name="migration"></a>Migração

Para migrar para a análise de origem, [habilite ou instale os analisadores .net](install-net-analyzers.md). Como violações de regras de análise herdadas, as violações de análise de código-fonte aparecem na janela Lista de Erros no Visual Studio. Além disso, as violações de análise de código-fonte também aparecem no editor de códigos como *ondulado* no código incorreto. A cor da linha ondulada depende da [configuração de gravidade](../code-quality/use-roslyn-analyzers.md#configure-severity-levels) da regra. Para ver o status das regras portadas para os novos analisadores .NET, consulte [regras portadas e não portadas](../code-quality/fxcop-rule-port-status.md).

> [!NOTE]
> Antes do Visual Studio 2019 16,8 e do .NET 5,0, esses analisadores foram fornecidos como `Microsoft.CodeAnalysis.FxCopAnalyzers` [pacote NuGet](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers). A partir do Visual Studio 2019 16,8 e do .NET 5,0, esses analisadores estão [incluídos no SDK do .net](/dotnet/fundamentals/code-analysis/overview). Eles também estão disponíveis como `Microsoft.CodeAnalysis.NetAnalyzers` [pacote NuGet](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers). Para obter mais informações, consulte [migrar de analisadores do FxCop para analisadores do .net](migrate-from-fxcop-analyzers-to-net-analyzers.md).

## <a name="configuration"></a>Configuração

Para saber mais sobre como configurar os analisadores do .NET:

- Para configurar os analisadores do .NET, consulte [Configurar analisadores .net](/dotnet/fundamentals/code-analysis/code-quality-rule-options).

- Para saber mais sobre como configurar analisadores usando regras predefinida com EditorConfig ou um arquivo de conjunto de regras, consulte [Habilitar uma categoria de regras](/dotnet/fundamentals/code-analysis/code-quality-rule-options).

## <a name="see-also"></a>Consulte também

- [Migrar de analisadores do FxCop para analisadores de .NET](migrate-from-fxcop-analyzers-to-net-analyzers.md)
