---
title: 'Instruções passo a passo: gerenciando código usando modelos de texto'
description: Saiba que a geração de código permite que você produza um código de programa fortemente digitado e que ainda possa ser alterado facilmente quando o modelo de origem for alterado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- walkthroughs [text templates], generating application code
- walkthroughs [text templates]
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 22940fb86ab0cfd7262a3ca7845521847add2dff
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388120"
---
# <a name="walkthrough-generate-code-by-using-text-templates"></a>Passo a passo: gerar código usando modelos de texto

A geração de código permite que você produza um código de programa fortemente digitado e que ainda possa ser alterado facilmente quando o modelo de origem for alterado. Contraste isso com a técnica alternativa de escrever um programa completamente genérico que aceita um arquivo de configuração, que é mais flexível, mas resulta em código que não é tão fácil de ler e alterar, nem tem um desempenho tão bom. Este passo a passo demonstra esse benefício.

## <a name="typed-code-for-reading-xml"></a>Código digitado para ler XML

O System.Xml namespace fornece ferramentas abrangentes para carregar um documento XML e, em seguida, navegá-lo livremente na memória. Infelizmente, todos os nós têm o mesmo tipo, XmlNode. Portanto, é muito fácil cometer erros de programação, como esperar o tipo errado de nó filho ou os atributos errados.

Neste projeto de exemplo, um modelo lê um arquivo XML de exemplo e gera classes que correspondem a cada tipo de nó. No código escrito manualmente, você pode usar essas classes para navegar no arquivo XML. Você também pode executar seu aplicativo em qualquer outro arquivo que use os mesmos tipos de nó. A finalidade do arquivo XML de exemplo é fornecer exemplos de todos os tipos de nó com os quais você deseja lidar com seu aplicativo.

> [!NOTE]
> O aplicativo [xsd.exe](/dotnet/standard/serialization/xml-schema-definition-tool-xsd-exe), que está incluído no Visual Studio, pode gerar classes fortemente digitados de arquivos XML. O modelo mostrado aqui é fornecido como um exemplo.

Este é o arquivo de exemplo:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<catalog>
  <artist id ="Mike%20Nash" name="Mike Nash Quartet">
    <song id ="MikeNashJazzBeforeTeatime">Jazz Before Teatime</song>
    <song id ="MikeNashJazzAfterBreakfast">Jazz After Breakfast</song>
  </artist>
  <artist id ="Euan%20Garden" name="Euan Garden">
    <song id ="GardenScottishCountry">Scottish Country Garden</song>
  </artist>
