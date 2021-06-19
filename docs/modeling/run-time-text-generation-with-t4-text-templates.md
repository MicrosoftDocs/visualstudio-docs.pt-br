---
title: Geração de texto de tempo de execução com modelos de texto T4
description: Saiba como você pode gerar cadeias de caracteres de texto em seu aplicativo em tempo de execução usando Visual Studio de texto de runtime.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- Preprocessed Text Template project item
- TextTemplatingFilePreprocessor custom tool
- text templates, TransformText() method
- text templates, generating files at run time
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 96d37bc586f9e8d6134377244c3181a52ec11a84
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387548"
---
# <a name="run-time-text-generation-with-t4-text-templates"></a>Geração de texto de tempo de execução com modelos de texto T4

Você pode gerar cadeias de caracteres de texto em seu aplicativo em tempo de execução usando Visual Studio de texto de runtime. O computador em que o aplicativo é executado não precisa ter Visual Studio. Os modelos de runtime às vezes são chamados de "modelos de texto pré-processadores", pois, em tempo de compilação, o modelo gera código que é executado em tempo de execução.

Cada modelo é uma combinação do texto, pois ele aparecerá na cadeia de caracteres gerada e nos fragmentos do código do programa. Os fragmentos de programa fornecem valores para as partes variáveis da cadeia de caracteres e também controlam partes condicionais e repetidas.

Por exemplo, o modelo a seguir pode ser usado em um aplicativo que cria um relatório HTML.

```html
<#@ template language="C#" #>
<html><body>
<h1>Sales for Previous Month</h2>
<table>
    <# for (int i = 1; i <= 10; i++)
       { #>
         <tr><td>Test name <#= i #> </td>
             <td>Test value <#= i * i #> </td> </tr>
    <# } #>
 </table>
This report is Company Confidential.
</body></html>
```

Observe que o modelo é uma página HTML na qual as partes variáveis foram substituídas pelo código do programa. Você pode começar o design de uma página desse tipo escrevendo um protótipo estático da página HTML. Em seguida, você pode substituir a tabela e outras partes variáveis pelo código do programa que gera o conteúdo que varia de uma ocasião para outra.

Usar um modelo em seu aplicativo torna mais fácil ver a forma final da saída do que você poderia em, por exemplo, uma longa série de instruções de gravação. Fazer alterações na forma da saída é mais fácil e confiável.

## <a name="creating-a-run-time-text-template-in-any-application"></a>Criando um Run-Time de texto em qualquer aplicativo

### <a name="to-create-a-run-time-text-template"></a>Para criar um modelo de texto em tempo de run-time

1. No Gerenciador de Soluções, no menu de atalho do projeto, escolha **Adicionar**  >  **Novo Item**.

2. Na caixa **de diálogo Adicionar Novo Item,** selecione Modelo de Texto em **Runtime**. (Em Visual Basic em Itens **Comuns**  >  **Geral**.)

3. Digite um nome para o arquivo de modelo.

    > [!NOTE]
    > O nome do arquivo de modelo será usado como um nome de classe no código gerado. Portanto, ele não deve ter espaços ou pontuação.

4. Escolha **Adicionar**.

    Um novo arquivo é criado com a extensão **.tt**. Sua **propriedade Ferramenta** Personalizada é definida como **TextTemplatingFilePreprocessor**. Ele contém as seguintes linhas:

    ```
    <#@ template language="C#" #>
    <#@ assembly name="System.Core" #>
    <#@ import namespace="System.Linq" #>
    <#@ import namespace="System.Text" #>
    <#@ import namespace="System.Collections.Generic" #>
    ```

## <a name="converting-an-existing-file-to-a-run-time-template"></a>Convertendo um arquivo existente em um Run-Time modelo

Uma boa maneira de criar um modelo é converter um exemplo existente da saída. Por exemplo, se seu aplicativo gerar arquivos HTML, você poderá começar criando um arquivo HTML simples. Certifique-se de que ele funciona corretamente e se sua aparência está correta. Em seguida, inclua-o em seu projeto Visual Studio e converta-o em um modelo.

### <a name="to-convert-an-existing-text-file-to-a-run-time-template"></a>Para converter um arquivo de texto existente em um modelo de tempo de executar

1. Inclua o arquivo em seu Visual Studio projeto. No Gerenciador de Soluções, no menu de atalho do projeto, escolha **Adicionar**  >  **Item Existente**.

