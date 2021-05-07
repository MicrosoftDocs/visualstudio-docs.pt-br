---
title: Análise de código usando os analisadores do Roslyn
ms.date: 09/01/2020
description: Familiarizar-se com a análise de código-fonte Visual Studio. Saiba mais sobre correções de código e os diferentes tipos de analisadores e níveis de severidade.
ms.custom: SEO-VS-2020
ms.topic: overview
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
- code analyzers
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: c3a7192ac55dc4138746e3e1e1abe4eaa6928395
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798330"
---
# <a name="overview-of-source-code-analysis"></a>Visão geral da análise de código-fonte

.NET Compiler Platform analisadores (Roslyn) inspecionam seu código C# ou Visual Basic por estilo, qualidade, capacidade de manutenção, design e outros problemas. Essa inspeção ou análise é feita durante o tempo de design em todos os arquivos abertos.

Os analisadores podem ser divididos nos seguintes grupos:

- [Os analisadores](/dotnet/fundamentals/code-analysis/code-style-rule-options?preserve-view=true&view=vs-2019#convention-categories) de estilo de código são integrados Visual Studio. A ID de diagnóstico ou código para esses analisadores é do formato IDExxxx, por exemplo, IDE0067. Você pode configurar preferências na página [de opções do editor de texto](../ide/code-styles-and-code-cleanup.md) ou em um arquivo [EditorConfig](/dotnet/fundamentals/code-analysis/code-style-rule-options). A partir do .NET 5.0, os analisadores de estilo de código são incluídos no SDK do .NET e podem ser imposto estritamente como avisos de build ou erros. Para mais informações, consulte [aqui](/dotnet/fundamentals/productivity/code-analysis#code-style-analysis).

- [Os analisadores](/dotnet/fundamentals/code-analysis/quality-rules/index) de qualidade de código agora estão incluídos no SDK do .NET 5 e habilitados por padrão. A ID de diagnóstico ou código para esses analisadores é do formato CAxxxx, por exemplo, CA1822. Para obter mais informações, consulte [Visão geral da análise de qualidade de código do .NET.](/dotnet/fundamentals/productivity/code-analysis#code-quality-analysis)

- Os analisadores de terceiros podem ser instalados como um pacote NuGet ou uma extensão Visual Studio aplicativo. Analisadores de terceiros, como [StyleCop,](https://www.nuget.org/packages/StyleCop.Analyzers/) [Roslynator,](https://www.nuget.org/packages/Roslynator.Analyzers/) [Analisadores XUnit](https://www.nuget.org/packages/xunit.analyzers/)e [Sonar Analyzer.](https://www.nuget.org/packages/SonarAnalyzer.CSharp/)

## <a name="severity-levels-of-analyzers"></a>Níveis de severidade de analisadores

Cada analisador tem um dos seguintes níveis de severidade:

| Gravidade (Gerenciador de Soluções) | Gravidade (arquivo EditorConfig) | Comportamento de tempo de build | Comportamento do editor |
|-|-|-|
| Erro | `error` | As violações aparecem como *erros* na lista de erros e na saída da compilação da linha de comando e causam a falha das compilações.| O código incorreto é sublinhado com um ondulado vermelho e marcado por uma pequena caixa vermelha na barra de rolagem. |
| Aviso | `warning` | As violações aparecem como *avisos* no lista de erros e na saída da compilação da linha de comando, mas não causam a falha das compilações. | O código incorreto é sublinhado com um ondulado verde e marcado por uma pequena caixa verde na barra de rolagem. |
| Info | `suggestion` | As violações aparecem como *mensagens* no lista de erros, e não em uma saída de compilação de linha de comando. | O código incorreto é sublinhado com um rabisco cinza e marcado por uma pequena caixa cinza na barra de rolagem. |
| Hidden | `silent` | Não visível para o usuário. | Não visível para o usuário. No entanto, o diagnóstico é reportado para o mecanismo de diagnóstico do IDE. |
| Nenhum | `none` | Suprimido completamente. | Suprimido completamente. |
| Padrão | `default` | Corresponde à severidade padrão da regra. Para determinar qual é o valor padrão de uma regra, procure na janela Propriedades. | Corresponde à severidade padrão da regra. |

Se violações de regra forem encontradas por um analisador, elas serão relatadas no editor de códigos (como um *rabisco* no código incorreto) e na janela de lista de erros.

![Violação do analisador na janela Lista de Erros](../code-quality/media/code-analysis-error-list.png)

As violações do analisador relatadas na lista de erros correspondem à [configuração de nível de severidade](../code-quality/use-roslyn-analyzers.md#configure-severity-levels) da regra. As violações do analisador também aparecem no editor de códigos como ondulado no código incorreto. A imagem a seguir mostra três violações &mdash; um erro (ondulado vermelho), um aviso (ondulado verde) e uma sugestão (três pontos cinzas):

![Alternâncias no editor de códigos no Visual Studio](media/diagnostics-severity-colors.png)

Muitas regras de analisador, ou diagnóstico,  têm uma ou mais correções de código *associadas* que você pode aplicar para corrigir a violação de regra. As correções de código são mostradas no menu do ícone de lâmpada, juntamente com outros tipos de [Ações rápidas](../ide/quick-actions.md). Para saber mais sobre essas correções de código, confira [Ações rápidas comuns](../ide/quick-actions.md).

![Violação do analisador e correção de código de Ação Rápida](../code-quality/media/built-in-analyzer-code-fix.png)

## <a name="configure-analyzer-severity-levels"></a>Configurar níveis de severidade do analisador

Você pode configurar a severidade das regras do analisador, ou *diagnóstico,* em um [arquivo EditorConfig](../code-quality/use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file) ou no [menu de lâmpada](../code-quality/use-roslyn-analyzers.md#set-rule-severity-from-the-light-bulb-menu).

Os analisadores também podem ser configurados para inspecionar o código em tempo de build e ao vivo conforme você digita. Você pode configurar o escopo da análise de código ao vivo para executar apenas para o documento atual, todos os documentos abertos ou toda a solução. Consulte [Como configurar o escopo da análise de código ao vivo.](./configure-live-code-analysis-scope-managed-code.md)

> [!TIP]
> Erros e avisos de tempo de build dos analisadores de código serão mostrados apenas se os analisadores estiverem instalados como um pacote NuGet. Os analisadores integrados (por exemplo, IDE0067 e IDE0068) nunca são executados durante o build.

## <a name="nuget-package-versus-vsix-extension"></a>Pacote NuGet em comparação com a extensão do VSIX

Os analisadores de terceiros podem ser instalados por projeto por meio de um pacote NuGet. Alguns também estão disponíveis como uma extensão Visual Studio, caso em que se aplicam a qualquer solução que você abrir Visual Studio. Há algumas importantes diferenças de comportamento entre esses dois métodos de [instalar analisadores](../code-quality/install-roslyn-analyzers.md).

### <a name="scope"></a>Escopo

Se você instalar analisadores como uma extensão Visual Studio, eles serão aplicados no nível da solução e em todas as instâncias do Visual Studio. Se você instalar os analisadores como um pacote NuGet, que é o método preferencial, eles serão aplicáveis somente ao projeto em que o pacote NuGet foi instalado. Em ambientes de equipe, os analisadores instalados como pacotes NuGet estão no escopo para *todos os desenvolvedores* que trabalham nesse projeto.

### <a name="build-errors"></a>Erros de compilação

Para que as regras sejam impostas no tempo de build, incluindo por meio da linha de comando ou como parte de um build de CI (integração contínua), você pode escolher entre uma das seguintes opções:

- Crie um projeto do .NET 5.0 que inclui analisadores por padrão no SDK do .NET. A análise de código está habilitada, por padrão, para projetos direcionados ao .NET 5.0 ou posterior. Você pode habilitar a análise de código em projetos destinados a versões anteriores do .NET definindo a propriedade [EnableNETAnalyzers](/dotnet/core/project-sdk/msbuild-props#enablenetanalyzers) como true.

- Instalar analisadores como um pacote NuGet. Os erros e avisos do analisador não serão exibidos no relatório de build se você instalar os analisadores como uma extensão.

A imagem a seguir mostra a saída de build de linha de comando da criação de um projeto que contém uma violação de regra do analisador:

![Saída do MSBuild com violação de regra](media/command-line-build-analyzers.png)

### <a name="rule-severity"></a>Gravidade da regra

Você não pode configurar a severidade das regras de analisadores que foram instalados como uma extensão Visual Studio aplicativo. Para configurar a [gravidade da regra](../code-quality/use-roslyn-analyzers.md#configure-severity-levels), instale os analisadores como um pacote NuGet.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Instalar analisadores de código no Visual Studio](../code-quality/install-roslyn-analyzers.md)

> [!div class="nextstepaction"]
> [Usar analisadores de código no Visual Studio](../code-quality/use-roslyn-analyzers.md)

## <a name="see-also"></a>Consulte também

- [Perguntas frequentes sobre analisadores](analyzers-faq.yml)
- [Gravar seu próprio analisador de código](../extensibility/getting-started-with-roslyn-analyzers.md)
- [SDK da Plataforma do Compilador .NET](/dotnet/csharp/roslyn-sdk/)