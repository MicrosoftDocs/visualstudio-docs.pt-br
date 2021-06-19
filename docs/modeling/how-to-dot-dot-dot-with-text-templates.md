---
title: Como ... com modelos de texto
description: Saiba mais sobre as respostas a perguntas comuns encontradas ao usar modelos de texto para gerar texto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0c65a7ba67c3972620b3d589188e233827a12ffd
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387262"
---
# <a name="how-to--with-text-templates"></a>Como ... com modelos de texto
Os modelos de texto Visual Studio fornecem uma maneira útil de gerar texto de qualquer tipo. Você pode usar modelos de texto para gerar texto em tempo de executar como parte do aplicativo e em tempo de design para gerar parte do código do projeto. Este tópico resume o "Como fazer...?" Perguntas.

 Neste tópico, várias respostas precedidas por marcadores são sugestões alternativas.

 Para uma introdução geral aos modelos de texto, leia [Geração de Código e Modelos de Texto T4](../modeling/code-generation-and-t4-text-templates.md).

## <a name="how-to-"></a>Como...

### <a name="generate-part-of-my-application-code"></a>Gerar parte do código do meu aplicativo
 Tenho uma configuração ou modelo *em* um arquivo ou banco de dados. Uma ou mais partes do meu código dependem desse modelo.

