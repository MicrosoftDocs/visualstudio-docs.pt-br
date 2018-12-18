---
title: Geração de código e modelos de texto T4 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-techdebt
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.TextTemplating.TextTemplating
helpviewer_keywords:
- generating text
- .tt files
- code generation
- text templates
- generating code
ms.assetid: 74a0a748-5b11-4999-8bea-49572967827d
caps.latest.revision: 84
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: d1310d08138e4df172a5dc9f390d0407a68fe769
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49229809"
---
# <a name="code-generation-and-t4-text-templates"></a>Geração de código e modelos de texto T4
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], um *modelo de texto T4* é uma mistura de blocos de texto e a lógica de controle que pode gerar um arquivo de texto. A lógica de controle é escrita como fragmentos de código de programa na [!INCLUDE[csprcs](../includes/csprcs-md.md)] ou [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]. No Visual Studio 2015 atualização 2 e posterior, você pode usar os recursos de versão 6.0 do c# nas diretivas de modelos T4. O arquivo gerado pode ser texto de qualquer tipo, como uma página da Web, um arquivo de recurso ou código de origem do programa em qualquer idioma.  
  
 Há dois tipos de modelos de texto T4:  
  
 **Modelos de texto T4 de tempo de execução** ('pré-processado' modelos) é executado em seu aplicativo para produzir cadeias de caracteres de texto, normalmente como parte de sua saída.  
 Por exemplo, você pode criar um modelo para definir uma página HTML:  
  
```  
<html><body>  
 The date and time now is: <#= DateTime.Now #>  
</body></html>  
```  
  
 Observe que o modelo é semelhante a saída gerada. A semelhança do modelo para a saída resultante ajuda a evitar erros quando você deseja alterá-lo.  
  
 Além disso, o modelo contém fragmentos de código do programa. Você pode usar esses fragmentos repetir seções de texto, para tornar as seções condicionais e para mostrar os dados do seu aplicativo.  
  
 Para gerar a saída, o aplicativo chama uma função que é gerada pelo modelo. Por exemplo:  
  
```csharp  
string webResponseText = new MyTemplate().TransformText();  
  
```  
  
 Seu aplicativo pode ser executado em um computador que não tenha [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] instalado.  
  
 Para criar um modelo de tempo de execução, adicione uma **modelo de texto de pré-processado** ao seu projeto. Como alternativa, você pode adicionar um arquivo de texto sem formatação e defina suas **Custom Tool** propriedade **TextTemplatingFilePreprocessor**.  
  
 Para obter mais informações, consulte [geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md). Para obter mais informações sobre a sintaxe de modelos, consulte [gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md).  
  
 **Modelos de texto T4 em tempo de design** são executadas em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para definir a parte do código-fonte e outros recursos do seu aplicativo.  
 Normalmente você usaria vários modelos que ler os dados em um único arquivo de entrada ou o banco de dados e geram alguns dos seus `.cs`, `.vb`, ou outros arquivos de origem. Cada modelo gera um arquivo. Eles são executados dentro do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ou [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)].  
  
 Por exemplo, os dados de entrada pode ser um arquivo XML de dados de configuração. Sempre que você edite o arquivo XML durante o desenvolvimento, os modelos de texto poderia regenerar parte do código do aplicativo. Um dos modelos poderia se parecer com o exemplo a seguir:  
  
```  
<#@ output extension=".txt" #>  
<#@ assembly name="System.Xml" #>  
<#  
 System.Xml.XmlDocument configurationData = ...; // Read a data file here.  
#>  
namespace Fabrikam.<#= configurationData.SelectSingleNode("jobName").Value #>  
{  
  ... // More code here.   
}  
  
```  
  
 Depende dos valores no arquivo XML gerado `.cs` arquivo seria semelhante ao seguinte:  
  
```  
namespace Fabrikam.FirstJob  
{  
  ... // More code here.   
}  
```  
  
 Como outro exemplo, a entrada poderia ser um diagrama de fluxo de trabalho em uma atividade de negócios. Quando os usuários alterarem seu fluxo de trabalho de negócios ou quando você começa a trabalhar com novos usuários que têm um fluxo de trabalho diferente, é fácil gerar novamente o código de acordo com o novo modelo.  
  
 Modelos de tempo de design torná-lo mais rápido e confiável para alterar a configuração, quando os requisitos são alterados. Normalmente, a entrada é definida em termos de requisitos de negócios, como no exemplo de fluxo de trabalho. Isso torna mais fácil discutir as alterações com seus usuários. Modelos de tempo de design são, portanto, uma ferramenta útil em um processo de desenvolvimento do agile.  
  
 Para criar um modelo de tempo de design, adicione uma **modelo de texto** ao seu projeto. Como alternativa, você pode adicionar um arquivo de texto sem formatação e defina suas **Custom Tool** propriedade **TextTemplatingFileGenerator**.  
  
 Para obter mais informações, consulte [geração de código de tempo de Design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md). Para obter mais informações sobre a sintaxe de modelos, consulte [gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md).  
  
> [!NOTE]
>  O termo *modelo* , às vezes, é usado para descrever dados lidos por um ou mais modelos. O modelo pode estar em qualquer formato, em qualquer tipo de arquivo ou banco de dados. Ele não precisa ser um modelo UML ou um modelo de linguagem específica do domínio. 'Model' indica apenas que os dados podem ser definidos em termos de conceitos de negócios, em vez de que se assemelha o código.  
  
 O recurso de transformação do modelo de texto é denominado *T4*.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md)  
 Em qualquer aplicativo que gera arquivos de texto, modelos de texto pré-compilado são um método fácil e confiável de definir o texto. No entanto, esse método não pode ser usado para modelos de texto que alterar em tempo de execução.  
  
 [Geração de código no tempo de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md)  
 Geração de código e outros recursos de um modelo permite que você atualize seu aplicativo atualizando o modelo.  
  
 [Geração de código em um processo de build](../modeling/code-generation-in-a-build-process.md)  
 Se você tiver instalado o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] SDK de modelagem e visualização, você pode garantir o software gerado mantém atualizado com alterações no modelo.  
  
 [Gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md)  
 A sintaxe de um arquivo de modelo de texto.  
  
 [Passo a passo: gerenciando código usando modelos de texto](../modeling/walkthrough-generating-code-by-using-text-templates.md)  
 Uma demonstração de uma maneira de usar a geração de código.  
  
 [Depurando um modelo de texto T4](../modeling/debugging-a-t4-text-template.md)  
 Como depurar os modelos de texto e alguns erros comuns de modelo de texto.  
  
 [Gerando arquivos com o utilitário TextTransform](../modeling/generating-files-with-the-texttransform-utility.md)  
 A ferramenta de linha de comando que você pode usar para executar transformações de modelo de texto.  
  
 [Personalizando a transformação de texto T4](../modeling/customizing-t4-text-transformation.md)  
 Como gravar processadores de diretriz e hosts de modelagem personalizada para suas próprias fontes de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Gerar arquivos de um modelo UML](../modeling/generate-files-from-a-uml-model.md)   
 [Gerando código com base em uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md)



