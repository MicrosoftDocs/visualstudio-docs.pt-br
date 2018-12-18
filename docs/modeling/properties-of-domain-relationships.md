---
title: Propriedades de relacionamentos de domínio
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain relationships
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 3ec468ebedbe1d15ddff3527bcf0783b9831247e
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50966434"
---
# <a name="properties-of-domain-relationships"></a>Propriedades de relacionamentos de domínio
As propriedades na tabela a seguir estão associadas com uma relação de domínio. Para obter informações sobre as relações de domínio, consulte [Noções básicas sobre modelos, Classes e relacionamentos](../modeling/understanding-models-classes-and-relationships.md). Para obter mais informações sobre como usar essas propriedades, consulte [personalizando e estendendo uma linguagem específica do domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

|Propriedade|Descrição|Padrão|
|-|-|-|
|Modificador de acesso|O nível de acesso da relação de domínio (`public` ou `internal`).|`public`|
|Atributos personalizados|Usado para adicionar atributos à classe de código de origem que é gerado a partir a relação de domínio.|\<Nenhum >|
|Gera dupla derivado|Se `True`, uma classe base e uma classe parcial (para dar suporte à personalização por meio de substituições) é gerado. Para obter mais informações, consulte [substituindo e estendendo as Classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|`False`|
|Tem um construtor personalizado|Se `True`, indica que um construtor personalizado é fornecido no código-fonte. Para obter mais informações, consulte [substituindo e estendendo as Classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).|`False`|
|Modificador de herança|Descreve o tipo de herança da classe de código fonte que é gerado da relação de domínio (`none`, `abstract` ou `sealed`).|\<Nenhum >|
|Permite que as duplicatas|Se `True`, links duplicados da relação de domínio pode ser criados entre os mesmos dois elementos.|`False`|
|Relações de base|Se a relação de domínio é derivada, o relacionamento base a relação de domínio.|\<Nenhum >|
|É de inserção|Se `True`, a relação de domínio é uma relação de incorporação. Se `False`, a relação é uma relação de referência.|\<ambos >|
|Nome|O nome da relação de domínio.|Nome atual|
|Namespace|O namespace está afiliado a relação de domínio.|Namespace atual|
|Observações|Observações informais associadas a relação de domínio.|\<Nenhum >|
|Descrição|A descrição que é usada para documentar código e é usada na interface do usuário do designer gerado.|\<Nenhum >|
|Nome de Exibição|O nome que é exibido no designer gerado para a relação de domínio.|\<Nenhum >|
|Palavra-chave de ajuda|A palavra-chave opcional que é usada para indexar a Ajuda de F1 para o relacionamento de domínio.|\<Nenhum >|

## <a name="see-also"></a>Consulte também

- [Glossário de ferramentas de linguagem específica do domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)