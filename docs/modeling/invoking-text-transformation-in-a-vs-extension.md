---
title: Invocando transformação de texto em uma extensão VS
description: Saiba como você pode usar o serviço de modelagem de texto para transformar modelos de texto. Saiba também como obter o serviço STextTemplating e convertê-lo em ITextTemplating.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 71f376cbe0ffd6c2716802977f1570aa5036fcdb
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386768"
---
# <a name="invoke-text-transformation-in-a-visual-studio-extension"></a>Invocar a transformação de texto em uma extensão do Visual Studio

Se você estiver escrevendo uma extensão do Visual Studio, como um comando de menu ou uma [linguagem específica de domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md), poderá usar o serviço de modelagem de texto para transformar modelos de texto. Obtenha o serviço [STextTemplating](/previous-versions/visualstudio/visual-studio-2012/bb932394(v=vs.110)) e converta-o em [ITextTemplating](/previous-versions/visualstudio/visual-studio-2012/bb932392(v=vs.110)).

## <a name="get-the-text-templating-service"></a>Obter o serviço de modelagem de texto

```csharp
using Microsoft.VisualStudio.TextTemplating;
using Microsoft.VisualStudio.TextTemplating.VSHost;
...
// Get a service provider - how you do this depends on the context:
IServiceProvider serviceProvider = ...; // An instance of EnvDTE, for example

// Get the text template service:
ITextTemplating t4 = serviceProvider.GetService(typeof(STextTemplating)) as ITextTemplating;

// Process a text template:
string result = t4.ProcessTemplate(filePath, System.IO.File.ReadAllText(filePath));
```

## <a name="pass-parameters-to-the-template"></a>Passar parâmetros para o modelo

 Você pode passar parâmetros para o modelo. Dentro do modelo, você pode obter os valores dos parâmetros usando a diretiva `<#@parameter#>`.

 Para o tipo de um parâmetro, você deve usar um tipo que seja serializável ou que possa ser lido. Isto é, o tipo deve ser declarado com <xref:System.SerializableAttribute> ou deve ser derivado de <xref:System.MarshalByRefObject>. Essa restrição é necessária porque o modelo de texto é executado em um AppDomain separado. Todos os tipos internos, como **System. String** e **System. Int32** , são serializáveis.

 Para passar valores de parâmetros, o código de chamada pode colocar valores no dicionário `Session` ou em <xref:System.Runtime.Remoting.Messaging.CallContext>.

 O exemplo a seguir usa os dois métodos para transformar um modelo de teste curto:

```csharp
using Microsoft.VisualStudio.TextTemplating;
using Microsoft.VisualStudio.TextTemplating.VSHost;
...
// Get a service provider - how you do this depends on the context:
IServiceProvider serviceProvider = dte;

// Get the text template service:
ITextTemplating t4 = serviceProvider.GetService(typeof(STextTemplating)) as ITextTemplating;
ITextTemplatingSessionHost sessionHost = t4 as ITextTemplatingSessionHost;

// Create a Session in which to pass parameters:
sessionHost.Session = sessionHost.CreateSession();
sessionHost.Session["parameter1"] = "Hello";
sessionHost.Session["parameter2"] = DateTime.Now;

// Pass another value in CallContext:
System.Runtime.Remoting.Messaging.CallContext.LogicalSetData("parameter3", 42);

// Process a text template:
string result = t4.ProcessTemplate("",
   // This is the test template:
   "<#@parameter type=\"System.String\" name=\"parameter1\"#>"
 + "<#@parameter type=\"System.DateTime\" name=\"parameter2\"#>"
 + "<#@parameter type=\"System.Int32\" name=\"parameter3\"#>"
 + "Test: <#=parameter1#>    <#=parameter2#>    <#=parameter3#>");

// This test code yields a result similar to the following line:
//     Test: Hello    07/06/2010 12:37:45    42
```

## <a name="error-reporting-and-the-output-directive"></a>Relatório de erros e a diretiva de saída

Todos os erros que surgirem durante o processamento serão exibidos na janela de erro do Visual Studio. Além disso, você pode ser notificado de erros especificando um retorno de chamada que implementa [ITextTemplatingCallback](/previous-versions/visualstudio/visual-studio-2012/bb932397(v=vs.110)).

Se você quiser gravar a cadeia de caracteres de resultado em um arquivo, convém saber qual extensão e codificação de arquivo foram especificadas na diretiva `<#@output#>` no modelo. Essas informações também serão passadas para seu retorno de chamada. Para obter mais informações, consulte [diretiva de saída do T4](../modeling/t4-output-directive.md).

```csharp
void ProcessMyTemplate(string MyTemplateFile)
{
  string templateContent = File.ReadAllText(MyTemplateFile);
  T4Callback cb = new T4Callback();
  // Process a text template:
  string result = t4.ProcessTemplate(MyTemplateFile, templateContent, cb);
  // If there was an output directive in the MyTemplateFile,
  // then cb.SetFileExtension() will have been called.
  // Determine the output file name:
  string resultFileName =
    Path.Combine(Path.GetDirectoryName(MyTemplateFile),
        Path.GetFileNameWithoutExtension(MyTemplateFile))
      + cb.fileExtension;
  // Write the processed output to file:
  File.WriteAllText(resultFileName, result, cb.outputEncoding);
  // Append any error messages:
  if (cb.errorMessages.Count > 0)
  {
    File.AppendAllLines(resultFileName, cb.errorMessages);
  }
}

class T4Callback : ITextTemplatingCallback
{
  public List<string> errorMessages = new List<string>();
  public string fileExtension = ".txt";
  public Encoding outputEncoding = Encoding.UTF8;

  public void ErrorCallback(bool warning, string message, int line, int column)
  { errorMessages.Add(message); }

  public void SetFileExtension(string extension)
  { fileExtension = extension; }

  public void SetOutputEncoding(Encoding encoding, bool fromOutputDirective)
  { outputEncoding = encoding; }
}
```

O código pode ser testado com um arquivo de modelo semelhante ao seguinte:

```
<#@output extension=".htm" encoding="ASCII"#>
<# int unused;  // Compiler warning "unused variable"
#>
Sample text.
```

O aviso do compilador será exibido na janela de erro do Visual Studio e também gerará uma chamada para `ErrorCallback` .

## <a name="reference-parameters"></a>Parâmetros de referência

Você pode passar valores fora de um modelo de texto usando uma classe de parâmetro que é derivada de <xref:System.MarshalByRefObject>.

## <a name="related-articles"></a>Artigos relacionados

Para gerar texto de um modelo de texto pré-processado: chame o `TransformText()` método da classe gerada. Para obter mais informações, consulte [geração de texto em tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md).

Para gerar texto fora de uma extensão do Visual Studio: defina um host personalizado. Para obter mais informações, consulte [processando modelos de texto usando um host personalizado](../modeling/processing-text-templates-by-using-a-custom-host.md).

Para gerar o código-fonte que posteriormente pode ser compilado e executado: chame o método [PreprocessTemplate](/previous-versions/visualstudio/visual-studio-2012/ee844321(v=vs.110)) de [ITextTemplating](/previous-versions/visualstudio/visual-studio-2012/bb932392(v=vs.110)).
