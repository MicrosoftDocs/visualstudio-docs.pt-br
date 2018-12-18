---
title: Acessando o Visual Studio ou outros hosts a partir de um modelo de texto
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 9bb7bce5cb047018540599c9488fa4471dad2d1c
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53059292"
---
# <a name="access-visual-studio-or-other-hosts-from-a-text-template"></a>Acessar o Visual Studio ou outros hosts de um modelo de texto

Em um modelo de texto, você pode usar os métodos e propriedades que são expostas pelo host que executa o modelo. Visual Studio é um exemplo de um host.

> [!NOTE]
> Você pode usar propriedades e métodos de host nos modelos de texto normal, mas não no *pré-processado* modelos de texto.

## <a name="obtain-access-to-the-host"></a>Obter acesso ao host

Para acessar o host, defina `hostspecific="true"` no `template` diretiva. Agora você pode usar `this.Host`, que tem o tipo <xref:Microsoft.VisualStudio.TextTemplating.ITextTemplatingEngineHost>. O <xref:Microsoft.VisualStudio.TextTemplating.ITextTemplatingEngineHost> tipo tem membros que você pode usar, por exemplo, para resolver nomes de arquivo e log de erros.

### <a name="resolve-file-names"></a>Resolver nomes de arquivo

Para localizar o caminho completo de um arquivo em relação ao modelo de texto, use `this.Host.ResolvePath()`.

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="System.IO" #>
<#
 // Find a path within the same project as the text template:
 string myFile = File.ReadAllText(this.Host.ResolvePath("MyFile.txt"));
#>
Content of myFile is:
<#= myFile #>
```

### <a name="display-error-messages"></a>Exibir mensagens de erro

Este exemplo registra mensagens quando você transformar o modelo. Se o host for Visual Studio, os erros são adicionados para o **Error List**.

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="System.CodeDom.Compiler" #>
<#
  string message = "test message";
  this.Host.LogErrors(new CompilerErrorCollection()
    { new CompilerError(
       this.Host.TemplateFile, // Identify the source of the error.
       0, 0, "0",   // Line, column, error ID.
       message) }); // Message displayed in error window.
#>
```

## <a name="use-the-visual-studio-api"></a>Use a API do Visual Studio

Se você estiver executando um modelo de texto no Visual Studio, você pode usar `this.Host` para acessar os serviços fornecidos pelo Visual Studio e de pacotes ou as extensões que são carregadas.

Definir hostspecific = "true" e converta `this.Host` para <xref:System.IServiceProvider>.

Este exemplo obtém a API do Visual Studio, <xref:EnvDTE.DTE>, como um serviço:

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="EnvDTE" #>
<#
 IServiceProvider serviceProvider = (IServiceProvider)this.Host;
 DTE dte = serviceProvider.GetService(typeof(DTE)) as DTE;
#>
Number of projects in this solution: <#=  dte.Solution.Projects.Count #>
```

## <a name="use-hostspecific-with-template-inheritance"></a>Usar hostSpecific com herança do modelo

Especificar `hostspecific="trueFromBase"` se você também usar o `inherits` atributo, e se você herda de um modelo que especifica `hostspecific="true"`. Se você não fizer isso, você pode obter um compilador avisando que a propriedade `Host` foi declarada duas vezes.