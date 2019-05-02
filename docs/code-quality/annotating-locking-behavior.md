---
title: Anotando o comportamento de bloqueio
ms.date: 11/04/2016
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
ms.openlocfilehash: 6590a07ec7fc67bef5f1b1cfd96e80105fa325ce
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62560461"
---
# <a name="annotating-locking-behavior"></a>Anotando o comportamento de bloqueio
Para evitar bugs de simultaneidade em seu programa multithreaded, sempre siga uma disciplina de bloqueio apropriada e use anotações de SAL.

 Bugs de simultaneidade são notoriamente difíceis de reproduzir, diagnosticar e depurar porque eles são não determinísticas. Raciocínio sobre a intercalação de thread é difícil na melhor das hipóteses e se torna impraticável quando você estiver criando um corpo de código que tem mais de alguns segmentos. Portanto, é uma boa prática seguir uma bloqueio disciplina em seus programas multithread. Por exemplo, como obedecê uma ordem de bloqueio enquanto adquirir vários bloqueios ajuda a evitar deadlocks e adquirir o bloqueio de proteção apropriado antes de acessar um recurso compartilhado ajuda a evitar condições de corrida.

 Infelizmente, aparentemente simples regras de bloqueio podem ser surpreendentemente difícil seguir a prática. Uma limitação fundamental em compiladores e linguagens de programação de hoje é que eles não suportam diretamente a especificação e análise dos requisitos de simultaneidade. Os programadores precisam contar com comentários de código informal para expressar suas intenções sobre como eles usam bloqueios.

 Anotações de SAL de simultaneidade são projetadas para ajudar você a especificar o bloqueio efeitos colaterais, bloqueio de responsabilidade, guardianship de dados, hierarquia de ordem de bloqueio e outro comportamento esperado de bloqueio. Tornando regras implícitas explícita, anotações de simultaneidade SAL fornecem uma maneira consistente para documentar como seu código usa as regras de bloqueio. Anotações de simultaneidade também aumentam a capacidade de localizar condições de corrida, deadlocks, operações de sincronização não correspondentes e outros erros sutis de simultaneidade das ferramentas de análise de código.

## <a name="general-guidelines"></a>Diretrizes gerais
 Usando anotações, você pode declarar os contratos que são deduzidos por definições de função entre implementações (computadores chamados) e clientes (chamadores) e invariáveis de express e outras propriedades do programa que pode melhoram a análise.

 SAL dá suporte a muitos tipos diferentes de primitivos de bloqueio — por exemplo, seções críticas, mutexes, bloqueios de rotação e outros objetos de recurso. Anotações de simultaneidade de muitos levar a uma expressão de bloqueio como um parâmetro. Por convenção, um bloqueio é indicado pela expressão de caminho do objeto subjacente de bloqueio.

 Algumas regras de propriedade de thread para ter em mente:

- Bloqueios de rotação são uncounted bloqueios que têm a propriedade de thread não criptografado.

- Mutexes e seções críticas são contadas bloqueios que têm a propriedade de thread não criptografado.

- Semáforos e eventos são contados bloqueios que não têm a propriedade de thread não criptografado.

## <a name="locking-annotations"></a>Anotações de bloqueio
 A tabela a seguir lista as anotações de bloqueio.

