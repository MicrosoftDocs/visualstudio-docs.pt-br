---
title: Diretiva de parâmetro T4
description: Saiba que, Visual Studio, a diretiva de parâmetro declara propriedades no código do modelo que são inicializadas com os valores passados do contexto externo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8ef80179d43996669b9d883fd2ca9163208d18d7
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386092"
---
# <a name="t4-parameter-directive"></a>Diretiva de parâmetro T4

Em um Visual Studio de texto, a diretiva declara propriedades em seu código de modelo que são inicializadas com base em valores `parameter` passados do contexto externo. Você pode definir esses valores se escrever código que invoca a transformação de texto.

## <a name="using-the-parameter-directive"></a>Usando a diretiva Parameter

```
<#@ parameter type="Full.TypeName" name="ParameterName" #>
```

 A diretiva declara propriedades em seu código de modelo que são inicializadas de valores `parameter` passados do contexto externo. Você pode definir esses valores se escrever código que invoca a transformação de texto. Os valores podem ser passados no `Session` dicionário ou em <xref:System.Runtime.Remoting.Messaging.CallContext> .

 Você pode declarar parâmetros de qualquer tipo remota. Ou seja, o tipo deve ser declarado com <xref:System.SerializableAttribute> ou deve derivar de <xref:System.MarshalByRefObject> . Isso permite que os valores de parâmetro sejam passados para o AppDomain no qual o modelo é processado.

 Por exemplo, você pode escrever um modelo de texto com o seguinte conteúdo:

```
<#@ template language="C#" #>

<#@ parameter type="System.Int32" name="TimesToRepeat" #>

<# for (int i = 0; i < TimesToRepeat; i++) { #>
Line <#= i #>
<# } #>
```

## <a name="passing-parameter-values-to-a-template"></a>Passando valores de parâmetro para um modelo
 Se você estiver escrevendo uma extensão Visual Studio como um comando de menu ou um manipulador de eventos, poderá processar um modelo usando o serviço de edição de texto:

```csharp
// Get a service provider - how you do this depends on the context:
IServiceProvider serviceProvider = dte; // or dslDiagram.Store, for example
// Get the text template service:
ITextTemplating t4 = serviceProvider.GetService(typeof(STextTemplating)) as ITextTemplating;
ITextTemplatingSessionHost host = t4 as ITextTemplatingSessionHost;
// Create a Session in which to pass parameters:
host.Session = host.CreateSession();
// Add parameter values to the Session:
session["TimesToRepeat"] = 5;
// Process a text template:
string result = t4.ProcessTemplate("MyTemplateFile.t4",
  System.IO.File.ReadAllText("MyTemplateFile.t4"));
```

## <a name="passing-values-in-the-call-context"></a>Passando valores no contexto de chamada
 Como alternativa, você pode passar valores como dados lógicos no <xref:System.Runtime.Remoting.Messaging.CallContext> .

 O exemplo a seguir passa valores usando ambos os métodos:

```csharp
ITextTemplating t4 = this.Store.GetService(typeof(STextTemplating)) as ITextTemplating;
ITextTemplatingSessionHost host = t4 as ITextTemplatingSessionHost;
host.Session = host.CreateSession();
// Pass a value in Session:
host.Session["p1"] = 32;
// Pass another value in CallContext:
System.Runtime.Remoting.Messaging.CallContext.LogicalSetData("p2", "test");

// Process a small template inline:
string result = t4.ProcessTemplate("",
   "<#@parameter type=\"System.Int32\" name=\"p1\"#>"
 + "<#@parameter type=\"System.String\" name=\"p2\"#>"
 + "Test <#=p1#> <#=p2#>");

// Result value is:
//     Test 32 test
```

## <a name="passing-values-to-a-run-time-preprocessed-text-template"></a>Passando valores para um modelo Run-Time texto (pré-processador)
 Normalmente, não é necessário usar a diretiva com modelos de texto de tempo de `<#@parameter#>` run-time (pré-processamento). Em vez disso, você pode definir um construtor adicional ou uma propriedade settable para o código gerado, por meio do qual você passa valores de parâmetro. Para obter mais informações, consulte [Geração de texto em tempo de run-time com modelos de](../modeling/run-time-text-generation-with-t4-text-templates.md)texto T4 .

 No entanto, se você quiser usar em um modelo de tempo de run-time, poderá passar valores para ele `<#@parameter>` usando o dicionário de sessão. Por exemplo, suponha que você tenha criado o arquivo como um modelo pré-processado chamado `PreTextTemplate1` . Você pode invocar o modelo em seu programa usando o código a seguir.

```csharp
PreTextTemplate1 t = new PreTextTemplate1();
t.Session = new Microsoft.VisualStudio.TextTemplating.TextTemplatingSession();
t.Session["TimesToRepeat"] = 5;
// Add other parameter values to t.Session here.
t.Initialize(); // Must call this to transfer values.
string resultText = t.TransformText();
```

## <a name="obtaining-arguments-from-texttemplateexe"></a>Obtendo argumentos de TextTemplate.exe

> [!IMPORTANT]
> A `parameter` diretiva não recupera valores definidos no parâmetro do utilitário `-a` `TextTransform.exe` . Para obter esses valores, `hostSpecific="true"` de definido na diretiva e use `template` `this.Host.ResolveParameterValue("","","argName")` .
