---
title: Anotando parâmetros de função e valores de retorno
ms.date: 10/15/2019
ms.topic: conceptual
f1_keywords:
- _Outptr_opt_result_bytebuffer_to_
- _Inout_updates_all_opt_
- _Post_equal_to_
- _Outptr_opt_result_maybenull_
- _Out_writes_bytes_all_
- _Out_writes_all_opt_
- _In_opt_
- _Outptr_
- _Outptr_result_maybenull_
- _Outref_result_bytebuffer_all_maybenull_
- _Inout_updates_opt_z_
- _Inout_updates_z_
- _Out_writes_
- _Out_writes_to_ptr_opt_z_
- _In_reads_to_ptr_opt_
- _Ret_writes_to_maybenull_
- _Outref_result_maybenull_
- _Ret_writes_bytes_
- _Outptr_result_bytebuffer_
- _Out_writes_opt_
- _Inout_updates_bytes_opt_
- _In_z_
- _Inout_updates_to_
- _Ret_maybenull_
- _Ret_writes_bytes_to_
- _Ret_z_
- _COM_Outptr_
- _Ret_maybenull_z_
- _Out_opt_
- _In_reads_opt_z_
- _Outptr_result_bytebuffer_to_
- _Ret_notnull_
- _COM_Outptr_opt_result_maybenull_
- _Inout_updates_to_opt_
- _Inout_updates_
- _Outptr_opt_result_buffer_
- _Outptr_result_buffer_to_
- _Out_writes_to_ptr_opt_
- _Out_writes_bytes_all_opt_
- _Inout_updates_all_
- _Deref_inout_range_
- _Ret_writes_
- _Out_writes_z_
- _Ret_writes_to_
- _Out_writes_to_ptr_z_
- _Out_writes_bytes_to_opt_
- _In_reads_or_z_
- _Inout_updates_bytes_to_
- _In_reads_z_
- _In_opt_z_
- _Outref_result_buffer_maybenull_
- _Ret_range_
- _COM_Outptr_opt_
- _Ouptr_opt_result_maybenull_z_
- _In_reads_opt_
- _Inout_
- _Field_range_
- _Ret_writes_z_
- _Out_writes_to_
- _Out_writes_to_ptr_
- _Inout_opt_z_
- _Outref_
- _Deref_out_range_
- _Outref_result_buffer_
- _Outref_result_buffer_to_
- _Outref_result_bytebuffer_to_maybenull_
- _In_reads_bytes_
- _Outptr_opt_result_buffer_to_
- _Outref_result_buffer_all_
- _Out_writes_bytes_to_
- _Result_zeroonfailure_
- _In_reads_bytes_opt_
- _Outref_result_buffer_to_maybenull_
- _Outref_result_bytebuffer_all_
- _Outref_result_buffer_all_maybenull_
- _Ret_writes_maybenull_z_
- _In_range_
- _Inout_updates_bytes_all_opt_
- _Outref_result_bytebuffer_to_
- _Inout_updates_bytes_to_opt_
- _Pre_equal_to_
- _Ret_writes_bytes_maybenull_
- _COM_Outptr_result_maybenull_
- _Ret_writes_maybenull_
- _Out_writes_bytes_
- _Outptr_opt_
- _Out_writes_opt_z_
- _Outref_result_nullonfailure_
- _Outptr_opt_result_z_
- _Inout_opt_
- _Deref_in_range_
- _Outptr_result_z_
- _In_reads_to_ptr_opt_z_
- _Struct_size_bytes_
- _Outptr_result_nullonfailure_
- _In_
- _Inout_updates_bytes_
- _In_reads_to_ptr_z_
- _Ret_writes_bytes_to_maybenull
- _Outptr_opt_result_nullonfailure_
- _In_reads_to_ptr_
- _Outptr_result_buffer_
- _Out_
- _Outref_result_bytebuffer_maybenull_
- _Outptr_result_maybenull_z_
- _In_reads_
- _Inout_updates_opt_
- _Out_writes_to_opt_
- _Outptr_opt_result_bytebuffer_
- _Out_writes_all_
- _Out_range_
- _Inout_updates_bytes_all_
- _Inout_z_
- _Outref_result_bytebuffer_
- _Result_nullonfailure_
- _Ret_null_
- _Scanf_format_string_
- _Scanf_s_format_string_
- _Printf_format_string_
ms.assetid: 82826a3d-0c81-421c-8ffe-4072555dca3a
author: mikeblome
ms.author: mblome
manager: markl
ms.workload:
- multiple
ms.openlocfilehash: 8437a18bf2b732ee3f12774b04baedf12003d554
ms.sourcegitcommit: 8589d85cc10710ef87e6363a2effa5ee5610d46a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72806799"
---
# <a name="annotating-function-parameters-and-return-values"></a>Anotando parâmetros de função e valores de retorno
Este artigo descreve usos típicos de anotações para parâmetros de função simples – escalares e ponteiros para estruturas e classes – e a maioria dos tipos de buffers.  Este artigo também mostra padrões de uso comuns para anotações. Para anotações adicionais relacionadas a funções, consulte [anotando o comportamento da função](../code-quality/annotating-function-behavior.md).

