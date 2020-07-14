---
title: Propriedades de formas de compartimento
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.compartmentshape
helpviewer_keywords:
- Domain-Specific Language, compartment shape
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 51b652adcc482d6e326c0b64eda3a9d32efab309
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85532283"
---
# <a name="properties-of-compartment-shapes"></a>Propriedades de formas de compartimento
As formas de compartimento são uma das formas que você pode usar para exibir uma classe de domínio em uma linguagem específica de domínio. Você pode expandir e recolher os compartimentos.

 Para obter mais informações, consulte [como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md). Para obter mais informações sobre como usar essas propriedades, consulte [Personalizando e estendendo uma linguagem específica de domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

 As formas de compartimento têm as propriedades listadas na tabela a seguir.

|Propriedade|Descrição|Padrão|
|-|-|-|
|Padrão expandir estado de recolhimento|Se `Expanded` , os compartimentos são mostrados na criação. Se `Collapsed` não forem.|Expanded|
|Cor de Preenchimento|A cor de preenchimento desta forma.|Branco|
|Preencher modo de gradiente|O modo de gradiente de preenchimento desta forma.|Horizontal|
|Geometry|A geometria dessa forma (retângulo ou retângulo arredondado).|Retângulo|
|Tem pontos de conexão padrão|Se `True` , a forma usará os pontos de conexão superior, inferior, esquerdo e direito no designer gerado.|Falso|
|É um cabeçalho de compartimento único visível|Se `False` e a forma tiver um único compartimento, o cabeçalho do compartimento não será visível.|verdadeiro|
|Cor do contorno|A cor da estrutura de tópicos desta forma.|Preto|
|Estilo do contorno tracejado|O estilo do contorno tracejado dessa forma (sólido, traço, ponto, travessão ponto, travessão ponto ponto, personalizado).|Sólido|
|Espessura do contorno|A espessura da estrutura de tópicos desta forma.|0, 3125|
|Cor do texto|A cor usada para decoradores de texto associados a esta forma.|Preto|
|Modificador de acesso|O nível de acesso da forma do compartimento ( `public` ou `internal` ).|Público|
|Atributos personalizados|Usado para adicionar atributos à classe de código-fonte gerada a partir desta forma de compartimento|\<none>|
|Gera derivação dupla|Se `True` , uma classe base e uma classe parcial (para dar suporte à personalização através de substituições) serão geradas. Para obter mais informações, consulte [substituindo e estendendo as classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|Falso|
|Tem Construtor personalizado|Se `True` , um construtor personalizado será fornecido no código-fonte. Para obter mais informações, consulte [substituindo e estendendo as classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|Falso|
|Modificador de herança|Descreve o tipo de herança da classe de código-fonte gerada a partir da forma de compartimento `none` ( `abstract` ou `sealed` ).|Nenhum|
|Forma do compartimento de base|A classe base dessa forma.|(nenhum)|
|Nome|O nome desta forma.|Nome atual|
|Namespace|O namespace que é afiliado a esta forma.|Namespace atual|
|Tipo de dica de ferramenta|Como a dica de ferramenta é definida (fixa, variável ou nenhuma). Se for corrigido, o valor da `Fixed Tooltip Text` propriedade será usado como dica de ferramenta; se for variável, a dica de ferramenta será definida no código personalizado.|nenhum|
|Observações|Observações informais associadas a esta forma.|\<none>|
|Altura inicial|A altura inicial dessa forma, em polegadas. Para as formas de compartimento, esta é a altura da seção de cabeçalho somente e não pode ser redimensionada.|1|
|Largura inicial|A largura inicial dessa forma, em polegadas.|1.5|
|Cor de preenchimento exposta como Propriedade<br /><br /> Modo de gradiente de preenchimento exposto<br /><br /> Cor da estrutura de tópicos exposta como Propriedade<br /><br /> Contorno exposto traço estilo como Propriedade<br /><br /> Espessura da estrutura de tópicos exposta como Propriedade<br /><br /> Expõe a cor do texto|Se `True` , o usuário pode definir a propriedade declarada de uma forma. Para definir isso, clique com o botão direito do mouse na definição de forma e clique em **Adicionar exposto**.|Falso|
|Descrição|Usado para documentar o designer gerado.|\<none>|
|Nome de exibição|O nome que será exibido no designer gerado para essa forma.|\<none>|
|Texto de dica de ferramenta fixo|O texto que é usado para uma dica de ferramenta fixa.|\<none>|
|Palavra-chave de ajuda|A palavra-chave usada para indexar a ajuda F1 para essa forma.|\<none>|

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)