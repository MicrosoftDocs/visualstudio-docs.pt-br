---
title: Propriedades de relacionamentos de domínio
description: Saiba mais sobre as propriedades associadas a uma casa de relações de domínio, como Modificador de Acesso, Atributos Personalizados e Gera Derivada Dupla.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain relationships
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fc92bbc32a454208f3d455734b7697a2e69037b4
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390653"
---
# <a name="properties-of-domain-relationships"></a>Propriedades de relacionamentos de domínio
As propriedades na tabela a seguir estão associadas a uma relação de domínio. Para obter informações sobre relações de domínio, consulte [Noções básicas sobre modelos, classes e relações.](../modeling/understanding-models-classes-and-relationships.md) Para obter mais informações sobre como usar essas propriedades, consulte [Personalização](../modeling/customizing-and-extending-a-domain-specific-language.md)e extensão de uma linguagem Domain-Specific .

|Propriedade|Descrição|Padrão|
|-|-|-|
|Modificador de acesso|O nível de acesso da relação de domínio ( `public` ou `internal` ).|`public`|
|Atributos personalizados|Usado para adicionar atributos à classe de código-fonte gerada a partir da relação de domínio.|\<none>|
|Gera derivada dupla|Se , uma classe base e uma classe parcial (para dar suporte à personalização por meio de `True` substituições) são geradas. Para obter mais informações, [consulte Substituindo e estendendo as classes geradas.](../modeling/overriding-and-extending-the-generated-classes.md)|`False`|
|Tem construtor personalizado|Se `True` , indicará que um construtor personalizado é fornecido no código-fonte. Para obter mais informações, [consulte Substituindo e estendendo as classes geradas.](../modeling/overriding-and-extending-the-generated-classes.md)|`False`|
|Modificador de herança|Descreve o tipo de herança da classe de código-fonte gerada a partir da relação de domínio ( `none` ou `abstract` `sealed` ).|\<none>|
|Permite duplicatas|Se `True` , links duplicados da relação de domínio poderão ser criados entre os mesmos dois elementos.|`False`|
|Relações base|Se a relação de domínio for derivada, a relação base da relação de domínio.|\<none>|
|Está incorporando|Se `True` , a relação de domínio será uma relação de incorporação. Se `False` , a relação será uma relação de referência.|\<both>|
|Name|O nome da relação de domínio.|Nome atual|
|Namespace|O namespace que é afiliado à relação de domínio.|Namespace atual|
|Observações|Observações informais associadas à relação de domínio.|\<none>|
|Descrição|A descrição usada para documentar o código e é usada na interface do usuário do designer gerado.|\<none>|
|Nome de exibição|O nome que é exibido no designer gerado para a relação de domínio.|\<none>|
|Palavra-chave de ajuda|A palavra-chave opcional usada para indexar a ajuda F1 para a relação de domínio.|\<none>|

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](/previous-versions/bb126564(v=vs.100))