## <a name="pointer-parameters"></a>Parâmetros do ponteiro
Para as anotações na tabela a seguir, quando um parâmetro de ponteiro está sendo anotado, o analisador relatará um erro se o ponteiro for nulo.  Isso se aplica a ponteiros e a qualquer item de dados apontado.

**Anotações e descrições**

- `_In_`

     Anota os parâmetros de entrada que são escalares, estruturas, ponteiros para estruturas e similares.  Pode ser usado explicitamente em escalares simples.  O parâmetro deve ser válido em pré-estado e não será modificado.

- `_Out_`

     Anota os parâmetros de saída que são escalares, estruturas, ponteiros para estruturas e similares.  Não aplique isso a um objeto que não pode retornar um valor — por exemplo, um escalar que é passado por valor.  O parâmetro não precisa ser válido em pré-estado, mas deve ser válido no pós-Estado.

- `_Inout_`

     Anota um parâmetro que será alterado pela função.  Ele deve ser válido tanto para pré-estado quanto após o estado, mas é presumido ter valores diferentes antes e depois da chamada. Deve se aplicar a um valor modificável.

- `_In_z_`

     Um ponteiro para uma cadeia de caracteres terminada em nulo que é usada como entrada.  A cadeia de caracteres deve ser válida em pré-estado.  Variantes de `PSTR`, que já têm as anotações corretas, são preferenciais.

- `_Inout_z_`

     Um ponteiro para uma matriz de caracteres terminada em nulo que será modificada.  Ele deve ser válido antes e depois da chamada, mas o valor é considerado como alterado.  O terminador NULL pode ser movido, mas somente os elementos até o terminador NULL original podem ser acessados.

- `_In_reads_(s)`

     `_In_reads_bytes_(s)`

     Um ponteiro para uma matriz, que é lido pela função.  A matriz é do tamanho `s`, e todas devem ser válidas.

     A variante de `_bytes_` fornece o tamanho em bytes em vez de elementos. Use-o somente quando o tamanho não puder ser expresso como elementos.  Por exemplo, `char` cadeias de caracteres usarão a variante de `_bytes_` somente se uma função semelhante que usa `wchar_t`.

- `_In_reads_z_(s)`

     Um ponteiro para uma matriz terminada em nulo e tem um tamanho conhecido. Os elementos até o terminador nulo — ou `s` se não houver um terminador nulo — devem ser válidos em pré-estado.  Se o tamanho for conhecido em bytes, dimensione `s` pelo tamanho do elemento.

- `_In_reads_or_z_(s)`

     Um ponteiro para uma matriz terminada em nulo ou tem um tamanho conhecido, ou ambos. Os elementos até o terminador nulo — ou `s` se não houver um terminador nulo — devem ser válidos em pré-estado.  Se o tamanho for conhecido em bytes, dimensione `s` pelo tamanho do elemento.  (Usado para a família `strn`.)

