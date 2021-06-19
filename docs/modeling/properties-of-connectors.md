---
title: Propriedades de conectores
description: Saiba que os conectores representam relações de domínio em um designer gerado e que você usa essas propriedades para personalizar e estender uma linguagem específica de domínio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, connectors
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 43f55aecf134bf8e4d043a4fc7f6ffa2201f8e95
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390809"
---
# <a name="properties-of-connectors"></a>Propriedades de conectores
Os conectores representam relações de domínio em um designer gerado.

 Para obter mais informações, consulte [como definir um idioma de Domain-Specific](../modeling/how-to-define-a-domain-specific-language.md). Para obter mais informações sobre como usar essas propriedades, consulte [Personalizando e estendendo uma linguagem de Domain-Specific](../modeling/customizing-and-extending-a-domain-specific-language.md).

 Os conectores têm as propriedades listadas na tabela a seguir.

|Propriedade|Descrição|Padrão|
|-|-|-|
|Color|A cor deste conector.|Preto|
|Estilo do tracejado|O estilo de tracejado da linha para este conector (sólido, traço, ponto, travessão ponto, travessão ponto ponto ou personalizado).|Sólido|
|Estilo de extremidade de origem|O estilo de extremidade de origem deste conector (HollowArrow, EmptyArrow, FilledArrow, EmptyDiamond, FilledDiamond ou None).|Nenhum|
|Estilo final de destino|O estilo final de destino para esse conector (HollowArrow, EmptyArrow, FilledArrow, EmptyDiamond, FilledDiamond ou None).|Nenhum|
|Cor do texto|A cor que é usada para decoradores de texto associados a esse conector.|Preto|
|Espessura|A espessura da linha para esse conector, medida em polegadas.|0, 3125|
|Modificador de acesso|O nível de acesso da classe ( `public` ou `internal` ).|Público|
|Atributos personalizados|Usado para adicionar atributos à classe de código-fonte gerada por esse conector.|\<none>|
|Gera derivação dupla|Se `True` , uma classe base e uma classe parcial (para dar suporte à personalização através de substituições) serão geradas. Para obter mais informações, consulte [substituindo e estendendo as classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|Falso|
|Tem Construtor personalizado|Se `True` , um construtor personalizado será fornecido no código-fonte. Para obter mais informações, consulte [substituindo e estendendo as classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|Falso|
|Modificador de herança|Descreve o tipo de herança da classe de código-fonte gerada a partir do conector ( `none` `abstract` ou `sealed` ).|nenhum|
|Conector base|A classe base deste conector.|(nenhum)|
|Name|O nome deste conector.|Nome atual|
|Namespace|O namespace que é afiliado a esse conector.|Namespace atual|
|Tipo de dica de ferramenta|Como a dica de ferramenta é definida (fixa, variável ou nenhuma). Se for corrigido, o valor da `Fixed Tooltip Text` propriedade será usado como dica de ferramenta; se for variável, a dica de ferramenta será definida no código personalizado.|\<none>|
|Observações|Observações informais que estão associadas a este conector.|\<none>|
|Estilo de roteamento|O estilo usado para rotear o conector. Um `Rectilinear` conector faz com que o ângulo direito seja ativado conforme necessário; um `Straight` conector não.|Rectilinear|
|Cor exposta como Propriedade<br /><br /> O estilo de traço exposto como Propriedade<br /><br /> Espessura exposta como Propriedade<br /><br /> Expõe a cor do texto|Se `True` , o usuário pode definir a propriedade declarada de uma forma. Para definir isso, clique com o botão direito do mouse na definição de forma e clique em **Adicionar exposto**.|Falso|
|Descrição|Usado para documentar o designer gerado.|\<none>|
|Nome de exibição|O nome que será exibido no designer gerado para esse conector.|\<none>|
|Texto de dica de ferramenta fixo|O texto que é usado para uma dica de ferramenta fixa.|\<none>|
|Palavra-chave de ajuda|A palavra-chave usada para indexar a ajuda F1 para este elemento.|\<none>|

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](/previous-versions/bb126564(v=vs.100))