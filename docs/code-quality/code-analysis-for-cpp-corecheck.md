---
title: Referência de verificador das diretrizes principais do C++
ms.date: 03/22/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
helpviewer_keywords:
- code analysis, C++ core check
ms.assetid: f1429463-136e-41ed-8a75-a8dbf0b4fd89
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- cplusplus
ms.openlocfilehash: c11386dcd742e64737a4b06f2db9f55145f535d7
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53053380"
---
# <a name="c-core-guidelines-checker-reference"></a>Referência de verificador das diretrizes principais do C++

Esta seção lista avisos de verificação de diretrizes de principal do C++. Para obter informações sobre análise de código, consulte [/Analyze (análise de código)](/cpp/build/reference/analyze-code-analysis) e [início rápido: análise de código para C/C++](../code-quality/quick-start-code-analysis-for-c-cpp.md).

> [!NOTE]
> Alguns avisos pertencem a mais de um grupo, e nem todos os avisos têm um tópico de referência completa.

## <a name="ownerpointer-group"></a>Grupo OWNER_POINTER

[C26402 DONT_HEAP_ALLOCATE_MOVABLE_RESULT](C26402.md) retornar um objeto com escopo em vez de um heap alocado se ele tiver um construtor de movimentação. Ver [diretrizes principais do C++ R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr).

[C26403 RESET_OR_DELETE_OWNER](C26403.md) redefinir ou excluir explicitamente um proprietário\<T > ponteiro '% variable %'. Ver [diretrizes principais do C++ R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr).

[C26404 DONT_DELETE_INVALID](C26404.md) não exclua nenhum proprietário\<T > que possa estar em estado inválido. Ver [diretrizes principais do C++ R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr).

[C26405 DONT_ASSIGN_TO_VALID](C26405.md) não atribuir a um proprietário\<T > que possa estar em estado válido. Ver [diretrizes principais do C++ R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr).

[C26406 DONT_ASSIGN_RAW_TO_OWNER](C26406.md) não atribuir um ponteiro bruto a proprietário\<T >. Ver [diretrizes principais do C++ R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr).

[C26407 DONT_HEAP_ALLOCATE_UNNECESSARILY](C26407.md) prefira objetos com escopo, não aloque heap desnecessariamente. Ver [diretrizes principais do C++ R.5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped).

[C26429 USE_NOTNULL](C26429.md) símbolo '% % do símbolo' nunca é testado para nullness, ele pode ser marcado como not_null. Ver [diretrizes principais do C++ F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value).

[C26430 TEST_ON_ALL_PATHS](C26430.md) o símbolo '% % do símbolo' não é testado para nullness em todos os caminhos. Ver [diretrizes principais do C++ F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value).

[C26431 DONT_TEST_NOTNULL](C26431.md) o tipo da expressão '% expr % s' já está gsl:: Not_Null. Não teste-o para nullness. Ver [diretrizes principais do C++ F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value).

## <a name="rawpointer-group"></a>RAW_POINTER Group

[C26400 NO_RAW_POINTER_ASSIGNMENT](c26400.md) não atribua o resultado de uma alocação ou uma chamada de função com um proprietário\<T > retornam o valor a um ponteiro bruto; use proprietário\<T > em vez disso. Ver [diretrizes principais do C++ I.11](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Ri-raw).

[C26401 DONT_DELETE_NON_OWNER](c26401.md) não exclua um ponteiro bruto que não é um proprietário\<T >. Ver [diretrizes principais do C++ I.11](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Ri-raw).

[C26402 DONT_HEAP_ALLOCATE_MOVABLE_RESULT](C26402.md)   retornar um objeto com escopo em vez de um heap alocado se ele tiver um construtor de movimentação. Ver [diretrizes principais do C++ R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr).

[C26408 NO_MALLOC_FREE](C26408.md) Evite malloc () e Free (), prefira a versão nothrow de new com delete. Ver [diretrizes principais do C++ R.10](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-mallocfree).

