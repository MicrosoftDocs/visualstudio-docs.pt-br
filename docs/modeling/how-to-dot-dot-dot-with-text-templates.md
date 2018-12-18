---
title: Como ... com modelos de texto
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 20dbc5223ddb053355fa5e8076ae66badee688a4
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49883062"
---
# <a name="how-to--with-text-templates"></a>Como ... com modelos de texto
Modelos de texto no Visual Studio fornecem uma maneira útil de geração de texto de qualquer tipo. Você pode usar modelos de texto para gerar o texto em tempo de execução como parte do seu aplicativo e em tempo de design para gerar alguns dos seus códigos de projeto. Este tópico resume com mais frequência solicitado "Como faço...?" perguntas.

 Neste tópico, várias respostas que são precedidas por marcadores são sugestões alternativas.

 Para obter uma introdução geral para modelos de texto, leia [geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md).

## <a name="how-to-"></a>Como...

### <a name="generate-part-of-my-application-code"></a>Gerar parte do código do meu aplicativo
 Eu tenho uma configuração ou *modelo* em um arquivo ou um banco de dados. Uma ou mais partes do meu código dependem do modelo.

-   Gere alguns dos seus arquivos de código de modelos de texto. Para obter mais informações, consulte [geração de código de tempo de Design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md) e [o que é a melhor maneira de começar a escrever um modelo?](#starting).

### <a name="generate-files-at-run-time-passing-data-into-the-template"></a>Gerar arquivos em tempo de execução, passando dados para o modelo
 Em tempo de execução, o meu aplicativo gera arquivos de texto, como relatórios, que contêm uma mistura de texto padrão e os dados. Eu quero evitar a escrita de centenas de `write` instruções.

-   Adicione um modelo de texto de tempo de execução ao seu projeto. Este modelo cria uma classe em seu código, o que você pode instanciar e usar para gerar o texto. Você pode passar dados para ele nos parâmetros do construtor. Para obter mais informações, consulte [geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md).

-   Se você quiser gerar a partir de modelos que estão disponíveis somente em tempo de execução, você pode usar modelos de texto padrão. Se você estiver escrevendo uma extensão do Visual Studio, você pode invocar o serviço de modelagem de texto. Para obter mais informações, consulte [invocando transformação de texto em uma extensão do VS](../modeling/invoking-text-transformation-in-a-vs-extension.md). Em outros contextos, você pode usar o mecanismo de modelagem de texto. Para obter mais informações, consulte <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName>.

     Use o \<#@parameter#> diretiva para passar parâmetros para esses modelos. Para obter mais informações, consulte [diretiva de parâmetro T4](../modeling/t4-parameter-directive.md).

### <a name="read-another-project-file-from-a-template"></a>Ler a outro arquivo de projeto de um modelo
 Para ler um arquivo de projeto do Visual Studio como o modelo:

-   Insira `hostSpecific="true"` na diretiva `<#@template#>`.

     No seu código, use `this.Host.ResolvePath(filename)` para obter o caminho completo do arquivo.

### <a name="invoke-methods-from-a-template"></a>Invocar métodos de um modelo
 Se os métodos já existirem, por exemplo, no padrão [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] classes:

- Use o \<#@assembly#> diretiva para carregar o assembly e usar \<#@import#> para definir o contexto de namespace. Para obter mais informações, consulte [diretiva de importação T4](../modeling/t4-import-directive.md).

   Se você frequentemente usa o mesmo conjunto de assembly e importar diretivas, considere a possibilidade de escrever um processador de diretriz. Em cada modelo, você pode invocar o processador de diretriz, que pode carregar os assemblies e os arquivos de modelo e definir o contexto de namespace. Para obter mais informações, consulte [criando processadores diretiva de modelo de texto do personalizado T4](../modeling/creating-custom-t4-text-template-directive-processors.md).

  Se você estiver escrevendo os métodos:

- Se você estiver gravando um modelo de texto de tempo de execução, escreva uma definição de classe parcial que tem o mesmo nome que seu modelo de texto de tempo de execução. Adicione os métodos adicionais para essa classe.

- Gravar um bloco de controle de recurso de classe `<#+ ... #>` no qual você pode declarar métodos, propriedades e classes privadas. Quando o modelo de texto é compilado, ele será transformado em uma classe. Os blocos de controle padrão `<#...#>` e texto são transformados em um único método, e blocos de recurso de classe são inseridos como membros separados. Para obter mais informações, consulte [blocos de controle de modelo de texto](../modeling/text-template-control-blocks.md).

   Métodos definidos como recursos de classe também podem incluir os blocos de texto inserido.

   Considere a colocação de recursos de classe em um arquivo separado que você pode `<#@include#>` em um ou mais arquivos de modelo.

- Os métodos de gravação em um assembly separado (biblioteca de classes) e chamá-los a partir de seu modelo. Use o `<#@assembly#>` diretiva para carregar o assembly e `<#@import#>` para definir o contexto de namespace. Observe que para recompilar o assembly enquanto você depurá-lo, você terá que parar e reiniciar o Visual Studio. Para obter mais informações, consulte [diretivas de modelo de texto T4](../modeling/t4-text-template-directives.md).

### <a name="generate-many-files-from-one-model-schema"></a>Gerar muitos arquivos de esquema de um modelo
 Se você geralmente pode gerar arquivos de modelos que têm o mesmo esquema XML ou banco de dados:

-   Considere a possibilidade de escrever um processador de diretriz. Isso permite que você substitua várias instruções de assembly e importar instruções em cada modelo com uma única diretiva personalizada. O processador de diretriz pode também carregar e analisar o arquivo de modelo. Para obter mais informações, consulte [criando processadores diretiva de modelo de texto do personalizado T4](../modeling/creating-custom-t4-text-template-directive-processors.md).

### <a name="generate-files-from-a-complex-model"></a>Gerar arquivos de um modelo complexo

-   Considere a criação de uma linguagem específica de domínio (DSL) para representar o modelo. Isso torna muito mais fácil escrever os modelos, porque você usa tipos e propriedades que refletem os nomes dos elementos no seu modelo. Não é preciso analisar o arquivo ou navegar em nós XML. Por exemplo:

     `foreach (Book book in this.Library) { ... }`

     Para obter mais informações, consulte [Introdução às linguagens específicas de domínio](../modeling/getting-started-with-domain-specific-languages.md) e [código de geração de uma linguagem específica do domínio](../modeling/generating-code-from-a-domain-specific-language.md).

### <a name="get-data-from-visual-studio"></a>Obter dados do Visual Studio
 Para usar os serviços fornecidos no Visual Studio, por conjunto de `hostSpecific` atributo e carga a `EnvDTE` assembly. Por exemplo:

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#
  IServiceProvider serviceProvider = (IServiceProvider)this.Host;
  EnvDTE.DTE dte = (EnvDTE.DTE) serviceProvider.GetService(typeof(EnvDTE.DTE));
#>

Number of projects in this VS solution:  <#= dte.Solution.Projects.Count #>
```

### <a name="execute-text-templates-in-the-build-process"></a>Modelos de texto são executados no processo de compilação

-   Para obter mais informações, consulte [geração de código em um processo de compilação](../modeling/code-generation-in-a-build-process.md).

## <a name="more-general-questions"></a>Perguntas gerais mais

### <a name="starting"></a> O que é a melhor maneira de começar a escrever um modelo de texto?

1.  Escreva um exemplo específico do arquivo gerado.

2.  Transformá-lo em um modelo de texto inserindo o `<#@template #>` diretiva e a diretivas e o código que são necessárias para carregar o arquivo de entrada ou modelo.

3.  Progressivamente substitua partes do arquivo com a expressão e blocos de código.

### <a name="what-is-a-model"></a>O que é um "modelo"?

-   A entrada lida pelo seu modelo. É possível em um arquivo ou em um banco de dados. Pode ser um modelo UML ou um desenho do Visio, ou uma linguagem específica de domínio (DSL) ou XML, ou pode ser texto sem formatação. Ele poderia ser distribuído em vários arquivos. Normalmente, mais de um modelo lê um modelo.

     A implicação do termo "modelo" é que ele representa algum aspecto do seu negócio mais diretamente que o código de programa gerado ou outros arquivos. Por exemplo, ele pode representar o plano de uma rede de comunicação que seu software gerado será supervisionar.

### <a name="what-is-the-benefit-of-using-text-templates"></a>O que é a vantagem de usar modelos de texto?
 Normalmente, você gerar vários código ou outros arquivos de um modelo. O modelo representa os requisitos mais diretamente o código gerado. Ele omite o detalhe de implementação e é gravado em termos de requisitos, em vez do código. Quando os requisitos mudam – como geralmente fazem - você pode atualizar o modelo de forma mais fácil e mais confiável do que as diferentes partes do código do programa.

 Geração de código, portanto, é uma ferramenta valiosa da perspectiva de métodos de desenvolvimento do agile.

### <a name="what-best-practices-are-there-for-text-templates"></a>O que "práticas recomendadas" há para modelos de texto?

-   Para obter mais informações, consulte [diretrizes para modelos de texto T4 escrita](../modeling/guidelines-for-writing-t4-text-templates.md).

### <a name="what-is-t4"></a>O que é "T4"?

-   Outro nome para os recursos de modelo de texto do Visual Studio descrito aqui. A versão anterior, o que não foi publicada, foi uma abreviação de "Transformação de modelo de texto".
