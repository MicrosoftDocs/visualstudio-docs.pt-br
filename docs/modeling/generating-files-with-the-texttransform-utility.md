---
title: Gerando arquivos com o utilitário TextTransform
description: Saiba como o utilitário TextTransform é uma ferramenta de linha de comando que você pode usar para transformar um modelo de texto.
ms.custom: SEO-VS-2020
ms.date: 07/26/2019
ms.topic: conceptual
helpviewer_keywords:
- text templates, TextTransform utility
- TextTransform.exe
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 743b7deb118bb3506773ec1a82d2331633afa7bc
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388822"
---
# <a name="generate-files-with-the-texttransform-utility"></a>Gerar arquivos com o utilitário TextTransform

TextTransform.exe é uma ferramenta de linha de comando que você pode usar para transformar um modelo de texto. Ao chamar TextTransform.exe, especifique o nome de um arquivo de modelo de texto como um argumento. TextTransform.exe chama o mecanismo de transformação de texto e processa o modelo de texto. TextTransform.exe geralmente é chamado de scripts. No entanto, isso geralmente não é necessário, porque você pode executar a transformação de texto no Visual Studio ou no processo de build.

> [!NOTE]
> Se você quiser executar a transformação de texto como parte de um processo de build, considere usar a tarefa de transformação de texto do MSBuild. Para obter mais informações, consulte [Geração de código em um processo de build](../modeling/code-generation-in-a-build-process.md). Em um computador no qual o Visual Studio está instalado, você também pode escrever um aplicativo ou uma extensão Visual Studio que pode transformar modelos de texto. Para obter mais informações, [consulte Ing Text Templates by using a Custom Host](../modeling/processing-text-templates-by-using-a-custom-host.md).

TextTransform.exe está localizado no seguinte diretório:

::: moniker range=">=vs-2019"

**\Arquivos de Programas (x86)\Microsoft Visual Studio\2019\Professional\Common7\IDE**

para Professional Edition ou

**\Arquivos de Programas (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE**

para Enterprise Edition.

::: moniker-end

::: moniker range="vs-2017"

**\Arquivos de Programas (x86)\Microsoft Visual Studio\2017\Professional\Common7\IDE**

para Professional Edition ou

**\Arquivos de Programas (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE**

para Enterprise Edition.

Nas versões anteriores do Visual Studio, o arquivo é encontrado no seguinte local:

**\Arquivos de Programas (x86)\Common Files\Microsoft Shared\TextTemplating \{ version}**

em que {version} depende de qual versão anterior está instalada.

::: moniker-end

## <a name="syntax"></a>Sintaxe

```
TextTransform [<options>] <templateName>
```

### <a name="parameters"></a>Parâmetros

|**Argument**|**Descrição**|
|-|-|
|`templateName`|Identifica o nome do arquivo de modelo que você deseja transformar.|

|**Opção**|**Descrição**|
|-|-|
|**-out**\<filename>|O arquivo no qual a saída da transformação é escrita.|
|**-r**\<assembly>|Um assembly usado para compilar e executar o modelo de texto.|
|**-u**\<namespace>|Um namespace usado para compilar o modelo.|
|**-I**\<includedirectory>|Um diretório que contém os modelos de texto incluídos no modelo de texto especificado.|
|**-P**\<referencepath>|Um diretório para pesquisar assemblies especificados dentro do modelo de texto ou para usar a **opção -r.**<br /><br /> Por exemplo, para incluir assemblies usados para a API Visual Studio, use<br /><br /> `-P "%VSSHELLFOLDER%\Common7\IDE\PublicAssemblies"`|
|**-dp** \<processorName> ! \<className> !\<assemblyName&#124;codeBase>|O nome, o nome do tipo completo e o assembly de um processador de diretiva que pode ser usado para processar diretivas personalizadas dentro do modelo de texto.|
|**-a** [processorName]! [directiveName]! \<parameterName> !\<parameterValue>|Especifique um valor de parâmetro para um processador de diretiva. Se você especificar apenas o nome e o valor do parâmetro, o parâmetro estará disponível para todos os processadores de diretiva. Se você especificar um processador de diretiva, o parâmetro estará disponível somente para o processador especificado. Se você especificar um nome de diretiva, o parâmetro estará disponível somente quando a diretiva especificada estiver sendo processada.<br /><br /> Para acessar os valores de parâmetro de um processador de diretiva ou modelo de texto, use [ITextTemplatingEngineHost.ResolveParameterValue](/previous-versions/visualstudio/visual-studio-2012/bb126369\(v\=vs.110\)). Em um modelo de texto, `hostspecific` inclua na diretiva de modelo e invoque a mensagem em `this.Host` . Por exemplo:<br /><br /> `<#@template language="c#" hostspecific="true"#> [<#= this.Host.ResolveParameterValue("", "", "parameterName") #>]`.<br /><br /> Sempre digite as marcas '!', mesmo se você omitir os nomes de processador e diretiva opcionais. Por exemplo:<br /><br /> `-a !!param!value`|
|**-h**|Fornece ajuda.|

## <a name="related-topics"></a>Tópicos relacionados

|Tarefa|Tópico|
|-|-|
|Gere arquivos em uma Visual Studio solução.|[Geração de código na hora de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|
|Grave processadores de diretivas para transformar suas próprias fontes de dados.|[Personalizando transformação de texto T4](../modeling/customizing-t4-text-transformation.md)|
|Escreva um host de seleção de texto que permite invocar modelos de texto de seu próprio aplicativo.|[Processando modelos de texto usando um host personalizado](../modeling/processing-text-templates-by-using-a-custom-host.md)|
