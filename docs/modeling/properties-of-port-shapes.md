---
title: Propriedades de formas de porta
description: Saiba mais sobre formas de porta e como você pode usar formas de porta para representar classes de domínio no designer gerado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.port
helpviewer_keywords:
- Domain-Specific Language, port shape
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b5994d2629a49757980695ca99a6d12ae21160a6
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386521"
---
# <a name="properties-of-port-shapes"></a>Propriedades de formas de porta
Você pode usar formas de porta para representar classes de domínio no designer gerado.

 Para obter mais informações, consulte [como definir um idioma de Domain-Specific](../modeling/how-to-define-a-domain-specific-language.md). Para obter mais informações sobre como usar essas propriedades, consulte [Personalizando e estendendo uma linguagem de Domain-Specific](../modeling/customizing-and-extending-a-domain-specific-language.md).

 As formas de porta têm as propriedades listadas na tabela a seguir.

|Propriedade|Descrição|Padrão|
|-|-|-|
|Cor de Preenchimento|A cor de preenchimento desta forma.|Branca|
|Preencher modo de gradiente|O modo de gradiente de preenchimento desta forma.|Horizontal|
|Geometry|A geometria desta forma (retângulo, retângulo arredondado, elipse ou círculo).|Retângulo|
|Tem pontos de conexão padrão|Se `True` , a forma usará os pontos de conexão superior, inferior, esquerdo e direito no designer gerado.|Falso|
|Cor do contorno|A cor da estrutura de tópicos desta forma.|Preto|
|Estilo do contorno tracejado|O estilo de contorno tracejado dessa forma (sólido, traço, ponto, travessão ponto, travessão ponto ponto ou personalizado).|Sólido|
|Espessura do contorno|A espessura da estrutura de tópicos desta forma.|0, 3125|
|Cor do texto|A cor que é usada para decoradores de texto associados a essa forma.|Preto|
|Modificador de acesso|O nível de acesso da classe ( `public` ou `internal` ).|Público|
|Atributos personalizados|Usado para adicionar atributos à classe de código-fonte gerada com base nessa forma.|\<none>|
|Gera derivação dupla|Se `True` , uma classe base e uma classe parcial (para dar suporte à personalização através de substituições) serão geradas. Para obter mais informações, consulte [substituindo e estendendo as classes geradas](../modeling/overriding-and-extending-the-generated-classes.md)|Falso|
|Tem Construtor personalizado|Se `True` , um construtor personalizado será fornecido no código-fonte. Para obter mais informações, consulte [substituindo e estendendo as classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|Falso|
|Modificador de herança|Descreve o tipo de herança da classe de código-fonte que é gerada a partir da porta ( `none` , `abstract` ou `sealed` ).|nenhum|
|Porta base|A classe base dessa forma.|(nenhum)|
|Name|O nome desta forma.|Nome atual|
|Namespace|O namespace que é afiliado a esta forma.|Namespace atual|
|Tipo de dica de ferramenta|Como a dica de ferramenta é definida (fixa, variável ou nenhuma). Se for corrigido, o valor da `Fixed Tooltip Text` propriedade será usado como dica de ferramenta; se for variável, a dica de ferramenta será definida no código personalizado.|nenhum|
|Observações|Observações informais associadas a esta forma.|\<none>|
|Altura inicial|A altura inicial dessa forma, em polegadas.|1|
|Largura inicial|A largura inicial dessa forma, em polegadas.|1.5|
|Cor de preenchimento exposta como Propriedade<br /><br /> Modo de gradiente de preenchimento exposto<br /><br /> Cor da estrutura de tópicos exposta como Propriedade<br /><br /> Contorno exposto traço estilo como Propriedade<br /><br /> Espessura da estrutura de tópicos exposta como Propriedade<br /><br /> Expõe a cor do texto|Se `True` , o usuário pode definir a propriedade declarada de uma forma. Para definir isso, clique com o botão direito do mouse na definição de forma e clique em **Adicionar exposto**.|Falso|
|Descrição|Usado para documentar o designer gerado.|\<none>|
|Nome de exibição|O nome que será exibido no designer gerado para essa forma.|\<none>|
|Texto de dica de ferramenta fixa|O texto que é usado para uma dica de ferramenta fixa.|\<none>|
|Palavra-chave de ajuda|A palavra-chave usada para indexar a ajuda F1 para essa forma.|\<none>|

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](/previous-versions/bb126564(v=vs.100))