[C26409 NO_NEW_DELETE](C26409.md) evitar chamar new e delete explicitamente, use std:: make_unique\<T > em vez disso. Ver [diretrizes principais do C++ R.11](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-newdelete).

[C26429 USE_NOTNULL](C26429.md) símbolo '% % do símbolo' nunca é testado para nullness, ele pode ser marcado como not_null. Ver [diretrizes principais do C++ F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value).

[C26430 TEST_ON_ALL_PATHS](C26430.md) o símbolo '% % do símbolo' não é testado para nullness em todos os caminhos. Ver [diretrizes principais do C++ F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value).

[C26431 DONT_TEST_NOTNULL](C26431.md) o tipo da expressão '% expr % s' já está gsl:: Not_Null. Não teste-o para nullness. Ver [diretrizes principais do C++ F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value).

[C26481 NO_POINTER_ARITHMETIC](C26481.md) não use aritmética de ponteiro. Use o span. Ver [Bounds.1 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds).

[C26485 NO_ARRAY_TO_POINTER_DECAY](C26485.md).
A expressão '% expr %': Nenhuma matriz para ponteiro de decaimento. Ver [Bounds.3 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds).

## <a name="uniquepointer-group"></a>UNIQUE_POINTER Group

[C26410 NO_REF_TO_CONST_UNIQUE_PTR](C26410.md) o parâmetro '% parâmetro %' é uma referência ao `const` ponteiro exclusivo, use const T * ou const T & em vez disso. Ver [diretrizes principais do C++ R.32](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-uniqueptrparam).

[C26411 NO_REF_TO_UNIQUE_PTR](C26411.md) o parâmetro '% parâmetro %' é uma referência ao ponteiro exclusivo e nunca é reatribuído nem redefinido, use T * ou T & em vez disso. Ver [diretrizes principais do C++ R.33](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-reseat).

[C26414 RESET_LOCAL_SMART_PTR](C26414.md) mover, copiar, reatribua ou redefina um ponteiro inteligente local '% % do símbolo'. Ver [diretrizes principais do C++ R.5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped).

[C26415 SMART_PTR_NOT_NEEDED](C26415.md) '% % do símbolo' do parâmetro de ponteiro inteligente é usado somente para acessar o ponteiro independente. Use T * ou T & em vez disso. Ver [diretrizes principais do C++ R.30](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-smartptrparam).

## <a name="sharedpointer-group"></a>SHARED_POINTER Group

[C26414 RESET_LOCAL_SMART_PTR](C26414.md) mover, copiar, reatribua ou redefina um ponteiro inteligente local '% % do símbolo'. Ver [diretrizes principais do C++ R.5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped).

[C26415 SMART_PTR_NOT_NEEDED](C26415.md) '% % do símbolo' do parâmetro de ponteiro inteligente é usado somente para acessar o ponteiro independente. Use T * ou T & em vez disso. Ver [diretrizes principais do C++ R.30](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-smartptrparam).

[C26416 NO_RVALUE_REF_SHARED_PTR](C26416.md) parâmetro de ponteiro compartilhado '% % do símbolo' é passado por referência de rvalue. Passe por valor. Ver [diretrizes principais do C++ R.34](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam-owner).

[C26417 NO_LVALUE_REF_SHARED_PTR](C26417.md) parâmetro de ponteiro compartilhado '% % do símbolo' é passado por referência e não redefinido ou reatribuído. Use T * ou T & em vez disso. Ver [diretrizes principais do C++ R.35](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam).

[C26418 NO_VALUE_OR_CONST_REF_SHARED_PTR](C26418.md) parâmetro de ponteiro compartilhado '% Símbolo %' não é copiado ou movido. Use T * ou T & em vez disso. Ver [diretrizes principais do C++ R.36](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam-const).

## <a name="declaration-group"></a>DECLARAÇÃO de grupo

