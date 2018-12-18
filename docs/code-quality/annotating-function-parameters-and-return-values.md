---
title: Anotando parâmetros de função e valores de retorno
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
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
ms.assetid: 82826a3d-0c81-421c-8ffe-4072555dca3a
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- multiple
ms.openlocfilehash: ae4fcfa442f648126a93d1ec6a3b0d3c4fc7c981
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49924818"
---
# <a name="annotating-function-parameters-and-return-values"></a>Anotando parâmetros de função e valores de retorno
Este artigo descreve os usos comuns de anotações para parâmetros de função simples — escalares e ponteiros para estruturas e classes — e a maioria dos tipos de buffers.  Este artigo também mostra padrões comuns de uso para anotações. Para anotações adicionais que estão relacionadas a funções, consulte [anotando o comportamento da função](../code-quality/annotating-function-behavior.md)

## <a name="pointer-parameters"></a>Parâmetros de ponteiro
 Para obter as anotações na tabela a seguir, quando um parâmetro de ponteiro está sendo anotado, o analisador relatará um erro se o ponteiro for nulo.  Isso se aplica aos ponteiros e para qualquer item de dados que é apontado.

 **Descrições e anotações**

-   `_In_`

     Anota os parâmetros de entrada são escalares, estruturas, ponteiros para estruturas e assim por diante.  Explicitamente, pode ser usada em escalares simples.  O parâmetro deve ser válido no estado de pré-lançamento e não será modificado.

-   `_Out_`

     Anota os parâmetros de saída que são escalares, estruturas, ponteiros para estruturas e assim por diante.  Não aplicá-la a um objeto que não é possível retornar um valor — por exemplo, um escalar que é passado por valor.  O parâmetro não tem que ser válido no estado anterior ao, mas deve ser válido no pós estado de.

-   `_Inout_`

     Anota um parâmetro que será alterado pela função.  Ele deve ser válido no estado de pré e pós-estado, mas deve para ter valores diferentes de antes e depois da chamada. Aplique a um valor modificável.

-   `_In_z_`

     Um ponteiro para uma cadeia de caracteres terminada em nulo que é usado como entrada.  A cadeia de caracteres deve ser válida no estado de pré-lançamento.  Variantes de `PSTR`, que já tem as anotações corretas, são preferencial.

-   `_Inout_z_`

     Um ponteiro para uma matriz de caracteres terminada em nulo que será modificada.  Ele deve ser válido antes e depois da chamada, mas o valor será considerado ter sido alterado.  O terminador nulo pode ser movido, mas apenas os elementos até o terminador nulo original podem ser acessados.

-   `_In_reads_(s)`

     `_In_reads_bytes_(s)`

     Um ponteiro para uma matriz, que é lido pela função.  A matriz é do tamanho `s` elementos, que deve ser válido.

     O `_bytes_` variante fornece o tamanho em bytes em vez de elementos. Use isso somente quando o tamanho não pode ser expresso como elementos.  Por exemplo, `char` cadeias de caracteres seriam usar o `_bytes_` variante somente se a função uma semelhante que usa `wchar_t` seria.

-   `_In_reads_z_(s)`

     Um ponteiro para uma matriz que é terminada em nulo e tem um tamanho conhecido. Os elementos até o terminador nulo — ou `s` se houver um terminador nulo — deve ser válido no estado de pré-lançamento.  Se o tamanho é conhecido em bytes, dimensionar `s` pelo tamanho do elemento.

-   `_In_reads_or_z_(s)`

     Um ponteiro para uma matriz que é terminada em nulo ou tem um tamanho conhecido, ou ambos. Os elementos até o terminador nulo — ou `s` se houver um terminador nulo — deve ser válido no estado de pré-lançamento.  Se o tamanho é conhecido em bytes, dimensionar `s` pelo tamanho do elemento.  (Usado para o `strn` família.)

