---
title: Anotando o comportamento de bloqueio
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- _Releases_nonreentrant_lock_
- _Lock_kind_mutex_
- _Lock_kind_critical_section_
- _Acquires_lock_
- _Releases_lock_
- _Has_lock_kind_
- _Releases_exclusive_lock_
- _Post_same_lock_
- _Requires_exclusive_lock_held_
- _Requires_shared_lock_held_
- _Lock_kind_semaphore_
- _Requires_lock_held_
- _Acquires_exclusive_lock_
- _Create_lock_level_
- _Acquires_nonreentrant_lock_
- _Releases_shared_lock_
- _Has_lock_level_
- _Lock_kind_spin_lock_
- _Requires_lock_not_held_
- _Acquires_shared_lock_
- _Requires_no_locks_held_
- _Lock_level_order_
- _Lock_kind_event_
ms.assetid: 07769c25-9b97-4ab7-b175-d1c450308d7a
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- multiple
ms.openlocfilehash: 21c67bb8b99c2772e107ded9063a99940a7fac74
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31901522"
---
# <a name="annotating-locking-behavior"></a>Anotando o comportamento de bloqueio
Para evitar erros de simultaneidade em seu programa multithread, sempre siga uma disciplina de bloqueio apropriada e use anotações SAL.

 Bugs de simultaneidade são notoriamente difíceis de reproduzir, diagnosticar e depurar porque eles são não determinísticas. Raciocínio sobre a intercalação de thread é difícil na melhor das hipóteses e se torna prático quando você estiver criando um corpo de código que tem mais de alguns segmentos. Portanto, é uma boa prática seguir uma bloqueio disciplina em seus programas multithread. Por exemplo, obedecer a um pedido de bloqueio enquanto adquirir vários bloqueios ajuda a evitar deadlocks e adquirir o bloqueio de proteção adequado antes de acessar um recurso compartilhado ajuda a evitar condições de corrida.

 Infelizmente, aparentemente simples regras de bloqueio podem ser surpreendentemente difícil a seguir na prática. Uma limitação fundamental em linguagens de programação e a compiladores de hoje é que eles não diretamente dão suporte a especificação e análise dos requisitos de simultaneidade. Os programadores deve contar com os comentários de código informal para expressar suas intenções sobre como usar bloqueios.

 Anotações de SAL de simultaneidade são projetadas para ajudá-lo a especificar o bloqueio efeitos colaterais, bloqueio de responsabilidade, guardianship de dados, hierarquia de ordem de bloqueio e outro comportamento esperado de bloqueio. Fazendo regras implícitas explícita, as anotações SAL simultaneidade fornecem uma maneira consistente para documentar como o seu código usa regras de bloqueio. Anotações de simultaneidade também aprimoram a capacidade de ferramentas de análise de código para localizar condições de corrida, deadlocks, operações de sincronização não correspondentes e outros erros sutis simultaneidade.

## <a name="general-guidelines"></a>Diretrizes gerais
 Usando anotações, você pode declarar os contratos que são implícito de definições de função entre implementações (chamados) e clientes (chamadores) e invariáveis express e outras propriedades do programa que podem melhoram a análise.

 SAL dá suporte a vários tipos diferentes de primitivos de bloqueio — por exemplo, seções críticas, mutexes, bloqueios de rotação e outros objetos de recurso. Muitas anotações de simultaneidade levar uma expressão de bloqueio como um parâmetro. Por convenção, um bloqueio é denotado por expressão de caminho do objeto subjacente do bloqueio.

 Algumas regras de propriedade de thread para ter em mente:

-   Bloqueios de rotação são uncounted bloqueios que têm a propriedade de thread clara.

-   Mutexes e seções críticas são contadas bloqueios que têm a propriedade de thread clara.

-   Semáforos e eventos são contados bloqueios que não têm a propriedade de thread clara.

## <a name="locking-annotations"></a>Anotações de bloqueio
 A tabela a seguir lista as anotações de bloqueio.

