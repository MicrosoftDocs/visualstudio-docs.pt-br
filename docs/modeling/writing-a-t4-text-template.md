---
title: Gravando um modelo de texto T4
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, syntax
- text templates, guide
- text templates, functions that generate text
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 0d697f1fed2a7b17862ff4c6f72488674859f754
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50967292"
---
# <a name="writing-a-t4-text-template"></a>Gravando um modelo de texto T4
Um modelo de texto contém o texto que será gerado a partir dele. Por exemplo, um modelo que cria uma página da web conterá "\<html >..." e todas as outras partes padrão de uma página HTML. Inserido no modelo são *blocos de controle*, que são fragmentos de código do programa. Os blocos de controle fornecem valores variáveis​e permitem que partes do texto sejam condicionadas e repetidas.

 Essa estrutura facilita o desenvolvimento de um modelo, porque você pode começar com um protótipo do arquivo gerado e inserir, gradativamente, blocos de controle que variam o resultado.

 Os modelos de texto são compostos das seguintes partes:

-   **Diretivas** -elementos que controlam como o modelo é processado.

-   **Blocos de texto** – conteúdo que é copiado diretamente para a saída.

-   **Blocos de controle** -código de programa que insere valores de variáveis no texto e controla partes condicionais ou repetidas do texto.

Para testar os exemplos neste tópico, copiá-los em um arquivo de modelo conforme descrito em [geração de código de tempo de Design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md). Depois de editar o arquivo de modelo, salvá-lo e, em seguida, inspecione a saída **. txt** arquivo.

## <a name="directives"></a>Diretivas
 As diretivas de modelo de texto fornecem instruções gerais ao mecanismo de modelagem de texto sobre como gerar o código de transformação e o arquivo de saída.

 Por exemplo, a diretiva a seguir especifica que o arquivo de saída deve ter uma extensão .txt:

```
<#@ output extension=".txt" #>
```

 Para obter mais informações sobre diretivas, consulte [diretivas de modelo de texto T4](../modeling/t4-text-template-directives.md).

## <a name="text-blocks"></a>Blocos de texto
 Um bloco de texto insere o texto diretamente no arquivo de saída. Não há formatação especial para os blocos de texto. Por exemplo, o modelo de texto a seguir produzirá um arquivo de texto que contém a palavra "Olá":

```
<#@ output extension=".txt" #>
Hello
```

## <a name="control-blocks"></a>Blocos de controle
 Os blocos de controle são seções de código do programa usadas para transformar os modelos. A linguagem padrão é C#, mas para usar o [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)], você pode escrever essa diretiva no início do arquivo:

```
<#@ template language="VB" #>
```

 A linguagem na qual você escreve o código nos blocos de controle não está relacionada com a linguagem do texto gerado.

### <a name="standard-control-blocks"></a>Blocos de controle padrão
 Um bloco de controle padrão é uma seção do código de programa que gera parte do arquivo de saída.

 Você pode misturar vários blocos de texto e blocos de controle padrão em um arquivo de modelo. No entanto, não é possível colocar um bloco de controle dentro de outro. Cada bloco de controle padrão é delimitado pelos símbolos `<# ... #>`.

 Por exemplo, o seguinte bloco de texto e bloco de controle fazem com que o arquivo de saída contenha a linha "0, 1, 2, 3, 4 Olá!":

```
<#
    for(int i = 0; i < 4; i++)
    {
        Write(i + ", ");
    }
    Write("4");
#> Hello!
```

 Em vez de usar instruções explícitas `Write()`, você pode intercalar texto e código. O exemplo a seguir imprime "Olá!" quatro vezes:

```
<#
    for(int i = 0; i < 4; i++)
    {
#>
Hello!
<#
    }
#>
```

 Você pode inserir um bloco de texto sempre que uma instrução `Write();` for permitida no código.

> [!NOTE]
>  Quando você inserir um bloco de texto dentro de uma instrução composta, como um loop ou condicional, sempre use chaves {...} para conter o bloco de texto.

### <a name="expression-control-blocks"></a>Blocos de controle de expressão
 Um bloco de controle de expressão avalia uma expressão e a converte em uma cadeia de caracteres. Essa cadeia é inserida no arquivo de saída.

 Os blocos de controle de expressão são delimitados pelos símbolos `<#= ... #>`

 Por exemplo, o bloco de controle a seguir faz com que o arquivo de saída contenha "5":

```
<#= 2 + 3 #>
```

 Observe que o símbolo de abertura tem três caracteres "<#=".

 A expressão pode incluir qualquer variável que esteja no escopo. Por exemplo, este bloco imprime linhas com números:

