---
title: Estendendo o editor e os serviços de linguagem | Microsoft Docs
description: Você pode adicionar recursos de serviço de linguagem a um editor e estender recursos do editor de código do Visual Studio. Saiba mais sobre o Managed Extensibility Framework.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new -
ms.assetid: 8d04f8db-eda7-4b3e-b6eb-c06df104502a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8d85b018b4e0ea7d5ed1c91e617afcb2759d49b8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070109"
---
# <a name="extend-the-editor-and-language-services"></a>Estenda os serviços de editor e linguagem
Você pode adicionar recursos de serviço de linguagem (como IntelliSense) ao seu próprio editor e estender a maioria dos recursos do editor de código do Visual Studio.  Para obter uma lista completa do que você pode estender, consulte [serviço de linguagem e pontos de extensão do editor](../extensibility/language-service-and-editor-extension-points.md).

 Você estende a maioria dos recursos do editor usando o Managed Extensibility Framework (MEF). Por exemplo, se o recurso do editor que você deseja estender é a cor da sintaxe, você pode escrever uma *parte do componente* do MEF que define as classificações para as quais você deseja cores diferentes e como deseja que elas sejam manipuladas. O editor também dá suporte a várias extensões do mesmo recurso.

 A camada de apresentação do editor é baseada no Windows Presentation Framework (WPF). O WPF fornece uma biblioteca de gráficos para formatação de texto flexível e também fornece visualizações como gráficos e animações.

 O SDK do Visual Studio fornece adaptadores conhecidos como *shims* para dar suporte a VSPackages que foram escritos para versões anteriores. No entanto, se você tiver um VSPackage existente, recomendamos atualizá-lo para a nova tecnologia para obter melhor desempenho e confiabilidade.

## <a name="related-topics"></a>Tópicos relacionados

|Título|Descrição|
|-----------|-----------------|
|[Introdução ao serviço de linguagem e às extensões do editor](../extensibility/getting-started-with-language-service-and-editor-extensions.md)|Explica como criar uma extensão para o editor.|
|[Dentro do editor](../extensibility/inside-the-editor.md)|Descreve a estrutura geral do editor e lista alguns de seus recursos.|
|[Managed Extensibility Framework no editor](../extensibility/managed-extensibility-framework-in-the-editor.md)|Explica como usar o Managed Extensibility Framework (MEF) com o editor.|
|[Pontos de extensão do serviço de linguagem e do editor](../extensibility/language-service-and-editor-extension-points.md)|Lista os pontos de extensão do editor. Os pontos de extensão representam os recursos do editor que podem ser estendidos.|
|[Walkthrough: criar uma exibição Adornment, comandos e configurações (guias de coluna)](../extensibility/walkthrough-creating-a-view-adornment-commands-and-settings-column-guides.md)|Percorre e explica como criar um Adornment de exibição que desenha linhas de guia de coluna para ajudá-lo a manter o código para uma determinada largura de exibição.  Também mostra as configurações de leitura e gravação, bem como a declaração e a implementação de comandos que você pode invocar na janela de comando.|
|[Importações do editor](../extensibility/editor-imports.md)|Lista os serviços que uma extensão pode importar.|
|[Adaptar o código herdado ao editor](/previous-versions/visualstudio/visual-studio-2015/extensibility/adapting-legacy-code-to-the-editor?preserve-view=true&view=vs-2015)|Explica diferentes maneiras de adaptar o código herdado (pré-Visual Studio 2010) para estender o editor.|
|[Migrar um serviço de linguagem herdado](../extensibility/internals/migrating-a-legacy-language-service.md)|Explica como migrar um serviço de linguagem baseado em VSPackage.|
|[Walkthrough: vincular um tipo de conteúdo a uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)|Mostra como vincular um tipo de conteúdo a uma extensão de nome de arquivo.|
|[Walkthrough: criar um glifo de margem](../extensibility/walkthrough-creating-a-margin-glyph.md)|Mostra como adicionar um ícone a uma margem.|
|[Walkthrough: realçar texto](../extensibility/walkthrough-highlighting-text.md)|Mostra como usar *marcas* para realçar o texto.|
|[Walkthrough: adicionar estrutura de tópicos](../extensibility/walkthrough-outlining.md)|Mostra como adicionar estrutura de tópicos para tipos específicos de chaves.|
|[Walkthrough: Exibir chaves correspondentes](../extensibility/walkthrough-displaying-matching-braces.md)|Mostra como realçar chaves correspondentes.|
|[Walkthrough: Exibir dicas de ferramenta QuickInfo](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)|Mostra como exibir pop-ups QuickInfo que descrevem elementos de código como propriedades, métodos e eventos.|
|[Walkthrough: exibir a ajuda da assinatura](../extensibility/walkthrough-displaying-signature-help.md)|Mostra como exibir pop-ups que fornecem informações sobre o número e os tipos de parâmetros em uma assinatura.|
|[Passo a passo: exibir preenchimento de declaração](../extensibility/walkthrough-displaying-statement-completion.md)|Mostra como implementar a conclusão da instrução.|
|[Walkthrough: implementar trechos de código](../extensibility/walkthrough-implementing-code-snippets.md)|Mostra como implementar a expansão de trecho de código.|
|[Walkthrough: Exibir sugestões de lâmpada](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)|Mostra como exibir lâmpadas claras para sugestões de código.|
|[Walkthrough: usar um comando do shell com uma extensão do editor](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)|Mostra como associar um comando de menu em um VSPackage com um componente MEF.|
|[Walkthrough: usar uma tecla de atalho com uma extensão do editor](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)|Mostra como associar um atalho de menu em um VSPackage com um componente MEF.|
|[MEF (Managed Extensibility Framework)](/dotnet/framework/mef/index)|Fornece informações sobre o Managed Extensibility Framework (MEF).|
|[Windows Presentation Foundation](/dotnet/framework/wpf/index)|Fornece informações sobre o Windows Presentation Foundation (WPF).|

## <a name="reference"></a>Referência
 O editor do Visual Studio inclui os namespaces a seguir.

 <xref:Microsoft.VisualStudio.Language.Intellisense>

 <xref:Microsoft.VisualStudio.Language.StandardClassification>

 <xref:Microsoft.VisualStudio.Editor>

 <xref:Microsoft.VisualStudio.Text>

 <xref:Microsoft.VisualStudio.Text.Adornments>

 <xref:Microsoft.VisualStudio.Text.Classification>

 <xref:Microsoft.VisualStudio.Text.Differencing>

 <xref:Microsoft.VisualStudio.Text.Document>

 <xref:Microsoft.VisualStudio.Text.Editor>

 <xref:Microsoft.VisualStudio.Text.Editor.OptionsExtensionMethods>

 <xref:Microsoft.VisualStudio.Text.Formatting>

 <xref:Microsoft.VisualStudio.Text.IncrementalSearch>

 <xref:Microsoft.VisualStudio.Text.Operations>

 <xref:Microsoft.VisualStudio.Text.Outlining>

 <xref:Microsoft.VisualStudio.Text.Projection>

 <xref:Microsoft.VisualStudio.Text.Tagging>

 <xref:Microsoft.VisualStudio.Utilities>