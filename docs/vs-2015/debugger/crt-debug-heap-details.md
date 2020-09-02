---
title: Detalhes de heap de depuração CRT | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- debug heap, accessing
- heap functions
- _CRTDBG_CHECK_ALWAYS_DF macro
- _CrtMemDumpStatistics function
- debugging [C++], debug heap
- _CRT_BLOCK macro
- DBGINT.H file
- _CrtMemDumpAllObjectsSince function
- _crtBreakAlloc global variable
- _CrtMemState function
- _CLIENT_BLOCK macro
- _FREE_BLOCK block
- _CrtMemBlockHeader function
- heap state reporting functions
- _CRTDBG_ALLOC_MEM_DF macro
- _CrtSetBreakAlloc function
- memory blocks, allocation types on debug heap
- debugging [C++], CRT debug support
- debug heap, tracking heap allocation requests
- memory allocation, debug heap
- _NORMAL_BLOCK block
- crtBreakAlloc global variable
- _CrtDoForAllClientObjects function
- new operator, using debug heap from C++
- _CrtSetDumpClient function
- debugging [CRT], heap-related problems
- debug heap, solving memory allocation problems
- _CrtMemCheckpoint function
- debug builds, linking to debug heap
- _IGNORE_BLOCK block
- _crtDbgFlag function
- client blocks, specifying subtypes
- memory leaks, tracking
- _CrtSetDbgFlag function
- nBlockUse method
- memory leaks, CRT debug library functions
- _CRTDBG_DELAY_FREE_MEM_DF macro
- allocation request numbers
- _CRTDBG_LEAK_CHECK_DF macro
- debug heap
- memory, debugging
- _CrtReportBlockType function
- _CrtDumpMemoryLeaks function
- _CrtCheckMemory function
- debug heap, CRT
- memory blocks, free
- _BLOCK_TYPE macro
- debug heap, memory blocks
- heap allocation, debug
- debugging memory leaks
- _BLOCK_SUBTYPE macro
- debug heap, using from C++
- _CrtMemDifference function
- heap allocation, tracking requests
- debugging [Visual Studio], debug heap
- delete operator, using debug heap from C++
- blocks, types of on the debug heap
- _CRTDBG_CHECK_CRT_DF macro
- debug heap, reporting functions
ms.assetid: bf78ace6-28e4-4a04-97c6-39e0cdd00ba4
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 158aff0f14886ea5d714c35456bf53d5768f57b8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697864"
---
# <a name="crt-debug-heap-details"></a>Detalhes da pilha de depuração CRT
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico fornece um aspecto detalhado na heap de depuração de CRT.  
  
