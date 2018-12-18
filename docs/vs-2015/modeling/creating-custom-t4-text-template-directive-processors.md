---
title: Criando processadores de diretiva do modelo de texto de T4 personalizados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- text templates, custom directive processors
ms.assetid: 422b47af-5441-4b02-b5ad-1b8b328457e3
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 0defae5127b3443eb30f02558fd1acf545651e3e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49852733"
---
# <a name="creating-custom-t4-text-template-directive-processors"></a>Criando processadores de diretiva de modelo de texto T4 personalizados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O *processo de transformação de modelo de texto* leva um *modelo de texto* arquivo como entrada e gera um arquivo de texto como saída. O *mecanismo de transformação do modelo de texto* controles que o processo e o mecanismo interage com um host de transformação de modelo de texto e o modelo de texto de um ou mais *processadores de diretriz* para concluir o processo. Para obter mais informações, consulte [o processo de transformação de modelo de texto](../modeling/the-text-template-transformation-process.md).  
  
 Para criar um processador de diretriz personalizado, é preciso criar uma classe herdada de <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> ou de <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>.  
  
 A diferença entre essas duas é que <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> implementa a interface mínima que é necessária para obter os parâmetros do usuário e para gerar o código que produz o arquivo de saída do modelo. <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> implementa o padrão de design requer/fornece. <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> lida com dois parâmetros especiais, `requires` e `provides`.  Por exemplo, um processador de diretriz personalizado pode aceitar um nome de arquivo do usuário, abra e ler o arquivo e, em seguida, armazenar o texto do arquivo em uma variável chamada `fileText`. Uma subclasse do <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> classe pode levar a um nome de arquivo do usuário como o valor da `requires` parâmetro e o nome da variável na qual armazenar o texto como o valor do `provides` parâmetro. Esse processador seria abrir e ler o arquivo e, em seguida, armazenar o texto do arquivo na variável especificada.  
  
 Antes de chamar um processador de diretriz personalizado de um modelo de texto no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], você deve registrá-lo.  
  
 Para obter mais informações sobre como adicionar a chave do registro, consulte [Implantando um processador de diretriz personalizado](../modeling/deploying-a-custom-directive-processor.md).  
  
## <a name="custom-directives"></a>Diretivas personalizadas  
 Uma diretiva personalizada tem esta aparência:  
  
 `<#@ MyDirective Processor="MyDirectiveProcessor" parameter1="value1" … #>`  
  
 Você pode usar um processador de diretriz personalizado quando quiser acessar dados externos ou recursos de um modelo de texto.  
  
 Modelos de texto diferentes podem compartilhar a funcionalidade que fornece um único processador de diretriz, portanto, processadores de diretriz oferecem uma maneira de código de fator para reutilização. Interno `include` diretiva é semelhante, pois você pode usá-lo para fatorar o código e compartilhá-lo entre modelos de texto diferente. A diferença é que qualquer funcionalidade que o `include` diretiva fornece é fixo e não aceita parâmetros. Se você quiser fornecer funcionalidade comum de um modelo de texto e permitir que o modelo para passar parâmetros, você deve criar um processador de diretriz personalizado.  
  
 Alguns exemplos de processadores de diretriz personalizados podem ser:  
  
-   Um processador de diretriz para retornar dados de um banco de dados que aceita um nome de usuário e senha como parâmetros.  
  
-   Um processador de diretriz para abrir e ler um arquivo que aceita o nome do arquivo como um parâmetro.  
  
### <a name="principal-parts-of-a-custom-directive-processor"></a>Partes de entidade de segurança de um processador de diretriz personalizado  
 Para desenvolver um processador de diretriz, você deve criar uma classe herdada de <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> ou <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>.  
  
 O mais importante `DirectiveProcessor` são os métodos que você deve implementar.  
  
- `bool IsDirectiveSupported(string directiveName)` – Retorne `true` se o processador de diretriz pode lidar com a diretiva nomeada.  
  
- `void ProcessDirective (string directiveName, IDictionary<string, string> arguments)` -O mecanismo de modelo chama esse método para cada ocorrência de uma diretiva no modelo. O processador deve salvar os resultados.  
  
  Depois de todas as chamadas para ProcessDirective (), o mecanismo de modelagem chamará esses métodos:  
  
- `string[] GetReferencesForProcessingRun()` -Retorne os nomes dos assemblies que exige que o código de modelo.  
  
- `string[] GetImportsForProcessingRun()` – Retorne os namespaces que podem ser usados no código do modelo.  
  
- `string GetClassCodeForProcessingRun()` -Retorna o código de métodos, propriedades e outras declarações que o código de modelo pode usar. A maneira mais fácil de fazer isso é criar uma cadeia de caracteres que contém o código c# ou Visual Basic. Para fazer com que o processador de diretriz capaz de sendo chamado de um modelo que use qualquer linguagem CLR, você pode construir as instruções de como uma árvore CodeDom e, em seguida, retornar o resultado de serializar a árvore no idioma usado pelo modelo.  
  
- Para obter mais informações, consulte [instruções passo a passo: Criando um processador de diretriz personalizado](../modeling/walkthrough-creating-a-custom-directive-processor.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Implantando um processador de diretiva personalizada](../modeling/deploying-a-custom-directive-processor.md)  
 Explica como registrar um processador de diretriz personalizado.  
  
 [Passo a passo: criando um processador de diretiva personalizado](../modeling/walkthrough-creating-a-custom-directive-processor.md)  
 Descreve como criar um processador de diretriz personalizado, como registrar e testar o processador de diretriz e como formatar o arquivo de saída como HTML.



