---
title: Invocando transformação de texto em uma extensão do VS | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 64674976-841f-43cb-8e61-0645c8a89eec
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 0751229e778e13375698f591d789edfd318b3ffc
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49298617"
---
# <a name="invoking-text-transformation-in-a-vs-extension"></a>Invocando transformação de texto em uma extensão VS
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se você estiver escrevendo uma [extensão do Visual Studio](http://msdn.microsoft.com/library/5b1b5db3-6005-44cf-83b0-e608d7764d14) como um comando de menu ou [linguagem específica do domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md), você pode usar o serviço de modelagem de texto para transformar modelos de texto. Obtenha o serviço <xref:Microsoft.VisualStudio.TextTemplating.VSHost.STextTemplating> e converta-o em <xref:Microsoft.VisualStudio.TextTemplating.VSHost.ITextTemplating>.  
  
## <a name="getting-the-text-templating-service"></a>Obtendo o serviço de modelagem de texto  
  
```csharp  
using Microsoft.VisualStudio.TextTemplating;  
using Microsoft.VisualStudio.TextTemplating.VSHost;  
...  
// Get a service provider – how you do this depends on the context:  
IServiceProvider serviceProvider = ...; // An instance of EnvDTE, for example   
  
// Get the text template service:  
ITextTemplating t4 = serviceProvider.GetService(typeof(STextTemplating)) as ITextTemplating;  
  
// Process a text template:  
string result = t4.ProcessTemplate(filePath, System.IO.File.ReadAllText(filePath));  
  
```  
  
## <a name="passing-parameters-to-the-template"></a>Passando parâmetros para o modelo  
 Você pode passar parâmetros para o modelo. Dentro do modelo, você pode obter os valores dos parâmetros usando a diretiva `<#@parameter#>`.  
  
 Para o tipo de um parâmetro, você deve usar um tipo que seja serializável ou que possa ser lido. Isto é, o tipo deve ser declarado com <xref:System.SerializableAttribute> ou deve ser derivado de <xref:System.MarshalByRefObject>. Essa restrição é necessária porque o modelo de texto é executado em um AppDomain separado. Todos os tipos internos, como **System. String** e **System.Int32** são serializáveis.  
  
 Para passar valores de parâmetros, o código de chamada pode colocar valores no dicionário `Session` ou em <xref:System.Runtime.Remoting.Messaging.CallContext>.  
  
 O exemplo a seguir usa os dois métodos para transformar um modelo de teste curto:  
  
```  
using Microsoft.VisualStudio.TextTemplating;  
using Microsoft.VisualStudio.TextTemplating.VSHost;  
...  
// Get a service provider – how you do this depends on the context:  
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
  
## <a name="error-reporting-and-the-output-directive"></a>Relatório de erros e diretiva de saída  
 Os erros que ocorrem durante o processamento serão exibidos na janela de erro do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Além disso, você pode ser notificado dos erros especificando um retorno de chamada que implementa <xref:Microsoft.VisualStudio.TextTemplating.VSHost.ITextTemplatingCallback>.  
  
 Se você quiser gravar a cadeia de caracteres de resultado em um arquivo, convém saber qual extensão e codificação de arquivo foram especificadas na diretiva `<#@output#>` no modelo. Essas informações também serão passadas para seu retorno de chamada. Para obter mais informações, consulte [T4 diretiva de saída](../modeling/t4-output-directive.md).  
  
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
  
 O aviso do compilador aparecerá na janela de erro do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e também gerará uma chamada para `ErrorCallback`.  
  
## <a name="reference-parameters"></a>Parâmetros de referência  
 Você pode passar valores fora de um modelo de texto usando uma classe de parâmetro que é derivada de <xref:System.MarshalByRefObject>.  
  
## <a name="related-topics"></a>Tópicos relacionados  
 Para gerar o texto a partir de um modelo de texto pré-processado:  
 Chame o método `TransformText()` da classe gerada. Para obter mais informações, consulte [geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md).  
  
 Para gerar o texto fora de uma extensão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]:  
 Defina um host personalizado. Para obter mais informações, consulte [modelos de processamento de texto usando um Host personalizado](../modeling/processing-text-templates-by-using-a-custom-host.md).  
  
 Para gerar um código-fonte que possa ser compilado e executado posteriormente:  
 Chame o método `t4.PreprocessTemplate()` de <xref:Microsoft.VisualStudio.TextTemplating.VSHost.ITextTemplating>.



