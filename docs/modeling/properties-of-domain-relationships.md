---
title: Propriedades de relacionamentos de domínio
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain relationships
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2de06e33b26f7af66dc0670193561758c5fa5896
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544151"
---
# <a name="properties-of-domain-relationships"></a>Propriedades de relacionamentos de domínio
As propriedades na tabela a seguir são associadas a uma relação de domínio. Para obter informações sobre relações de domínio, consulte [noções básicas sobre modelos, classes e relações](../modeling/understanding-models-classes-and-relationships.md). Para obter mais informações sobre como usar essas propriedades, consulte [Personalizando e estendendo uma linguagem específica de domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

|Propriedade|Descrição|Padrão|
|-|-|-|
|Modificador de acesso|O nível de acesso da relação de domínio ( `public` ou `internal` ).|`public`|
|Atributos personalizados|Usado para adicionar atributos à classe de código-fonte que é gerada a partir da relação de domínio.|\<none>|
|Gera derivação dupla|Se `True` , uma classe base e uma classe parcial (para dar suporte à personalização por meio de substituições) serão geradas. Para obter mais informações, consulte [substituindo e estendendo as classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|`False`|
|Tem Construtor personalizado|Se `True` , indica que um construtor personalizado é fornecido no código-fonte. Para obter mais informações, consulte [substituindo e estendendo as classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|`False`|
|Modificador de herança|Descreve o tipo de herança da classe de código-fonte que é gerada a partir da relação de domínio ( `none` `abstract` ou `sealed` ).|\<none>|
|Permite duplicatas|Se `True` , os links duplicados da relação de domínio poderão ser criados entre os mesmos dois elementos.|`False`|
|Relações de base|Se a relação de domínio for derivada, a relação base da relação de domínio.|\<none>|
|Está incorporando|Se `True` , a relação de domínio é uma relação incorporada. Se `False` , a relação é uma relação de referência.|\<both>|
|Nome|O nome da relação de domínio.|Nome atual|
|Namespace|O namespace que é afiliado ao relacionamento de domínio.|Namespace atual|
|Observações|Observações informais que estão associadas à relação de domínio.|\<none>|
|Descrição|A descrição usada para documentar o código e é usada na interface do usuário do designer gerado.|\<none>|
|Nome de exibição|O nome que é exibido no designer gerado para a relação de domínio.|\<none>|
|Palavra-chave de ajuda|A palavra-chave opcional que é usada para indexar a ajuda F1 para a relação de domínio.|\<none>|

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)