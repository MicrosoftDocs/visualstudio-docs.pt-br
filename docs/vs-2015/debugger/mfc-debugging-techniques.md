---
title: Técnicas de depuração do MFC | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- AfxEnableMemoryTracking
- CMemoryState
- delayFreeMemDF
- checkAlwaysMemDF
- vs.debug.mfc
- vs.debug.objects.dump
- vs.debug.memory.dump
- allocMemDF
- afxMemDF
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- debugging [MFC]
ms.assetid: b154fc31-5e90-4734-8cbd-58dd9fe1f750
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f1e7a1ea69da1cafa38ae2a7bfa4551d3d40a8d4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51745116"
---
# <a name="mfc-debugging-techniques"></a>Técnicas de depuração MFC
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se você estiver depurando um programa MFC, essas técnicas de depuração poderão ser úteis.  
  
##  <a name="BKMK_In_this_topic"></a> Neste tópico  
 [AfxDebugBreak](#BKMK_AfxDebugBreak)  
  
 [A macro TRACE](#BKMK_The_TRACE_macro)  
  
 [Detectando vazamentos de memória no MFC](#BKMK_Memory_leak_detection_in_MFC)  
  
- [Acompanhando alocações de memória](#BKMK_Tracking_memory_allocations)  
  
- [Habilitando o diagnóstico de memória](#BKMK_Enabling_memory_diagnostics)  
  
- [Tirar instantâneos de memória](#BKMK_Taking_memory_snapshots)  
  
- [Exibindo estatísticas de memória](#BKMK_Viewing_memory_statistics)  
  
- [Obtendo despejos de objeto](#BKMK_Taking_object_dumps)  
  
  - [Interpretando despejos de memória](#BKMK_Interpreting_memory_dumps)  
  
  - [Personalizando despejos de objeto](#BKMK_Customizing_object_dumps)  
  
    [Reduzir o tamanho de uma compilação de depuração do MFC](#BKMK_Reducing_the_size_of_an_MFC_Debug_build)  
  
  - [Criando um aplicativo do MFC com informações de depuração para os módulos selecionados](#BKMK_Building_an_MFC_app_with_debug_information_for_selected_modules)  
  
##  <a name="BKMK_AfxDebugBreak"></a> AfxDebugBreak  
 O MFC fornece um especial [AfxDebugBreak](http://msdn.microsoft.com/library/c4cd79b9-9327-4db5-a9d6-c4004a92aa30) função para codificar os pontos de interrupção no código-fonte:  
  
```  
AfxDebugBreak( );  
  
```  
  
 Em plataformas Intel, o `AfxDebugBreak` produz o código a seguir, que é interrompido no código-fonte em vez de no código kernel:  
  
```  
_asm int 3  
```  
  
 Em outras plataformas, o `AfxDebugBreak` simplesmente chama o `DebugBreak`.  
  
 Não se esqueça de remover as instruções `AfxDebugBreak` ao criar uma compilação da versão ou usar as `#ifdef _DEBUG` para delimitá-los.  
  
 [Neste tópico](#BKMK_In_this_topic)  
  
##  <a name="BKMK_The_TRACE_macro"></a> A macro TRACE  
 Para exibir mensagens de seu programa no depurador [janela de saída](../ide/reference/output-window.md), você pode usar o [ATLTRACE](http://msdn.microsoft.com/library/c796baa5-e2b9-4814-a27d-d800590b102e) macro ou o MFC [rastreamento](http://msdn.microsoft.com/library/7b6f42d8-b55a-4bba-ab04-c46251778e6f) macro. Como o [asserções](../debugger/c-cpp-assertions.md), as macros de rastreamento estão ativas somente na versão de depuração do seu programa e desaparecem quando compiladas na versão de lançamento.  
  
 Os exemplos a seguir mostram algumas das maneiras como você pode usar o **rastreamento** macro. Como o `printf`, o **rastreamento** macro pode lidar com um número de argumentos.  
  
```  
int x = 1;  
int y = 16;  
float z = 32.0;  
TRACE( "This is a TRACE statement\n" );  
  
TRACE( "The value of x is %d\n", x );  
  
TRACE( "x = %d and y = %d\n", x, y );  
  
TRACE( "x = %d and y = %x and z = %f\n", x, y, z );  
```  
  
 A macro TRACE trata adequadamente char * e wchar_t\* parâmetros. Os exemplos a seguir demonstram o uso da macro TRACE junto com os diferentes tipos de parâmetros de cadeia de caracteres.  
  
```  
TRACE( "This is a test of the TRACE macro that uses an ANSI string: %s %d\n", "The number is:", 2);  
  
TRACE( L"This is a test of the TRACE macro that uses a UNICODE string: %s %d\n", L"The number is:", 2);  
  
TRACE( _T("This is a test of the TRACE macro that uses a TCHAR string: %s %d\n"), _T("The number is:"), 2);  
  
```  
  
 Para obter mais informações sobre o **rastreamento** macro, consulte [serviços de diagnóstico](http://msdn.microsoft.com/library/8d78454f-9fae-49c2-88c9-d3fabd5393e8).  
  
 [Neste tópico](#BKMK_In_this_topic)  
  
##  <a name="BKMK_Memory_leak_detection_in_MFC"></a> Detectando vazamentos de memória no MFC  
 O MFC fornece classes e funções para detectar a memória alocada, mas nunca desalocada.  
  
###  <a name="BKMK_Tracking_memory_allocations"></a> Acompanhando alocações de memória  
 No MFC, você pode usar a macro [DEBUG_NEW](http://msdn.microsoft.com/library/9b379344-4093-4bec-a3eb-e0d8a63ada9d) em vez da **novos** perdas de operador para ajudar a localizar a memória. Na versão de depuração do programa, o `DEBUG_NEW` controla o nome de arquivo e o número de linha para cada objeto que aloca. Quando você compila uma versão de lançamento do seu programa `DEBUG_NEW` resolve para um simples **nova** operação sem os nome e a linha número informações do arquivo. Dessa forma, você não paga penalidade de velocidade da versão de lançamento do programa.  
  
 Se você não deseja reescrever o programa inteiro para usar `DEBUG_NEW` em vez de **nova**, você pode definir essa macro nos arquivos de origem:  
  
```  
#define new DEBUG_NEW  
```  
  
 Ao fazer uma [despejo de objeto](#BKMK_Taking_object_dumps), cada objeto alocado com `DEBUG_NEW` mostrará o número de arquivo e de linha em que ele foi alocado, permitindo que você localize as fontes de vazamentos de memória.  
  
 A versão de depuração da estrutura MFC usa `DEBUG_NEW` automaticamente, mas seu código não. Se você quiser que os benefícios da `DEBUG_NEW`, você deve usar `DEBUG_NEW` explicitamente ou **#define new** conforme mostrado acima.  
  
 [Neste tópico](#BKMK_In_this_topic)  
  
###  <a name="BKMK_Enabling_memory_diagnostics"></a> Habilitando o diagnóstico de memória  
 Para que você possa usar os recursos de diagnóstico de memória, deverá habilitar o rastreamento de diagnóstico.  
  
 **Para habilitar ou desabilitar o diagnóstico de memória**  
  
- Chame a função global [AfxEnableMemoryTracking](http://msdn.microsoft.com/library/0a40e0c4-855d-46e2-9577-a8f2346f47db) para habilitar ou desabilitar o alocador de diagnóstico de memória. Como o diagnóstico de memória é ativado por padrão na biblioteca de depuração, você normalmente usará essa função para desativá-la temporariamente, o que aumenta a velocidade de execução do programa e reduz a saída de diagnóstico.  
  
  **Para selecionar os recursos de diagnóstico de memória específicos com afxMemDF**  
  
- Se você quiser um controle mais preciso sobre os recursos de diagnóstico de memória, você pode seletivamente ativar recursos de diagnóstico de memória individuais e desativar, definindo o valor da variável global MFC [afxMemDF](http://msdn.microsoft.com/library/cf117501-5446-4fce-81b3-f7194bc95086). Essa variável pode ter os seguintes valores conforme especificado pelo tipo enumerado **afxMemDF**.  
  
  |Valor|Descrição|  
  |-----------|-----------------|  
  |**allocMemDF**|Ativar o alocador de diagnóstico de memória (padrão).|  
  |**delayFreeMemDF**|Atrase a liberação de memória ao chamar `delete` ou até `free` até o programa fechar. Isso fará o programa alocar a quantidade máxima de memória possível.|  
  |**checkAlwaysMemDF**|Chame [AfxCheckMemory](http://msdn.microsoft.com/library/4644da71-7d14-41dc-adc0-ee9558fd7a28) sempre que a memória é alocada ou liberada.|  
  
   Esses valores podem ser usados em combinação executando uma operação OR lógica, como mostrado a seguir:  
  
  ```cpp  
  afxMemDF = allocMemDF | delayFreeMemDF | checkAlwaysMemDF;  
  ```  
  
  [Neste tópico](#BKMK_In_this_topic)  
  
###  <a name="BKMK_Taking_memory_snapshots"></a> Tirar instantâneos de memória  
  
1. Criar uma [CMemoryState](http://msdn.microsoft.com/en-us/8fade6e9-c6fb-4b2a-8565-184a912d26d2) objeto e a chamada a [CMemoryState::Checkpoint](http://msdn.microsoft.com/library/b2d80fea-3d21-457e-816d-b035909bf21a) função de membro. Isso cria o primeiro instantâneo de memória.  
  
2. Depois que seu programa executar as operações de alocação e desalocação de memória, crie outro objeto `CMemoryState` e chame `Checkpoint` para esse objeto. Isso obtém um segundo instantâneo do uso da memória.  
  
3. Crie um terceiro `CMemoryState` objeto e chame seu [CMemoryState::Difference](http://msdn.microsoft.com/library/aba69e2f-71dd-4255-99b5-3da2e56a0c9c) função de membro, fornecendo como argumentos os dois anteriores `CMemoryState` objetos. Se houver uma diferença entre os dois estados da memória, a função `Difference` retornará um valor diferente de zero. Isso indica que alguns blocos de memória não foram desalocados.  
  
    Esse exemplo mostra a aparência deste código:  
  
   ```  
   // Declare the variables needed  
   #ifdef _DEBUG  
       CMemoryState oldMemState, newMemState, diffMemState;  
       oldMemState.Checkpoint();  
   #endif  
  
       // Do your memory allocations and deallocations.  
       CString s("This is a frame variable");  
       // The next object is a heap object.  
      CPerson* p = new CPerson( "Smith", "Alan", "581-0215" );  
  
   #ifdef _DEBUG  
       newMemState.Checkpoint();  
       if( diffMemState.Difference( oldMemState, newMemState ) )  
       {  
           TRACE( "Memory leaked!\n" );  
       }  
   #endif  
   ```  
  
    Observe que as instruções de verificação de memória são envolvidas por `#ifdef` [Debug](http://msdn.microsoft.com/library/a9901568-4846-4731-a404-399d947e2e7a)/ **#endif** blocos para que eles sejam compilados apenas em versões de depuração do seu programa.  
  
    Agora que você sabe que existe um vazamento de memória, você pode usar outra função de membro [CMemoryState::DumpStatistics](http://msdn.microsoft.com/library/90d5f281-b92f-4725-a996-23ab94cf4b5d) que o ajudará a localizá-lo.  
  
   [Neste tópico](#BKMK_In_this_topic)  
  
###  <a name="BKMK_Viewing_memory_statistics"></a> Exibindo estatísticas de memória  
 O [CMemoryState::Difference](http://msdn.microsoft.com/library/aba69e2f-71dd-4255-99b5-3da2e56a0c9c) função examina os dois objetos de estado da memória e detecta todos os objetos não desalocados do heap entre os estados de início e fim. Depois que você tiver tirado instantâneos de memória e comparado-os usando `CMemoryState::Difference`, você pode chamar [CMemoryState::DumpStatistics](http://msdn.microsoft.com/library/90d5f281-b92f-4725-a996-23ab94cf4b5d) para obter informações sobre os objetos que não foram desalocados.  
  
 Considere o exemplo a seguir:  
  
```  
if( diffMemState.Difference( oldMemState, newMemState ) )  
{  
   TRACE( "Memory leaked!\n" );  
   diffMemState.DumpStatistics();  
}  
```  
  
 Um despejo de exemplo tem a seguinte aparência:  
  
```  
0 bytes in 0 Free Blocks  
22 bytes in 1 Object Blocks  
45 bytes in 4 Non-Object Blocks  
Largest number used: 67 bytes  
Total allocations: 67 bytes  
```  
  
 Os blocos livres são os blocos cuja desalocação será atrasada se `afxMemDF` tiver sido definido como `delayFreeMemDF`.  
  
 Os blocos de objeto comuns, mostrados na segunda linha, permanecem alocados no heap.  
  
 Os blocos diferentes de objeto incluem as matrizes e as estruturas alocadas com `new`. Nesse caso, quatro blocos diferentes de objeto foram alocados no heap, mas não desalocados.  
  
 `Largest number used` dá o máximo de memória utilizada pelo programa a qualquer momento.  
  
 `Total allocations` dá a quantidade total de memória usada pelo programa.  
  
 [Neste tópico](#BKMK_In_this_topic)  
  
###  <a name="BKMK_Taking_object_dumps"></a> Obtendo despejos de objeto  
 Em um programa MFC, você pode usar [CMemoryState::DumpAllObjectsSince](http://msdn.microsoft.com/library/a7f89034-bca4-4786-88d5-1571a5425ab2) para despejar uma descrição de todos os objetos no heap que não foram desalocados. `DumpAllObjectsSince` Despeja todos os objetos alocados desde o último [CMemoryState::Checkpoint](http://msdn.microsoft.com/library/b2d80fea-3d21-457e-816d-b035909bf21a). Se nenhuma chamada de `Checkpoint` tiver ocorrido, o `DumpAllObjectsSince` despejará todos os objetos e não objetos atualmente na memória.  
  
> [!NOTE]
>  Antes de usar o despejo de objeto do MFC, você deve [habilitar o rastreamento de diagnóstico](../debugger/mfc-debugging-techniques.md#BKMK_Enabling_Memory_Diagnostics).  
  
> [!NOTE]
>  O MFC despeja automaticamente todos os objetos vazados quando o programa sair, portanto você não precisará criar o código para despejar objetos nesse momento.  
  
 O código a seguir testa um vazamento de memória comparando dois estados de memória e despeja todos os objetos se um vazamento for detectado.  
  
```  
if( diffMemState.Difference( oldMemState, newMemState ) )  
{  
   TRACE( "Memory leaked!\n" );  
   diffMemState.DumpAllObjectsSince();  
}  
```  
  
 O conteúdo do despejo é semelhante ao seguinte:  
  
```  
Dumping objects ->  
  
{5} strcore.cpp(80) : non-object block at $00A7521A, 9 bytes long  
{4} strcore.cpp(80) : non-object block at $00A751F8, 5 bytes long  
{3} strcore.cpp(80) : non-object block at $00A751D6, 6 bytes long  
{2} a CPerson at $51A4  
  
Last Name: Smith  
First Name: Alan  
Phone #: 581-0215  
  
{1} strcore.cpp(80) : non-object block at $00A7516E, 25 bytes long  
```  
  
 Os números entre chaves no início da maioria das linhas especificam a ordem na qual os objetos foram alocados. O objeto alocado mais recentemente tem o número mais alto e aparece no alto do despejo.  
  
 Para obter a quantidade máxima de informações fora de um despejo de objeto, você poderá substituir a função de membro `Dump` de qualquer objeto derivado de `CObject` para personalizar o despejo do objeto.  
  
 Você pode definir um ponto de interrupção em uma alocação de memória específica configurando a variável global `_afxBreakAlloc` com o número mostrado entre chaves. Se você executar novamente o programa, o depurador interromperá a execução quando essa alocação ocorrer. Você pode em seguida analisar a pilha de chamadas para ver como o programa chegou a esse ponto.  
  
 A biblioteca de tempo de execução C tem uma função semelhante, [crtsetbreakalloc](http://msdn.microsoft.com/library/33bfc6af-a9ea-405b-a29f-1c2d4d9880a1), que você pode usar para alocações de tempo de execução C.  
  
 [Neste tópico](#BKMK_In_this_topic)  
  
####  <a name="BKMK_Interpreting_memory_dumps"></a> Interpretando despejos de memória  
 Observe este despejo de objeto com mais detalhes:  
  
```  
{5} strcore.cpp(80) : non-object block at $00A7521A, 9 bytes long  
{4} strcore.cpp(80) : non-object block at $00A751F8, 5 bytes long  
{3} strcore.cpp(80) : non-object block at $00A751D6, 6 bytes long  
{2} a CPerson at $51A4  
  
Last Name: Smith  
First Name: Alan  
Phone #: 581-0215  
  
{1} strcore.cpp(80) : non-object block at $00A7516E, 25 bytes long  
```  
  
 O programa que gerou este despejo tinha apenas duas alocações explícitas- uma na pilha e uma no heap:  
  
```  
// Do your memory allocations and deallocations.  
CString s("This is a frame variable");  
// The next object is a heap object.  
CPerson* p = new CPerson( "Smith", "Alan", "581-0215" );  
```  
  
 O construtor `CPerson` usa três argumentos que são os ponteiros para `char`, que são usados para inicializar variáveis de membro `CString`. No despejo de memória, você pode ver o objeto `CPerson` junto com três blocos diferentes de objeto (3, 4 e 5). Eles mantêm os caracteres para as variáveis de membro `CString` e não serão excluídos quando o destruidor do objeto `CPerson` for invocado.  
  
 O bloco número 2 é o próprio objeto `CPerson`. `$51A4` representa o endereço do bloco e é seguido pelos conteúdos do objeto, que eram gerados pelo `CPerson`::`Dump` quando chamado por [DumpAllObjectsSince](http://msdn.microsoft.com/library/a7f89034-bca4-4786-88d5-1571a5425ab2).  
  
 Você pode determinar a qual bloco o número 1 está associado com a variável de quadro `CString` devido ao número e ao tamanho da sequência, que corresponde ao número de caracteres na variável `CString` do quadro. As variáveis alocadas no quadro são desalocadas automaticamente quando o quadro sai do escopo.  
  
 **Variáveis do quadro**  
  
 Em geral, você não precisa se preocupar com objetos heap associados a variáveis do quadro porque eles são desalocados automaticamente quando as variáveis do quadro saem do escopo. Para evitar a confusão nos despejos de diagnóstico de memória, você deve posicionar suas chamadas para `Checkpoint` de modo que fiquem fora do escopo de variáveis do quadro. Por exemplo, coloque colchetes de escopo em volta do código de alocação anterior, como mostrado a seguir:  
  
```  
oldMemState.Checkpoint();  
{  
    // Do your memory allocations and deallocations ...  
    CString s("This is a frame variable");  
    // The next object is a heap object.  
    CPerson* p = new CPerson( "Smith", "Alan", "581-0215" );  
}  
newMemState.Checkpoint();  
```  
  
 Com os colchetes de escopo no lugar, o despejo de memória para este exemplo ocorre da seguinte maneira:  
  
```  
Dumping objects ->  
  
{5} strcore.cpp(80) : non-object block at $00A7521A, 9 bytes long  
{4} strcore.cpp(80) : non-object block at $00A751F8, 5 bytes long  
{3} strcore.cpp(80) : non-object block at $00A751D6, 6 bytes long  
{2} a CPerson at $51A4  
  
Last Name: Smith  
First Name: Alan  
Phone #: 581-0215  
```  
  
 **Alocações diferentes de objeto**  
  
 Observe que algumas alocações são objetos (como `CPerson`) e algumas são alocações diferentes de objeto. "Alocações diferentes de objeto" são alocações para objetos não derivados de `CObject` ou alocações de tipos C primitivos como `char`, `int`, ou **longo**. Se o **CObject -** classe derivada aloca espaço adicional, como para buffers internos, esses objetos mostrarão as alocações de objeto e diferentes de objeto.  
  
 **Evitando vazamentos de memória**  
  
 Observe no código acima que o bloco de memória associado à variável do quadro `CString` foi desalocado automaticamente e não aparece como um vazamento de memória. A desalocação automática associada a regras de escopo é responsável pela maioria dos vazamentos de memória associados a variáveis do quadro.  
  
 Para os objetos alocados no heap, no entanto, você deve excluir explicitamente o objeto para evitar um vazamento de memória. Para limpar o último vazamento de memória no exemplo anterior, exclua o objeto `CPerson` alocado no heap, da seguinte maneira:  
  
```  
{  
    // Do your memory allocations and deallocations.  
    CString s("This is a frame variable");  
    // The next object is a heap object.  
    CPerson* p = new CPerson( "Smith", "Alan", "581-0215" );  
    delete p;  
}  
```  
  
 [Neste tópico](#BKMK_In_this_topic)  
  
####  <a name="BKMK_Customizing_object_dumps"></a> Personalizando despejos de objeto  
 Quando você deriva uma classe de [CObject](http://msdn.microsoft.com/library/95e9acd3-d9eb-4ac0-b52b-ca4a501a7a3a), você pode substituir o `Dump` a função de membro para fornecer informações adicionais quando você usa [DumpAllObjectsSince](http://msdn.microsoft.com/library/a7f89034-bca4-4786-88d5-1571a5425ab2) para despejar objetos para o [Janela de saída](../ide/reference/output-window.md).  
  
 O `Dump` função grava uma representação textual do membro do objeto variáveis para um contexto de despejo ([CDumpContext](http://msdn.microsoft.com/library/98c52b2d-14b5-48ed-b423-479a4d1c60fa)). O contexto de despejo é semelhante a um fluxo de E/S. Você pode usar o operador de anexação (**<<**) para enviar dados para um `CDumpContext`.  
  
 Quando você substitui a função `Dump`, primeiro deve chamar a versão da classe base do `Dump` para despejar o conteúdo do objeto da classe base. Em seguida, gere uma descrição e um valor textuais para cada variável de membro da sua classe derivada.  
  
 A declaração da função `Dump` é semelhante a esta:  
  
```  
class CPerson : public CObject  
{  
public:  
#ifdef _DEBUG  
    virtual void Dump( CDumpContext& dc ) const;  
#endif  
  
    CString m_firstName;  
    CString m_lastName;  
    // And so on...  
};  
```  
  
 Porque o objeto de despejo só faz sentido quando você estiver depurando seu programa, a declaração do `Dump` função é agrupada com um **#ifdef DEBUG / #endif** bloco.  
  
 No exemplo a seguir, a função `Dump` primeiro chama a função `Dump` para a sua classe base. Em seguida, ela grava uma breve descrição de cada variável de membro junto com o valor do membro no fluxo de diagnóstico.  
  
```  
#ifdef _DEBUG  
void CPerson::Dump( CDumpContext& dc ) const  
{  
    // Call the base class function first.  
    CObject::Dump( dc );  
  
    // Now do the stuff for our specific class.  
    dc << "last name: " << m_lastName << "\n"  
        << "first name: " << m_firstName << "\n";  
}  
#endif  
```  
  
 Você deve fornecer um argumento de `CDumpContext` para especificar para onde a saída de despejo irá. A versão de depuração do MFC fornece um objeto `CDumpContext` predefinido chamado `afxDump` que envia a saída para o depurador.  
  
```  
CPerson* pMyPerson = new CPerson;  
// Set some fields of the CPerson object.  
//...  
// Now dump the contents.  
#ifdef _DEBUG  
pMyPerson->Dump( afxDump );  
#endif  
```  
  
 [Neste tópico](#BKMK_In_this_topic)  
  
##  <a name="BKMK_Reducing_the_size_of_an_MFC_Debug_build"></a> Reduzir o tamanho de uma compilação de depuração do MFC  
 As informações de depuração para um aplicativo MFC grande pode utilizar muito espaço em disco. Você pode usar um destes procedimentos para reduzir o tamanho:  
  
1. Recrie as bibliotecas MFC usando o [/Z7, /Zi, /ZI (formato de informações de depuração)](http://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8) opção, em vez de **/Z7**. Essas opções criam um único arquivo de banco de dados do programa (PDB) que contém informações de depuração para a biblioteca inteira, reduzindo a redundância e economizando espaço.  
  
2. Recrie as bibliotecas MFC sem informações de depuração (nenhuma [/Z7, /Zi, /ZI (formato de informações de depuração)](http://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8) opção). Nesse caso, a falta de informações de depuração impedirão que você use a maioria dos recursos do depurador no código da biblioteca MFC, mas como as bibliotecas MFC já estão completamente depuradas, isso pode não ser um problema.  
  
3. Crie seu próprio aplicativo com informações de depuração para os módulos selecionados apenas como descrito abaixo.  
  
   [Neste tópico](#BKMK_In_this_topic)  
  
###  <a name="BKMK_Building_an_MFC_app_with_debug_information_for_selected_modules"></a> Criando um aplicativo do MFC com informações de depuração para os módulos selecionados  
 Criar os módulos selecionados com as bibliotecas de depuração MFC permite usar a depuração e outros recursos nesses módulos. Esse procedimento utiliza os modos de depuração e liberação do makefile do Visual C++, necessitando das alterações descritas nas etapas a seguir (e também fazendo uma operação de "recompilar tudo” quando uma compilação de liberação completa for necessária).  
  
1. No Gerenciador de Soluções, selecione o projeto.  
  
2. Dos **modo de exibição** menu, selecione **páginas de propriedade**.  
  
3. Primeiro, você criará uma nova configuração de projeto.  
  
   1.  No  **\<projeto > páginas de propriedades** caixa de diálogo, clique o **Configuration Manager** botão.  
  
   2.  No [caixa de diálogo do Configuration Manager](http://msdn.microsoft.com/en-us/fa182dca-282e-4ae5-bf37-e155344ca18b), localize seu projeto na grade. No **Configuration** coluna, selecione  **\<novo... >**.  
  
   3.  No [caixa de diálogo nova configuração de projeto](http://msdn.microsoft.com/en-us/cca616dc-05a6-4fe3-bdc1-40c72a66f2be), digite um nome para a nova configuração, como "Depuração parcial", o **nome de configuração do projeto** caixa.  
  
   4.  No **copiar configurações de** , escolha **versão**.  
  
   5.  Clique em **Okey** para fechar o **nova configuração de projeto**caixa de diálogo.  
  
   6.  Fechar o **Configuration Manager** caixa de diálogo.  
  
4. Agora, você definirá opções para o projeto inteiro.  
  
   1.  No **páginas de propriedades** caixa de diálogo de **propriedades de configuração** pasta, selecione o **geral** categoria.  
  
   2.  Na grade de configurações de projeto, expanda **padrões de projeto** (se necessário).  
  
   3.  Sob **padrões de projeto**, localize **uso do MFC**. A configuração atual é exibida na coluna direita da grade. Clique na configuração atual e altere-o para **usar MFC em uma biblioteca estática**.  
  
   4.  No painel esquerdo do **páginas de propriedades** caixa de diálogo, abra o **C/C++** pasta e selecione **pré-processador**. Na grade de propriedades, localize **definições de pré-processador** e substitua "NDEBUG" por debug".  
  
   5.  No painel esquerdo do **páginas de propriedades** caixa de diálogo, abra o **vinculador** pasta e selecione o **entrada** categoria. Na grade de propriedades, localize **dependências adicionais**. No **dependências adicionais** configuração, digite "NAFXCWD. LIB"e"NAFXCWD."  
  
   6.  Clique em **Okey** para salvar as novas opções de compilação e fechar o **páginas de propriedade** caixa de diálogo.  
  
5. Dos **construir** menu, selecione **recompilar**. Isso remove todas as informações de depuração de seus módulos, mas não afeta a biblioteca MFC.  
  
6. Agora você deve adicionar as informações de depuração de volta para os módulos selecionados em seu aplicativo. Lembre-se de que você pode definir pontos de interrupção e executar outras funções de depurador apenas nos módulos que você compilou com informações de depuração. Para cada arquivo de projeto em que você quer incluir informações de depuração, execute as seguintes etapas:  
  
   1.  No Gerenciador de soluções, abra o **arquivos de origem** pasta localizada em seu projeto.  
  
   2.  Selecione o arquivo para o qual você quer definir informações de depuração.  
  
   3.  Dos **modo de exibição** menu, selecione **páginas de propriedade**.  
  
   4.  No **páginas de propriedades** caixa de diálogo a **definições de configuração** pasta, abra o **C/C++** , em seguida, selecione uma pasta a **geral** categoria.  
  
   5.  Na grade de propriedades, localize **formato informações de depuração.**  
  
   6.  Clique o **formato de informações de depuração** as configurações e selecione a opção desejada (normalmente **/ZI**) para obter informações de depuração.  
  
   7.  Se você estiver usando um aplicativo gerado por assistente ou se tiver cabeçalhos pré-compilado, será preciso desativar os cabeçalhos pré-compilados ou recompilá-los antes de compilar os outros módulos. Caso contrário, você receberá o aviso C4650 e mensagens de erro C2855. Você pode desligar cabeçalhos pré-compilados alterando a **criar/usar cabeçalho pré-compilado** definindo na  **\<projeto > propriedades** caixa de diálogo (**propriedades de configuração**  pasta, **C/C++** subpasta **cabeçalhos pré-compilados** categoria).  
  
7. Do **Build** menu, selecione **Build** para recompilar os arquivos de projeto que estão desatualizados.  
  
   Como alternativa à técnica descrita neste tópico, você pode usar um makefile externo para definir opções individuais para cada arquivo. Nesse caso, para vincular com as bibliotecas de depuração MFC, você deve definir a [Debug](http://msdn.microsoft.com/library/a9901568-4846-4731-a404-399d947e2e7a) sinalizador para cada módulo. Se você quiser usar bibliotecas de versão MFC, deverá definir NDEBUG. Para obter mais informações sobre como escrever makefiles externos, consulte a [referência de NMAKE](http://msdn.microsoft.com/library/0421104d-8b7b-4bf3-86c1-928d9b7c1a8c).  
  
   [Neste tópico](#BKMK_In_this_topic)  
  
## <a name="see-also"></a>Consulte também  
 [Depuração do Visual C++](../debugger/debugging-native-code.md)



