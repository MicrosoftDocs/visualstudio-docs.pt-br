---
title: Funções intrínsecas | Microsoft Docs
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
- _String_length_
- _Param_
- _Curr_
- _Old_
- _Nullterm_length_
- _Inexpressible_
ms.assetid: adf29f8c-89fd-4a5e-9804-35ac83e1c457
caps.latest.revision: 9
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: 7258092b79ca0c10079a986e2a80b34c25660054
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51788102"
---
# <a name="intrinsic-functions"></a>Funções intrínsecas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Uma expressão no SAL pode ser uma expressão de C/C++, desde que seja uma expressão que não tem efeitos colaterais — por exemplo, + +, -- e chamadas de função, todos têm efeitos colaterais neste contexto.  No entanto, o SAL fornecem alguns objetos de função e alguns símbolos reservados que podem ser usados em expressões de SAL. Esses são denominados *funções intrínsecas*.  
  
## <a name="general-purpose"></a>Uso geral  
 As seguintes anotações da função instrinsic fornecem utilitário gerais de SAL.  
  
|Anotação|Descrição|  
|----------------|-----------------|  
|`_Curr_`|Um sinônimo para o objeto que está sendo anotado no momento.  Quando o `_At_` anotação está em uso, `_Curr_` é o mesmo que o primeiro parâmetro para `_At_`.  Caso contrário, ele é o parâmetro ou o valor de inteiro/retorno de função ao qual a anotação está lexicalmente associada.|  
|`_Inexpressible_(expr)`|Expressa uma situação em que o tamanho de um buffer é muito complexo para representar por meio de uma expressão de anotação — por exemplo, quando ela é calculada pela verificação de um conjunto de dados de entrada e, em seguida, contar membros selecionados.|  
|`_Nullterm_length_(param)`|`param` é o número de elementos no buffer até, mas não incluindo um terminador nulo. Ele pode ser aplicado a qualquer buffer de tipo não agregado, não nulo.|  
|`_Old_(expr)`|Quando ela é avaliada de pré-condição, `_Old_` retorna o valor de entrada `expr`.  Quando ela é avaliada em pós-condições, ele retorna o valor `expr` conforme ele seria avaliado na pré-condição.|  
|`_Param_(n)`|O `n`º parâmetro para uma função, contando a partir de 1 para `n`, e `n` é uma literal constante integral. Se o parâmetro é chamado, essa anotação é idêntica ao acessar o parâmetro por nome. **Observação:** `n` podem se referir a parâmetros posicionais que são definidos por um sinal de reticências, ou podem ser usados em protótipos de função em que os nomes não são usados.|  
|`return`|Palavra-chave reservada do C/C++ `return` pode ser usado em uma expressão de SAL para indicar o valor de retorno de uma função.  O valor só está disponível no estado de post; é um erro de sintaxe para usá-lo em um estado anterior.|  
  
## <a name="string-specific"></a>Cadeia de caracteres específica  
 As anotações a função intrínseca seguir habilitam a manipulação de cadeias de caracteres. Todos os quatro dessas funções têm a mesma finalidade: para retornar o número de elementos do tipo que for encontrado antes de um terminador nulo. As diferenças são os tipos de dados em elementos que são chamados. Observe que se você quiser especificar o comprimento de uma terminação nula de buffers que não é composto de caracteres, use o `_Nullterm_length_(param)` anotação da seção anterior.  
  
|Anotação|Descrição|  
|----------------|-----------------|  
|`_String_length_(param)`|`param` é o número de elementos na cadeia de caracteres até, mas não incluindo um terminador nulo. Essa anotação é reservada para tipos de cadeia de caracteres.|  
|`strlen(param)`|`param` é o número de elementos na cadeia de caracteres até, mas não incluindo um terminador nulo. Essa anotação é reservada para uso em caracteres, matrizes e se parece com a função de tempo de execução C [strlen](http://msdn.microsoft.com/library/16462f2a-1e0f-4eb3-be55-bf1c83f374c2).|  
|`wcslen(param)`|`param` é o número de elementos na cadeia de caracteres até (mas não incluindo) um terminador nulo. Essa anotação é reservada para uso no caractere largo matrizes e se parece com a função de tempo de execução C [wcslen](http://msdn.microsoft.com/library/16462f2a-1e0f-4eb3-be55-bf1c83f374c2).|  
  
## <a name="see-also"></a>Consulte também  
 [Usando anotações de SAL para reduzir defeitos de código C/C++](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [Noções básicas de SAL](../code-quality/understanding-sal.md)   
 [Anotando parâmetros de função e valores de retorno](../code-quality/annotating-function-parameters-and-return-values.md)   
 [Anotando o comportamento da função](../code-quality/annotating-function-behavior.md)   
 [Anotando estruturas e Classes](../code-quality/annotating-structs-and-classes.md)   
 [Anotando o comportamento de bloqueio](../code-quality/annotating-locking-behavior.md)   
 [Especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md)   
 [Práticas recomendadas e exemplos](../code-quality/best-practices-and-examples-sal.md)



