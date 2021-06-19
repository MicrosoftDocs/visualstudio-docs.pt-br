---
title: Processando modelos de texto usando um host personalizado
description: Saiba que o processo de transformação do modelo de texto aceita um arquivo de modelo de texto como a entrada e produz um arquivo de texto como a saída.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, in application or VS extension
- text templates, custom directive hosts
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a301df6edaf8558ade5c8a297f233b58de6d8f4e
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390926"
---
# <a name="process-text-templates-by-using-a-custom-host"></a>Processar modelos de texto usando um host personalizado

O *processo de transformação do modelo* de texto assume um arquivo de *modelo* de texto como a entrada e produz um arquivo de texto como a saída. Você pode chamar o mecanismo de transformação de texto de uma extensão Visual Studio ou de um aplicativo autônomo em execução em um computador no qual Visual Studio está instalado. No entanto, você deve fornecer um *host de emplatação de texto*. Essa classe conecta o modelo ao ambiente, localizando recursos, como assemblies e arquivos de inclusão, e resolvendo a saída e as mensagens de erro.

> [!TIP]
> Se você estiver escrevendo um pacote ou extensão que será executado no Visual Studio, considere usar o serviço de emplatação de texto, em vez de escrever seu próprio host. Para obter mais informações, consulte [Invocando a transformação de texto em uma extensão do VS.](../modeling/invoking-text-transformation-in-a-vs-extension.md)

> [!NOTE]
> Não recomendamos usar transformações de modelo de texto em aplicativos de servidor. Não recomendamos usar transformações de modelo de texto, exceto em um thread único. Isso ocorre porque o mecanismo de modelagem de texto reutiliza um único AppDomain para converter, compilar e executar modelos. O código convertido não foi criado para ser isento de threads. O Mecanismo foi projetado para processar arquivos em série, pois eles estão em um projeto Visual Studio em tempo de design.
>
> Para aplicativos em tempo de run time, considere o uso de modelos de texto pré-processadores: consulte Geração de texto em tempo de [run-time com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md).

Se seu aplicativo usa um conjunto de modelos que são fixos no tempo de compilação, é mais fácil usar modelos de texto pré-processados. Você também poderá usar essa abordagem se o aplicativo for executado em um computador no qual Visual Studio não está instalado. Para obter mais informações, consulte [Geração de texto em tempo de run-time com modelos de](../modeling/run-time-text-generation-with-t4-text-templates.md)texto T4 .

## <a name="execute-a-text-template-in-your-application"></a>Executar um modelo de texto em seu aplicativo

Para executar um modelo de texto, chame o método ProcessTemplate de <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName>:

```csharp
using Microsoft.VisualStudio.TextTemplating;
...
Engine engine = new Engine();
string output = engine.ProcessTemplate(templateString, host);
```

 Seu aplicativo deve localizar e fornecer o modelo, e deve lidar com a saída.

 No parâmetro `host` , você deve fornecer uma classe que implementa [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110)). Isso é chamado novamente pelo mecanismo.

 O host deve ser capaz de registrar erros, resolver referências ao assembly e arquivos de inclusão, fornecer um domínio de aplicativo no qual o modelo pode executar e chamar o processador adequado para cada diretiva.

 <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName> é definido em **Microsoft.VisualStudio.TextTemplating. \*.0.dll** e [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110)) é definido em **Microsoft.VisualStudio.TextTemplating.Interfaces. \*.0.dll**.

## <a name="in-this-section"></a>Nesta seção
 [Passo a passo: criando um host de modelo de texto personalizado](../modeling/walkthrough-creating-a-custom-text-template-host.md) Mostra como criar um host de modelo de texto personalizado que disponibiliza a funcionalidade de modelo de texto fora do Visual Studio.

## <a name="reference"></a>Referência
 [Itexttemplatingenginehost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))

## <a name="related-sections"></a>Seções relacionadas

- [O Processo de Transformação Modelo de](../modeling/the-text-template-transformation-process.md) Texto descreve como funciona a transformação de texto e quais partes você pode personalizar.
- [A criação de processadores de diretiva de modelo de](../modeling/creating-custom-t4-text-template-directive-processors.md) texto T4 personalizado fornece uma visão geral dos processadores de diretiva de modelo de texto.