</catalog>
```

No projeto que este passo a passo constrói, você pode escrever código como o seguinte e o IntelliSense solicita o atributo e os nomes filho corretos conforme você digita:

```csharp
Catalog catalog = new Catalog(xmlDocument);
foreach (Artist artist in catalog.Artist)
{
  Console.WriteLine(artist.name);
  foreach (Song song in artist.Song)
  {
    Console.WriteLine("   " + song.Text);
  }
}
```

Contraste isso com o código sem tipo que você pode escrever sem o modelo:

```csharp
XmlNode catalog = xmlDocument.SelectSingleNode("catalog");
foreach (XmlNode artist in catalog.SelectNodes("artist"))
{
    Console.WriteLine(artist.Attributes["name"].Value);
    foreach (XmlNode song in artist.SelectNodes("song"))
    {
         Console.WriteLine("   " + song.InnerText);
     }
}
```

Na versão fortemente digitada, uma alteração no esquema XML resulta em alterações nas classes. O compilador realça as partes do código do aplicativo que devem ser alteradas. Na versão sem tipo que usa código XML genérico, não há esse suporte.

Neste projeto, um único arquivo de modelo é usado para gerar as classes que possibilitam a versão digitada.

## <a name="set-up-the-project"></a>Configurar o projeto

### <a name="create-or-open-a-c-project"></a>Criar ou abrir um projeto em C#

Você pode aplicar essa técnica a qualquer projeto de código. Este passo a passo usa um projeto C# e, para fins de teste, usamos um aplicativo de console.

1. No menu **Arquivo** , clique **em Novo** e, em seguida, clique **em Projeto**.

2. Clique no **nó Visual C#** e, no painel **Modelos,** clique em **Aplicativo de Console.**

### <a name="add-a-prototype-xml-file-to-the-project"></a>Adicionar um arquivo XML de protótipo ao projeto

A finalidade desse arquivo é fornecer exemplos dos tipos de nó XML que você deseja que seu aplicativo possa ler. Pode ser um arquivo que será usado para testar seu aplicativo. O modelo produzirá uma classe C# para cada tipo de nó nesse arquivo.

O arquivo deve fazer parte do projeto para que o modelo possa lê-lo, mas não será integrado ao aplicativo compilado.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto, clique **em Adicionar** e em Novo **Item**.

2. Na caixa de diálogo Adicionar Novo **Item,** selecione **Arquivo XML** no **painel** Modelos.

3. Adicione o conteúdo de exemplo ao arquivo.

4. Para este passo a passo, nomeia o arquivo `exampleXml.xml` . De definir o conteúdo do arquivo como o XML mostrado na seção anterior.

### <a name="add-a-test-code-file"></a>Adicionar um arquivo de código de teste

Adicione um arquivo C# ao seu projeto e escreva nele um exemplo do código que você deseja poder escrever. Por exemplo:

```csharp
using System;
namespace MyProject
{
  class CodeGeneratorTest
  {
    public void TestMethod()
    {
      Catalog catalog = new Catalog(@"..\..\exampleXml.xml");
      foreach (Artist artist in catalog.Artist)
      {
        Console.WriteLine(artist.name);
        foreach (Song song in artist.Song)
        {
          Console.WriteLine("   " + song.Text);
} } } } }
```

Neste estágio, esse código não será compilado. Ao escrever o modelo, você gerará classes que permitem que ele seja bem-sucedido.

Um teste mais abrangente pode verificar a saída dessa função de teste em relação ao conteúdo conhecido do arquivo XML de exemplo. Mas neste passo a passo, vamos ser atendidos quando o método de teste for compilado.

### <a name="add-a-text-template-file"></a>Adicionar um arquivo de modelo de texto

Adicione um arquivo de modelo de texto e de definir a extensão de saída *como .cs.*

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto, clique **em Adicionar** e em Novo **Item**.

2. Na caixa de diálogo Adicionar Novo **Item,** selecione **Modelo de** Texto **no painel** Modelos.

    > [!NOTE]
    > Certifique-se de adicionar um Modelo de Texto e não um Modelo de Texto Pré-processado.

3. No arquivo, na diretiva de modelo, altere o `hostspecific` atributo para `true` .

     Essa alteração permitirá que o código do modelo obtenha acesso aos Visual Studio serviços.

4. Na diretiva de saída, altere o atributo de extensão para ".cs", para que o modelo gere um arquivo C#. Em um Visual Basic, você o alteraria para ".vb".

5. Salve o arquivo. Neste estágio, o arquivo de modelo de texto deve conter estas linhas:

    ```
    <#@ template debug="false" hostspecific="true" language="C#" #>
    <#@ output extension=".cs" #>
    ```

Observe que um arquivo .cs aparece Gerenciador de Soluções como uma subsidiária do arquivo de modelo. Você pode vê-lo clicando em [+] ao lado do nome do arquivo de modelo. Esse arquivo é gerado do arquivo de modelo sempre que você salva ou move o foco para fora do arquivo de modelo. O arquivo gerado será compilado como parte do seu projeto.

Para sua conveniência enquanto desenvolve o arquivo de modelo, organize as janelas do arquivo de modelo e o arquivo gerado para que você possa vê-los ao lado uns dos outros. Isso permite que você veja imediatamente a saída do modelo. Você também observará que, quando o modelo gerar um código C# inválido, os erros aparecerão na janela da mensagem de erro.

Todas as edições que você executar diretamente no arquivo gerado serão perdidas sempre que você salvar o arquivo de modelo. Portanto, você deve evitar editar o arquivo gerado ou editá-lo somente para experimentos curtos. Às vezes, é útil tentar um pequeno fragmento de código no arquivo gerado, em que o IntelliSense está em operação e, em seguida, copiá-lo para o arquivo de modelo.

## <a name="develop-the-text-template"></a>Desenvolver o modelo de texto

Seguindo as melhores orientações sobre o desenvolvimento agile, desenvolveremos o modelo em pequenas etapas, limpando alguns dos erros em cada incremento, até que o código de teste seja compilado e executado corretamente.

### <a name="prototype-the-code-to-be-generated"></a>Protótipo do código a ser gerado

O código de teste requer uma classe para cada nó no arquivo. Portanto, alguns dos erros de compilação desaparecerão se você anexar essas linhas ao modelo e, em seguida, salvá-lo:

```csharp
class Catalog {}
class Artist {}
class Song {}
```

Isso ajuda você a ver o que é necessário, mas as declarações devem ser geradas dos tipos de nó no arquivo XML de exemplo. Exclua essas linhas experimentais do modelo.

### <a name="generate-application-code-from-the-model-xml-file"></a>Gerar código do aplicativo do arquivo XML do modelo

Para ler o arquivo XML e gerar declarações de classe, substitua o conteúdo do modelo pelo seguinte código de modelo:

```
<#@ template debug="false" hostspecific="true" language="C#" #>
<#@ output extension=".cs" #>
<#@ assembly name="System.Xml"#>
<#@ import namespace="System.Xml" #>
<#
 XmlDocument doc = new XmlDocument();
 // Replace this file path with yours:
 doc.Load(@"C:\MySolution\MyProject\exampleXml.xml");
 foreach (XmlNode node in doc.SelectNodes("//*"))
 {
#>
  public partial class <#= node.Name #> {}
<#
 }