## <a name="contents"></a><a name="BKMK_Contents"></a> Índice  
 [Localizar saturações de buffer com heap de depuração](#BKMK_Find_buffer_overruns_with_debug_heap)  
  
 [Tipos de blocos na heap de depuração](#BKMK_Types_of_blocks_on_the_debug_heap)  
  
 [Verificar a integridade de heap e vazamentos de memória](#BKMK_Check_for_heap_integrity_and_memory_leaks)  
  
 [Configurar heap de depuração](#BKMK_Configure_the_debug_heap)  
  
 [new, delete e _CLIENT_BLOCKs no heap de depuração C++](#BKMK_new__delete__and__CLIENT_BLOCKs_in_the_C___debug_heap)  
  
 [Funções de relatório de estado de heap](#BKMK_Heap_State_Reporting_Functions)  
  
 [Rastrear solicitações de alocação de heap](#BKMK_Track_Heap_Allocation_Requests)  
  
## <a name="find-buffer-overruns-with-debug-heap"></a><a name="BKMK_Find_buffer_overruns_with_debug_heap"></a> Localizar estouros de buffer com heap de depuração  
 Dois dos problemas intratáveis mais comuns que os programadores encontram estão substituindo o final de um buffer alocado e os vazamentos de memória (não liberam alocações depois que não são mais necessários.) O heap de depuração fornece ferramentas avançadas para resolver problemas de alocação de memória desse tipo.  
  
 As versões de depuração de funções heap chamam o padrão ou as versões de base usadas nas compilações da release. Quando você solicita um bloco de memória, o gerenciador da heap de depuração aloca um bloco de memória ligeiramente maior do que o solicitado da heap de base e retorna um ponteiro para sua parte desse bloco. Por exemplo, suponha que seu aplicativo contém a chamada: `malloc( 10 )`. Em uma compilação de versão, o [malloc](https://msdn.microsoft.com/library/144fcee2-be34-4a03-bb7e-ed6d4b99eea0) chamaria a rotina de alocação de heap de base solicitando uma alocação de 10 bytes. Em uma compilação de depuração, no entanto, `malloc` chamaria [_malloc_dbg](https://msdn.microsoft.com/library/c97eca51-140b-4461-8bd2-28965b49ecdb), o que chamaria a rotina de alocação de heap de base solicitando uma alocação de 10 bytes mais aproximadamente 36 bytes de memória adicional. Todos os blocos de memória resultantes no heap de depuração estão conectados em uma única lista vinculada, ordenados de acordo com a data em que foram alocados.  
  
 Memória adicional alocada por rotinas da heap de depuração é usada para informações de contabilidade, para ponteiros que vinculam blocos de memória de depuração juntos, e para buffers pequenos em ambos os lados de seus dados para capturar substituições da região alocada.  
  
 Atualmente, a estrutura de cabeçalho de bloco usada para armazenar informações para contabilidade de heap de depuração são declaradas da seguinte forma no arquivo de cabeçalho DBGINT.H:  
  
```  
typedef struct _CrtMemBlockHeader  
{  
// Pointer to the block allocated just before this one:  
    struct _CrtMemBlockHeader *pBlockHeaderNext;  
// Pointer to the block allocated just after this one:  
    struct _CrtMemBlockHeader *pBlockHeaderPrev;  
    char *szFileName;    // File name  
    int nLine;           // Line number  
    size_t nDataSize;    // Size of user block  
    int nBlockUse;       // Type of block  
    long lRequest;       // Allocation number  
// Buffer just before (lower than) the user's memory:  
    unsigned char gap[nNoMansLandSize];  
} _CrtMemBlockHeader;  
  
/* In an actual memory block in the debug heap,  
 * this structure is followed by:  
 *   unsigned char data[nDataSize];  
 *   unsigned char anotherGap[nNoMansLandSize];  
 */  
```  
  
 Os buffers de `NoMansLand` em ambos os lados da área de dados do usuário do bloco estão atualmente com 4 bytes de tamanho e são preenchidos com um valor conhecido de bytes usado por rotinas de heap de depuração para verificar se os limites do bloco de memória de usuário não foram substituídos. O heap de depuração também preenche novos blocos de memória com um valor conhecido. Se você optar por manter blocos liberados na lista vinculada da heap como explicado abaixo, esses blocos liberados também serão preenchidos com um valor conhecido. Atualmente, os valores reais de bytes são usados como segue:  
  
 NoMansLand (0xFD)  
 Os buffers de “NoMansLand” em ambos os lados de memória usados pelo aplicativo são preenchidos com 0xFD atualmente.  
  
 Blocos liberados (0xDD)  
 Os blocos liberados mantidos não usados na lista vinculada da heap de depuração quando o sinalizador de `_CRTDBG_DELAY_FREE_MEM_DF` for ajustado serão preenchidos com 0xDD atualmente.  
  
 Novos objetos (0xCD)  
 Novos objetos são preenchidos com 0xCD quando são alocados.  
  
 ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop")  
  
 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
## <a name="types-of-blocks-on-the-debug-heap"></a><a name="BKMK_Types_of_blocks_on_the_debug_heap"></a> Tipos de blocos no heap de depuração  
 Cada bloco de memória no heap de depuração é atribuído a um dos cinco tipos de alocação. Esses tipos são controlados e relatados de maneira diferente para fins de relatórios de estado e de detecção de vazamento. Você pode especificar o tipo de bloco atribuindo-o e usando uma chamada direta para uma das funções de alocação do heap de depuração como [_malloc_dbg](https://msdn.microsoft.com/library/c97eca51-140b-4461-8bd2-28965b49ecdb). Os cinco tipos de blocos de memória no heap de depuração (definido no membro de **nBlockUse** da estrutura de **_CrtMemBlockHeader**) são:  
  
 **_NORMAL_BLOCK**  
 Uma chamada para [malloc](https://msdn.microsoft.com/library/144fcee2-be34-4a03-bb7e-ed6d4b99eea0) ou [calloc](https://msdn.microsoft.com/library/17bb79a1-98cf-4096-90cb-1f9365cd6829) cria um bloco Normal. Se pretender usar somente os blocos Normais e não tiver necessidade de blocos Clientes, defina [_CRTDBG_MAP_ALLOC](https://msdn.microsoft.com/library/435242b8-caea-4063-b765-4a608200312b), que fará com que todas as chamadas de alocação de heap sejam mapeadas para os equivalentes de depuração em builds de depuração. Isso permitirá que informações de número de linha e de nome de arquivo sobre cada chamada de alocação sejam armazenadas no cabeçalho de bloco correspondente.  
  
 `_CRT_BLOCK`  
 Os blocos de memória alocados internamente por muitas funções da biblioteca em tempo de execução são marcados como blocos de CRT para que possam ser tratados separadamente. Como resultado, a detecção de escape e outras operações não precisam ser afetadas por eles. Uma alocação nunca deve atribuir, realocar ou liberar qualquer bloco do tipo CRT.  
  
 `_CLIENT_BLOCK`  
 Um aplicativo pode manter um acompanhamento especial de um determinado grupo de alocações para fins de depuração alocando-as como esse tipo de bloco de memória, usando chamadas explícitas para funções de heap de depuração. O MFC, por exemplo, aloca qualquer **CObjects** como blocos de Cliente; outros aplicativos podem manter objetos diferentes de memória em blocos de Cliente. Os subtipos de blocos de cliente também podem ser especificados para maior granularidade de rastreamento. Para especificar subtipos de blocos de cliente, desloque o número à esquerda por 16 bits e `OR` com `_CLIENT_BLOCK`. Por exemplo:  
  
```  
#define MYSUBTYPE 4  
freedbg(pbData, _CLIENT_BLOCK|(MYSUBTYPE<<16));  
```  
  
 Uma função de cliente fornecida pelo cliente para despejar objetos armazenados em blocos de clientes pode ser instalada usando [_CrtSetDumpClient](https://msdn.microsoft.com/library/f3dd06d0-c331-4a12-b68d-25378d112033) e será chamada sempre que um bloco do cliente for despejado por uma função de depuração. Além disso, [_CrtDoForAllClientObjects](https://msdn.microsoft.com/library/d0fdb835-3cdc-45f1-9a21-54208e8df248) pode ser usado para chamar uma função determinada fornecida pelo aplicativo para cada bloco de cliente no heap de depuração.  
  
 **_FREE_BLOCK**  
 Normalmente, os blocos liberados são removidos da lista. Para verificar se a memória liberada ainda não está sendo gravada ou para simular condições de memória baixa, você optar por manter os blocos liberados na lista vinculada, marcados como livres e preenchidos com um valor conhecido de byte (atualmente 0xDD).  
  
 **_IGNORE_BLOCK**  
 É possível desativar as operações de heap de depuração por um período. Durante este momento, blocos de memória são mantidos na lista, mas marcados como blocos Ignorar.  
  
 Para determinar o tipo e o subtipo de um bloco determinado, use a função [_CrtReportBlockType](https://msdn.microsoft.com/library/0f4b9da7-bebb-4956-9541-b2581640ec6b) e as macros **_BLOCK_TYPE** e **_BLOCK_SUBTYPE**. As macros são definidas (em crtdbg.h), como a seguir:  
  
```  
#define _BLOCK_TYPE(block)          (block & 0xFFFF)  
#define _BLOCK_SUBTYPE(block)       (block >> 16 & 0xFFFF)  
```  
  
 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
## <a name="check-for-heap-integrity-and-memory-leaks"></a><a name="BKMK_Check_for_heap_integrity_and_memory_leaks"></a> Verifique a integridade e vazamentos de memória do heap  
 Vários dos recursos da heap de depuração devem ser acessados de dentro de seu código. A seção a seguir descreve alguns dos recursos e como usá-los.  
  
 `_CrtCheckMemory`  
 Você pode usar uma chamada para [_CrtCheckMemory](https://msdn.microsoft.com/library/457cc72e-60fd-4177-ab5c-6ae26a420765), por exemplo, para verificar a integridade do heap a qualquer momento. Essa função inspeciona cada bloco de memória na heap, verifica se as informações de cabeçalho do bloco de memória são válidas, e confirma que os buffers não foram alterados.  
  
 `_CrtSetDbgFlag`  
 Você pode controlar como o heap de depuração acompanha as alocações usando um sinalizador interno, [_crtDbgFlag](https://msdn.microsoft.com/library/9e7adb47-8ab9-4e19-81d5-e2f237979973), que pode ser lido e definido usando a função [_CrtSetDbgFlag](https://msdn.microsoft.com/library/b5657ffb-6178-4cbf-9886-1af904ede94c). Alterando este sinalizador, você pode instruir o heap de depuração para verificar vazamentos de memória quando o programa encerra e relata todos os vazamentos detectados. Da mesma forma, você pode especificar se blocos de memória liberados não serão removidos da lista vinculada, para simular situações de memória baixa. Quando a heap é verificada, esses blocos liberados são inspecionados em sua totalidade para garantir que não estão perturbados.  
  
 O sinalizador **_crtDbgFlag** contém os seguintes campos de bits:  
  
|Campo de bits|Padrão<br /><br /> value|Descrição|  
|---------------|-----------------------|-----------------|  
|**_CRTDBG_ALLOC_MEM_DF**|Ativado|Ativa a alocação de depuração. Quando esse bit está desativado, as alocações permanecem encadeadas juntas, mas seu tipo de bloco é **_IGNORE_BLOCK**.|  
|**_CRTDBG_DELAY_FREE_MEM_DF**|Desativado|Impede que a memória seja liberada realmente para simular condições de memória baixa. Quando esse bit estiver ativado, os blocos liberados são mantidos na lista vinculada da heap de depuração, mas são marcados como **_FREE_BLOCK** e preenchidos com um valor especial de byte.|  
|**_CRTDBG_CHECK_ALWAYS_DF**|Desativado|Faz com que **_CrtCheckMemory** seja chamado em cada alocação e desalocação. Isso deixa a execução lenta, mas captura os erros rapidamente.|  
|**_CRTDBG_CHECK_CRT_DF**|Desativado|Faz com que blocos marcados como o tipo **_CRT_BLOCK** sejam inclusos em operações de detecção de escape e diferença de estado. Quando esse bit está desativado, a memória usada internamente pela biblioteca em tempo de execução é ignorada durante essas operações.|  
|**_CRTDBG_LEAK_CHECK_DF**|Desativado|Faz com que a verificação de escape seja executada na saída do programa através de uma chamada a **_CrtDumpMemoryLeaks**. Um relatório de erro é gerado se o aplicativo não liberou qualquer memória atribuída.|  
  
 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
## <a name="configure-the-debug-heap"></a><a name="BKMK_Configure_the_debug_heap"></a> Configurar o heap de depuração  
 Todas as chamadas para funções heap, como `malloc`, `free`, `calloc`, `realloc`, `new` e `delete` resolvem depurar versões dessas funções que operam no heap de depuração. Quando você libera um bloco de memória, a heap de depuração verifica automaticamente a integridade dos buffers em ambos os lados de sua área atribuída e emite um relatório de erro case a substituição tenha ocorrido.  
  
 **Para usar a heap de depuração**  
  
- Vincule a compilação de depuração de seu aplicativo a uma versão de depuração da biblioteca em tempo de execução do C.  
  
  **Para alterar um ou mais campos de bits _crtDbgFlag e criar um novo estado para o sinalizador**  
  
1. Chamar `_CrtSetDbgFlag` com o parâmetro `newFlag` definido como `_CRTDBG_REPORT_FLAG` (para obter o estado atual de `_crtDbgFlag`) e armazenar o valor retornado em uma variável temporária.  
  
2. Ative qualquer bit a `OR` -ing (símbolo de &#124; bits) a variável temporária com as bitmasks correspondentes (representadas no código do aplicativo por constantes do manifesto).  
  
3. Desative os outros bits por `AND` -ing (bit & Symbol) da variável com um `NOT` (símbolo bit ~) dos bitmasks apropriados.  
  
4. Chamar `_CrtSetDbgFlag` com o parâmetro de `newFlag` definido como o valor armazenado na variável temporária para criar o novo estado para `_crtDbgFlag`.  
  
   Por exemplo, as seguintes linhas de código ativam detecção automática de escape e desativam a verificação de blocos de tipo `_CRT_BLOCK`:  
  
```  
// Get current flag  
int tmpFlag = _CrtSetDbgFlag( _CRTDBG_REPORT_FLAG );  
  
// Turn on leak-checking bit.  
tmpFlag |= _CRTDBG_LEAK_CHECK_DF;  
  
// Turn off CRT block checking bit.  
tmpFlag &= ~_CRTDBG_CHECK_CRT_DF;  
  
// Set flag to the new value.  
_CrtSetDbgFlag( tmpFlag );  
```  
  
 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
## <a name="new-delete-and-_client_blocks-in-the-c-debug-heap"></a><a name="BKMK_new__delete__and__CLIENT_BLOCKs_in_the_C___debug_heap"></a> novo, excluir e _CLIENT_BLOCKs no heap de depuração do C++  
 As versões de depuração de biblioteca em tempo de execução de C contêm versões de depuração do C++ `new` e operadores de `delete`. Se você usar o tipo de alocação `_CLIENT_BLOCK`, deverá chamar a versão de depuração do operador `new` diretamente ou criar macros que substituam o operador `new` no modo de depuração, como mostrado no exemplo a seguir:  
  
```  
/* MyDbgNew.h  
 Defines global operator new to allocate from  
 client blocks  
*/  
  
#ifdef _DEBUG  
   #define DEBUG_CLIENTBLOCK   new( _CLIENT_BLOCK, __FILE__, __LINE__)  
#else  
   #define DEBUG_CLIENTBLOCK  
#endif // _DEBUG  
  
/* MyApp.cpp  
        Use a default workspace for a Console Application to  
 *      build a Debug version of this code  
*/  
  
#include "crtdbg.h"  
#include "mydbgnew.h"  
  
#ifdef _DEBUG  
#define new DEBUG_CLIENTBLOCK  
#endif  
  
int main( )   {  
    char *p1;  
    p1 =  new char[40];  
    _CrtMemDumpAllObjectsSince( NULL );  
}  
```  
  
 A versão de depuração do operador `delete` funciona com todos os tipos de bloco e não requer nenhuma alteração em seu programa quando você compilar uma versão de lançamento.  
  
 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
## <a name="heap-state-reporting-functions"></a><a name="BKMK_Heap_State_Reporting_Functions"></a> Funções de relatório de estado de heap  
 **_CrtMemState**  
  
 Para capturar um instantâneo de resumo do estado da heap em um determinado momento, use a estrutura _CrtMemState definida em CRTDBG.H:  
  
```  
typedef struct _CrtMemState  
{  
    // Pointer to the most recently allocated block:  
    struct _CrtMemBlockHeader * pBlockHeader;  
    // A counter for each of the 5 types of block:  
    size_t lCounts[_MAX_BLOCKS];  
    // Total bytes allocated in each block type:  
    size_t lSizes[_MAX_BLOCKS];  
    // The most bytes allocated at a time up to now:  
    size_t lHighWaterCount;  
    // The total bytes allocated at present:  
    size_t lTotalCount;  
} _CrtMemState;  
```  
  
 Essa estrutura salva um ponteiro para o primeiro bloco (recentemente atribuído) na lista vinculada da heap de depuração. Em seguida, em duas matrizes, ele registra quanto de cada tipo de bloco de memória (_NORMAL_BLOCK, `_CLIENT_BLOCK`, _FREE_BLOCK, e assim por diante) está na lista e o número de bytes atribuídos em cada tipo de bloco. Finalmente, registra o maior número de bytes atribuídos no heap como um todo até esse ponto, e o número de bytes atribuídos no momento.  
  
 **Outras Funções de Relatório do CRT**  
  
 As funções a seguir informam o estado e o conteúdo da heap e usam as informações para ajudar a detectar vazamentos de memória e outros problemas.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[_CrtMemCheckpoint](https://msdn.microsoft.com/library/f1bacbaa-5a0c-498a-ac7a-b6131d83dfbc)|Salva um instantâneo da heap em uma estrutura de **_CrtMemState** fornecida pelo aplicativo.|  
|[_CrtMemDifference](https://msdn.microsoft.com/library/0f327278-b551-482f-958b-76941f796ba4)|Compara duas estruturas de estado de memória, salva a diferença entre elas em uma estrutura de estado e retorna VERDADEIRO se os dois estados forem diferentes.|  
|[_CrtMemDumpStatistics](https://msdn.microsoft.com/library/27b9d731-3184-4a2d-b9a7-6566ab28a9fe)|Despeja uma determinada estrutura **_CrtMemState**. A estrutura pode conter um instantâneo de estado da heap de depuração em um determinado momento ou a diferença entre os dois instantâneos.|  
|[_CrtMemDumpAllObjectsSince](https://msdn.microsoft.com/library/c48a447a-e6bb-475c-9271-a3021182a0dc)|Despeja informações sobre todos os objetos atribuídos como um instantâneo determinado extraído do heap do início de execução. Cada vez que despeja um bloco **_CLIENT_BLOCK**, uma função de hook fornecida pelo aplicativo é chamada se instalada usando **_CrtSetDumpClient**.|  
|[_CrtDumpMemoryLeaks](https://msdn.microsoft.com/library/71b2eab4-7f55-44e8-a55a-bfea4f32d34c)|Determina se qualquer vazamento de memória ocorreu desde o início da execução do programa e, em caso afirmativo, despeja todos os objetos atribuídos. Cada vez que **_CrtDumpMemoryLeaks** despeja um bloco **_CLIENT_BLOCK**, uma função de hook fornecida pelo aplicativo é chamada se instalada usando **_CrtSetDumpClient**.|  
  
 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
## <a name="track-heap-allocation-requests"></a><a name="BKMK_Track_Heap_Allocation_Requests"></a> Solicitações de alocação da heap de rastreamento  
 Apesar de localizar o nome do arquivo de origem e o número da linha, no qual uma declaração ou uma macro de relatório executa, é geralmente muito útil localizar a causa de um problema, provavelmente o mesmo não é verdade para funções de alocação do heap. Quando macros podem ser inseridas em vários pontos apropriados na árvore de lógica de um aplicativo, uma alocação geralmente é ocultada em uma rotina especial que é chamada de vários locais diferentes em muitas vezes diferentes. A pergunta geralmente não é qual linha de código fez uma alocação incorreta, mas qual das milhares de alocações feitas por essa linha de código está incorreta e porque.  
  
 **Números de solicitação de alocação exclusiva e _crtBreakAlloc**  
  
 A maneira mais simples de identificar a chamada específica de alocação da heap que não foi bem-sucedida é aproveitar o número exclusivo de solicitação de alocação associado com cada bloco na heap de depuração. Quando as informações sobre um bloco são relatadas por uma das funções de despejo, esse número de solicitação de alocação é colocado entre chaves (por exemplo, "{36}").  
  
 Depois que souber o número de solicitação de alocação de um bloco alocado inadequado, você pode passar este número para [_CrtSetBreakAlloc](https://msdn.microsoft.com/library/33bfc6af-a9ea-405b-a29f-1c2d4d9880a1) para criar um ponto de interrupção. A execução será interrompida logo após a alocação do bloco, e é possível voltar de modo a determinar que rotina foi responsável pela chamada incorreta. Para evitar recompilar, é possível fazer a mesma coisa no depurador definindo **_crtBreakAlloc** para o número de solicitação de alocação que você está interessado.  
  
 **Criando versões de depuração de suas rotinas de alocação**  
  
 Uma abordagem um pouco mais complicada é criar versões de depuração com base em suas próprias rotinas de alocação, comparáveis às versões de **_dbg** de [funções de alocação de heap](../debugger/debug-versions-of-heap-allocation-functions.md). Você pode passar o arquivo de origem e os argumentos do número da linha para as rotinas de alocação do heap e você, e você poderá imediatamente ver onde uma alocação incorreta foi originada.  
  
 Por exemplo, suponha que seu aplicativo contém uma rotina usada com frequência semelhante à seguinte:  
  
```  
int addNewRecord(struct RecStruct * prevRecord,  
                 int recType, int recAccess)  
{  
    // ...code omitted through actual allocation...   
    if ((newRec = malloc(recSize)) == NULL)  
    // ... rest of routine omitted too ...   
}  
```  
  
 Em um arquivo de cabeçalho, você poderia adicionar código como o seguinte:  
  
```  
#ifdef _DEBUG  
#define  addNewRecord(p, t, a) \  
            addNewRecord(p, t, a, __FILE__, __LINE__)  
#endif  
```  
  
 Em seguida, você pode alterar a alocação em sua rotina de criação de registro como a seguir:  
  
```  
int addNewRecord(struct RecStruct *prevRecord,  
                int recType, int recAccess  
#ifdef _DEBUG  
               , const char *srcFile, int srcLine  
#endif  
    )  
{  
    /* ... code omitted through actual allocation ... */  
    if ((newRec = _malloc_dbg(recSize, _NORMAL_BLOCK,  
            srcFile, scrLine)) == NULL)  
    /* ... rest of routine omitted too ... */  
}  
```  
  
 Agora o nome do arquivo de origem e o número da linha onde `addNewRecord` foi chamado serão armazenados em cada bloco resultante atribuído no heap de depuração e relatados quando esse bloco é examinado.  
  
 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
## <a name="see-also"></a>Consulte Também  
 [Depurando código nativo](../debugger/debugging-native-code.md)
