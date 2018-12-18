---
title: Gerando arquivos com o utilitário TextTransform | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- text templates, TextTransform utility
- TextTransform.exe
ms.assetid: 06a48235-fe02-403e-a1cf-2ae70b4db62f
caps.latest.revision: 43
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: e7dbe189c9b46c10dc7bac5da4b87457d7c6ecbf
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49227442"
---
# <a name="generating-files-with-the-texttransform-utility"></a>Gerando arquivos com o utilitário TextTransform
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

TextTransform.exe é uma ferramenta de linha de comando que você pode usar para transformar um modelo de texto. Quando você chama TextTransform.exe, você especifica o nome de um arquivo de modelo de texto como um argumento. TextTransform.exe chama o mecanismo de transformação de texto e processa o modelo de texto. TextTransform.exe geralmente é chamado de scripts. No entanto, não é geralmente necessário, porque você pode executar a transformação de texto no Visual Studio ou no processo de compilação.  
  
> [!NOTE]
>  Se você deseja executar a transformação de texto como parte de um processo de compilação, considere usar a tarefa de transformação de texto do MSBuild. Para obter mais informações, consulte [geração de código em um processo de compilação](../modeling/code-generation-in-a-build-process.md). Em um computador em que [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] estiver instalado, você também pode escrever um aplicativo ou [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensão que pode transformar modelos de texto. Para obter mais informações, consulte [modelos de processamento de texto usando um Host personalizado](../modeling/processing-text-templates-by-using-a-custom-host.md).  
  
 TextTransform.exe está localizado no seguinte diretório:  
  
 **\Program Files\Microsoft Shared\TextTemplating\11.0**  
  
## <a name="syntax"></a>Sintaxe  
  
```  
TextTransform [<options>] <templateName>  
```  
  
#### <a name="parameters"></a>Parâmetros  
  
|**Argumento**|**Descrição**|  
|------------------|---------------------|  
|`templateName`|Identifica o nome do arquivo de modelo que você deseja transformar.|  
  
|**Opção**|**Descrição**|  
|----------------|---------------------|  
|**-out** \<filename >|O arquivo no qual a saída da transformação é gravada.|  
|**-r** \<assembly >|Um assembly usado para compilar e executar o modelo de texto.|  
|**-u** \<namespace>|Um namespace que é usado para compilar o modelo.|  
|**-I** \<includedirectory >|Um diretório que contém os modelos de texto incluídos no modelo de texto especificado.|  
|**-P** \<referencepath >|Um diretório para procurar por assemblies especificados no modelo de texto ou usando o **- r** opção.<br /><br /> Por exemplo, para incluir os assemblies usados para a API do Visual Studio, use<br /><br /> `-P "%VSSHELLFOLDER%\Common7\IDE\PublicAssemblies"`|  
|**-dp** \<processorName>!\<className>!\<assemblyName&#124;codeBase>|O nome, o nome completo do tipo e o assembly de um processador de diretriz que pode ser usado para processar as diretivas personalizadas dentro do modelo de texto.|  
|**-um** [processorName]! [ directiveName]! \<parameterName >! \<parameterValue >|Especifique um valor de parâmetro para um processador de diretriz. Se você especificar apenas o nome do parâmetro e o valor, o parâmetro será disponibilizado para todos os processadores de diretriz. Se você especificar um processador de diretriz, o parâmetro está disponível somente para o processador especificado. Se você especificar um nome de diretiva, o parâmetro está disponível somente quando a diretiva especificada está sendo processada.<br /><br />  Em um modelo de texto, inclua `hostspecific` na diretiva do modelo e invocar a mensagem em `this.Host`. Por exemplo:<br /><br /> `<#@template language="c#" hostspecific="true"#> [<#= this.Host.ResolveParameterValue("", "", "parameterName") #>]`.<br /><br /> Digite sempre o '!' marca, mesmo se você omitir o processador opcional e nomes de diretiva. Por exemplo:<br /><br /> `-a !!param!value`|  
|**-h**|Fornece ajuda.|  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Tarefa|Tópico|  
|----------|-----------|  
|Gerar arquivos em uma solução do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].|[Geração de código no tempo de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|  
|Grave processadores de diretivas para transformar suas próprias fontes de dados.|[Personalizando a transformação de texto T4](../modeling/customizing-t4-text-transformation.md)|  
|Escreva um host de modelagem de texto que permite que você invoque os modelos de texto de seu próprio aplicativo.|[Processando modelos de texto usando um host personalizado](../modeling/processing-text-templates-by-using-a-custom-host.md)|



