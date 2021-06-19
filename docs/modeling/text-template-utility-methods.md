---
title: Métodos de utilitário do modelo de texto
description: Saiba mais sobre os vários métodos de utilitário de modelo de texto que estão disponíveis para você quando você escreve código Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- text templates, utility methods
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b45bf6418562da5315c986a64a1295c137e982d6
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388679"
---
# <a name="text-template-utility-methods"></a>Métodos de utilitário do modelo de texto

Há vários métodos que estão sempre disponíveis para você quando você escreve código em um Visual Studio de texto. Esses métodos são definidos em <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> .

> [!TIP]
> Você também pode usar outros métodos e serviços fornecidos pelo ambiente de host em um modelo de texto regular (não pré-processado). Por exemplo, você pode resolver caminhos de arquivo, erros de log e obter serviços fornecidos por Visual Studio e quaisquer pacotes carregados. Para obter mais informações, [consulte Acessando Visual Studio de um modelo de texto](/previous-versions/visualstudio/visual-studio-2010/gg604090\(v\=vs.100\)).

## <a name="write-methods"></a>Métodos de gravação

Você pode usar os métodos e para anexar texto dentro de um bloco de código padrão, em vez `Write()` de usar um bloco de código de `WriteLine()` expressão. Os dois blocos de código a seguir são funcionalmente equivalentes.

### <a name="code-block-with-an-expression-block"></a>Bloco de código com um bloco de expressão

```
<#
int i = 10;
while (i-- > 0)
    { #>
        <#= i #>
    <# }
#>
```

### <a name="code-block-using-writeline"></a>Bloco de código usando WriteLine()

```
<#
    int i = 10;
    while (i-- > 0)
    {
        WriteLine((i.ToString()));
    }
#>
```

Você pode achar útil usar um desses métodos utilitários em vez de um bloco de expressão dentro de um bloco de código longo com estruturas de controle aninhadas.

Os métodos e têm duas sobrecargas, uma que aceita um único parâmetro de cadeia de caracteres e outra que leva uma cadeia de caracteres de formato composto mais uma matriz de objetos a incluir na cadeia de `Write()` `WriteLine()` caracteres (como o `Console.WriteLine()` método ). Os dois usos a seguir `WriteLine()` de são funcionalmente equivalentes:

```
<#
    string msg = "Say: {0}, {1}, {2}";
    string s1 = "hello";
    string s2 = "goodbye";
    string s3 = "farewell";

    WriteLine(msg, s1, s2, s3);
    WriteLine("Say: hello, goodbye, farewell");
#>
```

## <a name="indentation-methods"></a>Métodos de recuo

Você pode usar métodos de recuo para formatar a saída do modelo de texto. A classe tem uma propriedade de cadeia de caracteres que mostra o recuo atual no modelo de texto e um campo que é uma lista dos recuos que <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> `CurrentIndent` foram `indentLengths` adicionados. Você pode adicionar um recuo com o método `PushIndent()` e subtrair um recuo com o `PopIndent()` método . Se você quiser remover todos os recuos, use o `ClearIndent()` método . O seguinte bloco de código mostra o uso desses métodos:

```
<#
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
    ClearIndent();
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
#>
```

Esse bloco de código produz a seguinte saída:

```
Hello
        Hello
                Hello
Hello
        Hello
```

## <a name="error-and-warning-methods"></a>Métodos de erro e aviso

Você pode usar métodos de utilitário de erro e aviso para adicionar mensagens à lista Visual Studio erros. Por exemplo, o código a seguir adicionará uma mensagem de erro à Lista de Erros.

```
<#
  try
  {
    string str = null;
    Write(str.Length.ToString());
  }
  catch (Exception e)
  {
    Error(e.Message);
  }
#>
```

## <a name="access-to-host-and-service-provider"></a>Acesso ao host e ao provedor de serviços

A propriedade `this.Host` pode fornecer acesso às propriedades expostas pelo host que está executando o modelo. Para usar `this.Host` , você deve definir o atributo na diretiva `hostspecific` `<@template#>` :

`<#@template ... hostspecific="true" #>`

O tipo de `this.Host` depende do tipo de host no qual o modelo está sendo executado. Em um modelo em execução no Visual Studio, você pode fazer a seleção para para obter acesso a `this.Host` `IServiceProvider` serviços como o IDE. Por exemplo:

```
EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)
                       .GetService(typeof(EnvDTE.DTE));
```

## <a name="using-a-different-set-of-utility-methods"></a>Usando um conjunto diferente de métodos de utilitário

Como parte do processo de geração de texto, o arquivo de modelo é transformado em uma classe, que é sempre nomeada `GeneratedTextTransformation` e herda de <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> . Se você quiser usar um conjunto diferente de métodos, poderá escrever sua própria classe e especificá-la na diretiva de modelo. Sua classe deve herdar de <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> .

```
<#@ template inherits="MyUtilityClass" #>
```

Use a `assembly` diretiva para referenciar o assembly em que a classe compilada pode ser encontrada.
