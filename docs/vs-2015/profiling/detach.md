---
title: Desanexar | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: d9d1b52c-7f28-467d-b1e0-512afc4e46c9
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1262e88055fceef0b2170c304c8ff646eea07205
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54793068"
---
# <a name="detach"></a>Detach
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A opção de **Desanexar** VSPerfCmd.exe desconecta o criador de perfil de todos os processos ou dos processos especificados se nenhum estiver especificado. A criação de perfil deve ter sido inicializada usando o método de amostragem.  
  
 A criação de perfil que foi iniciada com as opções **Iniciar** ou o **Anexar** pode ser desconectada com **Desanexar**. O criador de perfil pode ser reconectado usando os comandos **Anexar** subsequentes.  
  
 **Desanexar** não fecha o arquivo de dados de criação de perfil. Use a opção **Desligamento** para finalizar a criação de perfil e fechar o arquivo de dados.  
  
> [!NOTE]
>  Se a opção **Iniciar** foi especificada com a opção **Crosssession**, todas as chamadas para **VSPerfCmd /Attach** ou **VSPerfCmd /Detach** também devem especificar **Crosssession**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
VSPerfCmd.exe /Detach[:PIDs|ProcessNames]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `PIDs|ProcessNames`  
 `PID` - O identificador numérico do sistema de um ou mais processos.  
  
 `ProcessNames` - o nome do processo. Se estiver executando várias instâncias do processo nomeado, os resultados serão imprevisíveis.  
  
 Separe vários processos com vírgulas.  
  
 Se nenhum processo for especificado, o criador de perfil será desanexado de todos os processos com perfil.  
  
## <a name="valid-options"></a>Opções válidas  
 As opções **VSPerfCmd** a seguir podem ser combinadas com a opção **Anexar** em uma única linha de comando.  
  
 **Crosssession**  
 Permite aplicativos de criação de perfil em sessões que não seja a sessão de logon. Necessário se a opção **Iniciar** foi especificada com a opção **Crosssession**.  
  
## <a name="example"></a>Exemplo  
 Neste exemplo, o comando **Desanexar** suspende a criação de perfil e o comando **Desligamento** fecha o arquivo de dados do criador de perfil.  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe  
;REM Excercise the application  
VSPerfCmd.exe /Detach  
VSPerfCmd.exe /Shutdown  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)
