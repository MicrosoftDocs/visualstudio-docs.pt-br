---
title: Diretrizes para escrever modelos de texto T4
description: Conheça as diretrizes gerais que são úteis se você estiver gerando código de programa ou outros recursos de aplicativo no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4f043e95ef477558028e634bf6b48aded2960ec2
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386651"
---
# <a name="guidelines-for-writing-t4-text-templates"></a>Diretrizes para escrever modelos de texto T4

Essas diretrizes gerais podem ser úteis se você estiver gerando código de programa ou outros recursos de aplicativo no Visual Studio. Elas não são regras fixas.

## <a name="guidelines-for-design-time-t4-templates"></a>Diretrizes para modelos Design-Time T4

Modelos T4 de tempo de design são modelos que geram código em seu projeto do Visual Studio em tempo de design. Para obter mais informações, consulte [geração de código em tempo de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md).

Gere aspectos variáveis do aplicativo.

A geração de código é mais útil para os aspectos do aplicativo que podem ser alterados durante o projeto ou que serão alterados entre versões diferentes do aplicativo. Separe esses aspectos variáveis dos aspectos mais invariáveis para que você possa determinar com mais facilidade o que precisa ser gerado. Por exemplo, se seu aplicativo fornece um site, separe a página padrão que atende às funções da lógica que define os caminhos de navegação de uma página para outra.

Codifique os aspectos variáveis em um ou mais modelos de origem.

Um modelo é um arquivo ou banco de dados que cada modelo lê para obter valores específicos para partes variáveis do código que deve ser gerado. Os modelos podem ser bancos de dados, arquivos XML de seu próprio design, diagramas ou linguagens específicas de domínio. Normalmente, um modelo é usado para gerar muitos arquivos em um projeto do Visual Studio. Cada arquivo é gerado a partir de um modelo separado.

Você pode usar mais de um modelo em um projeto. Por exemplo, você pode definir um modelo para navegação entre páginas da Web e um modelo separado para o layout das páginas.

Concentre o modelo nas necessidades e no vocabulário dos usuários, não em sua implementação.

Por exemplo, em um aplicativo de site, você espera que o modelo faça referência a páginas da Web e hiperlinks.

Idealmente, escolha uma forma de apresentação que atenda ao tipo de informação que o modelo representa. Por exemplo, um modelo de caminhos de navegação por meio de um site pode ser um diagrama de caixas e setas.

Teste o código gerado.

Use testes manuais ou automatizados para verificar se o código resultante funciona conforme os usuários exigem. Evite gerar testes do mesmo modelo do qual o código é gerado.

Em alguns casos, os testes gerais podem ser executados diretamente no modelo. Por exemplo, você poderia escrever um teste que garanta que cada página no site possa ser acessada pela navegação de qualquer outro.

Permitir código personalizado: gerar classes parciais.

Permita o código que você escreve manualmente, além do código gerado. É incomum que um esquema de geração de código seja capaz de considerar todas as variações possíveis que possam surgir. Portanto, você deve esperar adicionar ou substituir parte do código gerado. Onde o material gerado está em uma linguagem .NET, como C# ou Visual Basic, duas estratégias são especialmente úteis:

- As classes geradas devem ser parciais. Isso permite que você adicione conteúdo ao código gerado.

- As classes devem ser geradas em pares, uma herdada da outra. A classe base deve conter todos os métodos e propriedades gerados, e a classe derivada deve conter apenas os construtores. Isso permite que o código escrito manualmente substitua qualquer um dos métodos gerados.

Em outras linguagens geradas, como XML, use a `<#@include#>` diretiva para fazer combinações simples de conteúdo escrito manualmente e gerado. Em casos mais complexos, talvez seja necessário escrever uma etapa de pós-processamento que combine o arquivo gerado com arquivos escritos manualmente.

Mova o material comum para arquivos de inclusão ou modelos de tempo de execução.

Para evitar a repetição de blocos semelhantes de texto e código em vários modelos, use a `<#@ include #>` diretiva. Para obter mais informações, consulte [diretiva de inclusão T4](../modeling/t4-include-directive.md).

Você também pode criar modelos de texto em tempo de execução em um projeto separado e, em seguida, chamá-los do modelo de tempo de design. Para fazer isso, use a `<#@ assembly #>` diretiva para acessar o projeto separado.

Considere mover grandes blocos de código para um assembly separado.

Se você tiver grandes blocos de código e blocos de recursos de classe, poderá ser útil mover alguns desses códigos para métodos que você compilar em um projeto separado. Você pode usar a `<#@ assembly #>` diretiva para acessar o código no modelo. Para obter mais informações, consulte [diretiva de assembly T4](../modeling/t4-assembly-directive.md).

Você pode colocar os métodos em uma classe abstrata que o modelo pode herdar. A classe abstrata deve herdar de <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation?displayProperty=fullName> . Para obter mais informações, consulte [diretiva de modelo T4](../modeling/t4-template-directive.md).

Gerar código, não arquivos de configuração.

Um método de escrever um aplicativo variável é escrever um código de programa genérico que aceite um arquivo de configuração. Um aplicativo escrito dessa maneira é muito flexível e pode ser reconfigurado quando os requisitos de negócios mudam, sem recompilar o aplicativo. No entanto, uma desvantagem dessa abordagem é que o aplicativo será executado menos bem do que um aplicativo mais específico. Além disso, o código do programa será mais difícil de ler e manter, parcialmente porque ele sempre lida com os tipos mais genéricos.

