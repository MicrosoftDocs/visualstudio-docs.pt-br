---
title: Encontrar vazamentos de memória com a biblioteca CRT | Microsoft Docs
ms.date: 10/04/2018
ms.topic: how-to
dev_langs:
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5deb42b2ab708bae572aebbcac15af2d077b14fa
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350479"
---
# <a name="find-memory-leaks-with-the-crt-library"></a>Localizar vazamentos de memória com a biblioteca CRT

Vazamentos de memória estão entre os bugs mais sutis e difíceis de detectar em aplicativos C/C++. Vazamentos de memória resultam da falha para desalocar corretamente a memória que foi alocada anteriormente. Um pequeno vazamento de memória não pode ser notado a princípio, mas com o tempo pode causar sintomas variando de baixo desempenho para falhar quando o aplicativo ficar sem memória. Um aplicativo de vazamento que usa toda a memória disponível pode fazer com que outros aplicativos falhem, criando confusão sobre qual aplicativo é responsável. Até mesmo vazamentos de memória inofensivas podem indicar outros problemas que devem ser corrigidos.

O [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] depurador e a biblioteca de tempo de execução do C (CRT) podem ajudá-lo a detectar e identificar vazamentos de memória.

## <a name="enable-memory-leak-detection"></a>Habilitar detecção de vazamento de memória

As principais ferramentas para detectar vazamentos de memória são o depurador do C/C++ e as funções de heap de depuração da biblioteca de tempo de execução do C (CRT).

Para habilitar todas as funções de heap de depuração, inclua as seguintes instruções em seu programa C++, na seguinte ordem:

```cpp
#define _CRTDBG_MAP_ALLOC
#include <stdlib.h>
#include <crtdbg.h>
```

