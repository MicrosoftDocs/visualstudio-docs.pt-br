---
title: Propriedades de formas de compartimento
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.compartmentshape
helpviewer_keywords:
- Domain-Specific Language, compartment shape
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 98013b53641efec6a088c1e89bf521613fc7659e
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50966564"
---
# <a name="properties-of-compartment-shapes"></a>Propriedades de formas de compartimento
Formas de compartimento são uma das formas que você pode usar para exibir uma classe de domínio em uma linguagem específica de domínio. Você pode expandir e recolher os compartimentos.

 Para obter mais informações, consulte [como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md). Para obter mais informações sobre como usar essas propriedades, consulte [personalizando e estendendo uma linguagem específica do domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

 Formas do compartimento têm as propriedades que são listadas na tabela a seguir.

|Propriedade|Descrição|Padrão|
|-|-|-|
|Padrão expandir estado recolhido|Se `Expanded`, os compartimentos são mostrados na criação. Se `Collapsed`, eles não são.|Expandido|
|Cor de preenchimento|A cor de preenchimento desta forma.|Branco|
|Modo de gradiente de preenchimento|O modo gradiente de preenchimento desta forma.|Horizontal|
|geometria|A geometria desta forma (retângulo ou um retângulo arredondado).|Retângulo|
|Tem pontos de Conexão padrão|Se `True`, a forma usará superior, inferior, esquerda e pontos de conexão certa no designer gerado.|False|
|Cabeçalho de compartimento único está visível|Se `False`e a forma tem um único compartimento, o cabeçalho do compartimento não será visível.|verdadeiro|
|Cor do contorno|A cor do contorno desta forma.|Preto|
|Estilo de contorno tracejado|O estilo de contorno tracejado desta forma (sólido, traço, Dot, Traçoponto, Traçopontoponto, personalizado).|Sólido|
|Espessura do contorno|A espessura do contorno desta forma.|0.03125|
|Cor do texto|A cor usada para os decoradores de texto que estão associados esta forma.|Preto|
|Modificador de acesso|O nível de acesso de forma do compartimento (`public` ou `internal`).|Público|
|Atributos personalizados|Usado para adicionar atributos à classe de código de origem que é gerado a partir desta forma de compartimento|\<Nenhum >|
|Gera dupla derivado|Se `True`, serão geradas uma classe base e uma classe parcial (para dar suporte à personalização por meio de substituições). Para obter mais informações, consulte [substituindo e estendendo as Classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|False|
|Tem um construtor personalizado|Se `True`, um construtor personalizado será fornecido no código-fonte. Para obter mais informações, consulte [substituindo e estendendo as Classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|False|
|Modificador de herança|Descreve o tipo de herança da classe de código de origem que é gerada de forma do compartimento (`none`, `abstract` ou `sealed`).|Nenhum|
|Forma de compartimento base|A classe base dessa forma.|(nenhum)|
|Nome|O nome desta forma.|Nome atual|
|Namespace|O namespace que é afiliado desta forma.|Namespace atual|
|Tipo de dica de ferramenta|Como a dica de ferramenta é definida (fixo, variável ou nenhum). Se fixo, em seguida, o valor da `Fixed Tooltip Text` propriedade é usada como a dica de ferramenta; se a variável, em seguida, a dica de ferramenta é definida no código personalizado.|nenhum|
|Observações|Observações informais associadas esta forma.|\<Nenhum >|
|Altura inicial|A altura inicial desta forma em polegadas. Para formas de compartimento, essa é a altura da seção de cabeçalho somente e ela não pode ser redimensionada.|1|
|Largura inicial|A largura inicial desta forma em polegadas.|1.5|
|Cor de preenchimento expostos como propriedade<br /><br /> Modo de gradiente de preenchimento exposto<br /><br /> Exposto a cor do contorno como propriedade<br /><br /> Exposto o estilo de contorno tracejado como propriedade<br /><br /> Exposto como propriedade de espessura do contorno<br /><br /> Expõe a cor do texto|Se `True`, o usuário pode definir a propriedade indicada de uma forma. Para configurar isso, a definição de forma com o botão direito e clique em **adicionar exposto**.|False|
|Descrição|Usado para documentar o designer gerado.|\<Nenhum >|
|Nome de Exibição|O nome que será exibido no designer gerado para esta forma.|\<Nenhum >|
|Texto de dica de ferramenta fixa|O texto que é usado para uma dica de ferramenta fixa.|\<Nenhum >|
|Palavra-chave de ajuda|A palavra-chave que é usada para indexar a Ajuda de F1 para esta forma.|\<Nenhum >|

## <a name="see-also"></a>Consulte também

- [Glossário de ferramentas de linguagem específica do domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)