- Gere alguns dos seus arquivos de código de modelos de texto. Para obter mais informações, consulte Geração de código em tempo de design usando modelos de [texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md) e Qual é a melhor maneira de começar [a escrever um modelo?](#starting).

### <a name="generate-files-at-run-time-passing-data-into-the-template"></a>Gerar arquivos em tempo de executar, passando dados para o modelo
 Em tempo de executar, meu aplicativo gera arquivos de texto, como relatórios, que contêm uma combinação de texto e dados padrão. Quero evitar escrever centenas de `write` instruções.

- Adicione um modelo de texto de runtime ao seu projeto. Esse modelo cria uma classe em seu código, que pode ser criada e usada para gerar texto. Você pode passar dados para ele nos parâmetros do construtor. Para obter mais informações, consulte [Geração de texto em tempo de run-time com modelos de](../modeling/run-time-text-generation-with-t4-text-templates.md)texto T4 .

- Se você quiser gerar com base em modelos que estão disponíveis somente em tempo de operação, poderá usar modelos de texto padrão. Se você estiver escrevendo uma extensão Visual Studio, poderá invocar o serviço de emplatação de texto. Para obter mais informações, consulte [Invocando a transformação de texto em uma extensão do VS.](../modeling/invoking-text-transformation-in-a-vs-extension.md) Em outros contextos, você pode usar o mecanismo de emplatação de texto. Para obter mais informações, consulte <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName>.

     Use a \<#@parameter#> diretiva para passar parâmetros para esses modelos. Para obter mais informações, consulte [Diretiva de parâmetro T4](../modeling/t4-parameter-directive.md).

### <a name="read-another-project-file-from-a-template"></a>Ler outro arquivo de projeto de um modelo
 Para ler um arquivo do mesmo projeto Visual Studio que o modelo:

- Insira `hostSpecific="true"` na diretiva `<#@template#>`.

     Em seu código, use `this.Host.ResolvePath(filename)` para obter o caminho completo do arquivo.

### <a name="invoke-methods-from-a-template"></a>Invocar métodos de um modelo

Se os métodos já existirem, por exemplo, em classes .NET:

- Use a \<#@assembly#> diretiva para carregar o assembly e use para definir o contexto do \<#@import#> namespace. Para obter mais informações, consulte [Diretiva de importação T4](../modeling/t4-import-directive.md).

   Se você usar com frequência o mesmo conjunto de diretivas de assembly e importação, considere escrever um processador de diretiva. Em cada modelo, você pode invocar o processador de diretiva, que pode carregar os assemblies e os arquivos de modelo e definir o contexto do namespace. Para obter mais informações, consulte Criando processadores de diretiva de modelo de [texto T4 personalizados.](../modeling/creating-custom-t4-text-template-directive-processors.md)

Se você estiver escrevendo os métodos por si mesmo:

- Se você estiver escrevendo um modelo de texto de runtime, escreva uma definição de classe parcial que tenha o mesmo nome que o modelo de texto de runtime. Adicione os métodos adicionais a essa classe.

- Escreva um bloco de controle de recursos de classe no qual `<#+ ... #>` você pode declarar métodos, propriedades e classes privadas. Quando o modelo de texto é compilado, ele é transformado em uma classe. Os blocos de controle padrão e o texto são transformados em um único método e os blocos de recursos de classe `<#...#>` são inseridos como membros separados. Para obter mais informações, consulte [Blocos de controle de modelo de texto](../modeling/text-template-control-blocks.md).

   Métodos definidos como recursos de classe também podem incluir blocos de texto inseridos.

   Considere colocar recursos de classe em um arquivo separado que você pode `<#@include#>` em um ou mais arquivos de modelo.

- Escreva os métodos em um assembly separado (biblioteca de classes) e chame-os de seu modelo. Use a `<#@assembly#>` diretiva para carregar o assembly e para definir o contexto do `<#@import#>` namespace. Observe que, para recriar o assembly durante a depuração, talvez seja preciso parar e reiniciar Visual Studio. Para obter mais informações, consulte [Diretivas de modelo de](../modeling/t4-text-template-directives.md)texto T4 .

### <a name="generate-many-files-from-one-model-schema"></a>Gerar muitos arquivos de um esquema de modelo
 Se você geralmente gera arquivos de modelos que têm o mesmo esquema XML ou de banco de dados:

- Considere escrever um processador de diretiva. Isso permite que você substitua várias instruções de assembly e instruções de importação em cada modelo por uma única diretiva personalizada. O processador de diretiva também pode carregar e analisar o arquivo de modelo. Para obter mais informações, consulte Criando processadores de diretiva de modelo de [texto T4 personalizados.](../modeling/creating-custom-t4-text-template-directive-processors.md)

### <a name="generate-files-from-a-complex-model"></a>Gerar arquivos de um modelo complexo

- Considere a criação de uma linguagem específica do domínio (DSL) para representar o modelo. Isso torna muito mais fácil escrever os modelos, pois você usa tipos e propriedades que refletem os nomes dos elementos em seu modelo. Você não precisa analisar o arquivo nem navegar por nós XML. Por exemplo:

     `foreach (Book book in this.Library) { ... }`

     Para obter mais informações, [consulte Ponto de Partida com linguagens Domain-Specific e](../modeling/getting-started-with-domain-specific-languages.md) [Gerando código de uma linguagem Domain-Specific .](../modeling/generating-code-from-a-domain-specific-language.md)

### <a name="get-data-from-visual-studio"></a>Obter dados de Visual Studio
 Para usar os serviços fornecidos Visual Studio, de acordo com o `hostSpecific` atributo e carregue o `EnvDTE` assembly. Por exemplo:

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

### <a name="execute-text-templates-in-the-build-process"></a>Executar modelos de texto no processo de build

- Para obter mais informações, consulte [Geração de código em um processo de build](../modeling/code-generation-in-a-build-process.md).

## <a name="more-general-questions"></a>Perguntas mais gerais

### <a name="what-is-the-best-way-to-start-writing-a-text-template"></a><a name="starting"></a> Qual é a melhor maneira de começar a escrever um modelo de texto?

1. Escreva um exemplo específico do arquivo gerado.

2. Transforme-o em um modelo de texto inserindo a diretiva e as diretivas e o código necessários para carregar o `<#@template #>` arquivo ou modelo de entrada.

3. Substitua progressivamente partes do arquivo por blocos de expressão e código.

### <a name="what-is-a-model"></a>O que é um “modelo”?

- A entrada lida pelo modelo. Ele pode estar em um arquivo ou em um banco de dados. Pode ser XML ou um desenho do Visio ou uma linguagem específica do domínio (DSL), ou um modelo UML ou pode ser texto sem-texto. Ele pode ser distribuído em vários arquivos. Normalmente, mais de um modelo lê um modelo.

     A implicação do termo "modelo" é que ele representa algum aspecto da sua empresa mais diretamente do que o código do programa gerado ou outros arquivos. Por exemplo, ele pode representar o plano de uma rede de comunicações que o software gerado vai supervisionar.

### <a name="what-is-the-benefit-of-using-text-templates"></a>Qual é o benefício de usar modelos de texto?
 Normalmente, você gera vários códigos ou outros arquivos de um modelo. O modelo representa os requisitos mais diretamente do que o código gerado. Ele omite detalhes de implementação e é escrito em termos dos requisitos, em vez do código. Quando os requisitos mudam – como geralmente fazem – você pode atualizar o modelo mais facilmente e de forma mais confiável do que as diferentes partes do código do programa.

 A geração de código é, portanto, uma ferramenta valiosa da perspectiva dos métodos de desenvolvimento agile.

### <a name="what-best-practices-are-there-for-text-templates"></a>Quais "práticas recomendadas" existem para modelos de texto?

- Para obter mais informações, consulte [Diretrizes para escrever modelos de texto T4](../modeling/guidelines-for-writing-t4-text-templates.md).

### <a name="what-is-t4"></a>O que é "T4"?

- Outro nome para as Visual Studio de modelo de texto descritas aqui. A versão anterior, que não foi publicada, era uma abreviação de "Transformação modelo de texto".
