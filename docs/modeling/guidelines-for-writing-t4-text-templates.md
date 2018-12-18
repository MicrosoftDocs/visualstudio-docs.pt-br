---
title: Diretrizes para escrever modelos de texto T4
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 09ed896c85807da5a65084360fa62e24c3cca141
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49896205"
---
# <a name="guidelines-for-writing-t4-text-templates"></a>Diretrizes para escrever modelos de texto T4
Estas diretrizes gerais podem ser úteis se você estiver gerando o código do programa ou outros recursos de aplicativo no Visual Studio. Eles não são fixos regras.

## <a name="guidelines-for-design-time-t4-templates"></a>Diretrizes para os modelos T4 em tempo de Design
 Modelos do T4 em tempo de design são modelos que geram o código em seu projeto do Visual Studio em tempo de design. Para obter mais informações, consulte [geração de código de tempo de Design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md).

 Gere variável aspectos do aplicativo.
Geração de código é mais útil para os aspectos do aplicativo que pode ser alterada durante o projeto, ou será alterado entre versões diferentes do aplicativo. Separe esses aspectos variável dos aspectos mais invariáveis para que você possa determinar mais facilmente o que precisa ser gerado. Por exemplo, se seu aplicativo oferece um site, separe a página padrão que atende a funções da lógica que define os caminhos de navegação de uma página para outra.

 Codifica os aspectos de variável em um ou mais modelos de origem.
Um modelo é um arquivo ou banco de dados que lê de cada modelo para obter valores específicos para as partes variáveis do código que deve ser gerado. Modelos podem ser bancos de dados, arquivos XML de seu próprio design, diagramas ou linguagens específicas de domínio. Normalmente, um modelo é usado para gerar vários arquivos em um projeto do Visual Studio. Cada arquivo é gerado a partir de um modelo separado.

 Você pode usar mais de um modelo em um projeto. Por exemplo, você pode definir um modelo para a navegação entre páginas da web e um modelo separado para o layout das páginas.

 Concentre-se o modelo nas necessidades dos usuários e o vocabulário, não em sua implementação.
Por exemplo, um aplicativo do site, você esperaria o modelo para se referir a páginas da web e hiperlinks.

 Idealmente, escolha um formulário de apresentação que adequado para o tipo de informação que representa o modelo. Por exemplo, um modelo de caminhos de navegação por meio de um site da Web poderia ser um diagrama das caixas e setas.

 Teste o código gerado.
Use testes manuais ou automatizados para verificar se o código resultante funciona conforme os usuários precisam. Evite a geração de testes do mesmo modelo do qual o código é gerado.

 Em alguns casos, os testes gerais podem ser executados no modelo diretamente. Por exemplo, você poderia escrever um teste que garante que todas as páginas no site podem ser alcançada pela navegação de qualquer outro.

 Permitir código personalizado: gerar classes parciais.
Permitir código que você escrever à mão além para o código gerado. É incomum para um esquema de geração de código para ser capaz de levar em conta todas as variações possíveis que podem surgir. Portanto, você deve esperar adicionar ou substituir algumas do código gerado. Em que o material gerado está em uma linguagem .NET, como [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] ou [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)], duas estratégias são especialmente úteis:

- As classes geradas devem ser parciais. Isso permite que você adicione conteúdo para o código gerado.

