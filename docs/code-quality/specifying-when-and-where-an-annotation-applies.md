---
title: Especificando quando e onde uma anotação se aplica
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- _Group_
- _At_
- _When_
- _At_buffer_
ms.assetid: 8e4f4f9c-5dfa-4835-87df-ecd1698fc650
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- multiple
ms.openlocfilehash: 9d99ebce3adc27039763e11ed4882a20199e8469
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31920609"
---
# <a name="specifying-when-and-where-an-annotation-applies"></a>Especificando quando e onde uma anotação se aplica
Quando uma anotação condicional, ele pode exigir outras anotações para especificar que o analisador.  Por exemplo, se uma função tem uma variável que pode ser síncronas ou assíncronas, a função se comporta da seguinte maneira: no caso síncrono sempre eventualmente tiver êxito, mas no caso assíncrono relata um erro se ele não pode ser bem-sucedida imediatamente. Quando a função é chamada de forma síncrona, verificar o valor do resultado não fornece um valor para o analisador de código porque não poderia ter retornado.  No entanto, quando a função é chamada de forma assíncrona e o resultado da função não estiver marcado, pode ocorrer um erro grave. Este exemplo ilustra uma situação em que você pode usar o `_When_` anotação — descrito posteriormente neste artigo, para habilitar a verificação.

## <a name="structural-annotations"></a>Anotações estruturais
 Para controlar quando e onde aplicam anotações, use as seguintes anotações estruturais.

|Anotação|Descrição|
|----------------|-----------------|
|`_At_(expr, anno-list)`|`expr` é uma expressão que produz um lvalue. As anotações na `anno-list` são aplicadas ao objeto que é chamado por `expr`. Para cada anotação em `anno-list`, `expr` é interpretado em pré-condição se a anotação é interpretada da pré-condição e na pós-condição de se a anotação é interpretada da pós condição de.|
|`_At_buffer_(expr, iter, elem-count, anno-list)`|`expr` é uma expressão que produz um lvalue. As anotações na `anno-list` são aplicadas ao objeto que é chamado por `expr`. Para cada anotação em `anno-list`, `expr` é interpretado em pré-condição se a anotação é interpretada na pré-condição e na pós-condição de se a anotação é interpretada da pós condição de.<br /><br /> `iter` é o nome de uma variável que é o escopo para a anotação (inclusivo do `anno-list`). `iter` tem um tipo implícito `long`. Variáveis com o mesmo nome em qualquer escopo delimitador ficam ocultos na avaliação.<br /><br /> `elem-count` é uma expressão que é avaliada como um número inteiro.|
|`_Group_(anno-list)`|As anotações no `anno-list` são considerados ter qualquer qualificador que se aplica a anotação de grupo é aplicada a cada anotação.|
|`_When_(expr, anno-list)`|`expr` é uma expressão que pode ser convertida em `bool`. Quando ele for diferente de zero (`true`), as anotações são especificadas em `anno-list` são considerados aplicável.<br /><br /> Por padrão, para cada anotação em `anno-list`, `expr` é interpretado como usando os valores de entrada, se a anotação é uma pré-condição e como usar os valores de saída se a anotação é uma pós condição de. Para substituir o padrão, você pode usar o `_Old_` intrínseco ao avaliar uma pós-condição de para indicar que os valores de entrada devem ser usados. **Observação:** anotações diferentes podem ser habilitadas como consequência usando `_When_` se um valor mutável — por exemplo, `*pLength`— está envolvido porque o resultado avaliado da `expr` na pré-condição podem diferir das suas avaliado resulta em pós-condição.|

## <a name="see-also"></a>Consulte também
 [Usando anotações de SAL para reduzir defeitos de código C/C++](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md) [Compreendendo SAL](../code-quality/understanding-sal.md) [anotando parâmetros de função e valores de retorno](../code-quality/annotating-function-parameters-and-return-values.md) [anotando o comportamento da função](../code-quality/annotating-function-behavior.md) [Anotando estruturas e Classes](../code-quality/annotating-structs-and-classes.md) [anotando o comportamento de bloqueio](../code-quality/annotating-locking-behavior.md) [funções intrínsecas](../code-quality/intrinsic-functions.md) [práticas recomendadas e exemplos](../code-quality/best-practices-and-examples-sal.md)