- `_Out_writes_(s)`

     `_Out_writes_bytes_(s)`

     Um ponteiro para uma matriz de elementos `s` (resp. bytes) que será gravado pela função.  Os elementos da matriz não precisam ser válidos em pré-estado e o número de elementos que são válidos no pós-Estado não é especificado.  Se houver anotações no tipo de parâmetro, elas serão aplicadas em pós-Estado. Por exemplo, considere o código a seguir.

     `typedef _Null_terminated_ wchar_t *PWSTR; void MyStringCopy(_Out_writes_ (size) PWSTR p1,    _In_ size_t size,    _In_ PWSTR p2);`

     Neste exemplo, o chamador fornece um buffer de elementos `size` para `p1`.  `MyStringCopy` torna alguns desses elementos válidos. O mais importante é que a anotação `_Null_terminated_` em `PWSTR` significa que `p1` é terminada em nulo no post-State.  Dessa forma, o número de elementos válidos ainda é bem definido, mas uma contagem de elementos específica não é necessária.

     A variante de `_bytes_` fornece o tamanho em bytes em vez de elementos. Use-o somente quando o tamanho não puder ser expresso como elementos.  Por exemplo, `char` cadeias de caracteres usarão a variante de `_bytes_` somente se uma função semelhante que usa `wchar_t`.

- `_Out_writes_z_(s)`

     Um ponteiro para uma matriz de elementos `s`.  Os elementos não precisam ser válidos em pré-estado.  No pós-Estado, os elementos acima do terminador nulo — que devem estar presentes — devem ser válidos.  Se o tamanho for conhecido em bytes, dimensione `s` pelo tamanho do elemento.

- `_Inout_updates_(s)`

     `_Inout_updates_bytes_(s)`

     Um ponteiro para uma matriz, que é lido e gravado na função.  É do tamanho `s`, e é válido em pré e após o estado.

     A variante de `_bytes_` fornece o tamanho em bytes em vez de elementos. Use-o somente quando o tamanho não puder ser expresso como elementos.  Por exemplo, `char` cadeias de caracteres usarão a variante de `_bytes_` somente se uma função semelhante que usa `wchar_t`.

- `_Inout_updates_z_(s)`

     Um ponteiro para uma matriz terminada em nulo e tem um tamanho conhecido. Os elementos acima do terminador nulo — que devem estar presentes — devem ser válidos em pré e após o estado.  O valor no pós-Estado é presumido que seja diferente do valor no pré-estado; Isso inclui o local do terminador nulo. Se o tamanho for conhecido em bytes, dimensione `s` pelo tamanho do elemento.

- `_Out_writes_to_(s,c)`

     `_Out_writes_bytes_to_(s,c)`

     `_Out_writes_all_(s)`

     `_Out_writes_bytes_all_(s)`

     Um ponteiro para uma matriz de elementos `s`.  Os elementos não precisam ser válidos em pré-estado.  No pós-Estado, os elementos até o elemento `c`-ésimo devem ser válidos.  Se o tamanho for conhecido em bytes, dimensione `s` e `c` pelo tamanho do elemento ou use a variante `_bytes_`, que é definida como:

     `_Out_writes_to_(_Old_(s), _Old_(s))    _Out_writes_bytes_to_(_Old_(s), _Old_(s))`

     Em outras palavras, todos os elementos que existem no buffer até `s` no pré-estado são válidos no pós-Estado.  Por exemplo:

     `void *memcpy(_Out_writes_bytes_all_(s) char *p1,    _In_reads_bytes_(s) char *p2,    _In_ int s); void * wordcpy(_Out_writes_all_(s) DWORD *p1,     _In_reads_(s) DWORD *p2,    _In_ int s);`

- `_Inout_updates_to_(s,c)`

     `_Inout_updates_bytes_to_(s,c)`

     Um ponteiro para uma matriz, que é lido e gravado pela função.  É de tamanho `s` elementos, que devem ser válidos em pré-estado e `c` elementos devem ser válidos no pós-Estado.

     A variante de `_bytes_` fornece o tamanho em bytes em vez de elementos. Use-o somente quando o tamanho não puder ser expresso como elementos.  Por exemplo, `char` cadeias de caracteres usarão a variante de `_bytes_` somente se uma função semelhante que usa `wchar_t`.

