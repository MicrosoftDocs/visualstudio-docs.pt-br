---
title: Localizar vazamentos de memória com a biblioteca CRT | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- breakpoints, on memory allocation
- _CrtMemState
- _CrtMemCheckpoint
- memory leaks
- _CrtMemDifference
- memory leaks, detecting and isolating
- _CrtDumpMemoryLeaks
- _CrtSetBreakAlloc
- _crtBreakAlloc
- _CrtSetReportMode
- memory, debugging
- _CrtMemDumpStatistics
- debugging memory leaks
- _CRTDBG_MAP_ALLOC
- _CrtSetDbgFlag
ms.assetid: cf6dc7a6-cd12-4283-b1b6-ea53915f7ed1
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3b797e8c8068523b4c782c4d7f02a3853c1d37d1
ms.sourcegitcommit: 12d6398c02e818de4fbcb4371bae9e5db6cf9509
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050099"
---
# <a name="find-memory-leaks-with-the-crt-library"></a>Localizar vazamentos de memória com a biblioteca CRT

Vazamentos de memória estão entre a maioria dos bugs sutis e difíceis de detectar aplicativos em C/C++. Resultado da falha em desalocar corretamente a memória que foi alocada anteriormente vazamentos de memória. Um pequeno vazamento de memória pode não ser observado no início, mas ao longo do tempo pode causar os sintomas que variam de baixo desempenho a falhar quando o aplicativo é executado sem memória. Um aplicativo de vazamento que usa toda a memória disponível pode fazer com que outros aplicativos falhasse, criando a confusão sobre o qual aplicativo é responsável. Vazamentos de memória até mesmo inofensiva podem indicar outros problemas que devem ser corrigidos.  

 O [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] depurador e a biblioteca de tempo de execução C (CRT) podem ajudá-lo a detectar e identificar vazamentos de memória.  

## <a name="enable-memory-leak-detection"></a>Habilitar a detecção de vazamento de memória  

As principais ferramentas para detectar vazamentos de memória são o depurador de C/C++ e a biblioteca de tempo de execução C (CRT) depurar funções de heap.  

Para habilitar todas as funções de heap de depuração, inclua as seguintes instruções em seu programa de C++, na seguinte ordem:  

```cpp
#define _CRTDBG_MAP_ALLOC  
#include <stdlib.h>  
#include <crtdbg.h>  
```  

