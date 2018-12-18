---
title: Práticas recomendadas e exemplos (SAL) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 666276fb-99c2-4dc9-8bac-d74861c203ea
caps.latest.revision: 14
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: 9327ab850bb5f62158e48abc4c8445d3f9b6fe9b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51743745"
---
# <a name="best-practices-and-examples-sal"></a>Práticas recomendadas e exemplos (SAL)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aqui estão algumas maneiras de obter o máximo de fora a fonte de código SAL (Annotation Language) e evitar alguns problemas comuns.  
  
## <a name="in"></a>\_In\_
 Se a função deve para gravar o elemento, use `_Inout_` em vez de `_In_`. Isso é particularmente relevante em casos de conversão automatizado de macros mais antigas em SAL. Antes de SAL, muitos programadores usavam macros como comentários — macros que foram nomeadas `IN`, `OUT`, `IN_OUT`, ou variantes desses nomes. Embora seja recomendável que você converta essas macros para SAL, também solicitamos que você tomar cuidado ao convertê-los porque o código pode ter sido alterado desde o protótipo original foi escrito e a macro antiga não pode refletir o código faz. Cuidado especial sobre o `OPTIONAL` comentar macro porque ele frequentemente é colocado incorretamente — por exemplo, no lado errado de uma vírgula.  
  
```cpp  
  
// Incorrect  
void Func1(_In_ int *p1)  
{  
    if (p1 == NULL)   
        return;  
  
    *p1 = 1;  
}  
  
// Correct  
void Func2(_Inout_ PCHAR p1)  
{  
    if (p1 == NULL)   
        return;  
  
    *p1 = 1;  
}  
```  
  
## <a name="opt"></a>\_opt\_  
 Se o chamador não tem permissão para passar um ponteiro nulo, use `_In_` ou `_Out_` em vez de `_In_opt_` ou `_Out_opt_`. Isso se aplica até mesmo para uma função que verifica seus parâmetros e retorna um erro se ele for nulo quando ele não deve ser. Apesar de ter uma função que verificar seu parâmetro para nulo inesperado e retornar normalmente é uma boa prática de codificação defensiva, isso não significa que a anotação do parâmetro pode ser de um tipo opcional (\_*Xxx*opt\_).  
  
```cpp  
  
// Incorrect  
void Func1(_Out_opt_ int *p1)  
{  
    *p = 1;  
}  
  
// Correct  
void Func2(_Out_ int *p1)  
{  
    *p = 1;  
}  
  
```  
  
## <a name="predefensive-and-postdefensive"></a>\_Pre_defensive\_ e \_Post_defensive\_  
 Se uma função é exibida em um limite de confiança, é recomendável que você use o `_Pre_defensive_` anotação.  O modificador "defensivo" modifica determinadas anotações para indicar que, no ponto de chamada, a interface deve ser verificada estritamente, mas no corpo da implementação deve presumir que os parâmetros incorretos podem ser passados. Nesse caso, `_In_ _Pre_defensive_` é preferencial em um limite de confiança para indicar que, embora um chamador receberá um erro se tentar passar NULL, o corpo da função será analisado como se o parâmetro pode ser NULL e qualquer tentativa de cancelar a referência de ponteiro sem primeiro a verificação para nulo será sinalizada.  Um `_Post_defensive_` anotação também está disponível, para uso nos retornos de chamada em que a parte confiável é considerado como o chamador e o código não confiável é o código de chamada.  
  
## <a name="outwrites"></a>\_Out_writes\_  
 O exemplo a seguir demonstra um uso indevido comuns do `_Out_writes_`.  
  
```cpp  
  
// Incorrect  
void Func1(_Out_writes_(size) CHAR *pb,   
    DWORD size  
);  
  
```  
  
 A anotação `_Out_writes_` significa que você tem um buffer. Ele tem `cb` bytes alocados, com o primeiro byte inicializado na saída. Essa anotação não é estritamente errada e é útil expressar o tamanho alocado. No entanto, ela não informa quantos elementos são inicializados pela função.  
  
 O exemplo a seguir mostra três maneiras corretas para especificar completamente o tamanho exato da parte inicializado do buffer.  
  
```cpp  
  
// Correct  
void Func1(_Out_writes_to_(size, *pCount) CHAR *pb,   
    DWORD size,  
    PDWORD pCount  
);  
  
void Func2(_Out_writes_all_(size) CHAR *pb,   
    DWORD size  
);  
  
void Func3(_Out_writes_(size) PSTR pb,   
    DWORD size  
);  
  
```  
  
## <a name="out-pstr"></a>\_Out\_ PSTR  
 O uso de `_Out_ PSTR` é quase sempre errado. Isso é interpretado como tendo um parâmetro de saída que aponta para um buffer de caracteres e é terminada em nulo.  
  
```cpp  
  
// Incorrect  
void Func1(_Out_ PSTR pFileName, size_t n);  
  
// Correct  
void Func2(_Out_writes_(n) PSTR wszFileName, size_t n);  
  
```  
  
 Como uma anotação `_In_ PCSTR` é comum e útil. Ele aponta para uma cadeia de caracteres de entrada que tem terminação NULL porque a pré-condição de `_In_` permite que o reconhecimento de uma cadeia de caracteres terminada em nulo.  
  
## <a name="in-wchar-p"></a>\_No\_ WCHAR * p  
 `_In_ WCHAR* p` diz que há um ponteiro de entrada `p` que aponta para um caractere. No entanto, na maioria dos casos, isso provavelmente não é a especificação que se destina. Em vez disso, o que provavelmente destina-se é a especificação de uma matriz terminada em nulo; Para fazer isso, use `_In_ PWSTR`.  
  