-   `_Out_writes_(s)`

     `_Out_writes_bytes_(s)`

     Um ponteiro para uma matriz de `s` elementos (bytes Resp) que serão gravados pela função.  Os elementos da matriz não precisa ser válido no pré- estado de e o número de elementos que são válidos em pós-estado não está especificado.  Se não houver anotações no tipo de parâmetro, elas são aplicadas na pós-estado. Por exemplo, considere o código a seguir.

     `typedef _Null_terminated_ wchar_t *PWSTR; void MyStringCopy(_Out_writes_ (size) PWSTR p1,    _In_ size_t size,    _In_ PWSTR p2);`

     Neste exemplo, o chamador fornece um buffer de `size` elementos para `p1`.  `MyStringCopy` Alguns desses elementos torna válido. Mais importante, o `_Null_terminated_` anotação no `PWSTR` significa que `p1` é terminada em nulo no pós estado de.  Dessa forma, o número de elementos válidos é ainda bem definido, mas a contagem de um elemento específico não é necessária.

     O `_bytes_` variante fornece o tamanho em bytes em vez de elementos. Use isso somente quando o tamanho não pode ser expresso como elementos.  Por exemplo, `char` cadeias de caracteres seriam usar o `_bytes_` variante somente se a função uma semelhante que usa `wchar_t` seria.

-   `_Out_writes_z_(s)`

     Um ponteiro para uma matriz de `s` elementos.  Os elementos não precisam ser válido no estado de pré-lançamento.  Pós-estado, os elementos de backup por meio do terminador nulo — que deve estar presente — deve ser válido.  Se o tamanho é conhecido em bytes, dimensionar `s` pelo tamanho do elemento.

-   `_Inout_updates_(s)`

     `_Inout_updates_bytes_(s)`

     Um ponteiro para uma matriz, que é lida e gravada na função.  Ele é do tamanho `s` elementos e é válido no estado de pré e pós-estado.

     O `_bytes_` variante fornece o tamanho em bytes em vez de elementos. Use isso somente quando o tamanho não pode ser expresso como elementos.  Por exemplo, `char` cadeias de caracteres seriam usar o `_bytes_` variante somente se a função uma semelhante que usa `wchar_t` seria.

-   `_Inout_updates_z_(s)`

     Um ponteiro para uma matriz que é terminada em nulo e tem um tamanho conhecido. Os elementos de backup por meio do terminador nulo — que deve estar presente — deve ser válido no estado de pré e pós-estado.  É provável que o valor no estado após ser diferente do valor no pré estado; Isso inclui o local do terminador nulo. Se o tamanho é conhecido em bytes, dimensionar `s` pelo tamanho do elemento.

-   `_Out_writes_to_(s,c)`

     `_Out_writes_bytes_to_(s,c)`

     `_Out_writes_all_(s)`

     `_Out_writes_bytes_all_(s)`

     Um ponteiro para uma matriz de `s` elementos.  Os elementos não precisam ser válido no estado de pré-lançamento.  Pós-estado, elementos até o `c`- ésimo elemento deve ser válido.  Se o tamanho é conhecido em bytes, dimensione `s` e `c` pelo tamanho do elemento ou use o `_bytes_` variante, que é definida como:

     `_Out_writes_to_(_Old_(s), _Old_(s))    _Out_writes_bytes_to_(_Old_(s), _Old_(s))`

     Em outras palavras, todos os elementos que existe no buffer até `s` no estado de pré-lançamento é válido no pós estado de.  Por exemplo:

     `void *memcpy(_Out_writes_bytes_all_(s) char *p1,    _In_reads_bytes_(s) char *p2,    _In_ int s); void * wordcpy(_Out_writes_all_(s) DWORD *p1,     _In_reads_(s) DWORD *p2,    _In_ int s);`

-   `_Inout_updates_to_(s,c)`

     `_Inout_updates_bytes_to_(s,c)`

     Um ponteiro para uma matriz, que é lida e gravada pela função.  Ele é de tamanho `s` elementos, que deve ser válido no estado de pré-lançamento, e `c` elementos devem ser válidos no pós estado de.

     O `_bytes_` variante fornece o tamanho em bytes em vez de elementos. Use isso somente quando o tamanho não pode ser expresso como elementos.  Por exemplo, `char` cadeias de caracteres seriam usar o `_bytes_` variante somente se a função uma semelhante que usa `wchar_t` seria.

