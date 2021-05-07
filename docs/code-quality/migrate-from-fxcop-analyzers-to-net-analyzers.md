---
title: Migrar de analisadores do FxCop para analisadores de .NET
ms.custom: SEO-VS-2020
description: Saiba como migrar de analisadores do FxCop para analisadores do .NET
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
ms.openlocfilehash: d6f9c36b1b64abe648c3aa9014c633e4e4949b1a
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798252"
---
# <a name="migrate-from-fxcop-analyzers-to-net-analyzers"></a>Migrar de analisadores do FxCop para analisadores de .NET

Análise de origem por .NET Compiler Platform ("Roslyn") analisadores substitui a [análise herdada](code-analysis-for-managed-code-overview.md) para código gerenciado. Muitas das regras de análise herdada (FxCop) já foram reescritas como analisadores de origem.

Antes do Visual Studio 2019 16,8 e do .NET 5,0, esses analisadores foram fornecidos como `Microsoft.CodeAnalysis.FxCopAnalyzers` [pacote NuGet](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers).

A partir do Visual Studio 2019 16,8 e do .NET 5,0, esses analisadores estão [incluídos no SDK do .net](/dotnet/fundamentals/code-analysis/overview). Se você não quiser migrar para o SDK do .NET 5 + ou se preferir um modelo baseado em pacote NuGet, os analisadores também estarão disponíveis no `Microsoft.CodeAnalysis.NetAnalyzers` [pacote NuGet](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers). Você pode preferir um modelo baseado em pacote para atualizações de versão sob demanda.

> [!NOTE]
> Os analisadores de .NET primários são independentes de plataforma de destino. Ou seja, seu projeto não precisa ter como destino uma plataforma .NET específica. Os analisadores funcionam para projetos direcionados `net5.0` , bem como para versões anteriores do .net, como `netcoreapp` , `netstandard` e `net472` .

## <a name="migration-steps"></a>Etapas da migração

A partir da versão `3.3.2` , o `Microsoft.CodeAnalysis.FxCopAnalyzers` pacote NuGet foi preterido. Siga as etapas abaixo para migrar seu projeto ou solução do `Microsoft.CodeAnalysis.FxCopAnalyzers` para os analisadores do .net:

1. Desinstalar o `Microsoft.CodeAnalysis.FxCopAnalyzers` pacote NuGet

2. [Habilite ou instale os analisadores do .net](install-net-analyzers.md). Observe que você não precisa alterar a plataforma de destino do projeto.

3. Habilitar regras adicionais: `Microsoft.CodeAnalysis.NetAnalyzers` é muito mais conservador em comparação com `Microsoft.CodeAnalysis.FxCopAnalyzers` . Ao contrário do pacote FxCopAnalyzers, ele tem apenas algumas regras de correção que são [habilitadas por padrão como avisos de compilação](/dotnet/fundamentals/code-analysis/overview#enabled-rules). Você pode [habilitar regras adicionais](/dotnet/fundamentals/code-analysis/overview#enable-additional-rules) Personalizando a propriedade do MSBuild do [analysismode](/dotnet/core/project-sdk/msbuild-props#analysismode) . Por exemplo, definir a propriedade como `AllEnabledByDefault` habilitará todas as regras de autoridade de certificação aplicáveis como avisos de compilação por padrão.

   ```xml
   <PropertyGroup>
     <AnalysisMode>AllEnabledByDefault</AnalysisMode>
   </PropertyGroup>
   ```

## <a name="see-also"></a>Consulte também

- [Análise de código-fonte versus análise herdada](net-analyzers-faq.yml#what-s-the-difference-between-legacy-fxcop-and--net-analyzers-)
- [Migrar da análise herdada para analisadores de .NET](migrate-from-legacy-analysis-to-net-analyzers.md)
- [Habilitar ou instalar analisadores do .NET](install-net-analyzers.md)
- [Perguntas frequentes sobre analisadores .NET](net-analyzers-faq.yml)
- [Configurar analisadores .NET](/dotnet/fundamentals/code-analysis/code-quality-rule-options)
