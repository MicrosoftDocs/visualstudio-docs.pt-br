---
title: Acessando o Visual Studio ou outros hosts a partir de um modelo de texto
description: Saiba como você pode usar métodos e propriedades em um modelo de texto exposto pelo host que executa o modelo.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3cde4b2afe6d09c3958bbabe7a5669a13f8de8f2
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389118"
---
# <a name="access-visual-studio-or-other-hosts-from-a-text-template"></a>Acessar Visual Studio ou outros hosts de um modelo de texto

Em um modelo de texto, você pode usar métodos e propriedades expostos pelo host que executa o modelo. Visual Studio é um exemplo de um host.

> [!NOTE]
> Você pode usar métodos e propriedades de host em modelos de texto regulares, mas não em *modelos de texto pré-processadas.*

## <a name="obtain-access-to-the-host"></a>Obter acesso ao host

Para acessar o host, de `hostspecific="true"` definido na `template` diretiva . Agora você pode usar `this.Host` , que tem o tipo [ITextTemplatingEngineHost.](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110)) O [tipo ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110)) tem membros que você pode usar para resolver nomes de arquivo e erros de log, por exemplo.

### <a name="resolve-file-names"></a>Resolver nomes de arquivo

Para encontrar o caminho completo de um arquivo em relação ao modelo de texto, use `this.Host.ResolvePath()` .

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

Este exemplo registra mensagens quando você transforma o modelo. Se o host for Visual Studio, os erros serão adicionados à **Lista de Erros**.

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

## <a name="use-the-visual-studio-api"></a>Usar a API Visual Studio dados

Se você estiver executando um modelo de texto no Visual Studio, poderá usar para acessar os serviços fornecidos pelo Visual Studio e quaisquer pacotes ou extensões `this.Host` carregados.

De definir hostspecific="true" e cast `this.Host` em <xref:System.IServiceProvider> .

Este exemplo obtém a API Visual Studio, <xref:EnvDTE.DTE> , como um serviço:

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

## <a name="use-hostspecific-with-template-inheritance"></a>Usar hostSpecific com herança de modelo

`hostspecific="trueFromBase"`Especifique se você também usa o atributo e se herdar de um modelo que especifica `inherits` `hostspecific="true"` . Caso não faça isso, você poderá receber um aviso do compilador de que a `Host` propriedade foi declarada duas vezes.
