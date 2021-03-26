---
title: Visão geral do modelo de automação | Microsoft Docs
description: Saiba mais sobre o modelo de automação do Visual Studio que consiste em um conjunto de objetos em que você pode escrever um suplemento ou uma extensão do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], about automation
- extensibility
ms.assetid: 12b6d6db-0d22-4aaa-aa7d-1365f759b7b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d763fea140ddac1b4dba955421c563700373dc22
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086229"
---
# <a name="automation-model-overview"></a>Visão geral do modelo de automação
O modelo de automação consiste em um conjunto de objetos em que é possível escrever um suplemento ou uma extensão do Visual Studio. Um suplemento é um aplicativo que pode manipular o ambiente do Visual Studio e automatizar tarefas comuns. Uma extensão do Visual Studio pode criar componentes personalizados do Visual Studio ou adicionar à funcionalidade de componentes padrão, como o editor de texto.

## <a name="objects-in-the-automation-model"></a>Objetos no modelo de automação
 O modelo de automação consiste em grupos de objetos relacionados que controlam as principais facetas do ambiente comum. O diagrama a seguir mostra o amplo conjunto de objetos do Visual Studio que compõem o modelo de automação.

 ![Gráfico de objeto de automação do Visual Studio](../../extensibility/internals/media/vsvisualstudioautomationobjectchart.gif "vsVisualStudioAutomationObjectChart")

 Para obter mais informações, consulte [estender o ambiente do Visual Studio](/previous-versions/esk3eey8(v=vs.140)).

 O ambiente fornece um modelo para diferentes áreas funcionais. Por exemplo, há um modelo de código para vários elementos que você pode encontrar no código. Há um modelo de documento para vários elementos de documento. Uma área, a área do projeto, é de interesse particular para os provedores de VSPackage. Você provavelmente desejará que seus novos tipos de projeto contribuam para o modelo de automação da mesma forma que [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] e [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] contribuem para o modelo de automação. Esse processo é descrito em [fornecer automação para VSPackages](../../extensibility/internals/providing-automation-for-vspackages.md).

 Locais onde você pode considerar a extensão do modelo de automação do ambiente:

- Project

- Documento

- Código

- Build

Para obter mais informações sobre automação, consulte [automação e extensibilidade para o Visual Studio](/previous-versions/visualstudio/visual-studio-2015/extensibility/extensibility-in-visual-studio?preserve-view=true&view=vs-2015). Este documento e os documentos aos quais ele fornece links, ajudam você a tomar decisões sobre como você deve fornecer automação para seu VSPackage.

## <a name="see-also"></a>Confira também
- [Como: criar um suplemento](/previous-versions/80493a3w(v=vs.140))