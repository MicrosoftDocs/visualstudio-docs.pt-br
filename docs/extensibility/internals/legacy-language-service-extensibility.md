---
title: Extensibilidade de serviço de idioma herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services
- Visual Studio, language services
ms.assetid: 2700cd4d-5f68-43fc-b62f-dc80c3f3aa85
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: bb7d8165060fa3b9a6445ad71a977c79414056f3
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31129709"
---
# <a name="legacy-language-service-extensibility"></a>Extensibilidade de serviço de linguagem herdada
Um serviço de linguagem fornece suporte de idioma específico para a edição de código-fonte no IDE.  
  
 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações sobre a nova maneira de implementar um serviço de idioma, consulte [Editor e extensões de serviço de linguagem](../../extensibility/editor-and-language-service-extensions.md).  
  
 Esta seção discute a estrutura e a implementação de um serviço de linguagem herdada.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Migrar um serviço de linguagem herdado](../../extensibility/internals/migrating-a-legacy-language-service.md)  
 Explica como atualizar um serviço de linguagem do Visual Studio 2008 para a versão mais recente.  
  
 [Fundamentos do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-essentials.md)  
 Fornece informações importantes sobre como desenvolver serviços de linguagem para integrar uma linguagem de programação em Visual Studio.  
  
 [Desenvolver um serviço de linguagem herdado](../../extensibility/internals/developing-a-legacy-language-service.md)  
 Fornece links para tópicos que podem ajudá-lo a criar um serviço de linguagem.  
  
 [Coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)  
 Fornece informações sobre o suporte a realce de sintaxe em um serviço de linguagem.  
  
 [Implementar um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service1.md)  
 Fornece informações sobre como usar a estrutura de pacote gerenciado (MPF) para implementar um serviço de linguagem completos em código gerenciado.  
  
 [Suporte a ferramentas de navegação por símbolo](../../extensibility/internals/supporting-symbol-browsing-tools.md)  
 Descreve as bibliotecas e ferramentas que permitem que você navegue em modos de exibição de árvore de símbolos no IDE.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Editor e extensões do serviço de linguagem](../../extensibility/editor-and-language-service-extensions.md)  
 Fornece uma visão geral dos editores do Visual Studio.  
  
 [Suporte do serviço de linguagem para depuração](../../extensibility/internals/language-service-support-for-debugging.md)  
 Fornece informações sobre e um link para a depuração de SDK do Visual Studio, que contém as informações necessárias para criar e personalizar os componentes do depurador usados para depurar programas.