---
title: Processando modelos de texto usando um Host personalizado | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, in application or VS extension
- text templates, custom directive hosts
ms.assetid: affa3296-854d-47d6-9685-285f6d9ba5dc
caps.latest.revision: 35
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: e9f27d203f317a63049015dbeba073d8ee075e61
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63428080"
---
# <a name="processing-text-templates-by-using-a-custom-host"></a>Processando modelos de texto usando um host personalizado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O *transformação de modelo de texto* processar usa um *modelo de texto* arquivo como entrada e gera um arquivo de texto como saída. Você pode chamar o mecanismo de transformação de texto de uma extensão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ou da execução do aplicativo autônomo em um computador em que o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] está instalado. No entanto, você deve fornecer um *host de modelagem de texto*. Essa classe conecta o modelo ao ambiente, localizando recursos, como assemblies e arquivos de inclusão, e resolvendo a saída e as mensagens de erro.  
  
> [!TIP]
> Se você estiver escrevendo um pacote ou uma extensão que executará dentro do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], considere usar o serviço de modelagem de texto, em vez de escrever seu próprio host. Para obter mais informações, consulte [invocando transformação de texto em uma extensão do VS](../modeling/invoking-text-transformation-in-a-vs-extension.md).  
  
> [!NOTE]
> Não recomendamos usar transformações de modelo de texto em aplicativos de servidor. Não recomendamos usar transformações de modelo de texto, exceto em um thread único. Isso ocorre porque o mecanismo de modelagem de texto reutiliza um único AppDomain para converter, compilar e executar modelos. O código convertido não foi criado para ser isento de threads. O mecanismo é criado para processar arquivos em série, pois estão em um projeto do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] no tempo de design.  
>   
> Para aplicativos de tempo de execução, considere o uso de modelos de texto pré-processados: consulte [geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md).  
  
 Se seu aplicativo usa um conjunto de modelos que são fixos no tempo de compilação, é mais fácil usar modelos de texto pré-processados. Você também pode usar essa abordagem se seu aplicativo for executado em um computador em que o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] não está instalado. Para obter mais informações, consulte [geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md).  
  
## <a name="executing-a-text-template-in-your-application"></a>Executando um modelo de texto em seu aplicativo  
 Para executar um modelo de texto, chame o método ProcessTemplate de <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName>:  
  
```  
using Microsoft.VisualStudio.TextTemplating;  
...  
Engine engine = new Engine();  
string output = engine.ProcessTemplate(templateString, host);  
```  
  
 Seu aplicativo deve localizar e fornecer o modelo, e deve lidar com a saída.  
  
 No parâmetro `host`, você deve fornecer uma classe que implementa <xref:Microsoft.VisualStudio.TextTemplating.ITextTemplatingEngineHost>. Isso é chamado novamente pelo mecanismo.  
  
 O host deve ser capaz de registrar erros, resolver referências ao assembly e arquivos de inclusão, fornecer um domínio de aplicativo no qual o modelo pode executar e chamar o processador adequado para cada diretiva.  
  
 <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName> é definido em **Microsoft.VisualStudio.TextTemplating.\*. 0. dll**, e <xref:Microsoft.VisualStudio.TextTemplating.ITextTemplatingEngineHost> é definida no **Microsoft.VisualStudio.TextTemplating.Interfaces.\*. 0. dll**.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Passo a passo: Criar um host de modelo de texto personalizado](../modeling/walkthrough-creating-a-custom-text-template-host.md)  
 Demonstra como criar um host de modelo de texto personalizado que torna a funcionalidade do modelo de texto disponível fora do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
## <a name="reference"></a>Referência  
 <xref:Microsoft.VisualStudio.TextTemplating.ITextTemplatingEngineHost>  
  
## <a name="related-sections"></a>Seções relacionadas  
 [O processo de transformação de modelo de texto](../modeling/the-text-template-transformation-process.md)  
 Descreve como a transformação de texto funciona e que partes você pode personalizar.  
  
 [Criando processadores de diretiva de modelo de texto T4 personalizados](../modeling/creating-custom-t4-text-template-directive-processors.md)  
 Fornece uma visão geral de processadores de diretiva do modelo de texto.
