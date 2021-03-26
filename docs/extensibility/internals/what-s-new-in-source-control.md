---
title: O que há de novo no controle do código-fonte no SDK do Visual Studio 2015 | Microsoft Docs
description: Saiba mais sobre os recursos do VSPackages de controle do código-fonte e examine uma visão geral das etapas de implementação.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio SDK], source control
- source control [Visual Studio SDK], what's new
ms.assetid: bcf85418-18fb-4824-9dae-d14bf3d56a77
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: da10750629fcdae66ab8456b3074c07f44e3cf05
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069056"
---
# <a name="whats-new-in-source-control-for-the-visual-studio-2015-sdk"></a>O que há de novo no controle do código-fonte para o SDK do Visual Studio 2015

No [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] , você pode fornecer uma solução de controle do código-fonte profundamente integrada implementando um VSPackage de controle do código-fonte. Esta seção descreve os recursos do VSPackages de controle do código-fonte e fornece uma visão geral das etapas de implementação.

## <a name="the-source-control-vspackage"></a>O controle do código-fonte VSPackage

O Visual Studio dá suporte a dois tipos de soluções de controle do código-fonte. Em todas as versões do Visual Studio, você ainda pode integrar um plug-in baseado em API de plug-in de controle do código-fonte. Você também pode criar um VSPackage para controle do código-fonte que fornece uma integração profunda, [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] caminho adequado para soluções de controle do código-fonte que exigem um alto nível de sofisticação e autonomia.

Um VSPackage pode adicionar praticamente qualquer tipo de funcionalidade ao Visual Studio. Um VSPackage de controle do código-fonte fornece um recurso de controle do código-fonte completo para o Visual Studio, da interface do usuário apresentada para a comunicação back-end com o sistema de controle do código-fonte.

A implementação de um VSPackage de controle do código-fonte requer uma estratégia "tudo ou nada". O criador de um VSPackage de controle do código-fonte deve investir uma quantidade significativa de esforço na implementação de várias interfaces de controle do código-fonte e novos elementos da interface do usuário (caixas de diálogo, menus e barras de ferramentas) para cobrir toda a funcionalidade de controle do código-fonte, bem como interfaces necessárias de qualquer pacote para integração com o Visual Studio.

As etapas a seguir fornecem uma visão geral do que é necessário para implementar um pacote de controle do código-fonte. Para obter detalhes, consulte [criando um controle do código-fonte VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md).

1. Crie um VSPackage que proffers um serviço de controle do código-fonte privado.

2. Implemente as interfaces nos serviços relacionados ao controle do código-fonte que são proffered pelo Visual Studio (por exemplo, a <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> e a <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider> interface).

3. Registre seu VSPackage de controle do código-fonte.

4. Implemente toda a interface do usuário do controle do código-fonte, incluindo itens de menu, caixas de diálogo, barras de ferramentas e menus de contexto.

5. Todos os eventos relacionados ao controle do código-fonte são passados para o VSackage de controle do código-fonte quando ele está ativo e devem ser tratados pelo seu VSPackage.

6. O VSPackage de controle do código-fonte deve escutar eventos como aqueles que implementam a <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> interface, bem como controlar os eventos de documento do projeto (TPD) (conforme implementado pela <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> interface) e tomar a ação necessária.

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- [Visão geral](../../extensibility/internals/source-control-integration-overview.md)
- [Criar um VSPackage de controle do código-fonte](../../extensibility/internals/creating-a-source-control-vspackage.md)
