---
title: Gerando arquivos com o utilitário TextTransform
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- text templates, TextTransform utility
- TextTransform.exe
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 554ed126aa46b15148b902b901d8e9b664e3cdbd
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53062290"
---
# <a name="generate-files-with-the-texttransform-utility"></a>Gerar arquivos com o utilitário TextTransform

TextTransform.exe é uma ferramenta de linha de comando que você pode usar para transformar um modelo de texto. Quando você chama TextTransform.exe, você especifica o nome de um arquivo de modelo de texto como um argumento. TextTransform.exe chama o mecanismo de transformação de texto e processa o modelo de texto. TextTransform.exe geralmente é chamado de scripts. No entanto, não é geralmente necessário, porque você pode executar a transformação de texto no Visual Studio ou no processo de compilação.

> [!NOTE]
> Se você deseja executar a transformação de texto como parte de um processo de compilação, considere usar a tarefa de transformação de texto do MSBuild. Para obter mais informações, consulte [geração de código em um processo de compilação](../modeling/code-generation-in-a-build-process.md). Em um computador em que o Visual Studio está instalado, você também pode escrever um aplicativo ou extensão do Visual Studio que podem transformar modelos de texto. Para obter mais informações, consulte [modelos de processamento de texto usando um Host personalizado](../modeling/processing-text-templates-by-using-a-custom-host.md).

 TextTransform.exe está localizado no seguinte diretório:

 **\Program arquivos (x86) \Microsoft Visual Studio\2017\Professional\Common7\IDE**

para o Professional edition, ou

 **\Program arquivos (x86) \Microsoft Visual Studio\2017\Enterprise\Common7\IDE**

 para o Enterprise edition.

Nas versões anteriores do Visual Studio, o arquivo é encontrado no seguinte local:

**\Program arquivos (x86) \Common Files\Microsoft Shared\TextTemplating\{versão}**

onde {version} depende da versão anterior que está instalada.

## <a name="syntax"></a>Sintaxe

```
TextTransform [<options>] <templateName>
```

### <a name="parameters"></a>Parâmetros

|**Argumento**|**Descrição**|
|-|-|
|`templateName`|Identifica o nome do arquivo de modelo que você deseja transformar.|

|**Opção**|**Descrição**|
|-|-|
|**-out** \<filename >|O arquivo no qual a saída da transformação é gravada.|
|**-r** \<assembly >|Um assembly usado para compilar e executar o modelo de texto.|
|**-u** \<namespace>|Um namespace que é usado para compilar o modelo.|
|**-I** \<includedirectory >|Um diretório que contém os modelos de texto incluídos no modelo de texto especificado.|
|**-P** \<referencepath >|Um diretório para procurar por assemblies especificados no modelo de texto ou usando o **- r** opção.<br /><br /> Por exemplo, para incluir os assemblies usados para a API do Visual Studio, use<br /><br /> `-P "%VSSHELLFOLDER%\Common7\IDE\PublicAssemblies"`|
|**-dp** \<processorName>!\<className>!\<assemblyName&#124;codeBase>|O nome, o nome completo do tipo e o assembly de um processador de diretriz que pode ser usado para processar as diretivas personalizadas dentro do modelo de texto.|
|**-um** [processorName]! [ directiveName]! \<parameterName >! \<parameterValue >|Especifique um valor de parâmetro para um processador de diretriz. Se você especificar apenas o nome do parâmetro e o valor, o parâmetro será disponibilizado para todos os processadores de diretriz. Se você especificar um processador de diretriz, o parâmetro está disponível somente para o processador especificado. Se você especificar um nome de diretiva, o parâmetro está disponível somente quando a diretiva especificada está sendo processada.<br /><br /> Para acessar os valores de parâmetro de um processador de diretriz ou o modelo de texto, use [ITextTemplatingEngineHost.ResolveParameterValue](/previous-versions/visualstudio/visual-studio-2012/bb126369\(v\=vs.110\)). Em um modelo de texto, inclua `hostspecific` na diretiva do modelo e invocar a mensagem em `this.Host`. Por exemplo:<br /><br /> `<#@template language="c#" hostspecific="true"#> [<#= this.Host.ResolveParameterValue("", "", "parameterName") #>]`.<br /><br /> Digite sempre o '!' marca, mesmo se você omitir o processador opcional e nomes de diretiva. Por exemplo:<br /><br /> `-a !!param!value`|
|**-h**|Fornece ajuda.|

## <a name="related-topics"></a>Tópicos relacionados

|Tarefa|Tópico|
|-|-|
|Gere arquivos em uma solução do Visual Studio.|[Geração de código no tempo de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|
|Grave processadores de diretivas para transformar suas próprias fontes de dados.|[Personalizando a transformação de texto T4](../modeling/customizing-t4-text-transformation.md)|
|Escreva um host de modelagem de texto que permite que você invoque os modelos de texto de seu próprio aplicativo.|[Processando modelos de texto usando um host personalizado](../modeling/processing-text-templates-by-using-a-custom-host.md)|
