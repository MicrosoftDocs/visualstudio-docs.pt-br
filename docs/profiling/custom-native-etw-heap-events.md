---
title: Eventos de heap ETW nativo personalizado | Microsoft Docs
ms.custom: ''
ms.date: 02/24/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 668a6603-5082-4c78-98e6-f3dc871aa55b
author: mikejo5000
ms.author: mikejo
manager: douge
dev_langs:
- C++
ms.workload:
- cplusplus
ms.openlocfilehash: 98fc473a9459aa6d1a1d7c10be7b6f240a4ab7d0
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50744984"
---
# <a name="custom-native-etw-heap-events"></a>Eventos de heap de ETW nativos personalizados

O Visual Studio contém uma variedade de [ferramentas de criação de perfil e diagnóstico](../profiling/profiling-feature-tour.md), incluindo um criador de perfil de memória nativa.  Esse criador de perfil vincula [eventos ETW](/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-) do provedor de heap e fornece uma análise de como a memória está sendo alocada e utilizada.  Por padrão, essa ferramenta só pode analisar alocações feitas do heap padrão do Windows e todas as alocações fora desse heap nativo não serão exibidas.

Há vários casos em que você pode desejar usar seu próprio heap personalizado e evitar a sobrecarga de alocação do heap padrão.  Por exemplo, você poderá usar [VirtualAlloc](https://msdn.microsoft.com/library/windows/desktop/aa366887(v=vs.85).aspx) para alocar uma grande quantidade de memória no início do aplicativo ou do jogo e depois gerenciar seus próprios blocos nessa lista.  Nesse cenário, a ferramenta de criador de perfil de memória só verá essa alocação inicial e não o gerenciamento personalizado feito na parte de memória.  No entanto, ao usar o Provedor ETW de Heap Nativo Personalizado, é possível informar a ferramenta sobre as alocações que estão sendo feitas fora do heap padrão.

Por exemplo, em um projeto como o seguinte, em que `MemoryPool` é um heap personalizado, você verá apenas uma única alocação no heap do Windows:

```cpp
class Foo
{
public:
    int x, y;
};

...

// MemoryPool is a custom managed heap, which allocates 8192 bytes 
// on the standard Windows Heap named "Windows NT"
MemoryPool<Foo, 8192> mPool;

// the "allocate" method requests memory from the pool created above
// and is cast to an object of type Foo, shown above
Foo* pFoo1 = (Foo*)mPool.allocate();
Foo* pFoo2 = (Foo*)mPool.allocate();
Foo* pFoo3 = (Foo*)mPool.allocate();
```

Um instantâneo da ferramenta [Uso de Memória](../profiling/memory-usage.md) sem o acompanhamento de heap personalizado mostrará apenas a única alocação de byte 8192 e nenhuma das alocações personalizadas feitas pelo pool:

![Alocação de heap do Windows](media/heap-example-windows-heap.png)

Ao realizar as etapas a seguir, podemos usar essa mesma ferramenta para acompanhar o uso de memória em nosso heap personalizado.

## <a name="how-to-use"></a>Como usar

Essa biblioteca pode ser usada no C e C++ com facilidade.

1. Inclua o cabeçalho do provedor ETW de heap personalizado:

   ```cpp
   #include <VSCustomNativeHeapEtwProvider.h>
   ```

1. Adicione o decorador `__declspec(allocator)` a qualquer função no gerenciador de heap personalizado que retorna um ponteiro para a memória de heap recém-alocada.  Esse decorador permite que a ferramenta identifique corretamente o tipo da memória que está sendo retornado.  Por exemplo:

   ```cpp
   __declspec(allocator) void *MyMalloc(size_t size);
   ```
   
   > [!NOTE]
   > Esse decorador informará o compilador que essa função é uma chamada a um alocador.  Cada chamada à função gerará o endereço do site da chamada, o tamanho da instrução de chamada e a typeId do novo objeto para um novo símbolo `S_HEAPALLOCSITE`.  Quando uma pilha de chamadas for alocada, o Windows emitirá um evento ETW com essas informações.  A ferramenta de criador de perfil de memória percorre a pilha de chamadas em busca de uma correspondência de endereço de retorno com um símbolo `S_HEAPALLOCSITE` e as informações de typeId no símbolo são usadas para exibir o tipo de tempo de execução da alocação.
   >
   > Em resumo, isso significa que uma chamada parecida com `(B*)(A*)MyMalloc(sizeof(B))` será mostrada na ferramenta como sendo do tipo `B`, não `void` nem `A`.

1. Para o C++, crie o objeto `VSHeapTracker::CHeapTracker`, fornecendo um nome para o heap, que será mostrado na ferramenta de criação de perfil:

   ```cpp
   auto pHeapTracker = std::make_unique<VSHeapTracker::CHeapTracker>("MyCustomHeap");
   ```

   Se você estiver usando o C, use a função `OpenHeapTracker`.  Essa função retornará um identificador que será usado ao chamar outras funções de acompanhamento:
  
   ```C
   VSHeapTrackerHandle hHeapTracker = OpenHeapTracker("MyHeap");
   ```

1. Ao alocar a memória usando a função personalizada, chame o método `AllocateEvent` (C++) ou `VSHeapTrackerAllocateEvent` (C), passando o ponteiro para a memória e seu tamanho, para acompanhar a alocação:

   ```cpp
   pHeapTracker->AllocateEvent(memPtr, size);
   ```

   ou

   ```C
   VSHeapTrackerAllocateEvent(hHeapTracker, memPtr, size);
   ```

   > [!IMPORTANT]
   > Não se esqueça de marcar a função de alocador personalizada com o decorador `__declspec(allocator)` descrito anteriormente.

1. Ao desalocar a memória usando a função personalizada, chame a função `DeallocateEvent` (C++) ou `VSHeapTracerDeallocateEvent` (C), passando o ponteiro para a memória, para acompanhar a desalocação:

   ```cpp
   pHeapTracker->DeallocateEvent(memPtr);
   ```

   ou:

   ```C
   VSHeapTrackerDeallocateEvent(hHeapTracker, memPtr);
   ```

1. Ao realocar a memória usando a função personalizada, chame o método `ReallocateEvent` (C++) ou `VSHeapReallocateEvent` (C), passando um ponteiro para a nova memória, o tamanho da alocação e um ponteiro para a memória antiga:

   ```cpp
   pHeapTracker->ReallocateEvent(memPtrNew, size, memPtrOld);
   ```

   ou:

   ```C
   VSHeapTrackerReallocateEvent(hHeapTracker, memPtrNew, size, memPtrOld);
   ```

1. Por fim, para fechar e limpar o controlador de heap personalizado no C++, use o destruidor `CHeapTracker`, manualmente ou por meio de regras de escopo padrão ou a função `CloseHeapTracker` no C:

   ```cpp
   delete pHeapTracker;
   ```

   ou:

   ```C
   CloseHeapTracker(hHeapTracker);
   ```

## <a name="track-memory-usage"></a>Rastrear uso de memória
Com essas chamadas implementadas, o uso de heap personalizado agora pode ser acompanhado usando a ferramenta padrão **Uso de Memória** no Visual Studio.  Para obter mais informações sobre como usar essa ferramenta, consulte a documentação [Uso de memória](../profiling/memory-usage.md). Verifique se você habilitou a de criação de perfil de heap com instantâneos; caso contrário, você não verá o uso de heap personalizado exibido. 

![Habilitar a criação de perfil de heap](media/heap-enable-heap.png)

Para exibir o acompanhamento de heap personalizado, use o menu suspenso **Heap** localizado no canto superior direito da janela **Instantâneo** para alterar a exibição de *Heap NT* para seu próprio heap nomeado anteriormente.

![Seleção de heap](media/heap-example-custom-heap.png)

Usando o exemplo de código acima, com `MemoryPool` criando um objeto `VSHeapTracker::CHeapTracker` e nosso próprio método `allocate` agora chamando o método `AllocateEvent`, agora é possível ver o resultado da alocação personalizada, mostrando três instâncias que totalizam 24 bytes, todos do tipo `Foo`.

O heap padrão *Heap NT* tem a mesma aparência que anteriormente, com a adição de nosso objeto `CHeapTracker`.

![Heap NT com controlador](media/heap-example-windows-heap.png)

Assim como ocorre com o heap padrão do Windows, também é possível usar essa ferramenta para comparar instantâneos e procurar perdas e danos no heap personalizado, que é descrito na documentação principal [Uso de memória](../profiling/memory-usage.md).

> [!TIP]
> O Visual Studio também contém uma ferramenta **Uso de Memória** no conjunto de ferramentas **Criação de Perfil de Desempenho**, que é habilitada na opção de menu **Depurar** > **Criador de Perfil de Desempenho** ou na combinação de teclas **Alt**+**F2**.  Esse recurso não inclui o acompanhamento de heap e não exibirá o heap personalizado descrito aqui.  Somente a janela **Ferramentas de Diagnóstico**, que pode ser habilitada com o menu **Depurar** > **Windows** > **Mostrar Ferramentas de Diagnóstico** ou a combinação de teclas **Ctrl**+**Alt**+**F2**, contém essa funcionalidade.

## <a name="see-also"></a>Consulte também
[Introdução às ferramentas de criação de perfil](../profiling/profiling-feature-tour.md)  
[Uso de Memória](../profiling/memory-usage.md)