Por outro lado, um aplicativo cujas partes variáveis são geradas antes que a compilação possa ser fortemente tipada. Isso torna muito mais fácil e mais confiável escrever código escrito à mão e integrá-lo com as partes geradas do software.

Para obter o benefício completo da geração de código, tente gerar o código do programa em vez dos arquivos de configuração.

Use uma pasta de código gerada.

Coloque os modelos e os arquivos gerados em uma pasta de projeto chamada **código gerado**, para deixá-lo claro que esses não são arquivos que devem ser editados diretamente. Se você criar um código personalizado para substituir ou adicionar as classes geradas, coloque essas classes em uma pasta chamada **código personalizado**. A estrutura de um projeto típico tem esta aparência:

```
MyProject
   Custom Code
      Class1.cs
      Class2.cs
   Generated Code
      Class1.tt
          Class1.cs
      Class2.tt
          Class2.cs
   AnotherClass.cs
```

## <a name="guidelines-for-run-time-preprocessed-t4-templates"></a>Diretrizes para modelos T4 de Run-Time (pré-processados)

Mova o material comum para modelos herdados.

Você pode usar a herança para compartilhar métodos e blocos de texto entre modelos de texto T4. Para obter mais informações, consulte [diretiva de modelo T4](../modeling/t4-template-directive.md).

Você também pode usar arquivos de inclusão que têm modelos de tempo de execução.

Mova grandes corpos de código para uma classe parcial.

Cada modelo de tempo de execução gera uma definição de classe parcial que tem o mesmo nome que o modelo. Você pode escrever um arquivo de código que contenha outra definição parcial da mesma classe. Você pode adicionar métodos, campos e construtores à classe dessa maneira. Esses membros podem ser chamados a partir dos blocos de código no modelo.

Uma vantagem de fazer isso é que o código é mais fácil de escrever, pois o IntelliSense está disponível. Além disso, você pode obter uma separação melhor entre a apresentação e a lógica subjacente.

Por exemplo, em **MyReportText.tt**:

`The total is: <#= ComputeTotal() #>`

Em **MyReportText-Methods. cs**:

`private string ComputeTotal() { ... }`

Permitir código personalizado: forneça pontos de extensão.

Considere a geração de métodos virtuais no \<#+ class feature blocks #> . Isso permite que um único modelo seja usado em muitos contextos sem modificação. Em vez de modificar o modelo, você pode construir uma classe derivada que forneça a lógica adicional mínima. A classe derivada pode ser um código regular ou pode ser um modelo de tempo de execução.

Por exemplo, em MyStandardRunTimeTemplate.tt:

```
This page is copyright <#= CompanyName() #>.
<#+ protected virtual string CompanyName() { return ""; } #>
```

No código de um aplicativo:

```
class FabrikamTemplate : MyStandardRunTimeTemplate
{
  protected override string CompanyName() { return "Fabrikam"; }
}
...
  string PageToDisplay = new FabrikamTemplate().TextTransform();
```

## <a name="guidelines-for-all-t4-templates"></a>Diretrizes para todos os modelos T4

Separar a coleta de dados da geração de texto.

Tente evitar misturar blocos de computação e texto. Em cada modelo de texto, use o primeiro \<# code block #> para definir variáveis e executar cálculos complexos. Do primeiro bloco de texto até o final do modelo ou o primeiro \<#+ class feature block #> , evite expressões longas e evite loops e condicionais, a menos que eles contenham blocos de texto. Essa prática torna o modelo mais fácil de ler e manter.

Não use `.tt` para arquivos de inclusão.

Use uma extensão de nome de arquivo diferente, como `.ttinclude` para arquivos de inclusão. Use `.tt` somente para arquivos que você deseja que sejam processados como modelos de texto de tempo de execução ou de tempo de design. Em alguns casos, o Visual Studio reconhece `.tt` arquivos e define automaticamente suas propriedades para processamento.

Inicie cada modelo como um protótipo fixo.

Escreva um exemplo do código ou do texto que você deseja gerar e verifique se ele está correto. Em seguida, altere sua extensão para. tt e insira incrementalmente o código que modifica o conteúdo lendo o modelo.

Considere o uso de modelos tipados.

Embora você possa criar um esquema de banco de dados ou XML para seus modelos, pode ser útil criar uma DSL (linguagem específica de domínio). Uma DSL tem a vantagem de gerar uma classe para representar cada nó no esquema e propriedades para representar os atributos. Isso significa que você pode programar em termos do modelo de negócios. Por exemplo:

```
Team Members:
<# foreach (Person p in team.Members)
 { #>
    <#= p.Name #>
<# } #>
```

Considere o uso de diagramas para seus modelos.

Muitos modelos são apresentados e gerenciados com mais eficiência simplesmente como tabelas de texto, especialmente se eles são muito grandes.

No entanto, para alguns tipos de requisitos de negócios, é importante esclarecer conjuntos complexos de relações e fluxos de trabalho, e os diagramas são a mídia mais adequada. Uma vantagem de um diagrama é que é fácil discutir com usuários e outros stakeholders. Ao gerar código de um modelo no nível dos requisitos de negócios, você torna seu código mais flexível quando os requisitos mudam.

Você também pode criar seu próprio tipo de diagrama como uma linguagem específica do domínio (DSL). O código pode ser gerado de UML e DSLs. Para obter mais informações, consulte [Analisando e modelando arquitetura](../modeling/analyze-and-model-your-architecture.md).

## <a name="see-also"></a>Confira também

- [Geração de código na hora de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md)
- [Geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md)