|Anotação|Descrição|
|----------------|-----------------|
|`_Acquires_exclusive_lock_(expr)`|Anota uma função e indica que postagem de estado a função incrementa em um a contagem de bloqueio exclusivo do objeto de bloqueio que é chamada por `expr`.|
|`_Acquires_lock_(expr)`|Anota uma função e indica que postagem de estado a função incrementa em um a contagem de bloqueio do objeto de bloqueio que é chamada por `expr`.|
|`_Acquires_nonreentrant_lock_(expr)`|O bloqueio que é chamado por `expr` é adquirido.  Um erro será relatado se o bloqueio já é mantido.|
|`_Acquires_shared_lock_(expr)`|Anota uma função e indica que postagem de estado a função incrementa em um a contagem de bloqueio compartilhado do objeto de bloqueio que é chamada por `expr`.|
|`_Create_lock_level_(name)`|Uma instrução que declara o símbolo `name` como um nível de bloqueio para que ele pode ser usado nas anotações `_Has_Lock_level_` e `_Lock_level_order_`.|
|`_Has_lock_kind_(kind)`|Anota qualquer objeto para refinar as informações de tipo de um objeto de recurso. Às vezes, um tipo comum é usado para diferentes tipos de recursos e o tipo sobrecarregado não é suficiente para distinguir os requisitos de semânticos entre vários recursos. Aqui está uma lista de predefinido `kind` parâmetros:<br /><br /> `_Lock_kind_mutex_`<br /> ID de tipo de bloqueio por mutexes.<br /><br /> `_Lock_kind_event_`<br /> ID de tipo de bloqueio de eventos.<br /><br /> `_Lock_kind_semaphore_`<br /> ID de tipo de bloqueio de semáforos.<br /><br /> `_Lock_kind_spin_lock_`<br /> ID de tipo de bloqueio para bloqueios de rotação.<br /><br /> `_Lock_kind_critical_section_`<br /> ID de tipo de bloqueio para seções críticas.|
|`_Has_lock_level_(name)`|Anota um objeto de bloqueio e concede a ele o nível de bloqueio de `name`.|
|`_Lock_level_order_(name1, name2)`|Uma instrução que fornece o bloqueio de ordenação entre `name1` e `name2`.|
|`_Post_same_lock_(expr1, expr2)`|Anota uma função e indica que postagem de estado dois bloqueios, `expr1` e `expr2`, são tratados como se eles são o mesmo objeto de bloqueio.|
|`_Releases_exclusive_lock_(expr)`|Anota uma função e indica que postagem estado diminui a função por um a contagem de bloqueio exclusivo do objeto de bloqueio que é chamada por `expr`.|
|`_Releases_lock_(expr)`|Anota uma função e indica que postagem estado diminui a função por um a contagem de bloqueio do objeto de bloqueio que é chamada por `expr`.|
|`_Releases_nonreentrant_lock_(expr)`|O bloqueio que é chamado por `expr` é liberado. Um erro será relatado se o bloqueio não é mantido atualmente.|
|`_Releases_shared_lock_(expr)`|Anota uma função e indica que postagem estado diminui a função por um a contagem de bloqueio compartilhado do objeto de bloqueio que é chamada por `expr`.|
|`_Requires_lock_held_(expr)`|Anota uma função e indica que, na versão anterior, estado a contagem de bloqueio do objeto que é chamada por `expr` é pelo menos um.|
|`_Requires_lock_not_held_(expr)`|Anota uma função e indica que, na versão anterior, estado a contagem de bloqueio do objeto que é chamada por `expr` é zero.|
|`_Requires_no_locks_held_`|Anota uma função e indica que as contagens de bloqueio de todos os bloqueios que são conhecidos para o verificador de zero.|
|`_Requires_shared_lock_held_(expr)`|Anota uma função e indica que, na versão anterior, estado a contagem de bloqueio compartilhado do objeto que é chamada por `expr` é pelo menos um.|
|`_Requires_exclusive_lock_held_(expr)`|Anota uma função e indica que, na versão anterior, estado a contagem de bloqueio exclusivo do objeto que é chamada por `expr` é pelo menos um.|

## <a name="sal-intrinsics-for-unexposed-locking-objects"></a>SAL intrínsecos para objetos de bloqueio não expostos
 Determinados objetos de bloqueio não são expostos pela implementação das funções de bloqueio associadas.  A tabela a seguir lista variáveis SAL intrínsecos habilitar anotações em funções que operam nesses objetos de bloqueio não exposta.

|Anotação|Descrição|
|----------------|-----------------|
|`_Global_cancel_spin_lock_`|Descreve o bloqueio de rotação de cancelamento.|
|`_Global_critical_region_`|Descreve a região crítica.|
|`_Global_interlock_`|Descreve as operações integradas.|
|`_Global_priority_region_`|Descreve a região de prioridade.|

## <a name="shared-data-access-annotations"></a>Anotações de acesso de dados compartilhados
 A tabela a seguir lista as anotações para acesso de dados compartilhada.

|Anotação|Descrição|
|----------------|-----------------|
|`_Guarded_by_(expr)`|Anota uma variável e indica que sempre que a variável é acessada, a contagem de bloqueio do objeto de bloqueio que é chamada por `expr` é pelo menos um.|
|`_Interlocked_`|Anota uma variável e é equivalente a `_Guarded_by_(_Global_interlock_)`.|
|`_Interlocked_operand_`|O parâmetro de função anotado é o operando de destino de uma das várias funções Interlocked.  Os operandos devem ter propriedades adicionais específicas.|
|`_Write_guarded_by_(expr)`|Anota uma variável e indica que sempre que a variável é modificada, a contagem de bloqueio do objeto de bloqueio que é chamada por `expr` é pelo menos um.|

## <a name="see-also"></a>Consulte também
 [Usando anotações de SAL para reduzir defeitos de código C/C++](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md) [Compreendendo SAL](../code-quality/understanding-sal.md) [anotando parâmetros de função e valores de retorno](../code-quality/annotating-function-parameters-and-return-values.md) [anotando o comportamento da função](../code-quality/annotating-function-behavior.md) [Anotando estruturas e Classes](../code-quality/annotating-structs-and-classes.md) [especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md) [funções intrínsecas](../code-quality/intrinsic-functions.md) [práticas recomendadas e Exemplos](../code-quality/best-practices-and-examples-sal.md) [Blog da equipe de análise de código](http://go.microsoft.com/fwlink/p/?LinkId=251197)