-   `_Inout_updates_z_(s)`

     Um ponteiro para uma matriz que é terminada em nulo e tem um tamanho conhecido. Os elementos de backup por meio do terminador nulo — que deve estar presente — deve ser válido no estado de pré e pós-estado.  É provável que o valor no estado após ser diferente do valor no pré estado; Isso inclui o local do terminador nulo. Se o tamanho é conhecido em bytes, dimensionar `s` pelo tamanho do elemento.

-   `_Out_writes_to_(s,c)`

     `_Out_writes_bytes_to_(s,c)`

     `_Out_writes_all_(s)`

     `_Out_writes_bytes_all_(s)`

     Um ponteiro para uma matriz de `s` elementos.  Os elementos não precisam ser válido no estado de pré-lançamento.  Pós-estado, elementos até o `c`- ésimo elemento deve ser válido.  Se o tamanho é conhecido em bytes, dimensione `s` e `c` pelo tamanho do elemento ou use o `_bytes_` variante, que é definida como:

     `_Out_writes_to_(_Old_(s), _Old_(s))    _Out_writes_bytes_to_(_Old_(s), _Old_(s))`

     Em outras palavras, todos os elementos que existe no buffer até `s` no estado de pré-lançamento é válido no pós estado de.  Por exemplo:

     `void *memcpy(_Out_writes_bytes_all_(s) char *p1,    _In_reads_bytes_(s) char *p2,    _In_ int s); void * wordcpy(_Out_writes_all_(s) DWORD *p1,     _In_reads_(s) DWORD *p2,    _In_ int s);`

-   `_Inout_updates_to_(s,c)`

     `_Inout_updates_bytes_to_(s,c)`

     Um ponteiro para uma matriz, que é lida e gravada pela função.  Ele é de tamanho `s` elementos, que deve ser válido no estado de pré-lançamento, e `c` elementos devem ser válidos no pós estado de.

     O `_bytes_` variante fornece o tamanho em bytes em vez de elementos. Use isso somente quando o tamanho não pode ser expresso como elementos.  Por exemplo, `char` cadeias de caracteres seriam usar o `_bytes_` variante somente se a função uma semelhante que usa `wchar_t` seria.

-   `_Inout_updates_all_(s)`

     `_Inout_updates_bytes_all_(s)`

     Um ponteiro para uma matriz, que é lida e gravada pela função do tamanho `s` elementos. Definido como equivalente a:

     `_Inout_updates_to_(_Old_(s), _Old_(s))    _Inout_updates_bytes_to_(_Old_(s), _Old_(s))`

     Em outras palavras, todos os elementos que existe no buffer até `s` no estado de pré-lançamento é válido no estado de pré e pós-estado.

     O `_bytes_` variante fornece o tamanho em bytes em vez de elementos. Use isso somente quando o tamanho não pode ser expresso como elementos.  Por exemplo, `char` cadeias de caracteres seriam usar o `_bytes_` variante somente se a função uma semelhante que usa `wchar_t` seria.

-   `_In_reads_to_ptr_(p)`

     Um ponteiro para uma matriz para o qual a expressão `p`  -  `_Curr_` (ou seja, `p` menos `_Curr_`) é definido pelo padrão da linguagem apropriado.  Os elementos anteriores ao `p` deve ser válido no estado de pré-lançamento.

-   `_In_reads_to_ptr_z_(p)`

     Um ponteiro para uma matriz terminada em nulo para o qual a expressão `p`  -  `_Curr_` (ou seja, `p` menos `_Curr_`) é definido pelo padrão da linguagem apropriado.  Os elementos anteriores ao `p` deve ser válido no estado de pré-lançamento.

-   `_Out_writes_to_ptr_(p)`

     Um ponteiro para uma matriz para o qual a expressão `p`  -  `_Curr_` (ou seja, `p` menos `_Curr_`) é definido pelo padrão da linguagem apropriado.  Os elementos anteriores ao `p` não precisa ser válido no estado de pré-lançamento e deve ser válido no pós estado de.

-   `_Out_writes_to_ptr_z_(p)`

     Um ponteiro para uma matriz terminada em nulo para o qual a expressão `p`  -  `_Curr_` (ou seja, `p` menos `_Curr_`) é definido pelo padrão da linguagem apropriado.  Os elementos anteriores ao `p` não precisa ser válido no estado de pré-lançamento e deve ser válido no pós estado de.

