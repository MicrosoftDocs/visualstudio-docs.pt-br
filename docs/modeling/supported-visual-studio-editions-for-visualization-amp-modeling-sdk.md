---
title: Edições Visual Studio suporte para visualização e modelagem do SDK
description: Saiba mais sobre as Visual Studio edições com suporte com as Ferramentas DSL nos ambientes de implantação e de autor.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, supported Visual Studio editions
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b8435f37ebe68e954af135be0f513247191ea8a9
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386391"
---
# <a name="supported-visual-studio-editions-for-visualization--modeling-sdk"></a>Edições do Visual Studio compatíveis com o SDK de Visualização e Modelagem

A seguir estão as listas das Visual Studio edições com suporte nos [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] ambientes de implantação e de autor. Para obter mais informações sobre essas edições, consulte o Microsoft Visual Studio [Developer Center](https://visualstudio.microsoft.com/).

## <a name="authoring-edition"></a>Edição de Criação

Para definir uma DSL, é necessário ter instalados os seguintes componentes:

|Produto|Link de download|
|-|-|
|Visual Studio|[http://go.microsoft.com/fwlink/?LinkId=185579](https://visualstudio.microsoft.com/)|
|SDK do Visual Studio|[http://go.microsoft.com/fwlink/?LinkId=185580](/azure/devops/integrate/index?view=azure-devops&viewFallbackFrom=vsts&preserve-view=true)|
|SDK de Visualização e Modelagem do Visual Studio|[http://go.microsoft.com/fwlink/?LinkID=186128](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)|

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="deployment-editions"></a>Edições de Implantação

[!INCLUDE[dsl](../modeling/includes/dsl_md.md)] dá suporte às seguintes configurações para implantar os idiomas específicos do domínio que você cria:

- Visual Studio Enterprise

- Visual Studio Professional

- Pacote redistribuível Visual Studio Shell (modo integrado) pacote redistribuível

- Pacote redistribuível Visual Studio Shell (modo isolado) pacote redistribuível

> [!NOTE]
> Para tornar uma DSL capaz de ser executado em um produto Shell, você deve definir o campo **Edição do VS com** suporte no Manifesto da Extensão. Para obter mais informações, confira [Implantando soluções de linguagem específica de domínio](msi-and-vsix-deployment-of-a-dsl.md).

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](/previous-versions/bb126564(v=vs.100))