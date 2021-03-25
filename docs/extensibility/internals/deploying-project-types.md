---
title: Implantando tipos de projeto | Microsoft Docs
description: Saiba como implantar tipos de projeto de código gerenciado usando um novo agregador de tipo de projeto e Windows Installer pacote para redistribuição, no SDK do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], managed-code
- projects [Visual Studio SDK], aggregator
ms.assetid: 7f132f67-8589-464c-90dc-0d57ae02aa8f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 121dda58b8e01c5b0029d8b3c93ef66d2657446e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090974"
---
# <a name="deploy-project-types"></a>Implantar tipos de projeto
[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] instala um novo agregador de tipo de projeto (*ProjectAggregator2.dll*) e também um pacote Windows Installer para redistribuição (*ProjectAggregator2.msi*). Você deve usar o novo agregador para tipos de projeto de código gerenciado. ProjectAggregator2 trabalha em relação às limitações no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] agregador de projeto que impede que os tipos de projeto de código gerenciado funcionem corretamente. As etapas a seguir descrevem como alterar seu VSPackage para usar o novo agregador.

1. Remova o projeto NativeHierarchyWrapper da sua solução.

2. Remova todos os binários do NativeHierarchyWrapper da sua configuração.

3. Adicione *ProjectAggregator2.msi* à sua instalação.