## <a name="optional-pointer-parameters"></a>Parâmetros opcionais de ponteiro
 Quando uma anotação de parâmetro de ponteiro inclui `_opt_`, ele indica que o parâmetro pode ser nulo. Caso contrário, a anotação executa a mesma versão que não inclua `_opt_`. Aqui está uma lista da `_opt_` variantes de anotações de parâmetro de ponteiro:

||||
|-|-|-|
|`_In_opt_`<br /><br /> `_Out_opt_`<br /><br /> `_Inout_opt_`<br /><br /> `_In_opt_z_`<br /><br /> `_Inout_opt_z_`<br /><br /> `_In_reads_opt_`<br /><br /> `_In_reads_bytes_opt_`<br /><br /> `_In_reads_opt_z_`|`_Out_writes_opt_`<br /><br /> `_Out_writes_opt_z_`<br /><br /> `_Inout_updates_opt_`<br /><br /> `_Inout_updates_bytes_opt_`<br /><br /> `_Inout_updates_opt_z_`<br /><br /> `_Out_writes_to_opt_`<br /><br /> `_Out_writes_bytes_to_opt_`<br /><br /> `_Out_writes_all_opt_`<br /><br /> `_Out_writes_bytes_all_opt_`|`_Inout_updates_to_opt_`<br /><br /> `_Inout_updates_bytes_to_opt_`<br /><br /> `_Inout_updates_all_opt_`<br /><br /> `_Inout_updates_bytes_all_opt_`<br /><br /> `_In_reads_to_ptr_opt_`<br /><br /> `_In_reads_to_ptr_opt_z_`<br /><br /> `_Out_writes_to_ptr_opt_`<br /><br /> `_Out_writes_to_ptr_opt_z_`|

## <a name="output-pointer-parameters"></a>Parâmetros de ponteiro de saída
 Parâmetros de ponteiro de saída exigem uma notação especial para remover a ambiguidade a nulidade no parâmetro e o local apontado.

 **Descrições e anotações**

- `_Outptr_`

   O parâmetro não pode ser nulo e no pós-estado de o local apontado para não pode ser nulo e deve ser válido.

- `_Outptr_opt_`

   O parâmetro pode ser nulo, mas no pós-estado de o local apontado para não pode ser nulo e deve ser válido.

- `_Outptr_result_maybenull_`

   O parâmetro não pode ser nulo e no pós-estado de o local apontado pode ser nulo.

- `_Outptr_opt_result_maybenull_`

   O parâmetro pode ser nulo e no pós-estado de o local apontado pode ser nulo.

  Na tabela a seguir, as subcadeias de caracteres adicionais são inseridas no nome da anotação para qualificar ainda mais o significado da anotação.  Diversas subcadeias de caracteres são `_z`, `_COM_`, `_buffer_`, `_bytebuffer_`, e `_to_`.

> [!IMPORTANT]
>  Se a interface que você estiver fazendo anotações é COM, use o formulário COM dessas anotações. Não use anotações COM qualquer outra interface de tipo.

 **Descrições e anotações**

- `_Outptr_result_z_`

   `_Outptr_opt_result_z_`

   `_Outptr_result_maybenull_z_`

   `_Ouptr_opt_result_maybenull_z_`

   O ponteiro retornado tem o `_Null_terminated_` anotação.

- `_COM_Outptr_`

   `_COM_Outptr_opt_`

   `_COM_Outptr_result_maybenull_`

   `_COM_Outptr_opt_result_maybenull_`

   O ponteiro retornado tem semântica COM e, portanto, carrega um `_On_failure_` pós-condição em que o ponteiro retornado é nulo.

- `_Outptr_result_buffer_(s)`

   `_Outptr_result_bytebuffer_(s)`

   `_Outptr_opt_result_buffer_(s)`

   `_Outptr_opt_result_bytebuffer_(s)`

   O ponteiro retornado aponta para um buffer válido de tamanho `s` elementos ou bytes.

