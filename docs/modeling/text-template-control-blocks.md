---
title: Blocos de controle do modelo de texto
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, template code
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 90668c751005e697c4b78d0f3caf58f8a85db925
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49812018"
---
# <a name="text-template-control-blocks"></a>Blocos de controle do modelo de texto
Blocos de controle permitem que você escreva código em seu modelo de texto para variar a saída. Há três tipos de blocos de controle, que são diferenciados por seus colchetes de abertura:

-   `<# Standard control blocks #>` pode conter instruções.

-   `<#= Expression control blocks #>` pode conter expressões.

-   `<#+ Class feature control blocks #>` pode conter métodos, campos e propriedades.

## <a name="standard-control-block"></a>Bloco de controle padrão
 Blocos de controle padrão contêm instruções. Por exemplo, o bloco padrão a seguir obtém os nomes de todos os atributos no documento XML:

```
<#@ assembly name="System.Xml.dll" #>
<#@ import namespace="System.Xml" #>

<#
    List<string> allAttributes = new List<string>();
    XmlDocument xDoc = new XmlDocument();
    xDoc.Load(@"E:\CSharp\Overview.xml");
    XmlAttributeCollection attributes = xDoc.Attributes;
    if (attributes.Count > 0)
    {
       foreach (XmlAttribute attr in attributes)
       {
           allAtributes.Add(attr.Name);
       }
     }
#>
```

 Você pode inserir, como texto sem formatação em uma instrução composta `if` ou `for`. Por exemplo, este fragmento gera uma linha de saída em cada iteração do loop:

```
<#
       foreach (XmlAttribute attr in attributes)
       {
#>
Found another one!
<#
           allAtributes.Add(attr.Name);
       }
#>
```

> [!WARNING]
>  Sempre use {...} delimitar instruções aninhadas que contêm inserido texto sem formatação. O exemplo a seguir pode não funcionar corretamente:
>
>  `<# if (ShouldPrint) #> Some text. -- WRONG`
>
>  Em vez disso, você deve incluir chaves {}, da seguinte maneira:

```

<#
 if (ShouldPrint)
 {   //  "{" REQUIRED
#>
Some text.
<#
 }
#>
```

## <a name="expression-control-block"></a>Bloco de controle de expressão
 Blocos de controle de expressão são usados para o código que fornece as cadeias de caracteres a ser gravado no arquivo de saída. Por exemplo, no exemplo acima, você pode imprimir os nomes dos atributos para o arquivo de saída, modificando o bloco de código da seguinte maneira:

```
<#
    XmlDocument xDoc = new XmlDocument();
    xDoc.Load(@"E:\CSharp\Overview.xml");
    XmlAttributeCollection attributes = xDoc.Attributes;
    if (attributes != null)
    {
       foreach (XmlAttribute attr in attributes)
       {
#><#= attr.Name #><#
       }
    }
#>
```

## <a name="class-feature-control-block"></a>Bloco de controle de recurso de classe
 Você pode usar blocos de controle de recurso de classe para adicionar métodos, propriedades, campos ou as classes aninhadas, mesmo ao seu modelo de texto. O uso mais comum de blocos de recurso de classe é fornecer funções auxiliares para o código em outras partes do modelo de texto. Por exemplo, o seguinte bloco de recurso de classe coloca em maiuscula a primeira letra do nome do atributo (ou, se o nome contiver espaços em branco, ele coloca em maiuscula a primeira letra de cada palavra):

```
<#@ import namespace="System.Globalization" #>
```

```
<#+
    private string FixAttributeName(string name)
    {
        return CultureInfo.CurrentCulture.TextInfo.ToTitleCase(name);
    }
#>
```

> [!NOTE]
>  Um bloco de controle de recurso de classe não deve ser seguido por blocos de controle padrão no mesmo arquivo de modelo. No entanto, essa restrição não se aplica ao resultado do uso de `<#@include#>` diretivas. Cada arquivo incluído pode ter blocos padrão, seguidos por blocos de recurso de classe.

 Você pode criar uma função que gera a saída ao inserir blocos de texto e a expressão dentro de um bloco de controle de recurso de classe. Por exemplo:

```
<#+
    private void OutputFixedAttributeName(string name)
    {
#>
 Attribute:  <#= CultureInfo.CurrentCulture.TextInfo.ToTitleCase(name) #>
<#+  // <<< Notice that this is also a class feature block.
    }
#>
```

 Você poderia chamar essa função a partir de um bloco padrão ou outro bloco de recurso de classe:

```
<# foreach (Attribute attribute in item.Attributes)
{
  OutputFixedAttributeName(attribute.Name);
}
#>
```

## <a name="how-to-use-control-blocks"></a>Como usar blocos de controle
 Todo o código em todos os blocos de controle padrão e a expressão em um único modelo (incluindo todo o código em modelos incluídos) é combinado para formar o `TransformText()` método do código gerado. (Para obter mais informações sobre como incluir outros modelos de texto com o `include` diretiva, consulte [diretivas de modelo de texto T4](../modeling/t4-text-template-directives.md).)

 Você deve ter em mente as seguintes considerações ao usar blocos de controle:

-   **Idioma.** Você pode usar o código c# ou Visual Basic em um modelo de texto. O idioma padrão é c#, mas você pode especificar o Visual Basic com o `language` parâmetro do `template` diretiva. (Para obter mais informações sobre o `template` diretiva, consulte [diretivas de modelo de texto T4](../modeling/t4-text-template-directives.md).)

     O idioma usado nos blocos de controle não tem nada a ver com o idioma ou o formato do texto gerado em um modelo de texto. Você pode gerar em C# usando o Visual Basic código ou vice-versa.

     Você pode usar apenas um idioma em um modelo de texto especificado, incluindo todos os modelos de texto incluem com o `include` diretiva.

-   **Variáveis locais.** Como todo o código no controle padrão e a expressão de blocos em um modelo de texto é gerado como um único método, você deve Certifique-se de que não haja nenhum conflito com os nomes de variáveis locais. Se você estiver incluindo outros modelos de texto, certifique-se de que os nomes de variáveis são exclusivos em incluído todos os modelos. Uma maneira de garantir isso é adicionar uma cadeia de caracteres para cada nome de variável local que identifica o modelo de texto no qual ela foi declarada.

     Também é uma boa ideia para inicializar as variáveis locais para valores razoáveis, quando você declará-los, especialmente quando você está incluindo vários modelos de texto.

-   **Aninhamento de blocos de controle.** Blocos de controle não podem ser aninhados dentro uns aos outros. Você sempre deve encerrar um bloco de controle fornecido antes de abrir outra. Por exemplo, a seguir mostra como imprimir um texto em um bloco de expressão como parte de um bloco de controle padrão.

    ```
    <#
    int x = 10;
    while (x-- > 0)
    {
    #>
    <#= x #>
    <# } #>
    ```

-   **Refatoração.** Para manter seus modelos de texto curtos e fácil de entender, é altamente recomendável que você evite código repetitivo por fatorar o código reutilizável em funções auxiliares em blocos de recurso de classe ou criando sua própria classe de modelo de texto que herda a classe TextTransformation.