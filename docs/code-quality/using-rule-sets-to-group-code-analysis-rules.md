---
title: Conjunto de regras da análise de código
ms.date: 04/02/2018
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.rulesets.learnmore
helpviewer_keywords:
- code analysis, rule sets
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c95b442835289265d197b6806c6d87fa051f2c1b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62825078"
---
# <a name="use-rule-sets-to-group-code-analysis-rules"></a>Usar conjuntos de regras para agrupar regras de análise de código

Quando você configura a análise de código no Visual Studio, você pode escolher entre uma lista dos internas *conjuntos de regra*. Um conjunto de regras é um agrupamento de regras de análise de código que identificam problemas direcionados e condições específicas para o projeto. Por exemplo, você pode aplicar um conjunto de regras que foi projetada para digitalizar o código para as APIs disponíveis publicamente. Você também pode aplicar um conjunto de regras que inclui todas as regras disponíveis.

Você pode personalizar uma regra definida, adicionando ou excluindo regras ou alterando severidades de regra sejam exibidos como avisos ou erros na **Error List**. Conjuntos de regras personalizado podem atender uma necessidade para seu ambiente de desenvolvimento específico. Quando você personaliza um conjunto de regras, o editor de conjunto de regras fornece pesquisa e ferramentas para ajudá-lo no processo de filtragem.

Conjuntos de regras estão disponíveis para [análise estática de código gerenciado](how-to-configure-code-analysis-for-a-managed-code-project.md), [análise de código C++](using-rule-sets-to-specify-the-cpp-rules-to-run.md), e [analisadores de Roslyn](analyzer-rule-sets.md).

## <a name="rule-set-format"></a>Formato do conjunto de regras

Um conjunto de regras é especificado no formato XML em um *RuleSet* arquivo. Regras, que consistem em uma ID e um *ação*, são agrupados por ID de analisador e o namespace no arquivo.

O conteúdo de um *RuleSet* arquivo é semelhante a este XML:

```xml
<RuleSet Name="Rules for Hello World project" Description="These rules focus on critical issues for the Hello World app." ToolsVersion="10.0">
  <Localization ResourceAssembly="Microsoft.VisualStudio.CodeAnalysis.RuleSets.Strings.dll" ResourceBaseName="Microsoft.VisualStudio.CodeAnalysis.RuleSets.Strings.Localized">
    <Name Resource="HelloWorldRules_Name" />
    <Description Resource="HelloWorldRules_Description" />
  </Localization>
  <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
    <Rule Id="CA1001" Action="Warning" />
    <Rule Id="CA1009" Action="Warning" />
    <Rule Id="CA1016" Action="Warning" />
    <Rule Id="CA1033" Action="Warning" />
  </Rules>
  <Rules AnalyzerId="Microsoft.CodeQuality.Analyzers" RuleNamespace="Microsoft.CodeQuality.Analyzers">
    <Rule Id="CA1802" Action="Error" />
    <Rule Id="CA1814" Action="Info" />
    <Rule Id="CA1823" Action="None" />
    <Rule Id="CA2217" Action="Warning" />
  </Rules>
</RuleSet>
```

> [!TIP]
> É mais fácil [editar um conjunto de regras](../code-quality/working-in-the-code-analysis-rule-set-editor.md) no gráfico **Rule Set Editor** que manualmente.

## <a name="specify-a-rule-set-for-a-project"></a>Especifique uma regra definida para um projeto

A regra definida para um projeto é especificado o **CodeAnalysisRuleSet** propriedade no arquivo de projeto do Visual Studio. Por exemplo:

```xml
<PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
  ...
  <CodeAnalysisRuleSet>HelloWorld.ruleset</CodeAnalysisRuleSet>
</PropertyGroup>
```

## <a name="see-also"></a>Consulte também

- [Referência do conjunto de regras de análise de código](../code-quality/rule-set-reference.md)