A declaração de `#define` mapeia uma versão de base de funções heap de CRT para a versão de depuração correspondente. Se você deixar o `#define` instrução, o despejo de vazamento de memória será [menos detalhados](#interpret-the-memory-leak-report).  

Incluindo *crtdbg. h* mapeia o `malloc` e `free` funções para suas versões de depuração [malloc_dbg](/cpp/c-runtime-library/reference/malloc-dbg) e [free_dbg](/cpp/c-runtime-library/reference/free-dbg), quais rastrear memória alocação e desalocação. Esse mapeamento ocorre apenas em compilações de depuração, que tem `_DEBUG`. Compilações lançadas usam as funções `malloc` e `free`.  

Depois de habilitar as funções de heap de depuração usando as instruções anteriores, fazer uma chamada para [crtdumpmemoryleaks](/cpp/c-runtime-library/reference/crtdumpmemoryleaks) antes de um ponto de saída do aplicativo para exibir um relatório de vazamento de memória quando o aplicativo é encerrado.  

```cpp
_CrtDumpMemoryLeaks();  
```  

Se seu aplicativo tiver várias saídas, você não precisa inserir manualmente o `_CrtDumpMemoryLeaks` em cada ponto de saída. Para fazer com que uma chamada automática para `_CrtDumpMemoryLeaks` em cada ponto de saída, fazer uma chamada para `_CrtSetDbgFlag` no início do seu aplicativo com os campos de bits mostrados aqui:

```cpp
_CrtSetDbgFlag ( _CRTDBG_ALLOC_MEM_DF | _CRTDBG_LEAK_CHECK_DF );  
```  

Por padrão, `_CrtDumpMemoryLeaks` gera o relatório de vazamento de memória para o **Debug** painel da **saída** janela. Se você usar uma biblioteca, a biblioteca poderá redefinir a saída para outro local. 

Você pode usar `_CrtSetReportMode` para redirecionar o relatório para outro local ou de volta para o **saída** janela, conforme mostrado aqui:  

```cpp
_CrtSetReportMode( _CRT_ERROR, _CRTDBG_MODE_DEBUG );  
```  

## <a name="interpret-the-memory-leak-report"></a>Interpretar o relatório de vazamento de memória  

Se seu aplicativo não definir `_CRTDBG_MAP_ALLOC`, [crtdumpmemoryleaks](/cpp/c-runtime-library/reference/crtdumpmemoryleaks) exibe um relatório de vazamento de memória que se parece com:  

```cmd
Detected memory leaks!  
Dumping objects ->  
{18} normal block at 0x00780E80, 64 bytes long.  
 Data: <                > CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD  
Object dump complete.  
```  

Se seu aplicativo definir `_CRTDBG_MAP_ALLOC`, o relatório de vazamento de memória se parece com:  

```cmd
Detected memory leaks!  
Dumping objects ->  
c:\users\username\documents\projects\leaktest\leaktest.cpp(20) : {18}   
normal block at 0x00780E80, 64 bytes long.  
 Data: <                > CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD  
Object dump complete.  
```  

O segundo relatório mostra o nome de arquivo e número de linha em que a memória vazada é atribuída primeiro.  

Se você definir `_CRTDBG_MAP_ALLOC`, exibe o relatório de vazamento de memória:  

- O número de alocação de memória, que é `18` no exemplo  
- O tipo de bloco, `normal` no exemplo.  
- O local da memória hexadecimal, `0x00780E80` no exemplo.  
- O tamanho do bloco, `64 bytes` no exemplo.  
- Os primeiros 16 bytes de dados no bloco, no formulário hexadecimal.  

Tipos de bloco de memória são *normal*, *cliente*, ou *CRT*. Um *bloco normal* é a memória comum atribuída pelo seu programa. Um *bloco de cliente* é um tipo especial de bloco de memória usado por programas MFC para objetos que exigem um destruidor. O operador MFC `new` cria um bloco normal ou um bloco de cliente, como apropriado para o objeto que estiver sendo criado. 

Um *bloco de CRT* é alocado pela biblioteca de CRT para seu próprio uso. A biblioteca de CRT trata a desalocação desses blocos, para que os blocos de CRT não aparecerão no relatório de vazamento de memória, a menos que haja problemas sérios com a biblioteca de CRT.  

Há dois tipos de outros blocos de memória que nunca aparecem nos relatórios de escape de memória. Um *bloco livre* é a memória que foi liberada, portanto, por definição, não é perdido. Uma *bloco ignorar* é a memória que você marcou explicitamente para excluir do relatório de vazamento de memória.  

As técnicas anteriores identificam vazamentos de memória para a memória alocada usando o CRT padrão `malloc` função. Se seu programa aloca memória usando o C++ `new` operador, no entanto, você pode ver apenas o nome de arquivo e número de linha em que `operator new` chamadas `_malloc_dbg` no relatório de vazamento de memória. Para criar um relatório de vazamento de memória mais útil, você pode escrever uma macro semelhante ao seguinte para a linha que fez a alocação de relatório: 

```cpp  
#ifdef _DEBUG
    #define DBG_NEW new ( _NORMAL_BLOCK , __FILE__ , __LINE__ )
    // Replace _NORMAL_BLOCK with _CLIENT_BLOCK if you want the
    // allocations to be of _CLIENT_BLOCK type
#else
    #define DBG_NEW new
#endif
```  

Agora você pode substituir a `new` operador, usando o `DBG_NEW` macro em seu código. Em compilações de depuração `DBG_NEW` usa uma sobrecarga global `operator new` que usa parâmetros adicionais para o tipo de bloco, o arquivo e o número de linha. A sobrecarga de `new` chamadas `_malloc_dbg` para registrar as informações extras. Os relatórios de vazamento de memória mostram o nome de arquivo e número de linha em que os objetos vazados foram alocados. Builds de versão ainda usa o padrão `new`. Aqui está um exemplo da técnica:  

```cpp  
// debug_new.cpp
// compile by using: cl /EHsc /W4 /D_DEBUG /MDd debug_new.cpp
#define _CRTDBG_MAP_ALLOC
#include <cstdlib>
#include <crtdbg.h>

#ifdef _DEBUG
    #define DBG_NEW new ( _NORMAL_BLOCK , __FILE__ , __LINE__ )
    // Replace _NORMAL_BLOCK with _CLIENT_BLOCK if you want the
    // allocations to be of _CLIENT_BLOCK type
#else
    #define DBG_NEW new
#endif

struct Pod {
    int x;
};

void main() {
    Pod* pPod = DBG_NEW Pod;
    pPod = DBG_NEW Pod; // Oops, leaked the original pPod!
    delete pPod;

    _CrtDumpMemoryLeaks();
}
```  

Quando você executa esse código no Visual Studio do depurador, a chamada para `_CrtDumpMemoryLeaks` gera um relatório na **saída** janela semelhante a:  

```Output  
Detected memory leaks!
Dumping objects ->
c:\users\username\documents\projects\debug_new\debug_new.cpp(20) : {75}
 normal block at 0x0098B8C8, 4 bytes long.
 Data: <    > CD CD CD CD 
Object dump complete.
```  

Esta saída de relatórios que a alocação vazada foi na linha 20 *debug_new.cpp*.  

>[!NOTE]
>Não recomendamos que você criar uma macro de pré-processador chamada `new`, ou qualquer outra linguagem palavra-chave. 

## <a name="set-breakpoints-on-a-memory-allocation-number"></a>Definir pontos de interrupção em um número de alocação de memória  

O número de alocação de memória informa quando um bloco de memória vazado tiver sido atribuído. Um bloco com um número de alocação de memória de 18, por exemplo, é o 18º bloco de memória alocada durante a execução do aplicativo. O relatório de CRT conta todas as alocações de bloco de memória durante a execução, incluindo as alocações pela biblioteca de CRT e outras bibliotecas como MFC. Portanto, 18, número de bloco de alocação de memória provavelmente não é o 18º bloco de memória alocado pelo seu código. 

Você pode usar o número de alocação para definir um ponto de interrupção na alocação da memória.  

**Para definir um ponto de interrupção de alocação de memória usando a janela Inspeção:**  

1. Defina um ponto de interrupção no início do seu aplicativo e iniciar a depuração.  
   
1. Quando o aplicativo faz uma pausa no ponto de interrupção, abra uma **Watch** janela selecionando **Debug** > **Windows** > **inspeção 1** (ou **assistir 2**, **assistir 3**, ou **Assista 4**).  
   
1. No **Watch** , digite `_crtBreakAlloc` no **nome** coluna.  
   
   Se você estiver usando a versão com multithread da DLL da biblioteca CRT (a opção /MD), adicione o operador de contexto: `{,,ucrtbased.dll}_crtBreakAlloc`  
   
1. Pressione **ENTER**.  
   
   O depurador avalia a chamada e coloca o resultado na **valor** coluna. Esse valor será **-1** se você não definiu nenhum ponto de interrupção nas alocações de memória.  
   
1. No **valor** coluna, substitua o valor com o número de alocação da alocação de memória em que você deseja que o depurador seja interrompido.  

Depois de definir um ponto de interrupção em um número de alocação de memória, continue a depuração. Certifique-se ser executado com as mesmas condições, para que o número de alocação de memória não muda. Quando o programa interrompe a alocação de memória especificada, use o **pilha de chamadas** janela e outras janelas do depurador para determinar as condições sob as quais a memória foi alocada. Em seguida, você pode continuar a execução para observar o que acontece ao objeto e determinar por que não é deslocado corretamente.  

Definindo um ponto de interrupção de dados no objeto também pode ser útil. Para obter mais informações, consulte [usando pontos de interrupção](../debugger/using-breakpoints.md).  

Você também pode definir pontos de interrupção de alocação de memória no código. Você pode definir:  

```cpp
_crtBreakAlloc = 18;  
```  

 ou:  

```cpp
_CrtSetBreakAlloc(18);  
```  

## <a name="compare-memory-states"></a>Comparar os estados de memória  
 Outra técnica para localizar vazamentos de memória envolve pegar instantâneos do estado da memória do aplicativo em pontos-chave. Para obter um instantâneo do estado de memória em um determinado ponto no seu aplicativo, crie uma `_CrtMemState` estruturar e passá-lo para o `_CrtMemCheckpoint` função. 

```cpp
_CrtMemState s1;  
_CrtMemCheckpoint( &s1 );  
```  

O `_CrtMemCheckpoint` função preenche a estrutura com um instantâneo do estado atual de memória.  

Para exibir o conteúdo de um `_CrtMemState` estrutura, passe a estrutura para o `_ CrtMemDumpStatistics` função:  

```cpp
_CrtMemDumpStatistics( &s1 );  
```  

`_ CrtMemDumpStatistics` gera um despejo do estado de memória que se parece com:  

```cmd
0 bytes in 0 Free Blocks.  
0 bytes in 0 Normal Blocks.  
3071 bytes in 16 CRT Blocks.  
0 bytes in 0 Ignore Blocks.  
0 bytes in 0 Client Blocks.  
Largest number used: 3071 bytes.  
Total allocations: 3764 bytes.  
```  

Para determinar se um vazamento de memória ocorreu em uma seção de código, você pode capturar instantâneos do estado da memória antes e após a seção e, em seguida, usar `_ CrtMemDifference` para comparar os dois estados:  

```cpp
_CrtMemCheckpoint( &s1 );  
// memory allocations take place here  
_CrtMemCheckpoint( &s2 );  

if ( _CrtMemDifference( &s3, &s1, &s2) )  
   _CrtMemDumpStatistics( &s3 );  
```  

`_CrtMemDifference` compara os estados de memória `s1` e `s2` e retorna um resultado em (`s3`) que é a diferença entre `s1` e `s2`.  

Uma técnica para localizar vazamentos de memória começa colocando `_CrtMemCheckpoint` chamadas no início e no final de seu aplicativo, em seguida, usando `_CrtMemDifference` para comparar os resultados. Se `_CrtMemDifference` mostra um vazamento de memória, você pode adicionar mais `_CrtMemCheckpoint` chamadas para dividir seu programa usando uma pesquisa binária, até ter isolado a fonte do vazamento.  

## <a name="false-positives"></a>Falsos positivos  
 `_CrtDumpMemoryLeaks` poderá dar falsas indicações de vazamentos de memória, se uma biblioteca de marca alocações internas como os blocos normais, em vez de blocos de CRT ou blocos de cliente. Nesse caso, `_CrtDumpMemoryLeaks` não é capaz de reconhecer a diferença entre alocações de usuário e alocações internas de biblioteca. Se os destruidores globais das alocações de biblioteca forem executados após o ponto onde você chama `_CrtDumpMemoryLeaks`, cada alocação interna da biblioteca será relatada como um vazamento de memória. Versões da biblioteca padrão do modelo antes que o Visual Studio .NET pode causar `_CrtDumpMemoryLeaks` relatar tais falsos positivos.  

## <a name="see-also"></a>Consulte também  
 [Detalhes do heap de depuração CRT](../debugger/crt-debug-heap-details.md)   
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Depurando código nativo](../debugger/debugging-native-code.md)
