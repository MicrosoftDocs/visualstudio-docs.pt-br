---
title: Avisos de nomenclatura
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.namingrules
helpviewer_keywords:
- managed code analysis warnings, naming warnings
- naming warnings
- warnings, naming
ms.assetid: f97223ce-1d39-4134-81c9-fff2c75d979b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 27bc332d113bbf97744af8795979f238c90d6e84
ms.sourcegitcommit: 08c144d290da373df841f04fc799e3133540a541
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "72535726"
---
# <a name="naming-warnings"></a>Avisos de nomenclatura

Os avisos de nomenclatura dão suporte à adesão às convenções de nomenclatura das diretrizes de design do .NET.

## <a name="in-this-section"></a>Nesta seção

|Regra|Descrição|
|----------|-----------------|
|[CA1700: não nomear valores de enum como 'Reservados'](../code-quality/ca1700.md)|Esta regra pressupõe que um membro da enumeração que tenha um nome que contém "reserved" não é usado atualmente, mas é um espaço reservado a ser renomeado ou removido em uma versão futura. Renomear ou remover um membro é uma alteração drástica.|
|[CA1713: os eventos não devem ter um prefixo anterior ou posterior](../code-quality/ca1713.md)|O nome de um evento começa com "Before" ou "After". Para nomear eventos relacionados acionados em uma sequência específica, use o presente ou o pretérito para indicar a posição relativa na sequência de ações.|
|[CA1714: enums de sinalizadores devem ter nomes plurais](../code-quality/ca1714.md)|Uma enumeração pública tem o atributo System. FlagsAttribute e seu nome não termina em "s". Os tipos marcados com FlagsAttribute têm nomes que são plural porque o atributo indica que mais de um valor pode ser especificado.|
|[CA1704: os identificadores devem ter a ortografia correta](../code-quality/ca1704.md)|O nome de um identificador visível externamente contém uma ou mais palavras não reconhecidas pela biblioteca do verificador ortográfico da Microsoft.|
|[CA1708: os identificadores devem ser diferentes além de maiúsculas de minúsculas](../code-quality/ca1708.md)|Os identificadores de namespaces, tipos, membros e parâmetros não podem se diferenciar apenas por maiúsculas porque linguagens com o Common Language Runtime como destino não precisam diferenciar maiúsculas e minúsculas.|
|[CA1715: os identificadores devem ter o prefixo correto](../code-quality/ca1715.md)|O nome de uma interface visível externamente não começa com um "I" maiúsculo.  O nome de um parâmetro de tipo genérico em um tipo ou método visível externamente não começa com um "T" maiúsculo.|
|[CA1720: os identificadores não devem conter nomes de tipo](../code-quality/ca1720.md)|O nome de um parâmetro em um membro visível externamente contém um nome de tipo de dados, ou o nome de um membro visível externamente contém um nome de tipo de dados específico da linguagem.|
|[CA1722: os identificadores não devem ter prefixo incorreto](../code-quality/ca1722.md)|Por convenção, somente determinados elementos de programação têm nomes que começam com um prefixo específico.|
|[CA1711: os identificadores não devem ter sufixo incorreto](../code-quality/ca1711.md)|Por convenção, apenas os nomes de tipos que estendem determinados tipos de base ou que implementam determinadas interfaces, ou tipos derivados desses tipos, devem terminar com sufixos reservados específicos. Outros nomes de tipo não devem usar esses sufixos reservados.|
|[CA1717: apenas enums FlagsAttribute devem ter nomes plurais](../code-quality/ca1717.md)|As convenções de nomenclatura determinam que um nome no plural para uma enumeração indica que mais de um valor de enumeração pode ser especificado ao mesmo tempo.|
|[CA1725: os nomes de parâmetro devem corresponder à declaração base](../code-quality/ca1725.md)|A nomenclatura consistente dos parâmetros em uma hierarquia de substituição aumenta a usabilidade das substituições de método. Um nome de parâmetro em um método derivado diferente do nome na declaração de base pode causar confusão em relação à possibilidade do método ser uma substituição do método de base ou de uma nova sobrecarga do método.|
|[CA1719: os nomes de parâmetro não devem corresponder aos nomes de membro](../code-quality/ca1719.md)|Um nome de parâmetro deve comunicar o significado de um parâmetro e um nome de membro deve comunicar o significado de um membro. Seria um design raro se eles fossem iguais. A nomenclatura de um parâmetro com o mesmo nome do membro não é intuitiva e dificulta o uso da biblioteca.|
|[CA1701: as palavras compostas da cadeia de caracteres de recurso devem ter maiúsculas e minúsculas corretas](../code-quality/ca1701.md)|Cada palavra na cadeia de caracteres de recurso é dividida em tokens baseados em maiúsculas e minúsculas. Cada combinação contígua de dois tokens é verificada pela biblioteca do verificador ortográfico da Microsoft. Se reconhecidas, as palavras produzirão uma violação da regra.|
|[CA1703: as cadeias de caracteres do recurso devem ter a ortografia correta](../code-quality/ca1703.md)|Uma cadeia de caracteres de recurso contém uma ou mais palavras não reconhecidas pela biblioteca do verificador ortográfico da Microsoft.|
|[CA1724: os nomes de tipo não devem corresponder a namespaces](../code-quality/ca1724.md)|Os nomes de tipo não devem corresponder aos nomes dos namespaces do .NET. A violação dessa regra pode reduzir a usabilidade da biblioteca.|
|[CA1707: os identificadores não devem conter sublinhados](../code-quality/ca1707.md)|Por convenção, os nomes de identificador não contêm o caractere de sublinhado (_). Esta regra verifica namespaces, tipos, membros e parâmetros.|
|[CA1721: nomes de propriedade não devem corresponder a métodos get](../code-quality/ca1721.md)|O nome de um membro público ou protegido começa com "Get" e, de outra forma, corresponde ao nome de uma propriedade pública ou protegida. Métodos "Get" e propriedades devem ter nomes que diferenciem claramente a função.|
|[CA1716: os identificadores não devem corresponder a palavras-chave](../code-quality/ca1716.md)|Um nome de namespace ou um nome de tipo corresponde a uma palavra-chave reservada em uma linguagem de programação. Os identificadores de namespaces e tipos não devem corresponder a palavras-chave definidas por com o Common Language Runtime como destino.|
|[CA1726: usar termos preferenciais](../code-quality/ca1726.md)|O nome de um identificador visível externamente inclui um termo para o qual existe um termo preferido, alternativo. Como alternativa, o nome inclui o termo "Flag" ou "Flags".|
|[CA1709: os identificadores devem ter maiúsculas e minúsculas corretas](../code-quality/ca1709.md)|Por convenção, os nomes de parâmetro usam o camel case, e os nomes de namespace, tipo e membro usam a embalagem do Pascal.|
|[CA1702: palavras compostas devem ter maiúsculas e minúsculas corretas](../code-quality/ca1702.md)|O nome de um identificador contém várias palavras e pelo menos uma das palavras parece ser uma palavra composta que não tem maiúsculas corretas.|
|[CA1712: não usar valores de enum como prefixo com o nome do tipo](../code-quality/ca1712.md)|Os nomes dos membros de enumeração não são prefixados com o nome do tipo porque as informações de tipo devem ser fornecidas pelas ferramentas de desenvolvimento.|
|[CA1710: os identificadores devem ter o sufixo correto](../code-quality/ca1710.md)|Por convenção, os nomes de tipos que estendem determinados tipos de base ou que implementam determinadas interfaces, ou tipos derivados desses tipos, têm um sufixo associado ao tipo ou interface base.|
