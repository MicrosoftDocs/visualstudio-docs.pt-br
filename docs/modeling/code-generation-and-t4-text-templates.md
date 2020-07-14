---
title: Geração de código e modelos de texto T4
ms.date: 11/04/2016
ms.topic: overview
f1_keywords:
- VS.ToolsOptionsPages.TextTemplating.TextTemplating
helpviewer_keywords:
- generating text
- .tt files
- code generation
- text templates
- generating code
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fbcd41461ab57e3bbb5fb48849ddde8593c587fb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548233"
---
# <a name="code-generation-and-t4-text-templates"></a>Geração de código e modelos de texto T4

No Visual Studio, um *modelo de texto T4* é uma mistura de blocos de texto e lógica de controle que pode gerar um arquivo de texto. A lógica de controle é escrita como fragmentos de código de programa no [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] ou no [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] . No Visual Studio 2015 atualização 2 e posterior, você pode usar os recursos da versão 6,0 do C# em diretivas de modelos T4. O arquivo gerado pode ser um texto de qualquer tipo, como uma página da Web, um arquivo de recurso ou um código-fonte do programa em qualquer idioma.

Há dois tipos de modelos de texto T4: tempo de execução e tempo de design.

## <a name="run-time-t4-text-templates"></a>Modelos de texto T4 de tempo de execução

Também conhecidos como modelos ' pré-processados ', os modelos de tempo de execução são executados em seu aplicativo para produzir cadeias de caracteres de texto, normalmente como parte de sua saída. Por exemplo, você pode criar um modelo para definir uma página HTML:

```
<html><body>
 The date and time now is: <#= DateTime.Now #>
</body></html>
```

Observe que o modelo se assemelha à saída gerada. A similaridade do modelo para a saída resultante ajuda a evitar erros quando você deseja alterá-lo.

Além disso, o modelo contém fragmentos do código do programa. Você pode usar esses fragmentos para repetir seções de texto, para fazer seções condicionais e para mostrar dados de seu aplicativo.

Para gerar a saída, seu aplicativo chama uma função que é gerada pelo modelo. Por exemplo:

```csharp
string webResponseText = new MyTemplate().TransformText();
```

Seu aplicativo pode ser executado em um computador que não tem o Visual Studio instalado.

Para criar um modelo de tempo de execução, adicione um arquivo de **modelo de texto pré-processado** ao seu projeto. Como alternativa, você pode adicionar um arquivo de texto sem formatação e definir sua propriedade de **ferramenta personalizada** como **TextTemplatingFilePreprocessor**.

Para obter mais informações, consulte [geração de texto em tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md). Para obter mais informações sobre a sintaxe de modelos, consulte [escrevendo um modelo de texto T4](../modeling/writing-a-t4-text-template.md).

## <a name="design-time-t4-text-templates"></a>Modelos de texto T4 de tempo de design

Os modelos de tempo de design definem parte do código-fonte e outros recursos do seu aplicativo. Normalmente, você usa vários modelos que lêem os dados em um único arquivo de entrada ou banco de dado e geram alguns dos seus arquivos *. cs*, *. vb*ou outros. Cada modelo gera um arquivo. Eles são executados dentro do Visual Studio ou do MSBuild.

Por exemplo, os dados de entrada podem ser um arquivo XML de dados de configuração. Sempre que você editar o arquivo XML durante o desenvolvimento, os modelos de texto regenerarão parte do código do aplicativo. Um dos modelos pode ser semelhante ao exemplo a seguir:

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

Dependendo dos valores no arquivo XML, o arquivo *. cs* gerado seria semelhante ao seguinte:

```
namespace Fabrikam.FirstJob
{
  ... // More code here.
}
```

Como outro exemplo, a entrada pode ser um diagrama de fluxo de trabalho em uma atividade de negócios. Quando os usuários alteram seu fluxo de trabalho de negócios, ou quando você começa a trabalhar com novos usuários que têm um Workflow diferente, é fácil regenerar o código para se ajustar ao novo modelo.

Os modelos de tempo de design tornam mais rápido e mais confiável alterar a configuração quando os requisitos mudam. Normalmente, a entrada é definida em termos de requisitos de negócios, como no exemplo de fluxo de trabalho. Isso facilita a discussão sobre as alterações com seus usuários. Os modelos de tempo de design são, portanto, uma ferramenta útil em um processo de desenvolvimento ágil.

Para criar um modelo de tempo de design, adicione um arquivo de **modelo de texto** ao seu projeto. Como alternativa, você pode adicionar um arquivo de texto sem formatação e definir sua propriedade de **ferramenta personalizada** como **TextTemplatingFileGenerator**.

Para obter mais informações, consulte [geração de código em tempo de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md). Para obter mais informações sobre a sintaxe de modelos, consulte [escrevendo um modelo de texto T4](../modeling/writing-a-t4-text-template.md).

> [!NOTE]
> O termo *modelo* é, às vezes, usado para descrever os dados lidos por um ou mais modelos. O modelo pode estar em qualquer formato, em qualquer tipo de arquivo ou banco de dados. Ele não precisa ser um modelo UML ou um modelo de linguagem específico de domínio. ' Model ' indica apenas que os dados podem ser definidos em termos dos conceitos comerciais, em vez de se lembrar do código.

O recurso de transformação de modelo de texto se chama *T4*.

## <a name="see-also"></a>Confira também

- [Gerar código com base em uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md)