- `_Inout_updates_all_(s)`

     `_Inout_updates_bytes_all_(s)`

     Um ponteiro para uma matriz, que é lido e gravado pela função do tamanho `s` elementos. Definido como equivalente a:

     `_Inout_updates_to_(_Old_(s), _Old_(s))    _Inout_updates_bytes_to_(_Old_(s), _Old_(s))`

     Em outras palavras, cada elemento que existe no buffer até `s` no pré-estado é válido no pré-estado e no pós-Estado.

     A variante de `_bytes_` fornece o tamanho em bytes em vez de elementos. Use-o somente quando o tamanho não puder ser expresso como elementos.  Por exemplo, `char` cadeias de caracteres usarão a variante de `_bytes_` somente se uma função semelhante que usa `wchar_t`.

- `_In_reads_to_ptr_(p)`

     Um ponteiro para uma matriz para a qual a expressão `p` - `_Curr_` (ou seja, `p` menos `_Curr_`) é definido pelo padrão de idioma apropriado.  Os elementos anteriores à `p` devem ser válidos em pré-estado.

- `_In_reads_to_ptr_z_(p)`

     Um ponteiro para uma matriz terminada em nulo para o qual a expressão `p` - `_Curr_` (ou seja, `p` menos `_Curr_`) é definido pelo padrão de idioma apropriado.  Os elementos anteriores à `p` devem ser válidos em pré-estado.

- `_Out_writes_to_ptr_(p)`

     Um ponteiro para uma matriz para a qual a expressão `p` - `_Curr_` (ou seja, `p` menos `_Curr_`) é definido pelo padrão de idioma apropriado.  Os elementos anteriores à `p` não precisam ser válidos em pré-estado e devem ser válidos no pós-Estado.

- `_Out_writes_to_ptr_z_(p)`

     Um ponteiro para uma matriz terminada em nulo para o qual a expressão `p` - `_Curr_` (ou seja, `p` menos `_Curr_`) é definido pelo padrão de idioma apropriado.  Os elementos anteriores à `p` não precisam ser válidos em pré-estado e devem ser válidos no pós-Estado.

## <a name="optional-pointer-parameters"></a>Parâmetros de ponteiro opcionais

Quando uma anotação de parâmetro de ponteiro inclui `_opt_`, ela indica que o parâmetro pode ser nulo. Caso contrário, a anotação será executada da mesma forma que a versão que não inclui `_opt_`. Aqui está uma lista das variantes de `_opt_` das anotações de parâmetro de ponteiro:

||||
|-|-|-|
|`_In_opt_`<br /><br /> `_Out_opt_`<br /><br /> `_Inout_opt_`<br /><br /> `_In_opt_z_`<br /><br /> `_Inout_opt_z_`<br /><br /> `_In_reads_opt_`<br /><br /> `_In_reads_bytes_opt_`<br /><br /> `_In_reads_opt_z_`|`_Out_writes_opt_`<br /><br /> `_Out_writes_opt_z_`<br /><br /> `_Inout_updates_opt_`<br /><br /> `_Inout_updates_bytes_opt_`<br /><br /> `_Inout_updates_opt_z_`<br /><br /> `_Out_writes_to_opt_`<br /><br /> `_Out_writes_bytes_to_opt_`<br /><br /> `_Out_writes_all_opt_`<br /><br /> `_Out_writes_bytes_all_opt_`|`_Inout_updates_to_opt_`<br /><br /> `_Inout_updates_bytes_to_opt_`<br /><br /> `_Inout_updates_all_opt_`<br /><br /> `_Inout_updates_bytes_all_opt_`<br /><br /> `_In_reads_to_ptr_opt_`<br /><br /> `_In_reads_to_ptr_opt_z_`<br /><br /> `_Out_writes_to_ptr_opt_`<br /><br /> `_Out_writes_to_ptr_opt_z_`|

