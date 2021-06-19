---
title: Propriedades de formas de compartimento
description: Saiba que as formas de compartimento são uma das formas que você pode usar para exibir uma classe de domínio em um idioma específico do domínio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.compartmentshape
helpviewer_keywords:
- Domain-Specific Language, compartment shape
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0ec84057bfe7d49760a8f95132a30e8c927f60f0
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390822"
---
# <a name="properties-of-compartment-shapes"></a>Propriedades de formas de compartimento
Formas de compartimento são uma das formas que você pode usar para exibir uma classe de domínio em um idioma específico do domínio. Você pode expandir e ressumentar os compartimentos.

 Para obter mais informações, [consulte How to Define a Domain-Specific Language](../modeling/how-to-define-a-domain-specific-language.md). Para obter mais informações sobre como usar essas propriedades, consulte [Personalização](../modeling/customizing-and-extending-a-domain-specific-language.md)e extensão de uma linguagem Domain-Specific .

 As formas de compartimento têm as propriedades listadas na tabela a seguir.

|Propriedade|Descrição|Padrão|
|-|-|-|
|Expandir Estado de Ressalção Padrão|Se `Expanded` , os compartimentos serão mostrados na criação. Se `Collapsed` , eles não serão.|Expanded|
|Cor de Preenchimento|A cor de preenchimento dessa forma.|Branca|
|Modo gradiente de preenchimento|O modo de gradiente de preenchimento dessa forma.|Horizontal|
|Geometry|A geometria dessa forma (Retângulo ou Retângulo Arredondado).|Retângulo|
|Tem pontos de conexão padrão|Se , a forma usará os pontos de conexão `True` superior, inferior, esquerdo e direito no designer gerado.|Falso|
|É visível o header de compartimento único|Se `False` , e a forma tiver um único compartimento, o header do compartimento não será visível.|Verdadeiro|
|Cor do contorno|A cor do contorno dessa forma.|Preto|
|Estilo de traço de contorno|O estilo de traço de estrutura dessa forma (Solid, Dash, Dot, DashDot, DashDotDot, Custom).|Sólido|
|Espessura do contorno|A espessura do contorno dessa forma.|0.03125|
|Cor do texto|A cor usada para decoradores de texto associados a essa forma.|Preto|
|Modificador de acesso|O nível de acesso da forma do compartimento ( `public` ou `internal` ).|Público|
|Atributos personalizados|Usado para adicionar atributos à classe de código-fonte gerada a partir dessa forma de compartimento|\<none>|
|Gera derivada dupla|Se , uma classe base e uma classe parcial (para dar suporte à personalização por meio de `True` substituições) serão geradas. Para obter mais informações, [consulte Substituindo e estendendo as classes geradas.](../modeling/overriding-and-extending-the-generated-classes.md)|Falso|
|Tem construtor personalizado|Se `True` , um construtor personalizado será fornecido no código-fonte. Para obter mais informações, [consulte Substituindo e estendendo as classes geradas.](../modeling/overriding-and-extending-the-generated-classes.md)|Falso|
|Modificador de herança|Descreve o tipo de herança da classe de código-fonte gerada da forma do compartimento ( `none` ou `abstract` `sealed` ).|Nenhum|
|Forma do compartimento base|A classe base dessa forma.|(nenhum)|
|Name|O nome dessa forma.|Nome atual|
|Namespace|O namespace que é afiliado a essa forma.|Namespace atual|
|Tipo de dica de ferramenta|Como a dica de ferramenta é definida (fixa, variável ou nenhuma). Se for corrigido, o valor da propriedade será usado como a dica de ferramenta; se for variável, a dica de `Fixed Tooltip Text` ferramenta será definida no código personalizado.|nenhum|
|Observações|Observações informais associadas a essa forma.|\<none>|
|Altura inicial|A altura inicial dessa forma, em polegadas. Para formas de compartimento, essa é a altura da seção de header somente e não pode ser ressada.|1|
|Largura inicial|A largura inicial dessa forma, em polegadas.|1.5|
|Cor de preenchimento exposta como propriedade<br /><br /> Modo de gradiente de preenchimento exposto<br /><br /> Cor de contorno exposta como propriedade<br /><br /> Estilo de traço de contorno exposto como propriedade<br /><br /> Espessura de contorno exposta como propriedade<br /><br /> Expõe a cor do texto|Se `True` , o usuário poderá definir a propriedade declarado de uma forma. Para definir isso, clique com o botão direito do mouse na definição de forma e clique **em Adicionar Exposto.**|Falso|
|Descrição|Usado para documentar o designer gerado.|\<none>|
|Nome de exibição|O nome que será exibido no designer gerado para essa forma.|\<none>|
|Texto de dica de ferramenta fixo|O texto usado para uma dica de ferramenta fixa.|\<none>|
|Palavra-chave de ajuda|A palavra-chave usada para indexar a ajuda F1 para essa forma.|\<none>|

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](/previous-versions/bb126564(v=vs.100))