- `_Outptr_result_buffer_to_(s, c)`

   `_Outptr_result_bytebuffer_to_(s, c)`

   `_Outptr_opt_result_buffer_to_(s,c)`

   `_Outptr_opt_result_bytebuffer_to_(s,c)`

   O ponteiro retornado aponta para um buffer de tamanho `s` elementos ou bytes, dos quais o primeiro `c` são válidos.

  Certas convenções de interface presumem que os parâmetros de saída são inúteis em caso de falha.  Exceto para explicitamente COM código, os formulários na tabela a seguir são preferenciais.  Para o código de COM, use formas COM correspondentes que estão listadas na seção anterior.

  **Descrições e anotações**

- `_Result_nullonfailure_`

   Modifica a outras anotações. O resultado é definido como nulo se a função falhar.

- `_Result_zeroonfailure_`

   Modifica a outras anotações. O resultado é definido como zero se a função falhar.

- `_Outptr_result_nullonfailure_`

   O ponteiro retornado aponta para um buffer válido se a função for bem-sucedida, ou nulo se a função falhar. Essa anotação é para um parâmetro não opcionais.

- `_Outptr_opt_result_nullonfailure_`

   O ponteiro retornado aponta para um buffer válido se a função for bem-sucedida, ou nulo se a função falhar. Essa anotação é para um parâmetro opcional.

- `_Outref_result_nullonfailure_`

   O ponteiro retornado aponta para um buffer válido se a função for bem-sucedida, ou nulo se a função falhar. Essa anotação é para um parâmetro de referência.

## <a name="output-reference-parameters"></a>Parâmetros de referência de saída
 Um uso comum do parâmetro de referência é para parâmetros de saída.  Para parâmetros de referência de saída simples — por exemplo, `int&`—`_Out_` fornece a semântica correta.  No entanto, quando o valor de saída é um ponteiro — por exemplo `int *&`— as anotações equivalentes de ponteiro, como `_Outptr_ int **` não fornecem a semântica correta.  Para expressar concisa a semântica de referência de parâmetros de saída para tipos de ponteiro, use essas anotações de composição:

 **Descrições e anotações**

-   `_Outref_`

     Resultado deve ser válido no pós- estado de e não pode ser nulo.

-   `_Outref_result_maybenull_`

     Resultado deve ser válido no pós-estado de, mas pode ser nulo na pós-estado.

-   `_Outref_result_buffer_(s)`

     Resultado deve ser válido no pós- estado de e não pode ser nulo. Aponta para um buffer válido de tamanho `s` elementos.

-   `_Outref_result_bytebuffer_(s)`

     Resultado deve ser válido no pós- estado de e não pode ser nulo. Aponta para um buffer válido de tamanho `s` bytes.

-   `_Outref_result_buffer_to_(s, c)`

     Resultado deve ser válido no pós- estado de e não pode ser nulo. Aponta para o buffer de `s` elementos, dos quais o primeiro `c` são válidos.

-   `_Outref_result_bytebuffer_to_(s, c)`

     Resultado deve ser válido no pós- estado de e não pode ser nulo. Aponta para o buffer de `s` bytes da qual o primeiro `c` são válidos.

-   `_Outref_result_buffer_all_(s)`

     Resultado deve ser válido no pós- estado de e não pode ser nulo. Aponta para um buffer válido de tamanho `s` elementos válidos.

-   `_Outref_result_bytebuffer_all_(s)`

     Resultado deve ser válido no pós- estado de e não pode ser nulo. Aponta para um buffer válido de `s` bytes de elementos válidos.

-   `_Outref_result_buffer_maybenull_(s)`

     Resultado deve ser válido no pós-estado de, mas pode ser nulo na pós-estado. Aponta para um buffer válido de tamanho `s` elementos.

-   `_Outref_result_bytebuffer_maybenull_(s)`

     Resultado deve ser válido no pós-estado de, mas pode ser nulo na pós-estado. Aponta para um buffer válido de tamanho `s` bytes.

-   `_Outref_result_buffer_to_maybenull_(s, c)`

     Resultado deve ser válido no pós-estado de, mas pode ser nulo na pós-estado. Aponta para o buffer de `s` elementos, dos quais o primeiro `c` são válidos.

-   `_Outref_result_bytebuffer_to_maybenull_(s,c)`

     Resultado deve ser válido no pós-estado de, mas pode ser nulo no estado de postagem. Aponta para o buffer de `s` bytes da qual o primeiro `c` são válidos.