#>
```

Substitua o caminho do arquivo pelo caminho correto para seu projeto.

Observe que o bloco de código delimita `<#...#>` . Esses delimitadores colchetes de um fragmento do código do programa que gera o texto. O bloco de expressão delimita um colchete `<#=...#>` de uma expressão que pode ser avaliada como uma cadeia de caracteres.

Ao escrever um modelo que gera o código-fonte para seu aplicativo, você está lidando com dois textos de programa separados. O programa dentro dos delimitadores de bloco de código é executado sempre que você salva o modelo ou move o foco para outra janela. O texto gerado, que aparece fora dos delimitadores, é copiado para o arquivo gerado e se torna parte do código do aplicativo.

A `<#@assembly#>` diretiva se comporta como uma referência, disponibilizando o assembly para o código de modelo. A lista de assemblies vistos pelo modelo é separada da lista de Referências no projeto de aplicativo.

A `<#@import#>` diretiva atua como uma instrução , permitindo que você use os nomes `using` curtos de classes no namespace importado.

Infelizmente, embora esse modelo gere código, ele produz uma declaração de classe para cada nó no arquivo XML de exemplo, de modo que, se houver várias instâncias do nó, várias declarações da música de classe `<song>` serão exibidas.

### <a name="read-the-model-file-then-generate-the-code"></a>Leia o arquivo de modelo e, em seguida, gere o código

Muitos modelos de texto seguem um padrão no qual a primeira parte do modelo lê o arquivo de origem e a segunda parte gera o modelo. Precisamos ler todo o arquivo de exemplo para resumir os tipos de nó que ele contém e, em seguida, gerar as declarações de classe. Outro `<#@import#>` é necessário para que possamos usar `Dictionary<>:`

```
<#@ template debug="false" hostspecific="true" language="C#" #>
<#@ output extension=".cs" #>
<#@ assembly name="System.Xml"#>
<#@ import namespace="System.Xml" #>
<#@ import namespace="System.Collections.Generic" #>
<#
 // Read the model file
 XmlDocument doc = new XmlDocument();
 doc.Load(@"C:\MySolution\MyProject\exampleXml.xml");
 Dictionary <string, string> nodeTypes =
        new Dictionary<string, string>();
 foreach (XmlNode node in doc.SelectNodes("//*"))
 {
   nodeTypes[node.Name] = "";
 }
 // Generate the code
 foreach (string nodeName in nodeTypes.Keys)
 {
#>
  public partial class <#= nodeName #> {}
<#
 }
#>
```