[C26426 NO_GLOBAL_INIT_CALLS](C26426.md) inicializador Global chama uma função não constexpr '% Símbolo %'. Ver [diretrizes principais do C++ I.22](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#i22-avoid-complex-initialization-of-global-objects).

[C26427 NO_GLOBAL_INIT_EXTERNS](C26427.md) inicializador Global acessa um objeto externo '% Símbolo %'. Ver [diretrizes principais do C++ I.22](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#i22-avoid-complex-initialization-of-global-objects).

[C26444 NO_UNNAMED_RAII_OBJECTS](c26444.md) Evite sem nome objetos com construção e destruição personalizadas. Ver [ES.84: não (tente) declare uma variável local sem nome](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md).

## <a name="class-group"></a>Grupo de classe

[C26432 DEFINE_OR_DELETE_SPECIAL_OPS](C26432.md) se você definir ou excluir qualquer operação padrão no tipo '% % do símbolo', definir ou excluir todos eles. Ver [diretrizes principais do C++ 21](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c21-if-you-define-or-delete-any-default-operation-define-or-delete-them-all).

[C26433 OVERRIDE_EXPLICITLY](c26433.md) função '% % do símbolo' deve ser marcada com "override". Ver [C.128: funções virtuais devem especificar exatamente um dos virtual, substituição, ou final](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c128-virtual-functions-should-specify-exactly-one-of-virtual-override-or-final).

[C26434 DONT_HIDE_METHODS](C26434.md) função '% symbol_1% ' oculta uma função não virtual '% symbol_2% '. Ver [diretrizes principais do C++ C.128](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c128-virtual-functions-should-specify-exactly-one-of-virtual-override-or-final).

[C26435 SINGLE_VIRTUAL_SPECIFICATION](c26435.md) a função '% % do símbolo' deve especificar exatamente um dos 'virtual', 'override' ou 'final'. Ver [C.128: funções virtuais devem especificar exatamente um dos virtual, substituição, ou final](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md).


[C26436 NEED_VIRTUAL_DTOR](C26436.md) o tipo '% % do símbolo' com uma função virtual precisa de qualquer um dos destruidor não virtual protegido ou virtual público. Ver [diretrizes principais do C++ C.35](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c35-a-base-class-destructor-should-be-either-public-and-virtual-or-protected-and-nonvirtual).


[C26443 NO_EXPLICIT_DTOR_OVERRIDE](c26443.md) substituindo destruidor não deve usar especificadores 'virtuais' ou 'override' explícita. Ver [C.128: funções virtuais devem especificar exatamente um dos virtual, substituição, ou final](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md).


## <a name="type-group"></a>TIPO de grupo

[C26437 DONT_SLICE](C26437.md) não dividir. Ver [diretrizes principais do C++ ES.63](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es63-dont-slice).

## <a name="style-group"></a>Grupo de estilo

[C26438 NO_GOTO](C26438.md) evitar `goto`. Ver [diretrizes principais do C++ ES.76](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es76-avoid-goto).

## <a name="function-group"></a>Grupo de funções

[C26439 SPECIAL_NOEXCEPT](C26439.md) esse tipo de função não pode gerar. Declare- `noexcept`. Ver [diretrizes principais do C++ F.6](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept).

[C26440 DECLARE_NOEXCEPT](C26440.md) a função '% % do símbolo' pode ser declarada `noexcept`. Ver [diretrizes principais do C++ F.6](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept).

[C26447 DONT_THROW_IN_NOEXCEPT](c26447.md) a função é declarada **noexcept** , mas chama uma função que pode gerar exceções.
Ver [diretrizes principais do C++: F.6: se sua função pode lançar, declarar noexcept](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept).

## <a name="concurrency-group"></a>Grupo de SIMULTANEIDADE

[C26441 NO_UNNAMED_GUARDS](C26441.md) objetos de proteção devem ser nomeados. Ver [cp.44 de diretrizes de núcleo do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#cp44-remember-to-name-your-lock_guards-and-unique_locks).

## <a name="const-group"></a>Grupo de CONST

[C26460 USE_CONST_REFERENCE_ARGUMENTS](c26460.md) o argumento de referência '% % do argumento' para a função '% % de função' pode ser marcado como `const`. Ver [con.3 de diretrizes de núcleo do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-ref).

[C26461 USE_CONST_POINTER_ARGUMENTS](c26461.md): O argumento de ponteiro '% % do argumento' para a função '% % de função' pode ser marcado como um ponteiro para `const`. Ver [con.3 de diretrizes de núcleo do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-ref).

[C26462 USE_CONST_POINTER_FOR_VARIABLE](c26462.md) o valor apontado por '% variable %' é atribuído somente uma vez, marcá-la como um ponteiro para `const`. Ver [con.4 de diretrizes de núcleo do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction).

[C26463 USE_CONST_FOR_ELEMENTS](c26463.md) elementos da matriz '% % de matriz' são atribuídos somente uma vez, marque-os `const`. Ver [con.4 de diretrizes de núcleo do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction).

[C26464 USE_CONST_POINTER_FOR_ELEMENTS](c26464.md) os valores apontados por elementos de matriz '% % de matriz' são atribuídos somente uma vez, marque-os como ponteiro para `const`. Ver [con.4 de diretrizes de núcleo do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction).

[C26496 USE_CONST_FOR_VARIABLE](c26496.md) a variável '% variable %' é atribuída somente uma vez, marque-a como `const`. Ver [con.4 de diretrizes de núcleo do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction).

[C26497 USE_CONSTEXPR_FOR_FUNCTION](c26497.md) poderá ser marcada como essa função a função % % `constexpr` se a avaliação do tempo de compilação for desejada. Ver [diretrizes principais do C++ F.4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rf-constexpr).

[C26498 USE_CONSTEXPR_FOR_FUNCTIONCALL](c26498.md) essa chamada de função % % de função pode usar `constexpr` se a avaliação do tempo de compilação for desejada. Ver [con.5 de diretrizes de núcleo do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-constexpr).

## <a name="type-group"></a>TIPO de grupo

[C26465 NO_CONST_CAST_UNNECESSARY](c26465.md) não use `const_cast` para eliminar `const`. `const_cast` não é necessário; constness ou volatility não está sendo removido por essa conversão. Ver [Type.3 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-constcast).

[C26466 NO_STATIC_DOWNCAST_POLYMORPHIC](c26466.md) não use `static_cast` downcasts. Uma conversão de um tipo polimórfico deve usar dynamic_cast. Ver [Type.2 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-downcast).

[C26471 NO_REINTERPRET_CAST_FROM_VOID_PTR](c26471.md) Don't use `reinterpret_cast`. Uma conversão de void * pode usar `static_cast`. Ver [Type.1 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast).

[C26472 NO_CASTS_FOR_ARITHMETIC_CONVERSION](C26472.md) não use um `static_cast` para conversões aritméticas. Use a inicialização da chave, gsl:: narrow_cast ou gsl:: narow. Ver [Type.1 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast).

[C26473 NO_IDENTITY_CAST](C26473.md) não converta os tipos de ponteiro em que o tipo de origem e o tipo de destino são os mesmos. Ver [Type.1 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast).

[C26474 NO_IMPLICIT_CAST](C26474.md) não converta os tipos ponteiro quando a conversão puder ser implícita. Ver [Type.1 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast).

[C26475 NO_FUNCTION_STYLE_CASTS](C26475.md) não use conversões C do estilo de função. Ver [diretrizes principais do C++ ES.49](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es49-if-you-must-use-a-cast-use-a-named-cast).

[C26490 NO_REINTERPRET_CAST](c26490.md) não use `reinterpret_cast`. Ver [Type.1 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type).

[C26491 NO_STATIC_DOWNCAST](c26490.md) não use `static_cast` downcasts. Ver [Type.2 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type).

[C26492 NO_CONST_CAST](c26492.md) não use `const_cast` para eliminar `const`. Ver [Type.3 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type).

[C26493 NO_CSTYLE_CAST](c26493.md) não use conversões C-style. Ver [Type.4 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type).

[C26494 VAR_USE_BEFORE_INIT](c26494.md) variável '% variable %' não foi inicializada. Sempre inicialize um objeto. Ver [Type.5 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type).

[C26495 MEMBER_UNINIT](c26495.md) variável '% variable %' não foi inicializada. Sempre inicialize uma variável de membro. Ver [Type.6 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type).

## <a name="bounds-group"></a>Grupo de limites

[C26446 USE_GSL_AT](c26446.md) preferir usar `gsl::at()` em vez do operador subscrito desmarcado. Ver [diretrizes principais do C++: Bounds.4: não use funções de biblioteca padrão e tipos que não são limites verificados](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#probounds-bounds-safety-profile).

[C26481 NO_POINTER_ARITHMETIC](C26481.md).
Não use aritmética de ponteiro. Use o span. Consulte [Bounds.1 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26482 NO_DYNAMIC_ARRAY_INDEXING](c26482.md) somente indexe em matrizes que usam expressões constantes. Consulte [Bounds.2 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26483 STATIC_INDEX_OUT_OF_RANGE](c26483.md) valor % value % está fora dos limites (0, % acoplado %) da variável '% variable %'. Somente indexe em matrizes que usam expressões de constante que estão dentro dos limites da matriz. Consulte [Bounds.2 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26485 NO_ARRAY_TO_POINTER_DECAY](C26485.md) expressão '% expr %': Nenhuma matriz para ponteiro de decaimento. Consulte [Bounds.3 de diretrizes principais do C++](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

## <a name="gsl-group"></a>Grupo de GSL

[C26445 NO_SPAN_REF](c26445.md) uma referência ao `gsl::span` ou `std::string_view` pode ser uma indicação de um problema de tempo de vida.
Consulte [gsl de diretrizes principais do C++: modos de exibição](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#gslview-views)

[C26446 USE_GSL_AT](c26446.md) preferir usar `gsl::at()` em vez do operador subscrito desmarcado. Ver [diretrizes principais do C++: Bounds.4: não use funções de biblioteca padrão e tipos que não são limites verificados](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#probounds-bounds-safety-profile).

[C26448 USE_GSL_FINALLY ](c26448.md) considere o uso de `gsl::finally` se destina-se a ação final. Ver [diretrizes principais do C++: GSL.util: utilitários](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-utilities).

[C26449 NO_SPAN_FROM_TEMPORARY](c26449.md) 
 `gsl::span` ou `std::string_view` criado a partir de um temporário será inválido quando o temporário for invalidado. Ver [diretrizes principais do C++: gsl: modos de exibição](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#gslview-views).


## <a name="deprecated-warnings"></a>Avisos preteridos

Os avisos a seguir estão presentes em um conjunto de regra experimental antecipada do verificador de diretrizes de núcleo, mas agora são preteridos e podem ser ignorados com segurança. Os avisos são substituídos pelos avisos na lista acima.

- 26412 DEREF_INVALID_POINTER
- 26413 DEREF_NULLPTR
- 26420 ASSIGN_NONOWNER_TO_EXPLICIT_OWNER
- 26421 ASSIGN_VALID_OWNER
- 26422 VALID_OWNER_LEAVING_SCOPE
- 26423 ALLOCATION_NOT_ASSIGNED_TO_OWNER
- 26424 VALID_ALLOCATION_LEAVING_SCOPE
- 26425 ASSIGNING_TO_STATIC
- 26499 NO_LIFETIME_TRACKING

## <a name="see-also"></a>Consulte também
[Usando os verificadores de diretrizes principais do C++](using-the-cpp-core-guidelines-checkers.md)
