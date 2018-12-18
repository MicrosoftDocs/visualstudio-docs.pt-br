---
title: Anotando o comportamento da função
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- _On_failure_
- _Return_type_success_
- _Always_
- _Maybe_raises_SEH_exception_
- _Raises_SEH_exception_
- _Called_from_function_class_
- _Function_class_
- _Must_inspect_result_
- _Success_
- _Check_return_
- _Use_decl_annotations_
ms.assetid: c0aa268d-6fa3-4ced-a8c6-f7652b152e61
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- multiple
ms.openlocfilehash: 7ee46c277574b9ceec2c4b0a26685570d305990f
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31899349"
---
# <a name="annotating-function-behavior"></a>Anotando o comportamento da função
Além das anotações [parâmetros de função e valores de retorno](../code-quality/annotating-function-parameters-and-return-values.md), você pode anotar as propriedades da função inteira.

## <a name="function-annotations"></a>Anotações da função
 As anotações a seguir se aplicam a função como um todo e descrevem como ele se comporta ou o que espera seja verdadeira.

|Anotação|Descrição|
|----------------|-----------------|
|`_Called_from_function_class_(name)`|Não se destina a ser autônoma; em vez disso, ele é um predicado a ser usado com o `_When_` anotação. Para obter mais informações, consulte [especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md).<br /><br /> O `name` parâmetro é uma cadeia de caracteres arbitrária que também é exibida em um `_Function_class_` anotação na declaração de algumas funções.  `_Called_from_function_class_` Retorna zero se a função que está sendo analisada está anotada usando `_Function_class_` que tem o mesmo valor de `name`; caso contrário, retorna zero.|
|`_Check_return_`|Anota um valor de retorno e indica que o chamador deve inspecionar. O verificador de relata um erro se a função é chamada em um contexto de void.|
|`_Function_class_(name)`|O `name` parâmetro é uma cadeia de caracteres arbitrária que é designada pelo usuário.  Ela existe em um namespace que é diferente de outros namespaces. Uma função, o ponteiro de função, ou — mais útil — um tipo de ponteiro de função pode ser designado como pertencente a uma ou mais classes de função.|
|`_Raises_SEH_exception_`|Anota uma função que sempre gera uma exceção de manipulador (SEH) estruturado de exceções, sujeito a `_When_` e `_On_failure_` condições. Para obter mais informações, consulte [especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md).|
|`_Maybe_raises_SEH_exception_`|Anota uma função que pode opcionalmente gerar uma exceção SEH, sujeito a `_When_` e `_On_failure_` condições.|
|`_Must_inspect_result_`|Anota qualquer valor de saída, incluindo o valor de retorno, parâmetros e globais.  O analisador relata um erro se o valor do objeto anotado não é inspecionado posteriormente. "Inspeção" inclui se ele é usado em uma expressão condicional, é atribuído a um parâmetro de saída ou global ou é passado como um parâmetro.  Para valores de retorno, `_Must_inspect_result_` implica `_Check_return_`.|
|`_Use_decl_annotations_`|Pode ser usado em uma definição de função (também conhecido como um corpo de função) no lugar da lista de anotações no cabeçalho.  Quando `_Use_decl_annotations_` é usado, as anotações que aparecem em um cabeçalho em escopo para a mesma função são usadas como se eles também estão presentes na definição do que tem o `_Use_decl_annotations_` anotação.|

## <a name="successfailure-annotations"></a>Anotações de êxito/falha
 Uma função pode falhar, e quando isso acontecer, seus resultados podem estar incompletos ou diferem dos resultados quando a função tiver êxito.  As anotações na lista a seguir fornecem maneiras de expressar o comportamento de falha.  Para usar essas anotações, você deve habilitá-las determinar o sucesso. Portanto, um `_Success_` anotação é necessária.  Observe que `NTSTATUS` e `HRESULT` já tem um `_Success_` anotação internos; no entanto, se você especificar sua própria `_Success_` anotação em `NTSTATUS` ou `HRESULT`, ela substitui a anotação interna.

|Anotação|Descrição|
|----------------|-----------------|
|`_Always_(anno_list)`|Equivalente a `anno_list _On_failure_(anno_list)`; ou seja, as anotações na `anno_list` se aplicam se a função tiver êxito ou não.|
|`_On_failure_(anno_list)`|Para ser usado apenas quando `_Success_` também é usado para anotar a função — explícita ou implicitamente por meio de `_Return_type_success_` em um typedef. Quando o `_On_failure_` anotação está presente em um função parâmetro ou do valor retornado, cada anotação em `anno_list` (anno) se comporta como se ele foi codificado como `_When_(!expr, anno)`, onde `expr` é o parâmetro obrigatório `_Success_` anotação. Isso significa que o aplicativo implícito de `_Success_` não se aplicam a todas as pós-condições de para `_On_failure_`.|
|`_Return_type_success_(expr)`|Pode ser aplicado a um typedef. Indica que todas as funções que retornam que tipo e não têm explicitamente `_Success_` são anotados como se tivessem `_Success_(expr)`. `_Return_type_success_` não pode ser usado em uma função ou um typedef de ponteiro de função.|
|`_Success_(expr)`|`expr` é uma expressão que produz um rvalue. Quando o `_Success_` anotação está presente em uma declaração de função ou definição, cada anotação (`anno`) na função e pós-condição se comporta como se ele foi codificado como `_When_(expr, anno)`. O `_Success_` anotação pode ser usado apenas em uma função, não em seus parâmetros ou tipo de retorno. Pode haver no máximo uma `_Success_` anotação em uma função e ele não pode estar em qualquer `_When_`, `_At_`, ou `_Group_`. Para obter mais informações, consulte [especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md).|

## <a name="see-also"></a>Consulte também
 [Usando anotações de SAL para reduzir defeitos de código C/C++](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md) [Compreendendo SAL](../code-quality/understanding-sal.md) [anotando parâmetros de função e valores de retorno](../code-quality/annotating-function-parameters-and-return-values.md) [anotando estruturas e Classes](../code-quality/annotating-structs-and-classes.md) [Anotando o comportamento de bloqueio](../code-quality/annotating-locking-behavior.md) [especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md) [funções intrínsecas](../code-quality/intrinsic-functions.md) [práticas recomendadas e Exemplos](../code-quality/best-practices-and-examples-sal.md)