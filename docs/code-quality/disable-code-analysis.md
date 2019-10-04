---
title: Desativar análise de código
ms.date: 10/03/2019
ms.topic: conceptual
helpviewer_keywords:
- code analysis, disable
- disable code analysis
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d769accce87b789b207d9cf337d5b9adc46e413e
ms.sourcegitcommit: dc12a7cb66124596089f01d3e939027ae562ede9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71963322"
---
# <a name="how-to-disable-code-analysis-in-visual-studio"></a>Como desabilitar a análise de código no Visual Studio

::: moniker range=">=vs-2019"

Esta página ajuda a desabilitar a análise de código no Visual Studio. Há limitações para o que você pode desabilitar e o procedimento para desativar a análise de código difere dependendo de alguns fatores:

- Tipo de projeto (.NET Core/Standard versus .NET Framework)

  Os projetos .NET Core e .NET Standard têm opções em suas páginas de propriedades de análise de código que permitem desativar a análise de código de analisadores instalados como um pacote NuGet. Para obter mais informações, consulte [.NET Core e projetos de .net Standard](#net-core-and-net-standard-projects). Para desativar a análise de código-fonte para projetos .NET Framework, consulte [.NET Framework projetos](#net-framework-projects).

- Pacote do NuGet Analyzer versus VSIX ou analisadores internos

  No momento, não é possível desabilitar a análise de código ao vivo para os analisadores internos, por exemplo, ID de regra IDE0067. Da mesma forma, você não pode desabilitar a análise de código ao vivo para analisadores que foram instalados como parte de uma extensão do Visual Studio (VSIX). Para suprimir erros e avisos de analisadores internos e baseados em VSIX, escolha **analisar** > **Compilar e suprimir problemas ativos** na barra de menus. Você *pode* desabilitar a análise dinâmica e em tempo real para analisadores instalados como parte de um pacote NuGet.

- Análise de origem versus análise herdada

  Este tópico se aplica à análise de código-fonte e não à análise herdada (binário). Para obter informações sobre como desabilitar a análise herdada, consulte [How para: Habilitar e desabilitar a análise de código herdado @ no__t-0.

## <a name="net-core-and-net-standard-projects"></a>Projetos do .NET Core e do .NET Standard

A partir do Visual Studio 2019 versão 16,3, há duas caixas de seleção disponíveis na página de propriedades de análise de código que permitem controlar se os analisadores baseados em NuGet são executados no momento da compilação e no momento do design. Essas opções são específicas do projeto.

![Habilitar ou desabilitar a análise de código ao vivo ou no Build no Visual Studio](media/run-on-build-run-live-analysis.png)

Para abrir essa página, clique com o botão direito do mouse no nó do projeto em **Gerenciador de soluções** e selecione **Propriedades**. Selecione a guia **análise de código** .

- Para desabilitar a análise de origem no momento da compilação, desmarque a opção **executar no Build** .
- Para desabilitar a análise de origem ao vivo, desmarque a opção **executar na análise dinâmica** .

> [!NOTE]
> Os analisadores internos e baseados em VSIX continuarão a fornecer análise dinâmica do seu código, mesmo que a **execução na análise ao vivo** esteja desmarcada. Se você quiser suprimir erros e avisos desses analisadores, escolha **analisar** > **Compilar e suprimir problemas ativos** na barra de menus.

## <a name="net-framework-projects"></a>Projetos de .NET Framework

Para desativar a análise de código-fonte para analisadores instalados como parte de um pacote NuGet, adicione uma ou mais das seguintes propriedades do MSBuild ao [arquivo de projeto](../ide/solutions-and-projects-in-visual-studio.md#project-file).

| Propriedade do MSBuild | Descrição | Padrão |
| - | - | - |
| `RunAnalyzersDuringBuild` | Controla se os analisadores baseados em NuGet são executados no momento da compilação. | `true` |
| `RunAnalyzersDuringLiveAnalysis` | Controla se os analisadores baseados em NuGet analisam o código ao vivo em tempo de design. | `true` |
| `RunAnalyzers` | Desabilita os analisadores baseados em NuGet no momento da compilação e do design. Essa propriedade tem precedência sobre `RunAnalyzersDuringBuild` e `RunAnalyzersDuringLiveAnalysis`. | `true` |

Exemplos:

```xml
<RunAnalyzersDuringBuild>false</RunAnalyzersDuringBuild>
<RunAnalyzersDuringLiveAnalysis>false</RunAnalyzersDuringLiveAnalysis>
<RunAnalyzers>false</RunAnalyzers>
```

::: moniker-end

::: moniker range="vs-2017"

## <a name="source-analysis"></a>Análise de código-fonte

Não é possível desativar a [análise de origem](roslyn-analyzers-overview.md) no Visual Studio 2017. Se você quiser limpar erros do analisador do Lista de Erros, poderá suprimir todas as violações atuais escolhendo **analisar** > **executar análise de código e suprimir problemas ativos** na barra de menus. Para obter mais informações, consulte [suprimir violações](use-roslyn-analyzers.md#suppress-violations).

A partir do Visual Studio 2019 versão 16,3, você pode desativar a análise de código-fonte baseada em NuGet. Considere atualizar para o Visual Studio 2019.

## <a name="legacy-analysis"></a>Análise herdada

Você pode desabilitar a análise herdada e em tempo de compilação na página de propriedades de **análise de código** . Para obter mais informações, confira [Como: Habilitar e desabilitar a análise de código herdado @ no__t-0.

::: moniker-end

## <a name="see-also"></a>Consulte também

- [Suprimir violações](use-roslyn-analyzers.md#suppress-violations)
- [Como: Habilitar e desabilitar a análise de código herdado @ no__t-0