## <a name="output-pointer-parameters"></a>Parâmetros de ponteiro de saída
Os parâmetros de ponteiro de saída exigem notação especial para desambiguar NULL-qualidade no parâmetro e no local apontado.

**Anotações e descrições**

- `_Outptr_`

   O parâmetro não pode ser nulo e, no estado de postagem, o local apontado não pode ser nulo e deve ser válido.

- `_Outptr_opt_`

   O parâmetro pode ser nulo, mas, no estado de postagem, o local apontado não pode ser nulo e deve ser válido.

- `_Outptr_result_maybenull_`

   O parâmetro não pode ser nulo e, no estado de postagem, o local apontado pode ser nulo.

- `_Outptr_opt_result_maybenull_`

   O parâmetro pode ser nulo e, no estado de postagem, o local apontado pode ser nulo.

  Na tabela a seguir, subcadeias de caracteres adicionais são inseridas no nome da anotação para qualificar ainda mais o significado da anotação.  As várias subcadeias de caracteres são `_z`, `_COM_`, `_buffer_`, `_bytebuffer_`e `_to_`.

> [!IMPORTANT]
> Se a interface que você está anotando for COM, use a forma COM dessas anotações. Não use as anotações com com qualquer outra interface de tipo.

**Anotações e descrições**

- `_Outptr_result_z_`

   `_Outptr_opt_result_z_`

   `_Outptr_result_maybenull_z_`

   `_Ouptr_opt_result_maybenull_z_`

   O ponteiro retornado tem a anotação `_Null_terminated_`.

- `_COM_Outptr_`

   `_COM_Outptr_opt_`

   `_COM_Outptr_result_maybenull_`

   `_COM_Outptr_opt_result_maybenull_`

   O ponteiro retornado tem semântica COM e, portanto, transporta um `_On_failure_` pós-condição que o ponteiro retornado é nulo.

- `_Outptr_result_buffer_(s)`

   `_Outptr_result_bytebuffer_(s)`

   `_Outptr_opt_result_buffer_(s)`

   `_Outptr_opt_result_bytebuffer_(s)`

   O ponteiro retornado aponta para um buffer válido de tamanho `s` elementos ou bytes.

- `_Outptr_result_buffer_to_(s, c)`

   `_Outptr_result_bytebuffer_to_(s, c)`

   `_Outptr_opt_result_buffer_to_(s,c)`

   `_Outptr_opt_result_bytebuffer_to_(s,c)`

   O ponteiro retornado aponta para um buffer de tamanho `s` elementos ou bytes, dos quais o primeiro `c` é válido.

  Certas convenções de interface presumem que os parâmetros de saída sejam nullified em caso de falha.  Exceto pelo código COM explicitamente, os formulários na tabela a seguir são preferenciais.  Para o código COM, use os formulários COM correspondentes listados na seção anterior.

  **Anotações e descrições**

- `_Result_nullonfailure_`

   Modifica outras anotações. O resultado será definido como NULL se a função falhar.

- `_Result_zeroonfailure_`

   Modifica outras anotações. O resultado será definido como zero se a função falhar.

- `_Outptr_result_nullonfailure_`

   O ponteiro retornado aponta para um buffer válido se a função for bem-sucedida, ou NULL se a função falhar. Esta anotação é para um parâmetro não opcional.

- `_Outptr_opt_result_nullonfailure_`

   O ponteiro retornado aponta para um buffer válido se a função for bem-sucedida, ou NULL se a função falhar. Esta anotação é para um parâmetro opcional.

- `_Outref_result_nullonfailure_`

   O ponteiro retornado aponta para um buffer válido se a função for bem-sucedida, ou NULL se a função falhar. Esta anotação é para um parâmetro de referência.

## <a name="output-reference-parameters"></a>Parâmetros de referência de saída

Um uso comum do parâmetro de referência é para parâmetros de saída.  Para parâmetros de referência de saída simples — por exemplo, `int&`—`_Out_` fornece a semântica correta.  No entanto, quando o valor de saída é um ponteiro — por exemplo `int *&`— as anotações de ponteiro equivalentes, como `_Outptr_ int **` não fornecem a semântica correta.  Para expressar de forma concisa a semântica dos parâmetros de referência de saída para tipos de ponteiro, use estas anotações compostas:

