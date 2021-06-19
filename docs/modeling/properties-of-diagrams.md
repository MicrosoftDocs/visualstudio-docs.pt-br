---
title: Propriedades de diagramas
description: Saiba mais sobre diagramas e como você pode definir propriedades que especificam como os diagramas serão exibidos no designer gerado.
ms.custom: SEO-VS-2020
ms.date: 10/31/2018
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.dsldiagram
helpviewer_keywords:
- Domain-Specific Language, diagram
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8a060c79866d1746135f8a29aef15ca96dd51f63
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390666"
---
# <a name="properties-of-diagrams"></a>Propriedades de diagramas
Você pode definir propriedades que especificam como os diagramas serão exibidos no designer gerado. Por exemplo, você pode especificar uma cor padrão para o texto no diagrama.

 Para obter mais informações, [consulte Como definir um idioma específico do domínio](../modeling/how-to-define-a-domain-specific-language.md). Para obter mais informações sobre como usar essas propriedades, consulte [Personalizar e estender um idioma específico do domínio.](../modeling/customizing-and-extending-a-domain-specific-language.md)

 A tabela a seguir lista as propriedades dos diagramas.

|Propriedade|Descrição|Padrão|
|-|-|-|
|Cor de Preenchimento|A cor de preenchimento do diagrama.|Branca|
|Cor do texto|A cor do texto exibido no diagrama.|Preto|
|Modificador de acesso|O modificador de acesso da classe (público ou interno).|Público|
|Atributos personalizados|Usado para adicionar atributos à classe de código gerada.|\<none>|
|Gera derivada dupla|Se , uma classe base e uma classe parcial (para dar suporte à personalização por meio de `True` substituições) serão geradas. Para obter mais informações, consulte [Substituir e estender as classes geradas.](../modeling/overriding-and-extending-the-generated-classes.md)|Falso|
|Tem construtor personalizado|Se `True` , um construtor personalizado será fornecido no código-fonte. Para obter mais informações, consulte [Substituir e estender as classes geradas.](../modeling/overriding-and-extending-the-generated-classes.md)|Falso|
|Modificador de herança|Descreve o tipo de herança da classe de código-fonte gerada do diagrama ( `none` `abstract` , ou `sealed` ).|Nenhum|
|Diagrama base|A classe base deste diagrama.|(nenhum)|
|Name|O nome deste diagrama.|Nome atual|
|Namespace|O namespace que é afiliado a este diagrama.|Namespace atual|
|Classe representada|A classe de domínio raiz que este diagrama representa.|Classe raiz atual, se aplicável|
|Observações|Observações informais associadas a esse elemento.|\<none>|
|Expõe a cor de preenchimento como propriedade|Se `True` , o usuário poderá definir a cor de preenchimento do diagrama do designer gerado. Para definir essa propriedade, clique com o botão direito do mouse na forma do diagrama e clique **em Adicionar Exposto.**|Falso|
|Expõe a cor do texto como propriedade|Se `True` , o usuário poderá definir a cor do texto do diagrama no designer gerado. Para definir essa propriedade, clique com o botão direito do mouse na forma do diagrama e clique **em Adicionar Exposto.**|Falso|
|Descrição|A descrição usada para documentar o designer gerado.|\<none>|
|Nome de exibição|O nome que será exibido no designer gerado para este diagrama.|\<none>|
|Palavra-chave de ajuda|A palavra-chave usada para indexar a ajuda F1 para este diagrama.|\<none>|

## <a name="see-also"></a>Confira também

[Glossário de ferramentas de linguagem específicas do domínio](/previous-versions/bb126564(v=vs.100))