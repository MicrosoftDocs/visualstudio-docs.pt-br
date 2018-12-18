---
title: Implantar tipos de projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], managed-code
- projects [Visual Studio SDK], aggregator
ms.assetid: 7f132f67-8589-464c-90dc-0d57ae02aa8f
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4bed37260925d4961ed5b5b7d3e69d55169444ad
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39497895"
---
# <a name="deploy-project-types"></a>Implantar tipos de projeto
[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] instala um novo agregador do tipo de projeto (*ProjectAggregator2.dll*) e também um pacote do Windows Installer para redistribuição (*ProjectAggregator2.msi*). Você deve usar o novo agregador para tipos de projeto de código gerenciado. ProjectAggregator2 funciona com limitações no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] projeto agregador que impede que os tipos de projeto de código gerenciado de funcionar corretamente. As etapas a seguir descrevem como alterar o VSPackage para usar o novo agregador.  
  
1.  Remova o projeto de NativeHierarchyWrapper da sua solução.  
  
2.  Remova os binários do NativeHierarchyWrapper de sua configuração.  
  
3.  Adicione *ProjectAggregator2.msi* à sua instalação.