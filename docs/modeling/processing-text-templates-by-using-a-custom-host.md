---
title: Processando modelos de texto usando um host personalizado
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, in application or VS extension
- text templates, custom directive hosts
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 87d9f5f489bffcc624ff758c89e5d3a230a68d01
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47859335"
---
# <a name="process-text-templates-by-using-a-custom-host"></a>Processar modelos de texto usando um host personalizado

O *transformação de modelo de texto* processar usa um *modelo de texto* arquivo como entrada e gera um arquivo de texto como saída. Você pode chamar o mecanismo de transformação de texto de uma extensão do Visual Studio ou de um aplicativo autônomo em execução em um computador em que o Visual Studio está instalado. No entanto, você deve fornecer um *host de modelagem de texto*. Essa classe conecta o modelo ao ambiente, localizando recursos, como assemblies e arquivos de inclusão, e resolvendo a saída e as mensagens de erro.

> [!TIP]
> Se você estiver escrevendo um pacote ou a extensão que será executado dentro do Visual Studio, considere usar o serviço de modelagem de texto, em vez de escrever seu próprio host. Para obter mais informações, consulte [invocando transformação de texto em uma extensão do VS](../modeling/invoking-text-transformation-in-a-vs-extension.md).

> [!NOTE]
> Não recomendamos usar transformações de modelo de texto em aplicativos de servidor. Não recomendamos usar transformações de modelo de texto, exceto em um thread único. Isso ocorre porque o mecanismo de modelagem de texto reutiliza um único AppDomain para converter, compilar e executar modelos. O código convertido não foi criado para ser isento de threads. O mecanismo é projetado para processar arquivos em série, pois estão em um projeto do Visual Studio em tempo de design.
>
> Para aplicativos de tempo de execução, considere o uso de modelos de texto pré-processados: consulte [geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md).

Se seu aplicativo usa um conjunto de modelos que são fixos no tempo de compilação, é mais fácil usar modelos de texto pré-processados. Você também pode usar essa abordagem se o aplicativo será executado em um computador em que o Visual Studio não está instalado. Para obter mais informações, consulte [geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md).

## <a name="execute-a-text-template-in-your-application"></a>Executar um modelo de texto em seu aplicativo

Para executar um modelo de texto, chame o método ProcessTemplate de <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName>:

```csharp
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
 [Passo a passo: Criando um Host de modelo de texto personalizado](../modeling/walkthrough-creating-a-custom-text-template-host.md) mostra como criar um host de modelo de texto personalizado que torna a funcionalidade de modelo de texto disponível fora do Visual Studio.

## <a name="reference"></a>Referência
 <xref:Microsoft.VisualStudio.TextTemplating.ITextTemplatingEngineHost>

## <a name="related-sections"></a>Seções relacionadas

- [O processo de transformação do modelo de texto](../modeling/the-text-template-transformation-process.md) descreve como a transformação de texto funciona, e que partes você podem personalizar.
- [Criando processadores de diretiva de modelo de texto de T4 personalizados](../modeling/creating-custom-t4-text-template-directive-processors.md) fornece uma visão geral do texto processadores de diretiva de modelo.