|Anotação|Descrição|
|----------------|-----------------|
|`_Acquires_exclusive_lock_(expr)`|Anota uma função e indica que na postagem do estado a função incrementa em um a contagem de bloqueio exclusivo do objeto de bloqueio que é nomeado pelo `expr`.|
|`_Acquires_lock_(expr)`|Anota uma função e indica que na postagem do estado a função incrementa em um a contagem de bloqueio do objeto de bloqueio que é nomeado pelo `expr`.|
|`_Acquires_nonreentrant_lock_(expr)`|O bloqueio que é nomeado pelo `expr` é adquirido.  Um erro será relatado se o bloqueio já é mantido.|
|`_Acquires_shared_lock_(expr)`|Anota uma função e indica que na postagem do estado a função incrementa em um a contagem de bloqueio compartilhado do objeto de bloqueio que é nomeado pelo `expr`.|
|`_Create_lock_level_(name)`|Uma instrução que declara o símbolo `name` como um nível de bloqueio para que ele pode ser usado nas anotações `_Has_Lock_level_` e `_Lock_level_order_`.|
|`_Has_lock_kind_(kind)`|Anota a qualquer objeto para refinar as informações de tipo de um objeto de recurso. Às vezes, um tipo comum é usado para diferentes tipos de recursos e o tipo sobrecarregado não é suficiente para distinguir os requisitos de semânticos entre os vários recursos. Aqui está uma lista de predefinido `kind` parâmetros:<br /><br /> `_Lock_kind_mutex_`<br /> ID de tipo de bloqueio para mutexes.<br /><br /> `_Lock_kind_event_`<br /> ID de tipo de bloqueio para eventos.<br /><br /> `_Lock_kind_semaphore_`<br /> ID de tipo de bloqueio para semáforos.<br /><br /> `_Lock_kind_spin_lock_`<br /> ID de tipo de bloqueio para bloqueios de rotação.<br /><br /> `_Lock_kind_critical_section_`<br /> ID de tipo de bloqueio para seções críticas.|
|`_Has_lock_level_(name)`|Anota um objeto de bloqueio e concede a ele o nível de bloqueio de `name`.|
|`_Lock_level_order_(name1, name2)`|Uma instrução que fornece o bloqueio de ordenação entre `name1` e `name2`.|
|`_Post_same_lock_(expr1, expr2)`|Anota uma função e indica que, na postagem do estado dois bloqueios, `expr1` e `expr2`, são tratados como se eles forem o mesmo objeto de bloqueio.|
|`_Releases_exclusive_lock_(expr)`|Anota uma função e indica que na postagem do estado decrementa a função por um a contagem de bloqueio exclusivo do objeto de bloqueio que é nomeado pelo `expr`.|
|`_Releases_lock_(expr)`|Anota uma função e indica que na postagem do estado decrementa a função por um a contagem de bloqueio do objeto de bloqueio que é nomeado pelo `expr`.|
|`_Releases_nonreentrant_lock_(expr)`|O bloqueio que é nomeado pelo `expr` é liberado. Um erro será relatado se o bloqueio não é mantido no momento.|
|`_Releases_shared_lock_(expr)`|Anota uma função e indica que na postagem do estado decrementa a função por um a contagem de bloqueio compartilhado do objeto de bloqueio que é nomeado pelo `expr`.|
|`_Requires_lock_held_(expr)`|Anota uma função e indica que, na versão anterior, estado a contagem de bloqueio do objeto que é nomeado pelo `expr` é pelo menos um.|
|`_Requires_lock_not_held_(expr)`|Anota uma função e indica que, na versão anterior, estado a contagem de bloqueio do objeto que é nomeado pelo `expr` é zero.|
|`_Requires_no_locks_held_`|Anota uma função e indica que as contagens de bloqueio de todos os bloqueios que são conhecidos como o verificador de zero.|
|`_Requires_shared_lock_held_(expr)`|Anota uma função e indica que, na versão anterior, estado a contagem de bloqueio compartilhado do objeto que é nomeado pelo `expr` é pelo menos um.|
|`_Requires_exclusive_lock_held_(expr)`|Anota uma função e indica que, na versão anterior, estado a contagem de bloqueio exclusivo do objeto que é nomeado pelo `expr` é pelo menos um.|

## <a name="sal-intrinsics-for-unexposed-locking-objects"></a>Intrínsecos SAL para objetos de bloqueio não expostos
 Determinados objetos de bloqueio não são expostos pela implementação das funções de bloqueio associadas.  A tabela a seguir lista variáveis intrínsecas de SAL que permitem anotações em funções que operam nesses objetos de bloqueio não expostos.

|Anotação|Descrição|
|----------------|-----------------|
|`_Global_cancel_spin_lock_`|Descreve o bloqueio de rotação de cancelamento.|
|`_Global_critical_region_`|Descreve a região crítica.|
|`_Global_interlock_`|Descreve as operações interconectadas.|
|`_Global_priority_region_`|Descreve a região de prioridade.|

## <a name="shared-data-access-annotations"></a>Anotações de acesso de dados compartilhados
 A tabela a seguir lista as anotações para acesso a dados compartilhados.