**Anotações e descrições**

- `_Outref_`

     O resultado deve ser válido em pós-Estado e não pode ser nulo.

- `_Outref_result_maybenull_`

     O resultado deve ser válido em pós-Estado, mas pode ser nulo no pós-Estado.

- `_Outref_result_buffer_(s)`

     O resultado deve ser válido em pós-Estado e não pode ser nulo. Aponta para um buffer válido de tamanho `s` elementos.

- `_Outref_result_bytebuffer_(s)`

     O resultado deve ser válido em pós-Estado e não pode ser nulo. Aponta para um buffer válido de tamanho `s` bytes.

- `_Outref_result_buffer_to_(s, c)`

     O resultado deve ser válido em pós-Estado e não pode ser nulo. Aponta para o buffer de elementos `s`, dos quais os primeiros `c` são válidos.

- `_Outref_result_bytebuffer_to_(s, c)`

     O resultado deve ser válido em pós-Estado e não pode ser nulo. Aponta para o buffer de `s` bytes dos quais o primeiro `c` são válidos.

- `_Outref_result_buffer_all_(s)`

     O resultado deve ser válido em pós-Estado e não pode ser nulo. Aponta para um buffer válido de tamanho `s` elementos válidos.

- `_Outref_result_bytebuffer_all_(s)`

     O resultado deve ser válido em pós-Estado e não pode ser nulo. Aponta para um buffer válido de `s` bytes de elementos válidos.

- `_Outref_result_buffer_maybenull_(s)`

     O resultado deve ser válido em pós-Estado, mas pode ser nulo no pós-Estado. Aponta para um buffer válido de tamanho `s` elementos.

- `_Outref_result_bytebuffer_maybenull_(s)`

     O resultado deve ser válido em pós-Estado, mas pode ser nulo no pós-Estado. Aponta para um buffer válido de tamanho `s` bytes.

- `_Outref_result_buffer_to_maybenull_(s, c)`

     O resultado deve ser válido em pós-Estado, mas pode ser nulo no pós-Estado. Aponta para o buffer de elementos `s`, dos quais os primeiros `c` são válidos.

- `_Outref_result_bytebuffer_to_maybenull_(s,c)`

     O resultado deve ser válido em pós-Estado, mas pode ser nulo no estado de post. Aponta para o buffer de `s` bytes dos quais o primeiro `c` são válidos.

- `_Outref_result_buffer_all_maybenull_(s)`

     O resultado deve ser válido em pós-Estado, mas pode ser nulo no estado de post. Aponta para um buffer válido de tamanho `s` elementos válidos.

- `_Outref_result_bytebuffer_all_maybenull_(s)`

     O resultado deve ser válido em pós-Estado, mas pode ser nulo no estado de post. Aponta para um buffer válido de `s` bytes de elementos válidos.

## <a name="return-values"></a>Valores de Retorno

O valor de retorno de uma função é semelhante a um parâmetro `_Out_`, mas está em um nível diferente de de referência, e você não precisa considerar o conceito do ponteiro para o resultado.  Para as seguintes anotações, o valor de retorno é o objeto anotado — um escalar, um ponteiro para uma struct ou um ponteiro para um buffer. Essas anotações têm a mesma semântica que a anotação de `_Out_` correspondente.

|||
|-|-|
|`_Ret_z_`<br /><br /> `_Ret_writes_(s)`<br /><br /> `_Ret_writes_bytes_(s)`<br /><br /> `_Ret_writes_z_(s)`<br /><br /> `_Ret_writes_to_(s,c)`<br /><br /> `_Ret_writes_maybenull_(s)`<br /><br /> `_Ret_writes_to_maybenull_(s)`<br /><br /> `_Ret_writes_maybenull_z_(s)`|`_Ret_maybenull_`<br /><br /> `_Ret_maybenull_z_`<br /><br /> `_Ret_null_`<br /><br /> `_Ret_notnull_`<br /><br /> `_Ret_writes_bytes_to_`<br /><br /> `_Ret_writes_bytes_maybenull_`<br /><br /> `_Ret_writes_bytes_to_maybenull_`|

