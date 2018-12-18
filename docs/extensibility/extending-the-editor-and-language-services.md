---
title: Estender o Editor e os serviços de linguagem | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new -
ms.assetid: 8d04f8db-eda7-4b3e-b6eb-c06df104502a
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 7194b245ad3803112f5596c82308c384840d7bdf
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39637543"
---
# <a name="extend-the-editor-and-language-services"></a>Estender os serviços do editor e linguagem
Você pode adicionar recursos de serviço de linguagem (como o IntelliSense) para o seu próprio editor e estender a maioria dos recursos do editor de código do Visual Studio.  Para obter uma lista completa de como você pode estender, consulte [pontos de extensão de editor e o serviço de linguagem](../extensibility/language-service-and-editor-extension-points.md).  
  
 Usando o Managed Extensibility Framework (MEF) para estender a maioria dos recursos do editor. Por exemplo, se o recurso de editor que você deseja estender coloração de sintaxe, você pode escrever um MEF *parte do componente* que define as classificações para o qual você deseja cores diferentes e como eles devem ser tratados. O editor também dá suporte a várias extensões do mesmo recurso.  
  
 A camada de apresentação do editor baseia-se o Windows Presentation Framework (WPF). WPF fornece uma biblioteca de elementos gráficos para formatação de texto flexível e também fornece visualizações como gráficos e animações.  
  
 O SDK do Visual Studio fornece adaptadores conhecidos como *shims* para dar suporte a VSPackages que foram escritos para versões anteriores. No entanto, se você tiver um VSPackage existente, recomendamos que você atualize para a nova tecnologia para obter melhor desempenho e confiabilidade.  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Introdução a extensões de editor e o serviço de linguagem](../extensibility/getting-started-with-language-service-and-editor-extensions.md)|Explica como criar uma extensão do editor.|  
|[Dentro do editor](../extensibility/inside-the-editor.md)|Descreve a estrutura geral do editor e lista alguns dos seus recursos.|  
|[Managed Extensibility Framework no editor](../extensibility/managed-extensibility-framework-in-the-editor.md)|Explica como usar o MEF Managed Extensibility Framework () com o editor.|  
|[Pontos de extensão de editor e o serviço de linguagem](../extensibility/language-service-and-editor-extension-points.md)|Lista os pontos de extensão do editor. Pontos de extensão representam os recursos do editor que podem ser estendidos.|  
|[Passo a passo: Criar um adorno de exibição, comandos e configurações (guias de coluna)](../extensibility/walkthrough-creating-a-view-adornment-commands-and-settings-column-guides.md)|Percorre e explica a criação de um adorno de exibição que desenha linhas guia de coluna para ajudar a manter o código para uma determinada largura de exibição.  Também mostra lendo e gravando configurações, bem como declarar e implementar comandos que você pode invocar da janela de comando.|  
|[Importações do Editor](../extensibility/editor-imports.md)|Lista os serviços que uma extensão pode ser importado.|  
|[Adaptar o código herdado para o editor](../extensibility/adapting-legacy-code-to-the-editor.md)|Explica as diferentes maneiras de se adaptar (pré-Visual Studio 2010) para estender o editor de código herdado.|  
|[Migrar um serviço de linguagem herdado](../extensibility/internals/migrating-a-legacy-language-service.md)|Explica como migrar um serviço de linguagem de VSPackage com base.|  
|[Passo a passo: Vincular um tipo de conteúdo para uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)|Mostra como vincular um tipo de conteúdo para uma extensão de nome de arquivo.|  
|[Passo a passo: Criar um glifo de margem](../extensibility/walkthrough-creating-a-margin-glyph.md)|Mostra como adicionar um ícone para uma margem.|  
|[Passo a passo: Realçar texto](../extensibility/walkthrough-highlighting-text.md)|Mostra como usar *marcas* para realçar o texto.|  
|[Passo a passo: Adicionar a estrutura de tópicos](../extensibility/walkthrough-outlining.md)|Mostra como adicionar a estrutura de tópicos para tipos específicos de chaves.|  
|[Passo a passo: Exibir chaves correspondentes](../extensibility/walkthrough-displaying-matching-braces.md)|Mostra como destacar chaves correspondentes.|  
|[Passo a passo: Dicas de ferramenta de QuickInfo vídeo](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)|Mostra como exibir o pop-ups QuickInfo que descrevem os elementos de código como propriedades, métodos e eventos.|  
|[Passo a passo: Exibir Ajuda de assinatura](../extensibility/walkthrough-displaying-signature-help.md)|Mostra como exibir o pop-ups que fornecem informações sobre o número e tipos de parâmetros em uma assinatura.|  
|[Passo a passo: exibir preenchimento de declaração](../extensibility/walkthrough-displaying-statement-completion.md)|Mostra como implementar a conclusão da instrução.|  
|[Passo a passo: Trechos de código de implementação](../extensibility/walkthrough-implementing-code-snippets.md)|Mostra como implementar a expansão de trecho de código.|  
|[Passo a passo: Exibir sugestões de lâmpada](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)|Mostra como exibir as lâmpadas para sugestões de código.|  
|[Passo a passo: Usar um comando de shell com uma extensão do editor](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)|Mostra como associar um comando de menu em um VSPackage com um componente MEF.|  
|[Passo a passo: Usar uma tecla de atalho com uma extensão do editor](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)|Mostra como associar um atalho de menu em um VSPackage com um componente MEF.|  
|[MEF (Managed Extensibility Framework)](/dotnet/framework/mef/index)|Fornece informações sobre o MEF Managed Extensibility Framework ().|  
|[Windows Presentation Foundation](/dotnet/framework/wpf/index)|Fornece informações sobre o Windows Presentation Foundation (WPF).|  
  
## <a name="reference"></a>Referência  
 Editor do Visual Studio inclui os seguintes namespaces.  
  
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