|Anotação|Descrição|
|----------------|-----------------|
|`_Guarded_by_(expr)`|Anota uma variável e indica que sempre que a variável é acessada, a contagem de bloqueio do objeto de bloqueio que é nomeado pelo `expr` é pelo menos um.|
|`_Interlocked_`|Anota uma variável e é equivalente a `_Guarded_by_(_Global_interlock_)`.|
|`_Interlocked_operand_`|O parâmetro de função anotado é o operando de destino de uma das várias funções Interlocked.  Os operandos devem ter propriedades adicionais específicas.|
|`_Write_guarded_by_(expr)`|Anota uma variável e indica que sempre que a variável é modificada, a contagem de bloqueio do objeto de bloqueio que é nomeado pelo `expr` é pelo menos um.|

## <a name="smart-lock-and-raii-annotations"></a>Smart Lock e RAII anotações
 Normalmente, fechaduras inteligentes encapsulam bloqueios nativos e gerenciar seu tempo de vida. A tabela a seguir lista as anotações que podem ser usadas com fechaduras inteligentes e RAII padrões com suporte de codificação `move` semântica.

|Anotação|Descrição|
|----------------|-----------------|
|`_Analysis_assume_smart_lock_acquired_`|Informa o analisador de supor que um bloqueio inteligente foi adquirido. Essa anotação espera um tipo de bloqueio de referência como seu parâmetro.|
|`_Analysis_assume_smart_lock_released_`|Informa ao analisador de supor que um bloqueio inteligente foi liberado. Essa anotação espera um tipo de bloqueio de referência como seu parâmetro.|
|`_Moves_lock_(target, source)`|Descreve `move constructor` operação que transfere o estado do bloqueio da `source` do objeto para o `target`. O `target` é considerado um objeto construído recentemente, portanto, qualquer estado que tinha antes é perdido e substituído pelo `source` estado. O `source` é também a redefinição para um estado limpo com nenhum destino de contagens ou alias de bloqueio, mas aliases apontando para ele permanecem inalterados.|
|`_Replaces_lock_(target, source)`|Descreve `move assignment operator` semântica em que o bloqueio de destino é liberado antes de transferir o estado da origem. Isso pode ser considerado como uma combinação de `_Moves_lock_(target, source)` precedido por um `_Releases_lock_(target)`.|
|`_Swaps_locks_(left, right)`|Descreve o padrão `swap` comportamento que assume que os objetos `left` e `right` seu estado do exchange. O estado trocado inclui bloqueio contagem e o alias de destino, se estiver presente. Aliases que apontam para o `left` e `right` objetos permanecem inalterados.|
|`_Detaches_lock_(detached, lock)`|Descreve um cenário em que um tipo de wrapper de bloqueio permite desassociação com seu recurso independente. Isso é semelhante a como `std::unique_ptr` funciona com seu ponteiro interno: ele permite que os programadores extrair o ponteiro e deixar seu contêiner de ponteiro inteligente em um estado limpo. Lógica semelhante é compatível com `std::unique_lock` e pode ser implementado nos wrappers de bloqueio personalizado. O bloqueio desanexado manterá seu estado (bloqueio contagem e o alias de destino, se houver), enquanto o wrapper será redefinido para conter zero contagem de bloqueio e nenhum destino de geração de alias, enquanto retém seus próprios aliases. Não há nenhuma operação na contagem de bloqueio (liberar e adquirir). Essa anotação se comporta exatamente como `_Moves_lock_` , exceto que o argumento desanexado deve ser `return` em vez de `this`.|

## <a name="see-also"></a>Consulte também

- [Usando anotações de SAL para reduzir defeitos de código do C/C++](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)
- [Noções básicas de SAL](../code-quality/understanding-sal.md)
- [Anotando parâmetros de função e valores de retorno](../code-quality/annotating-function-parameters-and-return-values.md)
- [Anotando o comportamento da função](../code-quality/annotating-function-behavior.md)
- [Anotando estruturas e classes](../code-quality/annotating-structs-and-classes.md)
- [Especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md)
- [Funções intrínsecas](../code-quality/intrinsic-functions.md)
- [Práticas recomendadas e exemplos](../code-quality/best-practices-and-examples-sal.md)
- [Blog da equipe de análise de código](http://go.microsoft.com/fwlink/p/?LinkId=251197)