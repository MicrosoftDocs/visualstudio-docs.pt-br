---
title: Funções intrínsecas
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- _String_length_
- _Param_
- _Curr_
- _Old_
- _Nullterm_length_
- _Inexpressible_
ms.assetid: adf29f8c-89fd-4a5e-9804-35ac83e1c457
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- multiple
ms.openlocfilehash: 0e58f84a48104553e5517d24f746769e6f0959e5
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31920942"
---
# <a name="intrinsic-functions"></a>Funções intrínsecas
Uma expressão em SAL pode ser uma expressão de C/C++, desde que seja uma expressão que não têm efeitos colaterais — por exemplo, + +, -- e chamadas de função todos têm efeitos colaterais nesse contexto.  No entanto, SAL fornecem alguns objetos de função e alguns símbolos reservados que podem ser usados em expressões de SAL. Esses são chamados de *funções intrínsecas*.

## <a name="general-purpose"></a>Uso geral
 As seguintes anotações da função instrinsic fornecem utilitário geral de SAL.

|Anotação|Descrição|
|----------------|-----------------|
|`_Curr_`|Um sinônimo para o objeto que está sendo anotado no momento.  Quando o `_At_` anotação está em uso, `_Curr_` é o mesmo que o primeiro parâmetro para `_At_`.  Caso contrário, é o parâmetro ou o valor de inteiro/retorno de função ao qual a anotação está lexicalmente associada.|
|`_Inexpressible_(expr)`|Expressa uma situação em que o tamanho de um buffer é muito complexo para representar usando uma expressão de anotação — por exemplo, quando ele é calculado pela verificação de um conjunto de dados de entrada e, em seguida, contar membros selecionados.|
|`_Nullterm_length_(param)`|`param` é o número de elementos no buffer até, mas não incluindo um terminador nulo. Ele pode ser aplicado a qualquer buffer de tipo não agregado, não nulo.|
|`_Old_(expr)`|Quando ele é avaliado na pré-condição, `_Old_` retorna o valor de entrada `expr`.  Quando ele é avaliado em pós-condições, ela retorna o valor `expr` como ele será avaliado na pré-condição.|
|`_Param_(n)`|O `n`º parâmetro para uma função, contando a partir de 1 a `n`, e `n` é uma literal constante integral. Se o parâmetro é chamado, essa anotação é idêntica ao acessar o parâmetro pelo nome. **Observação:** `n` podem consultar os parâmetros posicionais que são definidos por um sinal de reticências, ou podem ser usados em protótipos de função em que os nomes não são usados.  |
|`return`|Palavra-chave reservadas para C/C++ `return` pode ser usado em uma expressão de SAL para indicar o valor de retorno de uma função.  O valor só está disponível no estado de post. é um erro de sintaxe para usá-lo em um estado anterior.|

## <a name="string-specific"></a>Cadeia de caracteres específica
 As seguintes anotações da função intrínseca permitem a manipulação de cadeias de caracteres. Todos os quatro dessas funções têm a mesma finalidade: para retornar o número de elementos do tipo que está localizado antes de um terminador nulo. As diferenças são os tipos de dados dos elementos que são chamadas. Observe que, se você quiser especificar o comprimento de uma terminação nula de buffers que não é composto de caracteres, use o `_Nullterm_length_(param)` anotação da seção anterior.

|Anotação|Descrição|
|----------------|-----------------|
|`_String_length_(param)`|`param` é o número de elementos na cadeia de caracteres até, mas não incluindo um terminador nulo. Esta anotação é reservada para tipos de cadeia de caracteres.|
|`strlen(param)`|`param` é o número de elementos na cadeia de caracteres até, mas não incluindo um terminador nulo. Esta anotação é reservada para uso em caractere matrizes e é semelhante a função do tempo de execução do C [strlen()](/cpp/c-runtime-library/reference/strlen-wcslen-mbslen-mbslen-l-mbstrlen-mbstrlen-l).|
|`wcslen(param)`|`param` é o número de elementos na cadeia de caracteres até (mas não incluindo) um terminador nulo. Esta anotação é reservada para uso em caractere largo matrizes e é semelhante a função do tempo de execução do C [wcslen()](/cpp/c-runtime-library/reference/strlen-wcslen-mbslen-mbslen-l-mbstrlen-mbstrlen-l).|

## <a name="see-also"></a>Consulte também
 [Usando anotações de SAL para reduzir defeitos de código C/C++](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md) [Compreendendo SAL](../code-quality/understanding-sal.md) [anotando parâmetros de função e valores de retorno](../code-quality/annotating-function-parameters-and-return-values.md) [anotando o comportamento da função](../code-quality/annotating-function-behavior.md) [Anotando estruturas e Classes](../code-quality/annotating-structs-and-classes.md) [anotando o comportamento de bloqueio](../code-quality/annotating-locking-behavior.md) [especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md) [práticas recomendadas e exemplos](../code-quality/best-practices-and-examples-sal.md)