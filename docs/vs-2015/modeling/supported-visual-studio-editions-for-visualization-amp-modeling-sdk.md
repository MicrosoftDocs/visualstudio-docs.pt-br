---
title: Edições do Visual Studio com suporte para visualização e SDK de modelagem | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, supported Visual Studio editions
ms.assetid: 7c313ba0-031d-45b8-8220-eead61754747
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3eebefeab6b78955b03d4546a60dd811f5e9ae4e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547648"
---
# <a name="supported-visual-studio-editions-for-visualization-amp-modeling-sdk"></a>Visual Studio Editions para SDK de modelagem de visualização com suporte &amp;
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Veja a seguir as listas das edições do Visual Studio com suporte [!INCLUDE[dsl](../includes/dsl-md.md)] no nos ambientes de criação e implantação. Para obter mais informações sobre essas edições, consulte o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] [centro de desenvolvedores](https://msdn.microsoft.com/vstudio/products/)da Microsoft.

## <a name="authoring-edition"></a>Edição de Criação
 Para definir uma DSL, é necessário ter instalados os seguintes componentes:

|Produto|Link de download|
|-|-|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[https://www.visualstudio.com/](https://www.visualstudio.com/)|
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[SDK do Visual Studio](../extensibility/visual-studio-sdk.md)|
|SDK de Visualização e Modelagem do Visual Studio|[Download do SDK de modelagem](https://www.microsoft.com/download/details.aspx?id=48148)|
## <a name="deployment-editions"></a>Edições de Implantação
 [!INCLUDE[dsl](../includes/dsl-md.md)]o oferece suporte às seguintes configurações para implantar as linguagens específicas de domínio que você cria:

- Visual Studio Enterprise

- Visual Studio Professional

- Pacote redistribuível Visual Studio Shell (modo integrado) pacote redistribuível

- Pacote redistribuível Visual Studio Shell (modo isolado) pacote redistribuível

> [!NOTE]
> Para tornar uma DSL capaz de executar em um produto de Shell, você deve definir o campo **com suporte do vs Edition** no manifesto de extensão. Para obter mais informações, confira [Implantando soluções de linguagem específica de domínio](../modeling/deploying-domain-specific-language-solutions.md).

## <a name="see-also"></a>Consulte Também
 [Glossário das Ferramentas de Linguagem Específica de Domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
