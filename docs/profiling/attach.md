---
title: Anexar | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 79614283-6733-4592-a53a-d428052271ad
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 482b3e80bce796910860cb7eab1e5a0066854238
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329871"
---
# <a name="attach"></a>Anexar
A opção *VSPerfCmd.exe* **Attach** inicia a criação de perfil de exemplo do processo em execução especificado pela ID do processo (PID).

 Para usar a opção **Anexar**, você deve especificar o método de **exemplo** na opção de início.

> [!NOTE]
> Se a opção **Iniciar** foi especificada com a opção **Crosssession**, todas as chamadas para **VSPerfCmd /Attach** ou **VSPerfCmd /Detach** também devem especificar **Crosssession**.

## <a name="syntax"></a>Sintaxe

```cmd
VSPerfCmd.exe /Attach:ProcessID [Options]
```

#### <a name="parameters"></a>Parâmetros
 `ProcessID` O PID (identificador do processo) do processo em execução. A PID de um processo em execução é listada na guia Processos do Gerenciador de Tarefas do Windows.

## <a name="valid-options"></a>Opções válidas
 As seguintes opções **VSPerfCmd** podem ser combinadas com a opção **Anexar** em uma única linha de comando.

 **Crosssession** Habilita aplicativos de criação de perfil em sessões que não seja a sessão de logon. Necessário se a opção **Iniciar** foi especificada com a opção **Crosssession**.

 **Início:** `Method` Inicializa a sessão do criador de perfil de linha de comando e define o método de criação de perfil especificado.

 **TargetCLR** Especifica a versão do CLR (Common Language Runtime) do .NET Framework a ser analisada quando mais de uma versão for carregada em uma sessão de criação de perfil. Por padrão, a primeira versão carregada é analisada.

 **GlobalOn GlobalOff** Retoma (**GlobalOn**) ou pausa (**GlobalOff**) a criação de perfil, mas não encerra a sessão de criação de perfil.

 **Processo:** `PID` **ProcessOff:** `PID` Retoma a criação de perfil (**processize**) ou pausas (**ProcessOff**) para o processo especificado.

## <a name="interval-options"></a>Opções de intervalo
 Uma das seguintes opções de intervalo de amostragem pode ser especificada na linha de comando Anexar. O intervalo de amostragem padrão é 10.000.000 ciclos de relógio do processador.

 **Timer**[**:** `Cycles` ]**PF**[**:** `Events` ]**Sys**[<strong>:</strong>Events]**contador**[**:** `Name` , `Reload` , `FriendlyName` ] Especifica o número e o tipo do intervalo de amostragem.

- **Temporizador** – exemplifica cada `Cycles` ciclo de relógio do processador. Se `Cycles` não for especificado, os 10.000.000 ciclos serão usados.

- **PF** – exemplifica cada `Events` falha de página. Se `Events` não for especificado, 10 falhas de página serão usadas.

- **Sys** – exemplifica cada `Events` chamadas para o sistema operacional. Se `Events` não for especificado, 10 chamadas do sistema serão usadas.

- **Contador** – exemplifica cada número `Reload` do contador de desempenho de CPU especificado por `Name`. Opcionalmente, `FriendlyName` pode especificar uma cadeia de caracteres para usar como o cabeçalho de coluna nos relatórios do criador de perfil.

## <a name="example"></a>Exemplo
 Este exemplo demonstra como anexar a uma instância em execução de um aplicativo com a ID de processo 12345.

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Attach:12345
```

## <a name="see-also"></a>Veja também
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [Aplicativos Autônomos de Perfil](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [Profile services (Serviços de perfil)](../profiling/command-line-profiling-of-services.md)
