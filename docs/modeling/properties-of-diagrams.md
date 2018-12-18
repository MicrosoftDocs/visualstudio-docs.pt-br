---
title: Propriedades de diagramas
ms.date: 10/31/2018
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.dsldiagram
helpviewer_keywords:
- Domain-Specific Language, diagram
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 39e3cc044913a592d5f49e685d8075cd43803e55
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50966473"
---
# <a name="properties-of-diagrams"></a>Propriedades de diagramas
Você pode definir propriedades que especificam como os diagramas aparecerá no designer gerado. Por exemplo, você pode especificar uma cor padrão para o texto no diagrama.

 Para obter mais informações, consulte [como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md). Para obter mais informações sobre como usar essas propriedades, consulte [personalizar e estender uma linguagem específica do domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

 A tabela a seguir lista as propriedades de diagramas.

|Propriedade|Descrição|Padrão|
|-|-|-|
|Cor de preenchimento|A cor de preenchimento para o diagrama.|Branco|
|Cor do texto|A cor do texto que é exibido no diagrama.|Preto|
|Modificador de acesso|O modificador de acesso da classe (público ou interno).|Público|
|Atributos personalizados|Usado para adicionar atributos para a classe do código gerado.|\<Nenhum >|
|Gera dupla derivado|Se `True`, serão geradas uma classe base e uma classe parcial (para dar suporte à personalização por meio de substituições). Para obter mais informações, consulte [substituir e estender as classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|False|
|Tem um construtor personalizado|Se `True`, um construtor personalizado será fornecido no código-fonte. Para obter mais informações, consulte [substituir e estender as classes geradas](../modeling/overriding-and-extending-the-generated-classes.md)...|False|
|Modificador de herança|Descreve o tipo de herança da classe de código fonte que é gerado do diagrama (`none`, `abstract`, ou `sealed`).|Nenhum|
|Diagrama base|A classe base deste diagrama.|(nenhum)|
|Nome|O nome do diagrama.|Nome atual|
|Namespace|O namespace que é afiliado neste diagrama.|Namespace atual|
|Classe representada|A classe de domínio de raiz que este diagrama representa.|Classe raiz atual se aplicável|
|Observações|Observações informais associadas esse elemento.|\<Nenhum >|
|Expõe a cor de preenchimento como propriedade|Se `True`, o usuário pode definir a cor de preenchimento do diagrama do designer gerado. Para definir essa propriedade, clique com botão direito na forma de diagrama e clique em **adicionar exposto**.|False|
|Expõe a cor do texto como propriedade|Se `True`, o usuário pode definir a cor do texto do diagrama no designer gerado. Para definir essa propriedade, clique com botão direito na forma de diagrama e clique em **adicionar exposto**.|False|
|Descrição|A descrição é usada para documentar o designer gerado.|\<Nenhum >|
|Nome de Exibição|O nome que será exibido no designer gerado para este diagrama.|\<Nenhum >|
|Palavra-chave de ajuda|A palavra-chave que é usada para indexar a Ajuda de F1 para este diagrama.|\<Nenhum >|

## <a name="see-also"></a>Consulte também

[Glossário de ferramentas de linguagem específica do domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