A declaração de `#define` mapeia uma versão de base de funções heap de CRT para a versão de depuração correspondente. Se você sair da `#define` instrução, o despejo de vazamento de memória será [menos detalhado](#interpret-the-memory-leak-report).

Incluir *CRTDBG. h* mapeia as `malloc` `free` funções e para suas versões de depuração, [_malloc_dbg](/cpp/c-runtime-library/reference/malloc-dbg) e [_free_dbg](/cpp/c-runtime-library/reference/free-dbg), que rastreiam a alocação e a desalocação da memória. Esse mapeamento ocorre apenas em compilações de depuração, que tem `_DEBUG`. Compilações lançadas usam as funções `malloc` e `free`.

Depois de habilitar as funções de heap de depuração usando as instruções anteriores, faça uma chamada para [_CrtDumpMemoryLeaks](/cpp/c-runtime-library/reference/crtdumpmemoryleaks) antes de um ponto de saída do aplicativo exibir um relatório de vazamento de memória quando o aplicativo for encerrado.

```cpp
_CrtDumpMemoryLeaks();
```

Se seu aplicativo tiver várias saídas, você não precisará colocá-las manualmente `_CrtDumpMemoryLeaks` em todos os pontos de saída. Para fazer uma chamada automática para `_CrtDumpMemoryLeaks` em cada ponto de saída, faça uma chamada para `_CrtSetDbgFlag` no início do seu aplicativo com os campos de bits mostrados aqui:

```cpp
_CrtSetDbgFlag ( _CRTDBG_ALLOC_MEM_DF | _CRTDBG_LEAK_CHECK_DF );
```

Por padrão, a saída `_CrtDumpMemoryLeaks` emite o relatório de vazamento de memória para o painel **Depurar** da janela de **Saída**. Se você usar uma biblioteca, a biblioteca poderá redefinir a saída para outro local.

Você pode usar `_CrtSetReportMode` o para redirecionar o relatório para outro local ou voltar para a janela de **saída** , conforme mostrado aqui:

```cpp
_CrtSetReportMode( _CRT_WARN, _CRTDBG_MODE_DEBUG );
```

## <a name="interpret-the-memory-leak-report"></a>Interpretar o relatório de vazamento de memória

Se seu aplicativo não definir `_CRTDBG_MAP_ALLOC` , [_CrtDumpMemoryLeaks](/cpp/c-runtime-library/reference/crtdumpmemoryleaks) exibirá um relatório de vazamento de memória parecido com o seguinte:

```cmd
Detected memory leaks!
Dumping objects ->
{18} normal block at 0x00780E80, 64 bytes long.
 Data: <                > CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD
Object dump complete.
```

Se seu aplicativo definir `_CRTDBG_MAP_ALLOC` , o relatório de vazamento de memória será semelhante a:

```cmd
Detected memory leaks!
Dumping objects ->
c:\users\username\documents\projects\leaktest\leaktest.cpp(20) : {18}
normal block at 0x00780E80, 64 bytes long.
 Data: <                > CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD
Object dump complete.
```

O segundo relatório mostra o nome do arquivo e o número da linha em que a memória vazada é alocada pela primeira vez.

Independentemente de você definir `_CRTDBG_MAP_ALLOC` , o relatório de vazamento de memória exibe:

- O número de alocação de memória, que está `18` no exemplo
- O tipo de bloco, `normal` no exemplo.
- O local da memória hexadecimal, `0x00780E80` no exemplo.
- O tamanho do bloco, `64 bytes` no exemplo.
- Os primeiros 16 bytes de dados no bloco, no formulário hexadecimal.

Os tipos de bloco de memória são *normal*, *cliente*ou *CRT*. Um *bloco normal* é a memória comum atribuída pelo seu programa. Um *bloco de cliente* é um tipo especial de bloco de memória usado por programas MFC para os objetos que exigem um destruidor. O operador MFC `new` cria um bloco normal ou um bloco de cliente, como apropriado para o objeto que estiver sendo criado.

Um *bloco de CRT* é atribuído pela biblioteca de CRT para seu próprio uso. A biblioteca CRT manipula a desalocação desses blocos, de modo que blocos CRT não aparecerão no relatório de vazamento de memória, a menos que haja problemas sérios com a biblioteca CRT.

Há dois tipos de outros blocos de memória que nunca aparecem nos relatórios de escape de memória. Um *bloco gratuito* é a memória que foi liberada, portanto, por definição não é vazado. Um *bloco de ignorar* é a memória que você marcou explicitamente para excluir do relatório de vazamento de memória.

As técnicas anteriores identificam vazamentos de memória para a memória alocada usando a função CRT padrão `malloc` . No entanto, se o seu programa alocar memória usando o operador C++, `new` você só poderá ver o nome do arquivo e o número da linha em que as `operator new` chamadas `_malloc_dbg` no relatório de vazamento de memória. Para criar um relatório de vazamento de memória mais útil, você pode escrever uma macro como a seguinte para relatar a linha que fez a alocação:

```cpp
#ifdef _DEBUG
    #define DBG_NEW new ( _NORMAL_BLOCK , __FILE__ , __LINE__ )
    // Replace _NORMAL_BLOCK with _CLIENT_BLOCK if you want the
    // allocations to be of _CLIENT_BLOCK type
#else
    #define DBG_NEW new
#endif
```

Agora você pode substituir o `new` operador usando a `DBG_NEW` macro em seu código. Em compilações de depuração, `DBG_NEW` o usa uma sobrecarga de global `operator new` que usa parâmetros adicionais para o tipo de bloco, o arquivo e o número de linha. A sobrecarga de `new` chamadas `_malloc_dbg` para registrar as informações extras. Os relatórios de vazamento de memória mostram o nome de arquivo e o número de linha onde os objetos vazados foram alocados. As compilações de versão ainda usam o padrão `new` . Aqui está um exemplo da técnica:

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

Quando você executa esse código no depurador do Visual Studio, a chamada para `_CrtDumpMemoryLeaks` gera um relatório na janela de **saída** que é semelhante a:

```Output
Detected memory leaks!
Dumping objects ->
c:\users\username\documents\projects\debug_new\debug_new.cpp(20) : {75}
 normal block at 0x0098B8C8, 4 bytes long.
 Data: <    > CD CD CD CD
Object dump complete.
```

Essa saída relata que a alocação vazada estava na linha 20 de *DEBUG_NEW. cpp*.

>[!NOTE]
>Não recomendamos que você crie uma macro de pré-processador chamada `new` ou qualquer outra palavra-chave de linguagem.

## <a name="set-breakpoints-on-a-memory-allocation-number"></a>Definir pontos de interrupção em um número de alocação de memória

O número de alocação de memória informa quando um bloco de memória vazado tiver sido atribuído. Um bloco com um número de alocação de memória de 18, por exemplo, é o bloco de memória 18 alocado durante a execução do aplicativo. O relatório CRT conta todas as alocações de bloco de memória durante a execução, incluindo as alocações da biblioteca CRT e outras bibliotecas, como MFC. Portanto, o número de blocos de alocação de memória 18 provavelmente não é o bloco de memória de 18 alocado pelo seu código.

Você pode usar o número de alocação para definir um ponto de interrupção na alocação da memória.

**Para definir um ponto de interrupção de alocação de memória usando a janela Inspeção:**

1. Defina um ponto de interrupção próximo ao início do seu aplicativo e inicie a depuração.

1. Quando o aplicativo pausa no ponto de interrupção, abra uma janela de **inspeção** selecionando **depurar**  >  **Windows**  >  **Watch 1** ( **ou assista 2**, **Watch 3**ou **Watch 4**).

1. Na janela **inspecionar** , digite `_crtBreakAlloc` a coluna **nome** .

   Se você estiver usando a versão de DLL multi-threaded da biblioteca CRT (a opção/MD), adicione o operador de contexto:`{,,ucrtbased.dll}_crtBreakAlloc`
   
   Verifique se os símbolos de depuração estão carregados. Caso contrário, `_crtBreakAlloc` será relatado como não *identificado*.

1. Pressione **Enter**.

   O depurador avalia a chamada e coloca o resultado na coluna de **Valor**. Esse valor será **-1** se você não definir nenhum ponto de interrupção nas alocações de memória.

1. Na coluna **valor** , substitua o valor pelo número de alocação da alocação de memória em que você deseja interromper o depurador.

Depois de definir um ponto de interrupção em um número de alocação de memória, continue a depuração. Certifique-se de executar sob as mesmas condições, portanto, o número de alocação de memória não é alterado. Quando o programa for interrompido na alocação de memória especificada, use a janela **pilha de chamadas** e outras janelas do depurador para determinar as condições sob as quais a memória foi alocada. Em seguida, você pode continuar a execução para observar o que acontece com o objeto e determinar por que ele não está desalocado corretamente.

Definindo um ponto de interrupção de dados no objeto também pode ser útil. Para obter mais informações, consulte [usando pontos de interrupção](../debugger/using-breakpoints.md).

Você também pode definir pontos de interrupção de alocação de memória no código. É possível definir:

```cpp
_crtBreakAlloc = 18;
```

 ou:

```cpp
_CrtSetBreakAlloc(18);
```

## <a name="compare-memory-states"></a>Comparar Estados de memória

Outra técnica para localizar vazamentos de memória envolve pegar instantâneos do estado da memória do aplicativo em pontos-chave. Para tirar um instantâneo do estado da memória em um determinado ponto em seu aplicativo, crie uma `_CrtMemState` estrutura e passe-a para a `_CrtMemCheckpoint` função.

```cpp
_CrtMemState s1;
_CrtMemCheckpoint( &s1 );
```

A `_CrtMemCheckpoint` função preenche a estrutura com um instantâneo do estado da memória atual.

Para gerar o conteúdo de uma `_CrtMemState` estrutura, passe a estrutura para a `_ CrtMemDumpStatistics` função:

```cpp
_CrtMemDumpStatistics( &s1 );
```

`_ CrtMemDumpStatistics`gera um despejo de estado de memória semelhante a:

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

`_CrtMemDifference`compara os Estados de memória `s1` e `s2` retorna um resultado em ( `s3` ) que é a diferença entre `s1` e `s2` .

Uma técnica para localizar vazamentos de memória começa colocando `_CrtMemCheckpoint` chamadas no início e no final do seu aplicativo e, em seguida, usando `_CrtMemDifference` para comparar os resultados. Se `_CrtMemDifference` o mostrar um vazamento de memória, você poderá adicionar mais `_CrtMemCheckpoint` chamadas para dividir seu programa usando uma pesquisa binária, até isolar a origem do vazamento.

## <a name="false-positives"></a>Falsos positivos

 `_CrtDumpMemoryLeaks`pode fornecer indicações falsas de vazamentos de memória se uma biblioteca marcar alocações internas como blocos normais em vez de blocos CRT ou blocos de cliente. Nesse caso, `_CrtDumpMemoryLeaks` não é capaz de reconhecer a diferença entre alocações de usuário e alocações internas de biblioteca. Se os destruidores globais das alocações de biblioteca forem executados após o ponto onde você chama `_CrtDumpMemoryLeaks`, cada alocação interna da biblioteca será relatada como um vazamento de memória. As versões da biblioteca de modelos padrão anteriores ao Visual Studio .NET podem fazer com que o `_CrtDumpMemoryLeaks` relate esses falsos positivos.

## <a name="see-also"></a>Veja também

- [Detalhes de heap de depuração CRT](../debugger/crt-debug-heap-details.md)
- [Segurança do depurador](../debugger/debugger-security.md)
- [Depuração de código nativo](../debugger/debugging-native-code.md)