2. De definir a propriedade Ferramentas Personalizadas **do** arquivo **como TextTemplatingFilePreprocessor**. No Gerenciador de Soluções, no menu de atalho do arquivo, escolha **Propriedades**.

    > [!NOTE]
    > Se a propriedade já estiver definida, certifique-se de que seja **TextTemplatingFilePreprocessor** e não **TextTemplatingFileGenerator**. Isso poderá acontecer se você incluir um arquivo que já tenha a **extensão .tt**.

3. Altere a extensão de nome de arquivo **para .tt**. Embora essa etapa seja opcional, ela ajuda você a evitar abrir o arquivo em um editor incorreto.

4. Remova espaços ou pontuação da parte principal do nome do arquivo. Por exemplo, "My Web Page.tt" estaria incorreto, mas "MyWebPage.tt" está correto. O nome do arquivo será usado como um nome de classe no código gerado.

5. Insira a linha a seguir no início do arquivo. Se você estiver trabalhando em um projeto Visual Basic, substitua "C#" por "VB".

    `<#@ template language="C#" #>`

## <a name="the-content-of-the-run-time-template"></a>O conteúdo do modelo Run-Time dados

### <a name="template-directive"></a>Diretiva de modelo

Mantenha a primeira linha do modelo como era quando você criou o arquivo:

`<#@ template language="C#" #>`

O parâmetro language dependerá do idioma do seu projeto.

### <a name="plain-content"></a>Conteúdo sem-texto

Edite **o arquivo .tt** para conter o texto que você deseja que seu aplicativo gere. Por exemplo:

```html
<html><body>
<h1>Sales for January</h2>
<!-- table to be inserted here -->
This report is Company Confidential.
</body></html>
```

### <a name="embedded-program-code"></a>Código do programa inserido

Você pode inserir o código do programa entre `<#` e `#>` . Por exemplo:

```csharp
<table>
    <# for (int i = 1; i <= 10; i++)
       { #>
         <tr><td>Test name <#= i #> </td>
             <td>Test value <#= i * i #> </td> </tr>
    <# } #>
 </table>
```

```vb
<table>
<#
    For i As Integer = 1 To 10
#>
    <tr><td>Test name <#= i #> </td>
      <td>Test value <#= i*i #> </td></tr>
<#
    Next
#>
</table>
```

Observe que as instruções são inseridas entre `<# ... #>` as expressões e são inseridas entre `<#= ... #>` . Para obter mais informações, consulte [Escrevendo um modelo de texto T4](../modeling/writing-a-t4-text-template.md).

## <a name="using-the-template"></a>Usando o modelo

### <a name="the-code-built-from-the-template"></a>O código criado com base no modelo

Quando você salva o **arquivo .tt,** um **arquivo .cs** ou **.vb** subsidiária é gerado. Para ver esse arquivo no **Gerenciador de Soluções**, expanda o **nó de arquivo .tt.** Em um Visual Basic, primeiro escolha **Mostrar Todos os Arquivos** na barra de **Gerenciador de Soluções** ferramentas.

Observe que o arquivo subsidiária contém uma classe parcial que contém um método chamado `TransformText()` . Você pode chamar esse método de seu aplicativo.

### <a name="generating-text-at-run-time"></a>Gerando texto em tempo de executar

No código do aplicativo, você pode gerar o conteúdo do modelo usando uma chamada como esta:

```csharp
MyWebPage page = new MyWebPage();
String pageContent = page.TransformText();
System.IO.File.WriteAllText("outputPage.html", pageContent);
```

```vb
Dim page = New My.Templates.MyWebPage
Dim pageContent = page.TransformText()
System.IO.File.WriteAllText("outputPage.html", pageContent)
```

Para colocar a classe gerada em um namespace específico, de acordo com a propriedade **Namespace** da Ferramenta Personalizada do arquivo de modelo de texto.

### <a name="debugging-runtime-text-templates"></a>Depurando modelos de texto de runtime

Depurar e testar modelos de texto de runtime da mesma maneira que o código comum.

Você pode definir um ponto de interrupção em um modelo de texto. Se você iniciar o aplicativo no modo de depuração do Visual Studio, poderá passar pelo código e avaliar as expressões de relógio da maneira normal.

