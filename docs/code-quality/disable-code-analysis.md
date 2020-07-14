---
title: Desativar análise de código
ms.date: 10/03/2019
ms.topic: how-to
helpviewer_keywords:
- code analysis, disable
- disable code analysis
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 163b925423ba5afc62b84866e839c5d86a6444e0
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371931"
---
# <a name="how-to-disable-source-code-analysis-for-managed-code"></a>Como desabilitar a análise de código-fonte para código gerenciado

::: moniker range=">=vs-2019"

Esta página ajuda a desabilitar a análise de código no Visual Studio. Há limitações para o que você pode desabilitar e o procedimento para desativar a análise de código difere dependendo de alguns fatores:

- Tipo de projeto (.NET Core/Standard versus .NET Framework)

  Os projetos .NET Core e .NET Standard têm opções em suas páginas de propriedades de análise de código que permitem desativar a análise de código de analisadores instalados como um pacote NuGet. Para obter mais informações, consulte [.NET Core e projetos de .net Standard](#net-core-and-net-standard-projects). Para desativar a análise de código-fonte para projetos .NET Framework, consulte [.NET Framework projetos](#net-framework-projects).

- Análise de origem versus análise herdada

  Este tópico se aplica à análise de código-fonte e não à análise herdada (binário). Para obter informações sobre como desabilitar a análise herdada, consulte [como habilitar e desabilitar a análise de código herdado](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md).

## <a name="net-core-and-net-standard-projects"></a>Projetos do .NET Core e do .NET Standard

A partir do Visual Studio 2019 versão 16,3, há duas caixas de seleção disponíveis na página de propriedades de análise de código que permitem controlar se os analisadores são executados no momento da compilação e no momento do design. Essas opções são específicas do projeto.

![Habilitar ou desabilitar a análise de código ao vivo ou no Build no Visual Studio](media/run-on-build-run-live-analysis.png)

Para abrir essa página, clique com o botão direito do mouse no nó do projeto em **Gerenciador de soluções** e selecione **Propriedades**. Selecione a guia **análise de código** .

- Para desabilitar a análise de origem no momento da compilação, desmarque a opção **executar no Build** .
- Para desabilitar a análise de origem ao vivo, desmarque a opção **executar na análise dinâmica** .

> [!NOTE]
> A partir do Visual Studio 2019 versão 16,5, se você preferir o fluxo de trabalho de execução da análise de código sob demanda, você poderá desabilitar a execução do analisador durante a análise ao vivo e/ou compilar e disparar manualmente a análise de código uma vez em um projeto ou em uma solução sob demanda. Para obter informações sobre como executar a análise de código manualmente, consulte [como executar a análise de código manualmente para código gerenciado](how-to-run-code-analysis-manually-for-managed-code.md).  

## <a name="net-framework-projects"></a>Projetos de .NET Framework

Para desativar a análise de código-fonte para analisadores, adicione uma ou mais das seguintes propriedades do MSBuild ao [arquivo de projeto](../ide/solutions-and-projects-in-visual-studio.md#project-file).

| Propriedade do MSBuild | Descrição | Padrão |
| - | - | - |
| `RunAnalyzersDuringBuild` | Controla se os analisadores são executados no momento da compilação. | `true` |
| `RunAnalyzersDuringLiveAnalysis` | Controla se os analisadores analisam o código ao vivo em tempo de design. | `true` |
| `RunAnalyzers` | Desabilita os analisadores no momento da compilação e do design. Essa propriedade tem precedência sobre `RunAnalyzersDuringBuild` e `RunAnalyzersDuringLiveAnalysis` . | `true` |

Exemplos:

```xml
<RunAnalyzersDuringBuild>false</RunAnalyzersDuringBuild>
<RunAnalyzersDuringLiveAnalysis>false</RunAnalyzersDuringLiveAnalysis>
<RunAnalyzers>false</RunAnalyzers>
```

::: moniker-end

::: moniker range="vs-2017"

## <a name="source-analysis"></a>Análise de código-fonte

Não é possível desativar a [análise de origem](roslyn-analyzers-overview.md) no Visual Studio 2017. Se você quiser limpar erros do analisador do lista de erros, poderá suprimir todas as violações atuais escolhendo **analisar**  >  **executar análise de código e suprimir problemas ativos** na barra de menus. Para obter mais informações, consulte [suprimir violações](use-roslyn-analyzers.md#suppress-violations).

A partir do Visual Studio 2019 versão 16,3, você pode desativar a análise de código-fonte ou executá-la sob demanda. Considere atualizar para o Visual Studio 2019.

## <a name="legacy-analysis"></a>Análise herdada

Você pode desabilitar a análise herdada e em tempo de compilação na página de propriedades de **análise de código** . Para obter mais informações, consulte [como habilitar e desabilitar a análise de código herdado](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md).

::: moniker-end

## <a name="see-also"></a>Veja também

- [Suprimir violações](use-roslyn-analyzers.md#suppress-violations)
- [Como habilitar e desabilitar a análise de código herdado](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
