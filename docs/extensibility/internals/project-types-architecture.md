---
title: Arquitetura de tipos de projeto | Microsoft Docs
description: Este artigo contém links para artigos que contêm informações detalhadas sobre a arquitetura de tipos de projeto no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], architecture
ms.assetid: 9c1d940f-8a54-41f7-a8aa-c870e324371c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4b03ca1db09df7176eb52d5c8141bf87b1637d79
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064261"
---
# <a name="project-types-architecture"></a>Arquitetura de tipos de projeto
Esta seção contém informações detalhadas sobre a arquitetura dos tipos de projeto no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

## <a name="in-this-section"></a>Nesta seção
- [Elementos de um modelo de projeto](../../extensibility/internals/elements-of-a-project-model.md)

 Lista os serviços que um tipo de projeto pode consumir e as interfaces que ele deve implementar.

- [Componentes principais do projeto modelo](../../extensibility/internals/project-model-core-components.md)

 Descreve as interfaces que os tipos de projeto devem implementar e, opcionalmente, podem implementar para fornecer funcionalidade adicional.

- [Quando criar tipos de projeto](../../extensibility/internals/when-to-create-project-types.md)

 Ajuda a decidir quando você deve criar um tipo de projeto e quando você pode usar outro [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] recurso de extensibilidade, como VSPackages e editores para atingir o mesmo objetivo.

- [Hierarquias e seleção](../../extensibility/internals/hierarchies-and-selection.md)

 Descreve como o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usa hierarquias e contexto de seleção para fornecer uma experiência de usuário consistente e simplificada.

## <a name="related-sections"></a>Seções relacionadas
- [Subtipos de projeto](../../extensibility/internals/project-subtypes.md)

 Explica como os subtipos de projeto permitem personalizar o comportamento dos sistemas de projeto do [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] e do [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] .

- [Tipos de Projeto](../../extensibility/internals/project-types.md)

 Fornece uma visão geral dos projetos como os blocos de construção básicos do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE (ambiente de desenvolvimento integrado). São fornecidos links para tópicos adicionais que explicam como os projetos controlam a criação e a compilação de código.
