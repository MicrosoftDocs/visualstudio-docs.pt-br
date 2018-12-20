---
title: Métodos de utilitário de modelo de texto | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- text templates, utility methods
ms.assetid: 8c11f9f7-678b-4f0c-b634-dc78fda699d1
caps.latest.revision: 52
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 4a9c5a0b4b6c85a301c5d3a0e12ad3687f54aeb0
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49186297"
---
# <a name="text-template-utility-methods"></a>Métodos de utilitário do modelo de texto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Há vários métodos que estão sempre disponíveis para você quando você escreve código um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] modelo de texto. Esses métodos são definidos no <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation>.  
  
> [!TIP]
>  Você também pode usar outros métodos e os serviços fornecidos pelo ambiente de host em um modelo de texto (não pré-processado) regular. Por exemplo, você pode resolver caminhos de arquivo, log de erros e obtenha serviços fornecidos pelo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e qualquer carregados pacotes.  Para obter mais informações, consulte [acessando o Visual Studio a partir de um modelo de texto](http://msdn.microsoft.com/en-us/0556f20c-fef4-41a9-9597-53afab4ab9e4).  
  
## <a name="write-methods"></a>Escrever métodos  
 Você pode usar o `Write()` e `WriteLine()` métodos para acrescentar texto dentro de um bloco de código padrão, em vez de usar um bloco de código de expressão. Os seguintes blocos de código são funcionalmente equivalentes.  
  
##### <a name="code-block-with-an-expression-block"></a>Bloco de código com um bloco de expressão  
  
```  
<#  
int i = 10;  
while (i-- > 0)  
    { #>  
        <#= i #>  
    <# }  
#>  
```  
  
##### <a name="code-block-using-writeline"></a>Bloco de código usando são  
  
```  
<#   
    int i = 10;  
    while (i-- > 0)  
    {   
        WriteLine((i.ToString()));  
    }  
#>  
```  
  
 Você talvez ache útil usar um dos seguintes métodos de utilitário em vez de um bloco de expressão dentro de um bloco de código longo com estruturas de controle aninhadas.  
  
 O `Write()` e `WriteLine()` métodos tem duas sobrecargas, uma que aceita um parâmetro de cadeia de caracteres única e outro que usa uma cadeia de caracteres de formato composto além de uma matriz de objetos a serem incluídos na cadeia de caracteres (como o `Console.WriteLine()` método). Os seguintes dois usos de `WriteLine()` são funcionalmente equivalentes:  
  
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
 Você pode usar métodos de recuo para formatar a saída do modelo de texto. O <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> classe tem um `CurrentIndent` propriedade string que mostra o recuo atual do modelo de texto e um `indentLengths` campo, ou seja, uma lista dos recuos que foram adicionados. Você pode adicionar um recuo com o `PushIndent()` método e subtraia um recuo com o `PopIndent()` método. Se você quiser remover todos os recuos, use o `ClearIndent()` método. O bloco de código a seguir mostra o uso desses métodos:  
  
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
  
 Este bloco de código produz a seguinte saída:  
  
```  
Hello  
        Hello  
                Hello  
Hello  
        Hello  
```  
  
## <a name="error-and-warning-methods"></a>Métodos de aviso e erro  
 Você pode usar métodos de utilitário de erro e aviso para adicionar mensagens para o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] lista de erros. Por exemplo, o código a seguir adicionará uma mensagem de erro para a lista de erros.  
  
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
  
## <a name="access-to-host-and-service-provider"></a>Acesso ao Host e o provedor de serviços  
 A propriedade `this.Host` pode fornecer acesso a propriedades expostas pelo host que está executando o modelo. Para usar `this.Host`, você deve definir `hostspecific` atributo no `<@template#>` diretiva:  
  
 `<#@template ... hostspecific="true" #>`  
  
 O tipo de `this.Host` depende do tipo de host no qual o modelo está em execução. Em um modelo que está sendo executado no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], você pode converter `this.Host` para `IServiceProvider` para obter acesso a serviços como o IDE. Por exemplo:  
  
```  
EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)  
                       .GetService(typeof(EnvDTE.DTE));  
```  
  
## <a name="using-a-different-set-of-utility-methods"></a>Usando um conjunto diferente de métodos de utilitário  
 Como parte do processo de geração de texto, seu arquivo de modelo é transformado em uma classe, que é sempre denominada `GeneratedTextTransformation`e herda <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation>. Se você quiser usar outro conjunto de métodos em vez disso, você pode escrever sua própria classe e especificá-lo na diretiva do modelo. Sua classe deve herdar de <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation>.  
  
```  
<#@ template inherits="MyUtilityClass" #>  
```  
  
 Use o `assembly` diretiva para referenciar o assembly em que a classe compilada pode ser encontrada.



