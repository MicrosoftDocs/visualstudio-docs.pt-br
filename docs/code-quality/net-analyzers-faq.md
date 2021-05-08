---
title: Análise de código FxCop (análise binária) e analisadores .NET (análise de origem)
ms.date: 09/06/2018
description: Entenda a diferença entre fxCop herdado (análise binária) e analisadores .NET (análise de origem) em Visual Studio. Consulte respostas para perguntas sobre como usar esses analisadores.
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis FAQ
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 951e9b951f1d90077fe29506e9c288fb19f2d5ff
ms.sourcegitcommit: dd2fc6e03a789c044f8438096b8f112e4dba5557
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2021
ms.locfileid: "108800467"
---
# <a name="frequently-asked-questions-about-legacy-fxcop-and-net-analyzers"></a>Perguntas frequentes sobre analisadores FxCop e .NET herdados

Pode ser um pouco confuso entender as diferenças entre fxCop herdado (análise binária) e analisadores .NET (análise de origem). O objetivo deste artigo é abordar algumas perguntas que você possa ter.

## <a name="whats-the-difference-between-legacy-fxcop-and-net-analyzers"></a>Qual é a diferença entre o FxCop herdado e os analisadores do .NET?

O FxCop herdado executa análise de pós-build em um assembly compilado. Ele é executado como um executável separado chamado **FxCopCmd.exe**. O FxCopCmd.exe carrega o assembly compilado, executa a análise de código e, em seguida, relata os resultados (ou *diagnóstico*).

Os analisadores do .NET são baseados no .NET Compiler Platform ("Roslyn"). [Habilita-os no SDK](install-net-analyzers.md) do .NET ou instala-os como um pacote NuGet referenciado pelo projeto ou pela solução. Os analisadores executarão a análise baseada em código-fonte durante a execução do compilador. Os analisadores são hospedados no  processo do compilador,csc.exeou **vbc.exe** e são executados quando o projeto é compilado. Os resultados do analisador são relatados junto com os resultados do compilador.

## <a name="whats-the-difference-between-fxcop-analyzers-and-net-analyzers"></a>Qual é a diferença entre analisadores FxCop e analisadores do .NET?

Os analisadores FxCop e os analisadores do .NET referem-se às implementações do analisador .NET Compiler Platform ("Roslyn") das regras de AC do FxCop. Antes Visual Studio 2019 16.8 e .NET 5.0, esses analisadores eram fornecidos como o `Microsoft.CodeAnalysis.FxCopAnalyzers` [pacote NuGet.](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers) A partir do Visual Studio 2019 16.8 e .NET 5.0, esses analisadores são incluídos no [SDK do .NET.](/dotnet/fundamentals/code-analysis/overview) Eles também estão disponíveis como pacote `Microsoft.CodeAnalysis.NetAnalyzers` [NuGet.](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers) Considere a [migração de analisadores FxCop para analisadores do .NET.](migrate-from-fxcop-analyzers-to-net-analyzers.md)

## <a name="does-the-run-code-analysis-command-run-net-analyzers"></a>O comando Executar Code Analysis executar analisadores do .NET?

Antes da Visual Studio 2019 16.5, quando você seleciona Analisar Executar Code Analysis , ele executa  >  a análise herdada. A partir Visual Studio 2019 16.5, **a** opção de menu Executar Code Analysis executa analisadores baseados em Roslyn para o projeto ou solução selecionado. Se você tiver instalado analisadores do .NET, eles também serão executados. Para obter mais informações, consulte [como executar a análise de código manualmente para código gerenciado](how-to-run-code-analysis-manually-for-managed-code.md).

## <a name="does-the-runcodeanalysis-msbuild-project-property-run-analyzers"></a>A propriedade do projeto msbuild RunCodeAnalysis executa analisadores?

Não. A propriedade **RunCodeAnalysis** em um arquivo de projeto (por exemplo, *.csproj*) só é usada para executar o FxCop herdado. Ele executa uma tarefa msbuild pós-build que invoca **FxCopCmd.exe**.

## <a name="so-how-do-i-run-net-analyzers-then"></a>Então, como executar os analisadores do .NET?

Para executar os analisadores do .NET, primeiro [habilite-os no SDK do .net ou instale-os como um pacote NuGet](install-net-analyzers.md). Em seguida, crie seu projeto ou solução com base no Visual Studio ou usando msbuild. Os avisos e erros que os analisadores de Roslyn geram aparecerão no **lista de erros** ou na janela de comando.

## <a name="i-get-warning-ca0507-even-after-ive-installed-the-net-analyzers-nuget-package"></a>Eu obtenho o aviso CA0507 mesmo depois de instalar o pacote NuGet dos analisadores .NET

Se você instalou os analisadores do .NET, mas continuar a obter o aviso CA0507 **"" executar análise de código "foi preterido em favor dos analisadores do FxCop, que são executados durante a compilação"**, talvez seja necessário definir a Propriedade MSBuild do **RunCodeAnalysis** no [arquivo de projeto](../ide/solutions-and-projects-in-visual-studio.md#project-file) como **false**. Caso contrário, a análise herdada será executada após cada compilação.

```xml
<RunCodeAnalysis>false</RunCodeAnalysis>
```

## <a name="which-rules-have-been-ported-to-net-analyzers"></a>Quais regras foram transportadas para os analisadores .NET?

Para obter informações sobre quais regras de análise herdadas foram modeladas para os analisadores do .NET, consulte [status da porta da regra do FxCop](fxcop-rule-port-status.md).

## <a name="code-analysis-warnings-are-treated-as-errors"></a>Os avisos de análise de código são tratados como erros

Se seu projeto usar a opção de compilação para tratar avisos como erros, os avisos do analisador poderão aparecer como erros. Para impedir que avisos de análise de código sejam tratados como erros, siga as etapas em [perguntas frequentes sobre análise de código](../code-quality/analyzers-faq.md#treat-warnings-as-errors).

## <a name="see-also"></a>Confira também

- [Visão geral dos analisadores do .NET Compiler Platform](roslyn-analyzers-overview.md)
- [Migrar para analisadores de .NET](migrate-from-legacy-analysis-to-net-analyzers.md)
- [Instalar analisadores de .NET](install-net-analyzers.md)
