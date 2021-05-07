---
title: EditorConfig versus analisadores
ms.date: 03/11/2019
description: Saiba mais sobre a análise de código baseada em .NET Compiler Platform no Visual Studio. Consulte as respostas para perguntas sobre arquivos EditorConfig, conjuntos de regras e outros tópicos.
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- analyzers, faq
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6d67471027f36d0e22c055f4306ce2137d972463
ms.sourcegitcommit: dd2fc6e03a789c044f8438096b8f112e4dba5557
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2021
ms.locfileid: "108800469"
---
# <a name="code-analysis-faq"></a>Perguntas frequentes sobre análise de código

Esta página contém respostas para algumas perguntas frequentes sobre a análise de código baseada em .NET Compiler Platform no Visual Studio.

## <a name="code-analysis-versus-editorconfig"></a>Análise de código versus EditorConfig

**P**: devo usar a análise de código ou EditorConfig para verificar o estilo de código?

**R: A** análise de código e os arquivos EditorConfig funcionam lado a lado. Quando você define estilos [de código em um arquivo EditorConfig](/dotnet/fundamentals/code-analysis/code-style-rule-options) ou na página de [Opções do editor de texto](../ide/code-styles-and-code-cleanup.md) , na verdade está configurando os analisadores de código que são criados no Visual Studio. Os arquivos EditorConfig podem ser usados para habilitar ou desabilitar as regras do analisador e também para configurar pacotes do NuGet Analyzer.

## <a name="editorconfig-versus-rule-sets"></a>EditorConfig versus conjuntos de regras

**P**: devo configurar meus analisadores usando um conjunto de regras ou um arquivo EditorConfig?

**R**: conjuntos de regras e arquivos EditorConfig podem coexistir e ambos podem ser usados para configurar analisadores. Os arquivos EditorConfig e os conjuntos de regras permitem habilitar e desabilitar regras e definir sua gravidade.

No entanto, os arquivos EditorConfig oferecem maneiras adicionais de configurar regras também:

- Para os analisadores de qualidade de código .NET, os arquivos EditorConfig permitem que você [Defina quais tipos de código analisar](/dotnet/fundamentals/code-analysis/code-quality-rule-options).
- Para os analisadores de estilo de código .NET criados no Visual Studio, os arquivos EditorConfig permitem que você [defina os estilos de código preferenciais](/dotnet/fundamentals/code-analysis/code-style-rule-options) para uma codebase.