```cpp  
  
// Incorrect  
void Func1(_In_ WCHAR* wszFileName);  
  
// Correct  
void Func2(_In_ PWSTR wszFileName);  
  
```  
  
 É comum que tem a especificação de apropriada de finalização NULL. Usar apropriado `STR` versão para substituir o tipo, conforme mostrado no exemplo a seguir.  
  
```cpp  
  
// Incorrect  
BOOL StrEquals1(_In_ PCHAR p1, _In_ PCHAR p2)  
{  
    return strcmp(p1, p2) == 0;  
}  
  
// Correct  
BOOL StrEquals2(_In_ PSTR p1, _In_ PSTR p2)  
{  
    return strcmp(p1, p2) == 0;  
}  
  
```  
  
## <a name="outrange"></a>\_Out_range\_  
 Se o parâmetro é um ponteiro e você deseja expressar o intervalo do valor do elemento que é apontado pelo ponteiro, use `_Deref_out_range_` em vez de `_Out_range_`. No exemplo a seguir, o intervalo de * pcbFilled é expresso, não pcbFilled.  
  
```cpp  
  
// Incorrect  
void Func1(  
    _Out_writes_bytes_to_(cbSize, *pcbFilled) BYTE *pb,   
    DWORD cbSize,   
    _Out_range_(0, cbSize) DWORD *pcbFilled  
);  
  
// Correct  
void Func2(  
    _Out_writes_bytes_to_(cbSize, *pcbFilled) BYTE *pb,   
    DWORD cbSize,   
    _Deref_out_range_(0, cbSize) _Out_ DWORD *pcbFilled   
);  
  
```  
  
 `_Deref_out_range_(0, cbSize)` não é estritamente necessária para algumas ferramentas porque ele pode ser inferido de `_Out_writes_to_(cbSize,*pcbFilled)`, mas ele é mostrado aqui para fins de integridade.  
  
## <a name="wrong-context-in-when"></a>Incorreto contexto em \_quando\_  
 Outro erro comum é usar a avaliação de pós-estado de pré-condições. No exemplo a seguir, `_Requires_lock_held_` é uma pré-condição.  
  
```cpp  
  
// Incorrect  
_When_(return == 0, _Requires_lock_held_(p->cs))  
int Func1(_In_ MyData *p, int flag);  
  
// Correct  
_When_(flag == 0, _Requires_lock_held_(p->cs))  
int Func2(_In_ MyData *p, int flag);  
  
```  
  
 A expressão `result` refere-se a um valor de pós-estado não está disponível no estado de pré-lançamento.  
  
## <a name="true-in-success"></a>TRUE em \_sucesso\_  
 Se a função obtiver êxito quando o valor de retorno é diferente de zero, use `return != 0` como a condição de êxito em vez de `return == TRUE`. NonZero não significa necessariamente equivalência para o valor real que o compilador fornece para `TRUE`. O parâmetro para `_Success_` é uma expressão, e as seguintes expressões são avaliadas como equivalentes: `return != 0`, `return != false`, `return != FALSE`, e `return` sem parâmetros ou comparações.  
  
```cpp  
  
// Incorrect  
_Success_(return == TRUE, _Acquires_lock_(*lpCriticalSection))  
BOOL WINAPI TryEnterCriticalSection(  
  _Inout_ LPCRITICAL_SECTION lpCriticalSection  
);  
  
// Correct  
_Success_(return != 0, _Acquires_lock_(*lpCriticalSection))  
BOOL WINAPI TryEnterCriticalSection(  
  _Inout_ LPCRITICAL_SECTION lpCriticalSection  
);  
  
```  
  
## <a name="reference-variable"></a>Variável de referência  
 Para uma variável de referência, a versão anterior do SAL usado o ponteiro implícito como o destino de anotação e exigiu a adição de um `__deref` para anotações anexadas a uma variável de referência. Essa versão usa o próprio objeto e não requer adicional `_Deref_`.  
  
```cpp  
  
// Incorrect  
void Func1(  
    _Out_writes_bytes_all_(cbSize) BYTE *pb,   
    _Deref_ _Out_range_(0, 2) _Out_ DWORD &cbSize  
);  
  
// Correct  
void Func2(  
    _Out_writes_bytes_all_(cbSize) BYTE *pb,   
    _Out_range_(0, 2) _Out_ DWORD &cbSize  
);  
  
```  
  
## <a name="annotations-on-return-values"></a>Anotações em valores de retorno  
 O exemplo a seguir mostra um problema comum em anotações de valor de retorno.  
  
```cpp  
  
// Incorrect  
_Out_opt_ void *MightReturnNullPtr1();  
  
// Correct  
_Ret_maybenull_ void *MightReturnNullPtr2();  
  
```  
  
 Neste exemplo, `_Out_opt_` diz que o ponteiro pode ser NULL como parte da pré-condição. No entanto, as pré-condições não podem ser aplicadas ao valor de retorno. Nesse caso, a anotação correta é `_Ret_maybenull_`.  
  
## <a name="see-also"></a>Consulte também  
 [Usando anotações de SAL para reduzir defeitos de código C/C++](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [Noções básicas de SAL](../code-quality/understanding-sal.md)   
 [Anotando parâmetros de função e valores de retorno](../code-quality/annotating-function-parameters-and-return-values.md)   
 [Anotando o comportamento da função](../code-quality/annotating-function-behavior.md)   
 [Anotando estruturas e Classes](../code-quality/annotating-structs-and-classes.md)   
 [Anotando o comportamento de bloqueio](../code-quality/annotating-locking-behavior.md)   
 [Especificando quando e onde uma anotação se aplica](../code-quality/specifying-when-and-where-an-annotation-applies.md)   
 [Funções intrínsecas](../code-quality/intrinsic-functions.md)