### <a name="passing-parameters-in-the-constructor"></a>Passando parâmetros no construtor

Normalmente, um modelo deve importar alguns dados de outras partes do aplicativo. Para facilitar, o código criado pelo modelo é uma classe parcial. Você pode criar outra parte da mesma classe em outro arquivo em seu projeto. Esse arquivo pode incluir um construtor com parâmetros, propriedades e funções que podem ser acessados pelo código inserido no modelo e pelo restante do aplicativo.

Por exemplo, você pode criar um arquivo separado **MyWebPageCode.cs:**

```csharp
partial class MyWebPage
{
    private MyData m_data;
    public MyWebPage(MyData data) { this.m_data = data; }}
```

No arquivo de modelo **MyWebPage.tt**, você pode escrever:

```html
<h2>Sales figures</h2>
<table>
<# foreach (MyDataItem item in m_data.Items)
   // m_data is declared in MyWebPageCode.cs
   { #>
      <tr><td> <#= item.Name #> </td>
          <td> <#= item.Value #> </td></tr>
<# } // end of foreach
#>
</table>
```

Para usar esse modelo no aplicativo:

```csharp
MyData data = ...;
MyWebPage page = new MyWebPage(data);
String pageContent = page.TransformText();
System.IO.File.WriteAllText("outputPage.html", pageContent);
```

#### <a name="constructor-parameters-in-visual-basic"></a>Parâmetros do construtor em Visual Basic

No Visual Basic, o arquivo separado **MyWebPageCode.vb** contém:

```vb
Namespace My.Templates
  Partial Public Class MyWebPage
    Private m_data As MyData
    Public Sub New(ByVal data As MyData)
      m_data = data
    End Sub
  End Class
End Namespace
```

O arquivo de modelo pode conter:

```html
<#@ template language="VB" #>
<html><body>
<h1>Sales for January</h2>
<table>
<#
    For Each item In m_data.Items
#>
    <tr><td>Test name <#= item.Name #> </td>
      <td>Test value <#= item.Value #> </td></tr>
<#
    Next
#>
</table>
This report is Company Confidential.
</body></html>
```

O modelo pode ser invocado passando o parâmetro no construtor:

```vb
Dim data = New My.Templates.MyData
    ' Add data values here ....
Dim page = New My.Templates.MyWebPage(data)
Dim pageContent = page.TransformText()
System.IO.File.WriteAllText("outputPage.html", pageContent)
```

#### <a name="passing-data-in-template-properties"></a>Passando dados nas propriedades do modelo

Uma maneira alternativa de passar dados para o modelo é adicionar propriedades públicas à classe de modelo em uma definição de classe parcial. Seu aplicativo pode definir as propriedades antes de invocar `TransformText()` .

Você também pode adicionar campos à classe de modelo em uma definição parcial. Isso permite que você passe dados entre execuções sucessivas do modelo.

### <a name="use-partial-classes-for-code"></a>Usar classes parciais para código

Muitos desenvolvedores preferem evitar escrever grandes corpos de código em modelos. Em vez disso, você pode definir métodos em uma classe parcial que tenha o mesmo nome que o arquivo de modelo. Chame esses métodos do modelo. Dessa forma, o modelo mostra mais claramente a aparência da cadeia de caracteres de saída de destino. Discussões sobre a aparência do resultado podem ser separadas da lógica de criação dos dados que ele exibe.

### <a name="assemblies-and-references"></a>Assemblies e referências

Se você quiser que seu código de modelo referenciar um .NET ou outro  assembly, como **System.Xml.dll**, adicione-o às Referências do projeto da maneira normal.

Se você quiser importar um namespace da mesma maneira que uma `using` instrução, poderá fazer isso com a diretiva `import` :

```
<#@ import namespace="System.Xml" #>
```

Essas diretivas devem ser colocadas no início do arquivo, imediatamente após a `<#@template` diretiva .

### <a name="shared-content"></a>Conteúdo compartilhado

Se você tiver um texto compartilhado entre vários modelos, poderá coloque-o em um arquivo separado e incluí-lo em cada arquivo no qual ele deverá aparecer:

```
<#@include file="CommonHeader.txt" #>
```

O conteúdo incluído pode conter qualquer combinação de código de programa e texto sem-texto, e pode conter outras diretivas de inclusão e outras diretivas.

