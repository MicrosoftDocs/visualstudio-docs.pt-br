---
title: Propriedades de classes de domínio
description: Saiba mais sobre as várias propriedades de classes de domínio, como Modificador de Acesso, Atributos Personalizados e Gera Derivada Dupla.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain class
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: eaaae0028d574a521319ae045cdb4f7f1bdafaa2
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390002"
---
# <a name="properties-of-domain-classes"></a>Propriedades de classes de domínio
As classes de domínio têm as propriedades na tabela a seguir. Para obter informações sobre classes de domínio, consulte [Noções básicas sobre modelos, classes e relações.](../modeling/understanding-models-classes-and-relationships.md) Para obter mais informações sobre como usar essas propriedades, consulte [Personalização](../modeling/customizing-and-extending-a-domain-specific-language.md)e extensão de uma linguagem Domain-Specific .

|Propriedade|Descrição|Padrão|
|-|-|-|
|Modificador de acesso|O nível de acesso da classe de domínio (`public` ou `internal`).|`public`|
|Atributos personalizados|Usado para adicionar atributos à classe de código-fonte gerada a partir dessa classe de domínio.|\<none>|
|Gera derivada dupla|Se , uma classe base e uma classe parcial (para dar suporte à personalização por meio de `True` substituições) serão geradas. Para obter mais informações, [consulte Substituindo e estendendo as classes geradas.](../modeling/overriding-and-extending-the-generated-classes.md)|`False`|
|Tem construtor personalizado|Se `True` , um construtor personalizado será fornecido no código-fonte. Para obter mais informações, [consulte Substituindo e estendendo as classes geradas.](../modeling/overriding-and-extending-the-generated-classes.md)|`False`|
|Modificador de herança|Descreve o tipo de herança da classe de código-fonte gerada da classe de domínio ( `none` ou `abstract` `sealed` ).|`none`|
|Classe base|Se essa classe de domínio for derivada, o nome da classe base.|\<none>|
|Name|O nome dessa classe de domínio.|Nome atual|
|Namespace|O namespace dessa classe de domínio.|Namespace atual|
|Observações|Observações informais associadas a essa classe de domínio.|\<none>|
|Descrição|A descrição usada para documentar a interface do usuário do designer gerado.|\<none>|
|Nome de exibição|O nome que será exibido no designer gerado para essa classe de domínio.|\<none>|
|Palavra-chave de ajuda|A palavra-chave opcional usada para indexar a ajuda F1 para essa classe de domínio.|\<none>|

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](/previous-versions/bb126564(v=vs.100))