---
title: Sintaxe do caminho de domínio
description: Saiba mais sobre a sintaxe do caminho de domínio e como as definições de DSL usam uma sintaxe semelhante a XPath para localizar elementos específicos em um modelo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, domain path
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 69dfd02dca5ead65d4f36303e547aaeba04cde98
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389092"
---
# <a name="domain-path-syntax"></a>Sintaxe do caminho de domínio
As definições de DSL usam uma sintaxe semelhante a XPath para localizar elementos específicos em um modelo.

 Normalmente, não é necessário trabalhar com essa sintaxe diretamente. Caso ela aparecer na janela Detalhes de DSL ou Propriedades, você pode clicar na seta para baixo e usar o editor de caminho. No entanto, o caminho aparecerá nesta forma no campo depois de você ter usado o editor.

 Um caminho de domínio tem a seguinte forma:

 *RelationshipName.PropertyName/!Role*

 ![Relação de referência de CommentReferencesSubjects](../modeling/media/dsl_reference.png)

 A sintaxe percorre a árvore do modelo. Por exemplo, a relação de domínio **CommentReferencesSubjects** na ilustração acima tem uma função **Subjects** . O segmento de caminho **/! Subject** especifica que o caminho termina em elementos acessados por meio da função **Subjects** .

 Cada segmento inicia com o nome de uma relação de domínio. Se a passagem for de um elemento para uma relação, o segmento de caminho aparecerá como *relationship. PropertyName*. Se o salto for de um link para um elemento, o segmento de caminho aparecerá como *relationship/! RoleName*.

 Barras separam a sintaxe de um caminho. Cada segmento de caminho é um salto de um elemento para um link (uma instância de uma relação) ou de um link para um elemento. Os segmentos de caminho normalmente aparecem em pares. Um segmento de caminho representa um salto de um elemento para um link e o próximo segmento representa um salto do link para o elemento na outra extremidade. (Qualquer link também pode ser a origem ou destino de uma relação).

 O nome que você usa para o salto do elemento ao link é o valor de `Property Name` da função. O nome que você usa para o salto do link ao elemento é o nome da função de destino.

## <a name="see-also"></a>Confira também

- [Noções básicas sobre modelos, classes e relações](../modeling/understanding-models-classes-and-relationships.md)
