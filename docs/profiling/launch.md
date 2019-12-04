---
title: Inicializar | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f81bde5c-3394-4b79-a315-c2f6491689b3
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 9834c10c58fb343de0707fa0b805586a6cdebcb3
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2019
ms.locfileid: "74778603"
---
# <a name="launch"></a>Inicie o
A opção **Inicializar** inicia o criador de perfil usando o método de amostragem e também inicia o aplicativo especificado.

 Para usar a opção **Inicializar**, você deve especificar o método de **Amostragem** na opção **Iniciar**.

## <a name="syntax"></a>Sintaxe

```cmd
VSPerfCmd.exe /Launch:AppName [Options]
```

#### <a name="parameters"></a>Parâmetros
 `AppName` O nome do aplicativo a ser iniciado. Há suporte para caminhos completos e parciais do diretório atual.

## <a name="valid-options"></a>Opções válidas
 As seguintes opções de VSPerfCmd podem ser combinadas com a opção **Inicializar** em uma única linha de comando.

 **Iniciar:** `Method` Inicializa a sessão do criador de perfil de linha de comando e define o método de criação de perfil especificado.

 **GlobalOn** e **GlobalOff** Retoma (**GlobalOn**) ou pausa (**GlobalOff**) a criação de perfil, mas não encerra a sessão de criação de perfil.

 **Processo:** `PID` e **ProcessOff**:`PID` retoma a criação de perfil (**processize**) ou pausa (**ProcessOff**) para o processo especificado.

 **TargetCLR** Especifica a versão do CLR (Common Language Runtime) do .NET Framework a ser analisada quando mais de uma versão for carregada em uma sessão de criação de perfil. Por padrão, a primeira versão carregada é analisada.

## <a name="exclusive-options"></a>Opções Exclusivas
 As opções a seguir só podem ser usadas com a opção **Inicializar**.

 **TargetCLR** Inicia o aplicativo de linha de comando especificado em uma nova janela.

 **Args:** `ArgList` especifica a lista de argumentos a serem passados para o aplicativo.

 **LineOff** Desabilita a coleta de dados de criação de perfil no nível de linha.

## <a name="sampling-options"></a>Opções de amostragem
 Uma das seguintes opções de intervalo de amostragem pode ser especificada na linha de comando **Inicializar**. O intervalo de amostragem padrão é 10.000.000 ciclos de relógio do processador.

 **Timer**[ **:** `Cycles`]**PF**[ **:** `Events`]**Sys**[ **:** `Events`]**Contador**[ **:** `Name`,`Reload`,`FriendlyName`]**GC**[:**alocação**&#124;**tempo de vida**] Especifica o número e o tipo de intervalo de amostragem.

- **Temporizador** – exemplifica cada ciclo de relógio do processador `Cycles` não interrompido. Se `Cycles` não for especificado, os 10.000.000 ciclos serão usados.

- **PF** – exemplifica cada `Events` falha de página. Se `Events` não for especificado, 10 falhas de página.

- **Sys** – exemplifica cada `Events` chamadas para o sistema operacional. Se `Events` não for especificado, 10 chamadas do sistema serão usadas.

- **Contador** – exemplifica cada número `Reload` do contador de desempenho de CPU especificado por `Name`. Opcionalmente, `FriendlyName` pode especificar uma cadeia de caracteres para usar como o cabeçalho de coluna nos relatórios do criador de perfil.

- **GC** – Coleta dados da memória de .NET. Por padrão (**alocação**), os dados são coletados em todos os eventos de alocação da memória. Quando o parâmetro **tempo de vida** é especificado, os dados também são coletados em todos os eventos de coleta de lixo.

## <a name="example"></a>Exemplo
 Este exemplo demonstra o uso de **Inicializar** para iniciar um aplicativo.

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe
```

## <a name="see-also"></a>Consulte também
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [Aplicativos Autônomos de Perfil](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [Profile services (Serviços de perfil)](../profiling/command-line-profiling-of-services.md)
