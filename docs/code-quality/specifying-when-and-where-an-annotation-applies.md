---
title: Especificando quando e onde uma anotação se aplica
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- _Group_
- _At_
- _When_
- _At_buffer_
ms.assetid: 8e4f4f9c-5dfa-4835-87df-ecd1698fc650
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- multiple
ms.openlocfilehash: f6efcc158ea0b5b2e44a5b9d0750bc897e442994
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2020
ms.locfileid: "77271844"
---
# <a name="specifying-when-and-where-an-annotation-applies"></a>Especificando quando e onde uma anotação se aplica
Quando uma anotação é condicional, ela pode exigir outras anotações para especificar que o analisador.  Por exemplo, se uma função tiver uma variável que possa ser síncrona ou assíncrona, a função se comportará da seguinte maneira: no caso síncrono, ela sempre será bem sucedido, mas, no caso assíncrono, relatará um erro se ele não puder ser bem executado imediatamente. Quando a função é chamada de forma síncrona, a verificação do valor de resultado não fornece nenhum valor para o analisador de código, pois ele não teria retornado.  No entanto, quando a função é chamada de forma assíncrona e o resultado da função não é verificado, pode ocorrer um erro sério. Este exemplo ilustra uma situação na qual você pode usar a anotação `_When_`, descrita mais adiante neste artigo, para habilitar a verificação.

## <a name="structural-annotations"></a>Anotações estruturais
Para controlar quando e onde as anotações se aplicam, use as seguintes anotações estruturais.

|Anotação|DESCRIÇÃO|
|----------------|-----------------|
|`_At_(expr, anno-list)`|`expr` é uma expressão que produz um lvalue. As anotações em `anno-list` são aplicadas ao objeto nomeado por `expr`. Para cada anotação no `anno-list`, `expr` será interpretado em condição prévia se a anotação for interpretada em pré-condição e, em pós-condição, se a anotação for interpretada em pós-condição.|
|`_At_buffer_(expr, iter, elem-count, anno-list)`|`expr` é uma expressão que produz um lvalue. As anotações em `anno-list` são aplicadas ao objeto nomeado por `expr`. Para cada anotação no `anno-list`, `expr` será interpretado em condição prévia se a anotação for interpretada em pré-condição e, em pós-condição, se a anotação for interpretada em pós-condição.<br /><br /> `iter` é o nome de uma variável que tem o escopo da anotação (inclusive `anno-list`). `iter` tem um tipo implícito `long`. Variáveis nomeadas de forma idêntica em qualquer escopo delimitador são ocultas da avaliação.<br /><br /> `elem-count` é uma expressão que é avaliada como um inteiro.|
|`_Group_(anno-list)`|As anotações em `anno-list` são consideradas como tendo qualquer qualificador que se aplique à anotação de grupo que é aplicada a cada anotação.|
|`_When_(expr, anno-list)`|`expr` é uma expressão que pode ser convertida em `bool`. Quando é diferente de zero (`true`), as anotações especificadas em `anno-list` são consideradas aplicáveis.<br /><br /> Por padrão, para cada anotação no `anno-list`, `expr` será interpretado como usando os valores de entrada se a anotação for uma pré-condição e como usar os valores de saída se a anotação for uma pós-condição. Para substituir o padrão, você pode usar o `_Old_` intrínseco ao avaliar uma pós-condição para indicar que os valores de entrada devem ser usados. **Observação:**  Anotações diferentes podem ser habilitadas como consequência do uso de `_When_` se um valor mutável — por exemplo, `*pLength`— estiver envolvido porque o resultado avaliado de `expr` em pré-condição pode ser diferente do resultado avaliado em post-Condition.|

## <a name="see-also"></a>Confira também

- [Usando anotações de SAL para reduzir defeitos de código do C/C++](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)
- [Noções básicas de SAL](../code-quality/understanding-sal.md)
- [Anotando parâmetros de função e valores de retorno](../code-quality/annotating-function-parameters-and-return-values.md)
- [Anotando o comportamento da função](../code-quality/annotating-function-behavior.md)
- [Anotando estruturas e classes](../code-quality/annotating-structs-and-classes.md)
- [Anotando o comportamento de bloqueio](../code-quality/annotating-locking-behavior.md)
- [Funções intrínsecas](../code-quality/intrinsic-functions.md)
- [Práticas recomendadas e exemplos](../code-quality/best-practices-and-examples-sal.md)