```
<#@ output extension=".txt" #>
<#
    for(int i = 0; i < 4; i++)
    {
#>
This is hello number <#= i+1 #>: Hello!
<#
    }
#>
```

### <a name="class-feature-control-blocks"></a>Blocos de controle de recurso de classe
 Um bloco de controle de recurso de classe define propriedades, métodos ou qualquer outro código que não deveria ser incluído na transformação principal. Os blocos de recurso de classe são usados com frequência para funções auxiliares.  Normalmente, os blocos de recurso de classe são colocados em arquivos separados para que eles possam ser [incluídos](#Include) por mais de um modelo de texto.

 Os blocos de controle de recurso de classe são delimitados pelos símbolos `<#+ ... #>`

 Por exemplo, o arquivo de modelo a seguir declara e usa um método:

```
<#@ output extension=".txt" #>
Squares:
<#
    for(int i = 0; i < 4; i++)
    {
#>
    The square of <#= i #> is <#= Square(i+1) #>.
<#
    }
#>
That is the end of the list.
<#+   // Start of class feature block
private int Square(int i)
{
    return i*i;
}
#>
```

 Os recursos de classe devem ser colocados no final do arquivo em que são gravados. Entretanto, você pode `<#@include#>` um arquivo que contenha um recurso de classe, mesmo que a diretiva `include` seja seguida por blocos de texto comum ou de controle padrão.

 Para obter mais informações sobre os blocos de controle, consulte [blocos de controle de modelo de texto](../modeling/text-template-control-blocks.md).

### <a name="class-feature-blocks-can-contain-text-blocks"></a>Blocos de recurso de classe podem conter blocos de texto
 Você pode gravar um método que gera texto. Por exemplo:

```
List of Squares:
<#
   for(int i = 0; i < 4; i++)
   {  WriteSquareLine(i); }
#>
End of list.
<#+   // Class feature block
private void WriteSquareLine(int i)
{
#>
   The square of <#= i #> is <#= i*i #>.
<#+
}
#>
```

 É particularmente útil usar um método que gera texto em um arquivo separado que pode ser incluído em mais de um modelo.

## <a name="using-external-definitions"></a>Usando definições externas

### <a name="assemblies"></a>Assemblies
 Os blocos de código de seu modelo podem usar tipos definidos como os assemblies .NET usados com mais frequência, tal como um System.dll. Além disso, você pode fazer referência a outros assemblies .NET ou aos seus próprios assemblies. Você pode fornecer um nome de caminho ou o nome forte de um assembly:

```
<#@ assembly name="System.Xml" #>
```

 Você deve usar nomes de caminho absolutos ou nomes de macro padrão no nome do caminho. Por exemplo:

```
<#@ assembly name="$(SolutionDir)library\MyAssembly.dll" #>
```

 A diretiva de assembly não tem nenhum efeito um [modelo de texto pré-processado](../modeling/run-time-text-generation-with-t4-text-templates.md).

 Para obter mais informações, consulte [diretiva de Assembly T4](../modeling/t4-assembly-directive.md).

### <a name="namespaces"></a>Namespaces
 A diretiva de importação é a mesma que a cláusula `using` em C# ou a cláusula `imports` em Visual Basic. Ela permite que você consulte tipos em seu código sem usar um nome totalmente qualificado:

```
<#@ import namespace="System.Xml" #>
```

 Você pode criar quantas diretivas quiser de `assembly` e `import`. Você deve posicioná-las antes de blocos de texto e de controle.

 Para obter mais informações, consulte [diretiva de importação T4](../modeling/t4-import-directive.md).

### <a name="Include"></a> Incluindo código e texto
 A diretiva `include` insere o texto de outro arquivo de modelo. Por exemplo, esta diretiva insere o conteúdo de `test.txt`.

```
<#@ include file="c:\test.txt" #>
```

 O conteúdo incluído é processado quase como se fizesse parte do modelo de texto de inclusão. Entretanto, você pode incluir um arquivo que contenha um bloco de recursos de classe `<#+...#>` mesmo se a diretiva include for seguida por blocos de texto comum ou de controle padrão.

 Para obter mais informações, consulte [diretiva Include do T4](../modeling/t4-include-directive.md).

### <a name="utility-methods"></a>Métodos de utilitários
 Existem vários métodos, tal como `Write()`, que estão sempre disponíveis para você em um bloco de controle. Eles incluem métodos para ajudá-lo a recuar a saída e relatar erros.

 Você pode escrever também seu próprio conjunto de métodos de utilitários.

 Para obter mais informações, consulte [métodos de utilitário de modelo de texto](../modeling/text-template-utility-methods.md).

## <a name="transforming-data-and-models"></a>Transformando dados e modelos
 A aplicação mais útil para um modelo de texto é gerar material com base no conteúdo de uma fonte, tal como um modelo, banco de dados ou arquivo de dados. Seu modelo extrai e formata os dados. Uma coleção de modelos pode transformar essa fonte em vários arquivos.

 Existem várias abordagens para a leitura do arquivo de origem.

 **Ler um arquivo de modelo de texto**. Esta é a maneira mais simples de colocar dados no modelo:

```
<#@ import namespace="System.IO" #>
<# string fileContent = File.ReadAllText(@"C:\myData.txt"); ...
```

 **Carregar um arquivo como um modelo navegável**. Um método mais eficiente é ler os dados como um modelo, pelo qual o código do modelo de texto pode navegar. Por exemplo, você pode carregar um arquivo XML e navegá-lo com expressões XPath. Você também pode usar [xsd.exe](http://go.microsoft.com/fwlink/?LinkId=178765) para criar um conjunto de classes com o qual você pode ler os dados XML.

 **Edite o arquivo de modelo em um diagrama ou formulário.** [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] fornece ferramentas que permitem editar um modelo como um diagrama ou formulário do Windows. Isso facilita discutir o modelo com os usuários do aplicativo gerado. [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] também cria um conjunto de classes fortemente tipado que reflete a estrutura do modelo. Para obter mais informações, consulte [código de geração de uma linguagem específica do domínio](../modeling/generating-code-from-a-domain-specific-language.md).

### <a name="relative-file-paths-in-design-time-templates"></a>Caminhos de arquivo relativos em modelos de tempo de design
 Em um [modelo de texto de tempo de design](../modeling/design-time-code-generation-by-using-t4-text-templates.md), se você quiser referenciar um arquivo em um local relativo ao modelo de texto, use `this.Host.ResolvePath()`. Você também pode definir `hostspecific="true"` na diretiva `template`:

```
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="System.IO" #>
<#
 // Find a path within the same project as the text template:
 string myFile = File.ReadAllText(this.Host.ResolvePath("MyFile.txt"));
#>
Content of MyFile.txt is:
<#= myFile #>
```

Você também pode obter outros serviços fornecidos pelo host. Para obter mais informações, consulte [acessando o Visual Studio ou outros Hosts de um modelo](/previous-versions/visualstudio/visual-studio-2010/gg604090\(v\=vs.100\)).

### <a name="design-time-text-templates-run-in-a-separate-appdomain"></a>Modelos de texto em tempo de design executados em um AppDomain separado

 Você deve estar ciente que uma [modelo de texto de tempo de design](../modeling/design-time-code-generation-by-using-t4-text-templates.md) é executado em um AppDomain separado do aplicativo principal. Na maioria dos casos, isso não é importante, mas você pode descobrir restrições em certos casos complexos. Por exemplo, se você quiser passar dados dentro ou fora do modelo a partir de um serviço separado, o serviço deve fornecer uma API serializável.

 (Isso não é verdadeiro para um [modelo de texto de tempo de execução](../modeling/run-time-text-generation-with-t4-text-templates.md), que fornece o código compilado junto com o restante do seu código.)

## <a name="editing-templates"></a>Editando modelos
 Editores de modelo de texto especializados podem ser baixados da Galeria Online do Gerenciador de Extensões. Sobre o **ferramentas** menu, clique em **Gerenciador de extensões**. Clique em **Galeria Online**e, em seguida, use a ferramenta de pesquisa.

## <a name="related-topics"></a>Tópicos relacionados

|Tarefa|Tópico|
|-|-|
|Gravando um modelo.|[Diretrizes para escrever modelos de texto T4](../modeling/guidelines-for-writing-t4-text-templates.md)|
|Gere texto usando código de programa.|[Estrutura do modelo de texto](../modeling/writing-a-t4-text-template.md)|
|Gere arquivos em uma solução do Visual Studio.|[Geração de código no tempo de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|
|Execute a geração de texto fora do Visual Studio.|[Gerando arquivos com o utilitário TextTransform](../modeling/generating-files-with-the-texttransform-utility.md)|
|Transforme dados na forma de uma linguagem específica do domínio.|[Gerando código com base em uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md)|
|Grave processadores de diretivas para transformar suas próprias fontes de dados.|[Personalizando a transformação de texto T4](../modeling/customizing-t4-text-transformation.md)|
