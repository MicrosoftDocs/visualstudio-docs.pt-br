---
title: Extensões do editor e do serviço de linguagem | Microsoft Docs
description: Você pode estender a maioria dos recursos do editor de código do Visual Studio, que é implementado usando Windows Presentation Foundation e é escrito em código gerenciado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK]
ms.assetid: 5653bac9-724f-4948-a820-68ce6aa96365
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 194fb7f159123b97ab1bb866b3c834320dd4bd88
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070317"
---
# <a name="editor-and-language-service-extensions"></a>Extensões do editor e do serviço de linguagem
Você pode estender a maioria dos recursos do editor de código do Visual Studio. O editor é baseado no Windows Presentation Foundation (WPF) e é escrito em código gerenciado. Embora esse design seja diferente dos projetos em versões anteriores do Visual Studio, ele fornece a maioria dos mesmos recursos. Para estender o editor, use o Managed Extensibility Framework (MEF).

 O SDK do Visual Studio fornece adaptadores conhecidos como *shims* para dar suporte a VSPackages que foram escritos para versões anteriores. No entanto, se você tiver um VSPackage existente, recomendamos atualizá-lo para a nova tecnologia para obter melhor desempenho e confiabilidade.

## <a name="related-topics"></a>Tópicos relacionados

|Título|Descrição|
|-----------|-----------------|
|[Criar uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md)|Introdução ao uso dos modelos de item do editor.|
|[Estenda os serviços de editor e linguagem](../extensibility/extending-the-editor-and-language-services.md)|Links para documentos que introduzem o design e os recursos do editor principal e mostram como estendê-lo.|
|[Interfaces herdadas no editor](/previous-versions/visualstudio/visual-studio-2015/extensibility/legacy-interfaces-in-the-editor?preserve-view=true&view=vs-2015)|Links para documentos que explicam como acessar o editor principal do código existente.|
|[Criar editores e designers personalizados](../extensibility/creating-custom-editors-and-designers.md)|Links para documentos que explicam como criar editores personalizados.|
|[Extensibilidade do serviço de linguagem herdada](../extensibility/internals/legacy-language-service-extensibility.md)|Links para documentos que descrevem como integrar linguagens de programação ao Visual Studio.|
|[MEF (Managed Extensibility Framework)](/dotnet/framework/mef/index)|Apresenta o Managed Extensibility Framework (MEF).|
|[Windows Presentation Foundation](/dotnet/framework/wpf/index)|Apresenta o Windows Presentation Foundation (WPF).|
