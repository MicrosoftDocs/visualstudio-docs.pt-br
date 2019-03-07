---
title: Propriedades de swimlanes
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.swimlane
helpviewer_keywords:
- Domain-Specific Language, swimlane
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ab2e10eed7452bf58390513bed68fac3f4c9a0f6
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55956838"
---
# <a name="properties-of-swimlanes"></a>Propriedades de swimlanes
Você pode adicionar as raias a um diagrama. As raias dividem um diagrama em áreas verticais ou horizontais. Você pode definir outras formas a ser exibido dentro de raias. Para obter mais informações, consulte [como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md). Para obter mais informações sobre como usar essas propriedades, consulte [personalizando e estendendo uma linguagem específica do domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

 As raias têm as propriedades que são listadas na tabela a seguir.

|Propriedade|Descrição|Padrão|
|-|-|-|
|Cor de preenchimento do corpo|A cor de preenchimento para o corpo da Raia.|Branco|
|Cor de preenchimento do cabeçalho|A cor de preenchimento para o cabeçalho da Raia.|Azul escuro|
|Cor do separador|A cor da linha do separador.|LightGray|
|Estilo de linha do separador|O estilo da linha do separador (`Solid`, `Dash`, `Dot`, `DashDot`, `DashDotDot`, ou `Custom`).|`Dash`|
|Espessura do separador|A espessura da linha do separador em polegadas.|0.03125|
|Cor do texto|A cor que é usada para os decoradores de texto que estão associados com desta Raia.|Preto|
|Modificador de acesso|O nível de acesso da classe (`public` ou `internal`).|Público|
|Atributos personalizados|Usado para adicionar atributos à classe de código que é gerado a partir desta Raia.|\<nenhum>|
|Gera dupla derivado|Se `True`, serão geradas uma classe base e uma classe parcial (para dar suporte à personalização por meio de substituições). Para obter mais informações, consulte [substituindo e estendendo as Classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|False|
|Tem um construtor personalizado|Se `True`, um construtor personalizado será fornecido no código-fonte. Para obter mais informações, consulte [substituindo e estendendo as Classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|False|
|Modificador de herança|Descreve o tipo de herança da classe de código fonte que é gerado a partir de Raia (`none`, `abstract` ou `sealed`).|nenhum|
|Raia base|A classe base desta Raia.|(nenhum)|
|Nome|O nome desta Raia.|Nome atual|
|Namespace|O namespace que é afiliado desta Raia.|Namespace atual|
|Tipo de dica de ferramenta|Como a dica de ferramenta é definida (`fixed`, `variable`, ou `none`). Se `fixed`, em seguida, o valor da `Fixed Tooltip Text` propriedade é usada; se `variable`, e em seguida, a dica de ferramenta é definida no código personalizado.|\<nenhum>|
|Observações|Observações informais associadas desta Raia.|\<nenhum>|
|Alinhamento|Alinhamento horizontal ou vertical.|Vertical|
|Altura inicial|A altura inicial desta Raia em polegadas. Aplicável somente às raias horizontais.|0|
|Largura inicial|A largura inicial desta Raia em polegadas. Aplicável somente às raias verticais.|0|
|Expõe a cor do texto|Se `True`, o usuário pode definir a cor de uma raia no designer gerado. Para definir isso, clique com botão direito na forma de Raia e clique em **adicionar exposto**.|False|
|Descrição|Usado para documentar o designer gerado.|\<nenhum>|
|Nome de Exibição|O nome que será exibido no designer gerado para se referir a essa classe de Raia.|\<nenhum>|
|Texto de dica de ferramenta fixa|O texto que é usado para uma dica de ferramenta fixa.|\<nenhum>|
|Palavra-chave de ajuda|A palavra-chave que é usada para indexar a Ajuda de F1 para desta Raia.|\<nenhum>|

## <a name="see-also"></a>Consulte também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)