## <a name="format-string-parameters"></a>Parâmetros de cadeia de caracteres de formato

- `_Printf_format_string_` indica que o parâmetro é uma cadeia de caracteres de formato para uso em uma expressão `printf`.

     **Exemplo**

    ```cpp
    int MyPrintF(_Printf_format_string_ const wchar_t* format, ...)
    {
           va_list args;
           va_start(args, format);
           int ret = vwprintf(format, args);
           va_end(args);
           return ret;
    }
    ```

- `_Scanf_format_string_` indica que o parâmetro é uma cadeia de caracteres de formato para uso em uma expressão `scanf`.

     **Exemplo**

    ```cpp
    int MyScanF(_Scanf_format_string_ const wchar_t* format, ...)
    {
           va_list args;
           va_start(args, format);
           int ret = vwscanf(format, args);
           va_end(args);
           return ret;
    }
    ```

- `_Scanf_s_format_string_` indica que o parâmetro é uma cadeia de caracteres de formato para uso em uma expressão `scanf_s`.

     **Exemplo**

    ```cpp
    int MyScanF_s(_Scanf_s_format_string_ const wchar_t* format, ...)
    {
           va_list args;
           va_start(args, format);
           int ret = vwscanf_s(format, args);
           va_end(args);
           return ret;
    }
    ```

## <a name="other-common-annotations"></a>Outras anotações comuns

**Anotações e descrições**

- `_In_range_(low, hi)`

     `_Out_range_(low, hi)`

     `_Ret_range_(low, hi)`

     `_Deref_in_range_(low, hi)`

     `_Deref_out_range_(low, hi)`

     `_Deref_inout_range_(low, hi)`

     `_Field_range_(low, hi)`

     O parâmetro, o campo ou o resultado está no intervalo (inclusive) de `low` a `hi`.  Equivalente a `_Satisfies_(_Curr_ >= low && _Curr_ <= hi)` que é aplicado ao objeto anotado junto com as condições de pré-estado ou pós-Estado apropriadas.

    > [!IMPORTANT]
    > Embora os nomes contenham "in" e "out", a semântica de `_In_` e `_Out_` **não** se aplicam a essas anotações.

- `_Pre_equal_to_(expr)`

     `_Post_equal_to_(expr)`

     O valor anotado é exatamente `expr`.  Equivalente a `_Satisfies_(_Curr_ == expr)` que é aplicado ao objeto anotado junto com as condições de pré-estado ou pós-Estado apropriadas.

- `_Struct_size_bytes_(size)`

     Aplica-se a uma declaração de struct ou Class.  Indica que um objeto válido desse tipo pode ser maior que o tipo declarado, com o número de bytes sendo fornecido por `size`.  Por exemplo:

     `typedef _Struct_size_bytes_(nSize) struct MyStruct {    size_t nSize;    ... };`

     O tamanho do buffer em bytes de um parâmetro `pM` do tipo `MyStruct *` é então usado para ser:

     `min(pM->nSize, sizeof(MyStruct))`

## <a name="related-resources"></a>Recursos relacionados

[Blog da equipe de análise de código](https://blogs.msdn.microsoft.com/codeanalysis/)

## <a name="see-also"></a>Consulte também

- [Usando anotações de SAL para reduzir defeitos de código do C/C++](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)
- [Noções básicas de SAL](../code-quality/understanding-sal.md)
- [Anotando o comportamento da função](../code-quality/annotating-function-behavior.md)
- [Anotando estruturas e classes](../code-quality/annotating-structs-and-classes.md)
- [Anotando o comportamento de bloqueio](../code-quality/annotating-locking-behavior.md)
- [Especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md)
- [Funções intrínsecas](../code-quality/intrinsic-functions.md)
- [Práticas recomendadas e exemplos](../code-quality/best-practices-and-examples-sal.md)
