---
title: Criando processadores de diretiva de modelo de texto T4 personalizados
description: Saiba mais sobre o processo de transformação do modelo de texto e como criar um processador de diretiva de modelo de texto T4 personalizado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, custom directive processors
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 59644275f17eac197074351a777959bb1826a5de
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389495"
---
# <a name="create-custom-t4-text-template-directive-processors"></a>Criar processadores personalizados de diretiva de modelo de texto T4

O *processo de transformação do modelo de* texto assume um arquivo de *modelo* de texto como a entrada e produz um arquivo de texto como a saída. O *mecanismo de transformação modelo* de texto controla o processo e o mecanismo interage com um host de transformação de modelo de texto e um ou mais processadores de diretiva *de* modelo de texto para concluir o processo. Para obter mais informações, consulte [O processo de transformação modelo de texto](../modeling/the-text-template-transformation-process.md).

Para criar um processador de diretriz personalizado, é preciso criar uma classe herdada de <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> ou de <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>.

A diferença entre esses dois é que implementa a interface mínima necessária para obter parâmetros do usuário e gerar o código que produz o <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> arquivo de saída do modelo. <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> implementa o padrão de design requires/provides. <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> trata dois parâmetros especiais, `requires` e `provides` .  Por exemplo, um processador de diretiva personalizado pode aceitar um nome de arquivo do usuário, abrir e ler o arquivo e, em seguida, armazenar o texto do arquivo em uma variável chamada `fileText` . Uma subclasse da classe pode ter um nome de arquivo do usuário como o valor do parâmetro e o nome da variável na qual armazenar o texto como o valor do <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> `requires` `provides` parâmetro. Esse processador abriria e leria o arquivo e armazenaria o texto do arquivo na variável especificada.

Antes de chamar um processador de diretiva personalizado de um modelo de texto Visual Studio, você deve registrá-lo.

Para obter mais informações sobre como adicionar a chave do Registro, consulte [Implantando um processador de diretiva personalizado.](../modeling/deploying-a-custom-directive-processor.md)

## <a name="custom-directives"></a>Diretivas personalizadas

Uma diretiva personalizada tem esta aparência:

`<#@ MyDirective Processor="MyDirectiveProcessor" parameter1="value1" ... #>`

Você pode usar um processador de diretiva personalizado quando quiser acessar dados externos ou recursos de um modelo de texto.

Modelos de texto diferentes podem compartilhar a funcionalidade que um processador de diretiva única fornece, portanto, os processadores de diretiva fornecem uma maneira de fatorar o código para reutilização. A diretiva interna é semelhante, porque você pode usá-la para fatorar o `include` código e compartilhá-lo entre diferentes modelos de texto. A diferença é que qualquer funcionalidade que a `include` diretiva fornece é fixa e não aceita parâmetros. Se você quiser fornecer uma funcionalidade comum a um modelo de texto e permitir que o modelo passe parâmetros, crie um processador de diretiva personalizado.

Alguns exemplos de processadores de diretiva personalizados podem ser:

- Um processador de diretiva para retornar dados de um banco de dados que aceita um nome de usuário e uma senha como parâmetros.

- Um processador de diretiva para abrir e ler um arquivo que aceita o nome do arquivo como um parâmetro.

### <a name="principal-parts-of-a-custom-directive-processor"></a>Partes principais de um processador de diretiva personalizado

Para desenvolver um processador de diretiva, você deve criar uma classe que herda de <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> ou <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> .

Os métodos mais `DirectiveProcessor` importantes que você deve implementar são os a seguir.

- `bool IsDirectiveSupported(string directiveName)` - Retornar `true` se o processador de diretiva puder lidar com a diretiva nomeada.

- `void ProcessDirective (string directiveName, IDictionary<string, string> arguments)` – O mecanismo de modelo chama esse método para cada ocorrência de uma diretiva no modelo. O processador deve salvar os resultados.

Depois de todas as chamadas para ProcessDirective(), o mecanismo de emplatação chamará estes métodos:

- `string[] GetReferencesForProcessingRun()` - Retornar os nomes de assemblies que o código de modelo requer.

- `string[] GetImportsForProcessingRun()` – Retornar os namespaces que podem ser usados no código do modelo.

- `string GetClassCodeForProcessingRun()` – Retornar o código de métodos, propriedades e outras declarações que o código de modelo pode usar. A maneira mais fácil de fazer isso é criar uma cadeia de caracteres que contém o código C# ou Visual Basic código. Para tornar seu processador de diretiva capaz de ser chamado de um modelo que usa qualquer linguagem CLR, você pode construir as instruções como uma árvore CodeDom e retornar o resultado da serialização da árvore no idioma usado pelo modelo.

- Para obter mais informações, consulte [Passo a passo: criando um processador de diretiva personalizado.](../modeling/walkthrough-creating-a-custom-directive-processor.md)

## <a name="see-also"></a>Confira também

- [Implantar um Processador de Diretiva Personalizada](../modeling/deploying-a-custom-directive-processor.md) explica como registrar um processador de diretiva personalizado.
- [Passo a passo:](../modeling/walkthrough-creating-a-custom-directive-processor.md) Criar um Processador de Diretiva Personalizada descreve como criar um processador de diretiva personalizado, como registrar e testar o processador de diretiva e como formatar o arquivo de saída como HTML.
