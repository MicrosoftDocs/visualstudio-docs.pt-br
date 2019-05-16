---
title: Suporte para edições do Visual Studio para visualização e o SDK de modelagem | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, supported Visual Studio editions
ms.assetid: 7c313ba0-031d-45b8-8220-eead61754747
caps.latest.revision: 29
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a8104eb9aa2d340545fb4cbfbd2e46286d953375
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696873"
---
# <a name="supported-visual-studio-editions-for-visualization-amp-modeling-sdk"></a>Suporte para edições do Visual Studio para visualização &amp; SDK de modelagem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Seguem listas das edições do Visual Studio que têm suporte com [!INCLUDE[dsl](../includes/dsl-md.md)] nos ambientes de criação e implantação. Para obter mais informações sobre essas edições, consulte o Microsoft [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] [Developer Center](http://go.microsoft.com/fwlink/?LinkId=75628).

## <a name="authoring-edition"></a>Edição de Criação
 Para definir uma DSL, é necessário ter instalados os seguintes componentes:

|||
|-|-|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[http://go.microsoft.com/fwlink/?LinkId=185579](http://go.microsoft.com/fwlink/?LinkId=185579)|
|SDK do Visual Studio|[http://go.microsoft.com/fwlink/?LinkId=185580](http://go.microsoft.com/fwlink/?LinkId=185580)|
|SDK de Visualização e Modelagem do Visual Studio|[http://go.microsoft.com/fwlink/?LinkID=186128](http://go.microsoft.com/fwlink/?LinkID=186128)|

## <a name="deployment-editions"></a>Edições de Implantação
 [!INCLUDE[dsl](../includes/dsl-md.md)] oferece suporte às seguintes configurações para implantação das linguagens específicas do domínio que foram compiladas:

- Visual Studio Enterprise

- Visual Studio Professional

- Pacote redistribuível do Visual Studio Shell (modo integrado) pacote redistribuível

- Pacote redistribuível Visual Studio Shell (modo isolado) pacote redistribuível

> [!NOTE]
> Para tornar uma DSL capaz de executar em um produto Shell, você deve definir a **suporte para a edição do VS** campo no manifesto de extensão. Para obter mais informações, confira [Implantando soluções de linguagem específica de domínio](../modeling/deploying-domain-specific-language-solutions.md).

## <a name="see-also"></a>Consulte também
 [Glossário das Ferramentas de Linguagem Específica de Domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
