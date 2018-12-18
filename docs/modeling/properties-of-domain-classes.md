---
title: Propriedades de classes de domínio
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain class
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 97ab03084a64adcf6644eeaaef8478c453fc3559
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50967149"
---
# <a name="properties-of-domain-classes"></a>Propriedades de classes de domínio
Classes de domínio têm as propriedades na tabela a seguir. Para obter informações sobre classes de domínio, consulte [Noções básicas sobre modelos, Classes e relacionamentos](../modeling/understanding-models-classes-and-relationships.md). Para obter mais informações sobre como usar essas propriedades, consulte [personalizando e estendendo uma linguagem específica do domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

|Propriedade|Descrição|Padrão|
|-|-|-|
|Modificador de acesso|O nível de acesso da classe de domínio (`public` ou `internal`).|`public`|
|Atributos personalizados|Usado para adicionar atributos para a classe de código de origem que é gerada a partir dessa classe de domínio.|\<Nenhum >|
|Gera dupla derivado|Se `True`, serão geradas uma classe base e uma classe parcial (para dar suporte à personalização por meio de substituições). Para obter mais informações, consulte [substituindo e estendendo as Classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|`False`|
|Tem um construtor personalizado|Se `True`, um construtor personalizado será fornecido no código-fonte. Para obter mais informações, consulte [substituindo e estendendo as Classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|`False`|
|Modificador de herança|Descreve o tipo de herança da classe de código de origem que é gerado a partir da classe de domínio (`none`, `abstract` ou `sealed`).|`none`|
|Classe base|Se essa classe de domínio é derivada, o nome da classe base.|\<Nenhum >|
|Nome|O nome dessa classe de domínio.|Nome atual|
|Namespace|O namespace da classe de domínio.|Namespace atual|
|Observações|Observações informais associadas essa classe de domínio.|\<Nenhum >|
|Descrição|A descrição é usada para documentar a interface do usuário do designer gerado.|\<Nenhum >|
|Nome de Exibição|O nome que será exibido no designer gerado para essa classe de domínio.|\<Nenhum >|
|Palavra-chave de ajuda|A palavra-chave opcional que é usada para indexar a Ajuda de F1 para esta classe de domínio.|\<Nenhum >|

## <a name="see-also"></a>Consulte também

- [Glossário de ferramentas de linguagem específica do domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)