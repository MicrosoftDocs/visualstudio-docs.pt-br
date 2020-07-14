---
title: Como definir um nome de thread em código nativo | Microsoft Docs
ms.date: 12/17/2018
ms.topic: how-to
dev_langs:
- C++
helpviewer_keywords:
- debugging [C++], threads
- SetThreadName function
- threading [Visual Studio], names
- thread names
- debugging [Visual Studio], threads
ms.assetid: c85d0968-9f22-4d69-87f4-acca2ae777b8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: ce6281a87900247cc54422a5175714d5f05b8e07
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349140"
---
# <a name="how-to-set-a-thread-name-in-native-code"></a>Como definir um nome de thread em código nativo
A nomeação de thread é possível em qualquer edição do Visual Studio. A nomenclatura de threads é útil para identificar threads de interesse na janela **threads** durante a depuração de um processo em execução. Ter threads com nomes reconhecidos também pode ser útil ao executar a depuração de post-mortem por meio da inspeção de despejo de memória e ao analisar capturas de desempenho usando várias ferramentas.

## <a name="ways-to-set-a-thread-name"></a>Maneiras de definir um nome de thread

Há duas maneiras de definir um nome de thread. A primeira é por meio da função [SetThreadDescription](/windows/desktop/api/processthreadsapi/nf-processthreadsapi-setthreaddescription) . A segunda é lançar uma exceção específica enquanto o depurador do Visual Studio é anexado ao processo. Cada abordagem tem benefícios e limitações. O uso do `SetThreadDescription` tem suporte a partir do Windows 10, versão 1607 ou Windows Server 2016.

Vale a pena observar que _ambas as_ abordagens podem ser usadas juntas, se desejado, já que os mecanismos pelos quais eles trabalham são independentes uns dos outros.

### <a name="set-a-thread-name-by-using-setthreaddescription"></a>Definir um nome de thread usando`SetThreadDescription`

Benefícios:
* Os nomes de thread são visíveis durante a depuração no Visual Studio, independentemente de o depurador ter sido anexado ou não ao processo no momento em que SetThreadDescription é invocado.
* Os nomes de thread são visíveis ao executar a depuração de post-mortem carregando um despejo de memória no Visual Studio.
* Os nomes de thread também são visíveis ao usar outras ferramentas, como o depurador do [windbg](/windows-hardware/drivers/debugger/debugger-download-tools) e o analisador de desempenho do [analisador de desempenho do Windows](/windows-hardware/test/wpt/windows-performance-analyzer) .

Restrições:
* Os nomes de thread só são visíveis no Visual Studio 2017 versão 15,6 e versões posteriores.
* Quando o post-mortem a depuração de um arquivo de despejo de memória, os nomes de thread só ficam visíveis se a falha foi criada no Windows 10 versão 1607, no Windows Server 2016 ou em versões posteriores do Windows.

*Exemplo:*

```C++
#include <windows.h>
#include <processthreadsapi.h>

int main()
{
    HRESULT r;
    r = SetThreadDescription(
        GetCurrentThread(),
        L"ThisIsMyThreadName!"
    );

    return 0;
}
```

### <a name="set-a-thread-name-by-throwing-an-exception"></a>Definir um nome de thread lançando uma exceção

Outra maneira de definir um nome de thread em seu programa é comunicar o nome de thread desejado para o depurador do Visual Studio lançando uma exceção especialmente configurada.

Benefícios:
* Funciona em todas as versões do Visual Studio.

Restrições:
* Só funcionará se o depurador estiver anexado no momento em que o método baseado em exceção for usado.
* Os nomes de thread definidos usando esse método não estarão disponíveis em despejos ou ferramentas de análise de desempenho.

*Exemplo:*

A `SetThreadName` função mostrada abaixo demonstra essa abordagem baseada em exceção. Observe que o nome do thread será copiado automaticamente para o thread, para que a memória do `threadName` parâmetro possa ser liberada depois que a `SetThreadName` chamada for concluída.

```C++
//
// Usage: SetThreadName ((DWORD)-1, "MainThread");
//
#include <windows.h>
const DWORD MS_VC_EXCEPTION = 0x406D1388;
#pragma pack(push,8)
typedef struct tagTHREADNAME_INFO
{
    DWORD dwType; // Must be 0x1000.
    LPCSTR szName; // Pointer to name (in user addr space).
    DWORD dwThreadID; // Thread ID (-1=caller thread).
    DWORD dwFlags; // Reserved for future use, must be zero.
} THREADNAME_INFO;
#pragma pack(pop)
void SetThreadName(DWORD dwThreadID, const char* threadName) {
    THREADNAME_INFO info;
    info.dwType = 0x1000;
    info.szName = threadName;
    info.dwThreadID = dwThreadID;
    info.dwFlags = 0;
#pragma warning(push)
#pragma warning(disable: 6320 6322)
    __try{
        RaiseException(MS_VC_EXCEPTION, 0, sizeof(info) / sizeof(ULONG_PTR), (ULONG_PTR*)&info);
    }
    __except (EXCEPTION_EXECUTE_HANDLER){
    }
#pragma warning(pop)
}
```

## <a name="see-also"></a>Veja também
- [Depurar aplicativos multithread](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)
- [Como definir um nome de thread no código gerenciado](../debugger/how-to-set-a-thread-name-in-managed-code.md)
