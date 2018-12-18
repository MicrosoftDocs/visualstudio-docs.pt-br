---
title: Acessando o Visual Studio ou outros Hosts de um modelo de texto | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a68886da-7416-4785-8145-3796bb382cba
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 3eb61ab5d372d02581c68391d125c7def23a402a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49298474"
---
# <a name="accessing-visual-studio-or-other-hosts-from-a-text-template"></a>Acessando o Visual Studio ou outros hosts a partir de um modelo de texto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em um modelo de texto, você pode usar os métodos e propriedades expostos pelo host que executa o modelo, como [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 Isso se aplica a modelos de texto normal, modelos de texto pré-processado não.  
  
## <a name="obtaining-access-to-the-host"></a>Como obter acesso ao host  
 Definir `hostspecific="true"` no `template` diretiva. Isso permite que você use `this.Host`, que tem o tipo <xref:Microsoft.VisualStudio.TextTemplating.ITextTemplatingEngineHost>. Esse tipo tem membros que você pode usar, por exemplo, para resolver nomes de arquivo e para registrar erros.  
  
### <a name="resolving-file-names"></a>Resolução de nomes de arquivo  
 Para localizar o caminho completo de um arquivo em relação ao modelo de texto, usá-lo. Host.ResolvePath().  
  
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
  
### <a name="displaying-error-messages"></a>Exibindo mensagens de erro  
 Este exemplo registra mensagens quando você transformar o modelo. Se o host for [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], eles são adicionados à janela de erro.  
  
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
  
## <a name="using-the-visual-studio-api"></a>Usando a API do Visual Studio  
 Se você estiver executando em um modelo de texto [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], você pode usar `this.Host` para acessar os serviços fornecidos pelo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e de pacotes ou as extensões que são carregadas.  
  
 Definir hostspecific = "true" e converta `this.Host` para <xref:System.IServiceProvider>.  
  
 Este exemplo obtém as [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] API, <xref:EnvDTE.DTE>, como um serviço:  
  
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
  
## <a name="using-hostspecific-with-template-inheritance"></a>Usando hostSpecific com herança do modelo  
 Especificar `hostspecific="trueFromBase"` se você também usar o `inherits` atributo, e se você herda de um modelo que especifica `hostspecific="true"`. Isso evita um aviso do compilador para o efeito que a propriedade `Host` foi declarada duas vezes.



