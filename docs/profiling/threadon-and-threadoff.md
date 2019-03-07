---
title: ThreadOn e ThreadOff | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 5cd5a695-0a14-484a-8952-ed47e13d8e92
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2516ff5597151e65276b0fcb2bef5bb81c929cd3
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56632713"
---
# <a name="threadon-and-threadoff"></a>ThreadOn e ThreadOff
Os subcomandos *ThreadOff* e **ThreadOn** do **VSPerfCmd.exe** só estão disponíveis em sessões de criação de perfil de linha de comando que usam o método de instrumentação. **ThreadOff** e **ThreadOn** pausam e retomam a criação de perfil para o thread especificado. O **ThreadOff** para a criação de perfil do thread e o **ThreadOn** inicia a criação de perfil do thread.

 Na maioria dos casos, você especifica **ThreadOn** ou **ThreadOff** como a única opção em uma linha de comando *VSPerfCmd.exe,* mas eles também podem ser combinados com os subcomandos **GlobalOn**, **GlobalOff**, **ProcessOn** e **ProcessOff**.

 Os subcomandos **ThreadOn** e **ThreadOff** interagem com os subcomandos **GlobalOn** e **GlobalOff**, que controlam a coleta de dados para todos os processos em uma sessão de criação de perfil de linha de comando, e os subcomandos **ProcessOn** e **ProcessOff**, que controlam a coleta de dados para um processo especificado.

 Os subcomandos **ThreadOff** e **ThreadOn** também afetam a contagem de início/parada de thread que é manipulada por funções da API do criador de perfil.

- O **ThreadOff** define imediatamente a contagem de início/parada de thread para 0 e, portanto, faz uma pausa de criação de perfil.

- O **ThreadOn** define imediatamente a contagem de início/parada de thread para 1 e, portanto, retoma de criação de perfil.

  Confira [APIs de ferramentas de criação de perfil](../profiling/profiling-tools-apis.md) para obter mais informações.

## <a name="syntax"></a>Sintaxe

```cmd
VSPerfCmd.exe /{ThreadOff|ThreadOn}:TID [Options]

```

#### <a name="parameters"></a>Parâmetros
 `TID` O identificador inteiro do thread a ser iniciado ou interrompido.

## <a name="valid-options"></a>Opções válidas
 O **ThreadOn** e **ThreadOff** podem ser especificados em linhas de comando que também contêm os subcomandos a seguir.

 **Iniciar:** `Method` Inicializa a sessão de criação de perfil de linha de comando e define o método de criação de perfil especificado.

 **GlobalOff**&#124;**GlobalOn** Interrompe ou inicia a criação de perfil para todos os processos em uma sessão de criação de perfil de linha de comando.

 {**ProcessOff**&#124;**ProcessOn**}**:**`TID` Interrompe ou inicia a criação de perfil para o processo especificado.

## <a name="example"></a>Exemplo
 Neste exemplo, o subcomando **ThreadOff** é usado para interromper a coleta de dados de criação de perfil para coletar apenas os dados de inicialização do aplicativo.

```cmd
; Initialize the profiler.
VSPerfCmd.exe /Start:Trace /Output:Instrument.vsp
; Start the instrumented application.
; Stop profiling the thread after startup.
VSPerfCmd.exe /ThreadOff:12345
; Shut down the target application.
; Close the profiler.
VSPerfCmd /Shutdown

```

## <a name="see-also"></a>Consulte também
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [Aplicativos Autônomos de Perfil](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [Profile services (Serviços de perfil)](../profiling/command-line-profiling-of-services.md)