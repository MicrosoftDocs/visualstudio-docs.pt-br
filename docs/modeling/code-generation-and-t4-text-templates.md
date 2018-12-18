---
title: Geração de código e modelos de texto T4
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.TextTemplating.TextTemplating
helpviewer_keywords:
- generating text
- .tt files
- code generation
- text templates
- generating code
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a273e6a82bbf99d1a3d57f3759504fedaa5532e6
ms.sourcegitcommit: 5b767247b3d819a99deb0dbce729a0562b9654ba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39176275"
---
# <a name="code-generation-and-t4-text-templates"></a>Geração de código e modelos de texto T4

No Visual Studio, uma *modelo de texto T4* é uma mistura de blocos de texto e a lógica de controle que pode gerar um arquivo de texto. A lógica de controle é escrita como fragmentos de código de programa na [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] ou [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]. No Visual Studio 2015 atualização 2 e posterior, você pode usar os recursos de versão 6.0 do c# nas diretivas de modelos T4. O arquivo gerado pode ser texto de qualquer tipo, como uma página da web, um arquivo de recurso ou código de origem do programa em qualquer idioma.

Há dois tipos de modelos de texto T4: tempo de execução e tempo de design.

## <a name="run-time-t4-text-templates"></a>Modelos de texto T4 de tempo de execução

Também conhecido como 'pré-processado' modelos, modelos de tempo de execução são executados em seu aplicativo para produzir cadeias de caracteres de texto, normalmente como parte de sua saída. Por exemplo, você pode criar um modelo para definir uma página HTML:

```
<html><body>
 The date and time now is: <#= DateTime.Now #>
</body></html>
```

Observe que o modelo é semelhante a saída gerada. A semelhança do modelo para a saída resultante ajuda a evitar erros quando você deseja alterá-lo.

Além disso, o modelo contém fragmentos de código do programa. Você pode usar esses fragmentos repetir seções de texto, para tornar as seções condicionais e para mostrar os dados do seu aplicativo.

Para gerar a saída, o aplicativo chama uma função que é gerada pelo modelo. Por exemplo:

```csharp
string webResponseText = new MyTemplate().TransformText();
```

Seu aplicativo pode ser executado em um computador que não tenha instalado o Visual Studio.

Para criar um modelo de tempo de execução, adicione uma **modelo de texto de pré-processado** ao seu projeto. Como alternativa, você pode adicionar um arquivo de texto sem formatação e defina suas **Custom Tool** propriedade **TextTemplatingFilePreprocessor**.

Para obter mais informações, consulte [geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md). Para obter mais informações sobre a sintaxe de modelos, consulte [gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md).

## <a name="design-time-t4-text-templates"></a>Modelos de texto T4 de tempo de design

Modelos de tempo de design definem parte do código-fonte e outros recursos do seu aplicativo. Normalmente você usar vários modelos que ler os dados em um único arquivo de entrada ou o banco de dados e gerar alguns dos seus *. CS*, *. vb*, ou outros arquivos de origem. Cada modelo gera um arquivo. Eles são executados dentro do Visual Studio ou o MSBuild.

Por exemplo, os dados de entrada pode ser um arquivo XML de dados de configuração. Sempre que você edite o arquivo XML durante o desenvolvimento, os modelos de texto regenerar parte do código do aplicativo. Um dos modelos poderia se parecer com o exemplo a seguir:

```
<#@ output extension=".cs" #>
<#@ assembly name="System.Xml" #>
<#
 System.Xml.XmlDocument configurationData = ...; // Read a data file here.
#>
namespace Fabrikam.<#= configurationData.SelectSingleNode("jobName").Value #>
{
  ... // More code here.
}
```

Dependendo dos valores no arquivo XML gerado *. CS* arquivo seria semelhante ao seguinte:

```
namespace Fabrikam.FirstJob
{
  ... // More code here.
}
```

Como outro exemplo, a entrada poderia ser um diagrama de fluxo de trabalho em uma atividade de negócios. Quando os usuários alterarem seu fluxo de trabalho de negócios ou quando você começa a trabalhar com novos usuários que têm um fluxo de trabalho diferente, é fácil gerar novamente o código de acordo com o novo modelo.

Modelos de tempo de design torná-lo mais rápido e confiável para alterar a configuração, quando os requisitos são alterados. Normalmente, a entrada é definida em termos de requisitos de negócios, como no exemplo de fluxo de trabalho. Isso torna mais fácil discutir as alterações com seus usuários. Modelos de tempo de design são, portanto, uma ferramenta útil em um processo de desenvolvimento do agile.

Para criar um modelo de tempo de design, adicione uma **modelo de texto** ao seu projeto. Como alternativa, você pode adicionar um arquivo de texto sem formatação e defina suas **Custom Tool** propriedade **TextTemplatingFileGenerator**.

Para obter mais informações, consulte [geração de código de tempo de Design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md). Para obter mais informações sobre a sintaxe de modelos, consulte [gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md).

> [!NOTE]
> O termo *modelo* , às vezes, é usado para descrever dados lidos por um ou mais modelos. O modelo pode estar em qualquer formato, em qualquer tipo de arquivo ou banco de dados. Ele não precisa ser um modelo UML ou um modelo de linguagem específica do domínio. 'Model' indica apenas que os dados podem ser definidos em termos de conceitos de negócios, em vez de que se assemelha o código.

O recurso de transformação do modelo de texto é denominado *T4*.

## <a name="see-also"></a>Consulte também

- [Gerar código com base em uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md)