-   `_Outref_result_buffer_all_maybenull_(s)`

     Resultado deve ser válido no pós-estado de, mas pode ser nulo no estado de postagem. Aponta para um buffer válido de tamanho `s` elementos válidos.

-   `_Outref_result_bytebuffer_all_maybenull_(s)`

     Resultado deve ser válido no pós-estado de, mas pode ser nulo no estado de postagem. Aponta para um buffer válido de `s` bytes de elementos válidos.

## <a name="return-values"></a>Valores de Retorno
 O valor de retorno de uma função é semelhante a um `_Out_` parâmetro, mas é um nível diferente de de-reference, e você não deve considerar o conceito do ponteiro para o resultado.  Para obter as seguintes anotações, o valor retornado é o objeto anotado — um escalar, um ponteiro para uma estrutura ou um ponteiro para um buffer. Essas anotações têm a mesma semântica correspondente `_Out_` anotação.

|||
|-|-|
|`_Ret_z_`<br /><br /> `_Ret_writes_(s)`<br /><br /> `_Ret_writes_bytes_(s)`<br /><br /> `_Ret_writes_z_(s)`<br /><br /> `_Ret_writes_to_(s,c)`<br /><br /> `_Ret_writes_maybenull_(s)`<br /><br /> `_Ret_writes_to_maybenull_(s)`<br /><br /> `_Ret_writes_maybenull_z_(s)`|`_Ret_maybenull_`<br /><br /> `_Ret_maybenull_z_`<br /><br /> `_Ret_null_`<br /><br /> `_Ret_notnull_`<br /><br /> `_Ret_writes_bytes_to_`<br /><br /> `_Ret_writes_bytes_maybenull_`<br /><br /> `_Ret_writes_bytes_to_maybenull_`|

## <a name="other-common-annotations"></a>Outras anotações comuns
 **Descrições e anotações**

-   `_In_range_(low, hi)`

     `_Out_range_(low, hi)`

     `_Ret_range_(low, hi)`

     `_Deref_in_range_(low, hi)`

     `_Deref_out_range_(low, hi)`

     `_Deref_inout_range_(low, hi)`

     `_Field_range_(low, hi)`

     O parâmetro, o campo ou o resultado está no intervalo (inclusivo) de `low` para `hi`.  Equivalente a `_Satisfies_(_Curr_ >= low && _Curr_ <= hi)` que é aplicado ao objeto anotado junto com as condições de estado pré ou pós-estaduais apropriados.

    > [!IMPORTANT]
    >  Embora os nomes contêm "in" e "out", a semântica dos `_In_` e `_Out_` fazer **não** se aplicam a essas anotações.

-   `_Pre_equal_to_(expr)`

     `_Post_equal_to_(expr)`

     O valor anotado é exatamente `expr`.  Equivalente a `_Satisfies_(_Curr_ == expr)` que é aplicado ao objeto anotado junto com as condições de estado pré ou pós-estaduais apropriados.

-   `_Struct_size_bytes_(size)`

     Aplica-se a uma declaração de classe ou struct.  Indica que um objeto válido desse tipo pode ser maior do que o tipo declarado, com o número de bytes que estão sendo fornecidos pelo `size`.  Por exemplo:

     `typedef _Struct_size_bytes_(nSize) struct MyStruct {    size_t nSize;    ... };`

     O tamanho do buffer em bytes de um parâmetro `pM` do tipo `MyStruct *` , em seguida, será tomado como:

     `min(pM->nSize, sizeof(MyStruct))`

## <a name="related-resources"></a>Recursos relacionados
 [Blog da equipe de análise de código](http://go.microsoft.com/fwlink/?LinkId=251197)

## <a name="see-also"></a>Consulte também
 [Usando anotações de SAL para reduzir defeitos de código C/C++](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md) [Noções básicas sobre o SAL](../code-quality/understanding-sal.md) [anotando o comportamento da função](../code-quality/annotating-function-behavior.md) [anotando estruturas e Classes](../code-quality/annotating-structs-and-classes.md) [ Anotando o comportamento de bloqueio](../code-quality/annotating-locking-behavior.md) [especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md) [funções intrínsecas](../code-quality/intrinsic-functions.md) [práticas recomendadas e exemplos](../code-quality/best-practices-and-examples-sal.md)