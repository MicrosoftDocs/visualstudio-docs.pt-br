---
title: Asserções C/C++ | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [MFC], assertions
- results, checking
- result checking
- Call Stack window, assertion failures
- debugging [C++], assertions
- VERIFY macro
- assertions, side effects
- assertions
- ASSERT macro
- errors [C++], catching with assertions
- testing, error conditions with assertion statements
- _DEBUG macro
- Assertion Failed dialog box
- failures, finding locations
ms.assetid: 2d7b0121-71aa-414b-bbb6-ede1093d0bfc
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: c91ff9d752e2043829b3ea310606a9d8b82b1e1e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49845986"
---
# <a name="cc-assertions"></a>Asserções C/C++
Uma instrução de declaração especifica uma condição que você espera ser verdadeira em um ponto específico em seu programa. Se essa condição não for true, a asserção falhará, a execução do programa é interrompida e o [caixa de diálogo Falha na asserção](../debugger/assertion-failed-dialog-box.md) é exibida.  

 O Visual C++ dá suporte a instruções de declaração baseadas nestes constructos:  

- Asserções MFC para programas MFC.  

- [{1&gt;ATLASSERT&lt;1](/cpp/atl/reference/debugging-and-error-reporting-macros#atlassert) para programas que usam ATL.  

- Asserções de CRT para programas que usam a biblioteca em tempo de execução C.  

- ANSI [função assert](/cpp/c-runtime-library/reference/assert-macro-assert-wassert) para outros programas C/C++.  

  Você pode usar asserções para capturar erros lógicos, para verificar os resultados de uma operação e para testar condições de erro que deveriam ter sido tratadas.  

##  <a name="BKMK_In_this_topic"></a> Neste tópico  
 [Como funcionam as asserções](#BKMK_How_assertions_work)  

 [Asserções em compilações de depuração e versão](#BKMK_Assertions_in_Debug_and_Release_builds)  

 [Efeitos colaterais do uso de asserções](#BKMK_Side_effects_of_using_assertions)  

 [Asserções CRT](#BKMK_CRT_assertions)  

 [Asserções MFC](#BKMK_MFC_assertions)  

- [MFC ASSERT_VALID e CObject::assertvalid&lt;1}](#BKMK_MFC_ASSERT_VALID_and_CObject__AssertValid)  

- [Limitações de assertvalid&lt;1}](#BKMK_Limitations_of_AssertValid)  

  [Usando asserções](#BKMK_Using_assertions)  

- [Capturando erros lógicos](#BKMK_Catching_logic_errors)  

- [Verificando resultados](#BKMK_Checking_results_)  

- [Localizando erros sem tratamento](#BKMK_Testing_error_conditions_)  

##  <a name="BKMK_How_assertions_work"></a> Como funcionam as asserções  
 Quando o depurador é interrompido devido a uma asserção MFC ou da biblioteca em tempo de execução C, então, se a origem está disponível, o depurador navega até o ponto no arquivo de origem onde a asserção ocorreu. A mensagem da asserção aparece em ambas as [janela de saída](../ide/reference/output-window.md) e o **Falha na asserção** caixa de diálogo. Você pode copiar a mensagem da asserção do **saída** janela para uma janela de texto se você deseja salvá-la para referência futura. O **saída** janela pode conter outras mensagens de erro. Examine essas mensagens com cuidado, pois elas fornecem indícios da causa da falha de asserção.  

 Use asserções para detectar erros durante o desenvolvimento. Em geral, use uma asserção para cada suposição. Por exemplo, se você supõe que um argumento não é NULL, use uma asserção para testar essa suposição.  

 [Neste tópico](#BKMK_In_this_topic)  

##  <a name="BKMK_Assertions_in_Debug_and_Release_builds"></a> Asserções em compilações de depuração e versão  
 As instruções de declaração são compiladas apenas se `_DEBUG` é definido. Caso contrário, o compilador trata as asserções como instruções nulas. Em virtude disso, as instruções de declaração não impõem nenhuma sobrecarga ou custo de desempenho no seu programa da versão final, e permitem que você evite usar políticas `#ifdef`.  

##  <a name="BKMK_Side_effects_of_using_assertions"></a> Efeitos colaterais do uso de asserções  
 Quando adicionar asserções ao seu código, verifique se elas não têm efeitos colaterais. Por exemplo, considere a seguinte asserção que altera o valor de `nM`:  

```cpp
ASSERT(nM++ > 0); // Don't do this!  
```  

 Como a expressão `ASSERT` não é avaliada na versão de liberação do programa, `nM` terá valores diferentes nas versões de depuração e de liberação. Para evitar esse problema no MFC, você pode usar o [VERIFY](/cpp/mfc/reference/diagnostic-services#verify) macro em vez de `ASSERT`.  `VERIFY` avalia a expressão em todas as versões, mas não verifica o resultado na versão de lançamento.  

 Tenha cuidado especial quando usar chamadas de função em instruções de declaração, porque a avaliação de uma função pode ter efeitos colaterais inesperados.  

```cpp
ASSERT ( myFnctn(0)==1 ) // unsafe if myFnctn has side effects  
VERIFY ( myFnctn(0)==1 ) // safe  
```  

 `VERIFY` chama `myFnctn` nas versões de depuração e de liberação, portanto seu uso é aceitável. Contudo, o uso de `VERIFY` impõe a sobrecarga de uma chamada de função desnecessária na versão de liberação.  

 [Neste tópico](#BKMK_In_this_topic)  

##  <a name="BKMK_CRT_assertions"></a> Asserções CRT  
 CRTDBG. Arquivo de cabeçalho de H define a [macros Assert e asserte](/cpp/c-runtime-library/reference/assert-asserte-assert-expr-macros) para verificação de asserção.  


| Macro | Resultado |
|------------| - |
| `_ASSERT` | Se a expressão especificada for avaliada como FALSE, o nome do arquivo e o número de `_ASSERT`. |
| `_ASSERTE` | Mesmo que `_ASSERT`, mais uma representação de cadeia de caracteres de expressão que foi declarada. |

 `_ASSERTE` é mais avançada porque informa a expressão declarada que foi avaliada como FALSE. Isso pode ser suficiente para identificar o problema sem fazer referência ao código-fonte. Porém, a versão de depuração do seu aplicativo conterá uma constante de cadeia de caracteres para cada expressão declarada usando `_ASSERTE`. Se você usar muitas macros `_ASSERTE`, essas expressões de cadeia de caracteres ocuparão uma quantidade significativa de memória. Se isso for um problema, use `_ASSERT` para economizar memória.  

 Quando `_DEBUG` é definido, a macro `_ASSERTE` é definida da seguinte forma:  

```cpp
#define _ASSERTE(expr) \  
   do { \  
      if (!(expr) && (1 == _CrtDbgReport( \  
         _CRT_ASSERT, __FILE__, __LINE__, #expr))) \  
         _CrtDbgBreak(); \  
   } while (0)  
```  

 Se a expressão declarada é avaliada como FALSE, o [crtdbgreport](/cpp/c-runtime-library/reference/crtdbgreport-crtdbgreportw) é chamado para informar a falha de asserção (usando uma caixa de diálogo de mensagem por padrão). Se você escolher **Repita** na caixa de diálogo de mensagem, `_CrtDbgReport` retornará 1 e `_CrtDbgBreak` chamará o depurador com `DebugBreak`.  

### <a name="checking-for-heap-corruption"></a>Verificando a corrupção do heap  
 O exemplo a seguir usa [crtcheckmemory](/cpp/c-runtime-library/reference/crtcheckmemory) para verificar se há corrupção de heap:  

```cpp
_ASSERTE(_CrtCheckMemory());  
```  

### <a name="checking-pointer-validity"></a>Verificando a validade do ponteiro  
 O exemplo a seguir usa [crtisvalidpointer](/cpp/c-runtime-library/reference/crtisvalidpointer) para verificar se um determinado intervalo de memória é válido para leitura ou gravação.  

```cpp
_ASSERTE(_CrtIsValidPointer( address, size, TRUE );  
```  

 O exemplo a seguir usa [crtisvalidheappointer](/cpp/c-runtime-library/reference/crtisvalidheappointer) para verificar se um ponteiro aponta para a memória no heap local (o heap criado e gerenciado por essa instância da biblioteca em tempo de execução C — uma DLL pode ter sua própria instância da biblioteca, e Portanto, seu próprio heap, fora do heap do aplicativo). Essa asserção captura endereços zero ou de fora dos limites, mas também ponteiros para variáveis estáticas, variáveis de pilha e qualquer outra memória não local.  

```cpp
_ASSERTE(_CrtIsValidPointer( myData );  
```  

### <a name="checking-a-memory-block"></a>Verificando um bloco de memória  
 O exemplo a seguir usa [crtismemoryblock](/cpp/c-runtime-library/reference/crtismemoryblock) para verificar se um bloco de memória está no heap local e tem um tipo de bloco válido.  

```cpp
_ASSERTE(_CrtIsMemoryBlock (myData, size, &requestNumber, &filename, &linenumber));  
```  

 [Neste tópico](#BKMK_In_this_topic)  

##  <a name="BKMK_MFC_assertions"></a> Asserções MFC  
 MFC define a [ASSERT](https://msdn.microsoft.com/Library/1e70902d-d58c-4e7b-9f69-2aeb6cbe476c) macro para verificação de asserção. Também define os métodos `MFC ASSERT_VALID` e `CObject::AssertValid` para verificar o estado interno de um objeto derivado de `CObject`.  

 Se o argumento da macro `ASSERT` do MFC for avaliado como zero ou false, a macro interromperá a execução do programa e alerta o usuário; caso contrário, a execução continuará.  

 Quando uma asserção falha, uma caixa de diálogo de mensagem mostra o nome do arquivo de origem e o número da linha da asserção. Se você escolher repetir na caixa de diálogo caixa, uma chamada para [AfxDebugBreak](/cpp/mfc/reference/diagnostic-services#afxdebugbreak) faz com que a execução para interromper o depurador. Nesse ponto, você pode examinar a pilha de chamadas e usar outros recursos do depurador para determinar o motivo da falha de asserção. Se você habilitou [Just-in-time depuração](../debugger/just-in-time-debugging-in-visual-studio.md)e o depurador não estava sendo executado, a caixa de diálogo pode iniciar o depurador.  

 O exemplo a seguir mostra como usar `ASSERT` para verificar o valor de retorno de uma função:  

```cpp
int x = SomeFunc(y);  
ASSERT(x >= 0);   //  Assertion fails if x is negative  
```  

 Você pode usar ASSERT com a [IsKindOf](https://docs.microsoft.com/cpp/mfc/reference/cobject-class#iskindof) função para fornecer verificação de tipo dos argumentos de função:  

```cpp
ASSERT( pObject1->IsKindOf( RUNTIME_CLASS( CPerson ) ) );  
```  

 A macro `ASSERT` não produz nenhum código na versão de liberação. Se você precisar avaliar a expressão na versão de lançamento, use o [VERIFY](https://msdn.microsoft.com/library/s8c29sw2.aspx#verify) macro em vez de ASSERT.  

###  <a name="BKMK_MFC_ASSERT_VALID_and_CObject__AssertValid"></a> MFC ASSERT_VALID e CObject::assertvalid&lt;1}  
 O [CObject:: Assertvalid](https://docs.microsoft.com/cpp/mfc/reference/cobject-class#assertvalid) método fornece verificações de tempo de execução do estado interno de um objeto. Embora não seja necessário substituir `AssertValid` quando você deriva a sua classe de `CObject`, é possível tornar sua classe mais confiável fazendo isso. `AssertValid` deve executar asserções em todas as variáveis de membro do objeto para verificar se contêm valores válidos. Por exemplo, ela deve verificar se as variáveis de membro do ponteiro não são NULL.  

 O exemplo a seguir mostra como declarar uma função `AssertValid`:  

```cpp
class CPerson : public CObject  
{  
protected:  
    CString m_strName;  
    float   m_salary;  
public:  
#ifdef _DEBUG  
    // Override  
    virtual void AssertValid() const;  
#endif  
    // ...  
};  
```  

 Quando você substitui `AssertValid`, chame a versão da classe base de `AssertValid` antes de executar suas próprias verificações. Em seguida, use a macro ASSERT para verificar os membros exclusivos da sua classe derivada, como mostrado a seguir:  

```cpp
#ifdef _DEBUG  
void CPerson::AssertValid() const  
{  
    // Call inherited AssertValid first.  
    CObject::AssertValid();  

    // Check CPerson members...  
    // Must have a name.  
    ASSERT( !m_strName.IsEmpty());  
    // Must have an income.  
    ASSERT( m_salary > 0 );  
}  
#endif  
```  

 Se alguma das variáveis de membro armazena objetos, você pode usar a macro `ASSERT_VALID` para testar a validade interna (caso as classes substituam `AssertValid`).  

 Por exemplo, considere uma classe `CMyData`, que armazena uma [CObList](/cpp/mfc/reference/coblist-class) em uma de suas variáveis de membro. A variável `CObList`, `m_DataList`, armazena uma coleção de objetos `CPerson`. Uma declaração abreviada de `CMyData` é semelhante a esta:  

```cpp
class CMyData : public CObject  
{  
    // Constructor and other members ...  
    protected:  
        CObList* m_pDataList;  
    // Other declarations ...  
    public:  
#ifdef _DEBUG  
        // Override:  
        virtual void AssertValid( ) const;  
#endif  
    // And so on ...  
};  
```  

 A substituição de `AssertValid` em `CMyData` é semelhante a esta:  

```cpp
#ifdef _DEBUG  
void CMyData::AssertValid( ) const  
{  
    // Call inherited AssertValid.  
    CObject::AssertValid( );  
    // Check validity of CMyData members.  
    ASSERT_VALID( m_pDataList );  
    // ...  
}  
#endif  
```  

 `CMyData` usa o mecanismo `AssertValid` para testar a validade dos objetos armazenados no membro de dados. A `AssertValid` que substitui `CMyData` invoca a macro `ASSERT_VALID` para sua própria variável de membro m_pDataList.  

 Os testes de validade não interrompem nesse nível porque a classe `CObList` também substitui `AssertValid`. Essa substituição executa testes adicionais de validade do estado interno da lista. Assim, um teste de validade em um objeto `CMyData` resulta em testes adicionais de validade para os estados internos de objetos armazenados na lista `CObList`.  

 Com um pouco mais de trabalho, você pode adicionar teste de validade para os objetos `CPerson` armazenados na lista também. Você pode derivar uma classe `CPersonList` de `CObList` e substituir `AssertValid`. Na substituição, você deve chamar `CObject::AssertValid` e iterar na lista, chamando `AssertValid` em cada objeto `CPerson` armazenado na lista. A classe `CPerson` mostrada no início deste tópico já substitui `AssertValid`.  

 Este é um mecanismo avançado quando você compila para depuração. Quando posteriormente você compila para liberação, o mecanismo é desativado automaticamente.  

###  <a name="BKMK_Limitations_of_AssertValid"></a> Limitações de assertvalid&lt;1}  
 Uma asserção disparada indica que o objeto está incorretamente definido e a execução será parada. No entanto, uma falta de asserção apenas indica que nenhum problema foi encontrado, mas que não há garantia de que o objeto seja bom.  

 [Neste tópico](#BKMK_In_this_topic)  

##  <a name="BKMK_Using_assertions"></a> Usando asserções  

###  <a name="BKMK_Catching_logic_errors"></a> Capturando erros lógicos  
 Você pode definir uma asserção em uma condição que deve ser verdadeira de acordo com a lógica do programa. A asserção não tem nenhum efeito a menos que ocorra um erro lógico.  

 Por exemplo, suponha que você esteja simulando moléculas de gás em um contêiner e que a variável `numMols` representa o número total de moléculas. Esse número não pode ser menor que zero, então você pode incluir uma instrução de declaração de MFC como esta:  

```cpp
ASSERT(numMols >= 0);  
```  

 Ou você pode incluir uma asserção de CRT como esta:  

```cpp
_ASSERT(numMols >= 0);  
```  

 Essas instruções não fazem nada se seu programa está funcionando corretamente. Se um erro lógico fizer com que `numMols` para ser menor que zero, no entanto, a asserção paralisa a execução do seu programa e exibe as [caixa de diálogo de falha de asserção](../debugger/assertion-failed-dialog-box.md).  

 [Neste tópico](#BKMK_In_this_topic)  

###  <a name="BKMK_Checking_results_"></a> Verificando resultados  
 As asserções são valiosas para testar operações cujos resultados não são óbvios em uma inspeção visual rápida.  

 Por exemplo, considere o seguinte código, que atualiza a variável `iMols` com base no conteúdo da lista vinculada apontada por `mols`:  

```cpp
/* This code assumes that type has overloaded the != operator  
 with const char *   
It also assumes that H2O is somewhere in that linked list.   
Otherwise we'll get an access violation... */  
while (mols->type != "H2O")  
{  
 iMols += mols->num;  
 mols = mols->next;  
}  
ASSERT(iMols<=numMols); // MFC version  
_ASSERT(iMols<=numMols); // CRT version  
```  

 O número de moléculas contadas por `iMols` deve ser sempre menor ou igual ao número total de moléculas, `numMols`. A inspeção visual do loop não mostra que esse será necessariamente o caso, por isso uma instrução de declaração é usada após o loop para testar a condição.  

 [Neste tópico](#BKMK_In_this_topic)  

###  <a name="BKMK_Testing_error_conditions_"></a> Localizando erros sem tratamento  
 Você pode usar asserções para testar condições de erro em um ponto no seu código onde todos os erros devem ser manipulados. No exemplo a seguir, uma rotina gráfica retorna um código de erro ou zero para êxito.  

```cpp
myErr = myGraphRoutine(a, b);  

/* Code to handle errors and  
   reset myErr if successful */  

ASSERT(!myErr); -- MFC version  
_ASSERT(!myErr); -- CRT version  
```  

 Se o código de tratamento de erros funcionar corretamente, o erro será tratado e `myErr` será redefinido como zero antes que a asserção seja atingida. Se `myErr` possui outro valor, a asserção falhará, o programa será interrompido e a [caixa de diálogo de falha de asserção](../debugger/assertion-failed-dialog-box.md) é exibida.  

 Apesar disso, as instruções de declaração não substituem o código de tratamento de erros. O exemplo a seguir mostra uma instrução de declaração que pode resultar em problemas no código da versão de liberação final:  

```cpp
myErr = myGraphRoutine(a, b);  

/* No Code to handle errors */  

ASSERT(!myErr); // Don't do this!  
_ASSERT(!myErr); // Don't do this, either!  
```  

 Esse código depende da instrução de declaração para tratar a condição de erro. Como resultado, todo código de erro retornado por `myGraphRoutine` não será tratado no código da versão de liberação final.  

 [Neste tópico](#BKMK_In_this_topic)  

## <a name="see-also"></a>Consulte também  
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Depurando código nativo](../debugger/debugging-native-code.md)   
 [Asserções em código gerenciado](../debugger/assertions-in-managed-code.md)
