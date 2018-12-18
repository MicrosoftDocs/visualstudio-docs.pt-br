---
title: Análise de código usando os analisadores do Roslyn
ms.date: 03/26/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: overview
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 620f2905e2511ed403f0d25f32fa1bfc9b1eca68
ms.sourcegitcommit: 54c65f81a138fc1e8ff1826f7bd9dcec710618cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51948836"
---
# <a name="overview-of-net-compiler-platform-analyzers"></a>Visão geral dos analisadores do .NET Compiler Platform

O Visual Studio 2017 inclui um conjunto interno de analisadores do .NET Compiler Platform que analisam o código C# e Visual Basic durante a digitação. Os analisadores examinam o estilo do código, a qualidade e a capacidade de manutenção do código, o design do código e outros problemas. Instale outros analisadores como uma extensão do Visual Studio ou por projeto como um pacote NuGet.

Se um analisador encontrar violações de regra, elas serão relatadas no editor de códigos como uma *linha ondulada* embaixo do código transgressor e na **Lista de Erros**.

Muitas regras do analisador ou *diagnósticos* têm uma ou mais *correções de código* associadas que podem ser aplicadas para corrigir o problema. Cada diagnóstico do analisador inserido no Visual Studio tem uma correção de código associada. Correções de código são mostradas no menu do ícone de lâmpada, juntamente com outros tipos de *Ações rápidas*. Para saber mais sobre essas correções de código, confira [Ações rápidas comuns](../ide/common-quick-actions.md).

![Violação do analisador e correção de código de Ação Rápida](../code-quality/media/built-in-analyzer-code-fix.png)

## <a name="roslyn-analyzers-vs-static-code-analysis"></a>Analisadores do Roslyn vs. análise de código estático

Os Analisadores do .NET Compiler Platform ("Roslyn") substituirão eventualmente a [análise de código estático](../code-quality/code-analysis-for-managed-code-overview.md) por código gerenciado. Muitas das regras de análise de código estático já foram reescritas como diagnóstico de analisador do Roslyn.

Como violações de regra de análise de código estático, as violações de analisador do Roslyn são exibidas na **Lista de Erros**. Além disso, as violações de analisador do Roslyn também são mostradas no editor de códigos, como *linhas onduladas* embaixo do código incorreto. A cor da linha ondulada depende da [configuração de gravidade](../code-quality/use-roslyn-analyzers.md#rule-severity) da regra. A captura de tela a seguir mostra três violações&mdash;uma vermelha, uma verde e uma cinza:

![Linhas onduladas no editor de códigos](media/diagnostics-severity-colors.png)

Os analisadores do Roslyn analisam código em tempo de build, como análise de código estático, se habilitada, mas também em tempo real conforme você digita! Os analisadores do Roslyn também poderão fornecer análise em tempo de design dos arquivos de código que não estão abertos no editor se você habilitar [análise de solução completa](../code-quality/how-to-enable-and-disable-full-solution-analysis-for-managed-code.md#to-toggle-full-solution-analysis).

> [!NOTE]
> Erros e avisos de tempo de build de analisadores do Roslyn serão mostrados apenas se os analisadores estiverem instalados como um pacote NuGet.

Os analisadores do Roslyn não só comunicam os mesmos tipos de problemas que a análise de código estático, mas também facilitam a correção de uma ou todas as ocorrências da violação no seu arquivo ou projeto. Essas ações são denominadas *correções de código*. As correções de código são específicas do IDE; no Visual Studio, elas são implementadas como [Ações rápidas](../ide/quick-actions.md). Nem todos os diagnósticos do analisador têm uma correção de código associada.

> [!NOTE]
> A opção de menu **Analisar** > **Executar análise de código** aplica-se apenas à análise de código estático. Além disso, na página de propriedades **Análise de código** de um projeto, as caixas de seleção **Habilitar análise de código no build** e **Suprimir resultados do código gerado** são aplicáveis apenas à análise de código estático. Eles não têm efeito nenhum sobre os analisadores do Roslyn.

Para diferenciar entre as violações de analisadores do Roslyn e análise de código estático na **Lista de Erros**, examine a coluna **Ferramenta**. Se o valor Ferramenta corresponder a um dos assemblies do analisador no **Gerenciador de Soluções**, por exemplo **Microsoft.CodeQuality.Analyzers**, a violação será proveniente de um analisador do Roslyn. Caso contrário, a violação será proveniente da análise de código estático.

![Coluna Ferramenta na Lista de Erros](media/code-analysis-tool-in-error-list.png)

## <a name="nuget-package-versus-vsix-extension"></a>Pacote NuGet em comparação com a extensão do VSIX

Os analisadores do .NET Compiler Platform podem ser instalados por projeto por meio de um pacote NuGet ou em todo o Visual Studio como uma extensão dele. Há algumas importantes diferenças de comportamento entre esses dois métodos de [instalar analisadores](../code-quality/install-roslyn-analyzers.md).

### <a name="scope"></a>Escopo

Se você instalar analisadores como uma extensão do Visual Studio, então aplique, no nível da solução, a todas as instâncias do Visual Studio. Se você instalar os analisadores como um pacote NuGet, que é o método preferencial, eles serão aplicáveis somente ao projeto em que o pacote NuGet foi instalado. Em ambientes de equipe, os analisadores instalados como pacotes NuGet estão no escopo para *todos os desenvolvedores* que trabalham nesse projeto.

### <a name="build-errors"></a>Erros de build

Para que as regras sejam impostas no tempo de build, incluindo por meio da linha de comando ou como parte de uma build de CI (integração contínua), instale os analisadores como um pacote NuGet. Os erros e avisos do analisador não serão exibidos no relatório de build se você instalar os analisadores como uma extensão.

A captura de tela a seguir mostra a saída de build da linha de comando da criação de um projeto que contém uma violação de regra de analisador:

![Saída do MSBuild com violação de regra](media/command-line-build-analyzers.png)

### <a name="rule-severity"></a>Gravidade da regra

Não é possível definir a gravidade das regras de analisadores que foram instalados como uma extensão do Visual Studio. Para configurar a [gravidade da regra](../code-quality/use-roslyn-analyzers.md#rule-severity), instale os analisadores como um pacote NuGet.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Instalar Analisadores do Roslyn no Visual Studio](../code-quality/install-roslyn-analyzers.md)

> [!div class="nextstepaction"]
> [Usar Analisadores do Roslyn no Visual Studio](../code-quality/use-roslyn-analyzers.md)

## <a name="see-also"></a>Consulte também

- [Ações rápidas no Visual Studio](../ide/quick-actions.md)
- [Escrever seu próprio analisador do Roslyn](../extensibility/getting-started-with-roslyn-analyzers.md)
- [SDK do .NET Compiler Platform](/dotnet/csharp/roslyn-sdk/)