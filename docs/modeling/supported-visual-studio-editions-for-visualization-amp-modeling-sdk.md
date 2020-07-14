---
title: Edições do Visual Studio com suporte para o SDK de visualização e modelagem
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, supported Visual Studio editions
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3be233ce8730879c2f0406ec9cc180685992c6bf
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544931"
---
# <a name="supported-visual-studio-editions-for-visualization--modeling-sdk"></a>Edições do Visual Studio compatíveis com o SDK de Visualização e Modelagem

Veja a seguir as listas das edições do Visual Studio com suporte [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] no nos ambientes de criação e implantação. Para obter mais informações sobre essas edições, consulte o Microsoft Visual Studio [Developer Center](https://visualstudio.microsoft.com/).

## <a name="authoring-edition"></a>Edição de Criação

Para definir uma DSL, é necessário ter instalados os seguintes componentes:

|Produto|Link de download|
|-|-|
|Visual Studio|[http://go.microsoft.com/fwlink/?LinkId=185579](https://visualstudio.microsoft.com/)|
|SDK do Visual Studio|[http://go.microsoft.com/fwlink/?LinkId=185580](/azure/devops/integrate/index?view=azure-devops&viewFallbackFrom=vsts)|
|SDK de Visualização e Modelagem do Visual Studio|[http://go.microsoft.com/fwlink/?LinkID=186128](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)|

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="deployment-editions"></a>Edições de Implantação

[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]o oferece suporte às seguintes configurações para implantar as linguagens específicas de domínio que você cria:

- Visual Studio Enterprise

- Visual Studio Professional

- Pacote redistribuível Visual Studio Shell (modo integrado) pacote redistribuível

- Pacote redistribuível Visual Studio Shell (modo isolado) pacote redistribuível

> [!NOTE]
> Para tornar uma DSL capaz de executar em um produto de Shell, você deve definir o campo **com suporte do vs Edition** no manifesto de extensão. Para obter mais informações, confira [Implantando soluções de linguagem específica de domínio](msi-and-vsix-deployment-of-a-dsl.md).

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