Além dos conjuntos de regras e arquivos EditorConfig, alguns analisadores são configurados por meio do uso de arquivos de texto marcados como [arquivos adicionais](../ide/build-actions.md#build-action-values) para os compiladores C# e VB.

> [!NOTE]
> - Os arquivos EditorConfig só podem ser usados para habilitar regras e definir sua gravidade no Visual Studio 2019 versão 16,3 e posterior.
> - Os arquivos EditorConfig não podem ser usados para configurar a análise herdada, enquanto os conjuntos de regras podem.

## <a name="code-analysis-in-ci-builds"></a>Análise de código em builds de CI

**P:** A .NET Compiler Platform de código baseada em dados funciona em builds de CI (integração contínua) ?

**R**: Sim. Para analisadores instalados de um pacote NuGet, essas regras são impostas em tempo [de build,](roslyn-analyzers-overview.md#build-errors)incluindo durante um build de CI. Analisadores usados em builds de CI respeitam a configuração de regra de conjuntos de regras e arquivos EditorConfig. Atualmente, os analisadores de código que são integrados Visual Studio não estão disponíveis como um pacote NuGet e, portanto, essas regras não são imposiveis em um build de CI.

## <a name="ide-analyzers-versus-stylecop"></a>Analisadores de IDE versus StyleCop

**P:** Qual é a diferença entre os analisadores de código Visual Studio IDE e os analisadores styleCop?

**R:** o Visual Studio IDE inclui analisadores integrados que buscam problemas de qualidade e estilo de código. Essas regras ajudam você a usar novos recursos de linguagem à medida que eles são introduzidos e a melhorar a capacidade de manutenção do código. Os analisadores de IDE são atualizados continuamente com cada Visual Studio versão.

[Os analisadores StyleCop](https://github.com/DotNetAnalyzers/StyleCopAnalyzers) são analisadores de terceiros instalados como um pacote NuGet que verificam a consistência de estilo em seu código. Em geral, as regras do StyleCop permitem definir preferências pessoais para uma base de código sem recomendar um estilo em vez de outro.

## <a name="code-analyzers-versus-legacy-analysis"></a>Analisadores de código versus análise herdada

**P:** Qual é a diferença entre a análise herdada e .NET Compiler Platform de código baseada em dados?

**R:**.NET Compiler Platform de código baseado em dados analisa o código-fonte em tempo real e durante a compilação, enquanto a análise herdada analisa arquivos binários após a conclusão do build. Para obter mais informações, [.NET Compiler Platform análise baseada em dados versus análise herdada](../code-quality/net-analyzers-faq.md#whats-the-difference-between-legacy-fxcop-and-net-analyzers).

## <a name="fxcop-analyzers-versus-net-analyzers"></a>Analisadores FxCop versus analisadores .NET

**P:** Qual é a diferença entre analisadores FxCop e analisadores do .NET?

**R:** Os analisadores FxCop e os analisadores do .NET referem-se às implementações do analisador .NET Compiler Platform ("Roslyn") das regras de AC do FxCop. Antes Visual Studio 2019 16.8 e .NET 5.0, esses analisadores eram fornecidos como o `Microsoft.CodeAnalysis.FxCopAnalyzers` [pacote NuGet.](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers) A partir do Visual Studio 2019 16,8 e do .NET 5,0, esses analisadores estão [incluídos no SDK do .net](/dotnet/fundamentals/code-analysis/overview). Eles também estão disponíveis como `Microsoft.CodeAnalysis.NetAnalyzers` [pacote NuGet](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers). Considere [migrar dos analisadores do FxCop para os analisadores do .net](migrate-from-fxcop-analyzers-to-net-analyzers.md).

## <a name="treat-warnings-as-errors"></a>Tratar avisos como erros

**P**: meu projeto usa a opção de compilação para tratar avisos como erros. Depois de migrar da análise herdada para a análise de código-fonte, todos os avisos de análise de código agora aparecem como erros. Como posso evitar isso?

**R**: para impedir que avisos de análise de código sejam tratados como erros, siga estas etapas:

  1. Crie um arquivo. props com o seguinte conteúdo:

     ```xml
     <Project>
        <PropertyGroup>
           <CodeAnalysisTreatWarningsAsErrors>false</CodeAnalysisTreatWarningsAsErrors>
        </PropertyGroup>
     </Project>
     ```

  2. Adicione uma linha a seu arquivo de projeto. csproj ou. vbproj para importar o arquivo. props criado na etapa anterior. Essa linha deve ser colocada antes de qualquer linha que importe os arquivos do Analyzer. props. Por exemplo, se o arquivo. props for nomeado CodeAnalysis. props:

     ```xml
     ...
     <Import Project="..\..\codeanalysis.props" Condition="Exists('..\..\codeanalysis.props')" />
     <Import Project="..\packages\Microsoft.CodeAnalysis.NetAnalyzers.5.0.0\build\Microsoft.CodeAnalysis.NetAnalyzers.props" Condition="Exists('..\packages\Microsoft.CodeAnalysis.NetAnalyzers.5.0.0\build\Microsoft.CodeAnalysis.NetAnalyzers.props')" />
     ...
     ```

## <a name="code-analysis-solution-property-page"></a>Página de propriedades da solução de análise de código

**P**: onde está a página de propriedades de análise de código para a solução?

**R**: a página de propriedades de análise de código no nível da solução foi removida em favor do grupo de propriedades compartilhada mais confiável. Para gerenciar a análise de código no nível do projeto, a página de propriedades de análise de código ainda está disponível. (Para projetos gerenciados, também recomendamos migrar de RuleSets para EditorConfig para a configuração de regra.)  Para compartilhar conjuntos de regras em vários/todos os projetos em uma solução ou um repositório, é recomendável definir um grupo de propriedades com a propriedade [CodeAnalysisRuleSet](../code-quality/using-rule-sets-to-group-code-analysis-rules.md#specify-a-rule-set-for-a-project) em um arquivo de propriedades/destinos compartilhado ou *diretório. props/Directory. targets* . Se você não tiver nenhuma Props ou destinos comuns que todos os seus projetos importam, considere adicionar um grupo de propriedades a um [diretório. props ou um arquivo Directory. targets](../msbuild/customize-your-build.md) em um diretório de solução de nível superior, que é importado automaticamente em todos os arquivos de projeto definidos no diretório ou em seus subpastas.

## <a name="see-also"></a>Confira também

- [Visão geral dos analisadores](roslyn-analyzers-overview.md)
- [Configurações da Convenção de codificação .NET para EditorConfig](/dotnet/fundamentals/code-analysis/code-style-rule-options)