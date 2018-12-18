---
title: Geração de texto de tempo de execução com modelos de texto T4 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Preprocessed Text Template project item
- TextTemplatingFilePreprocessor custom tool
- text templates, TransformText() method
- text templates, generating files at run time
ms.assetid: 79b4b3c6-a9a7-4446-b6fd-e2388fc6b05f
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 75da17b32d3997121777f398a6663932c7d7143d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49920125"
---
# <a name="run-time-text-generation-with-t4-text-templates"></a>Geração de texto de tempo de execução com modelos de texto T4
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode gerar cadeias de caracteres de texto em seu aplicativo em tempo de execução usando [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] modelos de texto de tempo de execução. O computador em que o aplicativo é executado não precisa ter [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Modelos de tempo de execução são chamados de "pré-processado modelos de texto" porque o tempo de compilação, o modelo gera um código que é executado no tempo de execução.  
  
 Cada modelo é uma mistura do texto como ele aparecerá na cadeia de caracteres gerada e fragmentos de código do programa. Os fragmentos de programa fornecem valores para as partes variáveis da cadeia de caracteres e também controlam partes Condicionadas e repetidas.  
  
 Por exemplo, o modelo a seguir pode ser usado em um aplicativo que cria um relatório HTML.  
  
```  
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
  
 Observe que o modelo é uma página HTML na qual as partes variáveis foram substituídas por código do programa. Você pode começar o design de uma página dessas, escrevendo um protótipo estático da página HTML. Em seguida, você poderia substituir a tabela e outras partes variáveis com o código do programa que gera o conteúdo que varia de uma vez para a próxima.  
  
 Usando um modelo no seu aplicativo faz é mais fácil de ver a forma final da saída do que seria possível em, por exemplo, uma longa série de instruções de gravação. Fazendo alterações em forma de saída é mais fácil e confiável.  
  
## <a name="creating-a-run-time-text-template-in-any-application"></a>Criando um modelo de texto de tempo de execução em qualquer aplicativo  
  
#### <a name="to-create-a-run-time-text-template"></a>Para criar um modelo de texto de tempo de execução  
  
1.  No Gerenciador de soluções, no menu de atalho do projeto, escolha **Add**, **Novo Item**.  
  
2.  No **Adicionar Novo Item** caixa de diálogo, selecione **modelo de texto de tempo de execução**. (No [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] procure **Items\General comuns**.)  
  
3.  Digite um nome para seu arquivo de modelo.  
  
    > [!NOTE]
    >  O nome do arquivo de modelo será ser usado como um nome de classe no código gerado. Portanto, ele não deve ter espaços ou pontuação.  
  
4.  Escolha **Adicionar**.  
  
     Um novo arquivo é criado que tem a extensão **. TT**. Sua **Custom Tool** estiver definida como **TextTemplatingFilePreprocessor**. Ele contém as seguintes linhas:  
  
    ```  
    <#@ template language="C#" #>  
    <#@ assembly name="System.Core" #>  
    <#@ import namespace="System.Linq" #>  
    <#@ import namespace="System.Text" #>  
    <#@ import namespace="System.Collections.Generic" #>  
    ```  
  
## <a name="converting-an-existing-file-to-a-run-time-template"></a>Convertendo um arquivo existente em um modelo de tempo de execução  
 É uma boa maneira de criar um modelo converter um exemplo existente da saída. Por exemplo, se seu aplicativo irá gerar arquivos HTML, você pode iniciar com a criação de um arquivo HTML simples. Certifique-se de que ele funcione corretamente e se a sua aparência está correta. Em seguida, inclua-o na sua [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] de projeto e convertê-lo em um modelo.  
  
#### <a name="to-convert-an-existing-text-file-to-a-run-time-template"></a>Para converter um arquivo de texto existente em um modelo de tempo de execução  
  
1.  Incluir o arquivo em seu [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto. No Gerenciador de soluções, no menu de atalho do projeto, escolha **Add**, **Item existente**.  
  
2.  O arquivo de conjunto **ferramentas personalizados** propriedade **TextTemplatingFilePreprocessor**. No Gerenciador de soluções, no menu de atalho do arquivo, escolha **propriedades**.  
  
    > [!NOTE]
    >  Se a propriedade já está definida, certifique-se de que se trata **TextTemplatingFilePreprocessor** e não **TextTemplatingFileGenerator**. Isso pode acontecer se você incluir um arquivo que já tenha a extensão **. TT**.  
  
3.  Alterar a extensão de nome de arquivo para **. TT**. Embora esta etapa seja opcional, ele ajuda a evitar abrir o arquivo em um editor incorreto.  
  
4.  Remova a parte principal do nome do arquivo qualquer espaço ou pontuação. Por exemplo, "My Web Page.tt" seria incorreta, mas "MyWebPage.tt" está correto. O nome do arquivo será ser usado como um nome de classe no código gerado.  
  
5.  Insira a seguinte linha no início do arquivo. Se você estiver trabalhando em um projeto do Visual Basic, substitua "C#" com "VB".  
  
     `<#@ template language="C#" #>`  
  
## <a name="the-content-of-the-run-time-template"></a>O conteúdo do modelo de tempo de execução  
  
### <a name="template-directive"></a>Diretiva de modelo  
 Lembre-se a primeira linha do modelo como ele era quando você criou o arquivo:  
  
 `<#@ template language="C#" #>`  
  
 O parâmetro de idioma serão dependem da linguagem do seu projeto.  
  
### <a name="plain-content"></a>Conteúdo simples  
 Editar o **. TT** arquivo para conter o texto que você deseja que seu aplicativo para gerar. Por exemplo:  
  
```  
<html><body>  
<h1>Sales for January</h2>  
<!-- table to be inserted here -->  
This report is Company Confidential.  
</body></html>  
```  
  
### <a name="embedded-program-code"></a>Código de programa incorporado  
 Você pode inserir o código do programa entre `<#` e `#>`. Por exemplo:  
  
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
  
 Observe que as instruções são inseridas entre `<# ... #>` e as expressões são inseridas entre `<#= ... #>`. Para obter mais informações, consulte [gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md).  
  
## <a name="using-the-template"></a>Usando o modelo  
  
### <a name="the-code-built-from-the-template"></a>O código criado a partir do modelo  
 Sempre que você salvar a **. TT** do arquivo, uma subsidiária **. CS** ou **. vb** arquivo será gerado. Para ver esse arquivo no Gerenciador de soluções, expanda o **. TT** nó do arquivo. Em um projeto do Visual Basic, você poderá expandir o nó depois de clicar em **Show All Files** na barra de ferramentas do Gerenciador de soluções.  
  
 Observe que esse arquivo subsidiário contém uma classe parcial que contém um método chamado `TransformText()`. Você pode chamar esse método de seu aplicativo.  
  
### <a name="generating-text-at-run-time"></a>Gerando texto em tempo de execução  
 No código do aplicativo, você pode gerar o conteúdo do seu modelo usando uma chamada como esta:  
  
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
  
 Para colocar a classe gerada em um namespace específico, defina as **Namespace de ferramenta personalizada** propriedade do arquivo de modelo de texto.  
  
### <a name="debugging-runtime-text-templates"></a>Depuração de modelos de texto de tempo de execução  
 Depurar e testar modelos de texto de tempo de execução da mesma forma como código comum.  
  
 Você pode definir um ponto de interrupção em um modelo de texto. Se você iniciar o aplicativo no modo de depuração do Visual Studio, você pode percorrer o código e avaliar expressões de inspeção da maneira usual.  
  
### <a name="passing-parameters-in-the-constructor"></a>Passando parâmetros no construtor  
 Normalmente, um modelo deve importar alguns dados de outras partes do aplicativo. Para facilitar isso, o código criado pelo modelo é uma classe parcial. Você pode criar outra parte da mesma classe em outro arquivo em seu projeto. Esse arquivo pode incluir um construtor com parâmetros, propriedades e funções que podem acessadas pelo código que é inserido no modelo e pelo restante do aplicativo.  
  
 Por exemplo, você pode criar um arquivo separado **MyWebPageCode.cs**:  
  
```csharp  
partial class MyWebPage  
{  
    private MyData m_data;  
    public MyWebPage(MyData data) { this.m_data = data; }}  
```  
  
 No seu arquivo de modelo **MyWebPage.tt**, você poderia escrever:  
  
```csharp  
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
  
#### <a name="constructor-parameters-in-visual-basic"></a>Parâmetros do construtor no Visual Basic  
 Na [!INCLUDE[vbprvb](../includes/vbprvb-md.md)], o arquivo separado **MyWebPageCode.vb** contém:  
  
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
  
```vb  
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
  
 E o modelo seria invocado passando o parâmetro no construtor:  
  
```vb  
Dim data = New My.Templates.MyData  
    ' Add data values here ....  
Dim page = New My.Templates.MyWebPage(data)  
Dim pageContent = page.TransformText()  
System.IO.File.WriteAllText("outputPage.html", pageContent)  
  
```  
  
#### <a name="passing-data-in-template-properties"></a>Passando dados nas propriedades do modelo  
 É um método alternativo de passagem de dados para o modelo adicionar propriedades públicas para a classe de modelo em uma definição de classe parcial. Seu aplicativo pode definir as propriedades antes de invocar `TransformText()`.  
  
 Você também pode adicionar campos à sua classe de modelo em uma definição parcial. Isso permite que você passar dados entre as execuções sucessivas do modelo.  
  
### <a name="use-partial-classes-for-code"></a>Usar as classes parciais para o código  
 Muitos desenvolvedores preferem não escrever grandes corpos de código em modelos. Em vez disso, defina métodos em uma classe parcial que tem o mesmo nome que o arquivo de modelo. Chame esses métodos do modelo. Dessa forma, o modelo mostra mais claramente quais destino cadeia de saída terá a seguinte aparência. Discussões sobre a aparência do resultado podem ser separadas da lógica da criação dos dados que ele exibe.  
  
### <a name="assemblies-and-references"></a>Assemblies e as referências  
 Se você quiser que seu código de modelo para fazer referência a um .NET ou em outro assembly, como **dll**, você deve adicioná-lo ao seu projeto **referências** da maneira usual.  
  
 Se você deseja importar um namespace da mesma forma como uma `using` instrução, você pode fazer isso com o `import` diretiva:  
  
```  
<#@ import namespace="System.Xml" #>  
```  
  
 Essas diretivas devem ser colocadas no início do arquivo, imediatamente após o `<#@template` diretiva.  
  
### <a name="shared-content"></a>Conteúdo compartilhado  
 Se você tiver um texto que é compartilhado entre vários modelos, você pode colocá-lo em um arquivo separado e incluí-lo em cada arquivo no qual ele deve aparecer:  
  
```  
<#@include file="CommonHeader.txt" #>  
```  
  
 O conteúdo incluído pode conter qualquer combinação de código do programa e texto sem formatação, e ele pode conter outros incluem diretivas e outras diretivas.  
  
 A diretiva de inclusão pode ser usada em qualquer lugar dentro do texto de um arquivo de modelo ou um arquivo incluído.  
  
### <a name="inheritance-between-run-time-text-templates"></a>Herança entre modelos de texto de tempo de execução  
 Você pode compartilhar conteúdo entre os modelos de tempo de execução ao escrever um modelo de classe base, que pode ser abstrato. Use o `inherits` parâmetro do `<@#template#>` diretiva para fazer referência a outra classe de modelo de tempo de execução.  
  
#### <a name="inheritance-pattern-fragments-in-base-methods"></a>Padrão de herança: fragmentos em métodos de Base  
 O padrão usado no exemplo a seguir, observe os seguintes pontos:  
  
- A classe base `SharedFragments` define os métodos dentro de blocos de recurso de classe `<#+ ... #>`.  
  
- A classe base não contém nenhum texto livre. Em vez disso, todos os seus blocos de texto ocorrem dentro de métodos da classe de recurso.  
  
- A classe derivada chama os métodos definidos na `SharedFragments`.  
  
- O aplicativo chama o `TextTransform()` método da classe derivada, mas não transforma a classe base `SharedFragments`.  
  
- As classes base e derivadas são modelos de texto de tempo de execução: ou seja, o **Custom Tool** estiver definida como **TextTemplatingFilePreprocessor**.  
  
  **SharedFragments.tt:**  
  
```csharp  
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
  
```csharp  
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
  
#### <a name="inheritance-pattern-text-in-base-body"></a>Padrão de herança: O texto no corpo de Base  
 Nessa abordagem alternativa ao uso de herança do modelo, a maior parte do texto é definida no modelo de base. Modelos derivados fornecerem dados e fragmentos de texto que se ajustam o conteúdo de base.  
  
 **AbstractBaseTemplate1.tt:**  
  
```csharp  
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
  
```csharp  
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
  
## <a name="related-topics"></a>Tópicos relacionados  
 Modelos de tempo de design: Se você quiser usar um modelo para gerar o código que se torna parte do seu aplicativo, consulte [geração de código de tempo de Design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md).  
  
 Modelos de tempo de execução podem ser usados em qualquer aplicativo em que os modelos e seus conteúdos são determinados em tempo de compilação. Mas se você quiser escrever um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensão que gera texto a partir de modelos que alterar em tempo de execução, consulte [invocando transformação de texto em uma extensão do VS](../modeling/invoking-text-transformation-in-a-vs-extension.md).  
  
## <a name="see-also"></a>Consulte também  
 [Geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md)   
 [Gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md)   
 [Noções básicas sobre T4: Modelos de texto pré-processado pelo {1&gt;{2&gt;oleg Sych](http://www.olegsych.com/2009/09/t4-preprocessed-text-templates/)



