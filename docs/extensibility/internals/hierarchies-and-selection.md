---
title: Hierarquias e seleção | Microsoft Docs
description: Saiba como o Visual Studio lida com hierarquias, como projetos, e como ele usa o contexto de seleção para determinar o que é exibido para o usuário.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, hierarchies
- selection
- hierarchies
ms.assetid: cad0a859-7a84-4ce5-b0a9-f7f64e5f8ebb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 927d55a5217699222aadcbcb7a3526f22e010e8f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074724"
---
# <a name="hierarchies-and-selection"></a>Hierarquias e seleção
Ao personalizar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o, você deve entender como o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] lida com hierarquias como projetos e como ele usa o contexto de seleção para determinar o que é exibido para o usuário. Esta seção aborda os conceitos de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] hierarquias e seleção.

## <a name="in-this-section"></a>Nesta seção
- [Hierarquias no Visual Studio](../../extensibility/internals/hierarchies-in-visual-studio.md)

 Descreve as hierarquias de projeto e o conceito geral de hierarquias.

- [Seleção e moeda no IDE](../../extensibility/internals/selection-and-currency-in-the-ide.md)

 Descreve como o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente de desenvolvimento integrado (IDE) mantém informações sobre os objetos ativos do usuário atualmente e permite que o VSPackages acompanhe a moeda.

- [Objetos de contexto de seleção](../../extensibility/internals/selection-context-objects.md)

 Discute o modelo de como você pode determinar o foco de contexto de seleção do usuário em uma janela.

- [Comentários para o usuário](../../extensibility/internals/feedback-to-the-user.md)

 Discute como a funcionalidade disponível no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] é baseada no contexto de seleção atual do usuário e no contexto geral do IDE.

## <a name="related-sections"></a>Seções relacionadas
- [Arquitetura de tipos de projeto](../../extensibility/internals/project-types-architecture.md)

 Fornece informações técnicas detalhadas sobre os tipos de projeto.
