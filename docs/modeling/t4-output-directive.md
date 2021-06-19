---
title: T4 Diretiva de saída
description: Saiba que, Visual Studio de texto, a diretiva de saída é usada para definir a extensão de nome de arquivo e a codificação do arquivo transformado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8105edc57e68aa7cedcb612ec4f6bcd0ef367d2f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386105"
---
# <a name="t4-output-directive"></a>T4 Diretiva de saída

Em Visual Studio de texto, a diretiva é usada para definir a extensão de nome de arquivo e a codificação `output` do arquivo transformado.

 Por exemplo, se seu projeto Visual Studio inclui um arquivo de modelo **chamado MyTemplate.tt** que contém a seguinte diretiva:

 `<#@output extension=".cs"#>`

 em Visual Studio gerará um arquivo chamado **MyTemplate.cs**

 A diretiva de `output` não é necessária em um modelo de texto de tempo de execução (pré-processado). Ao invés disso, o aplicativo obtém a cadeia de caracteres gerada ao chamar `TextTransform()`. Para obter mais informações, consulte [Geração de texto em tempo de run-time com modelos de](../modeling/run-time-text-generation-with-t4-text-templates.md)texto T4 .

## <a name="using-the-output-directive"></a>Usando a Diretiva de Saída

```
<#@ output extension=".fileNameExtension" [encoding="encoding"] #>
```

 Não deverá haver mais de uma diretiva de `output` em cada modelo de texto.

## <a name="extension-attribute"></a>atributo de extensão
 Especifica a extensão do nome de arquivo do arquivo de saída do texto gerado.

 O valor padrão é **.cs**

 Exemplos: `<#@ output extension=".txt" #>`

 `<#@ output extension=".htm" #>`

 `<#@ output extension=".cs" #>`

 `<#@ output extension=".vb" #>`

 Valores aceitáveis: qualquer extensão de nome de arquivo válida.

## <a name="encoding-attribute"></a>atributo de codificação
 Especifica a codificação usada ao gerar o arquivo de saída. Por exemplo:

 `<#@ output encoding="utf-8"#>`

 O valor padrão é a codificação usada pelo arquivo de modelo de texto.

 Valores aceitáveis: `us-ascii`

 `utf-16BE`

 `utf-16`

 `utf-8`

 `utf-7`

 `utf-32`

 `0` (Padrão do sistema)

 Em geral, é possível usar a cadeia de caracteres do WebName ou o número da CodePage de qualquer uma das codificações retornadas por <xref:System.Text.Encoding.GetEncodings%2A?displayProperty=fullName>.