A diretiva include pode ser usada em qualquer lugar dentro do texto de um arquivo de modelo ou de um arquivo incluído.

### <a name="inheritance-between-run-time-text-templates"></a>Herança entre Run-Time modelos de texto

Você pode compartilhar conteúdo entre modelos de tempo de run-time escrevendo um modelo de classe base, que pode ser abstrato. Use o `inherits` parâmetro da diretiva para `<@#template#>` referenciar outra classe de modelo de runtime.

#### <a name="inheritance-pattern-fragments-in-base-methods"></a>Padrão de herança: fragmentos em métodos base

No padrão usado no exemplo a seguir, observe os seguintes pontos:

- A classe base `SharedFragments` define métodos dentro de blocos de recursos de classe `<#+ ... #>` .

- A classe base não contém nenhum texto livre. Em vez disso, todos os seus blocos de texto ocorrem dentro dos métodos de recurso de classe.

- A classe derivada invoca os métodos definidos em `SharedFragments` .

- O aplicativo chama `TextTransform()` o método da classe derivada, mas não transforma a classe base `SharedFragments` .

- As classes base e derivada são modelos de texto de runtime; ou seja, a **propriedade Ferramenta** Personalizada é definida como **TextTemplatingFilePreprocessor**.

**SharedFragments.tt:**

```
<#@ template language="C#" #>
<#+
protected void SharedText(int n)
{
#>
   Shared Text <#= n #>
<#+
}
// Insert more methods here if required.
#>
```

**MyTextTemplate1.tt:**

```
<#@ template language="C#" inherits="SharedFragments" #>
begin 1
   <# SharedText(2); #>
end 1
```

**MyProgram.cs:**

```csharp
...
MyTextTemplate1 t1  = new MyTextTemplate1();
string result = t1.TransformText();
Console.WriteLine(result);
```

**A saída resultante:**

```
begin 1
    Shared Text 2
end 1
```

#### <a name="inheritance-pattern-text-in-base-body"></a>Padrão de herança: texto no corpo base

Nessa abordagem alternativa ao uso da herança de modelo, a maior parte do texto é definida no modelo base. Os modelos derivados fornecem dados e fragmentos de texto que se ajustam ao conteúdo base.

**AbstractBaseTemplate1.tt:**

```
<#@ template language="C#" #>

Here is the description for this derived template:
  <#= this.Description #>

Here is the fragment specific to this derived template:
<#
  this.PushIndent("  ");
  SpecificFragment(42);
  this.PopIndent();
#>
End of common template.
<#+
  // State set by derived class before calling TextTransform:
  protected string Description = "";
  // 'abstract' method to be defined in derived classes:
  protected virtual void SpecificFragment(int n) { }
#>
```

**DerivedTemplate1.tt:**

```
<#@ template language="C#" inherits="AbstractBaseTemplate1" #>
<#
  // Set the base template properties:
  base.Description = "Description for this derived class";

  // Run the base template:
  base.TransformText();

#>
End material for DerivedTemplate1.

<#+
// Provide a fragment specific to this derived template:

protected override void SpecificFragment(int n)
{
#>
   Specific to DerivedTemplate1 : <#= n #>
<#+
}
#>
```

**Código do aplicativo:**

```csharp
...
DerivedTemplate1 t1 = new DerivedTemplate1();
string result = t1.TransformText();
Console.WriteLine(result);
```

**Saída resultante:**

```
Here is the description for this derived template:
  Description for this derived class

Here is the fragment specific to this derived template:
     Specific to DerivedTemplate1 : 42
End of common template.
End material for DerivedTemplate1.
```

## <a name="related-topics"></a>Tópicos Relacionados

Modelos de tempo de design: se você quiser usar um modelo para gerar código que se torne parte do seu aplicativo, consulte Geração de código em tempo de design usando modelos de texto [T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md).

Modelos de tempo de run-time podem ser usados em qualquer aplicativo em que os modelos e seu conteúdo são determinados no tempo de compilação. Mas se você quiser escrever uma extensão Visual Studio que gera texto de modelos que mudam em tempo de operação, consulte [Invocando transformação](../modeling/invoking-text-transformation-in-a-vs-extension.md)de texto em uma extensão do VS .

## <a name="see-also"></a>Confira também

- [Geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md)
- [Gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md)
- [Caixa de ferramentas T4](http://olegsych.com/T4Toolbox/)