- As classes devem ser geradas em pares, um herdar de outra. A classe base deve conter todas as propriedades e métodos gerados, e a classe derivada deve conter somente os construtores. Isso permite que seu código escrito manualmente substituir qualquer um dos métodos gerados.

  Em outras linguagens geradas como XML, use o `<#@include#>` diretiva para tornar simples combinações de conteúdo escrito manualmente e gerado. Em casos mais complexos, você talvez precise escrever uma etapa de pós-processamento que combina o arquivo gerado com todos os arquivos gravados para à mão.

  Mover o material comum em arquivos de inclusão ou modelos de tempo de execução para evitar a repetição semelhantes blocos de texto e código em vários modelos, usam o `<#@ include #>` diretiva. Para obter mais informações, consulte [diretiva Include do T4](../modeling/t4-include-directive.md).

  Você pode também criar modelos de texto de tempo de execução em um projeto separado e, em seguida, chamá-los a partir do modelo de tempo de design. Para fazer isso, use o `<#@ assembly #>` diretiva para acessar o projeto separado. Para obter exemplos, consulte ["Herança em modelos de texto" no Blog de Gareth Jones](http://go.microsoft.com/fwlink/?LinkId=208373).

  Considere mover grandes blocos de código em um assembly separado.
  Se você tiver blocos de código grande e blocos de recurso de classe, pode ser útil mover alguns desse código em métodos que são compilados em um projeto separado. Você pode usar o `<#@ assembly #>` diretiva para acessar o código no modelo. Para obter mais informações, consulte [diretiva de Assembly T4](../modeling/t4-assembly-directive.md).

  Você pode colocar os métodos em uma classe abstrata que o modelo pode herdar. A classe abstrata deve herdar de <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation?displayProperty=fullName>. Para obter mais informações, consulte [diretiva de modelo T4](../modeling/t4-template-directive.md).

  Gerar código, não arquivos um método de configuração de escrever um aplicativo de variável é escrever um código de programa genérico que aceita um arquivo de configuração. Um aplicativo escrito dessa maneira é muito flexível e pode ser reconfigurado quando os requisitos de negócios mudam, sem recompilar o aplicativo. No entanto, uma desvantagem dessa abordagem é que o aplicativo será um desempenho inferior que um aplicativo mais específico. Além disso, seu código do programa será mais difícil de ler e manter, em parte porque ele sempre tem de lidar com os tipos mais genéricos.

  Por outro lado, um aplicativo cujas partes variáveis são gerados antes da compilação pode ser fortemente tipado. Isso torna muito mais fácil e mais confiáveis para escrever código escrito manualmente e integrá-lo com o gerado partes do software.

  Para obter todos os benefícios de geração de código, tente gerar o código do programa, em vez de arquivos de configuração.

  Use uma pasta de código gerados coloque os modelos e os arquivos gerados em uma pasta de projeto chamada **código gerado pelo**, para torná-lo limpar que esses não são arquivos que devem ser editados diretamente. Se você criar código personalizado para substituir ou adicionar a classes geradas, coloque essas classes em uma pasta denominada **código personalizado**. A estrutura de um projeto típico tem esta aparência:

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

## <a name="guidelines-for-run-time-preprocessed-t4-templates"></a>Diretrizes para modelos T4 de tempo de execução (pré-processado)
 Mover o material comum em modelos herdados, você pode usar herança para compartilhar os métodos e blocos de texto entre modelos de texto T4. Para obter mais informações, consulte [diretiva de modelo T4](../modeling/t4-template-directive.md).

 Você também pode usar incluem arquivos com modelos de tempo de execução.

 Mova grandes corpos de código em uma classe parcial.
Cada modelo de tempo de execução gera uma definição de classe parcial que tem o mesmo nome que o modelo. Você pode escrever um arquivo de código que contém outra definição parcial da mesma classe. Você pode adicionar os construtores, campos e métodos à classe dessa maneira. Esses membros podem ser chamados de blocos de código no modelo.

 Uma vantagem de fazer isso é que o código é mais fácil de escrever, porque o IntelliSense está disponível. Além disso, você pode obter uma separação melhor entre a apresentação e a lógica subjacente.

 Por exemplo, na **MyReportText.tt**:

 `The total is: <#= ComputeTotal() #>`

 Na **MyReportText Methods.cs**:

 `private string ComputeTotal() { ... }`

 Permitir código personalizado: fornecer pontos de extensão métodos virtuais geração de considere em \<bloqueia o recurso de classe #+ #>. Isso permite que um único modelo a ser usado em muitos contextos sem modificação. Em vez de modificar o modelo, você pode construir uma classe derivada que fornece a lógica adicional mínima. A classe derivada pode ser qualquer código regular, ou pode ser um modelo de tempo de execução.

 Por exemplo, no MyStandardRunTimeTemplate.tt:

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
 Coleta de dados separada da geração de texto tentar evitar a mistura de computação e blocos de texto. Em cada modelo de texto, use a primeira \<bloquear o código de # #> para definir as variáveis e executar cálculos complexos. Do primeiro bloco de texto até o fim do modelo ou a primeira \<bloquear o recurso de classe #+ #>, evite expressões longas e evitar loops e condicionais, a menos que eles contêm blocos de texto. Essa prática torna o modelo mais fácil de ler e manter.

 Não use `.tt` para incluir arquivos usam uma extensão de nome de arquivo diferente, como `.ttinclude` para arquivos de inclusão. Use `.tt` apenas nos arquivos que você deseja ser processados como tempo de execução ou tempo de design de modelos de texto. Em alguns casos, o Visual Studio reconhece `.tt` arquivos e define automaticamente suas propriedades para processamento.

 Cada modelo de início como um protótipo fixado.
Escreva um exemplo do código ou texto que você deseja gerar e certifique-se de que ele está correto. Em seguida, alterar sua extensão para. TT e inserir o código que modifica o conteúdo ao ler o modelo de forma incremental.

 Considere o uso de modelos com tipo.
Embora você possa criar um esquema XML ou banco de dados para seus modelos, pode ser útil criar uma linguagem específica de domínio (DSL). Uma DSL tem a vantagem que ele gera uma classe para representar cada nó no esquema e propriedades para representar os atributos. Isso significa que você pode programar em termos do modelo de negócios. Por exemplo:

```
Team Members:
<# foreach (Person p in team.Members)
 { #>
    <#= p.Name #>
<# } #>
```

 Considere o uso de diagramas para seus modelos.
Muitos modelos com mais eficiência são apresentados e gerenciados simplesmente como tabelas de texto, especialmente se eles forem muito grandes.

 No entanto, para alguns tipos de requisitos de negócios, é importante esclarecer conjuntos complexos de relações e fluxos de trabalho e os diagramas são o melhor meio adequado. Uma vantagem de um diagrama é que é fácil discutir com os usuários e outros participantes. Gerando o código de um modelo no nível de requisitos de negócios, você torna seu código mais flexível quando os requisitos são alterados.

 Você também pode criar seu próprio tipo de diagrama como uma linguagem específica de domínio (DSL). Código pode ser gerado a partir de UML e DSLs. Para obter mais informações, consulte [análise e modelagem de arquitetura](../modeling/analyze-and-model-your-architecture.md).

## <a name="see-also"></a>Consulte também

- [Geração de código no tempo de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md)
- [Geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md)