### <a name="add-an-auxiliary-method"></a>Adicionar um método auxiliar

Um bloco de controle de recursos de classe é um bloco no qual você pode definir métodos auxiliares. O bloco é delimitado por `<#+...#>` e deve aparecer como o último bloco no arquivo.

Se preferir que os nomes de classe comecem com uma letra maiúscula, você poderá substituir a última parte do modelo pelo seguinte código de modelo:

```
// Generate the code
 foreach (string nodeName in nodeTypes.Keys)
 {
#>
  public partial class <#= UpperInitial(nodeName) #> {}
<#
 }
#>
<#+
 private string UpperInitial(string name)
 { return name[0].ToString().ToUpperInvariant() + name.Substring(1); }
#>
```

Neste estágio, o arquivo *.cs* gerado contém as seguintes declarações:

```csharp
public partial class Catalog {}
public partial class Artist {}
public partial class Song {}
```

Mais detalhes, como propriedades para os nós filho, atributos e texto interno, podem ser adicionados usando a mesma abordagem.

### <a name="access-the-visual-studio-api"></a>Acessar a API Visual Studio dados

Definir o `hostspecific` atributo da diretiva permite que o modelo obtenha acesso à API `<#@template#>` Visual Studio. O modelo pode usar isso para obter o local dos arquivos de projeto, a fim de evitar o uso de um caminho de arquivo absoluto no código do modelo.

```
<#@ template debug="false" hostspecific="true" language="C#" #>
...
<#@ assembly name="EnvDTE" #>
...
EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)
                       .GetService(typeof(EnvDTE.DTE));
// Open the prototype document.
XmlDocument doc = new XmlDocument();
doc.Load(System.IO.Path.Combine(dte.ActiveDocument.Path, "exampleXml.xml"));
```

## <a name="complete-the-text-template"></a>Concluir o modelo de texto

O conteúdo do modelo a seguir gera código que permite que o código de teste seja compilado e executado.

```
<#@ template debug="false" hostspecific="true" language="C#" #>
<#@ output extension=".cs" #>
<#@ assembly name="System.Xml" #>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="System.Xml" #>
<#@ import namespace="System.Collections.Generic" #>
using System;using System.Collections.Generic;using System.Linq;using System.Xml;namespace MyProject{
<#
 // Map node name --> child name --> child node type
 Dictionary<string, Dictionary<string, XmlNodeType>> nodeTypes = new Dictionary<string, Dictionary<string, XmlNodeType>>();

 // The Visual Studio host, to get the local file path.
 EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)
                       .GetService(typeof(EnvDTE.DTE));
 // Open the prototype document.
 XmlDocument doc = new XmlDocument();
 doc.Load(System.IO.Path.Combine(dte.ActiveDocument.Path, "exampleXml.xml"));
 // Inspect all the nodes in the document.
 // The example might contain many nodes of the same type,
 // so make a dictionary of node types and their children.
 foreach (XmlNode node in doc.SelectNodes("//*"))
 {
   Dictionary<string, XmlNodeType> subs = null;
   if (!nodeTypes.TryGetValue(node.Name, out subs))
   {
     subs = new Dictionary<string, XmlNodeType>();
     nodeTypes.Add(node.Name, subs);
   }
   foreach (XmlNode child in node.ChildNodes)
   {
     subs[child.Name] = child.NodeType;
   }
   foreach (XmlNode child in node.Attributes)
   {
     subs[child.Name] = child.NodeType;
   }
 }
 // Generate a class for each node type.
 foreach (string className in nodeTypes.Keys)
 {
    // Capitalize the first character of the name.
#>
    partial class <#= UpperInitial(className) #>
    {      private XmlNode thisNode;      public <#= UpperInitial(className) #>(XmlNode node)       { thisNode = node; }

<#
    // Generate a property for each child.
    foreach (string childName in nodeTypes[className].Keys)
    {
      // Allow for different types of child.
      switch (nodeTypes[className][childName])
      {
         // Child nodes:
         case XmlNodeType.Element:
#>
      public IEnumerable<<#=UpperInitial(childName)#>><#=UpperInitial(childName) #>      {         get         {            foreach (XmlNode node in                thisNode.SelectNodes("<#=childName#>"))              yield return new <#=UpperInitial(childName)#>(node);       } }
<#
         break;
         // Child attributes:
         case XmlNodeType.Attribute:
#>
      public string <#=childName #>      { get { return thisNode.Attributes["<#=childName#>"].Value; } }
<#
         break;
         // Plain text:
         case XmlNodeType.Text:
#>
      public string Text  { get { return thisNode.InnerText; } }
<#
         break;
       } // switch
     } // foreach class child
  // End of the generated class:
#>
   }
<#
 } // foreach class

   // Add a constructor for the root class
   // that accepts an XML filename.
   string rootClassName = doc.SelectSingleNode("*").Name;
#>
   partial class <#= UpperInitial(rootClassName) #>   {      public <#= UpperInitial(rootClassName) #>(string fileName){        XmlDocument doc = new XmlDocument();        doc.Load(fileName);        thisNode = doc.SelectSingleNode("<#=rootClassName#>");}   }}
<#+
   private string UpperInitial(string name)
   {
      return name[0].ToString().ToUpperInvariant() + name.Substring(1);
   }
#>
```

