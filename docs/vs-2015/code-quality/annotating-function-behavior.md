---
title: Anotando o comportamento da função | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 13
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: 88213e1cd8112aecac527f7d72d2d74dbf10c559
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51783123"
---
# <a name="annotating-function-behavior"></a>Anotando o comportamento da função
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Além de anotar [parâmetros de função e valores de retorno](../code-quality/annotating-function-parameters-and-return-values.md), você pode anotar as propriedades da função inteira.  
  
## <a name="function-annotations"></a>Anotações da função  
 As anotações a seguir se aplicam para a função como um todo e descrevem como ele se comporta, ou o que espera ser verdadeira.  
  
|Anotação|Descrição|  
|----------------|-----------------|  
|`_Called_from_function_class_(name)`|Não se destina a autônomo; em vez disso, ele é um predicado a ser usado com o `_When_` anotação. Para obter mais informações, consulte [especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md).<br /><br /> O `name` parâmetro é uma cadeia de caracteres arbitrária que também aparece em um `_Function_class_` anotação na declaração de algumas funções.  `_Called_from_function_class_` Retorna não zero se a função que está sendo analisada no momento é anotada com o uso `_Function_class_` que tem o mesmo valor de `name`; caso contrário, ele retorna zero.|  
|`_Check_return_`|Anota um valor de retorno e indica que o chamador deve inspecionar. O verificador relata um erro se a função é chamada em um contexto de void.|  
|`_Function_class_(name)`|O `name` parâmetro é uma cadeia de caracteres arbitrária que é designada pelo usuário.  Ela existe em um namespace diferente de outros namespaces. Uma função, o ponteiro de função, ou — mais utilmente — um tipo de ponteiro de função pode ser designado como pertencente a uma ou mais classes de função.|  
|`_Raises_SEH_exception_`|Anota uma função que sempre gera uma exceção de (SEH) do manipulador de exceção estruturada, sujeito à `_When_` e `_On_failure_` condições. Para obter mais informações, consulte [especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md).|  
|`_Maybe_raises_SEH_exception_`|Anota uma função que, opcionalmente, pode gerar uma exceção SEH, sujeitos aos `_When_` e `_On_failure_` condições.|  
|`_Must_inspect_result_`|Anota a qualquer valor de saída, incluindo o valor de retorno, parâmetros e globais.  O analisador relatará um erro se o valor no objeto anotado subsequentemente não foi inspecionado. "Inspeção" inclui se ele é usado em uma expressão condicional, é atribuído a um parâmetro de saída ou global ou é passado como um parâmetro.  Para valores de retorno `_Must_inspect_result_` implica `_Check_return_`.|  
|`_Use_decl_annotations_`|Pode ser usada em uma definição de função (também conhecido como o corpo de uma função) no lugar da lista de anotações no cabeçalho.  Quando `_Use_decl_annotations_` é usado, as anotações que aparecem em um cabeçalho de dentro do escopo para a mesma função são usadas como se eles também estão presentes na definição do que tem o `_Use_decl_annotations_` anotação.|  
  
## <a name="successfailure-annotations"></a>Anotações de êxito/falha  
 Uma função pode falhar, e quando ele faz, seus resultados podem estar incompletas ou diferentes dos resultados quando a função for bem-sucedida.  As anotações na lista a seguir fornecem maneiras de expressar o comportamento de falha.  Para usar essas anotações, você deve habilitá-las determinar o sucesso. Portanto, um `_Success_` anotação é obrigatória.  Observe que `NTSTATUS` e `HRESULT` já tem um `_Success_` anotação incorporada a eles; no entanto, se você especificar seus próprios `_Success_` anotação no `NTSTATUS` ou `HRESULT`, ela substitui a anotação internos.  
  
|Anotação|Descrição|  
|----------------|-----------------|  
|`_Always_(anno_list)`|Equivalente a `anno_list _On_failure_(anno_list)`; ou seja, as anotações no `anno_list` se aplicam independentemente da função for bem-sucedida ou não.|  
|`_On_failure_(anno_list)`|A ser usado somente quando `_Success_` também é usado para anotar a função — explícita ou implicitamente por meio de `_Return_type_success_` em um typedef. Quando o `_On_failure_` anotação está presente em uma função parâmetro ou valor retornado, cada anotação na `anno_list` (anno) se comporta como se ele tivesse sido codificado como `_When_(!expr, anno)`, onde `expr` é o parâmetro necessário `_Success_` anotação. Isso significa que o aplicativo implícito da `_Success_` não se aplicam a todas as pós-condições para `_On_failure_`.|  
|`_Return_type_success_(expr)`|Pode ser aplicado a um typedef. Indica que todas as funções que retornam de tipo e não que explicitamente têm `_Success_` são anotadas como se tivessem `_Success_(expr)`. `_Return_type_success_` não pode ser usado em uma função ou um typedef de ponteiro de função.|  
|`_Success_(expr)`|`expr` é uma expressão que produz um rvalue. Quando o `_Success_` anotação está presente em uma declaração de função ou definição; cada anotação (`anno`) a função e em pós-condições que se comporta como se ele tivesse sido codificado como `_When_(expr, anno)`. O `_Success_` anotação pode ser usado apenas em uma função, não em seus parâmetros ou tipo de retorno. Pode haver no máximo um `_Success_` anotação em uma função e ele não pode estar em qualquer `_When_`, `_At_`, ou `_Group_`. Para obter mais informações, consulte [especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Usando anotações de SAL para reduzir defeitos de código C/C++](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [Noções básicas de SAL](../code-quality/understanding-sal.md)   
 [Anotando parâmetros de função e valores de retorno](../code-quality/annotating-function-parameters-and-return-values.md)   
 [Anotando estruturas e Classes](../code-quality/annotating-structs-and-classes.md)   
 [Anotando o comportamento de bloqueio](../code-quality/annotating-locking-behavior.md)   
 [Especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md)   
 [Funções intrínsecas](../code-quality/intrinsic-functions.md)   
 [Práticas recomendadas e exemplos](../code-quality/best-practices-and-examples-sal.md)



