---
title: T4 Diretiva de modelo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2b0a8e04-6fee-4c6c-b086-e49fc728a3ed
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: dcd11416bc067acaab8855b51969c7e1068e2c97
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49248214"
---
# <a name="t4-template-directive"></a>Diretiva de modelo T4
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um modelo de texto T4 do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] normalmente começa com uma diretiva `template`, que especifica como o modelo deve ser processado. Não deve haver mais de uma diretiva de modelo em um modelo de texto e nos arquivos que ele contenha.  
  
 Para obter uma visão geral da gravação de modelos de texto, consulte [gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md).  
  
## <a name="using-the-template-directive"></a>Usando a diretiva de modelo  
  
```  
<#@ template [language="VB"] [compilerOptions="options"] [culture="code"] [debug="true"] [hostspecific="true"] [inherits="templateBaseClass"] [visibility="internal"] [linePragmas="false"] #>  
```  
  
 A diretiva `template` tem vários atributos que permitem especificar diferentes aspectos da transformação. Todos os atributos são opcionais.  
  
## <a name="compileroptions-attribute"></a>Atributo compilerOptions  
 Exemplo:  
 `compilerOptions="optimize+"`  
  
 Valores válidos:  
 Algumas opções válidas do compilador. Para obter mais informações, consulte [opções de compilador c# está listadas por categoria](http://msdn.microsoft.com/library/96437ecc-6502-4cd3-b070-e9386a298e83) e [opções de compilador Visual Basic listadas por categoria](http://msdn.microsoft.com/library/fbe36f7a-7cfa-4f77-a8d4-2be5958568e3).  
  
 Ignorada para modelos de tempo de execução (pré-processados).  
  
 Estas opções são aplicadas quando o modelo é convertido em [!INCLUDE[csprcs](../includes/csprcs-md.md)] ou em [!INCLUDE[vb_current_short](../includes/vb-current-short-md.md)], e o código resultante é compilado.  
  
## <a name="culture-attribute"></a>Atributo culture  
 Exemplo:  
 `culture="de-CH"`  
  
 Valores válidos:  
 "", a cultura invariável, que é o padrão.  
  
 Uma cultura expressa como uma cadeia de caracteres no formato xx-XX. Por exemplo, en-US, ja-JP, de-CH, de-DE. Para obter mais informações, consulte <xref:System.Globalization.CultureInfo?displayProperty=fullName>.  
  
 O atributo culture especifica a cultura a ser usada quando um bloco de expressão é convertido em texto.  
  
## <a name="debug-attribute"></a>Atributo debug  
 Exemplo:  
 ```  
debug="true"  
```  
  
 Valores válidos:  
 `true, false`. O padrão é false.  
  
 Se o atributo `debug` for `true`, o arquivo de código intermediário conterá informações que permitem que o depurador identifique mais especificamente a posição em seu modelo onde ocorreu uma quebra ou uma exceção.  
  
 Para modelos de tempo de design, o arquivo de código intermediário será gravado para seus **% TEMP %** directory.  
  
 Para executar um modelo de tempo de design no depurador, salve o modelo de texto, em seguida, abra o menu de atalho do modelo de texto no Gerenciador de soluções e escolha **depurar modelo T4**.  
  
## <a name="hostspecific-attribute"></a>Atributo hostspecific  
 Exemplo:  
 ```  
hostspecific="true"  
```  
  
 Valores válidos:  
 `true, false, trueFromBase`. O padrão é false.  
  
 Se você definir o valor desse atributo como `true`, uma propriedade chamada `Host` será adicionado à classe gerada pelo modelo de texto. A propriedade é uma referência ao host do mecanismo de transformação e é declarada como <xref:Microsoft.VisualStudio.TextTemplating.ITextTemplatingEngineHost>. Se você definiu um host personalizado, pode convertê-lo no tipo de host personalizado.  
  
 Como o tipo dessa propriedade depende do tipo de host, ele só é útil se você estiver gravando um modelo de texto que funciona somente com um host específico. É aplicável às [modelos de tempo de design](../modeling/design-time-code-generation-by-using-t4-text-templates.md), mas não [modelos de tempo de execução](../modeling/run-time-text-generation-with-t4-text-templates.md).  
  
 Quando `hostspecific` for `true`, e você estiver usando [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], poderá converter `this.Host` em IServiceProvider para acessar recursos do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Você também pode usar `Host.ResolvePath(filename)` para obter o caminho absoluto de um arquivo no projeto. Por exemplo:  
  
```csharp  
<#@ template debug="false" hostspecific="true" language="C#" #>  
<#@ output extension=".txt" #>  
<#@ assembly name="EnvDTE" #>  
<#@ import namespace="EnvDTE" #>  
<#@ import namespace="System.IO" #>  
<# // Get the Visual Studio API as a service:  
 DTE dte = ((IServiceProvider)this.Host).GetCOMService(typeof(DTE)) as DTE;    
#>  
Number of projects in this solution: <#=  dte.Solution.Projects.Count #>  
  
<#  
 // Find a path within the current project:  
 string myFile = File.ReadAllText(this.Host.ResolvePath("MyFile.txt"));  
#>  
Content of myFile is:  
<#= myFile #>  
  
```  
  
 Se você usar os atributos `inherits` e `hostspecific` juntos, especifique host="trueFromBase" na classe derivada e host="true” na classe base. Isso evita uma definição dupla da propriedade `Host` no código gerado.  
  
## <a name="language-attribute"></a>Atributo language  
 Exemplo:  
 `language="VB"`  
  
 Valores válidos:  
 `C#` (padrão)  
  
 `VB`  
  
 O atributo language Especifica a linguagem ([!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ou [!INCLUDE[csprcs](../includes/csprcs-md.md)]) a ser usado para o código-fonte em blocos de instrução e expressão. O arquivo de código intermediário do qual o resultado é gerado usará essa linguagem. Essa linguagem não está relacionada à linguagem que seu modelo gera, que pode ser qualquer tipo de texto.  
  
 Por exemplo:  
  
```vb  
<#@ template language="VB" #>  
<#@ output extension=".txt" #>  
Squares of numbers:  
<#  
  Dim number As Integer  
  For number = 1 To 4  
#>  
  Square of <#= number #> is <#= number * number #>  
<#  
  Next number  
#>  
  
```  
  
## <a name="inherits-attribute"></a>Atributo inherits  
 Você pode especificar se o código do programa de seu modelo pode herdar de outra classe, que também pode ser gerado de um modelo de texto.  
  
### <a name="inheritance-in-a-run-time-preprocessed-text-template"></a>Herança em um modelo de texto de tempo de execução (pré-processado)  
 Você pode usar a herança entre modelos do texto de tempo de execução para criar um modelo básico que tenha muitas variantes derivadas. Modelos de tempo de execução são aqueles que têm o **Custom Tool** propriedade definida como **TextTemplatingFilePreprocessor**. Um modelo de tempo de execução gerencia o código que você pode chamar em seu aplicativo criar o texto definido no modelo. Para obter mais informações, consulte [geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md).  
  
 Se você não especificar um atributo `inherits`, uma classe base e uma classe derivada serão geradas a partir de seu modelo de texto. Quando você especificar um atributo `inherits`, somente a classe derivada será gerada. Você pode escrever uma classe base manualmente, mas deve fornecer os métodos usados pela classe derivada.  
  
 Normalmente, você especifica outro modelo pré-processado como a classe base. O modelo de base fornece os blocos de texto comuns, que podem ser intercalados com o texto dos modelos derivados. Você pode usar blocos de recursos de classe `<#+ ... #>` para definir os métodos que contêm fragmentos de texto. Por exemplo, você pode colocar o framework dp texto de saída no modelo de base, fornecendo métodos virtuais que podem ser substituídos em modelos derivados:  
  
 Modelo de texto de tempo de execução (pré-processado) BaseTemplate.tt:  
 ```scr  
This is the common header.  
<#   
  SpecificFragment1();   
#>  
A common central text.  
<#   
  SpecificFragment2();   
#>  
This is the common footer.  
<#+   
  // Declare abstract methods  
  protected virtual void SpecificFragment1() { }  
  protected virtual void SpecificFragment2() { }  
#>  
  
```  
  
 Modelo de texto de tempo de execução (pré-processado) DerivedTemplate1.tt:  
 ```csharp  
<#@ template language="C#" inherits="BaseTemplate" #>  
<#   
  // Run the base template:  
  base.TransformText();  
#>  
<#+  
// Provide fragments specific to this derived template:  
protected override void SpecificFragment1()  
{  
#>  
   Fragment 1 for DerivedTemplate1  
<#+  
}  
protected override void SpecificFragment2()  
{  
#>  
   Fragment 2 for DerivedTemplate1  
<#+  
}  
#>  
  
```  
  
 Código do aplicativo para invocar DerivedTemplate1:  
 ```csharp  
Console.WriteLine(new DerivedTemplate().TransformText());  
```  
  
 Saída resultante:  
 ```  
This is the common header.  
   Fragment 1 for DerivedTemplate1  
A common central text.  
   Fragment 2 for DerivedTemplate1  
This is the common footer.  
```  
  
 Você pode criar a base e as classes derivadas em projetos diferentes. Lembre-se de adicionar o projeto ou assembly de base às referências do projeto derivado.  
  
 Você também pode usar uma classe escrita manualmente comum como a classe base. A classe base deve fornecer os métodos usados pela classe derivada.  
  
> [!WARNING]
>  Se você usar os atributos `inherits` e `hostspecific` juntos, especifique hostspecific="trueFromBase" na classe derivada e host="true” na classe base. Isso evita uma definição dupla da propriedade `Host` no código gerado.  
  
### <a name="inheritance-in-a-design-time-text-template"></a>Herança em um modelo de texto de tempo de design  
 Um modelo de texto de tempo de design é um arquivo para o qual **Custom Tool** é definido como **TextTemplatingFileGenerator**. O modelo gera um arquivo de saída de código ou texto, que faz parte do seu projeto do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Para gerar o arquivo de saída, primeiro o modelo é convertido em um arquivo de código de programa intermediário, que você normalmente não vê. O atributo `inherits` especifica a classe base para esse código intermediário.  
  
 Para um modelo de texto de tempo de design, você pode especificar qualquer classe base que é derivada de <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation?displayProperty=fullName>. Use a diretiva `<#@assembly#>` para carregar o assembly ou projeto que contém a classe base.  
  
 Para obter mais informações, consulte ["Herança em modelos de texto" no Blog de Gareth Jones](http://go.microsoft.com/fwlink/?LinkId=208373).  
  
## <a name="linepragmas-attribute"></a>Atributo LinePragmas  
 Exemplo:  
 `linePragmas="false"`  
  
 Valores válidos:  
 `true` (padrão)  
  
 `false`  
  
 Definir esse atributo como false remove as marcas que identificam os números de linha no código gerado. Isso significa que o compilador relatará todos os erros usando os números de linha do código gerado. Isso fornece mais opções de depuração, pois você pode escolher depurar o modelo de texto ou o código gerado.  
  
 Esse atributo também pode ajudar se você descobrir que os nomes de arquivo absolutos em pragmas estão ofuscando mesclagens no controle do código-fonte.  
  
## <a name="visibility-attribute"></a>Atributo visibility  
 Exemplo:  
 `visibility="internal"`  
  
 Valores válidos:  
 `public` (padrão)  
  
 `internal`  
  
 Em um modelo de texto de tempo de execução, isso define o atributo visibility da classe gerada. Por padrão, a classe faz parte da API pública do código, mas definir `visibility="internal"` garante que somente seu código possa usar a classe text-generating.



