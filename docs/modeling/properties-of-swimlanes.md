---
title: Propriedades de swimlanes
description: Saiba como as raias dividem um diagrama em áreas verticais ou horizontais e como você pode definir outras formas a serem exibidas dentro de raias.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.swimlane
helpviewer_keywords:
- Domain-Specific Language, swimlane
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9c171bda2670b698297dd876a8a4403a91cd4af7
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386482"
---
# <a name="properties-of-swimlanes"></a>Propriedades de swimlanes
Você pode adicionar raias a um diagrama. As raias dividem um diagrama em áreas verticais ou horizontais. Você pode definir outras formas a serem exibidas dentro de raias. Para obter mais informações, consulte [como definir um idioma de Domain-Specific](../modeling/how-to-define-a-domain-specific-language.md). Para obter mais informações sobre como usar essas propriedades, consulte [Personalizando e estendendo uma linguagem de Domain-Specific](../modeling/customizing-and-extending-a-domain-specific-language.md).

 As raias têm as propriedades listadas na tabela a seguir.

|Propriedade|Descrição|Padrão|
|-|-|-|
|Cor de preenchimento do corpo|A cor de preenchimento do corpo da raia.|Branca|
|Cor de preenchimento do cabeçalho|A cor de preenchimento do cabeçalho da raia.|DarkGray|
|Cor do separador|A cor da linha do separador.|LightGray|
|Estilo da linha separadora|O estilo da linha do separador (,,,, `Solid` `Dash` `Dot` `DashDot` `DashDotDot` ou `Custom` ).|`Dash`|
|Espessura do separador|A espessura da linha do separador em polegadas.|0, 3125|
|Cor do texto|A cor usada para decoradores de texto associados a esta raia.|Preto|
|Modificador de acesso|O nível de acesso da classe ( `public` ou `internal` ).|Público|
|Atributos personalizados|Usado para adicionar atributos à classe de código gerada por essa raia.|\<none>|
|Gera derivação dupla|Se `True` , uma classe base e uma classe parcial (para dar suporte à personalização através de substituições) serão geradas. Para obter mais informações, consulte [substituindo e estendendo as classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|Falso|
|Tem Construtor personalizado|Se `True` , um construtor personalizado será fornecido no código-fonte. Para obter mais informações, consulte [substituindo e estendendo as classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|Falso|
|Modificador de herança|Descreve o tipo de herança da classe de código-fonte que é gerada a partir da raia ( `none` `abstract` ou `sealed` ).|nenhum|
|Raia base|A classe base dessa raia.|(nenhum)|
|Name|O nome desta raia.|Nome atual|
|Namespace|O namespace que é afiliado a esta raia.|Namespace atual|
|Tipo de dica de ferramenta|Como a dica de ferramenta é definida ( `fixed` , `variable` ou `none` ). Se `fixed` , em seguida, o valor da `Fixed Tooltip Text` propriedade será usado; se `variable` , em seguida, a dica de ferramenta será definida no código personalizado.|\<none>|
|Observações|Observações informais que estão associadas a esta raia.|\<none>|
|Alinhamento|Alinhamento horizontal ou vertical.|Vertical|
|Altura inicial|A altura inicial dessa raia, em polegadas. Aplicável somente a raias horizontais.|0|
|Largura inicial|A largura inicial dessa raia, em polegadas. Aplicável somente a raias verticais.|0|
|Expõe a cor do texto|Se `True` , o usuário pode definir a cor de uma raia no designer gerado. Para definir isso, clique com o botão direito do mouse na forma de raia e clique em **Adicionar exposto**.|Falso|
|Descrição|Usado para documentar o designer gerado.|\<none>|
|Nome de exibição|O nome que será exibido no designer gerado para se referir a essa classe de raia.|\<none>|
|Texto de dica de ferramenta fixo|O texto que é usado para uma dica de ferramenta fixa.|\<none>|
|Palavra-chave de ajuda|A palavra-chave usada para indexar a ajuda F1 para essa raia.|\<none>|

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](/previous-versions/bb126564(v=vs.100))