### <a name="run-the-test-program"></a>Executar o programa de teste

Na principal do aplicativo de console, as linhas a seguir executarão o método de teste. Pressione F5 para executar o programa no modo de depuração:

```csharp
using System;
namespace MyProject
{
  class Program
  {
    static void Main(string[] args)
    {
      new CodeGeneratorTest().TestMethod();
      // Allow user to see the output:
      Console.ReadLine();
    }
  }
}
```

### <a name="write-and-update-the-application"></a>Gravar e atualizar o aplicativo

O aplicativo agora pode ser escrito em estilo fortemente tipado, usando as classes geradas em vez de usar código XML genérico.

Quando o esquema XML é alterado, novas classes podem ser facilmente geradas. O compilador informará ao desenvolvedor onde o código do aplicativo deve ser atualizado.

Para regenerar as classes quando o arquivo XML de exemplo for alterado, clique em **transformar todos os modelos** na barra de ferramentas **Gerenciador de soluções** .

## <a name="conclusion"></a>Conclusão

Este tutorial demonstra várias técnicas e benefícios da geração de código:

- *Geração de código* é a criação de parte do código-fonte do seu aplicativo a partir de um *modelo*. O modelo contém informações em um formulário adequado ao domínio do aplicativo e pode ser alterado durante o tempo de vida do aplicativo.

- A tipagem forte é um benefício da geração de código. Embora o modelo represente informações em um formulário mais adequado para o usuário, o código gerado permite que outras partes do aplicativo lidem com as informações usando um conjunto de tipos.

- O IntelliSense e o compilador ajudam a criar códigos que aderem ao esquema do modelo, quando você escreve um novo código e quando o esquema é atualizado.

- A adição de um único arquivo de modelo incomplicado a um projeto pode fornecer esses benefícios.

- Um modelo de texto pode ser desenvolvido e testado de forma rápida e incremental.

Neste tutorial, o código do programa é realmente gerado a partir de uma instância do modelo, um exemplo representativo dos arquivos XML que o aplicativo processará. Em uma abordagem mais formal, o esquema XML seria a entrada para o modelo, na forma de um arquivo. xsd ou uma definição de linguagem específica de domínio. Essa abordagem tornaria mais fácil para o modelo determinar características como a multiplicidade de uma relação.

## <a name="troubleshoot-the-text-template"></a>Solucionar problemas do modelo de texto

Se você tiver visto o modelo de transformação ou erros de compilação no **lista de erros**, ou se o arquivo de saída não tiver sido gerado corretamente, você poderá solucionar o problema do modelo de texto com as técnicas descritas em [gerando arquivos com o utilitário TextTransform](../modeling/generating-files-with-the-texttransform-utility.md).

## <a name="see-also"></a>Confira também

- [Geração de código na hora de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md)
- [Gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md)
